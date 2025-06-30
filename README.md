# **Dokumentacja aplikacji `Studino`**
## **Spis treści**

# Wprowadzenie
Studino to mobilna aplikacja napisana w React Native, umożliwiająca użytkownikom tworzenie własnych quizów, rozgrywanie quizów stworzonych przez innych, granie w minigry edukacyjne z zakresu chemii, matematyki i języka angielskiego, które wzmacniają umiejętności oraz zarządzanie profilem. Aplikacja umożliwia użytkownikom rejestrację/logowanie e-mail i hasło lub Google Sign-In i komunikuje się z chmurą Firebase (Firestore i Firebase Authentication) w celu przechowywania danych i uwierzytelniania.
## Cel aplikacji
Umożliwienie użytkownikom łatwego tworzenia i rozgrywania quizów oraz śledzenia ich wyników, również rozwijanie umiejętności poprzez Minigry edukacyjne.
##Technologie
Studino zostało napisane w React Native i wykorzystuje Firebase do autentykacji, Firestore Database, Storage. Do zarządzania stanem aplikacji wykorzystywane są Hooki Reacta oraz bezpośrednie zapytania do bazy Firestore. Do przechodzenia między ekranami wykorzystano bibliotekę React Navigation (Stack Navigator), a do wyglądu UI różne biblioteki m.in. react-native-elements, react-native-modal, react-native-safe-area-context.

# Szybki Start
Aby szybko rozpocząć pracę z projektem Studino, należy postępować według poniższych kroków:

1. Wymagania wstępne:
   - **Node.js** i **npm** lub **yarn** – do instalacji zależności i uruchamiania bundlera React Native.
   - **Android Studio** z **Android SDK** – do budowania wersji na Android.
   - **Urządzenie lub emulator**: Można użyć fizycznego telefonu, podłączonego przez kabel USB lub emulatora Androida do testów.
   - **Google CLI Android**: Aby testować logowanie Google na Androidzie, trzeba skonfiguruować SHA-1 w konsoli Firebase i wygenerować plik `google-services.json`.
2. Pobranie projektu:
   - Pobierz plik .zip i go wypakuj
   - Przejdź do folderu za pomocą cd studino
3. W katalogu głównym wykonaj

   ```
   npm install
   ```

4. Uruchomienie aplikacji:

   ```
   npm run android
   ```

# Zależności projektu
Projekt wykorzystuje wiele bibliotek z React Native. Poniżej znajduje się lista głównych zależności (dependencies z package.json) wraz z krótkim opisem ich roli:
- @react-native-firebase/app/auth/firestore/storage: Pakiety Firebase służące do integracji z usługami Google Firebase.
  - `app` – inicjalizacja i konfiguracja Firebase.
  - `auth` – obsługa uwierzytelniania (logowanie, rejestracja użytkownika).
  - `firestore` – interakcje z bazą danych Firestore (kolekcje i dokumenty quizów, użytkowników, wyników).
  - `storage` – (opcjonalnie) przechowywanie plików (np. zdjęć), w projekcie wstępnie skonfigurowane.
 
