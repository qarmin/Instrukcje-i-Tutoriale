# Bezpieczny Firefox
Zapewne wielu z was spotkało podczas przeglądania internetu się ze stronami w internecie wyłudzającymi dane, wszędobylskimi reklamami, które oraz wyskakującymi okienkami.
Istnieje kilka dodatków i ustawień, które w znaczący sposób mogą zwiększyć bezpieczeństwo i prywatność użytkownika, spowodować szybsze otwieranie stron oraz zmniejszone użycie zasobów systemowych takich RAM czy czas CPU.
Niektóre porady będą opatrzone stopniem trudności dla mniej lub bardziej zaawansowanych użytkowników.

Porady zostały przygotowane w Firefoxie 70.0

## Spis Treści

## Kilka zasad bezpieczeństwa
Instaluj oprogramowanie otwartoźródłowe zamiast własnościowego gdy tylko masz taką możliwość.
Nie otwieraj plików z nieznanych źródeł, a jeśli musisz to przeskanuj je w serwisie Virustotal.com.
Nie udostępniaj nikomu swoich danych osobowych takich jak nazwisko czy miejsce zamieszkania.
Nie loguj się na swoje konta, na urządzeniach co do których nie masz pewności, że nie są zarażone wirusem.
Staraj się instalować programy ze stron domowej ich producenta.
Korzystaj z oprogramowania antywirusowego
Nie wpisuj swoich danych logowania na stronach nie obsługujących szyfrowania.
Stosuj unikalne hasła dla każdego serwisu, najlepiej korzystając z menedżera haseł




## Wtyczki
### Ublock Origin - Blokowanie Reklam
Zapewne wiele osób kojarzy Ublock Origin tylko jako narzędzie do blokowania reklam.
Jednak umożliwia o wiele więcej, a mianowicie blokowanie skryptów JavaScript, czcionek sieciowych, ramek z informacjami o ciasteczkach i RODO czy stron z wirusami i malware lub wykorzystwanych do oszukiwania ludzi.

**Dla początkujących**
Na początek należy zainstalować Ublock Origin z oficjalnej strony z dodatkami Mozilli - https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/

Następnie umożliwiamy działanie dodatku w oknach prywatnych.



Na sam początek pobierzemy oficjalne polskie filtry do Ublocka ze strony - https://github.com/MajkiIT/polish-ads-filter#about, klikając przy każdym filtrze przycisk **Subskrybuj**.

Następnie przechodzimy do ustawień dodatku do zakładki **Listy Filtrów**, gdzie znajdują się wszystkie dostępne filtry na tę chwilę.

Zalecam zaznaczenie dla skutecznej ochrony włączyć filtry takie jakie występują na obrazku.
Im więcej filtrów, tym większe wykorzystanie procesora, dlatego należy zachować umiar w ich włączaniu.
<zdjęcię gdzie są ustawienia>

W przypadku gdy dana strona nie będzie działała możemy wyłączyć na niej Ublock Origin, za pomocą tego niebieskiego przycisku, którym to możemy ponownie włączyć ochronę przed reklamami.

Domyślnie ustawienia o wyłączonych stronach są przechowywane do czasu ponownego uruchomienia przeglądarki, więc aby zapisac zmiany nalez← nacinąć na kłódkę, a aby je usunąć na gumkę.

**Dla zaawansowanych**
Na początek odblokujmy w Ublocku ustawienia zaawansowane w Ublocku.

Powinna pojawić nam się plansza, która to przedstawia po swojej lewej stronie ustawienia globalne, które tyczą się wszystkich witryn, oraz ustawienia lokalne używane jedynie na tej konkretnej stronie.



Ublock w swojej instukcji podpowiada, by wyłączyć skrypty i ramki z zewnętrzych witryn co powinno zwiększyć bezpieczeństwo użytkownika i nie powinno zbytnio zepsuć stron, w razie


Ublock Origin umożliwia całkowite wyłączenie JavaScript, dzięki czemu strony powinny ładować się bardzo szybko, zużywać bardzo mało pamięci i czasu procesora, lecz znaczna część z nich może nie wyświetlać się prawidłowo.

### HTTPS Everywhere - Szyfrowana sieć
Przez wiele lat przez sieć były wysałne pakiety HTTP, które nie były szyfrowane, dzięki czemu możliwe było proste podsłuchiwanie komunikacji. W dzisiejszych czasach większość stron obsługuje wysyłanie danych poprzez szyfrowany HTTP, lecz część z nich ciągle używa domyślnie HTTP. Dodatek HTTPS Everywhere został stworzony aby wymusić korzystanie z HTTPS przez serwery/strony internetowe.

**Dla początkujących**
Jedyne co musimy zrobić aby zaczął działać to pobrać go ze strony  -


**Dla zaawansowanych**
W przypadku gdy chcemy zwiększyć własne bezpieczeństwo i uniemożliwić podsłuchiwanie na wszystkich stronach, możemy wymusić na dodatku, by blokował wszystkie strony które korzystają z nieszyfrowanego protokołu.

W przypadku gdy akurat stona na którą musimy wejść przesyłana jest bez szyfrowania i blokowana przez dodatek, możemy zrobić dla niej wyjątek poprzez naciśnięcie na przycisk:


### AdNauseum - Dezorientowanie reklamodawców
Jeśli tak bardzo was denerwuje to, że strony zbierają o was wszelkie dostępne dane, możecie pomieszać nieco w ich danych używając dodatku AdNauserum, instalując go ze strony https://addons.mozilla.org/en-US/firefox/addon/adnauseam/.
Dodatek ten bazuje na Ublock Origin oraz dodatkowo symuluje kliknięcia w reklamy, dzięki czemu skutecznie dezorientuje szpiegów.

### DOH - szyfrowanie DNS
Dostępną od niedawna DoH, pozwala na szyfrowanie zapytań DNS, które to odpowiedzialne za konwersję nazwy strony np. 'facebook.com' na jej adres IP - '1.1.1.1'.

W firefoxie bardzo łatwo jest to włączyć.
Najpierw włączamy ustawienia, potem przechodzimy na sam dół i w zakładce **Sieć** zaznaczamy opcję ****.
Jeśli chcemy możemy zmienić adres domyślnego DNS, na taki, który umożliwia szyfrowanie zapytań.
### Decentraleyes - Zapobieganie szpiegowaniu przez CDN
