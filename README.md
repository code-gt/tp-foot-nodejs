## Étapes à suivre

1. **Initialisation du projet Node.js**
   - Créez un nouveau répertoire pour votre projet et initialisez un nouveau projet Node.js à l'intérieur.

     ```bash
     mkdir tp-foot
     cd tp-foot
     npm init -y
     ```

2. **Installation des dépendances nécessaires**
   - Nous aurons besoin de `express` pour la gestion des routes et de `tailwindcss` pour le style.

     ```bash
     <script src="https://cdn.tailwindcss.com"></script>
     ```

3. **Création du serveur Node.js**
   - Créez un fichier `server.js` pour votre serveur Node.js.

     ```javascript
     // server.js
     const express = require('express');
     const path = require('path');
     const app = express();
     const PORT = 3000;

     // Middleware pour parser le JSON
     app.use(express.json());
     // Middleware pour servir les fichiers statiques
     app.use(express.static(path.join(__dirname, 'public')));

     // Page d'accueil
     app.get('/', (req, res) => {
       res.sendFile(path.join(__dirname, 'public', 'index.html'));
     });

     // Page pour ajouter un joueur
     app.get('/add-player', (req, res) => {
       res.sendFile(path.join(__dirname, 'public', 'add-player.html'));
     });

     // Route pour soumettre un joueur
     app.post('/add-player', (req, res) => {
       // Traitement pour ajouter un joueur
       console.log(req.body);
       // Redirection vers la page d'accueil
       res.redirect('/');
     });

     // Route pour afficher les joueurs (simulé)
     app.get('/players', (req, res) => {
       // Simulons une liste de joueurs
       const players = [
         { id: 1, name: 'Joueur 1' },
         { id: 2, name: 'Joueur 2' },
         { id: 3, name: 'Joueur 3' }
       ];
       res.json(players);
     });

     app.listen(PORT, () => {
       console.log(`Server is running on http://localhost:${PORT}`);
     });
     ```

5. **Création des fichiers HTML**
   - Créez un dossier `public` à la racine du projet et créez les fichiers HTML suivants :

     - `index.html`

     ```html
     <!-- public/index.html -->
     <!DOCTYPE html>
     <html lang="en">
     <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Accueil</title>
       <link rel="stylesheet" href="/styles.css">
     </head>
     <body>
       <h1>Liste des joueurs</h1>
       <button onclick="window.location.href='/add-player'">Ajouter un joueur</button>
       <ul id="players-list"></ul>
       <script src="/scripts.js"></script>
     </body>
     </html>
     ```

     - `add-player.html`

     ```html
     <!-- public/add-player.html -->
     <!DOCTYPE html>
     <html lang="en">
     <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Ajouter un joueur</title>
       <link rel="stylesheet" href="/styles.css">
     </head>
     <body>
       <h1>Ajouter un joueur</h1>
       <form action="/add-player" method="POST">
         <label for="name">Nom du joueur:</label><br>
         <input type="text" id="name" name="name"><br>
         <button type="submit">Ajouter</button>
       </form>
     </body>
     </html>
     ```

6. **Création d'un fichier JavaScript pour les interactions client**
   - Créez un fichier `public/scripts.js`.

     ```javascript
     // public/scripts.js
     fetch('/players')
       .then(response => response.json())
       .then(players => {
         const playersList = document.getElementById('players-list');
         players.forEach(player => {
           const listItem = document.createElement('li');
           listItem.textContent = player.name;
           playersList.appendChild(listItem);
         });
       });
     ```

7. **Lancement du serveur**
   - Lancez votre serveur Node.js.

     ```bash
     node server.js
     ```

9. **Accéder à l'application**
   - Ouvrez votre navigateur et accédez à `http://localhost:3000` pour voir votre application en action.

## Conclusion
Félicitations ! Vous avez maintenant créé un serveur web simple en utilisant Node.js avec plusieurs routes et une intégration de Tailwind CSS pour le style.