# Cloud_Shoes 
Proposition de migration de commerce électronique vers Azure

![Logo_CloudShoes](https://user-images.githubusercontent.com/43493818/230494747-7a831060-0c33-4426-9479-42d126ed2b9f.png)

## Présentation de l'entreprise
Cloud Shoes est une entreprise du secteur de la chaussure, fondée en 2015.
L'entreprise a connu un processus d'expansion au cours duquel elle a considérablement augmenté son nombre de clients et ses ventes.
Au cours des dernières années, Cloud Shoes a simplifié sa structure en fermant son magasin physique pour se concentrer uniquement sur le commerce électronique.
En raison de ce changement structurel de l'entreprise, il est essentiel de rechercher des avancées technologiques fréquentes afin d'améliorer l'expérience finale du client et de transformer cela en rentabilité et en croissance pour l'entreprise.
Cloud Shoes ne commercialise que des chaussures et a pour objectif de se développer dans la vente de vêtements à l'avenir. Aujourd'hui, l'entreprise opère uniquement au Brésil et n'a pas de plans immédiats pour s'étendre à l'étranger.
L'entreprise dispose de la structure suivante :
- 500 employés
- 50 fournisseurs (sous-traitants)
- Siège social à São Paulo
- Bureau administratif à Belo Horizonte
- Infrastructure informatique (centre de données) à São Paulo.

## Infrastructure informatique
Cloud Shoes dispose actuellement de l'infrastructure informatique suivante :
- Son propre centre de données au siège de l'entreprise à São Paulo ;
- Plus de 10 applications en cours d'exécution pour prendre en charge l'activité de l'entreprise ;
- Environ 120 serveurs de production actifs ;
- Environ 40 serveurs de développement et de test actifs ;
- Toute l'infrastructure des serveurs est exécutée sur une virtualisation avec VMware fonctionnant sur 10 serveurs physiques ;
- L'entreprise utilise les systèmes d'exploitation Windows Server et Linux (Ubuntu Server et RedHat) ;
- La base de données est SQL Server 2016 Enterprise ;
- L'entreprise dispose de 2 Storages avec des disques SSD ;
- La politique de renouvellement des serveurs physiques est de 5 ans.
- Le dernier renouvellement a été effectué en 2020.

## Structure de commerce électronique
Aujourd'hui, la principale charge de travail de Cloud Shoes est son site de commerce électronique. C'est l'application la plus critique, où tout le processus de vente de Cloud Shoes a lieu.
La structure du site se compose des services suivants :
- 4 serveurs Windows Server 2019 - Frontend - exécutant IIS
- 4 serveurs Windows Server 2019 - Backend
- 2 serveurs Windows Server 2016 - SQL Server avec Cluster Failover
- 1 serveur Windows Server 2012 - Service d'intégration avec ERP
- Stockage pour le catalogue d'images du site d'une capacité de 2 To - 70 % utilisé
- Stockage utilisé pour le stockage des bases de données de SQL Server - 60 % utilisé
- 1 pare-feu de bordure effectuant la répartition de charge vers les serveurs frontend
- 1 équilibreur de charge interne partagé pour toutes les applications.

![EstruturaOnPremises](https://user-images.githubusercontent.com/43493818/230494533-f805b643-7ae0-4e79-969a-48dd6df73e2a.png)

## Statistiques de l'E-Commerce
Aujourd'hui, Cloud Shoes présente le tableau suivant avec des moyennes d'accès pour les principales périodes de vente du commerce au Brésil :

![Estatisticas](https://user-images.githubusercontent.com/43493818/230494623-0f713e81-6f11-43d4-bd5d-1341724a21b3.png)

## Problèmes rencontrés
Aujourd'hui, Cloud Shoes rencontre quelques problèmes liés à la structure et à la performance de sa charge de travail principale, ce qui entraîne parfois une perte de ventes et même une préférence des utilisateurs pour d'autres magasins concurrents.
Principaux problèmes rencontrés :
- On constate des périodes de grande lenteur dans l'accès des clients, notamment pour ouvrir les images des produits ;
- Certains jours, on constate une pénurie de ressources sur certains serveurs aux heures de pointe, alors qu'ils consomment moins de 10% en moyenne pendant la nuit ;
- Difficulté à analyser (surveiller) quels sont les produits les plus consultés sur le site et le temps de réponse sur les pages les plus consultées ;
- Problèmes de conformité liés à l'équipement de pare-feu qui publie l'application en externe, car il ne dispose pas de la fonctionnalité WAF ;
- Besoin d'un effort important de l'équipe pour provisionner de nouveaux serveurs pendant les périodes de forte affluence/ventes. Par la suite, toutes les ressources relatives aux serveurs provisionnés doivent être supprimées manuellement pour libérer du matériel.
- Le serveur d'intégration exécute une application héritée qui exécute des services de traitement asynchrone intégrant les données d'achat et les NFEs avec l'ERP. Cette application a des dépendances de services Windows et de certaines COM+. Ce serveur n'a pas de répartition de charge en raison de la surcharge de l'unique équilibreur de charge interne. Cloud Shoes attend l'achat d'un nouvel équilibreur de charge interne pour ajouter un nouveau serveur à ce service ;
- Coût élevé de stockage pour les images du catalogue anciennes ou non utilisées. Le stockage actuel ne dispose pas d'un modèle de disque moins cher pour « hiérarchiser » ces images inutilisées ;
- La sauvegarde de toutes les données de l'application et de la base de données est effectuée sur un stockage et conservée pendant 15 jours pour une restauration rapide. Passé cette période, elles sont envoyées sur des bandes de sauvegarde, collectées et emmenées dans un coffre-fort en dehors de la structure, rendant la restauration de données de plus de 15 jours difficile.

## Besoins
La société Cloud Shoes a aujourd'hui pour objectif stratégique de migrer 70 % de ses applications vers le cloud au cours des deux prochaines années. Le fournisseur choisi est Azure, en raison de son environnement étant 90 % Microsoft et de la plus grande familiarité technique de l'équipe d'infrastructure, de bases de données et d'applications. La migration vers le cloud vise à résoudre certains des problèmes actuellement rencontrés dans l'environnement local :

- Réduire les coûts liés au renouvellement des serveurs et à la garantie des équipements ;
- Fournir une plus grande capacité de mise à l'échelle aux dates de demande maximale du commerce ;
- Optimiser l'utilisation des ressources aux heures creuses ;
- Utiliser de nouvelles technologies pour améliorer les performances de l'expérience d'accès, de navigation et d'achat pour l'utilisateur final ;
- Réduire les efforts administratifs de l'équipe d'infrastructure serveurs ;
- Accroître la sécurité en ce qui concerne l'exposition de l'e-commerce ;
- Réduire le temps de restauration des données de plus de 15 jours ;
- Permettre à l'avenir aux clients de s'authentifier selon le format B2C en utilisant Google, Microsoft et d'autres fournisseurs ;
- Surveiller davantage les accès, les produits principaux et les temps de réponse ;
- Réduire le coût de stockage des images de catalogue anciennes (non utilisées pour le moment).

## En ce qui concerne la migration vers le Cloud
- Aujourd'hui, Cloud Shoes n'a aucune structure de production dans Azure. Il possède un abonnement PAYG dans Azure
essentiellement non consommé. Cloud Shoes possède déjà une réplication des utilisateurs de l'AD local avec Azure AD en raison
de l'utilisation de services de Microsoft 365 tels que Exchange Online, OneDrive et Teams.
- Il n'y a aucune connexion physique entre l'environnement local et Azure.
- Tous les serveurs Windows de Cloud Shoes font partie du domaine cloudshoes.local, où il existe 2
serveurs Active Directory avec des zones DNS intégrées.
- Toute l'authentification des clients externes pour effectuer des achats est effectuée directement dans une structure de
base de données SQL Server.
- Toute la structure de commerce électronique n'a pas de dépendance à d'autres workloads (sauf la structure d'AD et de DNS).
Seul le serveur d'intégration doit communiquer avec la structure de l'ERP pour transporter des données
liées aux ventes et aux NFE.
- À cette étape du projet, la migration n'est estimée que pour le workload E-Commerce.

## Sur la proposition
Cloud Shoes souhaite recevoir une proposition de la part de partenaires pour migrer son E-Commerce vers Azure. Cette première étape de la proposition devrait contenir les éléments suivants:
- Conception d'architecture pour la solution sur Azure;
- Brève description des principaux services utilisés dans la solution et aborder les principaux avantages pour le choix de cette solution;
- Tarification de la solution (élaboration de deux scénarios : 1° uniquement avec paiement mensuel. 2° utiliser une instance réservée de 3 ans pour les services possibles);
- Calendrier pour la migration de la charge de travail et les configurations nécessaires dans l'environnement Azure/Cloud Shoes;
- Prix de l'investissement pour la réalisation du projet (conseil).
