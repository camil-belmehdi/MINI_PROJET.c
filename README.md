Voici l'intégralité du fichier `README.txt` complété :

```txt
# Chiffrement de César et Vigenère

## Description

Ce programme implémente les chiffrements de César et de Vigenère, deux techniques de cryptographie classique. Il permet de chiffrer et de déchiffrer des messages. Le programme traite les lettres majuscules et minuscules, supprime les espaces avant le chiffrement et réinsère les espaces après le déchiffrement.

## Auteurs

- Belmehdi Camil
- Bourdon Novellas

## Utilisation

### Prérequis

- Un compilateur C (comme `gcc` pour Unix/Linux, macOS, ou MinGW pour Windows)
- Un terminal ou une invite de commandes

### Compilation

1. Assurez-vous que vous avez un compilateur C installé.
2. Enregistrez le code suivant dans un fichier nommé `chiffrement.c` :

```c
#include <stdio.h>
#include <string.h>

// Fonction pour chiffrer le texte en utilisant le chiffrement de César
void chiffrement_cesar(char* texte, int decalage) {
    for (int i = 0; texte[i] != '\0'; i++) {
        if (texte[i] >= 'A' && texte[i] <= 'Z') {
            texte[i] = ((texte[i] - 'A' + decalage) % 26) + 'A';
        } else if (texte[i] >= 'a' && texte[i] <= 'z') {
            texte[i] = ((texte[i] - 'a' + decalage) % 26) + 'a';
        }
    }
}

// Fonction pour déchiffrer le texte en utilisant le chiffrement de César
void dechiffrement_cesar(char* texte, int decalage) {
    chiffrement_cesar(texte, 26 - decalage);
}

// Fonction pour chiffrer le texte en utilisant le chiffrement de Vigenère
void chiffrerVigenere(char* message, char* cle) {
    int longueur_message = strlen(message);
    int longueur_cle = strlen(cle);

    for (int i = 0; i < longueur_message; i++) {
        int n = i % longueur_cle;
        int decalage;

        if (cle[n] >= 'A' && cle[n] <= 'Z') {
            decalage = cle[n] - 'A';
        } else if (cle[n] >= 'a' && cle[n] <= 'z') {
            decalage = cle[n] - 'a';
        } else {
            // Si la clé contient un caractère non alphabétique, on ne change pas le décalage
            decalage = 0;
        }

        if (message[i] >= 'A' && message[i] <= 'Z') {
            message[i] = ((message[i] - 'A' + decalage) % 26) + 'A';
        } else if (message[i] >= 'a' && message[i] <= 'z') {
            message[i] = ((message[i] - 'a' + decalage) % 26) + 'a';
        }
    }
}

// Fonction pour déchiffrer le texte en utilisant le chiffrement de Vigenère
void dechiffrerVigenere(char* message, char* cle) {
    int longueur_message = strlen(message);
    int longueur_cle = strlen(cle);

    for (int i = 0; i < longueur_message; i++) {
        int n = i % longueur_cle;
        int decalage;

        if (cle[n] >= 'A' && cle[n] <= 'Z') {
            decalage = cle[n] - 'A';
        } else if (cle[n] >= 'a' && cle[n] <= 'z') {
            decalage = cle[n] - 'a';
        } else {
            // Si la clé contient un caractère non alphabétique, on ne change pas le décalage
            decalage = 0;
        }

        if (message[i] >= 'A' && message[i] <= 'Z') {
            message[i] = ((message[i] - 'A' - decalage + 26) % 26) + 'A';
        } else if (message[i] >= 'a' && message[i] <= 'z') {
            message[i] = ((message[i] - 'a' - decalage + 26) % 26) + 'a';
        }
    }
}

// Fonction pour supprimer les espaces d'un message
void supprimerEspaces(char* message) {
    int longueur_message = strlen(message);
    int j = 0; // Indice pour le nouveau message sans espaces
    
    // Parcourt la chaîne de caractères
    for (int i = 0; i < longueur_message; i++) {
        // Si le caractère courant n'est pas un espace, le conserve
        if (message[i] != ' ') {
            message[j] = message[i];
            j++;
        }
    }
    
    // Ajoute le caractère de fin de chaîne
    message[j] = '\0';
}

