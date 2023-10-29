# Documentation et informations de déploiement du projet

## Informations

### Dossier [result](result)

#### Fichiers ajoutés

- [.dockerignore](result/.dockerignore)
- [Dockerfile](result/Dockerfile) (l'image a été ajoutée à Docker Hub pour le cluster)

#### Fichiers modifiés (Détail des modifications dans les commentaires)

- [server.js](result/server.js)

### Dossier [vote](vote)

#### Fichiers ajoutés

- [.dockerignore](vote/.dockerignore)
- [Dockerfile](vote/Dockerfile) (l'image a été ajoutée à Docker Hub pour le cluster)

#### Fichiers modifiés (Détail des modifications dans les commentaires)

- [app.py](vote/app.py)

### Dossier [worker](worker)

#### Fichiers ajoutés

- [.dockerignore](worker/.dockerignore)
- [Dockerfile](worker/Dockerfile) (l'image a été ajoutée à Docker Hub pour le cluster)

#### Fichiers modifiés (Détail des modifications dans les commentaires)

- [Program.cs](worker/Program.cs)

### Dossier [voting-app](.)

#### Fichiers ajoutés

- [compose.yaml](./compose.yaml)
- [(swarm) compose.yaml](<./(swarm)%20compose.yaml>)

## Déploiement

Nous avons utilisé `Vagrant` avec `VirtualBox` pour déployer un cluster avec un "manager" et deux "worker".

Voici la liste des étapes pour déployer le projet correctement :

- Installer `Vagrant` et `VirtualBox`
- Exécuter la commande suivante dans le dossier [cluster](cluster) pour installer les machines virtuelles pour le cluster :

```bash
vagrant up
```

- Une fois terminé, exécuter la commande suivante dans le dossier [cluster](cluster), pour se connecter en SSH au "manager" :

```bash
vagrant ssh manager1
```

- Après on créer un cluster avec la commande suivante :

```bash
docker swarm init --advertise-addr 192.168.99.100
```

- La dernière commande vous donne une autre commande à exécuter sur les deux "worker" pour qu'ils rejoignent le "swarm". Pour cela connectez-vous en SSH à ces derniers et exécutez la commande. Exemple de la commande :

```bash
docker swarm join --token <TOKEN>
```

- Ensuite connectez-vous en SSH au "manager", puis ajoutez le fichier [(swarm) compose.yaml](<./(swarm)%20compose.yaml>) dans le "manager". Pour cela il faut créer un fichier, puis le modifier et enfin coller le code du fichier [(swarm) compose.yaml](<./(swarm)%20compose.yaml>). Voici les commandes :

```bash
touch compose.yaml
```

```bash
nano compose.yaml
```

- Après avoir ajouté le fichier dans le "manager", il ne reste plus qu'à déployer avec cette commande :

```bash
docker stack deploy -c compose.yaml voting-app
```

Les services sont maintenant déployés, voici les liens pour les tester :

- Page web du vote : [http://192.168.99.100:8080](http://192.168.99.100:8080)
- Page web des résultats : [http://192.168.99.100:8888](http://192.168.99.100:8888)
