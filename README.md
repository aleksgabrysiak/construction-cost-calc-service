# Kalkulator Kosztów Usług Remontowo-Wykończeniowych

Prosta aplikacja webowa do szacowania kosztów remontu mieszkania. Generuje profesjonalne oferty PDF z pełną obsługą polskich znaków. Działa w całości jako jeden plik HTML — bez instalacji, bez backendu, gotowa do publikacji na GitHub Pages.

---

## Funkcje

- **Nazwa klienta** — pole na górze strony; trafia do nagłówka PDF i nazwy pliku
- **Katalog usług** — konfigurowalne pozycje (nazwa, jednostka, domyślna cena); dostępne jednostki: m², mb, szt., godz., kpl.
- **Pomieszczenia** — dynamiczne dodawanie pomieszczeń (kuchnia, łazienka itp.) z dowolną liczbą usług każde
- **Ilość i cena** — etykieta pola ilości zmienia się automatycznie wraz z wybraną jednostką
- **Podsumowanie** — tabela na żywo z kolumnami: Usługa / Pomieszczenie / Ilość / Jednostka / Cena / Łącznie + suma końcowa
- **Eksport PDF** — generowany przez PDFMake z pełną obsługą polskich znaków (Roboto), nazwą klienta, datą i stopką
- **Zapis lokalny** — katalog usług, pomieszczenia i nazwa klienta zapisywane w `localStorage`; odtwarzane przy kolejnym otwarciu strony
- **Sekcje zwijane** — każda sekcja (katalog, pomieszczenia, podsumowanie) oraz każde pomieszczenie można zwinąć/rozwinąć kliknięciem nagłówka

---

## Szybki start

1. Otwórz `index.html` w przeglądarce — żadna instalacja nie jest potrzebna
2. W sekcji **Katalog usług** skonfiguruj swoje usługi i ceny domyślne, a następnie kliknij **💾 Zapisz katalog**
3. W sekcji **Pomieszczenia** dodaj pomieszczenia, przypisz usługi i wpisz ilości oraz stawki
4. Kliknij **📄 Pobierz PDF** — plik zostanie pobrany od razu do przeglądarki

---

## Konfiguracja przed publikacją

Przed wgraniem na GitHub Pages otwórz `index.html` w edytorze i znajdź tablicę `DEFAULT_SERVICES` (oznaczona komentarzem `← Edit this array before publishing`). Ustaw swoje domyślne usługi, jednostki i ceny — będą wczytywane przy pierwszym uruchomieniu przez nowego użytkownika (zanim cokolwiek zostanie zapisane w localStorage).

```js
const DEFAULT_SERVICES = [
  { name: "Malowanie — ściany",  unit: "m²",   defaultPrice: 20 },
  { name: "Podłogi drewniane",   unit: "m²",   defaultPrice: 50 },
  { name: "Montaż drzwi",        unit: "szt.", defaultPrice: 150 },
  // ...
];
```

---

## Publikacja na GitHub Pages

1. Utwórz repozytorium na GitHubie i wgraj plik `index.html`
2. Wejdź w **Settings → Pages → Source → Deploy from branch → main / root**
3. Udostępnij wygenerowany link bratu lub klientowi

---

## Stos technologiczny

| Element | Technologia |
|---|---|
| Interfejs | Czysty HTML / CSS / JavaScript (bez frameworków) |
| Generowanie PDF | [PDFMake 0.2.7](https://pdfmake.github.io/docs/) + czcionka Roboto (vfs_fonts) |
| Zapis danych | `localStorage` przeglądarki |
| Hosting | GitHub Pages (pojedynczy plik, bez buildu) |

---

## Struktura pliku

```
index.html
├── <style>        — wszystkie style CSS (responsywne, zwijane sekcje)
├── <body>
│   ├── Nazwa klienta
│   ├── Katalog usług (z zapisem)
│   ├── Pomieszczenia (z zapisem)
│   └── Podsumowanie + eksport PDF
└── <script>
    ├── DEFAULT_SERVICES  ← tu konfigurujesz katalog
    ├── Logika katalogu, pomieszczeń, wierszy usług
    ├── refreshSummary()  — tabela podglądu na żywo
    ├── generatePDF()     — generowanie PDFMake
    └── loadFromStorage() / save*() — persystencja danych
```
