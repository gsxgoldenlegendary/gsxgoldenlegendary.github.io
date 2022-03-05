---
title: Huffman Compressor and Decompressor
date: 2021-11-29 22:13:04
tags: Data Structure
categories: Computer Science
---

# 数据结构 Huffman 压缩/解压器大作业 

## 项目环境

- 设备：Windows Surface Pro 7 Model 1866 i7
- 操作系统：Windows 11 Insider Preview 10.0.22504.1010 (rs_prerelease)
- 集成开发环境：JetBrain CLion 2021.2.1
- 编译器：MinGW 7.3.0 64-bit

<!--more-->

## Compress.h

```C++
//
// Created by administrator Guo on 23/11/2021 15:46.
//

#ifndef DSHW2_V1_COMPRESS_H
#define DSHW2_V1_COMPRESS_H
#include "main.h"

class Compress {
private:
    std::vector<HTNode> Huffman_tree;
    unsigned bit_of_unit;
    unsigned fork_of_tree;
    unsigned bit_of_move;
    unsigned long long read_buffer ;
    unsigned char read_buffer_temp ;
    unsigned bit_of_read_buffer ;
    unsigned read_complement ;
    unsigned long long write_buffer ;
    unsigned bit_of_write_buffer ;
    unsigned char write_buffer_temp ;
    std::string source_file_name;
    std::string compress_file_name;
    std::ifstream file_reader;
    std::ifstream file_reader2;
    std::ofstream file_writer;
    std::ofstream tree_printer;
public:
    Compress(unsigned ,unsigned ,const std::string&,const std::string&);
    void open_files();
    void get_leaves();
    void complete_leaves();
    void struct_tree();
    void encode(unsigned );
    void encode_tree();
    void print(unsigned ,unsigned );
    void print_tree();
    void write_tree();
    void write_content();
    void close_files();
};


#endif //DSHW2_V1_COMPRESS_H
```



## Compress.cpp

