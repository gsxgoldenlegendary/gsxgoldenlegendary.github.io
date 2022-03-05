---

title: Soduko by Java
date: 2021-10-20 18:59:11
tags: Java
categories: Computer Science
---

# 实现结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021061314460359.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81MjA3NTIxOQ==,size_16,color_FFFFFF,t_70#pic_center)

<!--more-->

# 功能介绍

```bash
Welcome to my sudoku world!
usage:
1.Enter "exit" or press "Exit" to quit programme in 5 minutes.
2.Enter "print" or press "Print" to print current sudoku state. 0 filled for vacancy. 
3.press "Input" to input a soduku. Cement format shown then.
4.Enter or press "generate" to generate a sudoku which has 17 non-zero at least numbers at random.
5.Enter "DFS" or press "Solve(DFS)" to solve surrent sudoku by depth-first search method.
6.Enter "IDDFS" or press "Solve(IDDFS)" to solve surrent sudoku by iterative deepening depth-first search method.
7.Enter "A*" or press "Solve(A*)" to solve surrent sudoku by heuristically search method.
8.Enter "put x y z" or choose number by mouse to put z into x row y column.Array counted from 0. 
9.Enter "hint" or press "Hint" to get a hint cell.
10.Press "Save" to save current sudoku. Operation following shown then.
11.Enter "show" or press "Show" to view saved game. Operation following shown then.
12.Enter "usage" or press "Usage" to get usage.
13.Enter "BT" or press "BT" to solve surrent sudoku by back-tracking method.

Error list:
Error1:syntax error
Error2:data range exceed
Error3:illegal location
Error4:illegal, the line x column y has the same number
Error5:there is already a number in this position
Error6:No Answer
Error7:file existed

Have fun!
```




# 组织架构

```bash
sudoku
	.vscode
		settings.json
	lib					//javafx 11
		javafx-swt.jar
		javafx.base.jar
		javafx.controls.jar
		javafx.fxml.jar
		javafx.graphics.jar
		javafx.properties
		javafx.swing.jar
		javafx.web.jar
		src.zip
	src
		backEnd
			data
				cache.txt
				Data.java
				usage.txt
			funtion
				FindAll.java
				Generate.java
				Hint.java
				Input.java
				IsOK.java
				Print.java
				Put.java
				Save.java
				Show.java
				Solve.java
		foreEnd
			frame
				Framework.java
				GameField.java
				MyTHread.java
				SelectNumFrame.java
				SudokuCell.java
				SuperTextArea.java
				Terminal.java
			menu
				MenuExit.java
				MenuFindAll.java
				MenuGenerate.java
				MenuHint.java
				MenuInput.java
				MenuPrint.java
				MenuPut.java
				MenuSave.java
				MenuShow.java
				MenuSolve.java
				MenuSolve2.java
				MenuSolve3.java
				MenuSolve4.java
				MenuUsage.java
		main
			Main.java
```

# 实验报告

移动端点击链接下载查看；

