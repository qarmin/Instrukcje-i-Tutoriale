Przydatne narzędzia przy sprawdzaniu i rozwijaniu kodu C/C++(i nie tylko)


Zapewne wielu z was spotkało się z błędami, które mimo, że były proste do naprawienia(np. copy-paste bugs) to kryły się w kodzie przez miesiące lub lata zanim zostały naprawione.  
Rozwiązaniem tych problemów w wielu przypadkach są statyczne i dynamiczne analizatory kodu oraz programy do sprawdzania wycieków pamięci czy czasu wykorzystania procesora przez funkcje, które pomagają lepiej optymalizować kod i wyszukiwać wąskie gardła w programie.

Wszystkie narzędzia które przedstawię są darmowe dla projektów open-source(z małym wyjątkiem PVS-Studio, ale o tym później), których znaczna część może być łatwo zintegrowana z CI(w moim wypadku Gitlab CI) do autymatycznego sprawdzania kodu i regresji.

Integrowałem z Sonarcloudem, Cppcheck oraz Coverity Scan wiele projektów, których kody wraz ze szczegółami implementacji można znaleźć tutaj - https://gitlab.com/dashboard/projects.

Wyniki skanów Sonarclouda można znaleźć tutaj - https://sonarcloud.io/organizations/qarmin-1/projects a Cppcheck w pipelinach w danym projekcie na Gitlabie np. https://qarmin.gitlab.io/-/godot/-/jobs/526221853/artifacts/report/index.html


## 1. Cppcheck
Jest to chyba najbardziej podstawowy i najprostszy w użytkowaniu program do wyszukiwania błędów w plikach źródłowych C/C++, który do działania nie wymaga kompilacji sprawdzanego programu.

Jedyne co musimy zrobić to wejść do katalogu z projektem i tam odpalić Cppcheck, lub skorzystać z wersji graficznej i to wyklikać.

Posiada wiele rodzajów prezentacji wyników, lecz dla mnie najwygodniejszą metodą jest eksport do html(pokazany w przykładzie na dole)

Przykład integracji z Gitlab CI - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml#L48-59 


### Przykładowe Raporty
Strona HTML - https://qarmin.gitlab.io/-/godot/-/jobs/526221853/artifacts/report/index.html

