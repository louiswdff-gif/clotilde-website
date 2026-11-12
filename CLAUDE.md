# Atelier Clotilde — Site de Portfolio

## Contexte du projet

Site portfolio/présentation pour **Clotilde Bouttet** (`@clotilde.frenchhair`), maître coloriste professionnelle basée à Paris / Thonon-les-Bains.

- **Ce n'est pas un site e-commerce** — pas de panier, pas de produits à acheter
- **Objectif** : présenter les réalisations, créer l'envie de prendre rendez-vous
- **Langue** : entièrement en anglais
- **Nom du site** : Atelier Clotilde
- **Instagram** : https://www.instagram.com/clotilde.frenchhair/

---

## Stack technique

- **Un seul fichier** : `index.html` — HTML + CSS + JS inline, zéro dépendance build
- **Fonts** : Google Fonts — Bodoni Moda (titres, éditorial) + DM Sans (corps)
- **Images** : dossier `images/` — PNG/JPG capturées depuis Instagram
- **Vidéos** : dossier `videos/` — à ajouter quand disponibles
- **Pas de framework**, pas de Node, pas de bundler — le fichier s'ouvre directement dans un navigateur

---

## Design system

### Direction (validée par le client, nov. 2026)
Beige clair, éditorial, **pas de codes « template »** : pas de bandeau défilant, pas d'étapes numérotées,
pas de chiffres clés, pas de cartes ni d'ombres. Clotilde est le sujet principal.

### Palette (tokens sur `:root`, thème clair uniquement)
```css
--bg #EDE5DA  --paper #F5F0E9  --ink #2B231E  --mid #5F5046
--mute #85746A  --accent #9A6650  --line #D6CABC
```

### Typographie
Titres `Bodoni Moda` 400 (italique pour les mots en `--accent`), corps `DM Sans` 300.

### Fil conducteur : la ligne de coupe + ciseaux 3D
- Une ligne pointillée (SVG `#cutSvg`) serpente sur toute la page, **entre** les photos et les textes.
- Elle est construite à partir des attributs `data-cut="x@y x@y"` (x = fraction de largeur de page,
  y = fraction de hauteur de l'élément). Sur mobile (< 900px) elle passe dans les marges.
- Des ciseaux 3D (three.js r128, CDN cdnjs) suivent la ligne au scroll, s'ouvrent/se ferment
  (« snip ») et la ligne derrière eux devient pleine (= découpée).
- Défilement fluide : Lenis 1.1.13 (CDN jsdelivr). Désactivé si `prefers-reduced-motion`.

### Accueil
Prénom « Clotilde » en très grand, Clotilde détourée devant (`images/clotilde_cut.webp`,
fond transparent, fondu à gauche et en bas). Sur mobile : prénom, puis photo, puis texte (empilés).

---

## Structure du fichier `index.html`

1. **Header** — marque, liens, Instagram
2. **Cover** — prénom + Clotilde détourée
3. **Intro** — une phrase sur sa façon de travailler
4. **Work** — collage de photos (`reals`), lightbox `<dialog>`
5. **About** — portrait + bio
6. **Contact** — « Take a seat » → Instagram, villes
7. **Footer**

### Données JS
```js
const reals = [ {id, cat, name, img, desc} ];   // cat: 'balayage' | 'colour' | 'cut' | 'bridal' | 'style'
```

---

## Images disponibles

| Fichier | Description | Catégorie |
|---------|-------------|-----------|
| `images/real_11.jpg` | Bronde soft, vue de profil | balayage |
| `images/real_12.jpg` | Brunette vers cuivré (session Revlon) | colour |
| `images/real_13.jpg` | Boucles avec mèches dorées | balayage |
| `images/real_14.jpg` | Balayage miel mi-long | balayage |
| `images/real_15.jpg` | Blond lumineux ondulé | colour |
| `images/real_16.jpg` | Long balayage, vue de face (aussi og:image) | balayage |
| `images/real_17.jpg` | Melt racine naturelle vers pointes claires | balayage |
| `images/real_18.jpg` | Brunette ondulée brillante | style |
| `images/real_19.jpg` | Brunette longue, noir et blanc | style |
| `images/real_20.jpg` | Carré long (lob) balayage | cut |
| `images/real_21.jpg` | Blond doré racine ombrée | colour |
| `images/clotilde_cut.webp` | Clotilde (pantalon rose) coiffant une cliente, détourée, fond transparent — source IMG_5646 | accueil |
| `images/salon.jpg` | Photo salon d'origine (non utilisée actuellement) | — |
| `images/clotilde_portrait.jpg` | Portrait de Clotilde | portrait (About) |

Les originaux d'appareil photo (`IMG_*`, `*.HEIC`) sont ignorés par git : ils sont lourds et contiennent la position GPS. Toujours en faire une version web (max 1200 px, ~150 Ko, sans EXIF) avant de les utiliser.

**Pour ajouter de nouvelles photos** : les déposer dans `images/`, puis ajouter une entrée dans le tableau `reals` dans `index.html`.

---

## Vidéos

Le dossier `videos/` est vide pour l'instant. Quand Clotilde fournit des vidéos :
- Les nommer `vid_01.mp4`, `vid_02.mp4`, etc.
- Créer une thumbnail `images/thumb_01.jpg`, etc.
- Mettre à jour le tableau `vids` dans `index.html`

---

## Ce qu'il faut améliorer / ce qui est à faire

1. **Photo d'accueil** — remplacée par IMG_5646 (meilleure qualité) ; une version encore plus grande serait un plus
2. **Lien de réservation** — pour l'instant tout pointe vers Instagram ; remplacer si Planity/Calendly
3. **Coordonnées réelles** — téléphone, email, adresse du salon (retirés du site tant qu'ils ne sont pas fournis)
4. **Vérifier les textes** — noms/descriptions des réalisations et « twelve years » à valider par Clotilde
5. **SEO** — sitemap.xml, robots.txt et URL absolues (og:image, canonical) une fois le domaine connu

---

## Directives de développement

- **Ne jamais introduire de build system** — le projet doit rester un seul `index.html`
- **Ne pas créer de fichiers CSS/JS séparés** — tout reste inline dans `index.html`
- **Maintenir le design éditorial** : pas de cards blanches, pas d'ombres lourdes, pas de gradients criards
- **Mobile-first** : toujours tester à 375px de large
- **Dark mode** : toujours maintenir les deux blocs de tokens dark
- **Les photos viennent de `images/`** — ne jamais hardcoder de URLs externes pour les images du portfolio

---

## Déploiement rapide

Le site est un fichier statique. Pour mettre en ligne :

```bash
# Option 1 — GitHub Pages (gratuit)
# → Settings > Pages > Deploy from branch > main > / (root)

# Option 2 — Netlify (gratuit)
# → Drag & drop du dossier clotilde-website sur netlify.com/drop

# Option 3 — Vercel
vercel deploy
```

---

## Prompt pour ajouter de nouvelles réalisations

> "Ajoute ces nouvelles photos au portfolio de Clotilde :
> - `images/real_11.jpg` — [description de la coiffure]
> - `images/real_12.jpg` — [description]
>
> Crée une entrée dans le tableau `reals` pour chacune avec la bonne catégorie
> (balayage / colour / cut / bridal / style) et une description en anglais
> de 1-2 phrases, dans le style éditorial du site."

---

*Site construit en novembre 2026 — Atelier Clotilde, maître coloriste à Paris.*