- **@react-navigation/native**, **@react-navigation/stack**: Biblioteki nawigacyjne React Navigation. Pozwalają na tworzenie stosów ekranów (StackNavigator) oraz kontrolę przepływu aplikacji między widokami.
- @react-native-community/netinfo: Biblioteka do monitorowania stanu połączenia sieciowego. Umożliwia sprawdzanie, czy urządzenie ma dostęp do Internetu.
- @react-native-community/progress-bar-android: Komponent ProgressBar dla Androida – używany do wizualizacji postępu.
- @react-native-google-signin/google-signin: Umożliwia logowanie użytkowników przy użyciu konta Google (Google Sign-In) w aplikacji.
- react-native-dropdown-picker, react-native-element-dropdown, react-native-select-dropdown: Zestaw komponentów graficznych typu dropdown (rozwijane listy wyboru) – np. wybór przedmiotu lub poziomu trudności w formularzu dodawania quizu.
- react-native-gesture-handler, react-native-screens: Biblioteki pomagające w efektywnej implementacji gestów dotykowych oraz nawigacji. Są często wymagane przez React Navigation.
- react-native-modal: Rozszerzony komponent Modal (okno dialogowe) – wykorzystywany np. w formularzu dodawania pytania (modale na dodawanie pytania, potwierdzenia itp.).
- react-native-safe-area-context: Zarządzanie obszarem bezpiecznym na ekranie (tzw. Safe Area) – szczególnie ważne na urządzeniach z wycięciem ekranu (notch).
- react-native-toast-message: Biblioteka do wyświetlania niefatolnych powiadomień (toast) – np. komunikatów o błędach, potwierdzeniach, informacjach zwrotnych.
- react-native-uuid oraz uuid: Narzędzia do generowania unikalnych identyfikatorów (UUID) – używane przy tworzeniu nowych obiektów (np. pytań w quizie).
- @babel/, eslint, prettier, jest itp.: Zależności deweloperskie do budowania, lintowania i testowania projektu.

Każdą z powyższych bibliotek można znaleźć w package.json, a opisy i dokumentację znajdziesz na stronach npm lub GitHub poszczególnych projektów.

> [!WARNING]
> Ważne: Po modyfikacji głównych zależności (np. aktualizacji React Native lub Firebase) należy sprawdzić kompatybilność wersji i ewentualnie wyczyścić cache (np. npx react-native start --reset-cache).

# Struktura katalogów

Poniżej przedstawiono przykładową strukturę katalogów projektu Studino.

```
Studino/
├─ App.jsx                 # Główny plik aplikacji (nawigacja i logika autoryzacji)
├─ firebase.js             # Inicjalizacja Firebase (auth, firestore)
├─ firebaseConfig.js       # Parametry konfiguracji Firebase (API keys)
├─ package.json            # Lista zależności i skryptów npm
├─ tsconfig.json           # Konfiguracja TypeScript (jeśli używany)
├─ .eslintrc.js            # Konfiguracja ESLint
├─ .prettierrc.js          # Konfiguracja Prettier
├─ index.js                # Punkt startowy aplikacji (registerComponent itp.)
├─ jsons                   # Pliki json
├─ screens/                # Katalog ekranów (widoków) aplikacji
│   ├─ AuthLoadingScreen.jsx  # Ekran sprawdzający stan logowania
│   ├─ LoginScreen.jsx        # Ekran logowania (Google Sign-In)
│   ├─ ProfileSetupScreen.jsx # Ekran konfiguracji profilu przy pierwszym logowaniu
│   ├─ HomeScreen.jsx         # Główny ekran po zalogowaniu
│   ├─ BrowseQuizzesScreen.jsx# Lista i wyszukiwanie quizów
│   ├─ QuizSelectScreen.jsx   # Wybór quizu (np. według przedmiotu)
│   ├─ QuizDetailsScreen.jsx  # Szczegóły wybranego quizu
│   ├─ QuizGameScreen.jsx     # Rozgrywka quizu (pytania wielokrotnego wyboru lub prawda/fałsz)
│   ├─ QuizResultsScreen.jsx  # Podsumowanie wyniku quizu
│   ├─ QuizHistoryScreen.jsx  # Historia rozegranych quizów (wyniki)
│   ├─ ManageQuizzesScreen.jsx# Zarządzanie własnymi quizami (lista i edycja)
│   ├─ CreateQuizScreen.jsx   # Formularz tworzenia nowego quizu
│   ├─ TitleSelectScreen.jsx  # Wybór tytułu/odznaki użytkownika
│   ├─ YourProfile.jsx        # Profil własnego użytkownika (statystyki)
│   ├─ PublicProfileScreen.jsx# Profil innego użytkownika (widok publiczny)
│   ├─ Settings.jsx           # Ustawienia aplikacji (wylogowanie itp.)
│   ├─ MathMinigameScreen.jsx # Minigra matematyczna (zadania arytmetyczne)
│   ├─ ChemistryMinigameScreen.jsx # Minigra chemiczna (wzory, definicje)
│   └─ EnglishMinigameScreen.jsx   # Minigra językowa (fiszki, słownictwo)
└─ images/                 # Obrazy używane w aplikacji (ikony, awatary, tła)
    ├─ icons/
    └─ avatars/
    └─ subject_images/

```

