# Projet-SFSD
# Simulateur de Gestion de Fichiers

Ce simulateur permet de gérer une mémoire secondaire simulée avec différentes organisations de fichiers et méthodes d'accès. Il implémente les concepts fondamentaux de la gestion des fichiers, notamment l'organisation contiguë et chaînée, ainsi que le tri interne des enregistrements.

## Table des matières
1. [Installation](#installation)
2. [Compilation](#compilation)
3. [Utilisation](#utilisation)
4. [Fonctionnalités](#fonctionnalités)
5. [Structures de données](#structures-de-données)
6. [Exemple d'utilisation](#exemple-dutilisation)

## Installation

### Prérequis
- Compilateur C (GCC recommandé)
- Terminal ou invite de commande
- Système d'exploitation compatible (Linux, macOS, Windows)

### Compilation

Pour compiler le programme, utilisez la commande suivante :

```bash
gcc -o file_simulator main.c
```

## Utilisation

1. Lancez le programme compilé :
```bash
./file_simulator
```

2. À l'initialisation, vous devrez spécifier :
   - Le nombre total de blocs dans la mémoire secondaire
   - La taille des blocs (facteur de blocage)

## Fonctionnalités

Le simulateur propose les fonctionnalités suivantes :

### 1. Création de fichiers
- Définition du nom du fichier
- Spécification du nombre d'enregistrements
- Choix de l'organisation globale :
  - `C` : Organisation contiguë
  - `L` : Organisation chaînée
- Choix de l'organisation interne :
  - `T` : Triée
  - `N` : Non triée

### 2. Gestion des enregistrements
- Insertion d'enregistrements
- Recherche par ID
- Suppression (logique ou physique)
- Défragmentation de fichier

### 3. Gestion des fichiers
- Renommage de fichiers
- Suppression de fichiers
- Affichage des métadonnées
- Compactage de la mémoire

### 4. Visualisation
- Affichage de l'état de la mémoire
- Représentation visuelle des blocs (libres/occupés)
- Consultation des métadonnées

## Structures de données

### Record (Enregistrement)
```c
typedef struct {
    int id;
    char isDeleted;
} Record;
```

### Metadata (Métadonnées)
```c
typedef struct {
    char filename[MAX_FILENAME];
    int numBlocks;
    int numRecords;
    int firstBlockAddress;
    char globalOrganization;
    char internalOrganization;
} Metadata;
```

### Block (Bloc)
```c
typedef struct {
    Record* records;
    int numRecords;
    int nextBlock;
    char filename[MAX_FILENAME];
} Block;
```

## Exemple d'utilisation

1. Création d'un fichier :
```
Choix: 1
Nom du fichier: test
Nombre d'enregistrements: 10
Organisation globale (C/L): C
Organisation interne (T/N): T
```

2. Insertion d'un enregistrement :
```
Choix: 5
Nom du fichier: test
ID du nouvel enregistrement: 1
```

3. Recherche d'un enregistrement :
```
Choix: 4
Nom du fichier: test
ID de l'enregistrement: 1
```

4. Visualisation de l'état :
```
Choix: 2
```

## Notes importantes

- Les blocs libres sont affichés en vert dans la visualisation de la mémoire
- Les blocs occupés sont affichés en rouge avec le nom du fichier
- La suppression logique marque simplement les enregistrements comme supprimés
- La suppression physique réorganise les enregistrements dans les blocs
- Le compactage de la mémoire déplace tous les fichiers vers le début de la mémoire
- La défragmentation réorganise les enregistrements valides dans un fichier

## Limitations

- Nombre maximum de fichiers : 100
- Taille maximum du nom de fichier : 50 caractères
- Nombre maximum d'enregistrements : 1000
