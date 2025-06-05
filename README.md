Voici une version restructurée et clarifiée de ton guide, organisée par étapes logiques, avec une mise en forme cohérente pour faciliter la lecture et l’exécution :

---

# 📁 Configuration de Samba et Partage de Dossier sur Zorin OS

## 🔧 Étape 1 : Lancer le terminal en mode administrateur

```bash
sudo su
```

---

## 📦 Étape 2 : Mettre à jour les paquets et installer Samba

```bash
apt-get update
apt install samba -y
```

---

## 📂 Étape 3 : Créer le dossier à partager

1. Afficher les fichiers et naviguer :

   ```bash
   ls
   cd ..
   ls
   ```

2. Créer le dossier de partage :

   ```bash
   mkdir nom_du_dossier_partagé
   ls
   ```

3. Modifier les droits d’accès (accès total pour tous) :

   ```bash
   chmod 777 nom_du_dossier_partagé
   ```

---

## 🛠️ Étape 4 : Configurer Samba

### 4.1 Vérifier le fichier de configuration

1. Aller dans le répertoire de configuration :

   ```bash
   cd /etc/samba
   ls
   ```

2. Sauvegarder le fichier de configuration :

   ```bash
   cp smb.conf smb.conf.save
   ```

3. Ouvrir le fichier pour le modifier :

   ```bash
   gedit smb.conf
   ```

---

### 4.2 Créer un groupe et un utilisateur Samba

```bash
groupadd nom_du_groupe
useradd -m -g nom_du_groupe nom_utilisateur
smbpasswd -a nom_utilisateur
```

---

### 4.3 Ajouter une section de partage dans `smb.conf`

Ouvrez à nouveau le fichier :

```bash
gedit smb.conf
```

#### 🔓 Accès total :

```ini
[nom_du_dossier_partage-W]
comment = Partage Samba
path = /home/nom_du_dossier_partagé
valid users = @nom_du_groupe
browseable = yes
read only = no
writable = yes
create mask = 0777
directory mask = 0777
```

#### 🔒 Lecture seule :

```ini
[nom_du_dossier_partage-R]
comment = Partage Samba
path = /home/nom_du_dossier_partagé
valid users = @nom_du_groupe
browseable = yes
read only = yes
writable = no
create mask = 0444
directory mask = 0444
```

---

## 🔄 Étape 5 : Redémarrer Samba

```bash
/etc/init.d/smbd restart
/etc/init.d/nmbd restart
/etc/init.d/smbd status
```

---

# 🌐 Partie 2 : Configuration du réseau en mode "Hôte-only"

### ⚙️ Côté Zorin (VM)

1. Aller dans **Paramètres VM > Réseau**

2. Choisir le mode **Hôte-only**

3. Configurer l'IP manuellement :

   ```
   IP : 192.168.10.1
   Masque : 255.255.255.0
   ```

---

### 🖥️ Côté Windows (client)

1. Aller dans :

   ```
   Paramètres > Réseau et Internet > Ethernet > Modifier l'adresse IP
   ```

2. Configurer manuellement :

   ```
   IP : 192.168.10.5
   Masque : 255.255.255.0
   ```

3. Désactiver temporairement le pare-feu pour les tests.

---

## 🔌 Tester la connexion entre les machines

### Depuis Windows :

```bash
ping 192.168.10.1
```

### Depuis Zorin :

```bash
ping 192.168.10.5
```

> Utilisez `Ctrl + C` pour arrêter le ping.

---

# 🗂️ Partie 3 : Accéder au dossier depuis Windows

1. Ouvrir l’**Explorateur de fichiers**
2. Dans la barre d’adresse, entrer :

   ```
   \\192.168.10.1
   ```
3. Entrer les identifiants Samba
4. Créer un dossier de test

---

## 🔁 Vérification dans les deux sens

### Depuis Zorin :

```bash
cd /home/nom_du_dossier_partagé
ls
mkdir test
ls
```

### Vérifier que le dossier "test" apparaît sur Windows.

---

## ➕ Pied de page personnalisé

(Pas de contenu clair ici, à développer si nécessaire)

---

## 🔁 Clonage local du wiki (optionnel)

(Pas d’instruction donnée, à préciser)

---

Souhaites-tu que je te prépare ce guide en PDF ou dans un format Markdown prêt à être partagé ?
