# Serveur Multimédia avec VPN

Cette configuration détaille la mise en place d'un serveur multimédia sécurisé par VPN en utilisant Docker Compose. Elle inclut une collection de services tels que des clients torrent, des serveurs multimédias et des indexeurs, tous routés à travers un client OpenVPN pour une sécurité et une confidentialité accrues.

## Services Inclus

- **Client OpenVPN** : Connexion sécurisée pour tous les services.
- **qBittorrent** : Client torrent avec une interface web.
- **Sonarr** : Outil de gestion de séries TV.
- **Radarr** : Outil de gestion de films.
- **Jackett** : Support API pour vos trackers torrent favoris.
- **Overseerr** : Outil de gestion de demandes et de découverte de médias.
- **Flaresolverr** : Permet d'accéder à des sites web protégés par Cloudflare.
- **Plex** : Logiciel serveur média pour organiser et diffuser votre contenu multimédia.

## Prérequis

- Docker et Docker Compose installés sur votre système hôte.
- Abonnement VPN et fichiers de configuration (non inclus dans cette configuration).
- Token PLEX_CLAIM valide si vous configurez Plex pour la première fois.

## Variables d'Environnement

Avant de démarrer, vous devez configurer vos variables d'environnement. Créez un fichier `.env` dans le répertoire de votre projet et définissez les variables suivantes :

```bash
PUID=<votre-id-utilisateur>
PGID=<votre-id-groupe>
TZ=<votre-fuseau-horaire>
RACINE=<chemin-de-vos-données>
PLEX_CLAIM=<votre-claim-plex>
```

## Instructions de Configuration

1. Clonez ce dépôt ou copiez le `docker-compose.yml` sur votre machine.
2. Créez un fichier `.env` dans le répertoire racine de ce projet comme décrit dans la section Variables d'Environnement.
3. Placez vos fichiers de configuration OpenVPN dans le répertoire `${RACINE}/vpn/config`.
4. Démarrez les services avec la commande :

```bash
docker-compose up -d
```

## Accès aux Services

- Flaresolverr : http://<ip-hôte>:8191
- qBittorrent : http://<ip-hôte>:8586
- Jackett : http://<ip-hôte>:9117
- Radarr : http://<ip-hôte>:7878
- Sonarr : http://<ip-hôte>:8989
- Overseerr : http://<ip-hôte>:5055
- Plex : http://<ip-hôte>:32400/web

## Remarques

- Les fichiers de configuration OpenVPN doivent être nommés `openvpn.ovpn` et `openvpn.auth` et doivent être placés dans le répertoire `${RACINE}/vpn/config`.

- Si vous utilisez un fournisseur de VPN qui utilise des certificats, vous devez placer vos fichiers de certificat dans le répertoire `${RACINE}/vpn/config` et les référencer dans votre fichier `.ovpn` comme suit :

```bash
ca /config/openvpn.crt
cert /config/openvpn.crt
key /config/openvpn.key
```

- Si vous utilisez un fournisseur de VPN qui utilise des clés, vous devez placer vos fichiers de clé dans le répertoire `${RACINE}/vpn/config` et les référencer dans votre fichier `.ovpn` comme suit :

```bash
auth-user-pass /config/openvpn.auth
```
