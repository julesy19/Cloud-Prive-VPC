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

# Tâche 2 : création de sous-réseaux
Un sous-réseau est une sous-plage d'adresses IP dans le VPC. Les ressources AWS peuvent être lancées dans un sous-réseau spécifié. Utilisez un sous-réseau public pour les ressources qui doivent être connectées à Internet, et un sous-réseau privé pour les ressources qui doivent rester isolées d'Internet.

Au cours de cette tâche, vous allez créer un sous-réseau public et un sous-réseau privé :


<img width="821" height="381" alt="image" src="https://github.com/user-attachments/assets/713df666-1cc7-4b8c-bf0e-dbae0f26db16" />



<----------==>

# Tâche 2.1 : création d'un sous-réseau public
Au cours de cette tâche, vous allez créer un sous-réseau public. Le sous-réseau public sera utilisé pour les ressources accessibles sur Internet.
Dans le volet de navigation de gauche, choisissez Sous-réseaux.
Choisissez Créer un sous-réseau.
Sur la page Créer un sous-réseau, configurez les options suivantes :
ID de VPC : choisissez Lab VPC (VPC de l'atelier).
Nom du sous-réseau : saisissez Public Subnet.
Zone de disponibilité : choisissez la première zone de disponibilité de la liste. Ne conservez pas Aucune préférence par défaut.
IPv4 subnet CIDR block (Bloc d'adresse CIDR de sous-réseau IPv4) : saisissez 10.0.0.0/24.
Choisissez Créer un sous-réseau.
Le VPC dispose d'un bloc d'adresse CIDR 10.0.0.0/16, qui inclut toutes les adresses IP 10.0.x.x. Le sous-réseau que vous venez de créer dispose d'un bloc d'adresse CIDR 10.0.0.0/24, qui inclut toutes les adresses IP 10.0.0.x. Ils peuvent se ressembler, mais le sous-réseau est plus petit que le VPC en raison du /24 dans la plage CIDR.
À présent, vous allez configurer le sous-réseau pour qu'il attribue automatiquement une adresse IP publique à toutes les instances lancées dans celui-ci.

Sélectionnez Sous-réseau public.
Choisissez Actions, puis Modifier les paramètres de sous-réseau.
Sur la page Modifier les paramètres de sous-réseau, pour Paramètres d'attribution automatique d'une adresse IP, sélectionnez Enable auto-assign public IPv4 address (Activer l'attribution automatique d'une adresse IPv4 publique).
Sélectionnez Enregistrer.
Ce sous-réseau a été nommé Sous-réseau public, mais il n'est pas encore public. Un sous-réseau public doit avoir une passerelle Internet, que vous allez attacher dans la tâche suivante.


<img width="1161" height="778" alt="image" src="https://github.com/user-attachments/assets/79b89259-5f44-4dab-a174-c2e8b95a1a61" />


<------------------->


<img width="1512" height="247" alt="image" src="https://github.com/user-attachments/assets/223a6c91-a0f3-4734-9121-adb1d71b49af" />


<------------------>


<img width="1134" height="540" alt="image" src="https://github.com/user-attachments/assets/0eb4c8a0-783c-4099-807b-1727e74cb37f" />


<------------------>


# Tâche 2.2 : création d'un sous-réseau privé
Au cours de cette tâche, vous allez créer un sous-réseau privé. Le sous-réseau privé est utilisé pour les ressources qui doivent rester isolées d'Internet.
Choisissez Créer un sous-réseau.
Sur la page Créer un sous-réseau, configurez les options suivantes :
ID de VPC : choisissez Lab VPC (VPC de l'atelier).    
Nom du sous-réseau : saisissez Private Subnet.
Zone de disponibilité : choisissez la première zone de disponibilité de la liste. Ne conservez pas Aucune préférence par défaut.
IPv4 subnet CIDR block (Bloc d'adresse CIDR de sous-réseau IPv4) : saisissez 10.0.2.0/23.
Le bloc d'adresse CIDR 10.0.2.0/23 inclut toutes les adresses IP qui commencent par 10.0.2.x et 10.0.3.x. Ce sous-réseau est plus grand que le sous-réseau public, car la plupart des ressources doivent rester privées, à moins qu'elles ne soient spécifiquement accessibles à partir d'Internet.
Choisissez Créer un sous-réseau.
Votre VPC possède désormais deux sous-réseaux. Toutefois, le sous-réseau public est totalement isolé et ne peut pas communiquer avec des ressources en dehors du VPC. Vous allez configurer le sous-réseau public pour qu'il se connecte à Internet par le biais d'une passerelle Internet.


<-------------------->


<img width="1127" height="777" alt="image" src="https://github.com/user-attachments/assets/82e61ad9-bc51-4a24-9871-fee5ad5c8b96" />


<---------------------->



<img width="1526" height="211" alt="image" src="https://github.com/user-attachments/assets/8fb9f164-aeb8-44bc-9868-0c3508900f86" />



 <--------------------->


# Tâche 3 : création d'une passerelle Internet
Une passerelle Internet est un composant de VPC mis à l'échelle horizontalement, redondant et hautement disponible. Elle permet la communication entre les instances figurant dans un VPC et Internet. Elle n'impose pas de risque de disponibilité ou de contraintes de bande passante au trafic réseau.
Une passerelle Internet a deux fonctions :
fournir une cible dans les tables de routage qui se connecte à Internet ;
effectuer la traduction d'adresses réseau (NAT) pour les instances auxquelles des adresses IPv4 publiques ont été attribuées
Au cours de cette tâche, vous allez créer une passerelle Internet afin que le trafic Internet puisse accéder au sous-réseau public.
Dans le volet de navigation de gauche, sélectionnez Passerelles Internet.
Choisissez Créer une passerelle Internet.
Pour Balise de nom, saisissez Lab IGW.
Choisissez Créer une passerelle Internet.
Vous pouvez désormais attacher la passerelle Internet au VPC de l'atelier.
Sélectionnez Actions, puis Attacher au VPC.
Pour VPC disponibles, sélectionnez Lab VPC (VPC de l'atelier).
Sélectionnez Attacher une passerelle Internet.
Cette action permet d'attacher la passerelle Internet au VPC de l'atelier. Bien que vous ayez créé une passerelle Internet et que vous l'ayez attachée à votre VPC, vous devez encore configurer la table de routage du sous-réseau public pour qu'il utilise la passerelle Internet.


<img width="1014" height="379" alt="image" src="https://github.com/user-attachments/assets/7f49f568-e40a-45bf-82d3-5bd9b5debbb4" />


<--------------->


<img width="1171" height="332" alt="image" src="https://github.com/user-attachments/assets/fba4ccaa-3742-4491-b672-d5c69ce58497" />


<------------->


<img width="1041" height="255" alt="image" src="https://github.com/user-attachments/assets/c3af51e5-2da8-4b1b-8bcd-ba36ae4b8fc1" />


<----------------->


<img width="1141" height="350" alt="image" src="https://github.com/user-attachments/assets/e45fff34-76e2-4bac-be75-164badfdf0b7" />


<------------------>



# Tâche 4 : configuration des tables de routage
Une table de routage contient un ensemble de règles, appelées routes, qui permettent de déterminer la direction du trafic réseau. Chaque sous-réseau d'un VPC doit être associé à une table de routage, car c'est elle qui contrôle le routage du sous-réseau. Un sous-réseau peut être associé à une seule table de routage à la fois, mais vous pouvez associer plusieurs sous-réseaux à une même table de routage.

Pour utiliser une passerelle Internet, la table de routage d'un sous-réseau doit contenir une route qui dirige le trafic Internet vers la passerelle Internet. Si un sous-réseau est associé à une table de routage comportant une route vers une passerelle Internet, il s'agit d'un sous-réseau public.
Au cours de cette tâche, vous allez effectuer les actions suivantes :
créer une table de routage publique pour le trafic Internet ;
ajouter une route à la table de routage pour diriger le trafic Internet vers la passerelle Internet ;
associer le sous-réseau public à la nouvelle table de routage.
Dans le volet de navigation de gauche, sélectionnez Tables de routage.
Plusieurs tables de routage s'affichent, mais seule l'une d'elles est associée au VPC de l'atelier. Cette table de routage achemine le trafic localement, c'est pourquoi on l'appelle table de routage privée.
Développez la colonne VPC afin de voir laquelle est utilisée par le VPC de l'atelier.
Sélectionnez la table de routage qui affiche Lab VPC (VPC de l'atelier).
Dans la colonne Nom, cliquez sur l'icône de modification (), et pour Edit Name (Modifier le nom), saisissez Private Route Table.
Sélectionnez Enregistrer.
Cliquez sur l'onglet Routes.
Il n'y a qu'une seule route. Il montre que tout le trafic destiné à 10.0.0.0/16 (qui est la plage du VPC de l'atelier) sera acheminé localement. Cette route permet à tous les sous-réseaux d'un VPC de communiquer entre eux.

Vous allez maintenant créer une table de routage publique pour envoyer le trafic public vers la passerelle Internet.
Sélectionnez Créer une table de routage et configurez les paramètres suivants :
Name - optional (Nom – facultatif) : saisissez Public Route Table.
VPC : choisissez Lab VPC (VPC de l'atelier).
Choisissez Créer une table de routage.
Dans l'onglet Routes, sélectionnez Modifier des routes.
À présent, vous allez ajouter une route pour diriger le trafic Internet (0.0.0.0/0) vers la passerelle Internet.
Sélectionnez Ajouter une route, puis configurez les paramètres suivants :
Destination : saisissez 0.0.0.0/0.
Cible : choisissez Passerelle Internet, puis Lab IGW dans la liste.
Choisissez Enregistrer les modifications.
Ensuite, vous allez associer cette nouvelle table de routage au sous-réseau public.
Sélectionnez l'onglet Associations de sous-réseau.
Sélectionnez Modifier les associations de sous-réseau.
Sélectionnez la ligne contenant Sous-réseau public.
Choisissez Enregistrer les associations.
Le sous-réseau public est désormais public, car il possède une entrée de table de routage qui envoie le trafic vers Internet par le biais de la passerelle Internet.
Pour résumer, vous pouvez créer un sous-réseau public en effectuant les étapes suivantes :
créer une passerelle Internet ;
créer une table de routage ;
ajouter une route à la table de routage qui dirige le trafic 0.0.0.0/0 vers la passerelle Internet ;
associer la table de routage à un sous-réseau, qui devient alors un sous-réseau public.



 <img width="1157" height="437" alt="image" src="https://github.com/user-attachments/assets/4012e6ae-95f7-49eb-9071-7fe9ba1f9d6b" />


 <----------------------->


 <img width="1187" height="387" alt="image" src="https://github.com/user-attachments/assets/fbdfb6a1-5fd3-4c0b-bec1-7cc5c40da85b" />



<----------------->


<img width="1136" height="425" alt="image" src="https://github.com/user-attachments/assets/5991bdf8-ee75-42a9-8d9c-95fa686d791a" />



<----------------->




<img width="1439" height="303" alt="image" src="https://github.com/user-attachments/assets/3addc2ee-b5c1-4d55-9aa9-8963adc8b6c9" />



<----------------->



<img width="1219" height="500" alt="image" src="https://github.com/user-attachments/assets/4e4417b0-875c-4305-9364-879eb2740b44" />



<---------------->



<img width="1334" height="318" alt="image" src="https://github.com/user-attachments/assets/25507312-5123-4972-bcd0-33385f5532ce" />



<--------------->


Associations des sous-reseaux 


<img width="1344" height="358" alt="image" src="https://github.com/user-attachments/assets/0cd8cc78-68e2-4259-865e-af733117aca0" />



<---------------->



<img width="1128" height="399" alt="image" src="https://github.com/user-attachments/assets/41c1adc1-b57c-47fc-a272-0f7a47bb72c9" />



<----------------->



Le sous-réseau public est désormais public, car il possède une entrée de table de routage qui envoie le trafic vers Internet par le biais de la passerelle Internet.
Pour résumer, vous pouvez créer un sous-réseau public en effectuant les étapes suivantes :
créer une passerelle Internet ;
créer une table de routage ;
ajouter une route à la table de routage qui dirige le trafic 0.0.0.0/0 vers la passerelle Internet ;
associer la table de routage à un sous-réseau, qui devient alors un sous-réseau public.



<------------------->


# Tâche 5 : création d'un groupe de sécurité pour le serveur d'application
Un groupe de sécurité fait office de pare-feu virtuel pour les instances afin de contrôler le trafic entrant et sortant. Les groupes de sécurité fonctionnent au niveau de l'interface Réseau Élastique de l'instance. Les groupes de sécurité ne fonctionnent pas au niveau du sous-réseau. Par conséquent, chaque instance peut avoir son propre pare-feu qui contrôle le trafic. Si vous ne spécifiez pas de groupe de sécurité en particulier lors du lancement, l'instance est automatiquement affectée au groupe de sécurité par défaut du VPC.
Au cours de cette tâche, vous allez créer un groupe de sécurité qui permet aux utilisateurs d'accéder à votre serveur d'application via HTTP.
Dans le volet de navigation de gauche, sélectionnez Groupes de sécurité.
Sélectionnez Créer un groupe de sécurité.
Sur la page Créer un groupe de sécurité, configurez les options suivantes :
Nom du groupe de sécurité : saisissez App-SG.
Description : saisissez Allow HTTP traffic.
VPC : choisissez Lab VPC (VPC de l'atelier).
Dans la section Règles entrantes, choisissez Ajouter une règle et configurez les options suivantes :
Type : choisissez HTTP.
Source : choisissez Anywhere-IPv4.
Pour Description - facultative : saisissez Allow web access.
Le paramétrage de règles entrantes détermine le trafic autorisé à atteindre l'instance. Vous allez les configurer pour autoriser le trafic HTTP (port 80) en provenance de n'importe où sur Internet (0.0.0.0/0).
Sélectionnez Créer un groupe de sécurité.
Vous utiliserez le groupe de sécurité App-SG dans la prochaine tâche.



<img width="1158" height="773" alt="image" src="https://github.com/user-attachments/assets/38c271f3-ba6c-4d84-8d33-cbd26076cb68" />




<--------------->




<img width="1310" height="428" alt="image" src="https://github.com/user-attachments/assets/cf876119-71e5-4b25-b9c0-ff9d63aee73f" />



<------------------->