![Zrzut ekranu z 2020-04-16 14-26-13](https://user-images.githubusercontent.com/41945903/80741896-b9c00080-8b1a-11ea-9ab6-639d76d2dddd.png)

### Instalacja na Ubuntu
```
sudo apt install cppcheck cppcheck-gui
```

### Sposób użycia 
Konsola - należy wykonać te polecenia wewnątrz folderu z projektem, a w folderze `report` zostanie wygenerowany plik HTML z kodem i błędami
```
cppcheck -q -j8 --enable=all --force --output-file=cppcheck.xml --xml --xml-version=2 .
mkdir report
cppcheck-htmlreport --source-dir=. --title=project --file=cppcheck.xml --report-dir=report
```

## 2. Sonarcloud
Sonarcloud umożliwia przeglądanie i sortowanie potencjalnych błędów poprzez stronę internetową.  
Jest darmowy do użytku dla projektów open source.  
Znajduje podobne błędy jak Cppcheck w przeciwieństwie do niego wymaga czasochłonnej kompilacji.


### Przykładowy Raport
Przykładowy raport - https://sonarcloud.io/project/issues?id=qarmin_assimp&resolved=false&rules=c%3AS2095%2Ccpp%3AS1035%2Ccpp%3AS1764%2Ccpp%3AS2259%2Ccpp%3AS2637%2Ccpp%3AS3584%2Ccpp%3AS836&types=BUG

![Sonarcloud](https://user-images.githubusercontent.com/41945903/80742549-d6a90380-8b1b-11ea-9ba4-220f35855368.png)

### Sposób użycia 
Przykład integracji z Gitlab CI - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml

## 3. Coverity Scan

Statyczny analizator podobny w działaniu do Sonarclouda(również można przeglądać wyniki online i jest darmowy dla rozwiązań open source) lecz nie pozwala na publiczne udostępnianie wyników, przez co każda z osobna osób musi prosić o dostęp do nich.  
Według moich doświadczeń znajduje więcej prawdziwych błędów niż poprzednie narzędzia.

### Przykładowy Raport
Przykładowy raport(wymaga prośby o dostęp) - https://scan.coverity.com/projects/qarmin-wine?tab=overview

![Coverity](https://user-images.githubusercontent.com/41945903/80742540-d3ae1300-8b1b-11ea-8e24-5d0cdc0054dd.png)

### Sposób użycia 

Przykładowa integracja z Gitlab CI - https://gitlab.com/qarmin/godot/-/blob/master/.gitlab-ci.yml#L7-26

Należy zamienić - $COVERITY_SCAN_TOKEN, $GITLAB_USER_EMAIL, $COVERITY_SCAN_PROJECT_NAME odpowiednimi nazwami  
oraz zmienić `g++ rr.cpp -o rr.out` na własne polecenia kompilacji
```
curl -o /tmp/cov-analysis-linux64.tgz https://scan.coverity.com/download/linux64 --form project=$COVERITY_SCAN_PROJECT_NAME --form token=$COVERITY_SCAN_TOKEN
tar xfz /tmp/cov-analysis-linux64.tgz
cov-analysis-linux64-*/bin/cov-build --dir cov-int g++ rr.cpp -o rr.out
tar cfz cov-int.tar.gz cov-int
curl https://scan.coverity.com/builds?project=$COVERITY_SCAN_PROJECT_NAME --form token=$COVERITY_SCAN_TOKEN --form email=$GITLAB_USER_EMAIL --form file=@cov-int.tar.gz

```
## 4. PVS Studio
Komercyjny statyczny analizator umożliwiający sprawdzanie kodu offline(internet jest chyba wymagany przy sprawdzaniu licencji).  
Posiada darmową wersję trial o którą można poprosić na stronie https://www.viva64.com/en/pvs-studio-download/, która trwa tydzień.  
Posiada też darmową wersję dla projektów open source, ale wymaga to dodania do każdego pliku komentarza:

// This is an open source non-commercial project. Dear PVS-Studio, please check it.
// PVS-Studio Static Code Analyzer for C, C++, C#, and Java: http://www.viva64.com

co oczywiście odstrasza znaczną ilość ludzi(w tym też mnie).  
Mimo to jest to chyba jeden z najlepszych statycznych analizatorów.

Korzystałem z darmowej wersji trial gdzieś około rok temu, dlatego nie mam akurat pod ręką własnych raportów a lista kroków do przeskanowania projektu może być nieco przestarzała.

### Przykładowy Raport
Przykładowy raport ze sprawdzenia Wine wraz z objaśnieniem błędów można znaleźć tutaj - https://www.viva64.com/en/b/0352/

### Instalacja i konfiguracja na Ubuntu
1. Pobranie i instalacja PVS ze strony(paczka deb) - https://www.viva64.com/en/pvs-studio-download/
2. Instalacja pakietu strace - `sudo apt install strace`
3. Aktywacja licencji - `pvs-studio-analyzer credentials usermail@gmail.com RRRR-WWWW-RRR0-TTTD`
4. Kompilacja - `pvs-studio-analyzer trace -- g++ rr.cpp -o rr.out`
5. Konwersja wyników do QtCreatora(również dostępne xml, csv, errorfile, html i fullhtml)
```
pvs-studio-analyzer analyze -j8 -o ./Nieczytelny.log -l ~/.config/PVS-Studio/PVS-Studio.lic
plog-converter -o ./Zadania.tasks -a GA:1,2 -t tasklist ./Nieczytelny.log
```
6. Otwarcie pliku z błędami w QtCreator - `qtcreator Zadania.tasks`


## 5. Hotspot
Świetne narzędzie do sprawdzania czasu jaki program spędza w procesorze.
Wyświetla czas użyty przez program pomiędzy różnymi wątkami i dostępnymi procesorami.
Umożliwia sprawdzanie również ilości ticków procesora używanych przez poszczególne funkcje.


### Przykładowy Raport
![Hotspot](https://user-images.githubusercontent.com/41945903/80742547-d577d680-8b1b-11ea-91ad-b543665ab4c0.png)
### Instalacja na Ubuntu
```
sudo apt install hotspot linux-cloud-tools-generic linux-tools-generic
```

### Sposób użycia 

1. Otwieramy GUI(najlepiej otworzyć za pomocą konta root)
2. Klikamy "Record Data"
3. Wpisujemy ścieżkę aplikacji
4. Naciskamy "Start Recording"
5. Naciskamy "Stop Recording" lub wyłaczamy program
6. Klikamy na "View Results"

## 6. Valgrind
Dynamiczny i otwarty analizator kodu.
Posiada możliwość wyszukiwania wycieków pamięci, nieprawidłowych zapisów odczytów czy profilowania aplikacji.
Uruchamia kod w jednym wątku przez co jego wydajność jest niezbyt satysfakcjonująca przy większych projektach, lecz działa wyśmienicie w mniejszych programach.


### Przykładowy Raport
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
### Instalacja na Ubuntu
```
sudo apt install valgrind
```

### Sposób użycia 
```
g++ rr.cpp -o rr.out
valgrind --leak-check=full ./rr.out
```
## 7. Heaptrack 
Wyświetla w formie graficznej liczbę alokacji, wycieki pamięci, zużycie pamięci w poszczególnej jednostce czasu.  
Jest dużo szybszy od Valgrinda w wykrywaniu wycieków pamięci, lecz chyba nie ma opcji wyświetlenia ich w formie tekstowej.

### Przykładowy Raport
![Heaptrack](https://user-images.githubusercontent.com/41945903/80742545-d4df4000-8b1b-11ea-82ca-ffc22b94ca2c.png)

### Instalacja na Ubuntu(chyba >19.10)
```
sudo apt install heaptrack heaptrack-gui
```

### Sposób użycia 
```
g++ rr.cpp -o rr.out
heaptrack ./rr.out
heaptrack_gui /home/rafal/heaptrack.rr.out.50388.gz # Nazwa pliku powinna wyświetlić się po wykonaniu poprzedniego polecenia
```

## 8. GCC i Clang dynamiczne analizatory
Zarówno GCC jak i Clang zawierają analizatory, które sprawdzają czy program nie zachowuje się nieprawidłowo podczas działania.  
W przeciwieństwie do Valgrinda umożliwiają uruchamianie programu na wielu wątkach, przez co są od niego zazwyczaj szybsze(nawet kilkakrotnie).
Program skompilowany z ich pomocą działa nawet kilkakrotnie wolniej oraz zajmuje kilka razy więcej pamięci RAM.


Na tę chwilę dostępne są poniższe analizatory:
- Leak Sanitizer - odpowiedzialny za wykrywanie wycieków pamięci.  
Pokazuje ile i w jakim miejscu została pamięć zaalokowana.   
To narzędzie ma minimalny narzut.
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
- Address Sanitizer - Odpowiedzialny za wykrywanie zapisów/odczytów wartości do niepoprawnego miejsc w w pamięci np. dopiero co zwolnionej.
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
- Undefined Sanitizer - Odpowiedzialny za wykrywanie sytuacji niezdefiniowanych w dokumentach opisujących standard języka C/C++ np. przesunięcie bitowe o wartość większą niż długość zmiennej(int a = 25 << 552), dzielenie przez zero albo zapisanie do zmiennej wartości spoza jej zakresu
```
servers/visual_server.cpp:513:17: runtime error: -2.42852 is outside the range of representable values of type 'unsigned char'
SUMMARY: UndefinedBehaviorSanitizer: undefined-behavior servers/visual_server.cpp:513:17 in 

or

rr.cpp:10:5: runtime error: applying non-zero offset 4 to null pointer
```
- Memory Sanitizer - dostępny wyłącznie w Clangu, odpowiedzialny jest za wykrywanie używania niezainicjalizowanych zmiennych(z moich testów nie zawsze to działa tak jak powinno)
```
==44112==WARNING: MemorySanitizer: use-of-uninitialized-value
    #0 0x4974b8 in main (/home/rafal/rr2.out+0x4974b8)
    #1 0x7f86d21ec0b2 in __libc_start_main /build/glibc-YYA7BZ/glibc-2.31/csu/../csu/libc-start.c:308:16
    #2 0x41c26d in _start (/home/rafal/rr2.out+0x41c26d)

SUMMARY: MemorySanitizer: use-of-uninitialized-value (/home/rafal/rr2.out+0x4974b8) in main

```
- Thread Sanitizer - odpowiedzialny za wykrywanie potencjalnych nieprawidłowych odczytów/zapisów pomiędzy różnymi wątkami(tzw. data race)
```
==44112==WARNING: MemorySanitizer: use-of-uninitialized-value
    #0 0x4974b8 in main (/home/rafal/rr2.out+0x4974b8)
    #1 0x7f86d21ec0b2 in __libc_start_main /build/glibc-YYA7BZ/glibc-2.31/csu/../csu/libc-start.c:308:16
    #2 0x41c26d in _start (/home/rafal/rr2.out+0x41c26d)

SUMMARY: MemorySanitizer: use-of-uninitialized-value (/home/rafal/rr2.out+0x4974b8) in main

```
### Instalacja na Ubuntu
```
sudo apt install gcc g++ clang
```

### Sposób użycia 
Wystarczy dodać flagi do kompilacji

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

## 9. Clang i GCC statyczne analizatory
Clang i GCC od wersji 10 posiadają również statyczne analizatory, które mogą wykrywać potencjalne błędy podczas kompilacji co niestety wydłuża czas potrzebny na jej wykonanie.


### Przykładowy Raport
```
rr.cpp:7:10: warning: Value stored to 'r' during its initialization is never read
    int* r =    new int[200];
         ^      ~~~~~~~~~~~~
rr.cpp:12:5: warning: Assigned value is garbage or undefined
    int qq = rr;
    ^~~~~~   ~~

```
### Instalacja na Ubuntu
```
sudo apt install gcc g++ clang clang-tools
```

### Sposób użycia 
```
scan-build clang++ rr.cpp -o rr.out #LLVM
gcc rr.cpp -o rr.out -fanalyzer #GCC
```