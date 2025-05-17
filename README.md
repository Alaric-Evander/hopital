# hopital
Rapport sur les technologies de persistance et de service dans un système Java
Ce rapport se concentre sur l'architecture logicielle et les technologies employées pour la gestion des données et la logique métier dans un système développé en Java, en se basant sur un ensemble de composants typiques d'une application moderne.

Java Persistence API (JPA) pour la gestion des données
Au cœur de la persistance des données se trouve JPA (Java Persistence API), une spécification standard de Java pour le mapping objet-relationnel (ORM). L'ORM est une technique de programmation qui permet de convertir des données entre le système de types utilisé dans un langage de programmation orienté objet et les tables d'une base de données relationnelle. JPA simplifie considérablement l'interaction avec la base de données en permettant aux développeurs de manipuler des objets Java classiques (POJOs), appelés entités, au lieu d'écrire directement des requêtes SQL complexes.

Les entités sont des classes Java annotées avec @Entity, indiquant qu'elles représentent des tables dans la base de données. Chaque instance d'une entité correspond à une ligne dans sa table respective. Les attributs de ces classes sont mappés à des colonnes de table, et JPA fournit des annotations pour gérer divers aspects de ce mapping :

@Id et @GeneratedValue pour définir et gérer les clés primaires, souvent avec des stratégies de génération automatique.
Des annotations pour les relations entre entités, telles que @OneToOne, @ManyToOne, et @OneToMany, permettent de modéliser les liens entre les différentes tables (par exemple, un patient peut avoir plusieurs rendez-vous). Ces relations peuvent être configurées pour un chargement différé (WorkspaceType.LAZY), optimisant ainsi les performances en ne chargeant les données associées que lorsque c'est nécessaire.
@Temporal pour spécifier comment les types date/heure Java doivent être persistés en base de données.
@Enumerated pour mapper des types énumérés Java à des représentations en base de données (chaîne de caractères ou ordinal).
Pour interagir avec ces entités, JPA définit l'interface EntityManager, qui fournit des opérations pour créer, lire, mettre à jour et supprimer (CRUD) des entités.

Spring Data JPA pour simplifier l'accès aux données
Pour faciliter davantage l'utilisation de JPA, le framework Spring Data JPA est couramment employé. Il s'appuie sur le concept de "Repositories". Les repositories sont des interfaces qui étendent JpaRepository (ou des interfaces parentes). En déclarant simplement ces interfaces, Spring Data JPA génère automatiquement les implémentations pour les opérations CRUD standard et permet de définir des méthodes de requête personnalisées en suivant des conventions de nommage (par exemple, findByNom(String nom) chercherait une entité par son attribut nom). Cela réduit considérablement le code répétitif lié à l'accès aux données.

Injection de dépendances et services avec Spring Framework
L'architecture observée utilise également le framework Spring, notamment pour l'injection de dépendances et la gestion des services.

Injection de Dépendances : Les composants, comme les services ou les repositories, ne créent pas leurs propres dépendances. Au lieu de cela, ces dépendances leur sont "injectées" par le conteneur Spring. Cela se manifeste souvent par des constructeurs qui acceptent des interfaces de repositories comme paramètres. Ce design favorise un couplage faible et une meilleure testabilité.
Services : La logique métier est encapsulée dans des classes de service, typiquement annotées avec @Service. Ces services coordonnent l'utilisation des repositories pour effectuer des opérations plus complexes.
Gestion des Transactions : L'annotation @Transactional est utilisée au niveau des classes de service ou de leurs méthodes. Elle indique à Spring de gérer les transactions de base de données. Cela garantit que les opérations sur la base de données sont atomiques : soit toutes les modifications d'une transaction sont appliquées, soit aucune ne l'est en cas d'erreur, maintenant ainsi la cohérence des données.
Autres considérations techniques
Lombok: Pour réduire la verbosité du code Java, des bibliothèques comme Lombok sont souvent utilisées. Des annotations comme @Data, @NoArgsConstructor, et @AllArgsConstructor génèrent automatiquement les getters, setters, constructeurs, méthodes toString(), equals(), et hashCode(), rendant le code des entités et autres objets de données plus concis.
JSON Handling: Des annotations comme @JsonProperty peuvent être utilisées pour contrôler la sérialisation et la désérialisation des objets Java en JSON, par exemple pour ignorer certains champs lors de la conversion (souvent pour éviter des références circulaires ou des données inutiles dans les API REST).
Captures d'écran :
![image](https://github.com/user-attachments/assets/8463edaf-a88c-4a7c-af58-370aed448dd9)
![image](https://github.com/user-attachments/assets/b0ca6e32-b5ad-413b-8a07-c91156076c75)
![image](https://github.com/user-attachments/assets/a12fc7f3-cfef-45ef-bee6-33b0166cab9e)
![image](https://github.com/user-attachments/assets/f86e2961-4e4f-41ee-bf0b-e0a18e059e5c)
![image](https://github.com/user-attachments/assets/7a03bb46-bec9-45e5-bc64-aad6c14a4a3f)





