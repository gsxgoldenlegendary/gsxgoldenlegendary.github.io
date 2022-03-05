---
title: Simulation of Elevator Events
date: 2021-10-29 17:12:08
tags: Data Structure
categories: Computer Science
---

# 数据结构离散事件的模拟大作业——电梯模拟

## 运行结果

![](https://gsxgoldenlegendary.github.io/images/1.png)

<!--more-->

## 项目环境

- 设备：Windows Surface Pro 7 Model 1866 i7
- 操作系统：Windows 11 Pro Insider Preview 10.0.22483.1011
- 集成开发环境：JetBrain CLion 2021.2.1
- 编译器：MinGW 7.3.0 64-bit

## Elevator.h

```C++
//
// Created by administrator Guo on 2021/9/28 12:32.
//

#ifndef DATASTRUCTUREBHW1_ELEVATOR_H
#define DATASTRUCTUREBHW1_ELEVATOR_H

#include "MyLinkList.h"
#include "Student.h"
#include "string"

enum ElevatorState {
    goingUp, goingDown, idle, preparing, opening, closing, enterOrLeave,
    acceleratingUp,acceleratingDown,deceleratingUp,deceleratingDown
};
//    bool enterOrLeave;  D1, whether man is entering or leaving elevator
//    bool idle;          D2, whether elevator has stayed for 300t
//    bool vainOpen;      D3, whether elevator door is open & nobody goes through

class Elevator {
public:
    int code;
    int currentFloor;               //current position of thr elevator
    ElevatorState state;            //current state of elevator
    MyLinkList passengers;  //use list to sort students in elevator
    int actionTime;                 //the time when next action of elevator occurs
    int station;                    //the next floor elevator need stop at
    int destination;                //the last floor where elevator end going up or down
    bool callCar[5];
    int distance[5];

    Elevator(int);
    void waitInFirstFloor();    //E1, wait in the first currentFloor

    //realised in controller function in system class
    //void changeState();       E2, determine whether to change the state

    void openDoor();            //E3, open the swing door
    void inAndOut();            //E4, let students get in and out of the elevator1
    void closeDoor();           //E5, shut the swing door
    void prepare();             //E6, prepare for moving
    void upOneFloor();          //E7, go up a currentFloor
    void downOneFloor();        //E8, go down a currentFloor
    void startDecelerate();
    int checkDistance();

    //maybe it isn't needed in this programme
    //void noAction();          E9, make D2 0

    std::string getState() const;
};

#endif //DATASTRUCTUREBHW1_ELEVATOR_H
```

## Elevator.cpp

```c++
//
// Created by administrator Guo on 2021/9/28 12:32.
//

#include <iostream>
#include "Elevator.h"
#include "main.h"

Elevator::Elevator(int i) {
    code = i;
    currentFloor = 1;           //when the programme starts, elevator is at floor 1
    state = idle;
    actionTime = 0;
    station = 1;
    destination = 1;
    for (auto i: callCar) {
        callCar[i] = false;
    }
    for (auto i: distance) {
        distance[i] = 100;      //100 means needn't reach
    }
}

void Elevator::waitInFirstFloor() {
    destination = 1;
    station = 1;
}

void Elevator::inAndOut() {
    state = enterOrLeave;
    //Students get off the elevator.
    for (auto *iter = passengers.head->next; iter != nullptr;) {
        if (iter->outFloor == currentFloor) {
            std::cout << "\tStudent " << iter->number << " gets off elevator " << code << " .\n";
            iter = passengers.erase(iter);
        } else {
            iter = iter->next;
        }
    }
    //Students get into the elevator
    if (!storey[currentFloor].callDown) {
        for (; !storey[currentFloor].listDown.empty()
               && passengers.size() != MAX_CAPACITY;) {
            Student s = storey[currentFloor].listDown.front();
            std::cout << "\tStudent " << s.number << " gets into elevator " << code << " .\n";
            passengers.push_back(s);
            callCar[s.outFloor] = true;
            storey[currentFloor].listDown.pop_front();
        }
    }
    if (!storey[currentFloor].callUp) {
        for (; !storey[currentFloor].listUp.empty()
               && passengers.size() != MAX_CAPACITY;) {
            Student s = storey[currentFloor].listUp.front();
            std::cout << "\tStudent " << s.number << " gets into elevator " << code << " .\n";
            passengers.push_back(s);
            callCar[s.outFloor] = true;
            storey[currentFloor].listUp.pop_front();
        }
    }
    actionTime = currentTime + ENTER_OR_LEAVE_TIME;
    system1.hasChanged = true;
}

void Elevator::openDoor() {
    //if elevator will go up, callUP canceled in current floor
    //it occurs when elevator is going up, or idle, or it has reached destination of going down
    if ((state == deceleratingUp
         || state == idle
         || state == deceleratingDown
            && destination == currentFloor)
        && storey[currentFloor].callUp) {
        storey[currentFloor].callUp = false;
    }
        //if elevator will go down, callDOWN canceled in current floor
        //it occurs when elevator is going down, or it has reached destination of going up
    else if ((state == deceleratingDown
              || state == idle
              || state == deceleratingUp
                 && destination == currentFloor)
             && storey[currentFloor].callDown) {
        storey[currentFloor].callDown = false;
    }
    //cancel the button of current floor
    callCar[currentFloor] = false;
    state = opening;
    actionTime = currentTime + OPEN_TIME;
    system1.hasChanged = true;
}

void Elevator::closeDoor() {
    state = closing;
    actionTime = currentTime + CLOSE_TIME;
    system1.hasChanged = true;
}

std::string Elevator::getState() const {
    switch (state) {
        case goingUp:
            return "GOING UP";
        case goingDown:
            return "GOING DOWN";
        case idle:
            return "IDLE";
        case preparing:
            return "PREPARING";
        case opening:
            return "OPENING";
        case closing:
            return "CLOSING";
        case enterOrLeave:
            return "ENTER OR LEAVE";
        case acceleratingUp:
            return "ACCELERATING UP";
        case acceleratingDown:
            return "ACCELERATING DOWN";
        case deceleratingUp:
            return "DECELERATING UP";
        case deceleratingDown:
            return "DECELERATING DOWN";
    }
}

void Elevator::upOneFloor() {
    currentFloor++;
    actionTime += UP_TIME;
    state = goingUp;
    system1.hasChanged = true;
}

void Elevator::downOneFloor() {
    currentFloor--;
    actionTime += DOWN_TIME;
    state = goingDown;
    system1.hasChanged = true;
}

void Elevator::prepare() {
    if (destination > currentFloor) {
        state = acceleratingUp;
        actionTime = currentTime + UP_ACCELERATE_TIME;
        system1.hasChanged = true;
    } else if (destination < currentFloor) {
        state = acceleratingDown;
        actionTime = currentTime + DOWN_ACCELERATE_TIME;
        system1.hasChanged = true;
    } else {
        state = idle;
        destination = currentFloor;
        station = currentFloor;
    }
}

void Elevator::startDecelerate() {
    if (state == goingUp) {
        state = deceleratingUp;
        actionTime = currentTime + UP_DECELERATE_TIME;
    } else if (state == goingDown) {
        state = deceleratingDown;
        actionTime = currentTime + DOWN_DECELERATE_TIME;
    }
    system1.hasChanged = true;
}

int Elevator::checkDistance() {
    for (int i = 0; i < 5; i++) {
        int distance1 = 100, distance2 = 100, distance3 = 100;
        //check callCar
        if (callCar[i]) {
            distance1 = abs(i - currentFloor);
        }
        //check callUp
        if (storey[i].callUp) {
            if (destination >= currentFloor) {
                if (i >= currentFloor) {
                    distance2 = i - currentFloor;
                } else {
                    distance2 = destination - i + destination - currentFloor;
                }
            } else {
                if (i < destination) {
                    distance2 = currentFloor - i;
                } else {
                    distance2 = i - destination + currentFloor - destination;
                }
            }
        }
        //check callDown
        if (storey[i].callDown) {
            if (destination >= currentFloor) {
                if (destination >= i) {
                    distance3 = destination - i + destination - currentFloor;
                } else {
                    distance3 = i - currentFloor;
                }
            } else {
                if (i > currentFloor) {
                    distance3 = i - destination + currentFloor - destination;
                } else {
                    distance3 = currentFloor - i;
                }
            }
        }
        distance[i] = std::min(std::min(distance1, distance2), distance3);
    }
}
```

## MyLinkList.h

```C++
//
// Created by administrator Guo on 2021/10/11 09:08.
//

#ifndef DATASTRUCTUREBHW1_MYLINKLIST_H
#define DATASTRUCTUREBHW1_MYLINKLIST_H

#include "Student.h"

using namespace std;

class MyLinkList {
public:
    Student *head;
    Student *tail;

    MyLinkList();
    int size();
    void pop_front();
    void push_back(Student &);
    Student *erase(Student *);
    Student front();
    bool empty();
};

#endif //DATASTRUCTUREBHW1_MYLINKLIST_H
```

## MyLinkList.cpp

```C++
//
// Created by administrator Guo on 2021/10/12 19:08.
//
#include "MyLinkList.h"

MyLinkList::MyLinkList() {
    head = new Student();
    head->next = nullptr;
    tail = head;
}

int MyLinkList::size() {
    auto *p = head->next;
    int n = 0;
    for (; p != nullptr; p = p->next) {
        n++;
    }
    return n;
}

bool MyLinkList::empty() {
    if (head->next == nullptr) {
        return true;
    } else {
        return false;
    }
}

Student MyLinkList::front() {
    if (!empty()) {
        return (Student) (*(head->next));
    }
}

void MyLinkList::push_back(Student& t) {
    auto *student=new Student(t);
    student->next = nullptr;
    tail->next = student;
    tail = tail->next;
}

void MyLinkList::pop_front() {
    Student *temp = head->next;
    if (!empty()) {
        if(tail==head->next){
            tail=head;
        }
        head->next = head->next->next;
        delete temp;
    }
}

Student *MyLinkList::erase(Student *t) {
    for (Student *p = head; p != tail; p = p->next) {
        if (p->next == t) {
            p->next = p->next->next;
            return p->next;
        }
    }
}
```

## Storey.h

```C++
//
// Created by administrator Guo on 2021/9/28 12:34.
//

#ifndef DATASTRUCTUREBHW1_STOREY_H
#define DATASTRUCTUREBHW1_STOREY_H

#include "MyLinkList.h"
#include "Student.h"

class Storey {
public:
    int floor;                      //the floor of the storey
    bool callUp;                    //up button at each storey
    bool callDown;                  //down button at each storey
    MyLinkList listUp;      //list of students going up, realised by list
    MyLinkList listDown;    //list of students going down, realised by list

    explicit Storey(int);
    //make a student in queue including listUp and listDown
    void enQueue(Student &);
    //check whether there is a student who wants to give up
    void checkGiveUp();
};

#endif //DATASTRUCTUREBHW1_STOREY_H
```

## Storey.cpp

```C++
//
// Created by administrator Guo on 2021/9/28 12:34.
//

#include <iostream>
#include "Storey.h"
#include "main.h"

//Enqueue students into two lists distinguished by up or down
void Storey::enQueue(Student &student) {
    if (student.outFloor > floor) {
        if (elevator1.state == enterOrLeave
            && elevator1.currentFloor == floor
            && elevator1.destination >= elevator1.currentFloor) {
            elevator1.inAndOut();
        } else if (elevator1.state == closing
                   && elevator1.currentFloor == floor
                   && elevator1.destination >= elevator1.currentFloor) {
            elevator1.openDoor();
        } else if (elevator2.state == enterOrLeave
                   && elevator2.currentFloor == floor
                   && elevator2.destination >= elevator2.currentFloor) {
            elevator2.inAndOut();
        } else if (elevator2.state == closing
                   && elevator2.currentFloor == floor
                   && elevator2.destination >= elevator2.currentFloor) {
            elevator2.openDoor();
        } else if (elevator1.state == opening
                   && elevator1.currentFloor == floor
                   && elevator1.destination >= elevator1.currentFloor
                   || elevator2.state == opening
                      && elevator2.currentFloor == floor
                      && elevator2.destination >= elevator2.currentFloor) {
            listUp.push_back(student);
        } else {
            listUp.push_back(student);
            callUp = true;
        }
    } else if (student.outFloor < floor) {
        if (elevator1.state == enterOrLeave
            && elevator1.currentFloor == floor
            && elevator1.destination <= elevator1.currentFloor) {
            elevator1.inAndOut();
        } else if (elevator1.state == closing
                   && elevator1.currentFloor == floor
                   && elevator1.destination <= elevator1.currentFloor) {
            elevator1.openDoor();
        } else if (elevator2.state == enterOrLeave
                   && elevator2.currentFloor == floor
                   && elevator2.destination <= elevator2.currentFloor) {
            elevator2.inAndOut();
        } else if (elevator2.state == closing
                   && elevator2.currentFloor == floor
                   && elevator2.destination <= elevator2.currentFloor) {
            elevator2.openDoor();
        } else if (elevator1.state == opening
                   && elevator1.currentFloor == floor
                   && elevator1.destination <= elevator1.currentFloor
                   || elevator2.state == opening
                      && elevator2.currentFloor == floor
                      && elevator2.destination <= elevator2.currentFloor) {
            listDown.push_back(student);
        } else {
            listDown.push_back(student);
            callDown = true;
        }
    }
}

void Storey::checkGiveUp() {
    for (auto *x = listDown.head->next; x != nullptr;) {
        if (x->giveUpTime == currentTime) {
            std::cout << "\tStudent " << x->number << " gives up at storey " << floor << "\n";
            x = listDown.erase(x);
            system1.hasChanged = true;
        } else {
            x = x->next;
        }
    }
    for (auto *x = listUp.head->next; x != nullptr;) {
        if (x->giveUpTime == currentTime) {
            std::cout << "\tStudent " << x->number << " gives up at storey " << floor << "\n";
            x = listUp.erase(x);
            system1.hasChanged = true;
        } else {
            x = x->next;
        }
    }
}

Storey::Storey(int f) {
    floor = f;
    callDown = false;
    callUp = false;
}
```

## Student.h

```C++
//
// Created by administrator Guo on 2021/9/28 15:56.
//

#ifndef DATASTRUCTUREBHW1_STUDENT_H
#define DATASTRUCTUREBHW1_STUDENT_H

class Student {
public:
    int inFloor;        //the floor student gets into elevator
    int outFloor;       //the floor student gets off elevator
    int giveUpTime;     //the time when student give up waiting for elevator
    int interTime;      //the time when next student occurs
    int number;         //the sequence of student
    Student*next;

    Student();
    explicit Student(int);         //M1, enter system, and prepare for next student's appearance
    //realised in storey and elevator class
//    void enterAndWait()const;    M2, press button and wait
//    void queue();                M3, wait in queue
//    void giveUp();               M4, give up
//    void enterElevator();        M5, enter the elevator
//    void leave();                M6, leave
};

#endif //DATASTRUCTUREBHW1_STUDENT_H
```

## Student.cpp

```C++
//
// Created by administrator Guo on 2021/9/28 15:56.
//

#include "Student.h"
#include "random"
#include "main.h"
#include "ctime"

extern "C" { errno_t rand_s(unsigned int *); }

Student::Student(int number) {
    Student::number = number;
    //although a seed is set, it is still not so randomly
    static std::mt19937_64 engine([]() -> unsigned int {
        unsigned int number;
        rand_s(&number);
        return number;
    }());
    std::uniform_real_distribution<double> random(0, 1);
    inFloor = int(random(engine) * 5);
    outFloor = int(random(engine) * 5);
    for (; inFloor == outFloor;) {
        outFloor = int(random(engine) * 5);
    }
    giveUpTime = currentTime + int(random(engine) * 100) + 300;
    interTime = int(random(engine) * 100) + 1;
    system1.hasChanged = true;
    next = nullptr;
}

Student::Student() {
}
```

## System.h

```C++
//
// Created by administrator Guo on 2021/9/28 17:13.
//

#ifndef DATASTRUCTUREBHW1_SYSTEM_H
#define DATASTRUCTUREBHW1_SYSTEM_H

#include "Elevator.h"
#include "Student.h"
#include "list"

class System {
public:
    bool hasChanged;                    //if the system has changed, it needs outputting.

    System();
    //static may result in bug
    static void Controller(Elevator &); //control elevator
    static void callElevator();         //give elevator station and destination in time
    static void outputState();          //output state of the system
    static void createStudent(int &);   //a student gets into the system
};

#endif //DATASTRUCTUREBHW1_SYSTEM_H
```

## System.cpp

```C++
//
// Created by administrator Guo on 2021/9/28 17:13.
//

#include <iostream>
#include "System.h"
#include "main.h"

System::System() {
    hasChanged = false;
}

void System::Controller(Elevator &elevator) {
    //there are several circumstances when the door need opening,
    //it is elevator is going up, going down, or idle & station equal to current floor,
    //& button of current floor in elevator is on, or the direction of elevator is equal to
    //the button which is on in current floor, or elevator has reached destination,
    //or elevator is closing, but a student press button in current floor & it is equal tp
    //the direction of elevator
    if ((currentTime == elevator.actionTime
         && (elevator.state == deceleratingDown
             || elevator.state == deceleratingUp)
         || elevator.state == idle)
        && ((elevator.currentFloor == elevator.station
             && (elevator.callCar[elevator.currentFloor]
                 || elevator.state == deceleratingDown
                    && storey[elevator.currentFloor].callDown
                 || elevator.state == deceleratingUp
                    && storey[elevator.currentFloor].callUp))
            || (elevator.currentFloor == elevator.destination
                && (storey[elevator.currentFloor].callUp
                    || storey[elevator.currentFloor].callDown)))
        || elevator.state == closing
           && elevator.passengers.size() != MAX_CAPACITY
           && (storey[elevator.currentFloor].callUp
               && elevator.destination > elevator.currentFloor
               || storey[elevator.currentFloor].callDown
                  && elevator.destination < elevator.currentFloor)) {
        elevator.openDoor();
    } else if (currentTime == elevator.actionTime
               && (goingUp == elevator.state
                   && elevator.station > elevator.currentFloor
                   || acceleratingUp == elevator.state)) {
        elevator.upOneFloor();
    } else if (currentTime == elevator.actionTime
               && (goingDown == elevator.state
                   && elevator.station < elevator.currentFloor
                   || acceleratingDown == elevator.state)) {
        elevator.downOneFloor();
    } else if (currentTime == elevator.actionTime
               && enterOrLeave == elevator.state) {
        elevator.closeDoor();
    } else if (currentTime == elevator.actionTime
               && opening == elevator.state) {
        elevator.inAndOut();
    } else if (currentTime == elevator.actionTime
               && closing == elevator.state
               || idle == elevator.state
                  && elevator.destination != elevator.currentFloor
               || elevator.state == idle
               || (elevator.state == deceleratingUp
                   && !elevator.callCar[elevator.currentFloor]
                   && !storey[elevator.currentFloor].callDown
                   && !storey[elevator.currentFloor].callUp)) {
        elevator.prepare();
    } else if (currentTime == elevator.actionTime + IDLE_TIME) {
        elevator.waitInFirstFloor();
    } else if (currentTime == elevator.actionTime
               && elevator.passengers.size() != MAX_CAPACITY
               && (goingDown == elevator.state
                   || goingUp == elevator.state)
               && elevator.station == elevator.currentFloor) {
        elevator.startDecelerate();
    }
    //haven't realized waiting in first floor
}

void System::callElevator() {
    elevator1.checkDistance();
    elevator2.checkDistance();
    int minDistance = 100, station_t = elevator1.currentFloor;
    //set station of elevator 1
    if (elevator1.state != acceleratingUp
        && elevator1.state != deceleratingUp
        && elevator1.state != acceleratingDown
        && elevator1.state != deceleratingDown) {
        for (int i = 0; i < 5; i++) {
            if (elevator1.distance[i] < minDistance
                && !(i == elevator1.currentFloor
                     && (elevator1.state == enterOrLeave
                         || elevator1.state == opening
                         || elevator1.state == closing))) {
                minDistance = elevator1.distance[i];
                station_t = i;
            }
        }
        elevator1.station = station_t;
        //set destination of elevator 1
        if (elevator1.station > elevator1.currentFloor
            || elevator1.station == elevator1.currentFloor
               && elevator1.destination > elevator1.currentFloor) {
            for (int i = 4; i >= elevator1.station; i--) {
                if (elevator1.callCar[i]
                    || storey[i].callDown
                    || storey[i].callUp) {
                    elevator1.destination = i;
                    break;
                }
            }
        } else if (elevator1.station < elevator1.currentFloor
                   || elevator1.station == elevator1.currentFloor
                      && elevator1.destination < elevator1.currentFloor) {
            for (int i = 0; i <= elevator1.station; i++) {
                if (elevator1.callCar[i]
                    || storey[i].callDown
                    || storey[i].callUp) {
                    elevator1.destination = i;
                    break;
                }
            }
        }
    }
    //set station of elevator 2
    if (elevator1.state != acceleratingUp
        && elevator1.state != deceleratingUp
        && elevator1.state != acceleratingDown
        && elevator1.state != deceleratingDown) {
        minDistance = 100, station_t = elevator2.currentFloor;
        for (int i = 0; i < 5; i++) {
            if (elevator2.distance[i] < minDistance
                && !(i == elevator2.currentFloor
                     && (elevator2.state == enterOrLeave
                         || elevator2.state == opening
                         || elevator2.state == closing))
                && (elevator2.callCar[i]
                    || elevator1.currentFloor <= elevator1.destination
                       && i != elevator1.destination
                       && (elevator1.currentFloor > i
                           || i > elevator1.destination
                           || storey[i].callDown)
                    || elevator1.currentFloor > elevator1.destination
                       && i != elevator1.destination
                       && (elevator1.currentFloor < i
                           || i < elevator1.destination
                           || storey[i].callUp))) {
                minDistance = elevator2.distance[i];
                station_t = i;
            }
        }
        elevator2.station = station_t;
        //set destination of elevator 2

        if (elevator2.station > elevator2.currentFloor
            || elevator2.station == elevator2.currentFloor
               && elevator2.destination > elevator2.currentFloor) {
            elevator2.destination = 4;
            for (int i = 4; i >= elevator2.station; i--) {
                if (elevator2.callCar[i]
                    || elevator2.station == i
                    || (storey[i].callDown
                        || storey[i].callUp)
                       && (elevator1.currentFloor <= elevator1.destination
                           && i != elevator1.destination
                           && (elevator1.currentFloor > i
                               || i > elevator1.destination
                               || storey[i].callDown)
                           || elevator1.currentFloor > elevator1.destination
                              && i != elevator1.destination
                              && (elevator1.currentFloor < i
                                  || i < elevator1.destination
                                  || storey[i].callUp))) {
                    elevator2.destination = i;
                    break;
                }
            }
        } else if (elevator2.station < elevator2.currentFloor
                   || elevator2.station == elevator2.currentFloor
                      && elevator2.destination < elevator2.currentFloor) {
            elevator2.destination = 0;
            for (int i = 0; i <= elevator2.station; i++) {
                if (elevator2.callCar[i]
                    || elevator2.station == i
                    || (storey[i].callDown
                        || storey[i].callUp)
                       && (elevator1.currentFloor <= elevator1.destination
                           && (elevator1.currentFloor > i
                               || i > elevator1.destination)
                           || elevator1.currentFloor > elevator1.destination
                              && (elevator1.currentFloor < i
                                  || i < elevator1.destination))) {
                    elevator2.destination = i;
                    break;
                }
            }
        }
    }
}

void System::outputState() {
    std::cout << "\tCurrent time:\t" << currentTime
              << "\n\tElevator1:\t"
              << "At floor " << elevator1.currentFloor
              << "\tState:\t" << elevator1.getState() << "\n\t"
              << elevator1.passengers.size() << " student in it."
              << "\tAction time:\t" << elevator1.actionTime
              << "\n\tStation:\t" << elevator1.station
              << "\tDestination:\t" << elevator1.destination
              << "\n\tElevator2:\t"
              << "At floor " << elevator2.currentFloor
              << "\tState:\t" << elevator2.getState() << "\n\t"
              << elevator2.passengers.size() << " student in it."
              << "\tAction time:\t" << elevator2.actionTime
              << "\n\tStation:\t" << elevator2.station
              << "\tDestination:\t" << elevator2.destination;
    for (int i = 0; i < 5; i++) {
        std::cout << "\n\tStorey" << i << ":\t" << storey[i].listUp.size() << " student for up\t"
                  << storey[i].listDown.size() << " student for down";
    }
    //debugging used
//    putchar('\n');
//    for (int i = 0; i < 5; i++) {
//        std::cout << elevator1.distance[i] << " ";
//    }
//    for (int i = 0; i < 5; i++) {
//        std::cout << elevator2.distance[i] << " ";
//    }
    std::cout << "\n\n";
}

void System::createStudent(int &i) {
    Student student(i++);
    occurTime += student.interTime;
    storey[student.inFloor].enQueue(student);
//    Output the new student's information
    std::cout << "\tstudent " << student.number << " appears!\n"
              << "\tFrom:\t" << student.inFloor
              << "\tTo:\t" << student.outFloor
              << "\n\tGive up time:\t" << student.giveUpTime
              << "\tNext student time:" << student.interTime + currentTime << "\n";
}
```

## main.h

```C++
//
// Created by administrator Guo on 2021/9/28 21:45.
//

#ifndef DATASTRUCTUREBHW1_MAIN_H
#define DATASTRUCTUREBHW1_MAIN_H

#include "System.h"
#include "Storey.h"
#include "Elevator.h"

typedef int Time;

extern Storey storey[5];                        //definition of 5 storeys
extern System system1;                          //definition of the event system
extern Elevator elevator1;                      //definition of elevator 1
extern Elevator elevator2;                      //definition of elevator 1
extern Time currentTime,occurTime;               //global time & current time

constexpr int MAX_CAPACITY(10);                 //max capacity of an elevator
constexpr int UP_TIME(51);                      //time of going up a floor
constexpr int DOWN_TIME(61);                    //time of going down a floor
constexpr int CLOSE_TIME(20);                   //time of closing door
constexpr int OPEN_TIME(20);                    //time of opening door
constexpr int ENTER_OR_LEAVE_TIME(20);          //time of the first time door open
constexpr int DURATION_TIME(1000);              //time of all the events
constexpr int IDLE_TIME(300);                   //if elevator isn't used for such time, it'll be set idle
constexpr int UP_ACCELERATE_TIME(15);           //time of elevator accelerate up
constexpr int DOWN_ACCELERATE_TIME(15);         //time of elevator accelerate down
constexpr int UP_DECELERATE_TIME(14);           //time of elevator decelerate up
constexpr int DOWN_DECELERATE_TIME(23);         //time of elevator decelerate down
#endif //DATASTRUCTUREBHW1_MAIN_H
```

## main.cpp

```C++
#include "System.h"
#include "Storey.h"
#include "main.h"

int currentTime, occurTime;
Storey storey[5] = {Storey(0), Storey(1), Storey(2), Storey(3), Storey(4)};
System system1;
Elevator elevator1(1);
Elevator elevator2(2);
//it is main function, the main part of the programme
int main() {
    //make CLion output when debugging
    setbuf(stdout, nullptr);
    for (int i = 0; currentTime <= DURATION_TIME; currentTime++) {
        //check whether student giving up at each floor
        for (auto &x: storey) {
            x.checkGiveUp();
        }
        //If it is the time to create another student,then occur one and make one into the system
        if (currentTime == occurTime) {
            System::createStudent(i);
        }
        //refresh state of elevator
        System::callElevator();
        //if it is time for an action to be taken, take action!
        System::Controller(elevator1);
        System::Controller(elevator2);
        //output state of system just when it has changed
        if (system1.hasChanged) {
            System::outputState();
            system1.hasChanged = false;
        }
//System::outputState();
//debugging used
    }
    //it is a good habit
    return 0;
}
```



