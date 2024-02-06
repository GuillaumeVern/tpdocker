Repo git du projet : [repo tp docker](https://github.com/GuillaumeVern/tpdocker.git)

1) Installation de docker

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.001.png)

2) commandes à tester  docker run hello-world

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.002.png)

docker run -it ubuntu bash

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.003.png)

docker images

docker ps -a![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.004.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.005.png)

docker run -p 80:80 nginx

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.006.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.007.png)

5) executer un serveur web
1) récupérer l’image : 

l’image récupérée précédemment est utilisée

2) vérifier que l’image est présente en local
3) créer un fichier index.html simple![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.008.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.009.png)

4) démarrer un conteneur avec une page html custom

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.010.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.011.png)

5) suppression des conteneurs

création du nouveau conteneur vierge![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.012.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.013.png)

copie des fichiers dans le conteneur

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.014.png)

démarrage du conteneur

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.015.png)

6) builder une image a)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.016.png)

dockerfile :

build de l’image![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.017.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.018.png)

b)

démarrage du conteneurs

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.019.png)

test

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.020.png)

c)

une différence observée est que la méthode 5) est plus rapide pour faire des tests rapides mais la méthode 6) est automatisée après l’avoir fait une fois il n’y a plus besoin d’y toucher

la méthode 6) correspond plus a une pratique devops car il est préférable de réduire au maximum les tâches répétitives, il faut donc chercher a automatiser au maximum.

7) utiliser une base de données dans un conteneur docker

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.021.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.022.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.023.png)

test creation db + table + insertion données

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.024.png)

8) pareil avec docker compose suppression des conteneurs

   docker compose file![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.025.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.026.png)

tout fonctionne![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.027.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.028.png)

1) docker compose est intéressant car il permet de facilement sauvegarder et déployer toute une infrastructure plutôt qu’un seul conteneur unique.
1) les variables d’environnement permettent de configurer l’utilisateur (MYSQL\_USER), la première base (MYSQL\_DATABASE), le mot de passe root (MYSQL\_ROOT\_PASSWORD), etc...
9) observation de l’isolation reseau entre 3 conteneurs

a)

fichier docker compose :

tests des différents réseaux :![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.029.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.030.png)

web sur 172.18

app sur 172.18 et 172.19 db sur 172.19

web ne peut pas ping db mais db et web peuvent ping app![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.031.png)

b)

la ligne NetworkID dans NetworkSettings justifie ce comportement

NetworkID de web : (réseau frontend)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.032.png)

NetworkID de app (2 network id qui correspondent au réseau frontend et backend)

NetworkID de db : (réseau backend)![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.033.png)

![](images/Aspose.Words.bb35b3bb-e509-4a85-ab2a-3eb16c802eed.034.png)

c)

on pourrait vouloir cette configuration réseau pour installer un pare feu sur app afin de protéger les données de la base de données

on pourrait utiliser nginx pour le conteneur web, node pour le conteneur app et mysql pour le conteneur db.