# Ekrany i funkcjonalności

Każdy ekran aplikacji Studino pełni określoną rolę. Poniżej szczegółowy opis najważniejszych ekranów i ich funkcji:

- **AuthLoadingScreen**:
  - Pierwszy ekran po uruchomieniu. Sprawdza stan autoryzacji (czy użytkownik jest już zalogowany).
  - Wyświetla spinner ładowania dopóki aplikacja inicjalizuje Firebase i sprawdza poświadczenia.
  - Jeśli użytkownik jest zalogowany i posiada profil w bazie, przechodzi do HomeScreen; w przeciwnym razie kieruje do LoginScreen.
- **LoginScreen**:
  - Ekran logowania za pomocą konta Google. Wykorzystuje bibliotekę Google Sign-In.
  - Po pomyślnym logowaniu tworzy (lub aktualizuje) wpis użytkownika w kolekcji users w Firestore. Następnie przechodzi do ekranu konfiguracji profilu (ProfileSetupScreen) jeśli to pierwsze logowanie lub bezpośrednio do HomeScreen.
  - Zawiera przycisk „Zaloguj się przez Google” oraz umożliwia logowanie e-mailem i hasłem.
- **ProfileSetupScreen**:
  - Wyświetlany po pierwszym logowaniu nowego użytkownika. Pozwala ustawić wstępne dane profilu takie jak nazwa użytkownika i awatar.
  - Po wypełnieniu formularza informacje zapisywane są w kolekcji users.
- **HomeScreen**:
  - Główny pulpit użytkownika po zalogowaniu. Zawiera możliwość nawigacji do najważniejszych sekcji:
    - Przycisk prowadzący do ekranu wyboru quizów.
    - Przyciski do grania w minigry edukacyjne: osobne przyciski dla chemii, matematyki, angielskiego.
    - Widżety z szybkimi statystykami użytkownika (np. obecny streak, ilość ukończonych quizów, procent dobrych odpowiedzi).
    - Przycisk dostępu do własnego Profilu i Ustawień.
  - Na dole ekranu jest pasek nawigacyjny prowadzący do innych ekranów (Quizy, Profil, Tytuły, Ustawienia).
- **BrowseQuizzesScreen**:
  - Ekran do przeglądania i wyszukiwania dostępnych quizów w bazie.
  - Zawiera pole do wyszukiwania po nazwie użytkownika i autorze
  - Możliwość sortowania lub filtrowania (np. najpopularniejsze, ostatnio dodane).
  - Wyświetla listę quizów z ich ogólnym opisem.
  - Kliknięcie w któryś otwiera ekran ze szczegółami.
- **QuizSelectScreen**:
  - Zawiera 4 przyciski do:
    - Tworzenia quizów
    - Szukania quizów
    - Zarządzania quizami
    - Historii quizów
- **QuizDetailsScreen**:
  - Wyświetla szczegółowe informacje o wybranym quizie.
  - Pokazuje statystyki: ile razy quiz był zagrany, ile razy polubiony, średni procent poprawnych odpowiedzi.
  - Przycisk „Zagraj w quiz” rozpoczyna rozgrywkę (otwiera QuizGameScreen).
  - Zawiera przyciski do polubienia i dodania do ulubionych
- **QuizGameScreen**:
  - Główny ekran rozgrywki wybranego quizu. Pytania mogą mieć różne typy: wielokrotnego wyboru (multiple choice) lub prawda/fałsz (true/false).
  - Użytkownik wybiera odpowiedź, a po potwierdzeniu przechodzi do następnego pytania.
  - Na końcu quizu następuje obliczenie wyniku (ilości poprawnych odpowiedzi, procentu) i zapisanie wyniku w bazie w kolekcji quiz_results. Następnie wyświetla się QuizResultsScreen.
