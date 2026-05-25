# 📄 Lønseddel Checker

Et Python-script der automatisk analyserer PDF-lønsedler og opsummerer arbejdstimer, sygedage og feriedage på tværs af alle dine sedler i én tabel.

---

## 🔍 Hvad gør scriptet?

- Læser alle PDF-lønsedler i en given mappe
- Udtrækker automatisk **arbejdstimer**, **sygedage** og **feriedage** vha. regex-mønstre
- Printer en pæn oversigt med totaler direkte i terminalen
- Understøtter `--debug` flag til fejlsøgning af regex-matches
- Fungerer med og uden `rich`-biblioteket

---

## 🛠️ Installation

```bash
# Klon repo
git clone https://github.com/BenkaDk/Loenseddel-checker.git
cd Loenseddel-checker

# Installer afhængigheder
pip install pdfplumber rich
```

> `rich` er valgfrit — scriptet fungerer uden, men tabellen bliver pænere med.

---

## 🚀 Brug

```bash
# Analyser PDF-filer i en bestemt mappe
python main.py --mappe ./lønsedler

# Aktivér debug-tilstand (viser rå PDF-tekst og regex-matches)
python main.py --mappe ./lønsedler --debug

# Analyser PDF-filer i aktuel mappe
python main.py
```

### Eksempel output

```
╭──────────────────────┬──────────────┬──────────┬───────────╮
│ Fil                  │ Arbejdstimer │ Sygedage │ Feriedage │
├──────────────────────┼──────────────┼──────────┼───────────┤
│ januar_2025.pdf      │       160,00 │      0,0 │       5,0 │
│ februar_2025.pdf     │       152,50 │      2,0 │       0,0 │
├──────────────────────┼──────────────┼──────────┼───────────┤
│ TOTAL                │       312,50 │      2,0 │       5,0 │
╰──────────────────────┴──────────────┴──────────┴───────────╯
```

---

## ⚙️ Tilpasning af mønstre

Scriptet bruger regex-mønstre til at genkende tal i PDF'en. Disse kan tilpasses til dit specifikke lønsystem.

Åbn `main.py` og find `PATTERNS`-ordbogen øverst:

```python
PATTERNS = {
    "arbejdstimer": [
        r"(?:arbejdstimer?|timer\s+i\s+alt|normaltimer|løntimer)[\s:]*([\d]{1,4}[,.]\d{1,2})",
        ...
    ],
    ...
}
```

**Eksempel** — hvis din lønseddel skriver `Norm.timer: 162,00`, tilføj:
```python
r"Norm\.timer[\s:]*([\d]{1,4}[,.]\d{1,2})"
```

Brug `--debug` til at se hvilke mønstre der matcher din lønseddels tekst.

---

## 📦 Krav

| Pakke       | Version | Krav     |
|-------------|---------|----------|
| Python      | 3.10+   | Påkrævet |
| pdfplumber  | latest  | Påkrævet |
| rich        | latest  | Valgfrit |

---

## 📁 Mappestruktur

```
Loenseddel-checker/
├── main.py          # Hovedscript
├── README.md
└── lønsedler/       # Læg dine PDF-lønsedler her (lav selv mappen)
    ├── januar.pdf
    └── februar.pdf
```

---

## 📝 Licens

MIT — brug frit.
