## Que sont les normes de codage ?
Considérez les normes de codage comme un ensemble de règles, de techniques et de bonnes pratiques permettant de créer un code plus propre, plus lisible, plus efficace et comportant un minimum d'erreurs. Elles offrent un format uniforme que les ingénieurs logiciels peuvent utiliser pour créer un code sophistiqué et hautement fonctionnel.

## Avantages de la mise en œuvre de normes de codage
 - Offre une uniformité au code créé par différents ingénieurs.
 - Permet la création d'un code réutilisable.
 - Facilite la détection des erreurs.
 - Rend le code plus simple, plus lisible et plus facile à maintenir.
 - Augmente l'efficacité des programmeurs et génère des résultats plus rapides.
## Glossaire :



## 1.1 Structurez votre solution par composants
Le pire piège des grandes applications est de maintenir une énorme base de code avec des centaines de dépendances - un tel monolithe ralentit les développeurs lorsqu'ils essaient d'intégrer de nouvelles fonctionnalités. Au lieu de cela, divisez votre code en composants, chacun ayant son propre dossier ou une base de code dédiée, et assurez-vous que chaque unité reste petite et simple. Consultez la rubrique "En savoir plus" ci-dessous pour voir des exemples de structure de projet correcte.

Sinon : Lorsque les développeurs qui codent de nouvelles fonctionnalités peinent à réaliser l'impact de leur changement et craignent de casser d'autres composants dépendants - les déploiements deviennent plus lents et plus risqués. Il est également considéré comme plus difficile de faire évoluer l'entreprise lorsque toutes les unités opérationnelles ne sont pas séparées.



## 1.2 Superposez vos composants, gardez la couche web dans ses limites.
Chaque composant doit contenir des "couches" - un objet dédié pour le code web, la logique et l'accès aux données. Cela permet non seulement d'établir une séparation nette des préoccupations, mais aussi de faciliter considérablement la simulation et le test du système. Bien qu'il s'agisse d'un modèle très courant, les développeurs d'API ont tendance à mélanger les couches en transmettant les objets de la couche Web (par exemple, Express req, res) à la logique métier et aux couches de données - ce qui rend votre application dépendante et accessible uniquement par des frameworks Web spécifiques.

Sinon : L'application qui mélange des objets web avec d'autres couches n'est pas accessible par le code de test, les tâches CRON, les déclencheurs des files d'attente de messages, etc.




## 1.3 Envelopper les utilitaires communs en tant que paquets npm
Dans une grande application qui constitue une grande base de code, les utilitaires transversaux comme un logger, le cryptage et autres, devraient être enveloppés par votre code et exposés comme des paquets npm privés. Cela permet de les partager entre plusieurs bases de code et projets.

Sinon : Vous devrez inventer votre déploiement et la roue des dépendances.




## 1.4 Séparer Express 'app' et 'server'.
Évitez la mauvaise habitude de définir l'ensemble de l'application Express dans un seul et unique fichier volumineux - séparez votre définition "Express" en au moins deux fichiers : la déclaration de l'API (app.js) et les préoccupations liées au réseau (WWW). Pour une structure encore meilleure, placez votre déclaration d'API dans les composants.

Autrement : Votre API sera accessible pour les tests uniquement via des appels HTTP (plus lent et beaucoup plus difficile de générer des rapports de couverture). Ce ne sera probablement pas un grand plaisir de maintenir des centaines de lignes de code dans un seul fichier.


## 1.5 Utiliser une configuration consciente de l'environnement, sécurisée et hiérarchisée
Une configuration parfaite et sans faille doit garantir que (a) les clés peuvent être lues à partir d'un fichier ET d'une variable d'environnement (b) les secrets sont conservés en dehors du code engagé (c) la configuration est hiérarchisée pour être plus facile à trouver. Il y a quelques paquets qui peuvent aider à cocher la plupart de ces cases comme rc, nconf, config, et convict.

Sinon : Si vous ne parvenez pas à satisfaire l'une ou l'autre des exigences de la configuration, l'équipe de développement ou de DevOps sera tout simplement embourbée. Probablement les deux


## 2. Bonnes pratiques ReactJS :

## 2.1 Réduire au minimum la création de composants
Vous pouvez toujours améliorer la réutilisabilité des composants en respectant la règle suivante : une fonction = un composant. Cela signifie que vous ne devez pas essayer de construire un nouveau composant pour une fonction s'il en existe déjà un pour cette fonction.

