
# Bezpieczny Firefox

Zapewne wielu z was spotkało podczas przeglądania internetu się ze stronami w internecie wyłudzającymi dane, wszędobylskimi reklamami, które zbierają o was informacje oraz samoodtwarzającymi się materiałami wideo.  
Istnieje kilka dodatków i ustawień, które w znaczący sposób mogą zwiększyć bezpieczeństwo i prywatność użytkownika, spowodować szybsze otwieranie stron oraz zmniejszone użycie zasobów systemowych takich RAM czy czas CPU.   
Niektóre porady będą opatrzone stopniem trudności dla mniej lub bardziej zaawansowanych użytkowników.

Porady zostały przygotowane w Firefoxie 70.0  
<center><img src="https://user-images.githubusercontent.com/41945903/68143010-cc24fd00-ff30-11e9-91e9-a0df62ce3bd5.png"></center>

## Spis Treści
- [Kilka Zasad Bezpieczeństwa](#kilka-zasad-bezpieczeństwa)
- [DOH](#doh---szyfrowanie-dns)
- [Telemetria Firefoxa](#telemetria-firefoxa)
- [Prywatna wyszukiwarka](#prywatna-wyszukiwarka)
- [Wbudowana ochrona przed śledzeniem](#wbudowana-ochrona-przed-śledzeniem)
- [Uprawnienia stron internetowych](#uprawnienia-stron-internetowych)
- [Wtyczki](#wtyczki)
 - [Ublock Origin](#ublock-origin---blokowanie-reklam)
 - [HTTPS Everywhere](#https-everywhere---szyfrowana-sieć)
 - [AdNauseum](#adnauseum---dezorientowanie-reklamodawców)

## Kilka zasad bezpieczeństwa
- Instaluj oprogramowanie otwartoźródłowe zamiast własnościowego gdy tylko masz taką możliwość.
- Nie otwieraj plików z nieznanych źródeł, a jeśli musisz to przeskanuj je w serwisie https://www.virustotal.com.
- Nie udostępniaj nikomu swoich danych osobowych takich jak nazwisko czy miejsce zamieszkania.
- Nie loguj się na swoje konta, na urządzeniach co do których nie masz pewności, że nie są zarażone wirusem.
- Staraj się instalować programy ze stron domowej ich producenta lub ze sklepów z oprogramowaniem
- Korzystaj z oprogramowania antywirusowego
- Nie wpisuj swoich danych logowania na stronach nieobsługujących szyfrowania.
- Stosuj unikalne hasła dla każdego serwisu, najlepiej korzystając z menedżera haseł

## DOH - szyfrowanie DNS
Dostępną od niedawna DoH, pozwala na szyfrowanie zapytań DNS, które to odpowiedzialne za konwersję nazwy strony np. 'facebook.com' na jej adres IP - '31.13.81.36', dzięki czemu nikt oprócz ciebie i serwera DNS nie będzie w stanie poznać nazwy strony którą chcemy odwiedzić.

Aby je włączyć najpierw otwieramy ustawienia i przechodzimy na sam dół i w zakładce **Sieć** otwieramy jej ustawienia a w nich zaznaczamy opcję **DNS poprzez HTTPS**.
Domyślnym dostawcą jest Cloudlare, lecz adres serwera DNS obsługującego szyfrowanie możemy dowolnie zmieniać.

![S](https://user-images.githubusercontent.com/41945903/68145118-5a02e700-ff35-11e9-8f3b-5a494cfa15e9.png)


## Telemetria Firefoxa
Firefox domyślnie zbiera pewne informacje telemetryczne i zgłoszenia awarii, więc jeśli chcemy pomóc w jego rozwoju, możemy zaznaczyć niektóre z opcji.  
Wyłączyć można je w opcjach Firefoxa w zakładce **Prywatność i Bezpieczeństwo** pod **Dane zbierane przez program Firefox**

![S](https://user-images.githubusercontent.com/41945903/68146588-a0a61080-ff38-11e9-882d-c97b505ef4e6.png)

## Prywatna wyszukiwarka

Domyślną wyszukiwarką w Firefoxie jest Google, która to jest jest w posiadaniu jednej z największych platform reklamowych zbierającej wszystkie możliwe dane użytkowników, celem lepszego profilowania ich profilowania.  

Jedną z lepszych alternatywnych wyszukiwarek jest DuckDuckGo, oferująca użytkownikom bezpieczne i wolne od szpiegowania przeglądanie wyników wyszukiwania.

Aby ją ustawić należy przejść do ustawień i w zakładce **Wyszukiwanie** pod **Domyślna wyszukiwarka** wybrać **DuckDuckGo**

![S](https://user-images.githubusercontent.com/41945903/68150615-650f4480-ff40-11e9-84c2-2c15610ad419.png)

## Wbudowana ochrona przed śledzeniem
Firefox oferuje domyślnie podstawową ochronę przed śledzącymi skryptami oraz ciasteczkami.  
Możliwe jest również użycie **Ścisłej** ochrony przed śledzeniem, blokującej więcej elementów śledzących lecz niektóre elementy na stronie mogą nie ładować się poprawnie.
Istnieje również tryb umożliwiający dostosowywanie poszczególnych elementów do blokowania.

![S](https://user-images.githubusercontent.com/41945903/68152230-8de50900-ff43-11e9-92f2-968e9c5ca4bc.png)

Można wyłączyć blokowanie na stronie, gdy powoduje ona jej błędne działanie.  
Dodatkowo w panelu po lewej stronie od paska adresu można przejrzeć wszystkie zablokowane elementy na stronie.

![S](https://user-images.githubusercontent.com/41945903/68185426-c74c6180-ffa1-11e9-8dfe-69374c9e8ac2.png)

## Uprawnienia stron internetowych
Zapewne wielu z was spotkało się z denerwującymi okienkami nt. powiadomień czy położenia użytkownika.
W ustawieniach w zakładce **Prywatność i bezpieczeństwo** pod **Uprawnienia** można prosto wyłączyć wszystkie pytania o lokalizację użytkownika, używanie kamery, mikrofonu oraz wyświetlanie powiadomień(to ostatnie zostanie prawdopodobnie domyślnie wprowadzone w wersji 72).

Aby zablokować takie zapytania, należy prawej stronie od danego uprawnienia nacisnąć na przycisk **Ustawienia...** i zaznaczyć **Blokowanie nowych próśb o ...** i nacisnąć przycisk **Zachowaj**.  
W tym samym oknie w razie potrzeby będzie można ustawić listę wyjątków dla stron.

Domyślnie Firefox blokuje autoodtwarzanie dźwięku na stronach, lecz dzięki opcji **Automatyczne odtwarzanie** można zablokować również autoodtwarzające się filmiki.


![S](https://user-images.githubusercontent.com/41945903/68152232-8de50900-ff43-11e9-9f98-3011b3a87f70.png)

## Wtyczki
### Ublock Origin - Blokowanie Reklam
Zapewne wiele osób kojarzy Ublock Origin tylko jako narzędzie do blokowania reklam.
Jednak umożliwia o wiele więcej, a mianowicie blokowanie skryptów JavaScript, czcionek sieciowych, ramek z informacjami o ciasteczkach i RODO czy stron z wirusami i malware lub wykorzystywanych do oszukiwania ludzi.  
Czas ładowania niektórych stron, dzięki użyciu Ublock Origin, może przyspieszyć ładowanie stron nawet kilkukrotnie(najlepszym przykładem jest serwis wykop.pl)

#### Dla początkujących
Na początek należy zainstalować Ublock Origin z oficjalnej strony z dodatkami Mozilli - https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/

Następnie umożliwiamy działanie dodatku w oknach prywatnych.

![S](https://user-images.githubusercontent.com/41945903/68144976-0a242000-ff35-11e9-899c-0e575b3e20f3.png)

Na sam początek pobierzemy oficjalne polskie filtry do Ublocka ze strony - https://github.com/MajkiIT/polish-ads-filter#about, klikając przy każdym filtrze przycisk **Subskrybuj**(niektóre się dublują, więc warto przeczytać adnotacje na dole strony).

Następnie przechodzimy do ustawień dodatku do zakładki **Listy Filtrów**, gdzie znajdują się wszystkie dostępne filtry na tę chwilę.

Zalecam zaznaczenie dla skutecznej ochrony włączyć filtry takie jakie występują na obrazku, należy jednak pamiętać, że im więcej filtrów, tym większe wykorzystanie procesora, dlatego należy zachować umiar w ich włączaniu.

![S](https://user-images.githubusercontent.com/41945903/68148430-46a74a00-ff3c-11e9-97b1-ad4e71437edb.png)

W przypadku gdy dana strona nie będzie działała możemy wyłączyć na niej Ublock Origin, za pomocą tego niebieskiego przycisku, którym to możemy ponownie włączyć ochronę przed reklamami.

![S](https://user-images.githubusercontent.com/41945903/68148620-a7368700-ff3c-11e9-9934-d52fabf0b16b.png)

#### Dla zaawansowanych
Na początek odblokujmy w Ublocku ustawienia zaawansowane, które umożliwią dostosowanie blokowania poszczególnych elementów na stronach.

Znajdują się tu również globalne ustawienia co do blokowania filtrów kosmetycznych, elementów multimedialnych, zdalnych czcionek czy JavaScript.

W przypadku korzystania ze słabszego komputera polecam w tym miejscu globalną blokadę JavaScript, przez co strony będą się dużo szybciej pobierać i wyświetlać. JavaScript niestety jest przez wiele stron wymagany do poprawnego działania, więc należy się uzbroić w cierpliwość przy tworzeniu listy wyjątków.

![S](https://user-images.githubusercontent.com/41945903/68149342-0d6fd980-ff3e-11e9-8d2a-a892a6e73fc1.png)

Powinna pojawić nam się plansza, która to przedstawia po swojej lewej stronie ustawienia globalne stosowane dla wszystkich witryn oraz ustawienia lokalne używane jedynie na tej konkretnej stronie.

Każdym zasobom z danej strony możemy przyporządkować stany oznaczone trzema kolorami:
- czerwony - oznacza  blokadę określonego elementu/zasobu z danej strony np. ustawienie czerwonej blokady na właściwości **domeny zewnętrzne** - spowoduje, że na danej stronie będą blokowane wszelkie zasoby pochodzące z zewnętrznych witryn
- szary - stosowany jest do neutralizacji stanu wyższego poziomu np. gdy globalnie(po lewej stronie) zablokujemy obrazki na wszystkich stronach(kolor czerwony), to możemy stworzyć wyjątek dla danej strony oznaczając tą samą właściwość, lecz tym razem po prawej stronie
- zielony - oznacza, że zasoby pochodzące z danego źródła/strony nie zostaną zablokowane ani przefiltrowane przez Ublocka. Używane są często, gdy ustawiliśmy bardzo agresywne filtry Ublocka blokujące elementy potrzebne do działania danej strony.

![S](https://user-images.githubusercontent.com/41945903/68149440-32fce300-ff3e-11e9-94e2-5af2548d3528.png)

Ublock Origin w swojej instukcji wskazuje, że można wyłączyć skrypty i ramki z zewnętrznych witryn co powinno zwiększyć bezpieczeństwo użytkownika i nie powinno zbytnio zepsuć stron, lecz w razie konieczności można dla konkretnej strony wyłączyć to ustawienie.


Aby  ustawienia o wyłączonych stronach są przechowywane do czasu ponownego uruchomienia przeglądarki, więc aby zapisać zmiany należy nacisnąć na kłódkę, a aby je usunąć na gumkę.

##### Filtry kosmetyczne

Bardzo przydatną Ublocka, jest możliwość usunięcia ze poszczególnych elementów ze strony zwanych **elementami kosmetycznymi**. Możemy zablokować dowolny taki element bazując na jego nazwie, identyfikatorze, umiejscowieniu czy wielu innych atrybutach.

Aktywować tę funkcję możemy poprzez naciśnięcie prawym przyciskiem myszy na ekran i wybranie opcji **Zablokuj element** lub w głównym panelu klikając na przycisk pod wyłączaniem Ublocka, podobny do strzykawki(niestety nie wiem jak to się fachowo nazywa)

![S](https://user-images.githubusercontent.com/41945903/68161262-c988ce80-ff55-11e9-828d-683a55e320a6.png)

Dobrym przykładem niech będzie strona Phoronix.com, do której to posiadam czytnik RSS newsów, dlatego panele boczne wypełnione artykułami nie są mi potrzebne. Zarówno stopka jak i informacje o autorze nie są mi wcale potrzebne, więc je też również usnąłem.

![S](https://user-images.githubusercontent.com/41945903/68183488-e4cafc80-ff9c-11e9-8ab2-ebc28d765755.png)

W razie potrzeby można zablokować/odblokować wyświetlanie elementów kosmetycznych, klikając na przekreślone oko w głównym panelu Ublocka.   
Listę własnych filtrów można przeglądać i modyfikować na stronie ustawień Ublocka w zakładce **Moje filtry** oraz **Moje reguły**


### HTTPS Everywhere - Szyfrowana sieć
Przez wiele lat przez sieć były wysyłane pakiety HTTP, które nie były szyfrowane, dzięki czemu możliwe było proste podsłuchiwanie komunikacji. W dzisiejszych czasach większość stron obsługuje wysyłanie danych poprzez szyfrowany HTTP, lecz część z nich ciągle używa domyślnie HTTP. Dodatek HTTPS Everywhere został stworzony aby wymusić korzystanie z HTTPS przez serwery/strony internetowe.

#### Dla początkujących
Jedyne co musimy zrobić aby zaczął działać to pobrać go ze strony  - https://addons.mozilla.org/pl/firefox/addon/https-everywhere/.  
W domyślnym trybie wymusza na określonych stronach stosowanie HTTPS zamiast nieszyfrowanego HTTP.


#### Dla zaawansowanych
W przypadku gdy chcemy zwiększyć własne bezpieczeństwo i uniemożliwić podsłuchiwanie na wszystkich stronach, możemy wymusić na dodatku, by blokował wszystkie strony oraz zasoby(obrazy czy skrypty) które korzystają z nieszyfrowanego protokołu HTTP. Należy włączyć opcję **Szyfruj wszystkie witryny**.

W przypadku gdy akurat strona na którą musimy wejść przesyłana jest bez szyfrowania i blokowana przez dodatek, możemy zrobić dla niej wyjątek poprzez naciśnięcie na przycisk **Wyłącz HTTPS Everywhere na tej stronie**

![S](https://user-images.githubusercontent.com/41945903/68146009-55d7c900-ff37-11e9-9696-44995ee0d79e.png)

### AdNauseum - Dezorientowanie reklamodawców
Jeśli tak bardzo was denerwuje to, że strony zbierają o was wszelkie dostępne informacje, możecie pomieszać nieco w ich danych używając dodatku AdNauserum, instalując go ze strony https://addons.mozilla.org/en-US/firefox/addon/adnauseam/.  
Dodatek ten bazuje na Ublock Origin dzięki czemu umożliwia blokowanie i ukrywanie reklam oraz dodatkowo symuluje kliknięcia w nie, dzięki czemu skutecznie dezorientuje szpiegów.

![S](https://user-images.githubusercontent.com/41945903/68145927-2c1ea200-ff37-11e9-8def-5638190000a9.png)

## Zaawansowane ustawienia
Znaczną ilość(jeśli nie wszystkie) opcji, które można ustawić poprzez graficzny interfejs użytkownika, można również ustawić w tekstowym panelu konfiguracyjnym przeznaczonym dla zaawansowanych użytkowników.  
Oto niektóre z ciekawszych opcji, które można  zmienić:
- `dom.popup_allowed_events = puste pole` oraz `dom.popup_maximum = 0` - Blokuje WSZYSTKIE wyskakujące okienka(dawniej i być może teraz opcja wyskakujących okienek nie blokowała wszystkich)
