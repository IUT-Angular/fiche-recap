# Fiche d'aide à la révision

## Concepts importants

### Projet

1. Création d'un projet en ligne de commande : `ng new <project-name>`

### Composants

1. Création d'un composant en ligne de commande : `ng generate component --skip-tests=true --inline-style <component-name>`
2. Affichage conditionnel ngIf / @if
3. Affichage itératif ngFor / @for
4. Mise en forme via des pipe. Exemple : `{{ property | date:'EEEE dd MMMM yyyy' }}`

### Form

1. https://angular.dev/guide/forms

### Services

1. Les services sont rangés dans le dossier `services`
2. Le décorateur `@Injectable()` permettra d'injecter le service dans les différents composants
3. Injection de dépendance directement dans le constructeur d'un composant

### Routing

1. https://angular.dev/guide/routing/common-router-tasks
2. Les routes sont déclarées au sein du fichier `app.routes.ts`
3. Gestion des paramètres via `:param` et que l'on récupère dans le composant via `this.activatedRoute.snapshot.params['param']`
4. Prévoir une page `NotFound`

### Modèle

1. Déclarer vos modèles/dtos en tant qu'interface via `export interface NomDto`
2. Pour déclarer un propriété : `title: string`
3. Pour déclarer un propriété acceptant la valeur null : `description: string | null`

### Injecter une donnée dans un composant enfant

1. Lien sur la doc : https://angular.dev/guide/components/inputs
2. Dans un composant <enfant> , si on souhaite injecter depuis le composant appelant/parent des données, la propriétés devra être déclarée avec le décorateur `@input`
```
public class enfant {
    @Input() name: string;
}
```

```
<enfant [name]="toto">
```

### Déclencher un événement depuis un composant enfant

1. Lien sur la doc : https://angular.dev/guide/components/output-fn
2. Dans un composant <enfant> , nous allons déclarer une propriété de type `output<T>` (ici T correspond au type de données qui sera transmis via l'événement)
```
public class enfant {
    eventName = output<string>()    // Ancienne méthode @Output() eventName;

    launchEvent(value: string) {
        this.eventName.emit(value);
    }
}
```

```
<enfant (eventName)="callback($event)">
```

La méthode `callback` est présente dans le composant parent.

## Requête HTTP

1. Afin de faire des requêtes HTTP, il est nécessaire d'injecter un client HTTP, de tpye `HttpClient` dans le composant/service où l'on souhaite l'utiliser
2. Pour interroger une API, nous allons utiliser les méthodes suivantes : 
 - HttpClient.get<T>(url) => permet de récupérer des éléments de type T
 - HttpClient.post<T>(url, element) => permet d'ajouter un élément de type T
 - HttpClient.put<T>(url, element) => permet de modifier un élément de type T
 - HttpClient.delete<T>(url) => permet de supprimmer un élément de type T

## Tutoriel

Un des tutoriels les mieux aboutis est le tutoriel officiel (longtemps batisé Tour of Heroes). Il vous permettra de réaliser une application Angular pas à pas directement dans le navigateur.

Lien : https://angular.dev/tutorials/learn-angular

## Bonnes pratiques

1. Toujours préciser le type de retour d'une méthode
2. Ne jamais utiliser le type `any`
3. Favoriser les interfaces pour les modèles/dto
4. Respecter l'arborescence de fichiers
5. Ne jamais commit ou distribuer le dossier `node_modules`, il faut l'ignorer via le `.gitignore`
