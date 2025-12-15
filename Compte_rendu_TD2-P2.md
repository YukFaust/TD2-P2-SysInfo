# TD 2 Partie II : Modélisation des Processus Métier (BPMN)

## Exercice 1 : Gestion de commandes de pizza

### 1. Description du processus
[cite_start]Le processus décrit la gestion d'une commande de pizza impliquant 3 acteurs : le Gestionnaire, le Pizzaiolo et le Livreur[cite: 8].

* **Déclencheur** : Réception de la commande ("Commander pizza").
* **Déroulement** : Le gestionnaire émet la facture tandis que le pizzaiolo prépare la commande en parallèle.
* **Fin** : La commande est livrée puis le paiement est encaissé.

### 2. Modélisation BPMN (Schéma)

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/4cd1b3d8-3595-415b-8d72-6002ad1dac27" />


### [cite_start]3. Analyse du niveau de modélisation [cite: 9, 10]

* **Niveau : Intermédiaire**.
* **Justification :**
    * Le processus utilise des **Couloirs (Lanes)** pour répartir les rôles (Gestionnaire, Pizzaiolo, Livreur).
    * Il utilise des **Portes logiques parallèles (Parallel Gateways)** pour synchroniser les tâches simultanées (préparation et facturation).
    * Il inclut des **Objets de données** (la facture).

---

## Exercice 2 : Sous-processus de Paiement

### 1. Consigne
[cite_start]Nous devons modifier le processus pour intégrer un mode de gestion des paiements plus complexe (chèque, espèces, carte) sous forme de sous-processus, et ce paiement doit intervenir **avant** la livraison[cite: 12].

### [cite_start]2. Modélisation du Sous-Processus "Gérer le paiement" [cite: 13]


<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/88b75248-29f9-42e6-9fb4-55591d8fb8c9" />


### [cite_start]3. Intégration et Justification [cite: 14, 15, 16]

* **Intégration :** Dans le processus principal, l'activité "Encaisser le paiement" est supprimée et remplacée par une activité de type "Appel de sous-processus" placée **après** la porte de jonction (préparation terminée + facture émise) et **avant** la tâche "Livrer la commande".
* **Niveau : Avancé**.
* **Justification :**
    * L'utilisation de **Sous-Processus** hiérarchise le modèle.
    * L'utilisation de **Portes Exclusives (XOR Gateways)** implique des règles de gestion conditionnelles.
    * La modification de la séquence (paiement avant livraison) impacte la logique temporelle du flux.

---

## Exercice 3 : Agence de Voyage

[cite_start]Nous devons modéliser trois processus distincts basés sur les 7 phases identifiées précédemment [cite: 18-25].

### [cite_start]Processus 1 : Commande d'un circuit [cite: 28]
*Phases : Recherche, Personnalisation, Émission Devis.*

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/cc4381e2-fe22-41c4-b5fc-519eb58ee2df" />


* **Type :** Intermédiaire (Utilisation de gateways de décision).

### [cite_start]Processus 2 : Réservation et Confirmation [cite: 29]
*Phases : Réservation Préliminaire, Paiement, Confirmation/Envoi.*

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/87c35d65-85f5-4de2-8197-5451ae558948" />


* **Type :** Avancé (Boucles logiques implicites et gestion d'états d'attente).

### [cite_start]Processus 3 : SAV [cite: 30]
*Phase : Assistance Avant & Pendant le Voyage.*

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/97f04536-c3d9-43ad-9aab-b3fbbbd5aa9c" />


* **Type :** Basique (Séquence simple).

### [cite_start]Intégration globale [cite: 32, 33, 34]

**Est-il possible d'intégrer les trois processus ?**
Oui. On crée un **Processus Global (End-to-End)** qui orchestre l'ensemble. Les processus 1, 2 et 3 deviennent des phases séquentielles ou des sous-processus.

**Structure intégrée :**
1.  Le processus global démarre par le **Sous-processus 1** (Commande).
2.  Si le devis est validé, il déclenche le **Sous-processus 2** (Réservation/Paiement).
3.  Le **Sous-processus 3** (SAV) est un "Processus événementiel" qui peut être déclenché à tout moment en parallèle une fois la réservation faite (via un événement de type Message ou Signal).

**Niveau du processus résultant : Avancé**.
* **Justification :** L'intégration nécessite l'utilisation de sous-processus (Sub-Processes), d'événements de fin et de début liés, et potentiellement d'événements frontières (Boundary Events) pour gérer le SAV en parallèle du flux principal.