```C++
//
// Created by administrator Guo on 23/11/2021 15:46.
//

#include "Compress.h"

Compress::Compress(unsigned bit_of_unit,unsigned fork_of_tree,const std::string& source_file_name,const std::string&  compress_file_name){
    Compress::bit_of_unit=bit_of_unit;
    Compress::fork_of_tree=fork_of_tree;
    bit_of_move = [fork_of_tree]() -> unsigned {
        if (fork_of_tree == 2)return 1;
        else if (3 <= fork_of_tree && fork_of_tree < 8)return 2;
        else if (8 <= fork_of_tree && fork_of_tree < 16)
            return 3;
        else return 4;
    }();
    read_buffer=0 ;
    read_buffer_temp=0 ;
    bit_of_read_buffer=0 ;
    read_complement=0 ;
    write_buffer=0;
    write_buffer_temp=0;
    bit_of_write_buffer=0;
    Compress::source_file_name=source_file_name;
    Compress::compress_file_name=compress_file_name;
    auto zeroth_HTNode = new HTNode();
    Huffman_tree.push_back(*zeroth_HTNode);
    tree_printer=std::ofstream ("tree.txt");
}

void Compress::open_files() {
    file_reader=std::ifstream (source_file_name, std::ios::binary);
    file_reader2=std::ifstream (source_file_name,std::ios::binary);
    file_writer=std::ofstream (compress_file_name,std::ios::binary);
    if(!file_reader.is_open()||!file_reader2.is_open()||!file_writer){
        std::cout<<"Fail in opening files!\n";
        exit(0);
    }
}

void Compress::get_leaves() {
    for (; file_reader.peek() != EOF || bit_of_read_buffer > 0;) {
        if (bit_of_read_buffer < bit_of_unit) {
            if (file_reader.peek() != EOF) {
                file_reader.read(reinterpret_cast<char *>(&read_buffer_temp), sizeof(char));
                read_buffer = (read_buffer << 8) + read_buffer_temp;
                bit_of_read_buffer += 8;
            } else {
                read_complement = bit_of_unit - bit_of_read_buffer;
                read_buffer = read_buffer << read_complement;
                bit_of_read_buffer = bit_of_unit;
            }
        } else {
            auto number = read_buffer >> (bit_of_read_buffer - bit_of_unit);
            bit_of_read_buffer -= bit_of_unit;
            read_buffer &= ((unsigned long long)1 << bit_of_read_buffer) - 1;
            auto iter = std::find(Huffman_tree.begin() + 1, Huffman_tree.end(), number);
            if (iter != Huffman_tree.end()) {
                ++iter->weight;
                if(iter->weight==INT32_MAX){
                    std::cout<<"To big to compress!\n";
                    exit(0);
                }
            } else {
                auto temp_HTNode = new HTNode();
                temp_HTNode->number = number;
                temp_HTNode->weight = 1;
                Huffman_tree.push_back(*temp_HTNode);
            }
        }
    }
}

void Compress::complete_leaves() {
    for (; (Huffman_tree.size() - 2) % (fork_of_tree - 1) != 0;) {
        auto temp_HTNode = new HTNode();
        Huffman_tree.push_back(*temp_HTNode);
    }
}

void Compress::struct_tree() {
    auto cycle_number = (Huffman_tree.size() - 2) / (fork_of_tree - 1);
    for (unsigned i = 0; i < cycle_number; ++i) {
        auto temp_HTNode = new HTNode();
        for (unsigned j = 0; j < fork_of_tree; ++j) {
            unsigned long long temp_weight;
            auto length = Huffman_tree.size();
            unsigned k = 1;
            for (; Huffman_tree[k].is_in_tree; ++k) {}
            temp_weight = Huffman_tree[k].weight;
            auto min_position = k;
            for (; k < length; ++k) {
                if (!Huffman_tree[k].is_in_tree && Huffman_tree[k].weight < temp_weight) {
                    temp_weight = Huffman_tree[k].weight;
                    min_position = k;
                }
            }
            Huffman_tree[min_position].parent = length;
            Huffman_tree[min_position].is_in_tree = true;
            temp_HTNode->child[j] = min_position;
            temp_HTNode->weight += Huffman_tree[min_position].weight;
        }
        Huffman_tree.push_back(*temp_HTNode);
    }
}

void Compress::encode(unsigned position) {
    for (int i = 0; i < fork_of_tree; ++i) {
        if (Huffman_tree[position].child[i]) {
            Huffman_tree[Huffman_tree[position].child[i]].code = (Huffman_tree[position].code << bit_of_move) + i;
            Huffman_tree[Huffman_tree[position].child[i]].bit_of_code = Huffman_tree[position].bit_of_code + bit_of_move;
            encode(Huffman_tree[position].child[i]);
        }
    }
}
void Compress::encode_tree() {
    Huffman_tree[Huffman_tree.size() - 1].code = 1;
    Huffman_tree[Huffman_tree.size() - 1].bit_of_code = bit_of_move;
    encode(Huffman_tree.size() - 1);
}

void Compress::print_tree() {
    print(Huffman_tree.size()-1,0);
    tree_printer.close();
}

void Compress::print(unsigned position, unsigned depth) {
    for (int i = 0; i < depth; ++i) {
        tree_printer << '\t';
    }
    tree_printer << Huffman_tree[position].code;
    int j = 0;
    for (; Huffman_tree[position].child[j] == 0 && j < fork_of_tree; ++j) {}
    if (j == fork_of_tree) {
        tree_printer << '\t' << Huffman_tree[position].number;
    }
    tree_printer << '\n';
    for (int i = 0; i < fork_of_tree; ++i) {
        if (Huffman_tree[position].child[i] != 0)
            print(Huffman_tree[position].child[i], depth + 1);
    }
}

void Compress::write_tree() {
    auto size = Huffman_tree.size() - 1;
    file_writer.write(reinterpret_cast<char *>(&bit_of_unit), sizeof bit_of_unit);
    file_writer.write(reinterpret_cast<char *>(&bit_of_move), sizeof bit_of_move);
    file_writer.write(reinterpret_cast<char *>(&fork_of_tree), sizeof fork_of_tree);
    file_writer.write(reinterpret_cast<char *>(&read_complement), sizeof read_complement);
    file_writer.write(reinterpret_cast<char *>(&size), sizeof size);
    for (auto iter = Huffman_tree.begin() + 1; iter != Huffman_tree.end(); ++iter) {
        file_writer.write(reinterpret_cast<char *>(&iter->number), sizeof iter->number);
        file_writer.write(reinterpret_cast<char *>(&iter->parent), sizeof iter->parent);
        for (int j = 0; j < fork_of_tree; ++j) {
            file_writer.write(reinterpret_cast<char *>(&iter->child[j]), sizeof iter->child[j]);
        }
    }
}

void Compress::write_content() {
    for (; file_reader2.peek() != EOF || bit_of_read_buffer > 0 || bit_of_write_buffer > 0;) {
        if (file_reader2.peek() == EOF && bit_of_read_buffer == 0 && bit_of_write_buffer < 8) {
            write_buffer = (write_buffer << (8 - bit_of_write_buffer));
            bit_of_write_buffer = 8;
        } else if (bit_of_write_buffer >= 8) {
            write_buffer_temp = write_buffer >> (bit_of_write_buffer - 8);
            bit_of_write_buffer -= 8;
            write_buffer &= ((unsigned long long)1<< bit_of_write_buffer) - 1;
            file_writer.write(reinterpret_cast<char *>(&write_buffer_temp), sizeof(char));
        } else if (bit_of_read_buffer < bit_of_unit) {
            if (file_reader2.peek() != EOF) {
                file_reader2.read(reinterpret_cast<char *>(&read_buffer_temp), sizeof(char));
                read_buffer = (read_buffer << 8) + read_buffer_temp;
                bit_of_read_buffer += 8;
            } else {
                read_complement = bit_of_unit - bit_of_read_buffer;
                read_buffer = read_buffer << read_complement;
                bit_of_read_buffer = bit_of_unit;
            }
        } else {
            auto number = read_buffer >> (bit_of_read_buffer - bit_of_unit);
            bit_of_read_buffer -= bit_of_unit;
            read_buffer &= ((unsigned long long) 1 << bit_of_read_buffer) - 1;
            auto iter = std::find(Huffman_tree.begin() + 1, Huffman_tree.end(), number);
            write_buffer = (write_buffer << iter->bit_of_code) + iter->code;
            bit_of_write_buffer += iter->bit_of_code;
        }
    }
}

void Compress::close_files() {
    file_reader.close();
    file_writer.close();
    file_reader2.close();
    std::cout<<"Compress successfully!\n";
}
```



