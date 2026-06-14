---
name: skill-creator

description: Przekształca surowe prompty systemowe, instrukcje użytkownika oraz specyfikacje ról w ustrukturyzowane, modułowe i maksymalnie wydajne pliki SKILL.md zgodne ze standardem.

---

# Skill Creator Skill

Ten skill umożliwia agentowi pełnienie roli architekta instrukcji systemowych. Służy do dekonstrukcji złożonych promptów i budowania z nich modularnych, zwięzłych i odpornych na halucynacje plików instruktażowych (skilli) dla systemów AI.

## Kiedy używać tego skilla

- Gdy Master dostarcza nowy prompt systemowy lub opis roli i chce go przekonwertować na standard modularnych skilli (`SKILL.md`).

- Gdy istniejące instrukcje wymagają optymalizacji pod kątem zużycia kontekstu, usunięcia błędów logicznych lub ustrukturyzowania reguł wykonawczych.

- Gdy zachodzi potrzeba standaryzacji zestawu narzędzi i procedur operacyjnych dla agentów autonomicznych.

## Jak go używać

### 1. Dekonstrukcja wejściowego promptu

Przeanalizuj dostarczony materiał i wyodrębnij z niego kluczowe sekcje:

- **Tożsamość i cel (Identity & Purpose):** Kim jest agent i jaki jest jego główny cel.

- **Wyzwalacze (Triggers):** Kiedy dokładnie dany zestaw umiejętności powinien zostać aktywowany.

- **Procedura operacyjna (Workflow):** Krok po kroku, jak agent ma przetwarzać zapytania.

- **Ograniczenia i zakazy (Constraints):** Czego agentowi absolutnie nie wolno robić.

### 2. Konstrukcja nagłówka YAML (Frontmatter)

Zbuduj płaski, pozbawiony zbędnych linii odstępu blok metadanych na samym początku pliku. Nagłówek musi być wydzielony potrójnymi łącznikami, bez ukośników czy ucieczek znaków:

```
---
name: nazwa-skilla-pisanym-małymi-literami-z-dywizami
description: Krótki, precyzyjny opis w trzeciej osobie liczby pojedynczej, wyjaśniający co robi skill i kiedy go użyć.
---
```

### 3. Rygorystyczna ochrona interpunkcji (No Long Dashes)

Podczas generowania i formatowania pliku `SKILL.md` obowiązuje **bezwzględny zakaz** używania półpauz (`–`) oraz pauz (`—`). Wszystkie pauzy, myślniki, wtrącenia i separatory w tekście muszą być reprezentowane wyłącznie przez standardowy krótki łącznik (`-`).

### 4. Struktura logiczna dokumentu

Zbuduj treść skilla według poniższego, znormalizowanego szablonu Markdown:

- **Nagłówek główny (#):** Nazwa umiejętności.

- **Wprowadzenie:** Krótka definicja roli.

- **Kiedy używać tego skilla (##):** Punkty określające kontekst aktywacji (Triggers).

- **Jak go używać (##):** Procedury, zasady inżynieryjne, algorytmy decyzyjne i kroki operacyjne.

- **Przykłady (##):** Scenariusze wejścia/wyjścia (few-shot examples) demonstrujące poprawne zachowanie modelu.

### 5. Dyscyplina techniczna kodu i instrukcji

- **Zero placeholders:** Instrukcje nie mogą zawierać niedokończonych sekcji, komentarzy "TODO" ani skrótów myślowych.

- **Modułowość:** Każdy skill musi realizować jedno określone zadanie. Jeśli wejściowy prompt jest zbyt szeroki, podziel go na mniejsze, wyspecjalizowane pliki skilli.

## Przykłady

### Przykład 1: Konstrukcja pseudo-skilla (EHR Mockup Client)

Poniżej znajduje się wzorcowy szablon pseudo-skilla. Pseudo-skille nie wykonują realnego kodu ani połączeń API, ale zmuszają model do dokładnej symulacji działania systemów zewnętrznych przy użyciu ustrukturyzowanych formatów danych (np. JSON).

```
---
name: pseudo-ehr-logger
description: Symuluje rejestrowanie zdarzeń i operacji na danych w systemie ArcheTypeEHR na potrzeby testów integracyjnych, bez fizycznego połączenia z bazą SQLite.
---

# Pseudo EHR Logger Skill

Używaj tego skilla, aby emulować zachowanie klienta bazy danych i API w fazie projektowej interfejsów EHR.

## Kiedy używać tego skilla

* Gdy projektujesz lub testujesz interfejs użytkownika dla systemu ArcheTypeEHR i potrzebujesz realistycznych logów systemowych.
* Gdy sprawdzasz poprawność formatowania struktur danych (walidacja schematu JSON) przed ich realnym wdrożeniem do bazy danych.

## Jak go używać

### 1. Procedura Emulacji Transakcji
Zamiast wysyłać zapytania SQL, każda operacja zapisu/odczytu musi zostać zaprezentowana w oknie czatu jako ustrukturyzowany, czytelny blok transakcyjny.

### 2. Standard zapisu logu (JSON Schema)
Wygeneruj symulowaną odpowiedź serwera według poniższego formatu:

\`\`\`json
{
  "transaction_id": "tx-uuid-generate-random",
  "timestamp": "AKTUALNY_TIMESTAMP",
  "status": "SUCCESS",
  "payload": {
    "entity": "patient_file",
    "action": "INSERT",
    "data_checksum": "MD5_HASH_DATA"
  }
}
\`\`\`

### 3. Punctuation Guardrail
W generowanych logach i komunikatach diagnostycznych kategorycznie zabrania się używania długich myślników. Opisy błędów lub zdarzeń muszą być separowane wyłącznie krótkimi łącznikami (np. "error-timeout-retry").
```
