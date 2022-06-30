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