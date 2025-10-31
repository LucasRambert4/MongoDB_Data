📚 LibDB – MongoDB Library Management Project
EFREI M1 Data Engineering – Groupe 3

Authors: Cindy Tchuiesseu & Joseph Rambert
Project: MongoDB NoSQL – Library and Books Database

🧩 Project Overview

LibDB is a NoSQL database built using MongoDB Atlas to manage information about libraries and their books across different French cities.
It demonstrates MongoDB’s core functionalities such as CRUD operations, aggregation pipelines, data referencing, indexing, and visualization using MongoDB Charts.

🗂️ Database Structure

Database name: libdb
Connection URI:

mongodb+srv://User:User@cluster0.ucqgbv9.mongodb.net/

Collections

books – Contains all the books available across libraries.

{
  "_id": ObjectId(),
  "title": "Les Misérables",
  "author": "Victor Hugo",
  "genre": "Roman",
  "publication_year": 1862,
  "copies": 8,
  "library_name": "Bibliothèque Centrale"
}


libraries – Lists libraries with embedded section information.

{
  "_id": ObjectId(),
  "name": "Bibliothèque Centrale",
  "city": "Paris",
  "established_year": 1985,
  "sections": [
    {"name": "Romans", "books_count": 1200},
    {"name": "Science", "books_count": 500}
  ],
  "budget_euros": 250000,
  "city_ref": 5
}


cities – Links each library to its corresponding city (referenced by city_ref).

{
  "_id": ObjectId(),
  "city_name": "Paris",
  "region": "Île-de-France",
  "city_id": 5
}

💾 Data Files
File	Description
books.json	Contains 50+ French literary works across genres (Roman, Poésie, Philosophie, Théâtre, etc.)
libraries.json	Defines 50 libraries across France with nested section data
Devoir – Projet MongoDB.pdf	Detailed project report (steps, queries, updates, indexes, charts)
EFREI_NOSQL_GROUPE_SIMPLE_3.pptx	Presentation slides used for project defense
Humongous Idea v6.pdf	Original assignment specification (“Humongous Idea” brief)
🧠 Features & MongoDB Operations
🔍 FIND Queries

Find by title:

db.books.find({ title: "Les Misérables" })


Filter by number of copies:

db.books.find({ copies: { $gt: 5 } })


Sort by genre and publication year:

db.books.find().sort({ genre: 1, publication_year: -1 })


Filter with $and:

db.books.find({ $and: [ { genre: "Roman" }, { copies: { $gt: 4 } } ] })

✏️ UPDATE Operations

Increment copies:

db.books.updateMany({}, { $inc: { copies: 2 } })


Add a new section:

db.libraries.updateOne(
  { name: "Bibliothèque Centrale" },
  { $push: { sections: { name: "Histoire", books_count: 200 } } }
)


Rename a field:

db.books.updateMany({}, { $rename: { "copies": "available_copies" } })

🔗 References & Aggregation

Create cities collection and reference using city_ref

Add computed field:

db.cities.updateMany({}, [ { $set: { city_id: { $strLenCP: "$city_name" } } } ])


Join libraries and cities:

db.libraries.aggregate([
  {
    $lookup: {
      from: "cities",
      localField: "city_ref",
      foreignField: "city_id",
      as: "city_info"
    }
  }
])

⚡ Indexes
db.books.createIndex({ title: 1 })
db.books.createIndex({ genre: 1, publication_year: -1 })
db.libraries.createIndex({ city: 1 })


Justification:

title → speeds up title searches.

genre + publication_year → improves sorting and filtering.

city → optimizes library searches by location.

📊 Visualizations (MongoDB Charts)

Books by Genre

Type: Horizontal Bar Chart

Source: books

X-axis: count(_id)

Y-axis: genre

Insight: Highlights diversity of genres (Romans, Aventure, Théâtre).

Library Budgets by Name

Type: Donut Chart

Source: libraries

Value: budget_euros

Label: name

Insight: Shows budget disparity, with Paris libraries dominating totals.

🚀 Setup Instructions

Clone the repository

git clone https://github.com/<your-username>/LibDB.git
cd LibDB


Import data into MongoDB

mongoimport --uri "mongodb+srv://User:User@cluster0.ucqgbv9.mongodb.net/libdb" \
--collection books --file books.json --jsonArray

mongoimport --uri "mongodb+srv://User:User@cluster0.ucqgbv9.mongodb.net/libdb" \
--collection libraries --file libraries.json --jsonArray


Explore with MongoDB Compass or Atlas
Use the connection URI provided above.

🧾 Deliverables

✅ JSON data files (books.json, libraries.json)

✅ MongoDB queries and updates

✅ Aggregations and indexes

✅ Charts and analysis

✅ Presentation slides and report

🏁 Conclusion

This project demonstrates the design and management of a NoSQL database in MongoDB, focusing on data modeling, embedded documents, referencing, and performance optimization.
It provides a practical example of how to handle complex datasets efficiently while visualizing insights using MongoDB Charts.
