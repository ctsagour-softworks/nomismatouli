# Νομισματούλι — setup and workflow

## Τι είναι αυτό / What this is

Μια τοπική εφαρμογή για να διαχειρίζεσαι τη συλλογή νομισμάτων και γραμματοσήμων σου, και μια δημόσια σελίδα που μπορείς να ανεβάσεις online.

A local app to manage your coin/stamp collection, plus a public page you can upload online.

---

## Αρχεία / Files

```
collection/
├── server.py         ← Flask server (run this)
├── editor.html       ← admin interface (private — never publish)
├── index.html        ← public page (the one visitors see)
├── catalog.json      ← your data
├── images/           ← photos, named like C-0001-a.jpg, C-0001-b.jpg
└── backups/          ← automatic catalog backups (last 10)
```

---

## Εγκατάσταση / Install (Windows)

1. Make sure Python 3 is installed.
2. Open PowerShell in this folder.
3. Install dependencies:
   ```
   pip install flask Pillow
   ```

---

## Πώς να τρέξεις / How to run

```
python server.py
```

Άνοιξε στον browser / Open in your browser:

- **http://127.0.0.1:8000/editor** → προσθήκη/επεξεργασία / add & edit items
- **http://127.0.0.1:8000/** → δες πώς φαίνεται για τους επισκέπτες / see what visitors see

Για να σταματήσεις / To stop: Ctrl+C in the terminal.

---

## Ροή εργασίας / Workflow

### Προσθήκη νέου κομματιού / Adding a new item

1. Στον editor, κλικ **+ New** / In the editor, click **+ New**
2. Ο editor προτείνει ID όπως `C-0006` / Editor suggests an ID
3. Συμπλήρωσε τα πεδία / Fill in the fields
4. Κλικ στο κενό πλαίσιο εικόνας → διάλεξε φωτογραφία / Click an empty image slot → pick a photo
5. Προσαρμογές: rotate, brightness, contrast, grayscale / Adjust: rotate, brightness, contrast, grayscale
6. Κλικ **Apply** → αποθηκεύεται στο `images/` / **Apply** saves it to `images/`
7. Κλικ **Save** (ή Ctrl+S) / Click **Save** (or Ctrl+S)

### Αλλαγή κατάστασης / Changing status

Διάλεξε κομμάτι → άλλαξε το status → **Save** / Select item → change status → **Save**

- `available` — διαθέσιμο
- `reserved` — κράτηση (εμφανίζεται με ετικέτα)
- `sold` — πουλήθηκε (γκρι + SOLD overlay)

### Διαγραφή / Delete

Κλικ **Delete** → επιβεβαίωση → **Save**. Οι εικόνες σβήνονται αυτόματα.
Click **Delete** → confirm → **Save**. Images auto-removed.

### Duplicate

Χρήσιμο για παρόμοια κομμάτια. Αντιγράφει όλα εκτός από ID και εικόνες.
Handy for similar items. Copies everything except ID and images.

### Backups

Κάθε Save δημιουργεί backup στο `backups/`. Κρατιούνται τα τελευταία 10. Restore από το **Backups** modal.
Every save creates a backup. Last 10 kept. Restore via **Backups** modal.

---

## Δημοσίευση online / Publishing online

### Τι ανεβάζεις / What to upload

**ΜΟΝΟ / ONLY:**
- `index.html`
- `catalog.json`
- `images/` (όλος ο φάκελος)

**ΠΟΤΕ / NEVER:**
- `server.py` ❌
- `editor.html` ❌
- `backups/` ❌

### Πού να ανεβάσεις / Where to host

**GitHub Pages** (δωρεάν):
1. Φτιάξε repo στο github.com
2. Ανέβασε τα 3 πάνω αρχεία
3. Settings → Pages → Deploy from branch → main
4. Η σελίδα θα είναι: `https://USERNAME.github.io/REPONAME/`

Άλλες επιλογές / Other options: Netlify, Cloudflare Pages, Vercel.

### Ρύθμιση επικοινωνίας / Contact info setup

Πριν ανεβάσεις, άνοιξε το `index.html` και άλλαξε:
Before uploading, open `index.html` and change:

```javascript
const CONTACT = {
  viber:     "30XXXXXXXXXX",
  messenger: "your.facebook.username",
  email:     "you@example.com"
};
```

Παράδειγμα Viber: 694 1234567 → `306941234567`.

### Όταν αλλάζεις κάτι / When you update

1. Αλλαγές τοπικά στον editor
2. Save
3. Ανέβασε ξανά `catalog.json` + νέες εικόνες στο `images/`

---

## Σχεδιαστικές σημειώσεις / Design notes

- **Παλέτα**: Αιγαιοπελαγίτικη (μπλε νερό + λευκό + τιρκουάζ + κίτρινο σαφράν + πορτοκαλί ηλιοβασίλεμα + κοραλί)
- **Γραμματοσειρές**: DM Serif Display (τίτλοι), Manrope (σώμα), JetBrains Mono (μετα-στοιχεία)
- **Brand**: Νομισματούλι · Κως

---

## Troubleshooting

**"No module named flask"** → `pip install flask Pillow`

**"Address already in use"** → άλλο πρόγραμμα έχει πάρει το 8000. Άλλαξε `PORT = 8000` σε 8001.

**"Catalog failed to load"** → δες ότι τρέχει ο server και ότι το catalog.json είναι έγκυρο JSON.

**Εικόνες δεν φαίνονται** → υπάρχει το αρχείο στο `images/`; Το όνομα ταιριάζει στο catalog;

---

Καλή συλλογή! / Happy collecting!
