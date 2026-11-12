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

### Direction
Éditorial « magazine de mode », **dark-first** (thème clair via le bouton en haut à droite, mémorisé en localStorage).
Pas de cartes, pas d'ombres, pas de dégradés criards, pas d'emoji : typographie, filets fins, vraies photos.

### Palette (tokens CSS sur `:root` = sombre ; `:root[data-theme="light"]` = clair)

```css
--bg #0E0807  --bg2 #170E0C  --ink #F2E8E4  --mid #C4A09A
--mute #8E6E66  --blush #C8908A  --bl-lt #3A2420  --bl-p #1F1210
--stage #0B0605   /* fond du hero 3D, toujours sombre */
```
Toujours maintenir les deux blocs (sombre + clair).

### Typographie
- Titres : `Bodoni Moda` (300, italique pour les mots accentués en `--blush`)
- Corps : `DM Sans` 300/400/500

### Hero 3D — chevelure WebGL
- `<canvas id="hair">` + module `Hair` dans le script : WebGL brut (pas de librairie), un seul draw call.
- ~1500 mèches (900 sur mobile), chacune passe sur un crâne sphérique puis tombe avec ondulations, vent, et un « peigne » qui écarte les mèches autour de la souris.
- Couleurs racine → longueurs → pointes peintes, définies dans le tableau `shades` (boutons « Try a shade »).
- Fallback sans WebGL : classe `no-gl` → photo `salon.jpg` en fond. `prefers-reduced-motion` → image fixe.
- Animation en pause quand le hero n'est pas visible.

---

## Structure du fichier `index.html`

1. **Nav** — logo, liens, « Book » (Instagram), bouton thème, burger mobile
2. **Hero** — chevelure 3D + titre « Colour, by hand. » + sélecteur de nuances
3. **Marquee** — techniques qui défilent
4. **Statement** — phrase qui s'allume mot à mot au scroll + photo salon en parallaxe
5. **Work** — galerie horizontale épinglée (desktop) / grille (mobile, reduced-motion), filtres, lightbox `<dialog>`
6. **Process** — 3 étapes (Consultation, Hand-painting, Gloss & finish)
7. **Videos** — masquée tant que `vids` est vide
8. **About** — portrait + bio + services
9. **Contact** — CTA Instagram, localisations
10. **Footer** — grand wordmark en contour

### Données JS (arrays à maintenir)

```js
const reals = [ {id, cat, name, img, desc} ];   // cat: 'balayage' | 'colour' | 'cut' | 'bridal' | 'style'
const vids  = [ {id, title, desc, src, thumb} ]; // src: 'videos/vid_01.mp4'
const shades = [ {name, c:[root, mid, ends]} ];  // couleurs de la chevelure 3D
```
Les filtres n'affichent que les catégories présentes dans `reals`.

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
| `images/salon.jpg` | Clotilde au travail dans le salon | hero |
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

1. **Ajouter des vidéos** quand Clotilde les fournit
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