- **QuizResultsScreen**:
  - Pokazuje podsumowanie quizu: procent poprawnych odpowiedzi, liczbę zdobytych punktów, czas trwania, oraz ewentualne uwagi.
  - Użytkownik może zobaczyć, które odpowiedzi udzielił poprawnie lub błędnie.
  - Przycisk pozwala powrócić do HomeScreen lub zagrać ponownie.
  - Wynik quizu jest też automatycznie zapisywany w historii użytkownika (kolekcja quiz_results).
- **QuizHistoryScreen**:
  - Lista wszystkich zagranych przez użytkownika quizów.
  - Umożliwia przeglądanie przeszłych wyników i analizę postępów.
- **ManageQuizzesScreen**:
  - Zawiera listę quizów stworzonych przez obecnego użytkownika
  - Dla każdego quizu dostępne są opcje „Edytuj” (przejście do formularza edycji) oraz „Usuń” (kasowanie quizu).
- **CreateQuizScreen**:
  - Formularz do tworzenia nowego quizu lub edycji istniejącego.
  - Pola do wypełnienia: tytuł quizu, przedmiot, poziom trudności (np. lista wyboru „łatwy/średni/trudny”), opis (opcjonalny).
  - Sekcja do dodawania pytań: pytanie oraz lista możliwych odpowiedzi. Użytkownik może wybrać typ pytania (jednokrotny wybór, wielokrotny wybór, prawda/fałsz) i wskazać poprawne odpowiedzi.
  - Możliwość dodawania kolejnych pytań przez kliknięcie „Dodaj pytanie”.
  - Zawiera przyciski „Zapisz quiz” oraz „Anuluj”.
  - Walidacja: sprawdza, czy quiz ma minimum 1 pytanie, czy wszystkie pytania mają oznaczone poprawne odpowiedzi.
- **TitleSelectScreen**:
  - Pozwala użytkownikowi wybrać swój tytuł ze zbioru dostępnych tytułów. Tytuły mogą być zdobywane po spełnieniu pewnych warunków (np. liczba zagranych quizów).
  - Po wybraniu aktualizuje selectedTitle w profilu użytkownika.
- **YourProfile**:
  - Ekran profilu własnego użytkownika. Zawiera:
    - Awatar, nazwa użytkownika i wybrany tytuł.
    - Statystyki osobiste
    - Lista ulubionych quizów i odblokowanych tytułów.
    - Przycisk do edycji avatara.
    - Przycisk zmiany tytułu.
- **PublicProfileScreen**:
  - Profil innego użytkownika (np. kliknięty autor quizu).
  - Pokazuje nazwę i awatar użytkownika, jego tytuł oraz statystyki.
- **Settings**:
  - Ekran ustawień aplikacji. Zawiera opcje typu: Wyloguj się, zmień hasło/nazwę użytkownika, usuń konto.
- **MathMinigameScreen / ChemistryMinigameScreen / EnglishMinigameScreen**:
  - Minigry edukacyjne dla trzech przedmiotów: matematyki, chemii i języka angielskiego.
  - Każda minigra jest osobnym ekranem, zawiera pytania.

# Właściwości aplikacji