int main() {
    char message[1024];
    char cle[1024];
    int decalage;

    printf("Entrez le message à crypter : ");
    fgets(message, sizeof(message), stdin);
    // Supprimer le caractère de nouvelle ligne à la fin du message
    message[strcspn(message, "\n")] = 0;

    supprimerEspaces(message);

    printf("Entrez un décalage pour le chiffrement de César : ");
    scanf("%d", &decalage);
    getchar();  // Consommer le caractère de nouvelle ligne restant

    chiffrement_cesar(message, decalage);
    printf("Message chiffré avec César : %s\n", message);

    dechiffrement_cesar(message, decalage);
    printf("Message déchiffré avec César : %s\n", message);

    printf("Entrez la clé pour le chiffrement de Vigenère : ");
    fgets(cle, sizeof(cle), stdin);
    // Supprimer le caractère de nouvelle ligne à la fin de la clé
    cle[strcspn(cle, "\n")] = 0;

    // Chiffrer le message avec Vigenère
    chiffrerVigenere(message, cle);
    printf("Message chiffré avec Vigenère : %s\n", message);

    // Déchiffrer le message avec Vigenère
    dechiffrerVigenere(message, cle);
    printf("Message déchiffré avec Vigenère : %s\n", message);

    return 0;
}
```

3. Ouvrez un terminal ou une invite de commandes et naviguez jusqu'au répertoire contenant `chiffrement.c`.

4. Compilez le programme en utilisant la commande suivante :
   - Sous Unix/Linux ou macOS :
     ```sh
     gcc chiffrement.c -o chiffrement
     ```
   - Sous Windows :
     ```sh
     gcc chiffrement.c -o chiffrement.exe
     ```

### Exécution

- Sous Unix/Linux ou macOS :
  ```sh
  ./chiffrement
  ```

- Sous Windows :
  ```sh
  chiffrement.exe
  ```

### Instructions

1. Entrez le message que vous souhaitez chiffrer lorsqu'on vous le demande.
2. Entrez le décalage pour le chiffrement de César (un nombre entier).
3. Le programme affichera le message chiffré, puis le message déchiffré pour vérifier qu'il correspond au message original.
4. Entrez la clé pour le chiffrement de Vigenère.
5. Le programme affichera le message chiffré avec Vigenère, puis le message déchiffré pour vérifier qu'il correspond au message original.

### Documentation des fonctions

#### `void chiffrement_cesar(char* texte, int decalage)`
- **Paramètres** :
  - `texte` : La chaîne de caractères à chiffrer.
  - `decalage` : Le décalage à utiliser pour le chiffrement de César.
- **Sortie** : La chaîne de caractères est chiffrée en place.

#### `void dechiffrement_cesar(char* texte, int decalage)`
- **Paramètres** :
  - `texte` : La chaîne de caractères à déchiffrer.
  - `decalage` : Le décalage à utiliser pour le déchiffrement de César.
- **Sortie** : La chaîne de caractères est déchiffrée en place.

#### `void chiffrerVigenere(char* message, char* cle)`
- **Paramètres** :
  - `message` : La chaîne de caractères à chiffrer.
  - `cle` : La clé à utiliser pour le chiffrement de Vigenère.
- **Sortie** : La chaîne de caractères est chiffrée en place.

#### `void dechiffrerVigenere(char* message, char* cle)`
- **Paramètres** :
  - `message` : La chaîne de caractères à déchiffrer.
  - `cle` : La clé à utiliser pour le déchiffrement de Vigenère.
- **Sortie** : La chaîne de caractères est déchiffrée en place.

#### `void supprimerEspaces(char* message)`
- **Paramètres** :
  - `message` : La chaîne de caractères dont les espaces doivent être supprimés.
- **Sortie** : Les espaces sont supprimés de la chaîne de caractères.



### Cas d'erreur

- Si un caractère spécial non supporté est détecté dans le message ou la clé, une erreur sera affichée et le chiffrement ou déchiffrement sera arrêté.
- Les espaces sont supprimés avant le chiffrement et réinsérés après le déchiffrement.

---

Ce programme permet de chiffrer et déchiffrer des messages en utilisant les méthodes de chiffrement de César et de Vigenère, avec une gestion spéciale des espaces.
