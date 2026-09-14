# DO1KRT Weltzeituhr (Luxartec-LED-Stil)

Live-Weltzeituhr für die Amateurfunk-Station **DO1KRT** (JO30RR · Eitorf/Stein).

- schwarzes Panel, weiße Weltkarte, rote LED-Zeiten
- **Eitorf** (Heimat) in Cyan, **UTC** in Blau
- läuft standalone und als iFrame auf [qrz.com/db/DO1KRT](https://www.qrz.com/db/DO1KRT)

## Live

Nach dem Netlify-Deploy z. B.:

`https://DEINE-SITE.netlify.app/`

## Lokal testen

```bash
python3 -m http.server 8765
# → http://localhost:8765
```

## Deploy: GitHub → Netlify

### 1. Repo auf GitHub anlegen

```bash
# einmalig, im Projektordner:
git init
git add .
git commit -m "Initial: DO1KRT Weltzeituhr Luxartec-LED"
git branch -M main

# Repo auf GitHub erstellen (Browser: github.com/new)
# Name z.B. do1krt-weltzeituhr, Public, ohne README
# danach:
git remote add origin https://github.com/DEIN-USER/do1krt-weltzeituhr.git
git push -u origin main
```

Oder mit GitHub CLI:

```bash
gh repo create do1krt-weltzeituhr --public --source=. --remote=origin --push
```

### 2. Netlify mit GitHub verbinden

1. [app.netlify.com](https://app.netlify.com) → **Add new site** → **Import an existing project**
2. **GitHub** wählen und Zugriff erlauben
3. Repo `do1krt-weltzeituhr` auswählen
4. Build-Einstellungen:
   - **Branch:** `main`
   - **Build command:** *(leer lassen bzw. wie in `netlify.toml`)*
   - **Publish directory:** `.` (Root)
5. **Deploy site**

Netlify deployed danach **automatisch bei jedem `git push`** auf `main`.

### 3. (Optional) Feste Subdomain

Site configuration → Domain management → z. B. `do1krt-weltzeituhr.netlify.app`

### 4. Bestehende Site umstellen (profound-pony-…)

Falls die alte manuelle Site weiterlaufen soll unter derselben URL:

1. Site öffnen → **Project configuration** → **Build & deploy**
2. **Link repository** → GitHub-Repo wählen
3. Publish directory = `.`
4. Speichern – nächster Push ersetzt den manuellen Deploy

## In QRZ einbetten

In `DO1KRT-qrz-snippet.html` stehen iFrame-URL und CSS.  
URL auf deine Netlify-Adresse setzen:

```html
<iframe class="dk-wc-iframe"
        src="https://DEINE-SITE.netlify.app/?v=1"
        title="Weltzeituhr DO1KRT – live"
        scrolling="no"></iframe>
```

Nach größeren Änderungen `?v=1` → `?v=2` erhöhen (Browser-Cache).

## Dateien

| Datei | Inhalt |
|-------|--------|
| `index.html` | Die Weltzeituhr (einzige Deploy-Datei) |
| `netlify.toml` | Build + Header (iFrame von QRZ erlaubt) |
| `_headers` | Fallback-Header |
| `DO1KRT-qrz-snippet.html` | Komplette QRZ-BIO-Seite zum Kopieren |

## Städte anpassen

In `index.html` das Array `CITIES` bearbeiten → committen → pushen → Netlify deployed live.
