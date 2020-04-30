# Useful tools for checking and developing C/C++ code (and more)


Probably many of you have encountered errors which, although they were easy to fix (e.g. copy-paste bugs), were hidden in the code for months or years before they were fixed.  
The solution to these problems in many cases are static and dynamic code analyzers and programs to check for memory leaks or CPU time usage by functions that help to better optimize the code and search for bottlenecks.

All tools I'm going to present are free for open-source projects (with a small exception of PVS-Studio, but about that later), many of which can be easily integrated with CI (in my case Gitlab CI) for autimatical code and regression checking.

I have integrated many projects with Sonarcloud, Cppcheck and Coverity Scan, whose codes and implementation details can be found here - https://gitlab.com/dashboard/projects.

The results of Sonarcloud scans can be found here - https://sonarcloud.io/organizations/qarmin-1/projects and Cppcheck in pipelins in a given project on Gitlab e.g. https://qarmin.gitlab.io/-/godot/-/jobs/526221853/artifacts/report/index.html


## 1. Cppcheck
This is probably the most basic and easiest to use error search program in C/C++ source files, which does not require compilation of the checked program to work.

All we have to do is enter the project directory and run Cppcheck there, or use the graphical version and click it.

It has many kinds of results presentation, but for me the most convenient method is to export to html (shown in the example at the bottom)

Example of integration with Gitlab CI

Translated with www.DeepL.com/Translator (free version) - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml#L48-59 


### Sample Reports
Strona HTML - https://qarmin.gitlab.io/-/godot/-/jobs/526221853/artifacts/report/index.html