## Decompress.h

```C++
//
// Created by administrator Guo on 23/11/2021 18:30.
//

#ifndef DSHW2_V1_DECOMPRESS_H
#define DSHW2_V1_DECOMPRESS_H

#include "main.h"
class Decompress {
private:
    std::vector<HTNode> Huffman_tree2;
    std::ifstream file_reader3;
    std::ofstream file_writer2;
    unsigned bit_of_unit2;
    unsigned fork_of_tree2;
    unsigned bit_of_move2;
    unsigned read_complement2;
    unsigned long long size2;
    unsigned long long read_buffer ;
    unsigned char read_buffer_temp ;
    unsigned bit_of_read_buffer ;
    unsigned long long write_buffer ;
    unsigned bit_of_write_buffer ;
    unsigned char write_buffer_temp ;
    std::string decompress_file_name;
    std::string compress_file_name;
public:
    Decompress(const std::string&,const std::string&);
    void open_files();
    void read_tree();
    void write_content();
    void close_files();
};


#endif //DSHW2_V1_DECOMPRESS_H
```



## Decompress.cpp

```C++
//
// Created by administrator Guo on 23/11/2021 18:30.
//

#include "Decompress.h"

Decompress::Decompress(const std::string&compress_file_name,const std::string&decompress_file_name) {
    read_buffer=0 ;
    read_buffer_temp=0 ;
    bit_of_read_buffer=0 ;
    read_complement2=0 ;
    write_buffer=0;
    write_buffer_temp=0;
    bit_of_write_buffer=0;
    bit_of_unit2=0;
    fork_of_tree2=0;
    bit_of_move2=0;
    size2=0;
    Decompress::compress_file_name=compress_file_name;
    Decompress::decompress_file_name=decompress_file_name;
    auto zeroth_HTNode2 = new HTNode();
    Huffman_tree2.push_back(*zeroth_HTNode2);
}

void Decompress::close_files() {
    file_reader3.close();
    file_writer2.close();
    std::cout<<"Decompress successfully!\n";
}

void Decompress::write_content() {
    unsigned long long position = Huffman_tree2.size() - 1;
    bool is_new_number = true;
    for (; file_reader3.peek() != EOF || bit_of_read_buffer > 0 || bit_of_write_buffer > read_complement2;) {
        if (bit_of_write_buffer >= read_complement2 + 8) {
            write_buffer_temp = write_buffer >> (bit_of_write_buffer - 8);
            bit_of_write_buffer -= 8;
            write_buffer &= ((unsigned long long)1 << bit_of_write_buffer) - 1;
            file_writer2.write(reinterpret_cast<char *>(&write_buffer_temp), sizeof write_buffer_temp);
        } else if (bit_of_read_buffer == 0) {
            file_reader3.read(reinterpret_cast<char *>(&read_buffer_temp), sizeof read_buffer_temp);
            bit_of_read_buffer += 8;
            read_buffer=(read_buffer<<8)+read_buffer_temp;
        } else {
            if (is_new_number) {
                if (read_buffer >> (bit_of_read_buffer - bit_of_move2) != 0) {
                    position = Huffman_tree2.size() - 1;
                    is_new_number = false;
                }
                bit_of_read_buffer -= bit_of_move2;
                read_buffer &= ((unsigned long long) 1 << bit_of_read_buffer) - 1;
            } else {
                int k = 0;
                for (; Huffman_tree2[position].child[k] == 0 && k < fork_of_tree2; ++k) {}
                if (k == fork_of_tree2) {
                    write_buffer = (write_buffer << bit_of_unit2) + Huffman_tree2[position].number;
                    bit_of_write_buffer += bit_of_unit2;
                    is_new_number = true;
                } else {
                    position = Huffman_tree2[position].child[read_buffer >> (bit_of_read_buffer - bit_of_move2)];
                    bit_of_read_buffer -= bit_of_move2;
                    read_buffer &= ((unsigned long long) 1 << bit_of_read_buffer) - 1;
                }
            }
        }
    }
}

void Decompress::read_tree() {
    file_reader3.read(reinterpret_cast<char *>(&bit_of_unit2), sizeof bit_of_unit2);
    file_reader3.read(reinterpret_cast<char *>(&bit_of_move2), sizeof bit_of_move2);
    file_reader3.read(reinterpret_cast<char *>(&fork_of_tree2), sizeof fork_of_tree2);
    file_reader3.read(reinterpret_cast<char *>(&read_complement2), sizeof read_complement2);
    file_reader3.read(reinterpret_cast<char *>(&size2), sizeof size2);
    for (int i = 0; i < size2; ++i) {
        auto temp_HTNode = new HTNode();
        file_reader3.read(reinterpret_cast<char *>(&temp_HTNode->number), sizeof temp_HTNode->number);
        file_reader3.read(reinterpret_cast<char *>(&temp_HTNode->parent), sizeof temp_HTNode->parent);
        for (int j = 0; j < fork_of_tree2; ++j) {
            file_reader3.read(reinterpret_cast<char *>(&temp_HTNode->child[j]), sizeof temp_HTNode->child[j]);
        }
        Huffman_tree2.push_back(*temp_HTNode);
    }
}

void Decompress::open_files() {
    file_reader3=std::ifstream (compress_file_name, std::ios::binary);
    file_writer2=std::ofstream (decompress_file_name, std::ios::binary);
    if(!file_reader3.is_open()||!file_writer2.is_open()){
        std::cout<<"Fail in opening files!\n";
        exit(0);
    }
}
```



