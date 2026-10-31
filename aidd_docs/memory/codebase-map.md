# Codebase Map

The macro layout: the top-level areas and what each holds. A map to navigate, not the full tree.

```mermaid
flowchart TD
  Root["CopyKit/ (dépôt)"] --> App["CopyKit/ · cible app"]
  Root --> Tests["CopyKitTests/ · Swift Testing"]
  Root --> UITests["CopyKitUITests/ · XCUITest"]
  Root --> Docs["docs/ · doc, ADR"]
  Root --> Aidd["aidd_docs/ · mémoire, produit, backlog"]
```

## Areas

- `CopyKit/`: la cible app ; `App/` (point d'entrée), `Resources/` (assets) ; `ContentView.swift` et `Item.swift` sont l'exemple du template Xcode, remplacés par la première story.
- `CopyKitTests/`: tests unitaires et d'intégration Swift Testing.
- `CopyKitUITests/`: tests d'interface XCUITest.
- `docs/`: notre documentation : plugins et workflow (`docs/plugins/`), décisions (`docs/adr/`).
- `aidd_docs/`: ce que produit AIDD : mémoire, brief, backlog, plans.

## Entry points

- `CopyKit/App/CopyKitApp.swift` : `@main`, scène principale et conteneur SwiftData.