| **Właściwości funkcjonalne**                                             | **Właściwości niefunkcjonalne**                                                                                                                 |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| *Użytkownik może się rejestrować/logować (Google).*                      | **Responsywność:** Aplikacja działa płynnie na urządzeniach mobilnych oraz uwzględnia różne rozdzielczości ekranu.                              |
| *Tworzenie quizu:* dodawanie pytań, odpowiedzi.                          | **Bezpieczeństwo:** Uwierzytelnianie Firebase, autoryzacja zapytań (reguły Firestore).                                                          |
| *Przeglądanie quizów:* filtrowanie wg przedmiotów, wyszukiwanie.         | **Skalowalność:** Baza Firestore działa w chmurze, pozwalając na obsługę wielu użytkowników i quizów bez własnej infrastruktury serwera.        |
| *Rozgrywka w quiz:* wybór odpowiedzi, obliczanie wyniku.                 | **Wysoka dostępność:** Dzięki Firebase usługi są zazwyczaj wysoko dostępne i replikowane (regionalnie).                                         |
| *Polubienie quizu (likes):* aktualizacja licznika i listy obserwujących. | **Szyfrowanie danych:** Komunikacja z Firebase odbywa się po HTTPS. Dane logowania użytkownika (hasło) przechowywane jako hasz w Firebase Auth. |
| *Historia wyników:* zapisywanie i wyświetlanie wyników quizów.           | **Wydajność:** Strumieniowe pobieranie danych z Firestore.                                      |
| *Minigry edukacyjne:* krótka grawalna zawartość dla danego przedmiotu.   | **Konwencje i standaryzacja:** Kod zgodny z ESLint/Prettier, jednolite nazewnictwo.                                                             |

# Zestaw kolorystyczny

Aplikacja Studino ma ciemny motyw z wyraźnymi akcentami kolorystycznymi. Oto główne używane kolory (zastosowania przykładowe):

| Kolor          | Użycie                                                             |
| -------------- | ------------------------------------------------------------------ |
| `#202020`      | **Tło główne** aplikacji (np. tła ekranów, nav bary w motywie).    |
| `#1F1F1F`      | Nieco jaśniejsze tło dodatkowe (np. karty, kontenery).             |
| `#1A1A1A`      | Tło sekcji, oddzielające części UI.                                |
| `#8E8E93`      | Szary kolor tekstu pomocniczego (np. opisy, placeholdery).         |
| `#FFFFFF`      | Biały tekst główny.                                                |
| `#FFA000`      | Pomarańczowy akcent (np. przycisk dodawania, ikony akcji *dodaj*). |
| `#FF9500`      | Inny odcień pomarańczowego – np. kolor aktywny w sliderze.         |
| `#FFC107`      | Żółty akcent (np. gwiazdki lub znaczniki).                         |
| `#2196F3`      | Błękitny akcent (np. linki, przyciski potwierdzenia).              |
| `#4CAF50`      | Zielony – np. oznaczenie poprawnej odpowiedzi lub sukcesu.         |
| `#DF2020`      | Czerwony – sygnalizacja błędu, niewłaściwej odpowiedzi.            |
| `#8b5cf6`      | Fioletowy – opcjonalnie w tle banerów lub akcent przy tytułach.    |
| `#AAA`, `#CCC` | Jasnoszare – obramowania, podziały sekcji lub tłumiony tekst.      |

# Architektura i wzorce projektowe

- Architektura ogólna: Aplikacja działa w architekturze klient–serwer w modelu serverless. Klient (urządzenie mobilne) komunikuje się bezpośrednio z usługami Firebase (Auth, Firestore) poprzez SDK. Nie ma pośredniego serwera REST – zamiast tego wykorzystywana jest baza NoSQL Firestore i reguły bezpieczeństwa.
- State Management: Projekt nie używa dużych bibliotek do zarządzania stanem, takich jak Redux czy MobX. Zamiast tego wykorzystano:
  - React Hooks (useState, useEffect itp.): do lokalnego stanu komponentów i ładowania danych z Firestore.
  - Firebase Firestore: Źródło informacji dla danych aplikacji (quizów, użytkowników). Aktualizacje i odczyt danych wykonuje się bezpośrednio z bazy. Dzięki temu spójność stanu aplikacji gwarantuje sama baza danych (np. kolekcja quizzes zawsze posiada aktualne dane o quizach).
- Modularność Katalog screens jest pogrupowany według funkcjonalności (Quiz, Profil, Minigry itp.). Dzięki temu kod jest łatwy do utrzymania i rozbudowy – np. jeśli chcemy dodać nową minigrę, tworzymy nowy ekran w screens.

