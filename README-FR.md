# Stremio Glass — correctif lecteur iPad 4.1

## Installation
Remplace à la racine de ton dépôt GitHub Pages les fichiers `index.html`, `sw.js`, `manifest.webmanifest`, `icon-192.png` et `icon-512.png` par ceux de cette archive. Fais un commit puis attends le déploiement GitHub Pages. Dans Safari, recharge le site. Si l'ancien lecteur reste en cache, ferme l'application PWA, ouvre le site dans Safari et recharge une fois.

## Corrections
- Ajout du serveur de streaming WebTorrent via `client.createServer({ controller: registration })`, indispensable avant `file.streamTo(video)`.
- Enregistrement et attente du Service Worker avant la création du serveur.
- Affichage des drapeaux de langue lorsqu'ils sont présents dans les métadonnées/texte Torrentio, de la qualité, de la taille et du nombre de pairs si disponible.
- Contrôles personnalisés lecture/pause, vitesse et plein écran compatibles avec les API Safari disponibles.
- Statut torrent avec nombre de pairs, débit et progression.

## Limites réelles
WebTorrent dans Safari utilise WebRTC. Il ne se connecte pas aux pairs BitTorrent TCP/UDP classiques. Un torrent doit avoir au moins un pair WebRTC compatible. Certains conteneurs/codecs (notamment certains MKV/HEVC) ne sont pas lisibles nativement par Safari. Les drapeaux ne peuvent être montrés que si Torrentio fournit un code de langue ou un drapeau dans le nom/la description; sinon ils ne sont pas inventés.

Le Service Worker importe le worker WebTorrent 3.0.21 depuis jsDelivr. Le premier chargement du service worker nécessite donc une connexion internet et que ce CDN soit accessible.