En réutilisant, non seulement vous garderez une certaine cohérence, mais vous contribuerez également à la communauté.

D'autre part, si un composant devient important ou difficile à maintenir, il est préférable de le décomposer en plusieurs composants plus petits.

Par exemple, vous pouvez même aller plus loin et créer un composant Bouton qui peut gérer les icônes. Ainsi, chaque fois que vous aurez besoin d'un bouton, vous aurez un composant à utiliser. Une plus grande modularité vous permettra de couvrir de nombreux cas avec le même morceau de code. Le mieux est de viser quelque part au milieu. Vos composants doivent être suffisamment abstraits, mais pas trop complexes.


     `const BaseButton = props => {
         const { loading, color, visible, ...rest } = props;
         if (visible === false) {
           return null;
         }
         const content = (
           <StyledButton disabled={loading} color={color || 'default'} {...rest}>
             {props.children || props.text}
             {props.loading && <CircularProgress size={14} />}
           </StyledButton>
         );
       };`
       
 ## 2.2 Utiliser un linter
 Le linting est un processus par lequel nous exécutons un programme qui analyse le code à la recherche d'erreurs potentielles.
 
 La plupart du temps, nous l'utilisons pour les problèmes liés au langage. Mais il peut également corriger automatiquement de nombreux autres problèmes, notamment le style du code. L'utilisation d'un linter dans votre code React vous aidera à garder votre code relativement exempt d'erreurs et de bogues.
 
 ## 2.3 Le code doit être testable
 Le code que vous écrivez doit être facilement et rapidement testable. Une bonne pratique consiste à nommer vos fichiers de test de la même manière que les fichiers sources, avec un suffixe '.test'. Il sera alors beaucoup plus facile de retrouver les fichiers que vous avez testés.
 
 Vous pouvez utiliser Cypress.io, et ou JEST pour tester votre code React.
 
 ## 2.4 Sécher votre code
 Une règle commune à tout le code est de le garder aussi bref que possible.
 
 Vous pouvez y parvenir en inspectant le code à la recherche de modèles. Si vous en trouvez, il est possible que vous répétiez du code et qu'il soit possible d'éliminer la duplication. Un peu de réécriture pourrait le rendre plus concis.
 
 
 Cela s'appuie sur le principe de réutilisabilité de React. Disons que vous voulez ajouter plusieurs boutons contenant des icônes. Ainsi, au lieu d'ajouter le balisage pour chaque bouton, vous pouvez simplement utiliser le composant Button que nous avons créé précédemment. Vous pouvez même aller plus loin en mappant tout dans un tableau.
 
 ## 2.5 Utiliser des gestionnaires plus robustes pour gérer l'état de l'application, comme Redux
 Redux est une bibliothèque JavaScript populaire pour gérer l'état de votre application. Elle est très courante et - si vous travaillez avec React - vous en avez probablement déjà entendu parler.
 
 Pour ceux d'entre vous qui n'ont aucune idée de ce qu'est un état d'application, il s'agit d'un objet global qui contient des informations que vous utilisez à diverses fins plus tard dans l'application (par exemple, pour prendre des décisions sur les composants à rendre et quand, pour rendre les données stockées, etc.)
 
 Les grandes applications ont de grands états d'application et leur gestion devient de plus en plus difficile au fur et à mesure que votre application se développe.
 
 C'est pourquoi nous avons besoin de bibliothèques de gestion d'état comme Redux.
 
 L'un des modèles que Redux suit est appelé "Single Source of Truth" - ce qui signifie que nous n'avons qu'un seul endroit (appelé Store) où nous stockons le seul état de l'application entière.
 
 En d'autres termes, une application - un magasin - un état.
 
 ## 2.6 Utiliser defaultProps et propTypes
 Au fur et à mesure que votre application se développe, vous pouvez attraper de nombreux bogues grâce à la vérification des types. Pour certaines applications, vous pouvez utiliser des extensions JavaScript comme Flow ou TypeScript pour vérifier le type de votre application dans son ensemble. Mais même si vous ne les utilisez pas, React possède des capacités de vérification de type intégrées. Pour effectuer un contrôle de type sur les accessoires d'un composant, vous pouvez attribuer la propriété spéciale propTypes :
 
  `import PropTypes from 'prop-types';
     
     class Greeting extends React.Component {
       render() {
         return (
           <h1>Hello, {this.props.name}</h1>
         );
       }
     }
     
     Greeting.propTypes = {
       name: PropTypes.string
     };
     Greeting.defaultProps = {
         name: 'stranger'
     };`
