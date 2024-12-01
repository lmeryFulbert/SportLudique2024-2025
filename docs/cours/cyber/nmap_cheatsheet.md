
# 07-Nmap Cheatsheet

## Commandes de base

### 1. Scans simples
- **Scan d'une seule IP** :
  ```bash
  nmap <IP>
  ```

- **Scan d'un nom de domaine** :
  ```bash
  nmap <nom_de_domaine>
  ```

- **Scan d'une plage d'IP** :
  ```bash
  nmap <IP_debut>-<IP_fin>
  ```

- **Scan d'un sous-réseau** :
  ```bash
  nmap <IP>/<CIDR>
  ```

### 2. Types de scan
- **Scan par défaut (SYN scan)** :
  ```bash
  nmap -sS <IP>
  ```

- **Scan TCP connect** :
  ```bash
  nmap -sT <IP>
  ```

### 3. Scans UDP
- **Scan UDP** :
  ```bash
  nmap -sU <IP>
  ```

- **Scan combiné SYN/UDP** :
  ```bash
  nmap -sS -sU <IP>
  ```

## Scan avancés

### 4. Scan de ports spécifiques
- **Scan d'un port unique** :
  ```bash
  nmap -p <port> <IP>
  ```

- **Scan de plusieurs ports** :
  ```bash
  nmap -p <port1>,<port2> <IP>
  ```

- **Scan d'une plage de ports** :
  ```bash
  nmap -p <port_debut>-<port_fin> <IP>
  ```

### 5. Détection d'OS et de versions de services
- **Détection d'OS** :
  ```bash
  nmap -O <IP>
  ```

- **Détection de la version des services** :
  ```bash
  nmap -sV <IP>
  ```

### 6. Scan en mode furtif
- **Scan furtif avec fragmentation** :
  ```bash
  nmap -f <IP>
  ```

- **Utiliser des paquets de taille aléatoire** :
  ```bash
  nmap --mtu <valeur> <IP>
  ```

### 7. Scan en mode verbeux
- **Verbosité simple** :
  ```bash
  nmap -v <IP>
  ```

- **Verbosity très élevé** :
  ```bash
  nmap -vv <IP>
  ```

### 8. Autres options
- **Scan rapide (limite les tests de ports)** :
  ```bash
  nmap -F <IP>
  ```

- **Scan d'une machine en évitant la détection par les IDS** :
  ```bash
  nmap -D RND:10 <IP>
  ```

- **Exclusion d'hôtes** :
  ```bash
  nmap --exclude <IP1>,<IP2>
  ```

- **Utilisation de scripts Nmap (NSE)** :
  ```bash
  nmap --script=<script> <IP>
  ```

## Exemples courants
- **Scan rapide des 1000 ports les plus courants** :
  ```bash
  nmap -F <IP>
  ```

- **Scan complet de tous les ports (1-65535)** :
  ```bash
  nmap -p- <IP>
  ```

- **Scan avec détection de version des services** :
  ```bash
  nmap -sV <IP>
  ```

- **Scan d'un sous-réseau entier avec détection d'OS et version des services** :
  ```bash
  nmap -O -sV <sous_reseau>
  ```

- **Scan avec export des résultats en XML** :
  ```bash
  nmap -oX scan.xml <IP>
  ```

