# AutomateUSA — Landing Page (Automate Chicago 2026)

Statyczna strona (landing page) DBR77 na targi **Automate 2026 w Chicago**.
Cel: podpiąć ją pod publiczną domenę **`automate.dbr77.com`**.

Strona to czysty **HTML/CSS/JS w jednym pliku** (`index.html`) + zdjęcia zespołu
w `team/`. Brak backendu, brak build-stepu — wystarczy serwować pliki statycznie.

---

## 📁 Co jest w repo

```
AutomateUSA/
├── index.html        ← cała strona (HTML + CSS + JS inline)
├── team/             ← zdjęcia zespołu (Torian, Justyna, Piotr)
│   ├── torian.png
│   ├── justyna.png
│   └── piotr.png
├── CNAME             ← domena dla GitHub Pages: automate.dbr77.com
└── README.md         ← ten plik
```

Logo DBR77 jest wbudowane jako inline SVG w `index.html` — nie wymaga pliku.

---

## 🚀 Dla Konrada — jak podpiąć pod `automate.dbr77.com`

Są dwie drogi. **Rekomendowana: GitHub Pages** (zero kosztów, repo już ma plik `CNAME`).

### ✅ Opcja A — GitHub Pages (rekomendowana)

1. **Włącz Pages w repo:**
   `Settings → Pages → Build and deployment`
   - **Source:** `Deploy from a branch`
   - **Branch:** `main` / katalog `/ (root)` → **Save**

2. **Custom domain** (powinno wczytać się automatycznie z pliku `CNAME`):
   - W `Settings → Pages → Custom domain` wpisane: `automate.dbr77.com`
   - Zaznacz **Enforce HTTPS** (gdy certyfikat się wygeneruje, ~kilka–kilkanaście minut)

3. **DNS** (u operatora domeny `dbr77.com`):

   > ⚠️ **UWAGA:** rekord `automate.dbr77.com` **już istnieje** i wskazuje obecnie na
   > serwer dbr77.com (`165.227.168.105`, CNAME → `dbr77.com`). Trzeba go **zmienić**
   > (nie dodawać drugiego!), żeby wskazywał na GitHub Pages:

   | Typ   | Nazwa (host) | Wartość (zmień na) | Proxy / TTL     |
   |-------|--------------|--------------------|-----------------|
   | CNAME | `automate`   | `dbr77.github.io`  | DNS only / Auto |

   > Jeśli DNS jest na Cloudflare — ustaw **DNS only** (szara chmurka), nie „Proxied",
   > żeby GitHub mógł wystawić własny certyfikat SSL.
   > Po zmianie rekordu wróć do `Settings → Pages` i kliknij **Enforce HTTPS**, gdy
   > GitHub zweryfikuje domenę i wygeneruje certyfikat (kilka–kilkanaście minut).

4. Po propagacji DNS (zwykle kilkanaście minut, max do 24h) strona działa pod
   **https://automate.dbr77.com**.

Adres techniczny Pages (do testu zanim wstanie domena):
**https://dbr77.github.io/AutomateUSA/**

### Opcja B — Cloudflare Pages / Netlify / Vercel

Jeśli wolisz hosting zewnętrzny:
1. Połącz konto z repo `DBR77/AutomateUSA`.
2. Build command: **(puste)** · Output directory: **`/`** (root) — to czysty statyczny HTML.
3. Custom domain: `automate.dbr77.com` → ustaw rekord CNAME wg instrukcji danego hostingu.
   (Wtedy plik `CNAME` z repo można zignorować — jest tylko dla GitHub Pages.)

---

## ⚠️ Jedna rzecz do podpięcia — formularz „Leave Your Contact" / „Recommended Next Step"

Formularz (imię, nazwisko, email, telefon, problem, zgoda) **na razie zapisuje
dane tylko lokalnie** w `localStorage` przeglądarki — czyli **nie trafiają nigdzie
do CRM**.

Żeby leady trafiały do HubSpot/CRM, trzeba podpiąć endpoint. W `index.html`
jest oznaczone miejsce w sekcji `<script>`:

```js
// TODO: POST `lead` to your CRM / HubSpot endpoint here.
// fetch('https://your-endpoint', { method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify(lead) });
```

Wystarczy wpisać URL formularza HubSpot (Forms API) lub własnego endpointu i odkomentować.
Obiekt `lead` zawiera: `firstName, lastName, email, phone, challenge, consent, ts, source`.

Linki do umawiania spotkań (przyciski „Book a meeting") działają od razu — prowadzą
do indywidualnych kalendarzy HubSpot (Torian / Justyna / Piotr).

---

## 🔧 Podgląd lokalny

```bash
# dowolny statyczny serwer, np.:
npx serve .
# albo
python3 -m http.server 8080
```

Strona jest mobile-first — testować przede wszystkim na telefonie (na targach
ludzie skanują QR i wchodzą z mobile).
