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

### Palette (tokens CSS sur `:root`)

```css
--bg:    #F9F5F1   /* crème clair, fond principal */
--bg2:   #EFE6DF   /* crème légèrement plus foncé, sections alternées */
--ink:   #120A08   /* quasi-noir chaud, texte principal */
--mid:   #6A4F49   /* brun moyen, liens nav, labels */
--mute:  #A08276   /* brun clair, texte secondaire */
--blush: #C2847C   /* rose terracotta, accent principal */
--bl-lt: #DFC4BE   /* rose poudré clair, bordures */
--bl-p:  #F3EBE8   /* rose très pâle, backgrounds cards */
```

Dark mode complet défini dans le fichier.

### Typographie

- Titres : `Bodoni Moda` — style éditorial mode/luxe
- Corps : `DM Sans` — lisible, moderne, discret

### Principe design

- **Éditorial, photo-first, asymétrique** — les photos parlent, le texte soutient
- **Pas de card-box** : overlays caption sur hover, pas de cadres blancs autour des photos
- **Grille masonry CSS** via `grid-row: span 2` et `grid-column: span 2`
- Fade-in au scroll via `IntersectionObserver`

---

## Structure du fichier `index.html`

### Sections (dans l'ordre)

1. **Nav** — logo "Atelier Clotilde" + liens + bouton "Book a Session"
2. **Hero** — grille 48/52, texte gauche + photo Clotilde droite
3. **Realizations** — filtres par catégorie + grille éditoriale + modal détail
4. **Videos** — grille de vidéos avec thumbnail + player
5. **About** — portrait + bio + chiffres clés
6. **Contact** — Instagram, email, localisation
7. **Footer**

### Données JS (arrays à maintenir)

```js
const reals = [
  {id, cat, name, img, desc}
  // cat: 'balayage' | 'colour' | 'cut' | 'bridal' | 'style'
  // img: chemin relatif depuis la racine ex: 'images/real_01.jpg'
];

const vids = [
  {id, title, desc, src, thumb}
  // src: 'videos/vid_01.mp4'
  // thumb: 'images/thumb_01.jpg'
];
```

---

## Images disponibles

| Fichier | Description | Catégorie |
|---------|-------------|-----------|
| `images/real_01.jpg` | Boucles naturelles balayage miel | balayage |
| `images/real_04.jpg` | Brunette warm caramel (formation Revlon) | colour |
| `images/real_05.jpg` | Long lisse balayage blonde | balayage |
| `images/real_06.jpg` | Blond doré wavy vue de côté | balayage |
| `images/real_07.jpg` | Long sandy blonde balayage | balayage |
| `images/real_08.jpg` | Bob mi-long blonde | cut |
| `images/real_09.jpg` | Bob brunette lustré | cut |
| `images/real_10.jpg` | Fondu foncé vers caramel + boucles | balayage |
| `images/clotilde_hero.jpg` | Portrait Clotilde (photo de profil IG) | hero |
| `images/clotilde_portrait.jpg` | Portrait Clotilde (about section) | portrait |

**Pour ajouter de nouvelles photos** : les déposer dans `images/`, puis ajouter une entrée dans le tableau `reals` dans `index.html`.

---

## Vidéos

Le dossier `videos/` est vide pour l'instant. Quand Clotilde fournit des vidéos :
- Les nommer `vid_01.mp4`, `vid_02.mp4`, etc.
- Créer une thumbnail `images/thumb_01.jpg`, etc.
- Mettre à jour le tableau `vids` dans `index.html`

---

## Ce qu'il faut améliorer / ce qui est à faire

1. **Vrai portrait détouré** pour la section hero — idéalement fond transparent (`.png`)
2. **Ajouter des vidéos** quand Clotilde les fournit
3. **Vrai lien "Book a Session"** — ajouter l'URL Calendly ou autre système de réservation
4. **Coordonnées réelles** — email, numéro WhatsApp, adresse du salon
5. **SEO** — meta description, og:image, sitemap
6. **Déploiement** — le site est prêt à être déployé sur Vercel, Netlify ou GitHub Pages en drag & drop

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