# API i Integracje

Aplikacja korzysta głównie z Firebase Firestore jako bazy danych (niezależnie hostowanej w chmurze) oraz Firebase Auth do uwierzytelniania. Poniżej opis integracji:

- Endpointy Firebase (Firestore):
  - Firestore nie używa tradycyjnych „endpointów” REST w kodzie – korzysta się z metod SDK (modułów getFirestore, doc(), setDoc, updateDoc, getDoc, getDocs, query etc.).
  - Kolekcje: users, quizzes, quiz_results. Każde zapytanie jest realizowane poprzez składanie obiektów Query w JS.
  - Obsługa błędów: Wszystkie operacje asynchroniczne (Firestore, Auth) opakowane są w bloki try/catch. W przypadku błędów (np. brak uprawnień, brak połączenia) wyświetlane są komunikaty.
  - Reguły bezpieczeństwa: (patrz niżej w dokumencie) definiują, kto może czytać i zapisywać dane. Kluczowe zasady: każdy może czytać dane quizów i użytkowników, ale zapisy i aktualizacje danych podlegają autoryzacji.
  - Brak zewnętrznego API: Aplikacja nie konsumuje żadnego publicznego API (np. REST) poza Firebase. Wszystkie serwisy są zarządzane przez Google/Firebase.
- Integracje dodatkowe:
  - Google Sign-In: Umożliwia szybkie logowanie. Wymaga konfiguracji w konsoli Google. W kodzie inicjuje się GoogleSignin.configure() z danymi klienta.

# Nawigacja i flow aplikacji

Aplikacja używa React Navigation (Stack Navigator) do przejść pomiędzy ekranami. Poniżej uproszczony diagram nawigacji oraz opis tras:

```
AuthLoadingScreen
    ├─ gdy zalogowany? ──> HomeScreen ──┬─> QuizSelectScreen ──┬─> BrowseQuizzesScreen ──> QuizDetailsScreen ──┬─> QuizGameScreen ──> QuizResultsScreen
    │                                  │                       ├─> CreateQuizScreen (tworzenie quizu)          └─> PublicProfileScreen
    │                                  │                       ├─> ManageQuizzesScreen ───> CreateQuizScreen (edycja quizu)
    │                                  ├                       └─> QuizHistoryScreen ──> QuizResultsScreen
    │                                  │                        
    │                                  ├─> YourProfile ────────> TitleSelectScreen
    │                                  ├─> PublicProfileScreen
    │                                  ├─> Settings
    │                                  ├─> ChemistryMinigameScreen
    │                                  ├─> MathMinigameScreen
    │                                  └─> EnglishMinigameScreen
    └─ gdy nie zalogowany ─────────> LoginScreen
    └─ po pierwszym logowaniu ───> ProfileSetupScreen

```

- Parametry tras: Przy nawigacji do ekranu QuizDetailsScreen przekazywany jest quizId i ewentualnie dane quizu, aby ekran mógł pobrać informacje i wyświetlić je.
- Hierarchia Stack: Główny Stack.Navigator zdefiniowany jest w App.jsx. Najpierw wstawiany jest AuthLoadingScreen. Po jego zakończeniu znikają ekrany logowania i wyświetlany jest stos właściwych ekranów (Home, Profile itd.).
- Powrót: System nawigacji umożliwia cofanie (Android back / nawigacja wstecz). Ekran QuizGameScreen po zakończeniu automatycznie kieruje do wyników, użytkownik może stamtąd wrócić do Home.

# UI

- Motyw ciemny: Cała aplikacja ma ciemne tło z jasnym (białym) tekstem. Przyciski i ważne akcje wyróżniono kolorami akcentującymi (pomarańczowy, zielony itp.).
- Ikony i obrazy: Korzystamy z plików PNG w katalogu images.
- Responsywność: Stylizacja odbywa się w StyleSheet.create. Większość layoutów wykorzystuje elastyczne style (flex: 1), procentowe marginesy/padding, dzięki czemu UI dostosowuje się do różnych ekranów.

