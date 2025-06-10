
# Szybkie podsumowanie

### 1. Wprowadzenie do baz danych

- **Baza danych (BD)**: uporządkowany zbiór danych odwzorowujący rzeczywistość, trwały, spójny, bezpieczny, współdzielony.
- **System Zarządzania Bazą Danych (SZBD)**: oprogramowanie do tworzenia, modyfikowania i zarządzania bazami danych.
- **Model danych**: abstrakcja rzeczywistości (domeny, związki, operacje).
- **Transakcje i ACID**:  
    - Atomowość – całość albo nic,
    - Coherence – spójność danych,
    - Izolacja – brak wzajemnego wpływu,
    - Durability – trwałość po zatwierdzeniu.

### 2. Modele danych

- Model konceptualny (ERD): encje, atrybuty, związki, kardynalności.
- Model logiczny: encje = tabele, atrybuty = kolumny, związki = klucze obce.
- Model fizyczny: sposób zapisu na dysku (indeksy, pliki, rekordy).
- Typy relacji: 1:1, 1:N, N:M, self-relation.
- Słaba encja: nie ma własnego identyfikatora – zależy od encji nadrzędnej.


### 3. Relacyjny model danych (SQL)

- **Pojęcia**:
    - Atrybut = kolumna, krotka = wiersz, relacja = tabela.
    - Klucz główny (PK), obcy (FK), dziedzina.
- **Zasady tabeli**:
    - Unikalność, brak powtórzeń, atomowość danych.
- **Integralność**:
    - Primary Key, Foreign Key, NOT NULL, UNIQUE, CHECK.
    - Referencyjna integralność: zachowanie spójności przy aktualizacji/usuwaniu (Restrict, Cascade, Set Null, Set Default).
- **Schemat relacyjny**: tabele, widoki, procedury, wyzwalacze.



### 4. Języki baz danych (SQL)

- **DDL** (Data Definition Language): CREATE, ALTER, DROP.
- **DML** (Data Manipulation Language): SELECT, INSERT, UPDATE, DELETE.
- **DCL** (Data Control Language): GRANT, REVOKE.
- Transakcyjność: COMMIT, ROLLBACK, LOCK (S – współdzielony, X – wyłączny).


### 5. Transakcyjność i współbieżność

- **Strict 2PL**: transakcje blokują dane do końca (pełna izolacja).
- **Weak 2PL**: możliwe wcześniejsze zwolnienie blokady odczytu.
- **Poziomy izolacji** (SQL):
    - READ UNCOMMITTED: widoczne niezatwierdzone zmiany.
    - READ COMMITTED: brak brudnych odczytów.
    - REPEATABLE READ: brak niepowtarzalnych odczytów.
    - SERIALIZABLE: pełna izolacja (brak fantomów).
- **Anomalie**: Dirty Read, Lost Update, Nonrepeatable Read, Phantom.


### 6. Architektury i typy baz danych

- Architektury:
    - Jednopoziomowa, klient-serwer, trójwarstwowa, rozproszona.
- Rodzaje baz danych:
    - Relacyjne (SQL) – tabele, np. MySQL, PostgreSQL.
    - Nierelacyjne (NoSQL) – dokumentowe (MongoDB), grafowe, kolumnowe, klucz-wartość.
    - Obiektowe, obiektowo-relacyjne, XML, hierarchiczne, sieciowe, kartotekowe.


### 7. Systemy zarządzania bazami danych (SZBD)

- **Oracle**: potężne, drogie, SQL i NoSQL.
- **MS SQL** Server: dobra integracja z Windows, wysoki koszt.
- **MySQL**: darmowy, szeroko wspierany, ale z ograniczeniami.
- **PostgreSQL**: open-source, relacyjno-obiektowy, wolniejszy w odczycie.


### 8. Modelowanie danych (ERD)

- Etapy:
    1.	Identyfikacja encji i kluczy.
    2.	Atrybuty (proste/złożone, wyliczane).
    3.	Związki (1:1, 1:N, N:M, opcjonalność).
    4.	Normalizacja danych – unikanie redundancji.
- Diagram ERD: graficzna reprezentacja encji i ich relacji.


### 9. NoSQL – bazy nierelacyjne

- **Rodzaje**:
    - Dokumentowe (MongoDB),
    - Grafowe (Neo4j),
    - Kolumnowe (Cassandra),
    - Klucz-wartość (Redis).