![Zrzut ekranu z 2020-04-16 14-26-13](https://user-images.githubusercontent.com/41945903/80741896-b9c00080-8b1a-11ea-9ab6-639d76d2dddd.png)

### Installation on Ubuntu
```
sudo apt install cppcheck cppcheck-gui
```

### Usage
Console - execute these commands inside the project folder, and an HTML file with code and errors will be generated inside the `report` folder
```
cppcheck -q -j8 --enable=all --force --output-file=cppcheck.xml --xml --xml-version=2 .
mkdir report
cppcheck-htmlreport --source-dir=. --title=project --file=cppcheck.xml --report-dir=report
```

## 2. Sonarcloud
Sonarcloud allows you to view and sort potential errors through the website.  
It is free to use for open source projects.  
It finds similar bugs as Cppcheck as opposed to it requires time-consuming compilation.


### Sample Report
Sample Report - https://sonarcloud.io/project/issues?id=qarmin_assimp&resolved=false&rules=c%3AS2095%2Ccpp%3AS1035%2Ccpp%3AS1764%2Ccpp%3AS2259%2Ccpp%3AS2637%2Ccpp%3AS3584%2Ccpp%3AS836&types=BUG

![Sonarcloud](https://user-images.githubusercontent.com/41945903/80742549-d6a90380-8b1b-11ea-9ba4-220f35855368.png)

### Usage
Example of integration with Gitlab CI - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml

## 3. Coverity Scan

A static analyzer similar in operation to Sonarcloud (you can also view the results online and it is free for open source solutions), but it does not allow to make the results publicly available, so each individual must ask for access to them.  
According to my experience it finds more real errors than previous tools.

### Sample Report
Sample Report(requires a request for access) - https://scan.coverity.com/projects/qarmin-wine?tab=overview

![Coverity](https://user-images.githubusercontent.com/41945903/80742540-d3ae1300-8b1b-11ea-8e24-5d0cdc0054dd.png)

### Usage

Example of integration with Gitlab CI - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml#L7-26

Names like - $COVERITY_SCAN_TOKEN, $GITLAB_USER_EMAIL, $COVERITY_SCAN_PROJECT_NAME should be changed with yours tokens, names etc.  
and also `g++ rr.cpp -o rr.out` should be changed to proper comilation instructions
```
curl -o /tmp/cov-analysis-linux64.tgz https://scan.coverity.com/download/linux64 --form project=$COVERITY_SCAN_PROJECT_NAME --form token=$COVERITY_SCAN_TOKEN
tar xfz /tmp/cov-analysis-linux64.tgz
cov-analysis-linux64-*/bin/cov-build --dir cov-int g++ rr.cpp -o rr.out
tar cfz cov-int.tar.gz cov-int
curl https://scan.coverity.com/builds?project=$COVERITY_SCAN_PROJECT_NAME --form token=$COVERITY_SCAN_TOKEN --form email=$GITLAB_USER_EMAIL --form file=@cov-int.tar.gz

```
## 4. PVS Studio
A commercial static analyser to check the code offline (internet is probably required when checking the licence).  
It has a free weekly trial version which can be requested at https://www.viva64.com/en/pvs-studio-download/.  
It also has a free version for open source projects, but this requires you to add a comment to each file:

// This is an open source non-commercial project. Dear PVS-Studio, please check it.
// PVS-Studio Static Code Analyzer for C, C++, C#, and Java: http://www.viva64.com

which of course scares a lot of people away, including me.  
Nevertheless, it is probably one of the best static analyzers.

I used the free trial version somewhere around a year ago, so I don't have my own reports at hand and the list of steps to scan the project may be a bit outdated.

### Sample Report
Sample Report from the Wine check, together with an explanation of the errors can be found here - https://www.viva64.com/en/b/0352/

### Installation and configuration on Ubuntu
1. Download and install the PVS from (deb package) - https://www.viva64.com/en/pvs-studio-download/
2) Installation of the strace package - `sudo apt install strace`
License activation - `pvs-studio-analyzer credentials usermail@gmail.com RRRR-WWWW-RRRR0-TTTD`.
4. Compilation - `pvs-studio-analyzer trace -- g++ rr.cpp -o rr.out`
5. Conversion of results to QtCreator (also available xml, csv, errorfile, html and fullhtml)
```
pvs-studio-analyzer analyze -j8 -o ./Nieczytelny.log -l ~/.config/PVS-Studio/PVS-Studio.lic
plog-converter -o ./Tasks.tasks -a GA:1,2 -t tasklist ./Nieczytelny.log
```
6. Opening an error file in QtCreator - `qtcreator Tasks.tasks`.


## 5. Hotspot
A great tool to check the time the program spends on the processor.
Displays the time used by the program between different threads and available processors.
Also allows you to check the number of processor ticks used by each function.


### Sample Report
![Hotspot](https://user-images.githubusercontent.com/41945903/80742547-d577d680-8b1b-11ea-91ad-b543665ab4c0.png)
### Installation on Ubuntu
```
sudo apt install hotspot linux-cloud-tools-generic linux-tools-generic
```

### Usage

1. Open a GUI (best opened with a root account)
2. Click "Record Data".
3. Enter the application path
4. Press "Start Recording"
5. Press "Stop Recording" or turn off the program
6. Click on "View Results"

## 6. Valgrind
Dynamic and open code analyzer.
It has the ability to search for memory leaks, incorrect readings or application profiling.
It runs the code in one thread, so its performance is not very satisfactory for larger projects, but it works perfectly in smaller programs.


### Sample Report
```
==50713== Memcheck, a memory error detector
==50713== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==50713== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==50713== Command: ./rr.out
==50713== 
==50713== 
==50713== HEAP SUMMARY:
==50713==     in use at exit: 2,400 bytes in 2 blocks
==50713==   total heap usage: 3 allocs, 1 frees, 75,104 bytes allocated
==50713== 
==50713== 800 bytes in 1 blocks are definitely lost in loss record 1 of 2
==50713==    at 0x483C583: operator new[](unsigned long) (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==50713==    by 0x10919E: main (in /home/rafal/rr.out)
==50713== 
==50713== 1,600 bytes in 1 blocks are definitely lost in loss record 2 of 2
==50713==    at 0x483C583: operator new[](unsigned long) (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
==50713==    by 0x1091AC: main (in /home/rafal/rr.out)
==50713== 
==50713== LEAK SUMMARY:
==50713==    definitely lost: 2,400 bytes in 2 blocks
==50713==    indirectly lost: 0 bytes in 0 blocks
==50713==      possibly lost: 0 bytes in 0 blocks
==50713==    still reachable: 0 bytes in 0 blocks
==50713==         suppressed: 0 bytes in 0 blocks
==50713== 
==50713== For lists of detected and suppressed errors, rerun with: -s
==50713== ERROR SUMMARY: 2 errors from 2 contexts (suppressed: 0 from 0)
```
### Installation on Ubuntu
```
sudo apt install valgrind
```

### Usage
```
g++ rr.cpp -o rr.out
valgrind --leak-check=full ./rr.out
```
## 7. Heaptrack 
Displays in graphic form the number of allocations, memory leaks, memory consumption per time unit.  
It is much faster than Valgrind in detecting memory leaks, but I guess there is no option to display them in text form.

### Sample Report
![Heaptrack](https://user-images.githubusercontent.com/41945903/80742545-d4df4000-8b1b-11ea-82ca-ffc22b94ca2c.png)

### Installation on Ubuntu(chyba >19.10)
```
sudo apt install heaptrack heaptrack-gui
```

### Usage
```
g++ rr.cpp -o rr.out
heaptrack ./rr.out
heaptrack_gui /home/rafal/heaptrack.rr.out.50388.gz # File name should appear after the previous command
```

## 8. GCC i Clang dynamic analyzers
Both GCC and Clang contain analyzers that check the program for malfunctions during operation.  
Unlike Valgrind, they allow the program to run on many threads, which makes them usually faster (even several times).
A program compiled with their help works even several times slower and takes up several times more RAM.


The following analyzers are available for the moment:
- Leak Sanitizer - responsible for detecting memory leaks.  
It shows how much and where memory has been allocated.   
This tool has minimal overhead.
```
Direct leak of 3672 byte(s) in 51 object(s) allocated from:
    #0 0x7fe4aeb98ae8 in malloc (/lib/x86_64-linux-gnu/libasan.so.5+0x10dae8)
    #1 0xd2d3c25 in Memory::alloc_static(unsigned long, bool) core/os/memory.cpp:82
    #2 0xd2d3b24 in operator new(unsigned long, char const*) core/os/memory.cpp:42
    #3 0x49c53ae in FileAccess* FileAccess::_create_builtin<FileAccessUnix>() core/os/file_access.h:77
    #4 0xd20d2d0 in FileAccess::create(FileAccess::AccessType) core/os/file_access.cpp:49
    #5 0xd20d707 in FileAccess::create_for_path(String const&) core/os/file_access.cpp:83
    #6 0xd20d9c7 in FileAccess::open(String const&, int, Error*) core/os/file_access.cpp:108
    #7 0xd64d3f4 in PCKPacker::pck_start(String const&, int) core/io/pck_packer.cpp:66
```
- Address Sanitizer - Responsible for detecting writing/reading of values to incorrect places in the memory, e.g. just released.
```
READ of size 8 at 0x61a001447e90 thread T0
    #0 0x9f01bf7 in TabContainer::_gui_input(Ref<InputEvent> const&) scene/gui/tab_container.cpp:89
    #1 0x2358959 in MethodBind1<Ref<InputEvent> const&>::call(Object*, Variant const**, int, Variant::CallError&) core/method_bind.gen.inc:775
    #2 0xe5d9137 in Object::call_multilevel(StringName const&, Variant const**, int) core/object.cpp:763

0x61a001447e90 is located 16 bytes inside of 1256-byte region [0x61a001447e80,0x61a001448368)
freed by thread T0 here:
    #0 0x7f5d74ba804f in __interceptor_free (/lib/x86_64-linux-gnu/libasan.so.5+0x10c04f)
    #1 0xeb7b37f in Memory::free_static(void*, bool) core/os/memory.cpp:181
    #2 0x158da38 in void memdelete<Object>(Object*) core/os/memory.h:118

previously allocated by thread T0 here:
    #0 0x7f5d74ba8448 in malloc (/lib/x86_64-linux-gnu/libasan.so.5+0x10c448)
    #1 0xeb7a32a in Memory::alloc_static(unsigned long, bool) core/os/memory.cpp:85
    #2 0xeb7a226 in operator new(unsigned long, char const*) core/os/memory.cpp:42
    #3 0x92d0b6b in Object* ClassDB::creator<PopupMenu>() (/usr/bin/godots+0x92d0b6b)
```
- Undefined Sanitizer - Responsible for detecting situations not defined in the documents describing the C/C++ language standard, e.g. a bit shift by a value greater than the length of a variable (int a = 25  552), dividing by zero or writing to a variable a value outside its range
```
servers/visual_server.cpp:513:17: runtime error: -2.42852 is outside the range of representable values of type 'unsigned char'
SUMMARY: UndefinedBehaviorSanitizer: undefined-behavior servers/visual_server.cpp:513:17 in 

or

rr.cpp:10:5: runtime error: applying non-zero offset 4 to null pointer
```
- Memory Sanitizer - available only in Clang, responsible for detecting the use of non-initialised variables (from my tests it does not always work as it should)
```
==44112==WARNING: MemorySanitizer: use-of-uninitialized-value
    #0 0x4974b8 in main (/home/rafal/rr2.out+0x4974b8)
    #1 0x7f86d21ec0b2 in __libc_start_main /build/glibc-YYA7BZ/glibc-2.31/csu/../csu/libc-start.c:308:16
    #2 0x41c26d in _start (/home/rafal/rr2.out+0x41c26d)

SUMMARY: MemorySanitizer: use-of-uninitialized-value (/home/rafal/rr2.out+0x4974b8) in main

```
- Thread Sanitizer - responsible for detecting potential abnormal read/writes between different threads (data races)
```
==44112==WARNING: MemorySanitizer: use-of-uninitialized-value
    #0 0x4974b8 in main (/home/rafal/rr2.out+0x4974b8)
    #1 0x7f86d21ec0b2 in __libc_start_main /build/glibc-YYA7BZ/glibc-2.31/csu/../csu/libc-start.c:308:16
    #2 0x41c26d in _start (/home/rafal/rr2.out+0x41c26d)

SUMMARY: MemorySanitizer: use-of-uninitialized-value (/home/rafal/rr2.out+0x4974b8) in main

```
### Installation on Ubuntu
```
sudo apt install gcc g++ clang
```

### Usage
Just add flags to the compilation

Leak Sanitizer:
```
g++ rr.cpp -o rr.out -fsanitize=leak #GCC
clang++ rr.cpp -o rr.out -fsanitize=leak  #LLVM
./rr.out
```
Address Sanitizer:
```
g++ rr.cpp -o rr.out -fsanitize=address #GCC
clang++ rr.cpp -o rr.out -fsanitize=address  #LLVM
./rr.out
```
Undefined Sanitizer:
```
g++ rr.cpp -o rr.out -fsanitize=undefined #GCC
clang++ rr.cpp -o rr.out -fsanitize=undefined  #LLVM
./rr.out
```
Memory Sanitizer:
```
clang++ rr.cpp -o rr.out -fsanitize=memory  #Only LLVM
./rr.out
```
Thread Sanitizer:
```
g++ rr.cpp -o rr.out -fsanitize=thread #GCC
clang++ rr.cpp -o rr.out -fsanitize=thread  #LLVM
./rr.out
```

## 9. Clang i GCC static analyzers
Clang and GCC from version 10 onwards also have static analyzers that can detect potential errors during compilation, which unfortunately extends the time needed for its execution.


### Sample Report
```
rr.cpp:7:10: warning: Value stored to 'r' during its initialization is never read
    int* r =    new int[200];
         ^      ~~~~~~~~~~~~
rr.cpp:12:5: warning: Assigned value is garbage or undefined
    int qq = rr;
    ^~~~~~   ~~

```
### Installation on Ubuntu
```
sudo apt install gcc g++ clang clang-tools
```

### Usage
```
scan-build clang++ rr.cpp -o rr.out #LLVM
gcc rr.cpp -o rr.out -fanalyzer #GCC
```
