# CopyKit

Application macOS native, 100 % Apple : Xcode 27.1, Swift 6.4 (mode de langage
Swift 6), SwiftUI, SwiftData, Swift Testing, XCUITest. Cible macOS 27.0.

## Règles

- **Zéro dépendance tierce** : aucun package Swift externe, aucun outil tiers
  dans le build ou les tests. Demander avant toute exception.
- **Architecture** : MV à la manière d'Apple, rangé par feature, cœur métier
  isolé dans des packages Swift locaux. Voir
  [ADR 0001](docs/adr/0001-architecture-mv-feature-core.md) et
  [l'arborescence et le nommage](docs/plugins/06-arborescence-et-nommage.md).
- **Nommage** : un type par fichier, le fichier porte le nom du type, le rôle
  est donné par un suffixe (`…View`, `…Row`, `…ViewModel`, `…Record`,
  `…Policy`, `…Service`, `…Error`…). Préfixes `System…` / `Fake…` seulement
  pour l'implémentation réelle / de test d'un protocole.
- **Pas de dossier ni de package vide** : on les crée avec leur premier fichier.
- **Skills de référence** : les skills Apple `xcode-integration:*` font foi
  (SwiftUI, Swift Testing, App Intents, accessibilité, traduction). En cas de
  désaccord entre deux sources, Apple a raison.
- **Réglages du projet** : passer par les outils MCP Xcode
  (`UpdateTargetBuildSetting`, `AddEntitlement`, `AddInfoPlist`…), ne pas
  éditer `project.pbxproj` à la main. Seule exception : référencer un dossier
  ou un fichier racine (règle suivante), qu'aucun outil MCP ne sait faire.
- **Tout doit être visible dans Xcode** :
  - `CopyKit/`, `CopyKitTests/`, `CopyKitUITests/` et `docs/` sont des
    dossiers synchronisés : tout ce qui est créé dedans apparaît tout seul ;
  - un **nouveau dossier à la racine** du dépôt est déclaré, dès sa création,
    comme dossier synchronisé (`PBXFileSystemSynchronizedRootGroup`) **sans
    cible** dans le groupe principal ;
  - un **nouveau fichier à la racine** est ajouté comme simple référence
    (`PBXFileReference`) sans cible ;
  - un package local dans `Packages/` apparaît quand on le relie au projet ;
  - après chaque modification, vérifier avec `plutil -lint` et un build.

## Commandes

Les builds et les tests passent par Portly (`portly temp` puis `portly wait`).

```bash
# Build
xcodebuild -project CopyKit.xcodeproj -scheme CopyKit -destination 'platform=macOS' build

# Tests unitaires (Swift Testing)
xcodebuild -project CopyKit.xcodeproj -scheme CopyKit -destination 'platform=macOS' test -only-testing:CopyKitTests

# Tous les tests, y compris l'interface (XCUITest)
xcodebuild -project CopyKit.xcodeproj -scheme CopyKit -destination 'platform=macOS' test
```

Quand Xcode est ouvert, les outils MCP Xcode (`BuildProject`, `RunAllTests`,
`RunSomeTests`, `RenderPreview`, `GetBuildLog`) font la même chose depuis
l'IDE.

## Arborescence actuelle

```text
CopyKit/
  App/CopyKitApp.swift      point d'entrée
  Resources/Assets.xcassets
  ContentView.swift         modèle du template, à remplacer par la première feature
  Item.swift                modèle du template, à remplacer par la première feature
CopyKitTests/               tests Swift Testing
CopyKitUITests/             tests XCUITest
docs/                       documentation (dossier synchronisé, sans cible)
```

`Features/`, `Shared/`, `Intents/` et `Packages/` apparaîtront avec leur premier
fichier.

## Documentation

- [docs/plugins/](docs/plugins/README.md) : plugins, stack, workflow, architecture.
- [docs/adr/](docs/adr/) : décisions d'architecture.
