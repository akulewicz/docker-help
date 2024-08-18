Oto krótka ściągawka z poleceń Docker, które mogą być przydatne do obsługi projektów opartych na PHP, MySQL oraz stosie LAMP (Linux, Apache, MySQL, PHP):

### Podstawowe polecenia Docker

1. **Budowanie i uruchamianie kontenerów**:
   - **Uruchomienie kontenerów z pliku `docker-compose.yml`**:
     ```bash
     docker-compose up -d
     ```
     `-d` uruchamia kontenery w tle (w trybie detached).

   - **Zbudowanie i uruchomienie kontenerów na nowo**:
     ```bash
     docker-compose up --build -d
     ```
     Buduje ponownie obrazy przed uruchomieniem kontenerów.

2. **Zatrzymywanie i usuwanie kontenerów**:
   - **Zatrzymanie uruchomionych kontenerów**:
     ```bash
     docker-compose stop
     ```

   - **Zatrzymanie i usunięcie wszystkich kontenerów oraz powiązanych z nimi sieci**:
     ```bash
     docker-compose down
     ```

   - **Zatrzymanie i usunięcie kontenerów, sieci oraz woluminów**:
     ```bash
     docker-compose down -v
     ```
     `-v` usuwa również przypisane woluminy.

3. **Sprawdzanie statusu kontenerów**:
   - **Wyświetlenie listy uruchomionych kontenerów**:
     ```bash
     docker ps
     ```

   - **Wyświetlenie wszystkich kontenerów, w tym zatrzymanych**:
     ```bash
     docker ps -a
     ```

4. **Dostęp do wnętrza kontenera**:
   - **Wejście do terminala kontenera (np. PHP)**:
     ```bash
     docker exec -it <nazwa_kontenera> bash
     ```
     Zamień `<nazwa_kontenera>` na rzeczywistą nazwę kontenera.

   - **Uruchomienie klienta MySQL wewnątrz kontenera**:
     ```bash
     docker exec -it <nazwa_kontenera_db> mysql -u root -p
     ```
     Zostaniesz poproszony o hasło do użytkownika `root`.

5. **Zarządzanie woluminami**:
   - **Wyświetlenie listy wszystkich woluminów**:
     ```bash
     docker volume ls
     ```

   - **Usunięcie nieużywanych woluminów**:
     ```bash
     docker volume prune
     ```
     Usuwa wszystkie woluminy, które nie są powiązane z żadnym kontenerem.

### Obsługa Specyficzna dla LAMP

1. **Przeładowanie konfiguracji Apache (bez restartu kontenera)**:
   - **Wejście do kontenera z Apache i przeładowanie**:
     ```bash
     docker exec -it <nazwa_kontenera> apachectl -k graceful
     ```

2. **Zarządzanie bazą danych MySQL**:
   - **Tworzenie nowej bazy danych**:
     ```sql
     CREATE DATABASE nazwa_bazy_danych;
     ```
   - **Importowanie bazy danych**:
     ```bash
     docker exec -i <nazwa_kontenera_db> mysql -u root -p<hasło> < nazwa_bazy_danych < /ścieżka/do/pliku.sql
     ```

3. **Praca z logami**:
   - **Podgląd logów Apache**:
     ```bash
     docker logs <nazwa_kontenera>
     ```

   - **Podgląd logów w czasie rzeczywistym**:
     ```bash
     docker logs -f <nazwa_kontenera>
     ```
     `-f` pozwala na śledzenie logów w czasie rzeczywistym.

4. **Restartowanie poszczególnych usług**:
   - **Restart konkretnego kontenera (np. Apache)**:
     ```bash
     docker-compose restart <nazwa_usługi>
     ```
     Zamień `<nazwa_usługi>` na rzeczywistą nazwę usługi, np. `web`.

5. **Usunięcie pojedynczego kontenera**:
   - **Zatrzymanie i usunięcie kontenera**:
     ```bash
     docker rm -f <nazwa_kontenera>
     ```
     `-f` wymusza usunięcie działającego kontenera.

### Optymalizacja pracy

1. **Czyszczenie zbędnych obrazów i kontenerów**:
   - **Usunięcie wszystkich nieużywanych obrazów, kontenerów, woluminów i sieci**:
     ```bash
     docker system prune -a
     ```

2. **Aktualizacja kontenerów**:
   - **Pobranie najnowszych wersji obrazów i aktualizacja kontenerów**:
     ```bash
     docker-compose pull && docker-compose up -d --build
     ```

Ta ściągawka powinna pomóc w zarządzaniu projektami LAMP za pomocą Dockera, pozwalając na szybkie wykonywanie najczęstszych operacji.