## main.h

```C++
//
// Created by administrator Guo on 23/11/2021 15:46.
//

#ifndef DSHW2_V1_MAIN_H
#define DSHW2_V1_MAIN_H
#include "iostream"
#include "fstream"
#include "string"
#include "vector"
#include "algorithm"
struct HTNode {
    unsigned long long number;
    unsigned code;
    unsigned bit_of_code;
    unsigned long long weight;
    unsigned child[16];
    unsigned parent;
    bool is_in_tree;

    bool operator==(const unsigned long long i) const {
        return number == i;
    }
};
#endif //DSHW2_V1_MAIN_H
```



## main.cpp

```C++
//
// Created by administrator Guo on 23/11/2021 15:46.
//
#include "Compress.h"
#include "Decompress.h"
//It's main function, the main part of the programme.
int main() {
    unsigned bit_of_unit;
    unsigned fork_of_tree;
    std::string operation;
    std::cout<<"Wait for command:\n";
    std::cin>>operation;
    std::string source_file_name;
    std::string compress_file_name;
    std::string decompress_file_name;
    if(operation=="compress"||operation=="c"){
        std::cout<<"Bits of unit:\n";
        std::cin>>bit_of_unit;
        if(!(bit_of_unit%2==0&&4<=bit_of_unit&&bit_of_unit<=32)){
            std::cout<<"Unsupported bit of unit!\n";
            exit(0);
        }
        std::cout<<"Forks of tree:\n";
        std::cin>>fork_of_tree;
        if(!(2<=fork_of_tree&&fork_of_tree<=16)){
            std::cout<<"Unsupported fork of tree!\n";
            exit(0);
        }
        std::cout<<"Source file name:\n";
        std::cin>>source_file_name;
        std::cout<<"Compress file name:\n";
        std::cin>>compress_file_name;
        Compress compress(bit_of_unit,fork_of_tree,source_file_name,compress_file_name);
        compress.open_files();
        compress.get_leaves();
        compress.complete_leaves();
        compress.struct_tree();
        compress.encode_tree();
        compress.print_tree();
        compress.write_tree();
        compress.write_content();
        compress.close_files();
    }else if(operation=="decompress"||operation=="d"){
        std::cout<<"Compress file name:\n";
        std::cin>>compress_file_name;
        std::cout<<"Decompress file name:\n";
        std::cin>>decompress_file_name;
        Decompress decompress(compress_file_name,decompress_file_name);
        decompress.open_files();
        decompress.read_tree();
        decompress.write_content();
        decompress.close_files();
    }else{
        std::cout<<"Illegal operation!\n";
    }
    //It's a good habit.
    return 0;
}
```





