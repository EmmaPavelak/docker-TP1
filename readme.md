Emma PAVELAK 

TP1 

4. Initialiser un nouveau repository git qui vous permettra de sauvegarder les fichiers créés pendant le TP. 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.001.png)

5. Exécuter un serveur web (apache, nginx, …) dans un conteneur docker 
1. Récupérer l’image sur le Docker Hub 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.002.jpeg)

2. Vérifier que cette image est présente en local  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.003.jpeg)

3. Créer un fichier index.html simple 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.004.png)

4. Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume (option 

-v de docker run)  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.005.jpeg)

5. Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.006.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.007.jpeg)

On copie l’index.html dans le conteneur :  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.008.jpeg)

6. Builder une image  
1. A l’aide d’un Dockerfile, créer une image (commande docker build)  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.009.png)

Contenu du Dockerfile : 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.010.png)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.011.jpeg)

2. Exécuter cette nouvelle image de manière à servir la page html (commande docker run)  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.012.png)

3. Quelles différences observez-vous entre les procédures 5. et 6. ?  

La procédure 5 utilise un conteneur existant à partir de dockerHub alors que la 6 créer une nouvelle image à partir d’un docker file. 

Avantages et inconvénients de l’une et de l’autre méthode ? (Mettre en relation ce qui est observé avec ce qui a été présenté pendant le cours)  

Pour la procédure 5 : Avantages : 

Les images de serveur web sont facilement accessibles sur le Docker Hub. 

L'utilisation d'un volume permet de séparer le code de l'application de l'image de l'application, ce qui facilite la maintenance et la mise à jour de l'application. 

Inconvénients : 

L'utilisation de volumes peut rendre la configuration de l'application plus complexe, en particulier si l'on utilise des volumes pour plusieurs applications. 

Pour la procédure 6 : Avantages : 

La méthode est plus flexible que l'utilisation d'une image existante, car elle permet de personnaliser l'image selon les besoins de l'application. 

Les images peuvent être créées de manière reproductible, ce qui facilite la mise à jour et la maintenance de l'application. 

La méthode est portable, car l'image de l'application peut être déplacée facilement entre différents environnements. 

Inconvénients : 

La création d'une image peut être plus complexe et prendre plus de temps que l'utilisation d'une image existante.  La maintenance est aussi plus complexe, car il est nécessaire de mettre à jour régulièrement le Dockerfile. 

7. Utiliser une base de données dans un conteneur docker  
1. Récupérer les images mysql:5.7 et phpmyadmin/phpmyadmin depuis le Docker Hub  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.013.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.014.jpeg)

2. Exécuter deux conteneurs à partir des images et ajouter une table ainsi que quelques enregistrements dans la base de données à l’aide de phpmyadmin  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.015.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.016.jpeg)

8. Faire la même chose que précédemment en utilisant un fichier docker-compose.yml  

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.017.png)

Contenu du docker-compose.yml : 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.018.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.019.jpeg)

1. Qu’apporte le fichier docker-compose par rapport aux commandes docker run ? Pourquoi est-il intéressant ? (cf. ce qui a été présenté pendant le cours)  Le fichier docker compose permet de décrire les configurations de plusieurs conteneurs dans un seul fichier YML. Ce qui simplifie la gestion, la création et le déploiement dans le cas où il y a plusieurs conteneurs. ‘docker run’ lui ne permet de lancer qu’un seul fichier à la fois. 
1. Quel moyen permet de configurer (premier utilisateur, première base de données, mot de passe root, …) facilement le conteneur mysql au lancement ? 
1. En utilisant l’option -e ici,on donne le user, le mot de passe et la database.

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.020.jpeg)

On peut aussi utiliser un fichier de configuration mysql, dans ce cas on lance la commande docker run de la façon suivante : 

docker run –name mysql -v /path/to/my.cnf:/etc/mysql/my.cnf -d mysql :5.7 

9. Observation de l’isolation réseau entre 3 conteneurs  
1. A l’aide de docker-compose et de l’image praqma/network-multitool disponible sur le Docker Hub créer 3 services (web, app et db) et 2 réseaux (frontend et backend). Les services web et db ne devront pas pouvoir effectuer de ping de l’un vers l’autre  

Contenu du docker-compose : 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.021.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.022.jpeg)

2. Quelles lignes du résultat de la commande docker inspect justifient ce comportement ? 

docker inspect permet de récupérer des informations sur le conteneur tel que les réseaux auquels le conteneurs est connecté 

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.023.png)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.024.png)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.025.jpeg)

![](Aspose.Words.a1da8cf7-31fa-4a66-8127-533b34d4d098.026.jpeg)

d.  Dans quelle situation réelles (avec quelles images) pourrait-on avoir cette configuration réseau ? Dans quel but ? Dans le cas ou un service de base données serait connecté à un réseau privé mais également à un réseau public. De cette façon, avoir des services isolés permette aux utilisateurs d’accéder aux services nécessaires en toute sécurité. 

Un autre cas serait un service web connecté à un réseau frontend pour communiquer avec un load balancer ainsi qu’un à un réseau backend pour communiquer avec une base de données. 
