
---
name: knowledge-visualizer  
description: Generuje estetyczne, responsywne i interaktywne karty wiedzy oraz dashboardy w formacie HTML i CSS, pozwalające na błyskawiczne strukturyzowanie i przyswajanie skomplikowanych danych.  



---

# Wizualizator Wiedzy - Karta Faktów

Ten skill pozwala na błyskawiczne przekształcanie surowych danych i złożonych konceptów w zapamiętywalne, interaktywne interfejsy użytkownika (UI). Celem jest osiągnięcie maksymalnego efektu poznawczego przy użyciu minimalistycznego, czystego kodu.

## Kiedy używać tego skilla

- Gdy Master potrzebuje czytelnie przedstawić skomplikowany proces, zestaw statystyk lub reguły techniczne.

- Gdy chcesz stworzyć interaktywne podsumowanie, dashboard lub strukturę typu Bento Grid.

- Gdy surowy tekst jest zbyt monotonny lub trudny do szybkiej analizy.

## Jak go używać

### 1. Stylistyka i Design System (Dark Editorial Premium)

Zaimplementuj spójny, profesjonalny i nowoczesny wygląd:

- **Tło:** Głęboka, nasycona ciemność (np. `#0D0F14`).

- **Elementy interfejsu:** Szklany efekt (glassmorphism) z rozmyciem tła (`backdrop-filter: blur()`) i subtelnymi, półprzezroczystymi ramkami.

- **Zaokrąglenia:** Nowoczesne zaokrąglenia krawędzi (standardowo klasy Tailwind typu `rounded-2xl` lub `rounded-3xl`).

- **Przestrzeń (Whitespace):** Dużo wolnej przestrzeni zapewniającej oddech i ułatwiającej skanowanie wzrokiem.

- **Typografia:** Czyste, nowoczesne fonty bezszeryfowe (standardowo Inter z Google Fonts).

### 2. Architektura Informacji i Interakcja

- **Układ Bento Grid:** Dziel informacje na kafelki o różnych rozmiarach i wagach wizualnych. Najważniejsze statystyki lub główne zasady powinny zajmować największe bloki.

- **Interaktywność:** Dodaj proste, bezbłędne mechanizmy interaktywne (np. filtry, karty z zakładkami, harmonijki, kalkulatory) napisane w czystym JavaScript.

- **Responsywność (RWD):** Kod musi wyglądać nienagannie zarówno na monitorach desktopowych, jak i na ekranach telefonów komórkowych. Unikaj sztywnych szerokości w pikselach.

### 3. Techniczne Standardy i Bezpieczeństwo

- **Brak zewnętrznych bibliotek JS:** Unikaj ładowania niepotrzebnych, ciężkich skryptów.

- **Paczki CSS:** Jeśli używasz Tailwind, ładuj go wyłącznie z bezpiecznego CDN w sekcji head.

- **Zabezpieczenie CSP (Content Security Policy):** Aby uniknąć rozsypania się interfejsu w środowiskach z restrykcyjnym CSP, zawsze dołączaj podstawowy blok `<style>` zawierający krytyczne style (layout, kolory tła i tekstu) jako fallback.

- **Atrybuty SVG:** Dla każdego elementu SVG zawsze definiuj parametry `width` i `height` bezpośrednio w znaczniku `<svg>`. Zapobiega to ich gigantycznemu powiększeniu przed załadowaniem arkusza CSS.

### 4. Dyscyplina Treści

- Nigdy nie upraszczaj ani nie usuwaj merytorycznych informacji na rzecz wyglądu.

- Kod musi być kompletny, w pełni funkcjonalny, bez komentarzy typu placeholder.
