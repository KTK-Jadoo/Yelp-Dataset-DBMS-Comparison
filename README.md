# PostgreSQL and MongoDB Query Analysis on the Yelp Open Dataset

This project benchmarks and analyzes relational (PostgreSQL) vs. non-relational (MongoDB) database systems using the **Yelp Open Dataset**. It demonstrates **data ingestion, schema design, and comparative query performance** across both systems on real-world, large-scale data.

---

## 📂 Dataset

We used the [Yelp Open Dataset](https://www.yelp.com/dataset), a **8.65 GB JSON dataset** containing:

* **6.99M Reviews** — text, ratings, metadata
* **150K Businesses** — names, locations, attributes (WiFi, parking, etc.)
* **1.98M Users** — profiles, review histories, friend networks
* **200K Photos** and **900K Tips** (not fully utilized)

A subset was sampled for experiments to balance **representativeness** and **computational efficiency**.

---

## ⚙️ Project Setup

### PostgreSQL

* Installed via `brew install postgresql@14`
* JSON → CSV transformation in Python
* Bulk loading with `COPY` and referential integrity checks
* Conflict handling with `ON CONFLICT DO NOTHING`

### MongoDB

* Direct JSON ingestion using `pymongo`
* Separate collections for users, businesses, reviews
* Schema-less flexibility vs PostgreSQL’s strict schema design

---

## 📊 Benchmark Queries

We designed five representative tasks:

1. **Aggregate Analysis of User Reviews**
   Group users by number of reviews; compare distribution across systems.

2. **Keyword Search in Reviews**
   Search for reviews containing *“horrible”*; compare performance of full text scans.

3. **Top Business Categories by Average Rating**
   Explode categories, compute average ratings, rank top categories.

4. *(Extension point for more complex joins — WIP)*

5. *(Extension point for geospatial/temporal queries — WIP)*

---

## 🚀 Key Findings

* **PostgreSQL**

  * Faster on structured queries and keyword searches when indexed
  * Bulk insert overhead and schema rigidity slowed ingestion
  * Superior indexing, query plans, and parallelization

* **MongoDB**

  * Extremely simple ingestion (direct JSON load)
  * Aggregation pipeline concise for semi-structured data
  * Slower on first runs due to lack of indexing, especially regex searches

Example:

* **Task 1 (Aggregate):** PostgreSQL \~13.6 s vs MongoDB \~23.2 s
* **Task 2 (Keyword Search):** PostgreSQL \~7 ms vs MongoDB \~23 s (collection scan)

---

## 📁 Repository Structure

```
├── data/                  # Yelp dataset (JSON, not included in repo)
├── notebooks/             # Jupyter notebooks with full query analysis
├── postgres_scripts/      # Python + SQL loaders, queries
├── mongo_scripts/         # Python + MongoDB ingestion & pipelines
├── er-diagram.png         # ER diagram of Yelp schema
├── report/                # LaTeX report (main.tex, compiled PDF)
└── README.md              # Project documentation
```

---

## 👨‍💻 Authors

* Kartikeya Sharma
* Clement Lui
* Richard Villagomez
* Nicholas Chae

---

## 📜 License

This project is for **academic purposes only**, based on the public [Yelp Open Dataset license](https://www.yelp.com/dataset).