- **Cechy**: brak schematu, elastyczność, skalowalność.
- **Zastosowanie**: Big Data, IoT, systemy rozproszone.
- Brak transakcyjności ACID → zamiast tego CAP i BASE (Eventually Consistent).


### 10. Administracja SQL/NoSQL

- **SQL**: tworzenie ról, użytkowników, backup, restore, eksport/import.
- **NoSQL**: zarządzanie kolekcjami, użytkownikami, indeksami.
- **Bezpieczeństwo**: autoryzacja, szyfrowanie, backup.

# ACID (dla baz SQL)

## Cechy transakcji (ACID)

- **Atomowość** - każda transakcja jest traktowana jako pojedyncza „jednostka”, która albo cała kończy się z sukcesem, albo cała się nie udaje
- **Spójność** - transakcja może tylko przenieść bazę danych z jednego
prawidłowego stanu do drugiego, zachowując niezmienniki bazy
danych: wszelkie dane zapisane w bazie danych muszą być
prawidłowe zgodnie ze wszystkimi zdefiniowanymi regułami
- **Izolacja** - równoczesne wykonywanie transakcji pozostawia bazę
danych w takim samym stanie, jaki zostałby uzyskany, gdyby
transakcje były wykonywane sekwencyjnie
- **Trwałość** - raz zatwierdzona transakcja pozostanie zatwierdzona
nawet w przypadku awarii systemu (jest zapisywana w pamięci
nieulotnej)

## Mechanizmy SZBD zapewniające ACID
- **Blokady** (zamki) (ang. Lock) zakładane na obiekty –
ograniczające/uniemożliwiające działanie innych transakcji na
zablokowanym obiekcie
- **Dziennik** (ang. Log) - zapisywanie wszystkich zmian w bazie danych do
specjalnego dziennika (logu), aby w razie potrzeby:
    - Wycofać wprowadzone zmiany dla transakcji niezatwierdzonej
    - Odtworzyć aktualny, spójny stan bazy danych w przypadku awarii
- **Wielowersyjność** - możliwość odczytywania danych zmienianych
równocześnie przez inne transakcje w takiej postaci, w jakiej istniały w
określonych momentach w przeszłości
- **Kopia zabezpieczająca bazy danych** (ang. Backup) - wykonywana w
regularnych odstępach czasu
    - W przypadku awarii danych na dysku pozwala przywrócić spójny stan bazy danych
- **Zapasowa instalacja** tej samej bazy danych utrzymywana w odległym węźle w trybie stand-by
    - Gotowość do zastąpienia głównej bazy danych

## Atomowość transakcji
- Transakcja może zakończyć się uzyskując:
    - **Zatwierdzenie** (**COMMIT**) – po zakończeniu wszystkich swoich
    akcji
    - **Samo-wycofanie** (**ROLLBACK**) - anulowaniem wszystkich
    wykonanych akcji
    - **Przerwanie** przez SZBD (ang. **Abort**) a następnie transakcja jest
    wycofana i restartowana (np. z powodu zakleszczenia)
    - **Przerwanie** z powodu awarii serwera lub dysku - po
    podniesieniu systemu po awarii dotychczasowe zmiany
    wprowadzone przez transakcję zostają na chwilę przywrócone
    a następnie wycofane przez system
- Cała transakcja zostaje wykonana albo żadna jej część
nie zostaje wykonana
- SZBD zapisuje wszystkie wykonywane akcje w dzienniku
transakcji (logu) tak aby możliwe były jej wycofanie czyli
anulowanie wszystkich jej akcj

## Blokady i zakleszczenia

- **Blokady** (zamki, ang. locks) zakładane na obiekty to podstawowy
mechanizm zapobiegający konfliktom przy współbieżnie
wykonywanych transakcjach są blokady (nazywane też zamkami)
- Rodzaje blokad:
    - **Współdzielona**, typu **S (ang. shared lock)** - daje transakcji
    **współdzielony dostęp do zasobu**, na przykład, kilka transakcji może
    jednocześnie odczytywać wiersze tej samej tabeli. Jeśli transakcja
    zakłada współdzieloną blokadę, inne transakcje też mogą założyć
    współdzieloną blokadę, ale nie mogą założyć blokady drugiego
    rodzaju, to jest wyłącznej blokady
    - **Wyłączna**, typu **X (ang. exclusive lock)** - daje transakcji **wyłączne prawo do wprowadzania zmian** obiektu. Tylko jedna transakcja może mieć
    założoną wyłączną blokadę na obiekcie i w tym czasie nie może być na
    nim założonej żadnej innej blokady nawet współdzielonej
