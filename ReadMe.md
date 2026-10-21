# Formula 1 — Hub Sezonul 2026

## 1. Descrierea Proiectului
Acest proiect constă într-o pagină web modernă și responsive dedicată prezentării **Sezonului 2026 de Formula 1**. Scopul paginii este de a oferi fanilor motorsportului o platformă centralizată unde pot explora grila extinsă a sezonului actual (11 echipe și 22 de piloți), clasamentele generale la zi, toate cele 24 de circuite din calendarul competițional, rezultatele curselor disputate și programul etapelor viitoare.

Proiectul a fost dezvoltat pornind de la o structură de bază generată cu ajutorul inteligenței artificiale generative, care a fost ulterior analizată, extinsă și personalizată manual folosind **HTML5 semantic** și **CSS3**.

---

## 2. Analiza Tehnică a Codului

### A. Rolul elementelor HTML5 semantice utilizate
Pentru a asigura o structură logică, ușor de parcurs atât de utilizatori, cât și de motoarele de căutare și cititoarele de ecran (accesibilitate), codul utilizează următoarele etichete semantice:
* **`<header>`**: Delimitează antetul fix (*sticky*) al paginii, care conține logo-ul proiectului și meniul principal.
* **`<nav>`**: Definește blocul de navigare principală, prevăzut cu atributul `aria-label="Meniu principal"`, oferind ancore rapide către secțiunile paginii.
* **`<main>`**: Încapsulează conținutul principal și unic al documentului.
* **`<section>`**: Împarte pagina în zone tematice distincte (`Hero`, `About`, `Services / Clasamente`, `Echipe`, `Piloți`, `Circuite`, `Rezultate` și `Contact`).
* **`<article>`**: Este utilizat pentru fiecare card individual (echipă, pilot, circuit sau rezultat de cursă), deoarece fiecare card reprezintă o entitate informațională independentă.
* **`<aside>`**: A fost introdus în secțiunea *About* pentru a marca semantic un conținut complementar textului principal — citatul celebru al lui Ayrton Senna.
* **`<footer>`**: Conține informațiile de copyright și detalii despre natura educațională a proiectului.

### B. Modul în care este utilizat Flexbox
Layout-ul paginii este construit integral pe **CSS Flexbox** (`display: flex`), fără a depinde de framework-uri externe:
* **Alinierea în Header și Footer (`.header-flex`, `.footer-flex`)**: Utilizează `justify-content: space-between` și `align-items: center` pentru a poziționa logo-ul în stânga și meniul de navigare în dreapta.
* **Secțiunea About și Clasamente (`.about-flex`, `.standings-wrapper`)**: Organizează textul descriptiv și casetele cu statistici/clasamente pe două coloane flexibile.
* **Grilele de carduri (`.services-grid`, `.cards-flex`)**: Folosesc `display: flex`, `flex-wrap: wrap` și proprietatea `gap: 22px`. Prin proprietatea `flex: 1 1 calc(...)`, cardurile își calculează dinamic lățimea (3 carduri pe rând pentru echipe/circuite/rezultate și 4 carduri pe rând pentru piloți pe ecranele desktop) și trec automat pe rândul următor atunci când spațiul devine insuficient.

### C. Realizarea Responsive Design-ului (Media Queries)
Adaptarea paginii pentru diferite dimensiuni de ecran este realizată prin trei praguri (*breakpoints*) principale folosind `@media`:
1. **Ecrane mari (`@media (min-width: 1440px)`)**: Extinde lățimea containerului principal la `1380px` și mărește dimensiunea titlului din secțiunea *Hero* pentru monitoare wide.
2. **Tablete și laptopuri mici (`@media (max-width: 992px)`)**: Modifică dimensiunea cardurilor la `flex: 1 1 calc(50% - 22px)`, afișând câte 2 carduri pe rând în loc de 3 sau 4.
3. **Telefoane mobile (`@media (max-width: 600px)`)**: Schimbă direcția axei principale în `flex-direction: column` pentru meniu, secțiunea *About*, clasamente, grilele de carduri și formularul de newsletter, stivuind elementele vertical pentru o citire optimă pe ecrane înguste.

---

## 3. Probleme Identificate în Codul Generat de AI și Soluții Aplicate

