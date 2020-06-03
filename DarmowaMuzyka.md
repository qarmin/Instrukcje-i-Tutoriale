# Jak pobierać muzykę z sieci za darmo?

Zapewne wielu z was jest zdenerwowana na Spotify z powodu dodawania niechcianych playlist związanych z niedawnymi wydarzeniami, niemożnością przeglądnięcia kodu źródłowego aplikacji co zagraża waszej prywatności oraz bezpieczeństwu i w końcu ograniczonej możliwości korzystania z muzyki offline(ciągle potrzebna jest aplikacja Spotify, którą trzeba uruchomić przynajmniej raz na 30 dni).

Rozwiązaniem tych problemów może być dla wielu skorzystanie z usługi `deezer`, przy pomocy której będziemy mieli możliwość pobrania plików muzycznych w formacie MP3 oraz FLAC i korzystania z nich tam gdzie do tej pory nie mogliśmy korzystać ze Spotify - radia samochodowe itp.

1. Zainstaluj Dockera - umożliwi to proste uruchomienie serwera bez konieczności zmiany konfiguracji komputera(dostępny jest również zwykły skrypt)

W Ubuntu 20.04 wystarczy uruchomić komendę `apt install -y docker-compose docker.io`

W starszych wersjach Ubuntu lub Linux Mint należy wykonać następujące polecenia:
```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

W przypadku problemów lub posiadania innej dystrybucji należy przejrzeć dokumentację - https://docs.docker.com/engine/install/ubuntu/

Na Windowsie i macOS należy zainstalować i skonfigurować Docker Desktop lub można też skorzystać z Dockera poprzez WSL 2


2. Zarejstruj i zaloguj się na stronie  https://www.deezer.com - W przeciwieństwie do Spotify umożliwia ona pobieranie plików muzycznych w formacie mp3 oraz flac.

3. Po zalogowaniu na stronie głównej naciśnij F12(w Firefoxie) i przejdź do zakładki Storage oraz wyszukaj i zapisz do pliku tekstowego wartość zmiennej `arl`(dość długa około 195 znaków).

![Heheszki](https://user-images.githubusercontent.com/41945903/83638574-a5ec3c00-a5a9-11ea-8002-2ff6f295842c.png)

4. Następnie w dowolnym miejscu stwórz plik konfiguracyjny `docker-compose.yml` i wklej tę zawartość do pliku.

```
version: '3.7'

services:
  deemix:
    container_name: deemix
    image: bocki/deemix
    restart: unless-stopped
    ports:
      - 9666:9666
    environment:
      - PUID=1000
      - PGID=1000
      - ARL=AAAAAAAAAAAAAAAAAAAAAAAAAA
    volumes:
      - /home/rafal/Place:/downloads
      - deemix-config-data:/config


  deemix-data:
    name: deemix-data
  deemix-config-data:
    name: deemix-config-data
```

5. Musisz w tym pliku zmienić `AAAAAAAAA` na wcześniej zapisany tekst arl, a zamiast `/home/rafal/Place` wybrać ścieżkę do której mają się zapisywać nowo pobrane piosenki.

6. Następnie będąc dokładnie w tym samym folderze możesz uruchomić serwer korzystając z polecenia `docker-compose up -d`

7. Po około 1 minucie(może trwać to trochę dłużej) można skorzystać z serwera pod adresem `http://localhost:9666/`

![Heheszki](https://user-images.githubusercontent.com/41945903/83638000-c36cd600-a5a8-11ea-92a2-b7c1249af4c4.png)

8. Można od tej pory pobierać dowolną muzykę do słuchania jej bez konieczności posiadania jakiejkolwiek aplikacji.