- Dopuszczana jest operacja podwyższenia blokady przez
transakcję. Mianowicie, transakcja, która założyła blokadę S,
może ją zmienić na X, pod warunkiem, że na obiekcie nie ma
założonej innej blokady S

## Protokół ścisłego blokowania dwufazowego (Strict 2PL)

1. Każda transakcja musi uzyskać blokadę S (współdzieloną) na obiekcie
przed odczytem oraz blokadę X (wyłączną) na obiekcie przed zapisem
2. Jeśli transakcja trzyma blokadę X na obiekcie, żadna inna transakcja nie
może założyć żadnej blokady (ani typu S ani X) na tym obiekcie
3. Jeśli transakcja trzyma blokadę S na obiekcie, żadna inna transakcja nie
może założyć blokady X na tym obiekcie
4. Gdy transakcja nie może założyć blokady na obiekcie, może ustawić się w
kolejce oczekujących transakcji stowarzyszonej z tym obiektem
5. Wszystkie blokady trzymane przez transakcję są zwalniane jednocześnie,
w chwili gdy transakcja kończy się (wycofaniem lub zatwierdzeniem)  

- Dwie fazy działania każdej transakcji związane z blokadami:
    - Transakcja zakłada blokady i dokonuje wymaganych odczytów i zapisów na obiektach,
    na których założyła blokadę
    - Transakcja wykonuje COMMIT/ROLLBACK jednocześnie zwalniając wszystkie założone
    blokady

## Protokół ścisłego blokowania dwufazowego (Strict 2PL)

- Protokół **Strict-2PL** zapewnia:
    - Niezatwierdzony odczyt nie może zajść, ponieważ aby
    zmienić wartość obiektu transakcja musi założyć blokadę X
    i od tej chwili do momentu zwolnienia blokady na koniec
    wykonywania transakcji żadna inna transakcja nie ma
    dostępu do zablokowanego obiektu (nawet w celu jego
    odczytania)
    - Niepowtarzalny odczyt nie może zajść, ponieważ przy
    pierwszym odczycie transakcja zakłada blokadę S (lub X) na
    odczytywany obiekt i zwalnia tę blokadę dopiero na sam
    koniec. W międzyczasie żadna inna transakcja nie uzyska
    blokady X na tym obiekcie aby go zmienić
    - Nadpisywanie niezatwierdzonych zmian nie może mieć
    miejsca, ponieważ zapisanie obiektu wymaga
    wcześniejszego założenia blokady X i do czasu zakończenia
    transakcji żadna inna transakcja nie może ani odczytać ani
    zapisać tego obiektu

- Protokół **Weak Strict-2PL**:
    - Transakcja nie może wcześniej zwolnić żadnej blokady
    X, ale w każdej chwili może zwolnić założoną do
    odczytu blokadę S
    - Przy użyciu tego protokołu odczyt danych może być
    niepowtarzalny dla transakcji - po zwolnieniu przez
    nią blokady S, inna transakcja może założyć blokadę X,
    zmienić dane i zatwierdzić zmiany

## Zakleszczenia

- **Zakleszczenie** (ang. deadlock) - cykl transakcji oczekujących
wzajemnie na zwolnienie blokady przez inną transakcję w
cyklu
- Pojawia się, kiedy dwie lub więcej transakcji wzajemnie
blokują sobie obiekty, które są im potrzebne do
kontynuowania operacji
- Przykład: transakcja T1 nałożyła blokadę na obiekt A, a
transakcja T2 - na obiekt B. W kolejnym kroku T1 chce
założyć blokadę na obiekt B, a T2 na obiekt A. Obie
transakcje przestają działać, oczekując na zwolnienie
blokady przez drugą transakcję.
- Sposoby radzenia sobie z zakleszczeniami:
    - Zapobieganie (przez przyporządkowywanie transakcjom priorytetów
    w zakładaniu blokad)
    - Wykrywanie cyklu oczekiwań na założenie blokady
    - Ustalenie limitu oczekiwania na blokadę (ang. Timeout)


## Anomalie transakcji