# Debugowanie i monitoring

- Logowanie i wyświetlanie błędów:
  - Konsola: Podczas developmentu używamy console.log() w JS/JSX do debugowania zmian stanu i wyników zapytań.
  - Powiadomienia w UI: Dla błędów i potwierdzeń w aplikacji wykorzystujemy bibliotekę react-native-toast-message. Użytkownik widzi krótkie powiadomienia typu „Błąd logowania”, „Quiz zapisany”, itp.
  - Alerty: W niektórych miejscach (np. potwierdzenie usunięcia quizu) używany jest natywny Alert z przyciskami „OK/Anuluj”.
- Debugowanie:
  - Narzędzia: React Native Debugger / Flipper (umożliwia inspekcję stanu Redux, sieci, Crashlytics). W projekcie React Native standardowo dostępne jest narzędzie Chrome DevTools (lub adb logcat na Androidzie).
  - Wyjątki: Firebase błędy (np. błędne reguły) logowane są w konsoli. 


# Baza Danych (Firebase Firestore)

## Wprowadzenie i cele

Firestore (część Google Firebase) jest nierelacyjną, dokumentową bazą danych w chmurze. Pozwala przechowywać dane w formie kolekcji dokumentów, które mogą mieć zagnieżdżone struktury (mapy, tablice). Celem wykorzystania Firestore w Studino jest zapewnienie:
  - Łatwego przechowywania danych aplikacji: użytkownicy, quizy i wyniki przechowywane są w przejrzystym formacie JSON.
  - Synchronizacji w czasie rzeczywistym: zmiany w bazie mogą być natychmiast dostarczane do aplikacji (jeśli użyto onSnapshot).
  - Skalowalności i utrzymania: Google Firebase dba o infrastrukturę, replikacje i backupy, dzięki czemu nie trzeba zarządzać własnymi serwerami baz danych.
Dzięki Firestore nie musimy pisać własnego backendu – nasza aplikacja mobilna łączy się bezpośrednio z bazą danych z wykorzystaniem reguł bezpieczeństwa.

## Architektura bazy danych

- Model dokumentowy: Dane są przechowywane jako dokumenty JSON w kolekcjach.
- Klucz główny: Każdy dokument ma swój unikalny identyfikator (ID). W kolejce users ID to zazwyczaj uid użytkownika (z Firebase Auth). W kolekcji quizzes i quiz_results – losowe lub generowane przez aplikację UUID.
- Brak sztywnych relacji: Nie ma kluczy obcych w sensie SQL. Relacje realizowane są przez przechowywanie referencji (np. w polach created_by w quizie zapisujemy userId).

## Schemat bazy (DDL)

Poniżej znajdują się kolekcje i definicje pól (odpowiednik tabel w bazie SQL). Firestore nie wymaga formalnego języka DDL, ale prezentuję strukturę dla przejrzystości:


1. Kolekcja users: (dokumenty użytkowników)
- ID dokumentu (userId): odpowiada UID z Firebase Auth
- Fields:
  - email (string) – adres e-mail użytkownika (z Firebase Auth).
  - username (string) – wybrana nazwa użytkownika.
  - avatar (string) – nazwa pliku awatara.
  - selectedTitle (string) – nazwa wybranego tytułu użytkownika.
  - titlesCount (number) – ile tytułów zdobył.
  - favorites (array<string>) – lista ID quizów oznaczonych jako ulubione.
  - liked_quizzes (array<string>) – ID quizów polubionych.
  - quizzesCreated (number) – liczba utworzonych quizów.
  - quizzesPlayed (number) – liczba rozegranych quizów.
  - longestStreak (number) – najdłuższa seria wygranych z rzędu.
  - currentStreak (number) – obecna seria wygranych z rzędu.
  - lastLoginAt (timestamp) – data i godzina ostatniego logowania.
  - createdAt (timestamp) – data utworzenia konta (pierwszego logowania).
  - Statystyki po przedmiotach:
    - mathAnswered (number), mathCorrect (number) – liczba odpowiedzi/liczba poprawnych odpowiedzi z matematyki.
    - chemistryAnswered, chemistryCorrect – analogicznie dla chemii.
    - englishFlashcardsAnswered, englishFlashcardsCorrect – dla fiszek angielskich.
  - totalQuestionsAnswered (number) – suma wszystkich udzielonych odpowiedzi.
  - totalPercentage (number) – całkowita liczba procentów poprawnych odpowiedzi (ze wszystkich quizów).
  - totalQuizTime (number) – łączny czas spędzony na quizach (w minutach).


