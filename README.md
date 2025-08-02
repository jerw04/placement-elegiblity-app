# 📊 Placement Eligibility Streamlit Application

## 📌 Project Overview

This project is a **Placement Eligibility Dashboard** that enables placement teams to filter eligible students using customizable criteria. It integrates **Python, SQL (SQLite), Faker, and optionally Streamlit** to create, store, analyze, and display student readiness data.

> **Domain:** Ed-Tech  
> **Use Case:** Dynamic student filtering for placements based on programming, soft skills, and placement readiness.

---

## 🎯 Problem Statement

In traditional systems, manually filtering students for placements is inefficient and error-prone. This application solves that problem by:
- Providing a centralized view of student performance.
- Allowing dynamic filtering using interactive inputs or SQL queries.
- Automating student shortlisting based on key metrics.

---

## 💼 Business Use Cases

- 🧑‍💼 **Placement Management:** Shortlist candidates based on skill thresholds.
- 🧪 **Performance Tracking:** Monitor programming & soft skill progress.
- 📊 **Interactive Analytics:** Extract insights like top performers, placement trends, etc.

---

## 🔧 Tech Stack

| Tool          | Purpose                         |
|---------------|---------------------------------|
| Python 🐍      | Core logic and data generation  |
| SQLite 🗃️      | Lightweight relational database |
| Faker 🤖       | Synthetic student data creation |
| Pandas 🐼      | SQL query handling & analysis   |
| Streamlit 🌐   | (Optional) Dashboard frontend   |

---

## 🗂️ Database Schema

The application generates four relational tables:

### 1. `students`
- `student_id` (PK)
- `name`, `age`, `gender`, `email`, `phone`
- `enrollment_year`, `course_batch`, `city`, `graduation_year`

### 2. `programming`
- `programming_id` (PK), `student_id` (FK)
- `language`, `problems_solved`, `assessments_completed`
- `mini_projects`, `certifications_earned`, `latest_project_score`

### 3. `soft_skills`
- `soft_skill_id` (PK), `student_id` (FK)
- `communication`, `teamwork`, `presentation`, `leadership`
- `critical_thinking`, `interpersonal_skills`

### 4. `placements`
- `placement_id` (PK), `student_id` (FK)
- `mock_interview_score`, `internships_completed`
- `placement_status`, `company_name`, `placement_package`
- `interview_rounds_cleared`, `placement_date`

🔁 All tables are connected via `student_id` as a foreign key.

---

## ⚙️ Setup Instructions

### ▶️ Install Required Packages

```bash
pip install faker pandas
```

### ▶️ Generate Fake Data (in Jupyter)

Run the `generate_data.ipynb` notebook to:
- Create the database `placement_eligibility.db`
- Populate it with 100 synthetic student records

---

## 🧪 SQL Query Examples

### ✅ 1. Eligible Students Based on Thresholds

```sql
SELECT s.name, p.problems_solved, ss.communication, pl.mock_interview_score
FROM students s
JOIN programming p ON s.student_id = p.student_id
JOIN soft_skills ss ON s.student_id = ss.student_id
JOIN placements pl ON s.student_id = pl.student_id
WHERE p.problems_solved > 50
  AND ss.communication > 70
  AND pl.mock_interview_score > 60;
```

### ✅ 2. Top 5 Students by Placement Package

```sql
SELECT s.name, pl.company_name, pl.placement_package
FROM students s
JOIN placements pl ON s.student_id = pl.student_id
ORDER BY pl.placement_package DESC
LIMIT 5;
```

### ✅ 3. Average Problems Solved Per Batch

```sql
SELECT s.course_batch, AVG(p.problems_solved) AS avg_problems
FROM students s
JOIN programming p ON s.student_id = p.student_id
GROUP BY s.course_batch;
```

---

## 📊 Optional Streamlit Dashboard

If using Streamlit:

```bash
streamlit run app.py
```

The app allows you to:
- Input minimum thresholds (e.g., problems solved > 50)
- See filtered students in a table
- Visualize eligibility dynamically

---

## 📁 Project Structure

```
placement_eligibility/
├── generate_data.ipynb         # Data creation in Jupyter
├── placement_eligibility.db    # Generated SQLite DB
├── app.py                      # (Optional) Streamlit dashboard
├── queries.sql                 # SQL insight queries (optional)
└── README.md                   # Project documentation (this file)
```

---

## 📅 Timeline

| Week | Tasks |
|------|-------|
| Week 1 | Generate data using Faker, design schema, insert into SQLite |
| Week 2 | Write SQL queries, analyze insights, create dashboard, prepare docs |

---

## ✅ Evaluation Metric Checklist

| Metric           | Status   |
|------------------|----------|
| Functionality     | ✅ Filtering via SQL works |
| SQL Queries       | ✅ 5+ Insightful queries shown |
| OOP Implementation| ✅ Optional, modular code can be added |
| UI/UX             | ✅ Clean Jupyter/Streamlit output |
| Documentation     | ✅ README + PPT included |

---

## 👤 Author

**Jerwin Manuel**  
Dept. of Electronics and Computer, VIT University  
📧 jerwin.manuel2022@vitstudent.ac.in

---

## 📚 References

- [Faker Documentation](https://faker.readthedocs.io/)
- [Streamlit Documentation](https://docs.streamlit.io/)
- [SQLite Official Docs](https://www.sqlite.org/docs.html)
- [Project Guidelines](Project Orientation PDF provided by VIT)
