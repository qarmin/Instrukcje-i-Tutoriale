# Zalety i wady kompilacji

## Błędne flagi kompilacji
Rozpoczynając przygodę z tworzeniem programów ze źródeł, często możemy spotkać się przy kopiowaniu poleceń kompilacji z brakiem wytłumaczenia co konkretne flagi robią.  
Kompilując możemy użyć zbyt "specjalistycznych" lub po prostu błędnych ustawień, którego to wynikiem będzie program np. o obniżonej wydajności czy zawierającym ogromną liczbę dodatkowych funkcji, które tylko by przeszkadzały.

![S](https://user-images.githubusercontent.com/41945903/85174478-c1c43300-b275-11ea-9124-eb81835151c9.png)

## Lepsze opisy błędów
Często zdarza się, że programy które pobieramy z racji posiadania mniejszego rozmiaru są okrojone z symboli debugowania i/lub mają wyłączone opcje pomagające w zbieraniu informacji o błędach w danej aplikacji.  
Kompilując samemu program, możemy uzyskać dużo bardziej szczegółowe informacje np. na temat dokładnego miejsca w którym program się wysypał.

Przykładowy backtrace z Godot Engine bez symboli debugowania:
```
[1] /lib/x86_64-linux-gnu/libc.so.6(+0x43f60) [0x7f39d24fbf60] (??:0)
[2] /home/user/Godot_v3.2.1-stable_x11.64() [0xbfa51f] (??:?)
[3] /home/user/Godot_v3.2.1-stable_x11.64() [0x1de1d0a] (??:?)
[4] /home/user/Godot_v3.2.1-stable_x11.64() [0x1dd1347] (??:?)
[5] /home/user/Godot_v3.2.1-stable_x11.64() [0x219367e] (:?)
[6] /home/user/Godot_v3.2.1-stable_x11.64() [0x2196a90] (??:?)
[7] /home/user/Godot_v3.2.1-stable_x11.64() [0x219a787] (:?)
[8] /home/user/Godot_v3.2.1-stable_x11.64() [0x219b8ce] (:?)
[9] /home/user/Godot_v3.2.1-stable_x11.64() [0xbc8274] (??:?)
```
i z:
```
[1] /lib/x86_64-linux-gnu/libc.so.6(+0x43f60) [0x7fbb086b6f60] (??:0)
[2] String::parse_utf8(char const*, int) (/godot/core/ustring.cpp:1473)
[3] EditorSceneImporterGLTF::_parse_json(String const&, EditorSceneImporterGLTF::GLTFState&) (/godot/editor/import/editor_scene_importer_gltf.cpp:69)
[4] EditorSceneImporterGLTF::import_scene(String const&, unsigned int, int, List<String, DefaultAllocator>*, Error*) (/godot/editor/import/editor_scene_importer_gltf.cpp:2987)
[5] ResourceImporterScene::import(String const&, String const&, Map<StringName, Variant, Comparator<StringName>, DefaultAllocator> const&, List<String, DefaultAllocator>*, List<String, DefaultAllocator>*, Variant*) (/godot/editor/import/resource_importer_scene.cpp:1322)
[6] EditorFileSystem::_reimport_file(String const&) (/godot/editor/editor_file_system.cpp:1797)
[7] EditorFileSystem::reimport_files(Vector<String> const&) (/godot/editor/editor_file_system.cpp:1993 (discriminator 3))
[8] EditorFileSystem::_update_scan_actions() (/godot/editor/editor_file_system.cpp:591)
[9] EditorFileSystem::_notification(int) (/godot/editor/editor_file_system.cpp:1174)
```

## Zaśmiecanie systemu
Jeśli chcemy przekompilować program to zwykle oprócz odrobiny wolnego czasu(różnego w zależności od wielkości projektu i używanych narzędzi) potrzebujemy różnorakich pakietów z których nasza aplikacja korzysta.  
Ich instalacja, nie dość że często bywa dość skomplikowana(z racji wymagania konkretnych wersji) to jeszcze często nie jest używana przez żadną inną aplikację.  
Jeśli przestaliśmy już kompilować dany program lub w między czasie zmienią się wymagane zależności, to ich stare wersje, o ile sami ich nie usuniemy, zaczną zalegać nam w systemie i będą zużywać nam miejsce na dysku oraz czasami zasoby takie jak czas procesora czy pamięć RAM.

![S](https://user-images.githubusercontent.com/41945903/85174490-c688e700-b275-11ea-8b4b-08f70bb029d1.png)

## Bezpieczeństwo
Jednym z głównych argumentów podnoszonych w dyskusji o bezpieczeństwie pomiędzy oprogramowaniem Open Source oraz komercyjnym jest to, że przy tym pierwszym możemy swobodnie przeglądać jego kod źródłowy.  
Kompilując taki kod samemu mamy pewność że nikt nic po drodze(np. w instalatorze) nie dodał czegoś w stylu wirusów czy keyloggerów.

## Możliwość dostosowania pod siebie programu
Kompilując program własnoręcznie nie jesteśmy skazani jedynie na oficjalne wersje programu przygotowane przez twórców.  
Możemy wykonać modyfikacje np. aktywujące flagi zwiększające ogólną wydajność programu, które były wyłączone np. z powodu potrzeby zapewnienia kompatybilności ze starszymi urządzeniami/systemami.  
Dodatkowo w wielu programach możemy włączyć ukryte funkcje które są jeszcze formie eksperymentalnej.  
Znając się co nieco na programowaniu możemy naprawić niektóre z błędów które nas dotykają albo wyciszyć denerwujące nas ostrzeżenia.


![S](https://user-images.githubusercontent.com/41945903/85174698-2a131480-b276-11ea-9061-b71f7b75d0b1.png)
 
## Strata czasu
Może się zdarzyć, że tknięci chwilą lub skuszeni przez inne osoby potencjalnymi korzyściami, możemy spróbować wykonać kompilację programu samemu.  
Często jednak wtedy może się okazać że korzystając z wcześniej przygotowanej przez twórców wersji aplikacji moglibyśmy korzystać z mniejszego i szybszego programu pozbawionego niepotrzebnych nam symboli debugowania oraz zapewniającego szereg nieznanych nam optymalizacji(choćby przez wyselekcjonowane flagi kompilacji).


![S](https://user-images.githubusercontent.com/41945903/85174500-c983d780-b275-11ea-9b4a-9336755f7297.png)

## Szybsze otrzymywanie poprawek bezpieczeństwa i nowości
Zazwyczaj czas pomiędzy stworzeniem i włączeniem do repozytorium poprawki a dostarczeniem jej użytkownikowi jest bardzo różny i waha się od kilku godzin do nawet kilku lat w zależności od tego jak autorzy traktują to.  
Często jednak dlatego użytkownicy na własną rękę kompilują programy, aby skorzystać już w tej chwili z najnowszych poprawek błędów czy funkcjonalności, mimo, że autor nie udostępnił jeszcze oficjalnych binarek.  
Dodatkowo możemy kompilować i testować różne forki i PR nowych funkcji/poprawionych błędów mimo że jeszcze nie są one jeszcze włączone do danego repozytorium.

![S](https://user-images.githubusercontent.com/41945903/85174510-cbe63180-b275-11ea-8941-67b6ffb7d6f2.png)

## Lepsze zgłaszanie błędów
Jeśli zauważyliśmy niepoprawne działanie funkcji, która to działała poprawnie we wcześniejszych wersjach programu, to w zgłoszeniu błędu powinniśmy zawrzeć informacje pomiędzy jakimi wersjami zachodzi ten błąd.  
Często się jednak zdarza, że kolejne wersje programu dzieli kilkadziesiąt, kilkaset albo nawet kilka tysięcy commitów, przez co jest bardzo ale to bardzo trudno znaleźć konkretny commit, który spowodował dane błędne zachowanie.  
Aby przyspieszyć naprawę błędu(z doświadczenia to zwykle około dziesięciokrotne przyspieszenie), najlepiej byłoby wskazać konkretny commit który spowodował błędne zachowanie.  
Do takich rzeczy bardzo przydaje się narzędzie bisect dostępne w gicie, które przemieszczając się po historii pozwala traktować konkretne commity jako te w których błąd występuje lub takich w których tego błędu nie ma, dzięki czemu można wskazać które zmiany spowodowały błędy oraz naprawić je dużo szybciej.


![S](https://user-images.githubusercontent.com/41945903/85174515-cee12200-b275-11ea-86f6-5e7310eae6ee.png)
