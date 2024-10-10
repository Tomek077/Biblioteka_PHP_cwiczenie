**Temat lekcji: Prosty zapis i odczyt danych z bazy MySQL w PHP (Przykład z książkami)**

---

**Cel lekcji:**

- Nauczysz się, jak w prosty sposób zapisywać dane do bazy MySQL i odczytywać je za pomocą PHP, skupiając się tylko na podstawowych operacjach.

---

**Wprowadzenie:**

W tej lekcji pokażemy, jak połączyć się z bazą danych MySQL, zapisać do niej dane oraz je odczytać, używając PHP. Skupimy się na podstawowej funkcjonalności, pomijając sprawdzanie poprawności połączenia czy zabezpieczenia. Zamiast przykładu z uczniami, wykorzystamy bazę danych dotyczącą książek.

---

### **1. Tworzenie bazy danych i tabeli**

**a) Utworzenie bazy danych "biblioteka"**

- Otwórz phpMyAdmin w przeglądarce (np. `http://localhost/phpmyadmin`).
- Kliknij na zakładkę **"Bazy danych"**.
- W polu **"Utwórz bazę danych"** wpisz `biblioteka` i kliknij **"Utwórz"**.

**b) Utworzenie tabeli "ksiazki"**

- Wybierz bazę danych **"biblioteka"** z listy po lewej stronie.
- Kliknij na zakładkę **"SQL"** i wprowadź następujące polecenie SQL:

```sql
CREATE TABLE ksiazki (
    id INT AUTO_INCREMENT PRIMARY KEY,
    tytul VARCHAR(100),
    autor VARCHAR(100)
);
```

- Kliknij **"Wykonaj"**.

---

### **2. Tworzenie formularza HTML do wprowadzania danych**

**a) Utworzenie pliku "formularz.html"**

- Otwórz edytor tekstu (np. Notepad++ lub Notatnik).
- Wklej poniższy kod:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Dodaj książkę</title>
</head>
<body>
    <h1>Dodaj nową książkę</h1>
    <form action="dodaj.php" method="post">
        Tytuł:<br>
        <input type="text" name="tytul"><br><br>
        Autor:<br>
        <input type="text" name="autor"><br><br>
        <input type="submit" value="Dodaj">
    </form>
</body>
</html>
```

- Zapisz plik jako **`formularz.html`** w folderze serwera WWW (np. `htdocs` w przypadku XAMPP).

---

### **3. Tworzenie skryptu PHP do zapisywania danych**

**a) Utworzenie pliku "dodaj.php"**

- W edytorze tekstu utwórz nowy plik i wklej poniższy kod:

```php
<?php
// Połączenie z bazą danych
$polaczenie = mysqli_connect("localhost", "root", "", "biblioteka");

// Pobranie danych z formularza
$tytul = $_POST['tytul'];
$autor = $_POST['autor'];

// Wstawienie danych do bazy
mysqli_query($polaczenie, "INSERT INTO ksiazki (tytul, autor) VALUES ('$tytul', '$autor')");

// Potwierdzenie dodania danych
echo "Dodano książkę.<br>";
echo "<a href='lista.php'>Zobacz listę książek</a>";
?>
```

- Zapisz plik jako **`dodaj.php`** w folderze serwera WWW.

---

### **4. Tworzenie skryptu PHP do odczytywania danych**

**a) Utworzenie pliku "lista.php"**

- W edytorze tekstu utwórz nowy plik i wklej poniższy kod:

```php
<?php
// Połączenie z bazą danych
$polaczenie = mysqli_connect("localhost", "root", "", "biblioteka");

// Pobranie danych z bazy
$wynik = mysqli_query($polaczenie, "SELECT * FROM ksiazki");

// Wyświetlanie danych
echo "<h1>Lista książek:</h1>";
while($ksiazka = mysqli_fetch_assoc($wynik)) {
    echo $ksiazka['tytul'] . " - " . $ksiazka['autor'] . "<br>";
}
?>
```

- Zapisz plik jako **`lista.php`** w folderze serwera WWW.

---

### **5. Testowanie aplikacji**

**a) Uruchomienie serwera WWW**

- Upewnij się, że serwer Apache jest uruchomiony (np. w XAMPP).

**b) Dodawanie nowej książki**

- Otwórz przeglądarkę internetową.
- Przejdź do adresu `http://localhost/formularz.html`.
- Wypełnij formularz danymi książki i kliknij **"Dodaj"**.

**c) Wyświetlanie listy książek**

- Po dodaniu książki pojawi się komunikat oraz link do wyświetlenia listy książek.
- Kliknij na link **"Zobacz listę książek"**, aby zobaczyć wprowadzone dane.

---

### **Podsumowanie:**

- Stworzyliśmy prostą bazę danych i tabelę w MySQL dotyczącą książek.
- Napisaliśmy formularz HTML do wprowadzania danych.
- Utworzyliśmy skrypty PHP do zapisywania i odczytywania danych.
- Przetestowaliśmy działanie aplikacji.

---

### **Zadania do samodzielnego wykonania:**

1. **Dodaj pole "rok_wydania" do tabeli "ksiazki". Zaktualizuj formularz oraz skrypty PHP tak, aby móc wprowadzać i wyświetlać rok wydania książki.**

2. **Zmodyfikuj skrypt "lista.php", aby przed tytułem książki wyświetlał się jej numer ID.**

3. **Dodaj na stronie "lista.php" link powrotny do formularza, aby ułatwić dodawanie kolejnych książek.**

---

**Uwaga:**

W powyższych przykładach skupiliśmy się na podstawowej funkcjonalności, pomijając sprawdzanie poprawności połączenia i zabezpieczenia danych. W praktycznych zastosowaniach zawsze należy zabezpieczać dane wprowadzane przez użytkowników, aby uniknąć potencjalnych zagrożeń, takich jak ataki SQL injection.

---

**Powodzenia w dalszej nauce!**