În urma verificării primei variante generate de AI, au fost identificate și rezolvate următoarele limitări:

1. **Date incomplete și neactualizate pentru sezonul 2026**:
   * *Problemă*: Prima versiune generată de AI a inclus doar 4 echipe, 6 piloți, 3 circuite și un clasament restrâns la Top 5.
   * *Soluție*: Codul HTML și CSS a fost extins pentru a reflecta întreaga grilă a sezonului 2026 (**11 echipe** — inclusiv noii constructori Audi și Cadillac, **22 de piloți**, **toate cele 24 de circuite** ordonate cronologic și **clasamentele complete**).
2. **Dimensiuni inegale ale imaginilor din carduri**:
   * *Problemă*: La înlocuirea placeholder-elor cu imagini reale de proporții diferite, cardurile de pe același rând căpătau înălțimi diferite, stricând alinierea vizuală a grilei Flexbox.
   * *Soluție*: S-a impus o înălțime fixă (`height: 220px`) împreună cu proprietatea `object-fit: cover` pentru toate imaginile din carduri (`.team-card img`, `.driver-card img`, `.circuit-card img`), asigurând decuparea proporțională fără deformare.
3. **Afișarea forțată în Bold a textului italic din citatul introdus**:
   * *Problemă*: La adăugarea citatului lui Ayrton Senna în tag-ul `<i>`, întregul text era redat îngroșat (*bold italic*), iar numele autorului plasat în `<strong>` după închiderea tag-ului `<p>` era împins pe un rând nou (deoarece `<p>` este un element de tip *block*).
   * *Soluție*: S-a identificat faptul că linkul Google Fonts pentru *Titillium Web* importa doar greutatea `1,700` pentru stilul italic. Linkul din `<head>` a fost actualizat pentru a include și greutatea normală italică (`1,400`), iar structura HTML din interiorul elementului `<aside>` a fost ajustată pentru afișarea corectă.

---

## 4. Personalizări și Funcționalități Adăugate Manual

Pe lângă actualizarea conținutului, a imaginilor și a paletei cromatice oficiale pentru toate cele 11 echipe (declarate prin variabile CSS în `:root`), au fost implementate manual următoarele îmbunătățiri vizuale și micro-interacțiuni:

* **Efecte de „Color Tint” pe imaginile echipelor și piloților la `:hover`**: Folosind pseudo-elemente `::after` poziționate absolut peste zona imaginii și proprietatea `mix-blend-mode: multiply`, la trecerea cursorului peste un card, imaginea capătă o tentă semitransparentă în culoarea reprezentativă a echipei (ex. *Papaya Orange* pentru McLaren, *Rosso Corsa* pentru Ferrari, *Petronas Teal* pentru Mercedes etc.), însoțită de un efect de zoom fin (`transform: scale(1.05)`) și o ridicare a cardului (`translateY(-8px)`).
* **Efecte `:hover` dedicate pentru Circuite și Rezultate**: Cardurile circuitelor primesc un filtru gri metalic la interacțiune, iar cardurile de rezultate și curse viitoare își modifică subtil nuanța de fundal și primesc o umbră difuză roșie (`rgba(225, 6, 0, 0.15)`).
* **Subliniere animată în bara de navigare**: Linkurile din meniul principal au fost personalizate cu o linie albă creată prin pseudo-elementul `::after`, a cărei lățime crește animat de la `0` la `100%` la `:hover`.
* **Adăugarea unui element semantic `<aside>`**: Includerea citatului motivațional al lui Ayrton Senna în secțiunea *About*.

---

## 5. Structura Fișierelor Predate
* `index.html` — Structura semantică a paginii web.
* `style.css` — Stilizarea completă, variabilele de culoare, layout-ul Flexbox, animațiile `:hover` și regulile `@media`.
* `prompt.txt` — Promptul inițial utilizat pentru generarea structurii de bază.
* `README.md` — Documentația tehnică și analiza proiectului.
* Capturile de ecran (versiunea inițială generată de AI vs. versiunea finală personalizată).

## 6. Link Publicare (GitHub Pages)
Proiectul poate fi accesat live la următoarea adresă:
👉 **[Adaugă aici linkul tău de GitHub Pages după publicare]**
