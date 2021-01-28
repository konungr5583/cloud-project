# Cloud public - TP1

## Instructions
Durant ce TP, nous allons mettre en oeuvre l'infrastructure-as-a-service que nous avons vu durant le cours. Pour ce faire, nous allons déployer l'application PetClinic sur une machine virtuelle.

Voici à quoi ressemble l'architecture de l'application
![Architecture](https://spring-petclinic.github.io/images/petclinic-microservices-architecture.png "Architecture")

Le TP est découpé en deux parties : le fichier ```README.md``` suivant, ainsi qu'un fichier ```ÀNSWER.md``` qui contient 10 questions à répondre.

Le principe du TP est de répondre aux questions dans le fichier ```ANSWER.md``` et de le pousser sur votre repository. Le reste est expliqué au fur et à mesure de ce TP.

## 1 : Git
### 1.0 : Forker le repo du lab
Suivre le lien présent au tableau pour forker ce repository dans votre repository personnel GitHub Classroom. Si vous avez accès au repository, cela veut dire que la manipulation a bien fonctionné.

### 1.1 : Cloner le repository
Clonez le repo nouvellement copié sur votre ordinateur 
> A partir de maintenant, **vous ne travaillerez plus que dans votre copie**. Vous n'avez plus à revenir sur [le projet parent](https://github.com/cours-hei/tp1).
 
### 1.2 : Créer une issue
> ⚠️  **WARNING**: Créez une issue s'intitulant `1.2` ayant pour contenu les commandes que vous avez effectuées pour réaliser le clone de votre repo git.

## 2 : IaaS
Dans un premier temps, nous allons déployer cette architecture sur une machine virtuelle.

### 2.0 : Créer une machine virtuelle AWS
Pour créer une machine EC2, aller sur le portail AWS Educate et cliquer sur le menu EC2. Cliquer ensuite sur le bouton Launch Instance.

Il est conseillé de démarrer une machine virtuelle Ubuntu afin de pouvoir installer l'application facilement.

### 2.1 : Se connecter à la machine
Une fois la machine virtuelle créée, se connecter à la machine
```bash
ssh ubuntu@<public-ip>
```

### 2.2 : Installer les outils nécessaires
Installer ensuite les outils nécessaires au démarrage de l'application. Pour faire tourner correctement l'application, les outils à installer sont : ```git```, ```maven``` et ```openjdk-8-jdk```
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.2` ayant pour contenu les commandes que vous avez effectuées

### 2.3 : Cloner le repo Spring PetClinic
Cloner ensuite le repo PetClinic https://github.com/spring-projects/spring-petclinic
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.3` ayant pour contenu les commandes que vous avez effectuées

### 2.4 : Lancer Spring PetClinic
Lancer la commande suivante afin de compiler, puis lancer l'application
```bash
cd spring-petclinic
./mvnw package
java -jar target/*.jar
```

### 2.5 : Se connecter à l'application
Maintenant, essayer de se connecter à l'application. Il sera normalement impossible de s'y connecter.
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.5` expliquant pourquoi il est impossible de se connecter à l'application

### 2.6 Ouvrir le firewall
Afin de pouvoir se connecter à l'application, il faut ouvrir le port où écoute l'application. Le port d'écoute est le ```8080```

Pour ouvrir le port, il est nécessaire d'aller dans les ***Security Groups***.
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.6` ayant pour contenu les commandes que vous avez effectuées

### 2.7 : Vérifier le bon fonctionnement
Ouvrir le navigateur et aller à l'url suivante afin de voir l'application Petclinic : ```http://<public-ip>:<port>```

### 2.8 : Installer MariaDB
Par défault, l'application démarre sans serveur de base de données et donc ne persiste pas les données que vous pouvez modifier. Afin de pouvoir persister les données, il est nécessaire d'installer MariaDB et de modifier le fichier de configuration de l'application afin de pointer sur la base de données.

Installer MariaDB en suivant le mode opératoire suivant : https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.8` ayant pour contenu les commandes que vous avez effectuées

### 2.9 : Installer les schémas et les données
Dans le repo git, il existe les instructions afin de créer la base de données PetClinic. Ces instructions sont situés ici : ```spring-petclinic/src/main/resources/db/mysql/```

Le fichier txt présent dans le répertoire fait référence à Docker. Dans le cadre de ce TP, nous n'allons pas installer Docker, puisque nous avons déjà installé MariaDB.

Les fichiers à jouer sur la base de données MariaDB sont dans l'ordre : ```user.sql```, ```schema.sql``` et ```data.sql```

### 2.10 : Redémarrer l'application
Redémarrer l'application PetClinic avec le bon profil afin que l'application puisse utiliser le serveur MySQL. La commande doit être la suivante : ```java -Dspring.profiles.active=mysql -jar target/*.jar```

### 2.11 : Vérifier le bon fonctionnement
Ouvrir le navigateur et aller à l'url suivante afin de voir l'application Petclinic : ```http://<public-ip>:<port>```