[Diagonal Sudoku Programme](https://gsxgoldenlegendary.github.io/files/computer02.pdf)

PC端支持在线预览。

{% pdf https://gsxgoldenlegendary.github.io/files/computer02.pdf %}

# 具体代码

可在[Github仓库中下载](https://github.com/gsxgoldenlegendary/Sudoku)

## BackEnd
### Data 

```java
package backEnd.data;

public class Data {
    public static int[][] cells = new int[9][9];
    public static boolean[][] isPut = new boolean[9][9];
}

```
### FindAll

```java
package backEnd.function;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class FindAll {
    static int num;
    static boolean[][] isPut;

    public static class SuperThread extends Thread {
        int[][] tempArr;
        int m, n;

        public SuperThread(int x, int y, int[][] upper) {
            m = x;
            n = y;
            tempArr = new int[9][9];
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    tempArr[i][j] = upper[i][j];
        }

        @Override
        public void run() {
            int temp = 0;
            if (9 == m && 0 == n) {
                num++;
                String str = new String();
                str += "The" + num + "solution\n";
                for (int i = 0; i < 9; i++) {
                    for (int j = 0; j < 9; j++)
                        str += tempArr[i][j] + " ";
                    str += "\n";
                }
                Framework.textArea.append(str);
            } else if (0 <= m && m < 9 && 0 <= n && n < 9) {
                if (!isPut[m][n]) {
                    for (temp = tempArr[m][n] + 1; temp <= 9; temp++) {
                        if (isOK(m, n, temp, tempArr)) {
                            tempArr[m][n] = temp;
                            if (8 == n)
                                new SuperThread(m + 1, 0, tempArr).start();
                            else
                                new SuperThread(m, n + 1, tempArr).start();
                        }
                    }
                } else {
                    for (; m < 9 && isPut[m][n];)
                        if (8 == n) {
                            m++;
                            n = 0;
                        } else
                            n++;
                    new SuperThread(m, n, tempArr).start();
                }
            }
        }
    }

    public static void findall() {
        num = 0;
        isPut = new boolean[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                if (Data.cells[i][j] != 0)
                    isPut[i][j] = true;
        new SuperThread(0, 0, Data.cells).start();
    }

    public static boolean isOK(int x, int y, int value, int[][] sodu) {
        if (0 == value)
            return true;
        else {
            for (int i = 0; i < 9; i++) {
                if (i != x && value == sodu[i][y])
                    return false;
                if (i != y && value == sodu[x][i])
                    return false;
            }
            for (int i = x - x % 3; i <= x + 2 - x % 3; i++)
                for (int j = y - y % 3; j <= y + 2 - y % 3; j++)
                    if (!(i == x && j == y) && value == sodu[i][j])
                        return false;
            if (x == y)
                for (int i = 0; i < 9; i++)
                    if (i != x && value == sodu[i][i])
                        return false;
            if (x + y == 8)
                for (int i = 0; i < 9; i++)
                    if (i != x && value == sodu[i][8 - i])
                        return false;
            return true;
        }
    }
}
```
### Generate

```java
package backEnd.function;

import backEnd.data.Data;

public class Generate {
    public static void generate() {
        int temp[][] = { { 5, 8, 1, 4, 2, 7, 6, 9, 3 }, { 3, 7, 4, 5, 9, 6, 8, 1, 2 }, { 9, 6, 2, 1, 3, 8, 4, 7, 5 },
                { 6, 2, 9, 3, 8, 5, 7, 4, 1 }, { 1, 5, 7, 9, 6, 4, 3, 2, 8 }, { 8, 4, 3, 2, 7, 1, 5, 6, 9 },
                { 4, 1, 8, 7, 5, 2, 9, 3, 6 }, { 2, 9, 5, 6, 4, 3, 1, 8, 7 }, { 7, 3, 6, 8, 1, 9, 2, 5, 4 } };
        Data.cells = temp.clone();
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++) {
                Data.isPut[i][j] = false;
                if (10 * Math.random() > 5) {
                    Data.cells[i][j] = 0;
                    Data.isPut[i][j] = false;
                } else
                    Data.isPut[i][j] = true;
            }
        Print.print();
    }
}

```
### Hint
```java
package backEnd.function;

import java.awt.Color;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Hint {

    public static void hint() {
        int m = 0, n = 0;
        Solve.sodu = new int[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                Solve.sodu[i][j] = Data.cells[i][j];
        A: for (m = 0; m < 9; m++)
            for (n = 0; n < 9; n++)
                if (0 == Data.cells[m][n])
                    break A;
        if (true == Solve.dfs_sudoku(m, n)) {
            Framework.gamefield.cellbuttons[m][n].setText("" + Solve.sodu[m][n]);
            Framework.gamefield.cellbuttons[m][n].setBackground(Color.green);
            Data.cells[m][n] = Solve.sodu[m][n];
            Print.print();
        } else
            Framework.textArea.append("Error6:No Answer\n");
    }
}

```
### Input

```java
package backEnd.function;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Input {
    public static void input(String s) {
        if (s.length() > 167) {
            Framework.textArea.append("Error1:syntax error\nWait for command\n");
            return;
        } else {
            for (int i = 0, k = 6; i < 9; i++)
                for (int j = 0; j < 9; k++)
                    if (0 == k % 2) {
                        if (IsOK.isOK(i, j, s.charAt(k) - '0')) {
                            Data.cells[i][j] = s.charAt(k) - '0';
                            j++;
                        } else if (0 > s.charAt(k) || s.charAt(k) > 9) {
                            Framework.textArea.append("Error1:syntax error\nWait for command\n");
                            return;
                        }
                    } else if (1 == k % 2 && s.charAt(k) != ' ') {
                        Framework.textArea.append("Error1:syntax error\nWait for command\n");
                        return;
                    }
            Framework.textArea.append("Accept your input.\n");
            Print.print();
        }
    }
}

```
### IsOK

```java
package backEnd.function;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class IsOK {
    public static boolean isOK(int x, int y, int value) {
        if (0 >= value || value > 9) {
            Framework.textArea.append("Error2:data range exceed\n");
            return false;
        } else if (x < 0 || x >= 9 || y < 0 || y >= 9) {
            Framework.textArea.append("Error3:illegal location\n");
            return false;
        } else if (true == Data.isPut[x][y]) {
            Framework.textArea.append("Error5:there is already a number in this position\n");
            return false;
        } else {
            for (int i = 0; i < 9; i++) {
                if (i != x && value == Data.cells[i][y]) {
                    Framework.textArea
                            .append("Error4:illegal, the line " + i + " column " + y + " has the same number\n");
                    return false;
                }
                if (i != y && value == Data.cells[x][i]) {
                    Framework.textArea
                            .append("Error4:illegal, the line " + x + " column " + i + " has the same number\n");
                    return false;
                }
            }
            for (int i = x - x % 3; i <= x + 2 - x % 3; i++)
                for (int j = y - y % 3; j <= y + 2 - y % 3; j++)
                    if (!(i == x && j == y) && value == Data.cells[i][j]) {
                        Framework.textArea
                                .append("Error4:illegal, the line " + i + " column " + j + " has the same number\n");
                        return false;
                    }
            if (x == y) {
                for (int i = 0; i < 9; i++)
                    if (i != x && value == Data.cells[i][i]) {
                        Framework.textArea
                                .append("Error4:illegal, the line " + i + " column " + i + " has the same number\n");
                        return false;
                    }
            }
            if (8 == x + y) {
                for (int i = 0; i < 9; i++)
                    if (i != x && value == Data.cells[i][8 - i]) {
                        Framework.textArea.append("Error4:illegal, the line " + i + " column " + (int) (8 - i)
                                + " has the same number\n");
                        return false;
                    }
            }
        }
        return true;
    }
}

```
### Print

```java
package backEnd.function;

import java.awt.Color;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Print {
    public static void print() {
        Framework.textArea.append("Current sudoku state is:\n");
        /*
         * for (int i = 0; i < 9; i++) for (int j = 0; j < 9; j++)
         * Framework.gamefield.cellbuttons[i][j].setBackground(Color.black);
         */
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                Framework.textArea.append(" " + Data.cells[i][j]);
                if (0 != Data.cells[i][j]) {
                    Framework.gamefield.cellbuttons[i][j].setText("" + Data.cells[i][j]);
                    if (Data.isPut[i][j]) {
                        Framework.gamefield.cellbuttons[i][j].setBackground(Color.blue);
                        Framework.gamefield.cellbuttons[i][j].setEnabled(false);
                        Framework.gamefield.cellbuttons[i][j].removeMouseListener(Framework.gamefield);
                    } else {
                        if (Color.green != Framework.gamefield.cellbuttons[i][j].getBackground())
                            Framework.gamefield.cellbuttons[i][j].setBackground(Color.orange);
                        Framework.gamefield.cellbuttons[i][j].setEnabled(true);
                    }
                } else {
                    if (!Framework.gamefield.cellbuttons[i][j].isEnabled())
                        Framework.gamefield.cellbuttons[i][j].addMouseListener(Framework.gamefield);
                    Framework.gamefield.cellbuttons[i][j].setText("");
                    Framework.gamefield.cellbuttons[i][j].setEnabled(true);
                    Framework.gamefield.cellbuttons[i][j].setBackground(Color.black);
                }
            }
            Framework.textArea.append("\n");
        }
        Framework.textArea.append("Wait for command:\n");
    }
}

```
### Put

```java
package backEnd.function;

import java.awt.Color;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Put {
    public static void put(String s) {
        int x, y, value = 0;
        x = s.charAt(4) - '0';
        y = s.charAt(6) - '0';
        try {
            if (s.charAt(3) != ' ' || s.charAt(4) < '0' || s.charAt(4) > '9')
                Framework.textArea.append("Error1:syntax error\n");
            else if (s.charAt(5) >= '0' && s.charAt(5) <= '9')
                Framework.textArea.append("Error3:illegal location\n");
            else if (s.charAt(5) != ' ' || s.charAt(6) < '0' || s.charAt(6) > '9')
                Framework.textArea.append("Error1:syntax error\n");
            else if (s.charAt(7) >= '0' && s.charAt(7) <= '9')
                Framework.textArea.append("Error3:illegal location\n");
            else if (IsOK.isOK(x, y, value = Integer.parseInt(s.substring(8)))) {
                Data.cells[x][y] = value;
                Framework.gamefield.cellbuttons[x][y].setText("" + value);
                Framework.gamefield.cellbuttons[x][y].setBackground(Color.orange);
            }
        } catch (NumberFormatException e) {
            Framework.textArea.append("Error1:syntax error\n");
        }
    }
}

```
### Save

```java
package backEnd.function;

import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Date;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Save {
    public static void save(String s) {
        File f = new File(
                "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\"
                        + s + ".txt");
        Date d = new Date();
        if (f.exists()) {
            Framework.textArea.append("Error7:file existed\nInput your game record name again\n");
        } else {
            PrintWriter pw1 = null, pw2 = null;
            try {
                pw1 = new PrintWriter(
                        "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\"
                                + s + ".txt");
                pw2 = new PrintWriter(new BufferedWriter(new FileWriter(
                        "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\cache.txt",
                        true)));
            } catch (IOException e) {
                e.printStackTrace();
            }
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    pw1.print(Data.cells[i][j] + " ");
            pw1.print("\n");
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    if (true == Data.isPut[i][j])
                        pw1.print("1 ");
                    else
                        pw1.print("0 ");
            pw2.println(s + "\n" + d);
            pw1.close();
            pw2.close();
            Framework.textArea.append("Game state recorded successfully\n");
        }
    }
}

```
### Show

```java
package backEnd.function;

import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Show {
    static FileReader in;
    static FileReader in2;
    static BufferedReader reader;
    static BufferedReader reader2;
    String[] cache;

    public static void show() {
        int line = 0;
        String str;
        try {
            in = new FileReader(
                    "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\cache.txt");
            reader = new BufferedReader(in);
        } catch (FileNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        try {
            while ((str = reader.readLine()) != null) {
                if (str.length() > 0) {
                    if (0 == line % 2)
                        Framework.textArea.append(line / 2 + "-" + str);
                    else
                        Framework.textArea.append(" " + str + "\n");
                    line++;
                }
            }
            Framework.textArea
                    .append("Input the record code to load game\nFormat:\"show num\",num is a number showed\n");
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

    public static void show(String s) {
        int line = 0, l = 0;
        try {
            l = Integer.parseInt(s.substring(5));
        } catch (NumberFormatException e) {
            Framework.textArea.append("Error1:syntax error\n");
        }
        String str = new String();
        try {
            in = new FileReader(
                    "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\cache.txt");
            reader = new BufferedReader(in);
        } catch (FileNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        try {
            while ((str = reader.readLine()) != null) {
                if (line == 2 * l)
                    break;
                line++;
            }
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        try {
            in2 = new FileReader(
                    "C:\\Users\\GoldenLengendWindows\\Desktop\\Important Files\\VSCodeJava\\Sudoku\\src\\backEnd\\data\\"
                            + str + ".txt");
            reader2 = new BufferedReader(in2);
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++) {
                    Data.cells[i][j] = reader2.read() - '0';
                    reader2.read();
                }
            reader2.read();
            int temp = 0;
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++) {
                    temp = reader2.read();
                    if ('0' == temp)
                        Data.isPut[i][j] = false;
                    else if ('1' == temp)
                        Data.isPut[i][j] = true;
                    reader2.read();
                }
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        Framework.textArea.append("Last time suduko is\n");
        Print.print();
    }
}

```
### Solve

```java
package backEnd.function;

import java.util.Set;
import java.util.TreeSet;
import java.util.Vector;

import backEnd.data.Data;
import foreEnd.frame.Framework;
import javafx.util.Pair;

public class Solve {
    static int[][] sodu;
    static boolean[][][] possibility = new boolean[9][9][9];
    static int[][] hash2 = new int[82][2];
    static Vector<Set<Integer>> CandidaList;
    public static Vector<Pair<Integer, Integer>> Coord;

    public static void dfs_solve() {
        sodu = new int[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                sodu[i][j] = Data.cells[i][j];
        if (dfs_sudoku(0, 0) == true) {
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    Data.cells[i][j] = sodu[i][j];
            Print.print();
        } else
            Framework.textArea.append("Error6:no answer\n");
    }

    public static void a_star_solve() {
        sodu = new int[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                sodu[i][j] = Data.cells[i][j];
        if (a_star_sudoku() == true) {
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    Data.cells[i][j] = sodu[i][j];
            Print.print();
        } else
            Framework.textArea.append("Error6:no answer\n");
    }

    public static void bt_solve() {
        sodu = new int[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                sodu[i][j] = Data.cells[i][j];
        if (bt_sudoku() == true) {
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    Data.cells[i][j] = sodu[i][j];
            Print.print();
        } else
            Framework.textArea.append("Error6:no answer\n");
    }

    public static void iddfs_solve() {
        sodu = new int[9][9];
        EnterAndInitial();
        if (true == solve()) {
            for (int i = 0; i < 9; i++)
                for (int j = 0; j < 9; j++)
                    Data.cells[i][j] = sodu[i][j];
            Print.print();
        } else
            Framework.textArea.append("Error6:no answer\n");

    }

    static Pair<Integer, Integer> make_pair(int i, int j) {
        return new Pair<Integer, Integer>(i, j);
    }

    public static void Locat_Zero() {
        Coord = new Vector<Pair<Integer, Integer>>();
        Coord.clear();
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                if (sodu[i][j] == 0)
                    Coord.add(make_pair(i, j));
    }

    static void Compute_Cadida(int Count) {
        CandidaList = new Vector<Set<Integer>>();
        CandidaList.clear();
        for (int i = 0; i < Count; i++) {
            Set<Integer> Num = new TreeSet<Integer>();
            for (int j = 0; j < 9; j++)
                Num.add(j + 1);
            int x = Coord.elementAt(i).getKey();
            int y = Coord.elementAt(i).getValue();
            int x0 = x / 3, y0 = y / 3;
            for (int j = 0; j < 9; ++j)
                if (Num.contains(sodu[x][j]))
                    Num.remove(sodu[x][j]);
            for (int k = 0; k < 9; ++k)
                if (Num.contains(sodu[k][y]))
                    Num.remove(sodu[k][y]);
            for (int m = 0; m < 3; ++m)
                for (int n = 0; n < 3; ++n)
                    if (Num.contains(sodu[x0 * 3 + m][y0 * 3 + n]))
                        Num.remove(sodu[x0 * 3 + m][y0 * 3 + n]);
            if (x == y)
                for (int m = 0; m < 9; m++)
                    if (Num.contains(sodu[m][m]))
                        Num.remove(sodu[m][m]);
            if (x + y == 8)
                for (int m = 0; m < 9; m++)
                    if (Num.contains(sodu[m][8 - m]))
                        Num.remove(sodu[m][8 - m]);
            CandidaList.add(Num);
        }
    }

    static Pair<Integer, Integer> Find_Min(int Count) {
        int min = 10, min_index = -1;
        for (int i = 0; i < Count; ++i) {
            int temp = CandidaList.elementAt(i).size();
            if (temp < min) {
                min = temp;
                min_index = i;
            }
        }
        return make_pair(min, min_index);
    }

    public static boolean a_star_sudoku() {
        Locat_Zero();
        int TotalCount = 0, Count = Coord.size();
        Vector<Set<Integer>> popCandidateList = new Vector<Set<Integer>>();
        Vector<Pair<Integer, Integer>> popCoordList = new Vector<Pair<Integer, Integer>>();
        if (Count == 0)
            return true;
        while (Count > 0) {
            Compute_Cadida(Count);
            Pair<Integer, Integer> temp = Find_Min(Count);
            int Min = temp.getKey();
            int MinIndex = temp.getValue();
            if (Min == 0) {
                while (!popCandidateList.lastElement().isEmpty()) {
                    int x = popCoordList.lastElement().getKey();
                    int y = popCoordList.lastElement().getValue();
                    sodu[x][y] = 0;
                    ++Count;
                    Coord.add(popCoordList.lastElement());
                    popCoordList.remove(popCoordList.size() - 1);
                    popCandidateList.remove(popCandidateList.size() - 1);
                }
                int x = popCoordList.lastElement().getKey();
                int y = popCoordList.lastElement().getValue();
                sodu[x][y] = popCandidateList.lastElement().iterator().next();
                popCandidateList.lastElement().remove(sodu[x][y]);
                ++TotalCount;
            } else {
                int x = Coord.elementAt(MinIndex).getKey();
                int y = Coord.elementAt(MinIndex).getValue();
                sodu[x][y] = CandidaList.elementAt(MinIndex).iterator().next();
                CandidaList.elementAt(MinIndex).remove(CandidaList.elementAt(MinIndex).iterator().next());
                popCandidateList.add(CandidaList.elementAt(MinIndex));
                CandidaList.removeElementAt(MinIndex);
                popCoordList.add(Coord.elementAt(MinIndex));
                Coord.removeElementAt(MinIndex);
                --Count;
                ++TotalCount;
            }
        }
        if (TotalCount != 0)
            return true;
        else
            return false;
    }

    public static boolean bt_sudoku() {
        int m = 0, n = 0, temp = 0;
        for (;;) {
            if (9 == m && 0 == n)
                return true;
            else if (-1 == m && 8 == n)
                return false;
            else {
                if (!Data.isPut[m][n]) {
                    for (temp = sodu[m][n] + 1; temp <= 9; temp++) {
                        if (isOK(m, n, temp)) {
                            sodu[m][n] = temp;
                            break;
                        }
                    }
                    if (temp > 9) {
                        sodu[m][n] = 0;
                        do {
                            if (0 == n) {
                                m--;
                                n = 8;
                            } else
                                n--;
                        } while (Data.isPut[m][n] && m >= 0);
                        continue;
                    } else {
                        if (8 == n) {
                            m++;
                            n = 0;
                        } else
                            n++;
                        continue;
                    }
                } else {
                    if (8 == n) {
                        m++;
                        n = 0;
                    } else
                        n++;
                    continue;
                }
            }
        }
    }

    static int sudofind(int m, int n, int[] b) {
        int[] c = new int[10];
        for (int i = 0; i < 9; i++) {
            c[sodu[i][n]]++;
            c[sodu[m][i]]++;
        }
        for (int i = m - m % 3; i <= m + 2 - m % 3; i++)
            for (int j = n - n % 3; j <= n + 2 - n % 3; j++)
                c[sodu[i][j]]++;
        int k = 0;
        for (int i = 1; i < 10; i++)
            if (0 == c[i]) {
                b[k] = i;
                k++;
            }
        return k;
    }

    public static boolean dfs_sudoku(int m, int n) {
        if (8 == m && 8 == n) {
            if (0 != sodu[m][n])
                return true;
            else {
                int[] b = new int[9];
                sudofind(m, n, b);
                if (0 != b[0]) {
                    sodu[m][n] = b[0];
                    return true;
                } else
                    return false;
            }
        } else if (0 == sodu[m][n]) {
            int[] b = new int[9];
            int end = sudofind(m, n, b);
            if (0 == b[0])
                return false;
            else {
                for (int k = 0; k < end; k++) {
                    sodu[m][n] = b[k];
                    if (8 != n) {
                        if (true == dfs_sudoku(m, n + 1))
                            return true;
                    } else if (8 != m)
                        if (true == dfs_sudoku(m + 1, 0))
                            return true;
                    sodu[m][n] = 0;
                }
                return false;
            }
        } else if (8 != n) {
            if (true == dfs_sudoku(m, n + 1))
                return true;
        } else if (8 != m)
            if (true == dfs_sudoku(m + 1, 0))
                return true;
        return false;
    }

    static void EnterAndInitial() {
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++) {
                sodu[i][j] = Data.cells[i][j];
                if (sodu[i][j] != 0) {
                    for (int cnt3 = 0; cnt3 < 9; cnt3++)
                        possibility[i][j][cnt3] = false;
                    possibility[i][j][sodu[i][j] - 1] = true;
                } else
                    for (int cnt3 = 0; cnt3 < 9; cnt3++)
                        possibility[i][j][cnt3] = true;
            }
    }

    static void GetUniquity() {
        int temp1, temp2 = 0, temp3 = 0, x, y;
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++) {
                temp1 = 0;
                for (int cnt3 = 0; cnt3 < 9; cnt3++)
                    if (possibility[i][cnt3][j]) {
                        temp1++;
                        temp2 = cnt3;
                    }
                if (temp1 == 1) {
                    sodu[i][temp2] = j + 1;
                    for (int cnt3 = 0; cnt3 < 9; cnt3++)
                        possibility[i][temp2][cnt3] = false;
                    possibility[i][temp2][j] = true;
                }
            }
        for (int cnt1 = 0; cnt1 < 9; cnt1++)
            for (int cnt2 = 0; cnt2 < 9; cnt2++) {
                temp1 = 0;
                for (int cnt3 = 0; cnt3 < 9; cnt3++)
                    if (possibility[cnt3][cnt1][cnt2]) {
                        temp1++;
                        temp2 = cnt3;
                    }
                if (temp1 == 1) {
                    sodu[temp2][cnt1] = cnt2 + 1;
                    for (int cnt3 = 0; cnt3 < 9; cnt3++)
                        possibility[temp2][cnt1][cnt3] = false;
                    possibility[temp2][cnt1][cnt2] = true;
                }
            }
        for (x = 0; x < 9; x += 3)
            for (y = 0; y < 9; y += 3) {
                for (int cnt1 = 0; cnt1 < 9; cnt1++) {
                    temp1 = 0;
                    for (int cnt2 = 0; cnt2 < 3; cnt2++)
                        for (int cnt3 = 0; cnt3 < 3; cnt3++)
                            if (possibility[cnt2 + y][cnt3 + x][cnt1]) {
                                temp1++;
                                temp2 = cnt2;
                                temp3 = cnt3;
                            }
                    if (temp1 == 1) {
                        sodu[temp2 + y][temp3 + x] = cnt1 + 1;
                        for (int cnt3 = 0; cnt3 < 9; cnt3++)
                            possibility[temp2 + y][temp3 + x][cnt3] = false;
                        possibility[temp2 + y][temp3 + x][cnt1] = true;
                    }
                }
            }
    }

    static void DiminishPossibility() {
        int x, y;
        for (int cnt1 = 0; cnt1 < 9; cnt1++)
            for (int cnt2 = 0; cnt2 < 9; cnt2++) {
                if (sodu[cnt1][cnt2] != 0) {
                    if (cnt1 < 3)
                        y = 0;
                    else if (cnt1 < 6)
                        y = 3;
                    else
                        y = 6;
                    if (cnt2 < 3)
                        x = 0;
                    else if (cnt2 < 6)
                        x = 3;
                    else
                        x = 6;
                    for (int cnt3 = 0; cnt3 < 9; cnt3++) {
                        possibility[cnt1][cnt3][sodu[cnt1][cnt2] - 1] = false;
                        possibility[cnt3][cnt2][sodu[cnt1][cnt2] - 1] = false;
                    }
                    for (int cnt3 = 0; cnt3 < 3; cnt3++)
                        for (int cnt4 = 0; cnt4 < 3; cnt4++)
                            possibility[cnt3 + y][cnt4 + x][sodu[cnt1][cnt2] - 1] = false;
                }
            }
    }

    static int NextState() {
        int amountOfPossibility;
        int temp1 = 0;
        int rest = 81;
        for (int cnt1 = 0; cnt1 < 9; cnt1++)
            for (int cnt2 = 0; cnt2 < 9; cnt2++) {
                amountOfPossibility = 0;
                for (int cnt3 = 0; cnt3 < 9; cnt3++) {
                    if (possibility[cnt1][cnt2][cnt3]) {
                        amountOfPossibility++;
                        temp1 = cnt3 + 1;
                    }
                }
                if (amountOfPossibility == 1)
                    sodu[cnt1][cnt2] = temp1;
                if (sodu[cnt1][cnt2] != 0)
                    rest--;
            }
        return rest;
    }

    static boolean IsCalculatable() {
        int ptr = 0;
        int rest = 81, lastStepRest = 81;
        while (rest > 0) {
            GetUniquity();
            DiminishPossibility();
            rest = NextState();
            if (lastStepRest != rest)
                lastStepRest = rest;
            else {
                for (int cnt1 = 0; cnt1 < 9; cnt1++)
                    for (int cnt2 = 0; cnt2 < 9; cnt2++)
                        if (sodu[cnt1][cnt2] == 0) {
                            hash2[ptr][0] = cnt1;
                            hash2[ptr++][1] = cnt2;
                        }
                hash2[ptr][0] = -1;
                hash2[ptr][1] = -1;
                return false;
            }
        }
        return true;
    }

    static boolean IsRational() {
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++)
                if (!isOK(i, j, sodu[i][j]))
                    return false;
        return true;
    }

    public static boolean isOK(int x, int y, int value) {
        if (0 == value)
            return true;
        else {
            for (int i = 0; i < 9; i++) {
                if (i != x && value == sodu[i][y])
                    return false;
                if (i != y && value == sodu[x][i])
                    return false;
            }
            for (int i = x - x % 3; i <= x + 2 - x % 3; i++)
                for (int j = y - y % 3; j <= y + 2 - y % 3; j++)
                    if (!(i == x && j == y) && value == sodu[i][j])
                        return false;
            if (x == y)
                for (int i = 0; i < 9; i++)
                    if (i != x && value == sodu[i][i])
                        return false;
            if (x + y == 8)
                for (int i = 0; i < 9; i++)
                    if (i != x && value == sodu[i][8 - i])
                        return false;
            return true;
        }
    }

    static boolean DFS(int depth) {
        if (hash2[depth][0] == -1)
            return true;
        else {
            for (int cnt1 = 1; cnt1 <= 9; cnt1++) {
                if (possibility[hash2[depth][0]][hash2[depth][1]][cnt1 - 1]) {
                    sodu[hash2[depth][0]][hash2[depth][1]] = cnt1;
                    if (IsRational() && DFS(depth + 1))
                        return true;
                    else
                        sodu[hash2[depth][0]][hash2[depth][1]] = 0;
                }
            }
            return false;
        }
    }

    static boolean solve() {
        if (IsRational())
            if (IsCalculatable() || DFS(0))
                return true;
            else
                return false;
        else
            return false;
    }

}
```
## ForeEnd
### Framework

```java
package foreEnd.frame;

import java.awt.BorderLayout;
import java.awt.Container;
import java.util.Timer;

import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JScrollPane;
import javax.swing.JTextField;
import javax.swing.ScrollPaneConstants;

import foreEnd.menu.MenuExit;
import foreEnd.menu.MenuFindAll;
import foreEnd.menu.MenuGenerate;
import foreEnd.menu.MenuHint;
import foreEnd.menu.MenuInput;
import foreEnd.menu.MenuPrint;
import foreEnd.menu.MenuSave;
import foreEnd.menu.MenuShow;
import foreEnd.menu.MenuSolve;
import foreEnd.menu.MenuSolve2;
import foreEnd.menu.MenuSolve3;
import foreEnd.menu.MenuSolve4;
import foreEnd.menu.MenuUsage;

public class Framework extends JFrame {
    JMenuBar menuBar = new JMenuBar();
    JMenu file = new JMenu("File");
    JMenu function = new JMenu("Function");
    public static MenuExit menuExit = new MenuExit();
    public static MenuPrint menuPrint = new MenuPrint();
    public static MenuInput menuInput = new MenuInput();
    public static MenuGenerate menuGenerate = new MenuGenerate();
    public static MenuSolve menuSolve1 = new MenuSolve();
    public static MenuSolve2 menuSolve2 = new MenuSolve2();
    public static MenuSolve3 menuSolve3 = new MenuSolve3();
    public static MenuSolve4 menuSolve4 = new MenuSolve4();
    public static MenuFindAll menuFindAll = new MenuFindAll();
    public static MenuSave menuSave = new MenuSave();
    public static MenuHint menuHint = new MenuHint();
    public static MenuShow menuShow = new MenuShow();
    public static MenuUsage menuUsage = new MenuUsage();
    public static GameField gamefield = new GameField();
    public static SuperTextArea textArea = new SuperTextArea(14, 30);
    static JTextField textField = new JTextField(30);
    Container c = getContentPane();
    static int v = ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS;
    static int h = ScrollPaneConstants.HORIZONTAL_SCROLLBAR_ALWAYS;
    public static JScrollPane scrollPane = new JScrollPane(textArea, v, h);
    public Terminal terminal = new Terminal();
    public Timer userTimeAction;

    public Framework() {
        super("Sudoku");
        textArea.setEditable(false);
        MenuUsage.showUsage();
        textField.addActionListener(terminal);
        setLayout(new BorderLayout());
        setJMenuBar(menuBar);
        menuBar.add(file);
        menuBar.add(function);
        file.add(menuUsage);
        file.add(menuSave);
        file.add(menuShow);
        file.add(menuExit);
        function.add(menuPrint);
        function.add(menuInput);
        function.add(menuGenerate);
        function.add(menuSolve1);
        function.add(menuSolve2);
        function.add(menuSolve3);
        function.add(menuSolve4);
        function.add(menuFindAll);
        function.add(menuHint);
        c.add("Center", gamefield);
        c.add("South", terminal);
        terminal.add("North", scrollPane);
        terminal.add("Center", new JLabel("Input"));
        terminal.add("South", textField);
        setSize(550, 900);
        setLocation(400, 0);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);
    }
}

```
### GameField

```java
package foreEnd.frame;

import java.awt.Color;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;

import javax.swing.JPanel;
import javax.swing.border.TitledBorder;

import backEnd.data.Data;
import backEnd.function.IsOK;

public class GameField extends JPanel implements MouseListener {
    public SudokuCell[][] cellbuttons;
    private SelectNumFrame selectNum;

    GameField() {
        setBorder(new TitledBorder("GameField"));
        setLayout(null);
        cellbuttons = new SudokuCell[9][9];
        for (int i = 0; i < 9; i++)
            for (int j = 0; j < 9; j++) {
                cellbuttons[i][j] = new SudokuCell();
                cellbuttons[i][j].setLocation(20 + j * 50 + (j / 3) * 5, 20 + i * 50 + (i / 3) * 5);
                cellbuttons[i][j].x = i;
                cellbuttons[i][j].y = j;
                if (0 != Data.cells[i][j]) {
                    cellbuttons[i][j].setText("" + Data.cells[i][j]);
                    cellbuttons[i][j].setEnabled(false);
                    cellbuttons[i][j].setForeground(Color.black);
                } else
                    cellbuttons[i][j].addMouseListener(this);
                add(cellbuttons[i][j]);
            }
    }

    @Override
    public void mousePressed(MouseEvent e) {
        int i = ((SudokuCell) e.getSource()).x;
        int j = ((SudokuCell) e.getSource()).y;
        int value;
        if (selectNum != null) {
            selectNum.dispose();
        }
        selectNum = new SelectNumFrame();
        selectNum.setModal(true);
        selectNum.setLocation(e.getLocationOnScreen().x, e.getLocationOnScreen().y);
        selectNum.setCell((SudokuCell) e.getSource());
        selectNum.setVisible(true);
        value = Integer.parseInt(((SudokuCell) e.getSource()).getText());
        if (IsOK.isOK(i, j, value)) {
            Data.cells[i][j] = value;
            Framework.textArea.append("Your command:put " + i + " " + j + " " + value + "\nWait command\n");
        } else {
            cellbuttons[i][j].setText("");
            Data.cells[i][j] = 0;
            cellbuttons[i][j].setBackground(Color.black);
            Framework.textArea.append("Your command:put " + i + " " + j + " " + value + "\nWait command\n");
        }
    }

    @Override
    public void mouseClicked(MouseEvent e) {
    }

    public void mouseReleased(MouseEvent e) {
    }

    public void mouseEntered(MouseEvent e) {
    }

    public void mouseExited(MouseEvent e) {
    }
}

```
### Mythread

```java
package foreEnd.frame;

public class MyThread extends Thread {
    public MyThread() {
        setPriority(MAX_PRIORITY);
    }

    @Override
    public void run() {
        Framework.textField.setText("");
        Framework.textArea.append("Program exits in 5 seconds.Bye!\n");
        long begintime = System.currentTimeMillis();
        for (;;) {
            if (5000 < System.currentTimeMillis() - begintime)
                System.exit(0);
        }
    }
}

```
### SelectNumFrame

```java
package foreEnd.frame;

import java.awt.Color;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;

import javax.swing.JButton;
import javax.swing.JDialog;

class SelectNumFrame extends JDialog implements MouseListener {
    private SudokuCell cell;

    public void setCell(SudokuCell cell_2) {
        cell = cell_2;
    }

    public SelectNumFrame() {
        setTitle("Put");
        setSize(160, 185);
        setBackground(Color.blue);
        setLayout(null);
        addNum();
    }

    private void addNum() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                JButton btn = new JButton();
                btn.setSize(50, 50);
                btn.setLocation(i * 50, j * 50);
                btn.setText("" + (j * 3 + i + 1));
                btn.addMouseListener(this);
                this.add(btn);
            }
        }
    }

    @Override
    public void mousePressed(MouseEvent e) {
        cell.setText(((JButton) e.getSource()).getText());
        cell.setBackground(Color.orange);
        dispose();
    }

    public void mouseClicked(MouseEvent e) {
    }

    public void mouseReleased(MouseEvent e) {
    }

    public void mouseEntered(MouseEvent e) {
    }

    public void mouseExited(MouseEvent e) {
    }
}

```## SudokuCell

```java
package foreEnd.frame;

import java.awt.Color;
import java.awt.Font;

import javax.swing.JButton;

public class SudokuCell extends JButton {
    public int x, y;

    public SudokuCell() {
        setSize(50, 50);
        Font font = new Font("", 2, 24);
        setFont(font);
        setBackground(Color.black);
        setForeground(Color.white);
    }
}

```
### SuperTextArea

```java
package foreEnd.frame;

import java.awt.Font;

import javax.swing.JTextArea;

public class SuperTextArea extends JTextArea {
    public SuperTextArea(int m, int n) {
        super(m, n);
        setFont(new Font("Arial", Font.BOLD, 14));
    }

    public void append(String str) {
        super.append(str);
        this.setCaretPosition(this.getText().length());
    }
}

```
### Terminal

```java
package foreEnd.frame;

import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JPanel;
import javax.swing.border.TitledBorder;

import backEnd.function.FindAll;
import backEnd.function.Generate;
import backEnd.function.Hint;
import backEnd.function.Input;
import backEnd.function.Print;
import backEnd.function.Put;
import backEnd.function.Save;
import backEnd.function.Show;
import backEnd.function.Solve;
import foreEnd.menu.MenuUsage;

public class Terminal extends JPanel implements ActionListener {
    Terminal() {
        setBorder(new TitledBorder("Terminal"));
        setLayout(new BorderLayout());

    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.textField) {
            String s = Framework.textField.getText();
            Framework.textArea.append("Your command:" + s + "\n");
            Framework.textField.setText("");
            if (s.equals("exit"))
                new MyThread().start();
            else if (s.equals("print"))
                Print.print();
            else if (s.length() >= 167 && s.substring(0, 5).equals("input"))
                Input.input(s);
            else if (s.length() >= 9 && s.substring(0, 3).equals("put"))
                Put.put(s);
            else if (s.equals("generate"))
                Generate.generate();
            else if (s.equals("A*"))
                Solve.a_star_solve();
            else if (s.equals("BT"))
                Solve.bt_solve();
            else if (s.equals("DFS"))
                Solve.dfs_solve();
            else if (s.equals("IDDFS"))
                Solve.iddfs_solve();
            else if (s.equals("findall"))
                FindAll.findall();
            else if (s.length() >= 5 && s.charAt(4) == ' ' && s.substring(0, 4).equals("save"))
                Save.save(s.substring(5));
            else if (s.equals("hint"))
                Hint.hint();
            else if (s.equals("show"))
                Show.show();
            else if (s.equals("usage"))
                MenuUsage.showUsage();
            else if (s.length() >= 6 && s.substring(0, 4).equals("show"))
                Show.show(s);
            else
                Framework.textArea.append("Error1:syntax error\n");
            Framework.textArea.append("Wait for command\n");
        }
    }
}
```
### Menu

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import foreEnd.frame.Framework;
import foreEnd.frame.MyThread;

public class MenuExit extends JMenuItem implements ActionListener {
    public MenuExit() {
        setText("Exit");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuExit) {
            Framework.textArea.append("Your command:exit\n");
            new MyThread().start();
        }
    }
}
```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.FindAll;
import foreEnd.frame.Framework;

public class MenuFindAll extends JMenuItem implements ActionListener {
    public MenuFindAll() {
        setText("FindAll");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuFindAll) {
            Framework.textArea.append("Your command:findall\n");
            FindAll.findall();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Generate;
import foreEnd.frame.Framework;

public class MenuGenerate extends JMenuItem implements ActionListener {
    public MenuGenerate() {
        setText("Generate");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuGenerate) {
            Framework.textArea.append("Your command:generate\n");
            Generate.generate();
        }
    }
}
```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Hint;
import foreEnd.frame.Framework;

public class MenuHint extends JMenuItem implements ActionListener {
    public MenuHint() {
        setText("Hint");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuHint) {
            Framework.textArea.append("Your command:hint\n");
            Hint.hint();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import foreEnd.frame.Framework;

public class MenuInput extends JMenuItem implements ActionListener {
    public MenuInput() {
        setText("Input");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuInput) {
            Framework.textArea.append(
                    "Your command:input\nPlease input your sudoku formally in input textfield\nFormat:\"input a b...\",a,b...are numbers spilted by ONE vacancy\nWaiting for command");
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Print;
import foreEnd.frame.Framework;

public class MenuPrint extends JMenuItem implements ActionListener {
    public MenuPrint() {
        setText("Print");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuPrint) {
            Framework.textArea.append("Your command:print\n");
            Print.print();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import foreEnd.frame.Framework;

public class MenuSave extends JMenuItem implements ActionListener {
    public MenuSave() {
        setText("Save");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuSave) {
            Framework.textArea.append(
                    "Your command:save\nInput your game record name.\nFormat:\"save name\",name is your expected file name.");
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Show;
import foreEnd.frame.Framework;

public class MenuShow extends JMenuItem implements ActionListener {
    public MenuShow() {
        setText("Show");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuShow) {
            Framework.textArea.append("Your command:show\n");
            Show.show();
        }
    }
}
```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Solve;
import foreEnd.frame.Framework;

public class MenuSolve extends JMenuItem implements ActionListener {
    public MenuSolve() {
        setText("Solve(BT)");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuSolve1) {
            Framework.textArea.append("Your command:solve(BT)\n");
            Solve.bt_solve();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Solve;
import foreEnd.frame.Framework;

public class MenuSolve2 extends JMenuItem implements ActionListener {
    public MenuSolve2() {
        setText("Solve(IDDFS)");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuSolve2) {
            Framework.textArea.append("Your command:solve(IDDFS)\n");
            Solve.iddfs_solve();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Solve;
import foreEnd.frame.Framework;

public class MenuSolve3 extends JMenuItem implements ActionListener {
    public MenuSolve3() {
        setText("Solve(DFS)");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuSolve3) {
            Framework.textArea.append("Your command:solve(DFS)\n");
            Solve.dfs_solve();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import backEnd.function.Solve;
import foreEnd.frame.Framework;

public class MenuSolve4 extends JMenuItem implements ActionListener {
    public MenuSolve4() {
        setText("Solve(A*)");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuSolve4) {
            Framework.textArea.append("Your command:solve(A*)\n");
            Solve.a_star_solve();
        }
    }
}

```

```java
package foreEnd.menu;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JMenuItem;

import foreEnd.frame.Framework;

public class MenuUsage extends JMenuItem implements ActionListener {
    static String str = "Welcome to my sudoku world!\n" + "usage:\n"
            + "1.Enter \"exit\" or press \"Exit\" to quit programme in 5 minutes.\n"
            + "2.Enter \"print\" or press \"Print\" to print current sudoku state. 0 filled for vacancy. \n"
            + "3.press \"Input\" to input a soduku. Cement format shown then.\n"
            + "4.Enter or press \"generate\" to generate a sudoku which has 17 non-zero at least numbers at random.\n"
            + "5.Enter \"DFS\" or press \"Solve(DFS)\" to solve surrent sudoku by depth-first search method.\n"
            + "6.Enter \"IDDFS\" or press \"Solve(IDDFS)\" to solve surrent sudoku by iterative deepening depth-first search method.\n"
            + "7.Enter \"A*\" or press \"Solve(A*)\" to solve surrent sudoku by heuristically search method.\n"
            + "8.Enter \"put x y z\" or choose number by mouse to put z into x row y column.Array counted from 0. \n"
            + "9.Enter \"hint\" or press \"Hint\" to get a hint cell.\n"
            + "10.Press \"Save\" to save current sudoku. Operation following shown then.\n"
            + "11.Enter \"show\" or press \"Show\" to view saved game. Operation following shown then.\n"
            + "12.Enter \"usage\" or press \"Usage\" to get usage.\n"
            + "13.Enter \"findall\" or press\"FindAll\" to find all solution(s) by multi-threads method.\n"
            + "14.Enter \"BT\" or press \"Solve(BT)\" to solve surrent sudoku by back tracking method.\n"
            + "Error list:\n" + "Error1:syntax error\n" + "Error2:data range exceed\n" + "Error3:illegal location\n"
            + "Error4:illegal, the line x column y has the same number\n"
            + "Error5:there is already a number in this position\n" + "Error6:No Answer\n" + "Error7:file existed\n"
            + "Have fun!\n" + "Waiting for command:";

    public MenuUsage() {
        setText("Usage");
        addActionListener(this);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == Framework.menuUsage) {
            Framework.textArea.append("Your command:usage\n");
            showUsage();
        }
    }

    public static void showUsage() {
        Framework.textArea.append(str);
    }
}
```
## Main

```java
package main;

import backEnd.data.Data;
import foreEnd.frame.Framework;

public class Main {
    public static void main(String[] args) {
        new Data();
        new Framework();
    }
}
```

