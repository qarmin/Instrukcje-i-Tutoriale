
# Bezpieczny Firefox

Zapewne wielu z was spotkało podczas przeglądania internetu się ze stronami wyłudzającymi dane, wszędobylskimi reklamami, które zbierają informacje o każdym z nas oraz samoodtwarzającymi się materiałami wideo.  
Istnieje kilka dodatków i ustawień, które w znaczący sposób mogą zwiększyć bezpieczeństwo i prywatność użytkownika, spowodować szybsze otwieranie stron oraz zmniejszone użycie zasobów systemowych takich RAM czy czas CPU poprzez blokadę reklam i szpiegujących elementów.  
Niektóre porady będą opatrzone stopniem trudności dla mniej lub bardziej zaawansowanych użytkowników.

Porady zostały przygotowane w Firefoxie 70.0, dlatego niektóre elementy mogą się różnic w zależności od posiadanej wersji.

<center><img src="https://user-images.githubusercontent.com/41945903/68143010-cc24fd00-ff30-11e9-91e9-a0df62ce3bd5.png"></center>


Jeśli spodobał ci się tekst, możesz przekazać darowiznę
<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=Q8ZN556U7DGP8&source=url"><img src="https://raw.githubusercontent.com/qarmin/Godot-Poradnik/master/paypal.gif"></a>
lub zafundować mi kawę
<a href="https://ko-fi.com/qarmin"><img height="23" src="https://raw.githubusercontent.com/qarmin/Godot-Poradnik/master/buy_me_a_coffee.png"></a>

