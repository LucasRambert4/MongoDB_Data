📚 LibDB – Projet MongoDB
EFREI M1 Data Engineering – Groupe 3

Auteurs : Cindy Tchuiesseu & Joseph Rambert

🧩 Présentation

LibDB est une base de données NoSQL développée sous MongoDB Atlas pour gérer des bibliothèques et leurs livres à travers différentes villes françaises.
Le projet illustre les opérations FIND, UPDATE, AGGREGATE, INDEX et la visualisation avec MongoDB Charts.

🗂️ Structure de la base

Base : libdb
Connexion :

mongodb+srv://User:User@cluster0.ucqgbv9.mongodb.net/

Collections principales

books

libraries

cities

💾 Données

books.json → 50+ livres français (Romans, Poésie, Philosophie, etc.)

libraries.json → 50 bibliothèques françaises avec sections internes

Visualisations créées avec MongoDB Charts

⚙️ Exemples de requêtes
db.books.find({ title: "Les Misérables" })
db.books.find({ copies: { $gt: 5 } })
db.books.updateMany({}, { $inc: { copies: 2 } })
db.libraries.aggregate([
  { $lookup: { from: "cities", localField: "city_ref", foreignField: "city_id", as: "city_info" } }
])

📊 Visualisations

Répartition des livres par genre – Diagramme à barres

Budgets des bibliothèques – Diagramme en anneau


🏁 Objectif

Ce projet montre comment modéliser, interroger et visualiser des données NoSQL avec MongoDB, en appliquant les bonnes pratiques de performance et de structuration.