## 2.7 Structure des fichiers
React n'a pas de préférences sur la façon dont vous devriez mettre les fichiers dans les dossiers. Ceci étant dit, il y a quelques approches communes populaires dans l'écosystème que vous pourriez vouloir considérer.

Regroupement par fonctionnalités ou routes - une façon courante de structurer les projets est de placer les CSS, JS et les tests ensemble dans des dossiers regroupés par fonctionnalités ou routes.


      `api/
         APIUtils.js
         APIUtils.test.js
         ProfileAPI.js
         UserAPI.js
        components/
         Avatar.js
         Avatar.css
         Feed.js
         Feed.css
         FeedStory.js
         FeedStory.test.js
         Profile.js
         ProfileHeader.js
         ProfileHeader.css`
Regroupement par type de fichier - une autre façon populaire de structurer les projets consiste à regrouper les fichiers similaires, par exemple :


    `common/
       Avatar.js
       Avatar.css
       APIUtils.js
       APIUtils.test.js
     feed/
       index.js
       Feed.js
       Feed.css
       FeedStory.js
       FeedStory.test.js
       FeedAPI.js
     profile/
       index.js
       Profile.js
       ProfileHeader.js
       ProfileHeader.css
       ProfileAPI.js`
       
## 2.8 Utiliser des composants basés sur des fonctions avec état en commençant à utiliser les React Hooks
   Les hooks sont plus faciles à utiliser et à tester (en tant que fonctions séparées des composants React*). De plus, ils rendent le code plus propre et plus facile à lire - une logique connexe peut être étroitement couplée dans un hook personnalisé. Un code qui utilise des hooks est facilement lisible et comporte moins de lignes de code.
   
   Vous pouvez également définir plusieurs méthodes de cycle de vie séparées au lieu de les avoir toutes dans une seule méthode (ainsi, vous pouvez diviser la logique componentDidMount() avec facilité).
   
## 3. Bonnes pratiques de Flutter :

### lint-rules
Lorsque vous démarrez un projet à partir de zéro, ajoutez d'abord le paquet [Lint](https://pub.dev/packages/lint) qui peut vous aider à analyser statiquement votre code Flutter/dart et à améliorer la qualité de votre code, ce qui réduit évidemment les bogues et les erreurs.


### use-const

Essayez d'utiliser un mot-clé const chaque fois que possible, pour améliorer les performances de l'application. Par exemple : Lorsque vous l'utilisez pour certains widgets et que `setState` est appelé, il ne change pas le `widget` avec le mot-clé `const`.

        ```dart
        const Text(
          "Flutter Best Practices",
          style: const TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
          ),
        ),
        ```
### separate-color-class

Essayez d'avoir toutes les couleurs dans une seule classe pour votre application, faites de même avec les chaînes de caractères si vous n'utilisez pas la localisation, ainsi quand vous voulez ajouter la localisation, vous pouvez trouver toutes les chaînes de caractères à un seul endroit.

Note : Vous pourriez obtenir l'erreur de linting `avoid_classes_with_only_static_members` mais il est correct de l'ignorer pour ce type d'utilisation.