- **Brudny odczyt** (ang. **Dirty read** / Uncommitted dependency) - Transakcja
odczytuje dane, które nie zostały jeszcze zatwierdzone (COMMIT). Jeśli inne
transakcja ostatecznie wycofa zmiany (ROLLBACK) wtedy pierwsza transakcja
może odczytać zmiany, które nigdy nie istniały
- **Utracona modyfikacja** (ang. Lost update) – Sytuacja, w której więcej niż
jedna transakcja czyta te same dane. Modyfikacje wykonane później przez
pierwszą transakcję zostaną nadpisane przez inną transakcję nieświadomą
zmian, które nastąpiły
- **Niepowtarzalny odczyt** (ang. Nonrepeatable read / Inconsistent Analysis) -
Transakcja odczytuje dwa razy ten sam wiersz, ale dostaje inne dane za
każdym razem. Przykład: transakcja 1 czyta wiersz. Transakcja 2 modyfikuje
lub usuwa ten wiersz oraz zostaje zakończona (COMMIT). Jeśli transakcja 1
odczyta teraz ten wiersz to dostanie inne dane lub odkryje, że wiersz już nie
istnieje.
- **Fantomy** (ang. Phantoms) - Fantom to wiersz, który spełnia kryteria
wyszukiwania, ale nie jest widoczny na początku. Przykład: transakcja 1 czyta
zbiór wierszy, który spełnia kryteria wyszukiwania. Transakcja 2 dodaje
wiersz, który spełnia kryteria wyszukiwania transakcji 1. Jeśli transakcja 1
ponownie wykona to samo wyszukiwanie dostanie inny zbiór rekordów.

## Poziomy izolacji

- Nakładanie blokad na obiekty d.b. pozwala uzyskać możliwie
największa izolację użytkowników
- Powoduje to jednak ograniczenia w dostępie do tych
obiektów przez innych użytkowników
- Standard języka SQL definiuje cztery poziomy izolacji realizacji
transakcji

| Poziom izolacji | Niezatwierdzony odczyt | Niepowtarzalny odczyt | Fantomy |
|---|---|---|---|
| **READ UNCOMMITED** | TAK | TAK | TAK |
| **READ COMMITED** | NIE | TAK  | TAK |
| **REPEATABLE READS** | NIE | NIE | TAK |
| **SERIALIZABLE** | NIE | NIE | NIE |
  

### Poziom SERIALIZABLE (pełna izolacja)

- Transakcja T odczytuje tylko te
obiekty, których zmiany zostały
zatwierdzone
- Żadna wartość odczytana lub
zmieniona przez T nie może być
zmieniona przez inną transakcję,
dopóki T nie skończy działać
- Wyniki dowolnej instrukcji **SELECT**
wyliczone przez transakcję T nie
zmieniają się, dopóki T nie skończy
działać
- Transakcja T uzyskuje blokady do
odczytu i zapisu obiektów i zwalnia je
zgodnie z protokołem **Strict-2PL**
- Zakładane są blokady typu S na
zbiory wierszy wynikowych instrukcji
**SELECT**

### Poziom REPEATABLE READS

- Transakcja T odczytuje tylko te
obiekty, których zmiany zostały
zatwierdzone
- Żadna wartość odczytana lub
zmieniona przez T nie może być
zmieniona przez inną transakcję,
dopóki T nie skończy działać
- Transakcja T uzyskuje blokady do
odczytu i zapisu obiektów i zwalnia
je zgodnie z protokołem Strict-2PL
- Nie są zakładane blokady na
wiersze wynikowe instrukcji SELECT

### Poziom READ COMMITED

- Transakcja T odczytuje tylko te
obiekty, których zmiany zostały
zatwierdzone.
- Żadna wartość zmieniona
przez T nie może być zmieniona
przez inną transakcję, dopóki T nie
skończy działać
- Transakcja T uzyskuje blokady X
aby wykonać zmiany i utrzymuje te
blokady do końca swojego
działania
- Do wykonania odczytu
transakcja T uzyskuje blokadę S. Po
zakończeniu aktualnej instrukcji
blokada ta jest zwalniana (nie
czekając na koniec transakcji)

### Poziom READ UNCOMMITED (poziom najniższy)

- Transakcja może
odczytywać wiersze, na
których działają inne
transakcje

# BASE (dla baz NoSQL)

BASE (dla NoSQL)
- Podstawowa dostępność (**Basically Available**)
    - Baza danych sprzyja dostępności danych,
    a nie poprawności danych
- Stan miękki (**Soft State**)
    - Bazy danych (np. Repliki) nie muszą być
    cały czas spójne
- Ostateczna spójność (**Eventually Consistent**)
    - Po pewnym czasie magazyny baz danych
    będą ostatecznie wzajemnie spójne  

