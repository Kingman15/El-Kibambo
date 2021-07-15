# El-Kibambo

El Kibambo est une bibliothèque .NET qui va vous permettre de faire des recherches multi-colonnes sur des grilles de données.
En plus, la recherche n'est pas limitée à des tests d'égalité, plusieurs tests de comparaison sont possible.

Cette recherche se fait QUE sur les données affichées dans la grille.
El Kibambo considère que l'on veut recherché sur une colonne que si et seulement si l'on spécifie à la fois la valeur recherchée ET l'opérateur de comparaison.

Après ajout de la bibliothèque comme référence, il suffit d'instancier une variable de type Kibambo en passant au constructeur :

    - La grille contenant les données 
    - La grille de recherche 
    - Un tableau des objets de type KibamboColumn. Le constructeur de la classe KibamboColumn prend comme arguments :

        - Le nom interne de la colonne (si les données proviennent d'un DataSet dont les données sont issus d'une table de la base de données, dans ce cas ce nom correspond au nom de la colonne SQL ou aux alias éventuels) ;
        - Le nom de colonne qui sera affichée dans la grille de recherche ;
        - Le type de la colonne. Une valeur de l'énumération KibamboColumnType (String, Numeric). Très important : si vous spécifiez KibamboColumnType.String sur une colonne contenant des données numériques, dans ce cas les comparaisons sur cette colonne se feront par ordre alphabetique ;
        - Le nom de type qui sera affiché dans la grille de recherche.

    - La fonction de rappel qui sera appelé à chaque fois qu'une ligne n'a pas satisfait la condition. Elle doit être de la forme :
```
        void NomFonction(DataGridViewRow row)
        {
            // .....
        }
```
Un exemple d'instanciation :

    var kibambo = new Kibambo(
        dgvData,
        dgvSearch,
        new KibamboColumn[] { 
            new KibamboColumn("firstName", "Prénom", KibamboColumnType.String, "Texte"),
            new KibamboColumn("lastName", "Nom", KibamboColumnType.String, "Texte"),
            new KibamboColumn("age", "Age", KibamboColumnType.Numeric, "Nombre")
        },
        delegate(DataGridViewRow row)
        {
            row.Visible = false;
        });

La classe Kibambo possède deux méthodes :

    * Search() : pour effectuer une recherche de tri sur les données. Cette recherche est recursive, une prochaine recherche se fera exclusivement QUE sur les lignes affichées.

La classe Kibambo possède comme propriétés :

    * RowsUnsatisfied : une collection des lignes de la grille n'ayant pas satisfait à la recherche

Cette version est une version beta (de test). Les prochaines versions en cours d'écriture apporteront des améliorations très significatives. Citons :

    * La prise en charge d'une recherche intervaleur comme la clause BETWEEN de SQL ;
    * Une recherche par jeton comme la clause LIKE de SQL ;
    * Une recherche FULLTEXT comme celui disponible dans MySQL ;
    * Une recherche par motif grâce aux expressions régulières ;
    * Etc.

Cette bibliothèque a été mise au point par Michael Kyungu Ilunga, développeur C#.NET (web => ASP.NET, desktop => ..., mobile => Xamarin). Pour tout contact (remarques, suggestions, etc), vous pouvez passez par mes pages Facebook :

    * El Concept : page Facebook de ma start-up en cours de téléchargement (à préférer, d'ailleurs les éventuelles mise à jour de la bibliothèque seront annoncées ici) fb.me/elconcept15 ;
    * El Programming : page Facebook où je partage astuces et techniques de programmation https://web.facebook.com/elprogramming
    * Kingman Prod : ma page Facebook de divertissement.

Ou directement par mon numéro de contact : +243 97 37 19 693, ou par mon adresse e-mail : michaelkyunguilunga15@gmail.com

=> Cette documentation est accompagnée de deux tutoriels : 
- une version où les données proviennent de la base de données https://youtu.be/o1xzMwGrtUw
- et l'autre où les données sont écrits en dur dans le code https://youtu.be/7QnTq45FQGA
=> Les codes présentés peuvent être traduits aisement dans un autre langage de programmation .NET comme VB.NET.

© El Concept - Tous droit réservés

-------------------------------------------------------------------------
-------------------------------------------------------------------------