Citation de la [documentation] officielle (https://dart.dev/guides/language/effective-dart/design#avoid-defining-a-class-that-contains-only-static-members) : 
> Dans le Dart idiomatique, les classes définissent des types d'objets. Un type qui n'est jamais instancié est une odeur de code.
> Cependant, ce n'est pas une règle absolue. Avec les constantes et les types de type enum, il peut être naturel de les regrouper dans une classe.

Exemple de couleur :

        ```dart
        class AppColor {
          static const Color red = Color(0xFFFF0000);
          static const Color green = Color(0xFF4CAF50);
          static const Color errorRed = Color(0xFFFF6E6E);
        }
        ```
### define-theme

Définir le thème de l'application est une priorité absolue pour éviter le casse-tête du changement de thème dans les futures mises à jour. La mise en place du thème est certainement une tâche confuse mais unique.
Demandez à votre concepteur de partager toutes les données relatives au thème, comme les couleurs, les tailles de police et le poids.

Exemple :

    ```dart
    MaterialApp(
      title: appName,
      theme: ThemeData(
        // Define the default brightness and colors.
        brightness: Brightness.dark,
        
        // You can add the color from the seprate class here as well to maintain it well.
        primaryColor: Colors.lightBlue[800],
    
        // Define the default font family.
        fontFamily: 'Georgia',
    
        // Define the default `TextTheme`. Use this to specify the default
        // text styling for headlines, titles, bodies of text, and more.
        textTheme: const TextTheme(
          headline1: TextStyle(fontSize: 72.0, fontWeight: FontWeight.bold),
          headline6: TextStyle(fontSize: 36.0, fontStyle: FontStyle.italic),
          bodyText2: TextStyle(fontSize: 14.0, fontFamily: 'Hind'),
        ),
      ),
      home: const MyHomePage(
        title: appName,
      ),
    );
    ```
    
Vous pouvez faire beaucoup plus avec le thème, c'est-à-dire définir vos thèmes personnalisés de champ de texte, de carte, de barre de navigation inférieure pour une fois et les utiliser directement dans l'application. Consultez un exemple d'utilisation du thème [ici] (https://github.com/ibhavikmakwana/supabase_playground/blob/master/lib/values/theme.dart).

>En outre, dans une grande application/un grand projet, vous pouvez avoir plusieurs thèmes, pas seulement des thèmes pour les modes clair et foncé, mais aussi des thèmes personnalisés pour certains widgets/composants spécifiques. Vous pouvez donc toujours créer une classe/un fichier séparé et y maintenir tous les thèmes.

### éviter les widgets fonctionnels

Nous avons généralement une situation où nous devons séparer le code de l'interface utilisateur du widget, mais nous évitons de créer un widget séparé et utilisons une fonction qui renvoie le widget.
Cette pratique a quelques avantages, comme le fait de ne pas avoir à passer tous les paramètres dans votre nouveau widget, vous avez moins de code et moins de fichiers. Mais cette approche peut causer des problèmes lorsque vous voulez inspecter votre widget. Voyons cela en profondeur.

Lorsque vous utilisez un widget fonctionnel, le code ressemble à ceci.

    ```dart
    Widget functionWidget({ Widget child}) {
      return Container(child: child);
    }
    ```
Vous pouvez maintenant l'utiliser comme
    ```dart
    functionWidget(
      child: functionWidget(),
    );
    ```
Dans ce cas, l'arbre des widgets ressemblera à quelque chose comme ceci
    ```dart
    Container
      Container
    ```

Au lieu de cela, si nous utilisons Widget, notre widget ressemble à ceci
    ``` dart
    class ClassWidget extends StatelessWidget {
      final Widget child;

      const ClassWidget({Key key, this.child}) : super(key: key);
    
      @override
      Widget build(BuildContext context) {
        return Container(
          child: child,
        );
      }
    }
    ```
On peut l'utiliser comme
    ```dart
    new ClassWidget(
      child: new ClassWidget(),
    );
    ```
Et dans ce cas, l'arbre de widgets ressemble à ceci
    ```dart
    ClassWidget
      Container
        ClassWidget
          Container
    ```
Comme nous pouvons le voir ici, si nous utilisons des widgets, le framework le comprend mieux et l'interface utilisateur devient facile à inspecter.
Pour plus d'informations, suivez (https://stackoverflow.com/a/53234826/11445644) 

### avoid-print
Évitez d'utiliser `print()` dans votre code pour afficher les sorties dans la console, car si la sortie est trop importante en une seule fois, Android peut parfois ignorer certaines lignes du journal. Pour éviter cela, vous pouvez utiliser `debugPrint()`.

Vous pouvez également utiliser `log()` de `dart:developer` qui n'a pas de limite de longueur maximale comme print() ou debugPrint(), ce qui aide aussi les outils de développement de dart à montrer un enregistrement formaté.

## 4. Definition de done :


Nous continuerons à ajouter des détails et des exemples à ce sujet au fur et à mesure que nous comprenons les ambiguïtés qui se présentent.

Pour plus de clarté, une tâche ou une demande d'extraction ne sera pas considérée comme terminée tant que tous ces éléments n'auront pas été cochés.

 - La tâche a son propre issue GitHub (quelque chose qu'elle résout).
 - L'estimation du temps nécessaire à la réalisation de la tâche a été convenue avec toutes les personnes présentes et enregistrée avant de commencer la tâche.
 - Le numéro du problème est inclus dans les messages de validation pour la traçabilité.
 - Enregistrement du temps réel de la tâche dans le PR
 - Mettez à jour le fichier README.md avec les modifications/ajouts effectués.
 - Votre code suit le guide de style dwyl
 - Couverture des tests à 100%
 - Tous les tests passent