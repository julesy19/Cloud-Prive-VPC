# Cloud-Prive-VPC
 création d'un VPC

# Présentation de l'atelier et des objectifs
La mise en réseau traditionnelle est difficile. Elle nécessite du matériel, du câblage, des configurations complexes et des compétences spécialisées. Amazon Virtual Private Cloud (Amazon VPC) masque cette complexité et facilite le déploiement de réseaux privés sécurisés.
Cet atelier vous montre comment créer votre propre cloud privé virtuel (VPC) et y déployer des ressources.
À la fin de cet atelier, vous serez en mesure d'effectuer les tâches suivantes :
déployer un VPC ;
créer un sous-réseau public ;
créer un sous-réseau privé ;
créer une passerelle Internet et l'attacher au VPC ;
créer un serveur d'application pour tester le VPC. 

<------------------------>


<img width="985" height="619" alt="image" src="https://github.com/user-attachments/assets/29204369-768e-4ff8-b6bb-2e9a3a4fc9b0" />


<------------------------->


# Tâche 1 : création d'un VPC
Vous allez commencer par utiliser Amazon VPC pour créer un VPC.
Un VPC est un réseau virtuel dédié à votre compte Amazon Web Services (AWS). Il est logiquement isolé des autres réseaux virtuels dans le cloud AWS. Différentes ressources AWS, telles que des instances Amazon Elastic Compute Cloud (Amazon EC2), peuvent être lancées dans le VPC. Vous pouvez configurer le VPC en modifiant sa plage d'adresses IP et créer des sous-réseaux. Vous pouvez également configurer des tables de routage, des passerelles réseau et des paramètres de sécurité.

Dans la barre de recherche de la console de gestion AWS, saisissez et sélectionnez VPC pour ouvrir la console Amazon VPC.
La console VPC fournit un assistant qui peut créer automatiquement plusieurs architectures VPC. Toutefois, dans cet atelier, vous allez créer les composants VPC manuellement.

Dans le volet de navigation de gauche, choisissez Vos VPC.
Un VPC par défaut est fourni afin que vous puissiez lancer des ressources dès que vous commencez à utiliser AWS. Cependant, vous allez maintenant créer votre propre VPC.

Il disposera d'un bloc d'adresse CIDR (Classless Inter-Domain Routing) 10.0.0.0/16, qui inclut toutes les adresses IP commençant par 10.0.x.x. Elle contient plus de 65 000 adresses. Vous diviserez ensuite ces adresses en sous-réseaux distincts.
Choisissez Créer un VPC. 
Sur la page Créer un VPC, configurez les options suivantes :
Balise Nom - facultatif : saisissez Lab VPC.
IPv4 CIDR (CIDR IPv4) : saisissez 10.0.0.0/16.
Choisissez Créer un VPC.
Un message indiquant que le VPC a été créé avec succès s'affiche.

Sélectionnez l'onglet Balises.
Les balises sont utiles pour identifier des ressources. Par exemple, vous pouvez utiliser une balise pour identifier des centres de coûts ou différents environnements (tels que les environnements de développement, de test ou de production).

Choisissez Actions, puis Modifier les paramètres VPC.
Cette option attribue un nom DNS convivial aux instances Amazon EC2 dans le VPC, par exemple :
ec2-52-42-133-255.us-west-2.compute.amazonaws.com
Pour Paramètres DNS, sélectionnez Activer les noms d'hôte DNS.
Sélectionnez Enregistrer.
Toutes les instances EC2 lancées dans le VPC reçoivent désormais automatiquement un nom d'hôte DNS. En outre, vous pouvez ajouter ultérieurement un nom DNS plus significatif (par exemple, app.exemple.com) à l'aide d'Amazon Route 53.


<img width="1498" height="221" alt="image" src="https://github.com/user-attachments/assets/81a20098-8c5b-4fb7-a1f8-6489faa4d27e" />



<img width="1436" height="539" alt="image" src="https://github.com/user-attachments/assets/40f0262f-0824-4b75-98e8-d289e51b3f4e" />


<------------------>


<img width="1346" height="530" alt="image" src="https://github.com/user-attachments/assets/012fbe06-6bcc-4633-aff3-34bb52f5a518" />


<------------------->