## Spis Treści
- [Kilka Zasad Bezpieczeństwa](#kilka-zasad-bezpieczeństwa)
- [DoH](#doh---szyfrowane-dns)
- [Telemetria Firefoxa](#telemetria-firefoxa)
- [Prywatna wyszukiwarka](#prywatna-wyszukiwarka)
- [Wbudowana ochrona przed śledzeniem](#wbudowana-ochrona-przed-śledzeniem)
- [Uprawnienia stron internetowych](#uprawnienia-stron-internetowych)
- [Wtyczki](#wtyczki)
 - [Ublock Origin](#ublock-origin---blokowanie-reklam)
 - [HTTPS Everywhere](#https-everywhere---szyfrowana-sieć)
 - [AdNauseum](#adnauseum---dezorientowanie-reklamodawców)
 - [Decentraleyes](#decentraleyes)
 - [Containers](#containers---zamykanie-stron-w-kontenery)
- [Zaawansowane ustawienia](#zaawansowane-ustawienia)

## Kilka zasad bezpieczeństwa
- Instaluj oprogramowanie otwartoźródłowe zamiast własnościowego gdy tylko masz taką możliwość.
- Nie otwieraj plików z nieznanych źródeł, a jeśli musisz to przeskanuj je w serwisie https://www.virustotal.com.
- Nie udostępniaj nikomu swoich danych osobowych takich jak nazwisko czy miejsce zamieszkania.
- Nie loguj się na swoje konta, na urządzeniach co do których nie masz pewności, że nie są zarażone wirusem.
- Staraj się instalować programy ze stron domowej ich producenta lub ze sklepów z oprogramowaniem
- Korzystaj z oprogramowania antywirusowego
- Nie wpisuj swoich danych logowania na stronach nieobsługujących szyfrowania.
- Stosuj unikalne hasła dla każdego serwisu, najlepiej korzystając z menedżera haseł.
- Nie wpinaj do swojego komputera pendrivów i dysków nieznanego pochodzenia

## DoH - szyfrowane DNS
DoH jest dostępną od niedawna usługą, która pozwala na szyfrowanie zapytań DNS, które to odpowiedzialne są za konwersje nazw stron np. 'facebook.com' na adres IP do nich przypisany - '31.13.81.36', dzięki czemu nikt oprócz ciebie i serwera DNS nie będzie w stanie poznać nazwy strony którą chcemy odwiedzić.

Aby je włączyć najpierw otwieramy ustawienia, przechodzimy na sam dół i w zakładce **Sieć** otwieramy naciskamy na przycisk **Ustawienia...** a w nich zaznaczamy opcję **DNS poprzez HTTPS** i zatwierdzamy to klikając na **OK**.

Domyślnym dostawcą jest Cloudlare, lecz adres serwera DNS obsługującego szyfrowanie możemy dowolnie zmieniać.
https://www.privacytools.io/providers/dns/#dns https://gist.github.com/ookangzheng/c8fba46fe1dbcc8152e3231f53f91e86

![S](https://user-images.githubusercontent.com/41945903/68145118-5a02e700-ff35-11e9-8f3b-5a494cfa15e9.png)

Aby zwiększyć jakość szyfrowania - w **about:config**, wpisz **network.trr.mode** i ustaw na **2**

![s](https://www.ghacks.net/wp-content/uploads/2018/04/firefox-network-trr-dns-over-https.png)

Aby sprawdzić czy szyfrowany DNS działa, wykonaj test na stronie https://www.cloudflare.com/ssl/encrypted-sni/ lub też https://www.dnsleaktest.com/

## Telemetria Firefoxa
Firefox domyślnie zbiera pewne informacje telemetryczne i zgłoszenia awarii, więc jeśli chcemy pomóc w jego rozwoju, możemy zaznaczyć niektóre lub wszystkie z opcji.  
Wyłączyć można je w ustawieniach Firefoxa w zakładce **Prywatność i Bezpieczeństwo** pod **Dane zbierane przez program Firefox**

![S](https://user-images.githubusercontent.com/41945903/68146588-a0a61080-ff38-11e9-882d-c97b505ef4e6.png)

Jeśli masz najnowszą wersje przeglądarki, w **about:config** wpisz **telemetry** i ustaw wszystko na **false**

## Prywatna wyszukiwarka

Domyślną wyszukiwarką w Firefoxie jest wyszukiwarka Google, która to przetwarza zapytania użytkownika tworząc na jego podstawie profil użytkownika, sprzedając te dane reklamodawcom.  

Jedną z lepszych alternatywnych wyszukiwarek jest **DuckDuckGo**, oferująca użytkownikom bezpieczne i wolne od szpiegowania przeglądanie wyników wyszukiwania.

Aby ją ustawić jako domyślną wyszukiwarkę należy przejść do ustawień i w zakładce **Wyszukiwanie** pod **Domyślna wyszukiwarka** wybrać **DuckDuckGo**

![S](https://user-images.githubusercontent.com/41945903/68150615-650f4480-ff40-11e9-84c2-2c15610ad419.png)

Alternatywnie, możesz ustawić inną prywatną wyszukiwarkę <br/>
https://addons.mozilla.org/en-US/firefox/addon/add-custom-search-engine/ <br/>

więcej instancji searx `https://searx.space/`

```
https://search.privacytools.io/?q=%s&categories=general&language=pl-PL
```
```
https://www.mojeek.com/search?q=%s
```
```
https://www.qwant.com/?q=%s
```
```
https://yandex.pl/search/?text=%s
```

## Wbudowana ochrona przed śledzeniem
Firefox oferuje domyślnie **Standardową** ochronę przed śledzącymi skryptami, ciasteczkami czy kryptowalutami.  

Możliwe jest również użycie **Ścisłej** ochrony przed śledzeniem, blokującej więcej elementów śledzących lecz niektóre elementy na stronie mogą nie ładować się poprawnie.

Trzeci tryb **Własny** umożliwia dostosowanie nam poszczególnych elementów do blokowania.

![S](https://user-images.githubusercontent.com/41945903/68152230-8de50900-ff43-11e9-92f2-968e9c5ca4bc.png)

Można wyłączyć blokowanie na konkretnej stronie, gdy powoduje ona jej błędne działanie.  
Dodatkowo w panelu po lewej stronie od paska adresu można przejrzeć wszystkie zablokowane elementy na stronie.

![S](https://user-images.githubusercontent.com/41945903/68185426-c74c6180-ffa1-11e9-8dfe-69374c9e8ac2.png)

## Uprawnienia stron internetowych
Zapewne wielu z was spotkało się z denerwującymi okienkami nt. powiadomień czy zapytania o możliwość poznania położenia użytkownika.

W ustawieniach w zakładce **Prywatność i bezpieczeństwo** pod **Uprawnienia** można prosto wyłączyć wszystkie pytania o lokalizację użytkownika, używanie kamery, mikrofonu oraz wyświetlanie powiadomień(to ostatnie zostanie prawdopodobnie domyślnie wprowadzone w wersji 72).

Aby zablokować takie zapytania, należy prawej stronie od danego uprawnienia nacisnąć na przycisk **Ustawienia...** i zaznaczyć **Blokowanie nowych próśb o ...** i nacisnąć przycisk **Zachowaj**.  
W tym samym oknie w razie potrzeby będzie można ustawić listę wyjątków dla stron.

Domyślnie Firefox blokuje autoodtwarzanie dźwięku na stronach, lecz w ustawieniach opcji **Automatyczne odtwarzanie** można zablokować również autoodtwarzające się filmiki.

![S](https://user-images.githubusercontent.com/41945903/68152232-8de50900-ff43-11e9-9f98-3011b3a87f70.png)

## Wtyczki
### Ublock Origin - Blokowanie Reklam
Zapewne wiele osób kojarzy Ublock Origin tylko jako narzędzie do blokowania reklam.  
Ublock Origin ma jednak o wiele więcej możliwości a mianowicie blokowanie skryptów JavaScript, czcionek sieciowych, ramek z informacjami o ciasteczkach i RODO, stron z wirusami i malware lub wykorzystywanych do oszukiwania ludzi.  
Czas ładowania niektórych stron, dzięki użyciu Ublock Origin, może przyspieszyć ładowanie stron nawet kilkukrotnie(najlepszym przykładem jest serwis wykop.pl - http://www.wykop.pl/artykul/5173213/test-ublock-origin-na-stronach-internetowych-zuzycie-ram-i-czas-ladowania/)

#### Dla początkujących
Na początek należy zainstalować Ublock Origin z oficjalnej strony z dodatkami Mozilli - https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/

Następnie umożliwiamy działanie dodatku w oknach prywatnych.

![S](https://user-images.githubusercontent.com/41945903/68144976-0a242000-ff35-11e9-899c-0e575b3e20f3.png)

Na sam początek pobierzemy oficjalne polskie filtry do Ublocka ze strony - https://majkiit.github.io/polish-ads-filter/, klikając przy każdym filtrze przycisk **Subskrybuj**(niektóre się dublują, więc warto przeczytać adnotacje na dole strony).

Następnie przechodzimy do ustawień dodatku do zakładki **Listy Filtrów**, gdzie znajdują się wszystkie dostępne filtry na tę chwilę.

Zalecam, dla skutecznej ochrony, włączyć wszystkie filtry takie jakie występują na obrazku.  
Należy jednak pamiętać, że im więcej filtrów, tym większe wykorzystanie pamięci ram i dlatego należy zachować ich ilości.

![S](https://user-images.githubusercontent.com/41945903/68148430-46a74a00-ff3c-11e9-97b1-ad4e71437edb.png)

W przypadku gdy dana strona nie będzie działała możemy wyłączyć na niej Ublock Origin, za pomocą tego niebieskiego przycisku, którym to możemy również ponownie włączyć ochronę przed reklamami.

![S](https://user-images.githubusercontent.com/41945903/68148620-a7368700-ff3c-11e9-9934-d52fabf0b16b.png)

#### Dla zaawansowanych
Na początek musimy odblokować ustawienia zaawansowane w Ublocku, które umożliwią dostosowanie blokowania poszczególnych elementów na stronach.  
Znajdują się one w głównym menu ustawień.

Znajdują się tu również globalne ustawienia co do blokowania filtrów kosmetycznych, elementów multimedialnych, zdalnych czcionek czy JavaScript.

W przypadku korzystania ze słabszego komputera polecam w tym miejscu włączenie globalnej blokady JavaScript, przez co strony będą się dużo szybciej pobierać i wyświetlać zużywając przy tym znacznie mniej zasobów sprzętowych. JavaScript niestety jest przez wiele stron wymagany do poprawnego działania, więc należy się uzbroić w cierpliwość przy tworzeniu listy wyjątków.

![S](https://user-images.githubusercontent.com/41945903/68149342-0d6fd980-ff3e-11e9-8d2a-a892a6e73fc1.png)

Po naciśnięciu na czerwoną tarczę dodatku, powinien nam się ukazać dużo bardziej zaawansowany panel w którym to dodano kolumny ustawień. lewa to globalna (wszystkie strony), prawa to lokalna (tylko aktualna strona).

Każdym zasobom z danej strony możemy przyporządkować stany oznaczone trzema kolorami:
- **czerwony** - oznacza  blokadę określonego elementu/zasobu z danej strony np. ustawienie czerwonej blokady na właściwości **domeny zewnętrzne** - spowoduje, że na danej stronie będą blokowane wszelkie zasoby pochodzące z zewnętrznych witryn
- **szary** - stosowany jest do neutralizacji stanu wyższego poziomu np. gdy globalnie(po lewej stronie) zablokujemy obrazki na wszystkich stronach(kolor czerwony), to możemy stworzyć wyjątek dla tej konkretnej strony oznaczając tą samą właściwość, lecz tym razem po prawej stronie.
- **zielony** - oznacza, że zasoby pochodzące z danego źródła/strony nie zostaną zablokowane ani przefiltrowane przez Ublocka. Używane są często, gdy ustawiliśmy bardzo agresywne filtry Ublocka blokujące elementy potrzebne do działania danej strony. Ale nie powinny, bo to całkowicie odblokowuje połączenia do domeny. Zielony powinien być używany do testów lub do naprawiania błędów w filtrach, które to powinny być raczej zgłaszane [autorom filtrów](https://majkiit.github.io/polish-ads-filter/) do poprawki.

![S](https://user-images.githubusercontent.com/41945903/68149440-32fce300-ff3e-11e9-94e2-5af2548d3528.png)

Ublock Origin w swojej instukcji wskazuje, że można wyłączyć skrypty i ramki z zewnętrznych witryn co powinno zwiększyć bezpieczeństwo użytkownika i nie powinno zbytnio zepsuć stron, lecz w razie konieczności można dla konkretnej strony wyłączyć to ustawienie.


Ustawienia o wyłączonych stronach są przechowywane do czasu ponownego uruchomienia przeglądarki, więc aby zapisać zmiany należy nacisnąć po lewej stronie na górze panlelu na kłódkę, a aby przywrócić je do wcześniej zapisanego stanu na gumkę.

##### Filtry kosmetyczne

Bardzo przydatną Ublocka, jest możliwość usunięcia ze strony poszczególnych elementów zwanych **elementami kosmetycznymi**. Możemy zablokować dowolny taki element bazując na jego nazwie, identyfikatorze, umiejscowieniu czy wielu innych atrybutach.

Aktywować tę funkcję możemy poprzez naciśnięcie prawym przyciskiem myszy na ekran i wybranie opcji **Zablokuj element** lub w głównym panelu pod ikoną rozszerzenia, klikając na przycisk podobny do próbnika.

![S](https://user-images.githubusercontent.com/41945903/68161262-c988ce80-ff55-11e9-828d-683a55e320a6.png)

Dobrym przykładem niech będzie strona Phoronix.com, do której to posiadam czytnik RSS newsów, dlatego panele boczne wypełnione artykułami nie są mi potrzebne.  
Zarówno stopka jak i informacje o autorze nie są mi wcale potrzebne, więc je też również usnąłem.

![S](https://user-images.githubusercontent.com/41945903/68183488-e4cafc80-ff9c-11e9-8ab2-ebc28d765755.png)

W razie potrzeby można zablokować/odblokować wyświetlanie elementów kosmetycznych, klikając na przekreślone oko w głównym panelu Ublocka. `(czasami pomaga też na "lekkie" anty adbloki)`
Listę własnych filtrów można przeglądać i modyfikować na stronie ustawień Ublocka w zakładce **Moje filtry** oraz **Moje reguły**


### HTTPS Everywhere - Szyfrowana sieć
Przez wiele lat przez sieć były wysyłane pakiety HTTP, które nie były szyfrowane, dzięki czemu możliwe było proste podsłuchiwanie komunikacji. W dzisiejszych czasach większość stron obsługuje wysyłanie danych poprzez szyfrowany HTTP. Dodatek HTTPS Everywhere został stworzony aby wymusić korzystanie z HTTPS przez serwery/strony internetowe.

#### Dla początkujących
Jedyne co musimy zrobić aby zaczął działać to pobrać go ze strony  - https://addons.mozilla.org/pl/firefox/addon/https-everywhere/.  
W domyślnym trybie wymusza na określonych stronach stosowanie HTTPS zamiast nieszyfrowanego HTTP.


#### Dla zaawansowanych
W przypadku gdy chcemy zwiększyć własne bezpieczeństwo i uniemożliwić podsłuchiwanie na wszystkich stronach, możemy wymusić na dodatku, by blokował wszystkie strony oraz zasoby(obrazy czy skrypty) które korzystają z nieszyfrowanego protokołu HTTP. Należy włączyć opcję **Szyfruj wszystkie witryny**.

W przypadku gdy akurat strona na którą musimy wejść przesyłana jest bez szyfrowania i blokowana przez dodatek, możemy zrobić dla niej wyjątek poprzez naciśnięcie na przycisk **Wyłącz HTTPS Everywhere na tej stronie**

![S](https://user-images.githubusercontent.com/41945903/68146009-55d7c900-ff37-11e9-9696-44995ee0d79e.png)

### AdNauseum - Dezorientowanie reklamodawców
Jeśli tak bardzo was denerwuje to, że strony zbierają o was wszelkie dostępne informacje, możecie namieszać nieco w ich danych używając dodatku AdNauserum, instalując go ze strony https://addons.mozilla.org/en-US/firefox/addon/adnauseam/.  
Dodatek ten bazuje na Ublock Origin dzięki czemu umożliwia blokowanie i ukrywanie reklam oraz dodatkowo symuluje kliknięcia w nie, dzięki czemu skutecznie dezorientuje szpiegów.

![S](https://user-images.githubusercontent.com/41945903/68145927-2c1ea200-ff37-11e9-8def-5638190000a9.png)

### Decentraleyes - Blokowanie śledzenia przez CDN
Decentraleyes jest dodatkiem umożliwiającym blokowanie śledzenia przez CDN(Content Networks Delivery).  
Zapobiega wysyłaniu zapytań do sieci, które mogłyby zostać użyte w celu zbierania informacji o użytkowniku, poprzez dostarczanie lokalnie zasobów CDN.

Dodatek działa od razu po instalacji i można pobrać go ze strony - https://addons.mozilla.org/pl/firefox/addon/decentraleyes/

### Containers - Zamykanie stron w kontenery
#### Dla początkujących
Najbardziej podstawowym sposobem na opakowanie strony w kontener, który uniemożliwia śledzenie poczynań użytkownika poza daną stroną jest **Facebook Container** opakowujący stronę wraz z śledzącymi skryptami i ciasteczkami.

Aby zaczął działać wystarczy zainstalować go ze strony - https://addons.mozilla.org/en-US/firefox/addon/facebook-container/

#### Dla zaawansowanych
Istnieje również nieco bardziej zaawansowana forma tego dodatku.  
Nazywa się **Firefox Multi-Account Containers** i można ją pobrać ze strony https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/.  

Dodatek pozwala użytkownikowi na stworzenie wielu kontenerów, które będą uniemożliwiały podgląd ciasteczek i danych między sobą.  
Oprócz oczywistego zysku dla prywatności, umożliwia użytkownikom łatwe organizowanie kart, przez co w tym samym oknie przeglądarki z kartami w różnych kontenerach możemy mieć dostęp np. do dwóch kont na facebooku, jednym firmowym a drugim prywatnym.

![S](https://user-images.githubusercontent.com/41945903/68333738-6d4eb780-00d9-11ea-970b-42c08f54f573.png)

### Canvas Blocker (Fingerprint Protect) - Zmiana odcisku palca

Skuteczne narzędzie, pozwalające zmienić odcisk palca przy każdym odświeżeniu odwiedzanej strony
https://addons.mozilla.org/pl/firefox/addon/canvas-blocker-no-fingerprint/

aby przetestować, wejdź na https://browserleaks.com/canvas

### ClearURLs - Optymalizator linków

Usuwanie elementów śledzących, z linków przekierowywujących pomiędzy odwiedzanymi domenami
https://addons.mozilla.org/en-US/firefox/addon/clearurls/

### Privacy Possum - Utrudnia śledzenie [*](https://github.com/ghacksuserjs/ghacks-user.js/wiki/4.1-Extensions#small_orange_diamond-dont-bother)

Prywatność Possum sprawia, że śledzenie Ciebie jest mniej opłacalne. Firmy zbierają dane o Tobie, aby stworzyć asymetrię informacji, które wykorzystują do osiągania zysków w coraz bardziej ekspansywny sposób. Ich zysk pochodzi z Twojej niekorzystnej sytuacji informacyjnej. Prywatność Possum eliminuje powszechne komercyjne metody śledzenia poprzez redukcję i fałszowanie danych zebranych przez firmy śledzące. https://addons.mozilla.org/en-US/firefox/addon/privacy-possum/

### Polska Ciasteczkowa Zgoda

Rozszerzenie automatycznie akceptujące politykę ciasteczek/RODO na stronach dostępnych w języku polskim. Stanowi ono uzupełnienie [Polskich Filtrów Rodo-Ciasteczkowych](https://subscribe.adblockplus.org/?location=https://raw.githubusercontent.com/MajkiIT/polish-ads-filter/master/cookies_filters/adblock_cookies.txt&title=Polskie%20Filtry%20RODO-Ciasteczkowe) (wchodzących też w skład **Polskich Filtrów Elementów Irytujących**) oraz wymaganej przez nie listy [I don't care about cookies](https://subscribe.adblockplus.org/?location=https://www.i-dont-care-about-cookies.eu/abp/&title=I%20dont%20care%20about%20cookies).

https://addons.mozilla.org/pl/firefox/addon/polish-cookie-consent/

### Nano Defender

[Nano Defender](https://github.com/jspenguin2017/uBlockProtector/releases) to połączenie skryptu [AAK](https://github.com/reek/anti-adblock-killer/wiki/AAK-Dead-and-Discontinued) z dodatkiem [uBlock Origin Extra](https://github.com/gorhill/uBO-Extra). Korzystając z Nano Defendera i [uBlocka Origin](https://github.com/gorhill/uBlock/releases) lub [Nano Adblockera](https://github.com/LiCybora/NanoCoreFirefox/releases) nie będziesz musiał przejmować się skryptami anty-adblock które uniemożliwiają dostępu do stron.

https://majkiit.github.io/polish-ads-filter/docs/advanced/jak-zainstalowa%C4%87-nano-defender-na-firefoksie-waterfoksie-chroperze-albo-chrome/

### Tab Stash

Bezproblemowy sposób na zapisywanie i przywracanie partii zakładek jako zakładek. Oczyść karty, oczyść swój umysł. https://addons.mozilla.org/en-US/firefox/addon/tab-stash/

### Simple Translate

Szybkie tłumaczenie wybranego tekstu na stronie internetowej. W wyskakującym okienku na pasku narzędzi możesz przetłumaczyć wprowadzony tekst. https://addons.mozilla.org/pl/firefox/addon/simple-translate/

### Search by Image
Search by Image jest rozszerzeniem do przeglądarki, które umożliwia inicjowanie wyszukiwania zwrotnego obrazu z menu kontekstowego po kliknięciu prawym przyciskiem myszy lub w pasku narzędzi przeglądarki i jest obsługiwane przez ponad 30 wyszukiwarek. https://addons.mozilla.org/en-US/firefox/addon/search_by_image/

### KeePassXC
Oficjalna wtyczka do przeglądarki dla menedżera haseł KeePassXC 
https://addons.mozilla.org/en-US/firefox/addon/keepassxc-browser/

Sprawdź czy twoje dane są bezpieczne https://haveibeenpwned.com/

### Violentmonkey
Violentmonkey zapewnia obsługę skryptów użytkownika dla przeglądarek. Działa na przeglądarkach z obsługą WebExtensions. Obsługuje większość skryptów dla Greasemonkey i Tampermonkey. https://addons.mozilla.org/pl/firefox/addon/violentmonkey/

### Stylus
Zmień swoją ulubioną witrynę internetową za pomocą Stylusa, aktywnie rozwijanego i zarządzanego przez społeczność menedżera stylów użytkownika. Łatwo instaluj niestandardowe motywy z popularnych repozytoriów online lub twórz, edytuj i zarządzaj własnymi spersonalizowanymi arkuszami stylów CSS. https://addons.mozilla.org/pl/firefox/addon/styl-us/

### Rozszerzenia specyficzne dla YouTube
https://github.com/pietervanheijningen/clickbait-remover-for-youtube<br/>
https://github.com/lawfx/YoutubeNonStop#readme<br/>
https://github.com/erkserkserks/h264ify#readme<br/>
https://github.com/ajayyy/SponsorBlock#readme


## Zaawansowane ustawienia
Znaczną ilość(jeśli nie wszystkie) opcji, które można ustawić poprzez graficzny interfejs użytkownika, można również ustawić w tekstowym panelu konfiguracyjnym przeznaczonym dla zaawansowanych użytkowników.  
Oto niektóre z ciekawszych opcji, które można zmienić na stronie `about:config` wraz z zalecanymi wartościami:
- `dom.popup_allowed_events = "puste pole"` oraz `dom.popup_maximum = 0` - Blokuje WSZYSTKIE wyskakujące okienka(korzystałem z tego dawniej ponieważ opcja wyskakujących okienek nie blokowała ich wszystkich i nie wiem jak jest teraz)
- `dom.event.contextmenu.enabled = false` - Zapobiega blokowaniu menu po naciśnięciu prawego przycisku myszy na stronie.
- `media.peerconnection.enabled = false` - Zapobiega wyciekaniu naszego adresu IP, który może zostać odczytany mimo VPN.
- `geo.enabled = false` - Wyłącza geolokalizację w której trakcie mogą zostać wysłane informacje na temat bezprzewodowych sieci, naszego adresu IP oraz ID.
- `privacy.trackingprotection.fingerprinting.enabled = true` - Utrudnia pozyskiwanie odcisku palca użytkownika.
- `privacy.trackingprotection.cryptomining.enabled = true` - Blokuje koparki kryptowalut.
- `privacy.firstparty.isolate = true` - Izoluje ciasteczka tak aby działały w obrębie jednej witryny i uniemożliwia im odczytywanie danych z innych witryn.
- `privacy.trackingprotection.enabled = true` - Wbudowania ochrona przed szpiegowaniem wykorzystująca filtry Disconnect.me.
- `media.navigator.enabled = false` - Blokuje możliwość odczytu statusu kamery i mikrofonu.
- `webgl.disabled = true` - Wyłącza WebGL, które potencjalnie może być źródłem ataków oraz może pomóc jednoznacznie identyfikować użytkownika.
- `dom.event.clipboardevents.enabled = false` - Wyłącza powiadamianie strony, gdy coś się na niej skopiuje, wklei czy wytnie.
- `network.security.esni.enabled = true` - Wsparcie szyfrowania dla SNI, które blokujące możliwość poznania stron które odwiedzamy.
- `dom.battery.enabled = false` - Blokuje możliwość odczytu informacji o baterii
- `plugins.enumerable_names = "puste pole"` - Zapobiega odczytywaniu listy dostępnych wtyczek
- `security.tls.version.min = 2` - Skuteczniejsze szyfrowanie TLS 1.2

Szablony user.js dla Firefox
- ang [ghacks-user.js](https://github.com/ghacksuserjs/ghacks-user.js) - Trwający obszerny szablon user.js służący do konfigurowania i utwardzania prywatności, bezpieczeństwa i ochrony przed pobieraniem odcisków palców Firefoksa.
- ang [pyllyukko/user.js](https://github.com/pyllyukko/user.js) - Jest to plik konfiguracyjny user.js, który utwardza ustawienia Firefoksa i czyni go bardziej bezpiecznym.

sprawdź czy twoja konfiguracja jest powtarzalna https://amiunique.org/fp
