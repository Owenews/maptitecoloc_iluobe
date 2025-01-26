# MaPtiteColoc

Le but de ce projet est de créer une application web qui permet aux utilisateurs de gérer leurs colocations. Elle permettra également aux propriétaires de gérer les membres de leur colocation et de gérer les tâches associées à la colocation. Enfin, il permettra aux propriétaires de gérer leurs finances. 


## Installation

1. Cloner le dépôt Git.
2. Installer les dépendances :
   ```bash
   npm install
   ```

## Routes Principales

### Authentification - /api/users

- **POST /register**  
  Crée un nouvel utilisateur.

  Exemple de données :  
  ```json
  {
    "email": "john.doe@gmail.com",
    "password": "john123"
    "firstName": "John",
    "lastName": "Doe",
    "phoneNumber": "0612345678",
    "address": "12 rue de la mairie",
    "city": "Paris",
    "zipcode": "75001",
    "latitude": 48.856614,
    "longitude": 2.352222
  }
  ```

- **POST /login**  
  Authentifie un utilisateur.

  Exemple de données :
  ```json
  {
    "email": "john.doe@gmail.com",
    "password": "john123"
  }

- **POST /refresh**  
  Renouvelle le token d’authentification.

  Exemple de données :
  ```json
  {
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiI1ZTM1ODA1MDI0MDQ0NDk3MDk5IiwiaWF0IjoxNjI4NjQ5Njk2LCJleHAiOjE2Mjg2NDc2OTZ9.3-5w-3w3w3w3w3w3w3w3w3w3w3w3w"
  }
  ```

- **GET /me**  
  Récupère les informations de l’utilisateur connecté.

  Exemple de données :
  ```json
  {
    "id": "5f81b3d8d4f6c2d1f8f7f1",
    "email": "john.doe@gmail.com",
    "firstName": "John",
    "lastName": "Doe",
    "phoneNumber": "0612345678",
    "address": "12 rue de la mairie",
    "city": "Paris",
    "zipcode": "75001",
    "latitude": 48.856614,
    "longitude": 2.352222,
    "isAdmin": false,
    "createdAt": "2021-01-01T00:00:00.000Z",
    "updatedAt": "2021-01-01T00:00:00.000Z"
  }

### Colocation - /api/colocs

- **POST /create (protégé)**  
  Crée une nouvelle colocation.

  Exemple de données :
  ```json
  {
    "name": "Ma colocation",
    "address": "12 rue de la mairie",
    "city": "Paris",
    "zipcode": "75001",
    "latitude": 48.856614,
    "longitude": 2.352222,
    "description": "Ma première colocation",  
    "owner": "5f81b3d8d4f6c2d1f8f7f1",
    "guests": [
      "5f81b3d8d4f6c2d1f8f7f1",
      "5f81b3d8d4f6c2d1f8f7f2"
    ]
  }

- **GET /:id (protégé)**  
  Récupère les informations d’une colocation.

  Exemple de données :
  ```json
  {
    "id": "5f81b3d8d4f6c2d1f8f7f1",
    "name": "Ma colocation",
    "address": "12 rue de la mairie",
    "city": "Paris",
    "zipcode": "75001",
    "latitude": 48.856614,
    "longitude": 2.352222,
    "description": "Ma première colocation",
    "owner": "5f81b3d8d4f6c2d1f8f7f1",
    "guests": [
      "5f81b3d8d4f6c2d1f8f7f1",
      "5f81b3d8d4f6c2d1f8f7f2"
    ],
    "createdAt": "2021-01-01T00:00:00.000Z",
    "updatedAt": "2021-01-01T00:00:00.000Z"
  }

- **DELETE /:id (protégé)**  
  Supprime une colocation.

  Exemple de données :
  ```json
  {
    "id": "5f81b3d8d4f6c2d1f8f7f1"
  }


### Membres - /api/members

- **POST /add (protégé)**  
Ajout d'un membre à la colocation (autorisé uniquement au propriétaire).

- **DELETE /remove (protégé)**  
Suppression d'un membre de la colocation (autorisé uniquement au propriétaire).

Exemple de données :
```json
{
  "id": "5f81b3d8d4f6c2d1f8f7f1"
}

### Finances (Exemple) - /api/finances

- **POST /charges (protégé)**  
Ajout d'une charge

Exemple de données :
```json
{
  "id": "5f81b3d8d4f6c2d1f8f7f1",
  "amount": 100,
  "description": "Loyer",
  "date": "2021-01-01T00:00:00.000Z"
}

- **POST /pay (protégé)**  
Simule un paiement/remboursement.

Exemple de données :
```json
{
  "id": "5f81b3d8d4f6c2d1f8f7f1",
  "amount": 100,
  "description": "Loyer",
  "date": "2021-01-01T00:00:00.000Z"
}

- **GET /history (protégé)**  
  Retourne l’historique des transactions.

  Exemple de données :
  ```json
  [
    {
      "id": "5f81b3d8d4f6c2d1f8f7f1",
      "amount": 100,
      "description": "Loyer",
      "date": "2021-01-01T00:00:00.000Z"
    },
    {
      "id": "5f81b3d8d4f6c2d1f8f7f1",
      "amount": 100,
      "description": "Loyer",
      "date": "2021-01-01T00:00:00.000Z"
    }
  ]