- Bazy danych NoSQL są nastawione na
skalowalność
- Gdy repliki ulegną awarii, bazy danych
NoSQL nadal będą mogły zwracać dane,
chociaż nie będzie to najdokładniejsza
wersja

# Porównanie baz danych SQL i NoSQL

<table>
<tr>
<th> ACID </th>
<th> BASE </th>
</tr>
<tr>
<td>

ACID (dla SQL)
- Atomowość (**Atomic**)
    - Kiedy dochodzi do transakcji (odczytu / zapisu),
powinna ona nastąpić od razu lub wcale
    - Przerwanie transakcji nie powinno mieć
wpływu na bazę danych
    - Jeśli transakcja przechodzi, stan bazy danych
powinien odzwierciedlać zmianę
- Spójność (**Consistent**)
    - Po zakończeniu transakcji instancje baz danych
(np. Repliki) powinny w tym samym czasie
odzwierciedlać ten sam stan
- Izolacja (**Isolated**)
    - Każda transakcja powinna być wykonywana
oddzielnie.
    - Baza danych blokuje wiersz, aby zapewnić, że
transakcje są realizowane sekwencyjnie
- Trwałość (**Durable**)
    - Po zatwierdzeniu transakcji modyfikacja będzie
trwała, nawet w przypadku awarii systemu

- Właściwości ACID zapewniają spójność danych
po zakończeniu transakcji, ale kosztem
zablokowania bazy danych

</td>
<td>

BASE (dla NoSQL)
- Podstawowa dostępność (**Basically Available**)
    - Baza danych sprzyja dostępności danych,
    a nie poprawności danych
- Stan miękki (**Soft State**)
    - Bazy danych (np. Repliki) nie muszą być
    cały czas spójne
- Ostateczna spójność (**Eventually Consistent**)
    - Po pewnym czasie magazyny baz danych
    będą ostatecznie wzajemnie spójne  

- Bazy danych NoSQL są nastawione na
skalowalność
- Gdy repliki ulegną awarii, bazy danych
NoSQL nadal będą mogły zwracać dane,
chociaż nie będzie to najdokładniejsza
wersja

</td>
</tr>
</table>

## Porównanie baz danych SQL i NoSQL na kategorie

<table>
<tr>
<th>



</th>
<th>

SQL

</th>
<th>

NoSQL

</th>
</tr>
<tr>
<td>

Najlepsze dla:

</td>
<td>

- Obsługi danych, które są relacyjne i mają
logiczne i dyskretne wymagania, które można
z góry zidentyfikować
- Schematów, które muszą być utrzymywane i
synchronizowane między aplikacją a bazą
danych
- Starszych systemów budowanych dla struktur
relacyjnych
- Aplikacji wymagające złożonych zapytań lub
transakcji wielowierszowych


</td>
<td>

- Obsługi dużych, niepowiązanych,
nieokreślonych lub szybko zmieniających się
danych
- Danych niezależnych od schematu lub gdy
schemat jest narzucony przez aplikację
- Aplikacji, w których wydajność i dostępność
są ważniejsze niż silna spójność
- Zawsze dostępnych aplikacji, które służą
użytkownikom na całym świecie

</td>
</tr>
<tr>
<td>

Scenariusze:

</td>
<td>

- Systemy księgowe, finansowe i bankowe
- Systemy zarządzania zapasami
- Systemy zarządzania transakcjami

</td>
<td>

- Aplikacje mobilne
- Analizy w czasie rzeczywistym
- Zarządzanie zawartością
- Personalizacja
- Aplikacje IoT
- Migracja bazy danych

</td>
</tr>
<tr>
<td>

Skalowalność:

</td>
<td>

- Skalowanie danych w pionie, zwiększając
obciążenie serwera

</td>
<td>

- Skaluje dane w poziomie z wykorzystaniem
shardingu między serwerami

</td>
</tr>
<tr>
<td>

Model danych:

</td>
<td>

- Typ bazy danych: tabele wierszy,
pogrupowane w relacje
- Używanie strukturalnego języka zapytań
(SQL)
- Przechowywanie danych jako wiersze w
tabelach; powiązane dane przechowywane
osobno i łączone w przypadku złożonych
zapytań

</td>
<td>

- Typy baz danych: klucz-wartość,
dokumentowe, kolumnowe, grrafowe
- Przechowywanie danych w zależności od
typu bazy danych

</td>
</tr>
</table>
