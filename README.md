# Netflix Shows & Movies - Data Warehouse ETL Pipeline

An end-to-end Data Engineering project that extracts raw data from the Netflix movies and TV shows dataset, transforms it into an optimized **Star Schema (Dimensional Model)** using Python (Pandas), and loads it into a local **Microsoft SQL Server** instance for analytical purposes using Windows Authentication.

## 📌 Project Overview & Achievements
Today, we successfully built and deployed a robust ETL (Extract, Transform, Load) pipeline that bridges a flat raw dataset into an enterprise-grade Relational Database Management System (RDBMS). 

### Key Accomplishments:
1. **Data Cleaning & Preprocessing:** Handled missing values, stripped trailing whitespaces, and parsed data into correct data types (e.g., converted dates into normalized `datetime` objects).
2. **Dimensional Modeling:** Resolved multi-valued attributes (handling rows with multiple countries or categories) by exploding lists to eliminate spatial redundancy, creating a highly granular **Star Schema**.
3. **Database Security & Ingestion:** Configured Python (`SQLAlchemy` + `pyodbc`) to authenticate securely with **Microsoft SQL Server** via Windows Integrated Security, dynamically overriding local auto-signed certificate constraints (`TrustServerCertificate=yes`).
4. **DevOps & Portability:** Secured environment structures using an optimized `.gitignore` and successfully published the repository under the `main` branch configuration in GitHub.

---

## 📐 Data Warehouse Architecture (Star Schema)

The architecture splits the data into a centralized **Fact Table** surrounded by four decoupled **Dimension Tables** to maximize analytic query performance and reporting scalability.

```mermaid
erDiagram
    Fact_Shows {
        string show_id PK
        int sk_contenido FK
        int sk_tiempo FK
        int sk_geografia FK
        int sk_categoria FK
    }
    Dim_Contenido {
        int sk_contenido PK
        string show_id
        string type
        string title
        string director
        string cast
        string rating
        int release_year
    }
    Dim_Tiempo {
        int sk_tiempo PK
        date date_added
        int year
        int month
        int quarter
    }
    Dim_Geografia {
        int sk_geografia PK
        string country
    }
    Dim_Categorias {
        int sk_categoria PK
        string listed_in
    }

    Fact_Shows }|--|| Dim_Contenido : "maps to"
    Fact_Shows }|--|| Dim_Tiempo : "maps to"
    Fact_Shows }|--|| Dim_Geografia : "maps to"
    Fact_Shows }|--|| Dim_Categorias : "maps to"
