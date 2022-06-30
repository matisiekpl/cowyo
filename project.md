# Integracja projektu Open Source z systemem DevOps

## Wybór projektu
Wybrany projekt to cowyo. Cowyo to aplikacja internetowa napisana w Go, która umoliżliwa tworzenie i edytowanie notatek osobistych za pośrednictwem interfejsu graficznego w przeglądarce. Program udostępnia port HTTP (pod spodem TCP).

### Licencja projektu
Licencja projektu to MIT License. Umożliwia ona swobodne użycie aplikacji do działań komercyjnych.

## Budowa i testy uruchomione lokalnie
Aplikacja Go wymaga kompilacji
```bash
export GO111MODULE=on
go get -v # Instalacja zależności
go test ./... -v # Uruchomienie testów automatycznych
go build -o cowyo # Kompilacja do pliku binarnego cowyo
```

## Konteneryzacja
Autorzy projektu przygotowali plik Dockerfile, na podstawie którego można zbudować obraz kontenera.
```bash
docker build -t cowyo .
```
Uruchlomienie aplikacji:
```bash
docker run -p 8050:8050 cowyo
```
Następnie można udać się do przeglądarki pod adres `http://localhost:8050`, by zobaczyć interfejs graficzny.
Projekt cowyo nie przewiduje użycia za pośrednictwem kodu/terminala.

# Instancja Jenkins
## Instalacja
W celu zainstalowania Jenkinsa, można użyć oficjalnego pakietu WAR.
By uruchomić Jenkinsa, należy wydać następujące polecenia:
```bash
mkdir jenkins
cd jenkins
wget https://get.jenkins.io/war-stable/2.346.1/jenkins.war
java -jar jenkins.war
```

## Wstępna konfiguracja
Po zainstalowaniu Jenkinsa, pojawi się konfigurator wstępny.
![klucz](screenshots/klucz.png)
Należy podać hasło aktywacyjne, można je odczytać wywołując polecenie: `cat /Users/user/.jenkins/secrets/initialAdminPassword`
![klucz](screenshots/wtyczki.png)
Można też zainstalować sugerowane wtyczki
![klucz](screenshots/uzytkownik.png)
Oraz utworzyć pierwszego użytkownika

## Konfiguracja bezpieczeństwa

## Utworzenie projektu
Tworzymy projekt, klikając przycisk "Nowy projekt" w panelu głównym
![img.png](screenshots/projekt.png)
Następnie ustawiamy źródło definicji pipeline jako Jenkinsfile pobrany z systemu kontroli wersji i klikamy "Zapisz"
![img.png](screenshots/scm.png)


Po utworzeniu projektu na Jenkinsie, możemy uruchomić build'a:
![img.png](screenshots/run.png)

Podczas uruchamiania pojawi się też checkbox pytający dewelopera czy chce opublikować pakiet w Docker Hubie:

![img.png](screenshots/should_publish.png)