2. Kolekcja quizzes: (dokumenty quizów stworzonych przez użytkowników)
   - ID dokumentu (quizId): losowe UUID nadane przy tworzeniu.
   - Fields:
    - title (string) – tytuł quizu.
    - description (string) – opis quizu.
    - subject (string) – przedmiot quizu (np. "Chemia", "Matematyka").
    - difficulty (string) – poziom trudności ("łatwy", "średni", "trudny").
    - level (string) – dodatkowa kategoria poziomu (np. Podstawowy, Rozszerzony).
    - created_by (string) – ID użytkownika, który utworzył quiz.
    - created_by_name (string) – kopia nazwy użytkownika autora.
    - created_at (timestamp) – data utworzenia quizu.
    - updated_at (timestamp) – data ostatniej edycji quizu.
    - playsCount (number) – liczba rozpoczętych rozgrywek.
    - likes (number) – liczba polubień quizu.
    - favorited_by (array<string>) – lista ID użytkowników, którzy polubili quiz (opcjonalnie do śledzenia kto lubił).
    - totalPercentage (number) – całkowity procent poprawnych odpowiedzi wszystkich rozgrywek tego quizu.
    - questions (array of objects) – lista pytań w quizie. Każdy obiekt pytania zawiera:
      - id (string) – unikalne ID pytania wewnątrz quizu (np. UUID).
      - type (string) – typ pytania: "mcq" (wielokrotny wybór) lub "tf" (prawda/fałsz).
      - question (string) – treść pytania.
      - options (array<string>) – lista opcji odpowiedzi (dla "tf" może to być ["Prawda", "Fałsz"]).
      - correctIndexes (array<number>) – indeksy poprawnych odpowiedzi (np. [2] albo [0,3]).

3. Kolekcja quiz_results: (dokumenty z zapisanymi wynikami każdej ukończonej rozgrywki)
   - ID dokumentu (resultId): losowe UUID nadane przy zapisie wyniku.
   - Fields:
     - quizId (string) – ID quizu, którego dotyczy wynik.
     - userId (string) – ID użytkownika, który grał.
    - completedAt (timestamp) – data i godzina zakończenia quizu.
    - totalQuestions (number) – liczba pytań w quizie.
    - correctAnswers (number) – liczba poprawnych odpowiedzi.
    - percentage (number) – procent poprawnych odpowiedzi
    - totalTime (number) – całkowity czas quizu.
    - answers (array of maps) – szczegółowe odpowiedzi. Każdy element to obiekt z właściwościami:
      - questionIndex (number) – indeks pytania (kolejność w quizie).
      - questionText (string) – treść pytania (dla powtórki).
      - type (string) – typ pytania ("mcq" lub "tf").
      - options (array<string>) – (tylko dla mcq) lista odpowiedzi podana graczowi.
      - selected (boolean|string|array) – odpowiedź udzielona przez użytkownika (np. indeks, true/false albo tablica indeksów).
      - correct (boolean|string|array) – prawidłowa odpowiedź (tak jak wyżej).
      - isCorrect (boolean) – czy użytkownik odpowiedział poprawnie.
      - timeSpent (number) – czas spędzony nad tym pytaniem.





















