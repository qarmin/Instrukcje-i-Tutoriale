# Jak pomóc przy rozwoju otwartego oprogramowania?

Zapewne prawie każdy miał styczność z otwartoźródłowym oprogramowaniem i wiele osób używa na co dzień programów typu Gimp, Krita, Firefox, Blender czy nawet systemu Linux.

Z racji dostępności kodu źródłowego i możliwości jego modyfikowania oraz używania za darmo nawet w celach komercyjnych, wokół otwartoźródłowego oprogramowania wykształciła się społeczność, która pomaga tłumaczyć teksty czy naprawiać i tworzyć nowy kod.

Również i ty możesz dołączyć do tego grona osób pomagając przy rozwoju programów które lubisz i z których korzystasz.

## Tłumaczenie
W przypadku gdy nie znamy się zbytnio na programowaniu i/lub rażą nas w oczy nieprzetłumaczone na język ojczysty(albo i też inny) teksty, to możemy pomóc to zmienić tłumacząc interfejs czy dokumentację.

Tłumaczenia zazwyczaj znajdują się w zewnętrznych serwisach np. Weblate, w których można rozpocząć proces tłumaczenia zaraz po rejestracji.

![Weblate](https://user-images.githubusercontent.com/41945903/81387047-53d50980-9116-11ea-845d-8f1e10588d0e.png)

Przykładowe strony z tłumaczeniami:  
- Godot Engine - https://hosted.weblate.org/projects/godot-engine/godot/
- LibreOffice - https://translations.documentfoundation.org/
- Gnome - https://l10n.gnome.org/teams

Wymagania:
- Dobra znajomość przynajmniej dwóch języków, w tym angielskiego
- Poczucie dobrego "smaku" w tłumaczeniu

## Zgłaszanie błędów
Jest to najbardziej podstawowy sposób na wsparcie projektu open source.

Przy zgłaszaniu ważne jest by dostarczyć jak najwięcej informacji o systemie, wersji aplikacji oraz sytuacji w jakiej błąd się pojawia itp. ponieważ z doświadczenia mogę powiedzieć, że im więcej szczegółów jest zawartych w zgłoszeniu, tym przeważnie szybciej zostaje on naprawiony.

Ważne jest również poprawne nazywanie zgłoszeń błędów, ponieważ bardzo często tytuły w stylu "Proszę Pomóżcie POMOCY!!!!" skutkują natychmiastowym zamknięciem wątku i często są ignorowane przez większość użytkowników, a z kolei tytuły typu "Po kliknięciu w przycisk pomoc pojawiają się 2 okna zamiast jednego" zawierają wystarczają wiele informacji, aby osoby które mogą i potrafią pomóc zainteresowały się tematem.

Przydatne jest dołączanie obrazów, gifów, wideo czy nawet możliwych rozwiązaniach problemu.

Podczas zgłoszeń błędów należy się kierować wcześniej przygotowanymi szablonami(jeśli oczywiście istnieją) ale w szczególnych przypadkach możemy nieco je modyfikować, jeśli to konieczne.

Należy pamiętać, że zgłoszenia powinniśmy tworzyć w języku angielskim, tak aby każdy mógł zrozumieć ich treść(możemy skorzystać z darmowego tłumacza [Deepl](https://www.deepl.com/translator))

Przykładowy szablon z silnika Godot Engine:
```
**Godot version:**

**OS/device including version:**

**Issue description:**

**Steps to reproduce:**

**Minimal reproduction project:**
```
Przykład bardzo dobrego zgłoszenia błędu  
![Przydatne](https://user-images.githubusercontent.com/41945903/81387004-428bfd00-9116-11ea-9a13-8b0014877307.png)

Wymagania:
- Umiejętność zwięzłego i rzeczowego opisu problemu

## Tworzenie kodu 
Jest to chyba najtrudniejszy sposób pomaganie projektom open source lecz jednocześnie bez niego żaden nie mógłby się rozwijać.  

Zwykle dzieli się na dwa typy:
- Tworzenie/Usuwanie funkcji
- Naprawa istniejących błędów

Tworzenie czy usuwanie fragmentów kodu źródłowego zazwyczaj jest trudniejsze z tej dwójki ponieważ wymaga bardzo dobrej znajomości kodu i stylu w jakim został napisany tak aby się do niego stosować.

Naprawianie błędów bardzo często wiąże się z koniecznością dogłębnego poznania i zrozumienia kodu aby znaleźć fragment który nie działa poprawnie.  
Zdarza się jednak, że pobieżna analiza kodu w zupełności wystarczy.

Wiele błędów bierze się ze zwykłych literówek albo niepoprawnego używania narzędzi/operatorów danego języka.
Taki rodzaj błędów możemy w miarę prosto znaleźć za pomocą narzędzi tj. Cppcheck, Address i Leak Sanitizer czy Sonarcloud, które automatycznie skanują projekt w poszukiwaniu niepoprawnego kodu i wyświetlają listę w ich mniemaniu błędów, którą trzeba przejrzeć i ocenić czy się nie mylą.

![Gimp](https://user-images.githubusercontent.com/41945903/81387115-7404c880-9116-11ea-9bf4-13ebcce2aae0.png)

Zazwyczaj tworzenie lub modyfikacja kodu źródłowego wiąże się z kilkoma powtarzającymi się czynnościami
- Zapoznanie się z zasadami tworzenia kodu/poprawek dla danego projektu  
https://github.com/godotengine/godot/blob/master/CONTRIBUTING.md

- Sklonowanie repozytorium  
Musimy sklonować własne repozytorium i dodać do niego odniesienie do bazowego.
```
git clone https://github.com/username/godot.git
cd godot
git remote add upstream https://github.com/godotengine/godot.git
```
- Zainstalowanie zależności(programów wymaganych do kompilacji aplikacji)  
Na Ubuntu można to wykonać zazwyczaj za pomocą trzech komend(jednak zalecane jest korzystanie z oficjalnej dokumentacji)
```
sudo sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
sudo apt update

sudo apt build-dep -y godot
```
Na innych systemach musimy znaleźć instrukcję dostarczaną przez twórców programu  
https://docs.godotengine.org/en/latest/development/compiling/

- Testowa kompilacja  
Powinniśmy testowo przekompilować program, abyśmy byli pewni, że błędy które później mogą wystąpić są tylko winą naszych zmian.
```
scons p=linuxbsd -j8
```
- Naprawa błędu/dodanie kodu  
Tworzymy nową gałąź w Gicie na której będziemy zmieniać kod
```
git checkout -b "opengl_fix"
```
Następnie dodajemy wcześniej przez nas określoną funkcjonalność albo naprawiamy konkretny błąd, korzystając z różnych IDE np. VSCodium czy QT Creator.

- Kompilacja i sprawdzenie  
Po dodaniu/zmianie kodu musimy ponownie przekompilować kod i sprawdzić czy wszystko działa tak jak powinno.  
Jeśli są jakieś problemy to musimy naprawić nasz kod i spróbować ponownie.

- Dodanie plików do kolejki  
Należy sprawdzić jakie pliki zostały zmienione i dodać te, które chcemy zawrzeć w naszej poprawce.
```
git status
git add file1 folder2
```

- Tworzenie i wysłanie commita  
Po ukończonym tworzeniu poprawki możemy stworzyć commit, który będzie mógł zostać włączony do repozytorium.  
Musimy mieć na uwadze, że trzeba nadać mu dobry krótki tytuł.
```
git commit -m "Fixes problem with OpenGL driver on AMD cards"
git push --set-upstream origin opengl_fix
```
- Stworzenie PR  
Teraz poprzez webowy interfejs musimy stworzyć w Gitlabie, Githubie czy innym serwisie, PR z naszymi poprawkami zawierający w środku wyjaśnienie zmian.

![Konsola](https://user-images.githubusercontent.com/41945903/81387226-a4e4fd80-9116-11ea-8214-88d9fdfc1cee.png)

Wymagania:
- Doświadczenie w pisaniu kodu w języku programowania używanego w projekcie
- Znajomość systemu kontroli wersji GIT
- Umiejętność dostosowania stylu pisania kodu do tego używanego w repozytorium
- Znajomość podstawowych komend w konsoli

## Używanie 
Chociaż może wydać się to dziwne, to nawet tylko używając otwartoźródłowe oprogramowanie możemy pomóc.

Tworzymy sobie nawyki, poznajemy interfejs programu, przyzwyczajamy się do niego, przez co jest większa szansa że z czasem będziemy chcieli innymi sposobami pomóc w jego rozwoju oraz to, że wybierzemy go zamiast komercyjnego programu.

![Jedno](https://user-images.githubusercontent.com/41945903/81387318-c47c2600-9116-11ea-9f87-01b5420dbe90.png)

Wymagania:
- Ymmmm... No, używanie programu

## Promowanie 
W świecie bardzo ważna jest reklama i jedną ze skuteczniejszych form jest polecanie produktu/programu znajomym czy współpracownikom.

Dlatego jeśli lubisz korzystać z jakiegoś programu otwartoźródłowego, to bardzo dobrym pomysłem jest polecanie go innym osobom jeśli akurat potrzebują czegoś takiego.

Ważne jest aby w razie jakichś prostych problemów, te osoby mogłyby się zwrócić o pomoc do ciebie w ich rozwiązaniu.

Wymagania:
- Używanie programu
- Podstawowa wiedza o jego możliwościach i umiejętność korzystania z niego

## Tworzenie dokumentacji 
Często w razie pewnych problemów z programem lub szukaniem o nim konkretnych informacji sięgamy do jego dokumentacji.

Niestety zdarza się, że dokumentacja jest wybrakowana lub napisana niezrozumiałym dla wielu językiem, przez co osoby muszą tracić czas na odnajdywanie podstawowych informacji na własną rękę.

Zatem dla wielu projektów jednym z głównych celów powinno być stworzenie dokumentacji przyjaznej zarówno dla początkujących jak i zaawansowanych użytkowników, tak aby większość odpowiedzi na najczęściej nurtujące użytkowników pytania była w niej zawarta.

Bardzo ważnym jest aby dokumentacja nie zawierała wielu książkowych definicji, ale też miała sporo przykładów z życia wziętych.


![Docs](https://user-images.githubusercontent.com/41945903/81388155-26895b00-9118-11ea-96bc-1c9059d253b7.png)

Wymagania: 
- Znajomość programu
- Umiejętność przekazywania informacji w zwięzły i prosty sposób
## Artykuły i Poradniki 
Często bywa, że dokumentacja jest niekompletna i nie zawiera odpowiedzi na częste pytania lub jest napisana zbyt trudnym językiem.

W takim więc wypadku, jeśli posiadamy wiedzę na temat danej funkcji programu, a z różnych powodów nie jesteśmy w stanie pomóc przy tworzeniu dokumentacji, wtedy dobrym pomysłem jest stworzenie własnego poradnika w którym mamy pełną swobodę zarówno w temacie jak i stylu pisania.

![Krita](https://user-images.githubusercontent.com/41945903/81388300-68b29c80-9118-11ea-909d-8116c135c7d1.png)

Wymagania:
- Znajomość konkretnych zagadnień z działania/konfiguracji programu
- Umiejętność pisania

## Dotacje 
Mimo, że przeważnie wolne oprogramowanie jest dystrybuowane za darmo, to nie znaczy, że ludzie pracując nad jego rozwojem nie dostają za to pieniędzy.

Takie projekty jak kernel Linux są finansowane przez ogromne firmy opłacające programistów do pracy nad nim, jednak istnieją mniejsze projekty takie jak Linux Mint, Krita czy Godot Engine, które są rozwijane w znacznym stopniu z dotacji zwykłych osób, których środki przeznaczane są na rozwój i poprawianie kodu programu oraz utrzymanie infrastruktury fizycznej(serwery, łącza itp.).

Zazwyczaj informacja o możliwych formach wsparcia znajduje się na stronie głównej projektu lub w repozytorium.

![Dotacja](https://user-images.githubusercontent.com/41945903/81388444-94ce1d80-9118-11ea-9133-1430627b0e62.png)

Wymagania:
- Trzeba mieć wolne środki na koncie ¯\\_(ツ)\_/¯

## Zarządzanie projektem
Z chwilą gdy tworzymy swoje własne repozytorium stajemy się wtedy automatycznie osobami nim zarządzającymi.

Od naszych decyzji zależy w jakim kierunku poprowadzimy jego rozwój, jakie ustalimy cele i zasady w nim panujące czy w końcu jakie poprawki włączymy do projektu a jakie odrzucimy.

Podczas gdy stworzenie projektu w którym będzie się zarządzało jest dość proste to, zostanie osobą decyzyjną w innym projekcie wymaga zazwyczaj zaangażowania w procesie tworzenia i weryfikacji poprawek czy dyskutowaniem nt. przyszłych zmian w zasadach lub o nowych funkcjach.

Należy również umieć powiedzieć NIE pomysłom i zmianom, które nie podążają z założeniami projektu.

Trzeba jednak zrobić to w uprzejmy sposób popierając to silną argumentacją, ponieważ w przeciwnym przypadku można zrazić swoim niemiłym zachowaniem osoby które chciałyby pomóc w rozwoju projektu.

Wymagania:
- Bardzo dobra znajomość kodu projektu
- Doświadczenie przy zarządzaniu innymi projektami(wymagane głównie przy większych projektach)
- Opanowanie i życzliwość - Nie ma chyba nic gorszego jak nieuprzejma osoba odrzucająca twój PR w który włożyłeś sporo pracy

## Projektowanie/Tworzenie elementów graficznych
Mimo, że ogromna ilość oprogramowania open source to wersje konsolowe(CLI), które świetnie się sprawdza w automatyzacji wielu czynności, to również bardzo często jest tworzony interfejs graficzny(GUI), gdyż wiele codziennych czynności jest jego pomocą łatwiej wykonać i jest dużo bardziej przyjazny dla zwykłych użytkowników.

W takich aplikacjach kluczowy jest wygląd oraz czytelność i intuicyjność interfejsu.

Osoby z umiejętnością planowania przestrzennego, mogą się odnaleźć w planowaniu gdzie i jakie elementy mają się znaleźć tak aby użytkownik nie miał problemów w znalezieniu i użyciu danej rzeczy.

Ważne jest również aby ikony w projekcie w sposób jasny i czytelny oznaczały do czego służą.

![Ikony](https://user-images.githubusercontent.com/41945903/81536917-a4de3b00-936c-11ea-8378-c0946f00c8a0.png)

Wymagania:
- Dusza artysty

## Podsumowanie
Oprogramowanie Open Source jest dobrem wspólnym używanym przez rzesze ludzi na całym świecie, które zapewnia nam wolność jaką nosi za sobą możliwość przeglądania, używania i modyfikacji kodu źródłowego aplikacji.

Mimo, że wątpliwe abyśmy sami z tego kodu bezpośrednio korzystali, to istnieją ludzie, którzy za nas(a czasami z naszą pomocą, do czego szczerze zachęcam) będą testowali, naprawiali i dostarczali nam aplikację mając na względzie zarówno naszą wygodę jak i dbając o naszą prywatność i bezpieczeństwo, które mogą być zagrożone poprzez używanie oprogramowania, do którego jedynie garstka osób ma dostęp.
