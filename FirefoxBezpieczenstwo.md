
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
  - [uBlock Origin](#ublock-origin---blokowanie-reklam)
  - [HTTPS Everywhere](#https-everywhere---szyfrowana-sieć)
  - [LocalCDN](#localcdn---blokowanie-śledzenia-przez-cdn)
  - [Containers](#containers---zamykanie-stron-w-kontenery)
  - [Canvas Blocker](#canvas-blocker-fingerprint-protect---zmiana-odcisku-palca)
  - [Privacy Possum](#privacy-possum---utrudnia-śledzenie)
  - [Polska Ciasteczkowa Zgoda](#polska-ciasteczkowa-zgoda)
  - [Tab Stash](#tab-stash)
  - [Translate Web Pages](#translate-web-pages)
  - [Search by Image](#search-by-image)
  - [KeePassXC](#keepassxc)
  - [Violentmonkey](#violentmonkey)
  - [Stylus](#stylus)
  - [User Agent Switcher](#user-agent-switcher-and-manager)
  - [CSS Exfil Protection](#css-exfil-protection)
  - [Save To The Wayback Machine](#save-to-the-wayback-machine)
  - [FoxScroller](#foxscroller)
  - [weAutoPagerize](#weautopagerize)
  - [LibRedirect](#libredirect)
  - [Language Tool](#language-tool)
- [Zaawansowane ustawienia](#zaawansowane-ustawienia)

## Kilka zasad bezpieczeństwa
- Instaluj oprogramowanie [otwartoźródłowe](https://github.com/qarmin/Rewelacyjne-OpenSource#readme) zamiast własnościowego gdy tylko masz taką możliwość
- Nie otwieraj plików z nieznanych źródeł, a jeśli musisz to przeskanuj je w serwisie https://www.virustotal.com
- Nie udostępniaj nikomu swoich danych osobowych takich jak nazwisko czy miejsce zamieszkania
- Nie loguj się na swoje konta, na urządzeniach co do których nie masz pewności, że nie są zarażone wirusem
- Staraj się instalować programy ze stron domowej ich producenta, GitHuba lub ze sklepów z oprogramowaniem
- Na Windowsie korzystaj z oprogramowania antywirusowego i [zapory](https://github.com/henrypp/simplewall/releases) / Na [Linuxie](https://github.com/qarmin/GNU-Linux-Podstawy#readme) korzystaj z [sandboxa](https://github.com/netblue30/firejail#readme) i ufw
- Nie wpisuj swoich danych logowania na stronach [nieobsługujących szyfrowania](#https-everywhere---szyfrowana-sieć)
- Stosuj [unikalne](https://haveibeenpwned.com/Passwords) oraz [silne](https://user-images.githubusercontent.com/5884000/192772787-1ef51fcc-44a6-4817-ae93-c012896ccb31.png)
 hasła dla każdego serwisu, najlepiej korzystając z [menedżera haseł](#keepassxc)
- Nie wpinaj do swojego komputera pendrivów i dysków nieznanego pochodzenia
- Na ogólnodostępnych punktach wifi korzystaj z [vpn](https://www.privacytools.io/providers/vpn/#vpn) lub [wireguard](https://github.com/angristan/wireguard-install#readme)
- [Szyfruj](https://mhogomchungu.github.io/sirikali/#screenshots) swoje prywatne dane przed udostępnieniem w chmurze

## DoH - szyfrowane DNS
DoH jest dostępną od niedawna usługą, która pozwala na szyfrowanie zapytań DNS, które to odpowiedzialne są za konwersje nazw stron np. 'facebook.com' na adres IP do nich przypisany - '31.13.81.36', dzięki czemu nikt oprócz ciebie i serwera DNS nie będzie w stanie poznać nazwy strony którą chcemy odwiedzić.

Aby je włączyć najpierw otwieramy ustawienia, przechodzimy na sam dół i w zakładce **Sieć** otwieramy naciskamy na przycisk **Ustawienia...** a w nich zaznaczamy opcję **DNS poprzez HTTPS** i zatwierdzamy to klikając na **OK**.

Domyślnym dostawcą jest Cloudlare, lecz adres serwera DNS obsługującego szyfrowanie możemy dowolnie zmieniać.
https://www.privacytools.io/providers/dns/#dns https://gist.github.com/ookangzheng/c8fba46fe1dbcc8152e3231f53f91e86

Kierując się wyborem serwera DNS warto wybrać taki, który blokuje złośliwe oprogramowanie i/lub reklamy, np. [Cloudflare Family](https://developers.cloudflare.com/1.1.1.1/1.1.1.1-for-families), czy konfigurowalny [NextDNS](https://nextdns.io). 
NextDNS w zależności od ustawień posiada szeroki zakres możliwości, m.in. w domyślnej konfiguracji używa technologii Google Safe Browsing (bez wysyłania adresu IP do Google), mechanizmu sztucznej inteligencji wykrywającej nieznane złośliwe domeny, korzysta z zaufanych źródeł informacji o zagrożeniach: [KAD-Przekręty](https://kadantiscam.netlify.app), [CERT Polska](https://www.cert.pl/posts/2020/03/ostrzezenia_phishing/) i [innych](https://raw.githubusercontent.com/nextdns/metadata/master/security/threat-intelligence-feeds.json); pozwala na zablokowanie najczęstszych złośliwych domen nadrzędnych (np.: .xyz, .icu, .top), czy też nowo zarejestrowanych domen (poniżej 30 dni). Omawiane blokowania reklam oparte jest o rozwiązanie zewnętrznych list - AdGuard, EasyList, oisd.nl i innych.
Przykładowa konfiguracja NextDNS zalecana przez Przybornik #soo → https://soo.bearblog.dev/nextdns/

![S](https://user-images.githubusercontent.com/41945903/68145118-5a02e700-ff35-11e9-8f3b-5a494cfa15e9.png)

Aby zwiększyć skuteczność szyfrowania - w **about:config**, wpisz **network.trr.mode** i ustaw na **2**

![s](https://www.ghacks.net/wp-content/uploads/2018/04/firefox-network-trr-dns-over-https.png)

Aby sprawdzić czy szyfrowany DNS działa, wykonaj test na stronie https://www.cloudflare.com/ssl/encrypted-sni/ lub też https://www.dnsleaktest.com/


## Telemetria Firefoxa
Firefox domyślnie zbiera pewne informacje telemetryczne i zgłoszenia awarii, więc jeśli chcemy pomóc w jego rozwoju, możemy zaznaczyć niektóre lub wszystkie z opcji.  
Wyłączyć można je w ustawieniach Firefoxa w zakładce **Prywatność i Bezpieczeństwo** pod **Dane zbierane przez program Firefox**

![S](https://user-images.githubusercontent.com/41945903/68146588-a0a61080-ff38-11e9-882d-c97b505ef4e6.png)

Jeśli masz najnowszą wersje przeglądarki, w **about:config** wpisz **telemetry** i ustaw wszystko na **false**

`*` Nie wymagane w przypadku posiadania przeglądarki [LibreWolf](https://librewolf-community.gitlab.io/)

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
https://www.qwant.com/?q=%s
```

Aby na stałe odfiltrować jakąś strone z wyników wyszukiwania, użyj rozszerzenia 
https://addons.mozilla.org/en-US/firefox/addon/searchmage-search-enhancer/

Aby mieć wyniki wyszukiwania z podglądem, zainstaluj https://addons.mozilla.org/en-US/firefox/addon/searchpreview/

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
### uBlock Origin - Blokowanie Reklam
Zapewne wiele osób kojarzy uBlock Origin tylko jako narzędzie do blokowania reklam. uBlock Origin ma jednak o wiele więcej możliwości a mianowicie blokowanie skryptów JavaScript, czcionek sieciowych, ramek z informacjami o ciasteczkach i RODO, stron z wirusami i malware lub wykorzystywanych do oszukiwania ludzi. Czas ładowania niektórych stron, dzięki użyciu uBlock Origin, może przyspieszyć ładowanie stron nawet kilkukrotnie `(najlepszym przykładem jest serwis wykop.pl - http://www.wykop.pl/artykul/5173213/test-ublock-origin-na-stronach-internetowych-zuzycie-ram-i-czas-ladowania/)`

#### Dla początkujących
Na początek należy zainstalować uBlock Origin z oficjalnej strony z dodatkami Mozilli - https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/

Następnie umożliwiamy działanie dodatku w oknach prywatnych.

![S](https://user-images.githubusercontent.com/41945903/68144976-0a242000-ff35-11e9-899c-0e575b3e20f3.png)

Na sam początek pobierz oficjalne polskie filtry do uBlocka Origin ze strony - https://majkiit.github.io/polish-ads-filter/ lub https://polishannoyancefilters.netlify.app/otherfiltersforadblockers/, klikając przy każdym filtrze przycisk **Subskrybuj** `(niektóre się dublują, więc warto przeczytać adnotacje na dole strony)`

Następnie przechodzimy w ustawieniach rozszerzenia uBlock Origin do zakładki **Listy Filtrów**, gdzie znajdują się wszystkie dostępne filtry na tę chwilę. `(niektóre sekcje mogą być ukryte, ale wystarczy kliknąć + aby rozwinąć)`

Dla skutecznej ochrony, włącz wszystkie filtry takie jak występują na obrazku.

![S](https://user-images.githubusercontent.com/5884000/81131945-238e3f00-8f4d-11ea-9720-3f81a917333e.png)

Nie jest jednak zalecane dla początkujących użytkowników włączanie wszystkich list filtrów. Może to powodować problemy z działaniem stron, które trzeba będzie zgłosić opiekunom list filtrów. Można też wyłączyć uBlock Origin na stronie powodującej awarie, za pomocą tego niebieskiego przycisku pod ikoną rozszerzenia - którym to możemy również ponownie włączyć ochronę przed reklamami.

![S](https://user-images.githubusercontent.com/41945903/68148620-a7368700-ff3c-11e9-9934-d52fabf0b16b.png)

Jak zrobić kopie zapasową ustawionych filtrów https://majkiit.github.io/polish-ads-filter/docs/basic/ubo-backup/

#### Dla zaawansowanych
Na początek musimy odblokować ustawienia zaawansowane w Ublocku, które umożliwią dostosowanie blokowania poszczególnych elementów na stronach.  
Znajdują się one w głównym menu ustawień.

Znajdują się tu również globalne ustawienia co do blokowania filtrów kosmetycznych, elementów multimedialnych, zdalnych czcionek czy JavaScript.

W przypadku korzystania ze słabszego komputera polecam w tym miejscu włączenie globalnej blokady JavaScript, przez co strony będą się dużo szybciej pobierać i wyświetlać zużywając przy tym znacznie mniej zasobów sprzętowych. JavaScript niestety jest przez wiele stron wymagany do poprawnego działania, więc należy się uzbroić w cierpliwość przy tworzeniu listy wyjątków.

![S](https://user-images.githubusercontent.com/41945903/68149342-0d6fd980-ff3e-11e9-8d2a-a892a6e73fc1.png)

Po naciśnięciu na czerwoną tarczę dodatku, powinien nam się ukazać dużo bardziej zaawansowany panel w którym to dodano kolumny ustawień. Lewa to globalna `(wszystkie strony)`, prawa to lokalna `(tylko aktualna strona)`

Każdym zasobom z danej strony możemy przyporządkować stany oznaczone trzema kolorami:
- **czerwony** - oznacza  blokadę określonego elementu/zasobu z danej strony np. ustawienie czerwonej blokady na właściwości **domeny zewnętrzne** - spowoduje, że na danej stronie będą blokowane wszelkie zasoby pochodzące z zewnętrznych witryn
- **szary** - stosowany jest do neutralizacji stanu wyższego poziomu np. gdy globalnie(po lewej stronie) zablokujemy obrazki na wszystkich stronach(kolor czerwony), to możemy stworzyć wyjątek dla tej konkretnej strony oznaczając tą samą właściwość, lecz tym razem po prawej stronie.
- **zielony** - oznacza, że zasoby pochodzące z danego źródła/strony nie zostaną zablokowane ani przefiltrowane przez Ublocka. Używane są często, gdy ustawiliśmy bardzo agresywne filtry Ublocka blokujące elementy potrzebne do działania danej strony. Ale nie powinny, bo to całkowicie odblokowuje połączenia do domeny. Zielony powinien być używany do testów lub do naprawiania błędów w filtrach, które to powinny być raczej zgłaszane [autorom filtrów](https://majkiit.github.io/polish-ads-filter/) do poprawki.

![S](https://user-images.githubusercontent.com/41945903/68149440-32fce300-ff3e-11e9-94e2-5af2548d3528.png)

uBlock Origin w swojej instukcji wskazuje, że można wyłączyć skrypty i ramki z zewnętrznych witryn co powinno zwiększyć bezpieczeństwo użytkownika i nie powinno zbytnio zepsuć stron, lecz w razie konieczności można dla konkretnej strony wyłączyć to ustawienie.

Ustawienia o wyłączonych stronach są przechowywane do czasu ponownego uruchomienia przeglądarki, więc aby zapisać zmiany należy nacisnąć po lewej stronie na górze panlelu na kłódkę, a aby przywrócić je do wcześniej zapisanego stanu na gumkę.

##### Filtry kosmetyczne

Bardzo przydatną uBlocka, jest możliwość usunięcia ze strony poszczególnych elementów zwanych **elementami kosmetycznymi**. Możemy zablokować dowolny taki element bazując na jego nazwie, identyfikatorze, umiejscowieniu czy wielu innych atrybutach.

Aktywować tę funkcję możemy poprzez naciśnięcie prawym przyciskiem myszy na ekran i wybranie opcji **Zablokuj element** lub w głównym panelu pod ikoną rozszerzenia, klikając na przycisk podobny do próbnika.

![S](https://user-images.githubusercontent.com/41945903/68161262-c988ce80-ff55-11e9-828d-683a55e320a6.png)

Dobrym przykładem niech będzie strona Phoronix.com, do której to posiadam czytnik RSS newsów, dlatego panele boczne wypełnione artykułami nie są mi potrzebne.  
Zarówno stopka jak i informacje o autorze nie są mi wcale potrzebne, więc je też również usnąłem.

![S](https://user-images.githubusercontent.com/41945903/68183488-e4cafc80-ff9c-11e9-8ab2-ebc28d765755.png)

W razie potrzeby można zablokować/odblokować wyświetlanie elementów kosmetycznych, klikając na przekreślone oko w głównym panelu uBlocka Origin. `(czasami pomaga też na "lekkie" anty-adbloki)`
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

### LocalCDN - Blokowanie śledzenia przez CDN
LocalCDN jest forkiem [Decentraleyes](https://codeberg.org/nobody/LocalCDN#user-content-differences-between-localcdn-and-decentraleyes), umożliwiającym blokowanie śledzenia przez CDN(Content Networks Delivery).  
Zapobiega wysyłaniu zapytań do sieci, które mogłyby zostać użyte w celu zbierania informacji o użytkowniku, poprzez dostarczanie lokalnie zasobów CDN.

Dodatek działa od razu po instalacji i można pobrać go ze strony https://addons.mozilla.org/en-US/firefox/addon/localcdn-fork-of-decentraleyes/

### Containers - Zamykanie stron w kontenery
#### Dla początkujących
Najbardziej podstawowym sposobem na opakowanie strony w kontener, który uniemożliwia śledzenie poczynań użytkownika poza daną stroną jest **Facebook Container** opakowujący stronę wraz z śledzącymi skryptami i ciasteczkami.
https://addons.mozilla.org/en-US/firefox/addon/facebook-container/

#### Dla zaawansowanych
Istnieje również nieco bardziej zaawansowana forma tego dodatku.  
Nazywa się **Firefox Multi-Account Containers** i można ją pobrać ze strony https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers/.  

Dodatek pozwala użytkownikowi na stworzenie wielu kontenerów, które będą uniemożliwiały podgląd ciasteczek i danych między sobą.  
Oprócz oczywistego zysku dla prywatności, umożliwia użytkownikom łatwe organizowanie kart, przez co w tym samym oknie przeglądarki z kartami w różnych kontenerach możemy mieć dostęp np. do dwóch kont na facebooku, jednym firmowym a drugim prywatnym.

![S](https://user-images.githubusercontent.com/41945903/68333738-6d4eb780-00d9-11ea-970b-42c08f54f573.png)

### Canvas Blocker (Fingerprint Protect) - Zmiana odcisku palca

Skuteczne narzędzie[*](https://github.com/ghacksuserjs/ghacks-user.js/wiki/4.1-Extensions#small_orange_diamond-%EF%B8%8F-anti-fingerprinting-extensions-fk-no), pozwalające zmienić odcisk palca przy każdym odświeżeniu odwiedzanej strony.
https://addons.mozilla.org/pl/firefox/addon/canvas-blocker-no-fingerprint/

aby przetestować, wejdź na https://browserleaks.com/canvas

### ClearURLs - Optymalizator linków

Usuwanie elementów śledzących, z linków przekierowywujących pomiędzy odwiedzanymi domenami.
https://addons.mozilla.org/en-US/firefox/addon/clearurls/

### Privacy Possum - Utrudnia śledzenie

Prywatność Possum sprawia, że śledzenie Ciebie jest mniej opłacalne. Firmy zbierają dane o Tobie, aby stworzyć asymetryczną informacje, które wykorzystują do osiągania zysków w coraz bardziej ekspansywny sposób. Ich zysk pochodzi z Twojej niekorzystnej sytuacji informacyjnej. Privacy Possum eliminuje powszechne komercyjne metody śledzenia poprzez redukcję i fałszowanie danych zebranych przez firmy śledzące.
https://addons.mozilla.org/en-US/firefox/addon/privacy-possum/

Pamiętaj by nie duplikować z innymi rozszerzeniami, takimi jak: Ghostery, Disconnect i Privacy Badger

### Polska Ciasteczkowa Zgoda

Rozszerzenie automatycznie akceptujące politykę ciasteczek/RODO na stronach dostępnych w języku polskim. Stanowi ono uzupełnienie [Polskich Filtrów Rodo-Ciasteczkowych](https://subscribe.adblockplus.org/?location=https://raw.githubusercontent.com/MajkiIT/polish-ads-filter/master/cookies_filters/adblock_cookies.txt&title=Polskie%20Filtry%20RODO-Ciasteczkowe) (wchodzących też w skład **Polskich Filtrów Elementów Irytujących**) oraz wymaganej przez nie listy [I don't care about cookies](https://subscribe.adblockplus.org/?location=https://www.i-dont-care-about-cookies.eu/abp/&title=I%20dont%20care%20about%20cookies).
https://addons.mozilla.org/pl/firefox/addon/polish-cookie-consent/

### Tab Stash

Bezproblemowy sposób na zapisywanie i przywracanie partii zakładek jako zakładek. Oczyść karty, oczyść swój umysł. 
https://addons.mozilla.org/en-US/firefox/addon/tab-stash/

### Translate Web Pages

Szybkie tłumaczenie wybranego tekstu na stronie internetowej. W wyskakującym okienku na pasku narzędzi możesz przetłumaczyć wprowadzony tekst.
https://addons.mozilla.org/pl/firefox/addon/traduzir-paginas-web/

### Search by Image
Search by Image jest rozszerzeniem do przeglądarki, które umożliwia inicjowanie wyszukiwania zwrotnego obrazu z menu kontekstowego po kliknięciu prawym przyciskiem myszy lub w pasku narzędzi przeglądarki i jest obsługiwane przez ponad 30 wyszukiwarek.
https://addons.mozilla.org/en-US/firefox/addon/search_by_image/

### KeePassXC
Oficjalna wtyczka do przeglądarki dla menedżera haseł KeePassXC
https://addons.mozilla.org/en-US/firefox/addon/keepassxc-browser/

Sprawdź czy twoje dane są bezpieczne https://haveibeenpwned.com/

### Violentmonkey
Violentmonkey zapewnia obsługę skryptów użytkownika dla przeglądarek. Działa na przeglądarkach z obsługą WebExtensions. Obsługuje większość skryptów dla Greasemonkey i Tampermonkey. 
https://addons.mozilla.org/pl/firefox/addon/violentmonkey/

### Stylus
Zmień swoją ulubioną witrynę internetową za pomocą Stylusa, aktywnie rozwijanego i zarządzanego przez społeczność menedżera stylów użytkownika. Łatwo instaluj niestandardowe motywy z popularnych repozytoriów online lub twórz, edytuj i zarządzaj własnymi spersonalizowanymi arkuszami stylów CSS. 
https://addons.mozilla.org/pl/firefox/addon/styl-us/

### User Agent Switcher and Manager
Możesz zmienić ciąg znaków user-agenta, aby wskazać, że jesteś na urządzeniu mobilnym, jeśli chcesz oglądać mobilne wersje stron, aby ładowały się szybciej. 
https://addons.mozilla.org/pl/firefox/addon/user-agent-string-switcher/

Więcej ciekawych user-agentów https://www.whatismybrowser.com/guides/the-latest-user-agent/
https://www.whatismybrowser.com/detect/what-is-my-user-agent

### CSS Exfil Protection
CSS Exfil jest metodą, którą atakujący mogą wykorzystać do kradzieży danych ze stron internetowych za pomocą kaskadowych arkuszy stylów (CSS). Ten plugin odkaża i blokuje wszelkie reguły CSS, które mogą być przeznaczone do kradzieży danych. https://addons.mozilla.org/en-US/firefox/addon/css-exfil-protection/

Sprawdź podatność https://www.mike-gualtieri.com/css-exfil-vulnerability-tester

### Save To The Wayback Machine
Szybko zapisz strony internetowe na Wayback Machine w Archiwum internetowym i sprawdź, kiedy ostatnio twoja strona została zarchiwizowana. https://addons.mozilla.org/en-GB/firefox/addon/save-to-the-wayback-machine/

### FoxScroller
Ta wtyczka umożliwia automatyczne przewijanie bez użycia kółka myszy. Jeśli klikniesz.
https://addons.mozilla.org/en-US/firefox/addon/foxscroller/

### weAutoPagerize
Automatycznie wstawia następną stronę[*](https://github.com/wantora/weautopagerize#compatibility-table).
https://addons.mozilla.org/en-US/firefox/addon/weautopagerize/

### LibRedirect
Proste rozszerzenie internetowe, które przekierowuje Twittera, YouTube'a, Instagrama i Map Google do alternatyw przyjaznych dla prywatności. https://addons.mozilla.org/pl/firefox/addon/libredirect/

### Language Tool
Wielojęzyczne narzędzie do sprawdzania gramatyki, stylu i pisowni.
https://addons.mozilla.org/pl/firefox/addon/languagetool/

### Rozszerzenia specyficzne dla YouTube
https://github.com/zerodytrash/Simple-YouTube-Age-Restriction-Bypass#readme<br/>
https://github.com/pietervanheijningen/clickbait-remover-for-youtube#readme<br/>
https://github.com/lawrencehook/remove-youtube-suggestions#readme<br/>
https://github.com/Anarios/return-youtube-dislike#readme<br/>
https://github.com/lawfx/YoutubeNonStop#readme<br/>
https://github.com/ajayyy/SponsorBlock#readme<br/>
https://github.com/amitbl/blocktube#readme

## Zaawansowane ustawienia
Znaczną ilość(jeśli nie wszystkie) opcji, które można ustawić poprzez graficzny interfejs użytkownika, można również ustawić w tekstowym panelu konfiguracyjnym przeznaczonym dla zaawansowanych użytkowników.  
Oto niektóre z ciekawszych opcji, które można zmienić na stronie `about:config` wraz z zalecanymi wartościami:
- `dom.popup_allowed_events = "puste pole"` oraz `dom.popup_maximum = 0` - Blokuje WSZYSTKIE wyskakujące okienka(korzystałem z tego dawniej ponieważ opcja wyskakujących okienek nie blokowała ich wszystkich i nie wiem jak jest teraz)
- `network.IDN_show_punycode = true` - Zapobiega podszyciu się domeny przy pomocy homografów IDN (zmienia wyświetlanie adresu).
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
- `security.tls.version.min = 2` - Skuteczniejsze szyfrowanie TLS 1.2 (może powodować problemy ze stronami które nie wspierają silnego szyfrowania tls 1.2)

Szablony dla Firefox
- ang [arkenfox user.js](https://github.com/arkenfox/user.js) - Obszerny szablon user.js służący do konfigurowania i utwardzania prywatności, bezpieczeństwa i ochrony przed pobieraniem odcisków palców Firefoksa.

sprawdź czy twoja konfiguracja jest powtarzalna https://amiunique.org/fp
