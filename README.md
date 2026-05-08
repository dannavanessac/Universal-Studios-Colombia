# Universal Studios Colombia - Data Lake (NoSQL Database)

## Project Overview
This project involves the creation of a **Data Lake for Universal Studios Colombia's online record store**, utilizing **MongoDB** as the NoSQL database engine. The system models a collection of albums and song documents for six distinct international and Latin American artists across various musical genres. The main goal is to demonstrate NoSQL database management, including data modeling, insertion, updates, deletions, and data extraction using MongoDB Atlas.

---

## Tasks Summary

### Task 1: Initial Database Creation (`main` branch)
We initialized a MongoDB Atlas database cluster and created six collections representing six different albums from artists like Lady Gaga, BTS, Queen, Michael Jackson, Diomedes Díaz, and Ivy Queen. We populated these collections with the main tracks of each album, ensuring that each document contained all mandatory fields (`_id`, `titulo`, `anio_salida`, `autor`, `id_imagen_portada`) as well as optional metadata (`genero`, `duracion`, `numero_pista`, `popularidad`). BSON files and a consolidated CSV file were exported.

### Task 2: Album Updates (`actualizaciones` branch)
We expanded the database by incorporating lesser-known songs, hidden tracks, and remixes to each album collection. This phase simulated an active data pipeline update. We performed data integrity checks and exported the new, expanded database state into updated CSV and BSON formats.

### Task 3: Deletion Operations (`eliminaciones` branch)
We performed targeted deletions to simulate data purging. Two songs were removed from each active album collection, and the complete collection for the artist *Ivy Queen* (`Sentimiento` album) was entirely dropped from the database. The final state was exported, and related media (images) for the deleted collection were systematically removed.

---

## Data Model Structure
The database follows a document-oriented model appropriate for MongoDB:
- **Collections**: Each album serves as its own independent collection.
- **Documents**: Each song is an individual document within an album's collection.

**Document Schema Design:**
```json
{
  "_id": 1, // Unique identifier (Integer)
  "titulo": "Bad Romance", // Song title (String)
  "anio_salida": 2009, // Release year (Integer)
  "autor": "Lady Gaga", // Artist name (String)
  "id_imagen_portada": "lady_gaga.jpg", // Album cover filename reference (String)
  "genero": "Pop", // Optional: Musical genre (String)
  "duracion": "4:54", // Optional: Track length (String)
  "numero_pista": 1, // Optional: Track number (Integer)
  "popularidad": 98 // Optional: Popularity score 0-100 (Integer)
}
```

---

## Design Decisions
1. **Manual Execution via MongoSH**: We decided to execute our database commands directly using the MongoDB Shell (MongoSH) embedded in MongoDB Compass to ensure hands-on familiarity with native NoSQL queries (like `insertMany` and `deleteMany`).
2. **Export Strategy via Compass**: Instead of relying on external command-line tools, we utilized MongoDB Compass's native export functionalities. This provided a reliable way to export both full collections as CSV files and individual documents as JSON (acting as the BSON equivalent for the deliverables).
3. **Data Type Standardization**: Numeric IDs were used sequentially (`1`, `2`, `3`, etc.) instead of default MongoDB ObjectIDs to allow for easier tracking across tasks, simpler querying, and clearer JSON visualization.
4. **Segregation of Deliverables**: To manage Git branch requirements efficiently, we maintained a strict local folder structure for each task checkpoint before committing to the respective branches.

---

## Findings & Lessons Learned
- **MongoDB Flexibility**: The schemaless nature of MongoDB made it extremely easy to append new optional fields (`genero`, `duracion`) to the documents on the fly without running complex database schema migrations.
- **Exporting Challenges**: Exporting a consolidated CSV of *all* collections simultaneously is not natively supported by a single button in Compass. We had to export each collection individually and consolidate the deliverables, which highlighted the differences between relational DB exports and NoSQL document stores.
- **Git State Management**: Organizing NoSQL database dumps into Git branches requires careful orchestration to ensure that local file states accurately reflect the remote database state at any given task checkpoint.

---

## Instructions to Replicate
**Prerequisites:**
- MongoDB Compass installed.
- A MongoDB cluster running locally or via MongoDB Atlas.

**Steps:**
1. Clone the repository and navigate to the respective branch (`main`, `actualizaciones`, or `eliminaciones`).
2. Open MongoDB Compass and connect to your database cluster.
3. Import the BSON/JSON files from the `bson_collections` folder into your database to replicate the state.
4. To verify the insertions and deletions, use the Mongo Shell (`>_ MONGOSH`) at the bottom of Compass to run queries like `db.TheFameMonster.find()`.
