# Moj Motyw Blokowy (CMS-L4)

Autorski motyw blokowy WordPress stworzony w ramach laboratorium **CMS-L4**.

## Zrealizowane wymagania

* **G1 – Szkielet motywu:** `style.css`, `theme.json` (`version: 3`), `parts/header.html`, `parts/footer.html`.
* **G2 – Hierarchia szablonów:** komplet szablonów w katalogu `templates/` (`index.html`, `single.html`, `page.html`, `archive.html`, `404.html`).
* **G3 – Eksport i wersjonowanie:** motyw wyeksportowany za pomocą wtyczki *Create Block Theme* i opublikowany w repozytorium Git.
* **B1 – Wariant stylu (Tryb ciemny):** `styles/dark.json` nadpisujący globalną paletę kolorów.
* **B2 – Strona główna z wzorców:** dedykowany szablon `templates/front-page.html` złożony z autorskiego wzorca `patterns/sekcja-hero.php` (*Sekcja Hero*) oraz wzorca sekcji wezwania do działania.

---

## P1: Design Tokens — WordPress (`theme.json`) kontra Drupal Canvas

| Kryterium | WordPress (Block Themes) | Drupal Canvas (Drupal CMS 2.0) |
| :--- | :--- | :--- |
| **Źródło prawdy (Single Source of Truth)** | Centralny plik `theme.json` (sekcja `settings`) oraz pliki wariantów w `styles/*.json`. | Architektura komponentowa **Single Directory Components (SDC)** powiązana z globalnymi tokenami motywu bazowego. |
| **Mechanizm zmiennych CSS** | Automatyczna generacja zmiennych przez silnik WordPressa według schematu `--wp--preset--<typ>--<slug>` (np. `--wp--preset--color--cyan-bluish-gray`). | Standardowe zmienne CSS (*CSS Custom Properties*, np. `--color-primary`, `--spacing-md`) definiowane w arkuszach motywu i mapowane na właściwości (*props*) komponentów. |
| **Zakres działania i izolacja** | Globalny kontekst witryny z możliwością nadpisania per blok w `styles.blocks` oraz generowaniem klas pomocniczych (`.has-...`). | Izolacja na poziomie pojedynczego komponentu (SDC) — każdy komponent deklaruje własne style, sloty i warianty w plikach `.component.yml` oraz `.css`. |
| **Warianty stylistyczne (np. Dark Mode)** | Osobne pliki JSON w katalogu `styles/` (np. `styles/dark.json`), przełączane globalnie w *Edytorze Witryny -> Style*. | Warianty konfigurowane na poziomie właściwości (*props*) komponentów oraz globalnych tokenów motywu w wizualnym kreatorze Canvas. |
| **Edycja wizualna (No-Code)** | Panel *Style* w Edytorze Witryny (Site Editor) zapisujący zmiany bezpośrednio do `theme.json` przez *Create Block Theme*. | Wizualny edytor stron typu *drag-and-drop* (Drupal Canvas) operujący bezpośrednio na komponentach SDC i ich tokenach. |

### Podsumowanie różnic architektonicznych

1. **Podejście scentralizowane vs komponentowe:** WordPress opiera system projektowy na jednym centralnym pliku konfiguracyjnym (`theme.json`), z którego rdzeń systemu sam wyprowadza reguły CSS dla wszystkich bloków. Drupal Canvas przyjmuje podejście *component-first* (SDC), w którym design tokeny zasilają niezależne, hermetyczne komponenty interfejsu.
2. **Spójność i skalowalność:** W obu podejściach zmiana wartości tokenu (np. koloru głównego lub kroju pisma) aktualizuje wygląd całej witryny bez ręcznej edycji wielu szablonów, przy czym Drupal Canvas silniej wymusza strukturę poprzez typowane właściwości (*props*) komponentów.