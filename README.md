# Local Data Lakehouse Project

This repository demonstrates a full end-to-end **local Data Lakehouse** implementation:

* **Raw data ingestion** (PySpark → Delta Lake)
* **dbt data modeling** (staging, intermediate, marts)
* **DuckDB + Flask API** for querying Delta tables
* **Next.js + Tailwind CSS** frontend (dashboard + explore UI)
* **Docker Compose** orchestration of all services
* **GitHub Actions** for CI/CD of dbt models

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your machine:

* **Java** (OpenJDK 8 or 11)
* **Python** 3.8+
* **Node.js** 16+ and **Yarn** (or npm)
* **Docker** & **Docker Compose**
* **Git** (for cloning the repo)

---

## 🚀 Quickstart

1. **Clone this repository**

   ```bash
   git clone https://github.com/yourusername/lakehouse-project.git
   cd lakehouse-project
   ```

2. **Add raw data**

   * Place your CSV/JSON files into appropriate folders under `data/landing_zone/` (e.g., `data/landing_zone/nyc_taxi/`).

3. **Run everything with Docker Compose**

   ```bash
   docker-compose up --build
   ```

   * **Spark** ingestion job will process raw files into Delta Lake tables under `data/bronze/` and `data/silver/`.
   * **Flask API** will serve query endpoints on port **5000**.
   * **Next.js** frontend will be available at **[http://localhost:3000](http://localhost:3000)**.

4. **Interact with the app**

   * **Dashboard**: [http://localhost:3000/dashboard](http://localhost:3000/dashboard)
   * **Explore Data**: [http://localhost:3000/explore](http://localhost:3000/explore)
   * **Login credentials** are defined in `frontend/.env.local` (default: `admin` / `secret123`).

5. **Run dbt (locally)**

   ```bash
   cd dbt
   dbt deps
   dbt run
   dbt test
   dbt docs generate && dbt docs serve
   ```

---

## 📂 Folder Structure

```
lakehouse-project/
├── data/
│   ├── landing_zone/      ← Raw CSV/JSON files
│   ├── bronze/            ← Delta Lake bronze tables
│   ├── silver/            ← Delta Lake silver tables
│   └── gold/              ← (Optional) Delta Lake gold tables
├── ingestion/
│   ├── pyspark_job.py     ← PySpark ingestion script
│   └── requirements.txt   ← Python dependencies
├── dbt/
│   ├── dbt_project.yml    ← dbt project config
│   ├── profiles.yml       ← dbt connection profiles
│   └── models/            ← Staging, intermediate, and marts
├── api/
│   ├── app.py             ← Flask + DuckDB API
│   └── requirements.txt   ← Python dependencies
├── frontend/
│   ├── pages/             ← Next.js pages (login, dashboard, explore)
│   ├── components/        ← UI components (Layout, charts)
│   ├── styles/            ← Tailwind CSS config
│   └── package.json       ← Frontend dependencies & scripts
├── docker-compose.yml     ← Orchestrate Spark, API, and frontend
├── Dockerfile.api         ← Build Flask API container
├── Dockerfile.frontend    ← Build Next.js container
└── .github/
    └── workflows/
        └── dbt-ci.yml     ← GitHub Actions for dbt CI/CD
```

---

## 🔧 Customization & Next Steps

1. **Add More Datasets**

   * Drop additional files into `data/landing_zone/` and update `ingestion/pyspark_job.py` to handle them.

2. **Enhance dbt Models**

   * Create new intermediate models or marts (e.g., combine taxi + COVID data, add business logic).

3. **Improve Frontend**

   * Integrate a map (Leaflet/Mapbox) for geospatial visualizations.
   * Add dual-axis charts for COVID vs. taxi trends.

4. **Swap Query Engine**

   * Replace DuckDB with Trino for distributed querying; update API code accordingly.

5. **Deploy Publicly**

   * Push the Next.js app to Vercel for a live demo URL.
   * Use a managed Spark/Delta Lake service if you want to scale beyond local.

---

## 📄 License

This project is open-source under the **MIT License**. Feel free to reuse and adapt for your own portfolios!

---

*Enjoy building your local Lakehouse—and happy coding!*
