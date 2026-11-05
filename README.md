# King County Housing EDA Project Template

This is the starter template for the Exploratory Data Analysis (EDA) project. You will work with the King County housing dataset (home sales in and around Seattle, USA), uncover what drives house prices, and turn your findings into insights and recommendations for a client you choose.

## Learning Objectives

By the end of this repository, you should be able to:

- Connect to a PostgreSQL database from Python and load query results into a pandas DataFrame.
- Frame an exploratory data analysis around clear research questions and hypotheses.
- Clean and wrangle a real-world dataset by handling missing values, outliers, and feature transformations.
- Explore distributions and the relationships between features and the target variable (price).
- Translate your analysis into at least three insights and three client-specific recommendations.
- Present your work to a non-technical audience.

## Learning Path

Work through the files in order. Start with the assignment to understand the goal, follow the workflow as your guide, fetch the data, then run your analysis in the EDA notebook.

> [!TIP]
> The data lives in the **eda** schema of the database and is split across two tables. Before fetching anything in code, connect with DBeaver and explore that schema: inspect both tables, check [**Column Names**](column_names.md) for what each field means, and work out how to join them. Once you have a working `JOIN`, use it as the query in [**03 - Fetching the Data**](03_fetching_the_data_eda.ipynb) to load the combined dataset into pandas.

| File / Folder                                                   | Description                                                                                                              |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| [**01 - Assignment**](01_assignment.md)                      | The project brief: the dataset, your tasks, deliverables, and the list of clients to choose from.                        |
| [**02 - Workflow**](02_workflow.md)                          | A recommended EDA workflow, from understanding and questioning the data through cleaning, relationships, and presenting. |
| [**03 - Fetching the Data**](03_fetching_the_data_eda.ipynb) | Connect to the PostgreSQL database with psycopg2 and SQLAlchemy, then pull the data into a pandas DataFrame.             |
| [**04 - EDA**](04_eda.ipynb)                                 | Starter notebook for your exploratory data analysis.                                                                     |
| [**Column Names**](column_names.md)                          | Data dictionary describing each column in the King County housing dataset.                                               |

### Additional Folders and Files

| File / Folder                           | Description                                                                                    |
| --------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [**Data**](data/)                    | Where you save the dataset CSV. The folder is tracked, but its data files are kept out of git. |
| [**.env.example**](.env.example)     | Template for the database credentials. Copy it to `.env` and fill in your values.            |
| [**pyproject.toml**](pyproject.toml) | Project configuration and dependencies.                                                        |
| [**uv.lock**](uv.lock)               | Dependency lock file.                                                                          |

## Setup

Use [uv](https://docs.astral.sh/uv/getting-started/installation/) 0.13.5 or newer
and Python 3.13.17 or a newer 3.13 patch release, as defined in
[`.python-version`](.python-version).

> [!NOTE]
> Throughout these steps, text in angle brackets like `<repo-name>` is a **placeholder**. Replace it, including the `< >` brackets, with your own value. For example, `cd <repo-name>` becomes `cd ds-eda-project-template`.

### 1. Create the Repository from the Template

Click **Use this template** on GitHub.

When creating the repository:

- Set yourself as the **Owner**
- Choose a repository name
- Disable **Include all branches**
- Click **Create repository**

> [!IMPORTANT]
> If you are working in pairs or groups, only **one person** should complete this step.
---

### 2. Add Collaborators (Pairs/Groups Only)

If working with teammates:

1. Open the repository on GitHub
2. Go to **Settings → Collaborators**
3. Add your teammates as collaborators
4. Share the repository link with your team

Teammates should accept the invitation before continuing.

---

### 3. Clone the Repository

Copy the SSH URL from the **Code** button on GitHub, then run:

```bash
git clone <copied-ssh-url>
```

The copied SSH URL will look like `git@github.com:<your-username>/<repo-name>.git`.

---

### 4. Move into the Project Folder and Install Dependencies

This installs all dependencies and creates a virtual environment in `.venv/`.

```bash
cd <repo-name>
uv sync
```

> [!TIP]
> Need a library that is not installed yet (for example a mapping)? Add it with `uv add <package-name>`. This updates `pyproject.toml` and `uv.lock` and installs it into your `.venv`. Commit both files; teammates then run uv sync after pulling to get the same environment.

---

### 5. Set up your Database Credentials

The data-fetching notebook reads the database connection details from a `.env` file. Copy the template and fill in your own values:

```bash
cp .env.example .env
```

Open `.env` and replace the placeholders with the credentials for the King County housing database (the same ones you use in DBeaver). These values feed [**03 - Fetching the Data**](03_fetching_the_data_eda.ipynb).

> [!CAUTION]
> `.env` holds secrets and must never be committed. It is already listed in `.gitignore`. Only `.env.example`, with placeholder values, belongs in the repository.

---

### 6. Open the Notebooks

> [!NOTE]
> Make sure you open VS Code from the project root so it automatically detects the environment created by uv sync.

Launch VS Code in the project root folder:

```bash
code .
```

Then open a notebook and select the Python environment created by `uv sync` as the kernel.

## References & Further Reading

- [**House Sales in King County dataset**](https://www.kaggle.com/datasets/harlfoxem/housesalesprediction): The source dataset, with column descriptions and community notebooks.
- [**Pandas user guide**](https://pandas.pydata.org/docs/user_guide/index.html): The official guide to data manipulation with pandas.
- [**Seaborn tutorial**](https://seaborn.pydata.org/tutorial.html): Statistical data visualization in Python.
- [**SQLAlchemy documentation**](https://docs.sqlalchemy.org/en/20/): The database toolkit used to query PostgreSQL from Python.
- [**Hypothesis generation for EDA**](https://www.analyticsvidhya.com/blog/2020/11/an-efficient-way-of-performing-eda-hypothesis-generation/): How to form research questions and hypotheses before diving into the data.
- [**EDA Checklist**](https://github.com/neuefische/datascience-infographics/blob/main/EDA_Checklist.md): A phase-by-phase checklist for working through an exploratory analysis.
- [**Detailed EDA with Python**](https://www.kaggle.com/code/ekami66/detailed-exploratory-data-analysis-with-python): A worked example of a thorough EDA notebook on real data.
- [**Tips for data science presentations**](https://www.dataknowsall.com/storytelling.html): Storytelling techniques for presenting results to a non-technical audience.

*****
# King County Housing — Exploratory Data Analysis (EDA)

An exploratory data analysis of the King County housing dataset (Seattle and surrounding areas, May 2014 – May 2015), tailored to provide data-driven buying strategies and real estate recommendations for our target client persona.

---

## Team Members
* **Parand Khajehpour**
* **Rabih**
* **Gülşah Bayhan Ara**

---

## Client Persona: Thomas Hansen
* **Profile & Goal:** Thomas is looking for a home in King County for a large family of seven (himself, his wife, and five children).
* **Budget Constraint:** Strictly limited budget between **$200k – $250k**.
* **Key Preferences:** Needs sufficient living space (ideally 3+ bedrooms), prioritizes a dense and social neighborhood for his kids, and is open to older or lower-grade properties requiring cosmetic updates.

---

## Hypotheses & Key Findings

### H1: Bedroom Count & Price Reality (5–6 vs. 3–4 Bedrooms)
* **Hypothesis:** A large family home with 5–6 bedrooms is within reach under a $250k budget.
* **Finding:** **Rejected.** County-wide median prices for 5–6 bedroom properties average **$637k** (32% higher than 3–4 bedroom homes at **$482k**). In the sub-$250k market segment, only ~50 homes have 5+ bedrooms.
* **Takeaway:** Thomas must adjust his target to **3–4 bedroom properties**, where market inventory is significantly higher (~1,500 options under $250k).

### H2: Location, Social Neighborhood & Quality Trade-Offs
* **Hypothesis:** Certain zip codes offer an optimal balance of affordable 3+ bedroom listings, high community density (Social Score), and acceptable build quality.
* **Finding:** **Confirmed.** When filtering for 3+ bedroom homes priced between $200k and $250k, listings cluster heavily in specific suburban areas. Social scores and building conditions show no drastic deviations across the top hubs.
* **Recommended Zip Codes:**
  1. **98023:** 132 listings | Median Price: $230k | Social Score: 62.5 | Condition: 3.49 / Grade: 7.10
  2. **98042:** 105 listings | Median Price: $225k | Social Score: 64.3 | Condition: 3.81 / Grade: 6.81
  3. **98001:** 96 listings | Median Price: $224k | Social Score: 59.9 | Condition: 3.50 / Grade: 6.96

### H3: Timing & Seasonality Analysis
* **Hypothesis:** Buying in the winter months (Dec–Feb) offers a 5–8% price discount compared to the peak summer season (May–Jul).
* **Finding:** **Confirmed.** The peak season median price is **$465,000**, dropping to **$430,000** during winter, with an annual low of **$426,000** in February.
* **Result:** A statistically verified **7.5% price reduction**, translating to approximately **$15,000 – $18,000 in direct capital savings** for Thomas's budget tier.
* **Visual Integrity:** Visualized using an honest zero-based Y-axis to prevent artificial slope exaggeration and preserve objective data reporting.

---

## Actionable Recommendations for Thomas Hansen

1. **Target 3–4 Bedrooms:** Focus searches on 3–4 bedroom configurations to maximize available inventory while remaining within budget.
2. **Focus on Top 3 Zip Codes:** Prioritize properties in **98023**, **98042**, and **98001** for the highest supply and favorable lot-density metrics.
3. **Time the Purchase in Winter:** Enter negotiations and submit offers between **December and February** to capture the ~7.5% seasonal discount.
4. **Accept Necessary Trade-Offs:** Target homes built between 1960–1980 with construction grades 6–7; allocate seasonal savings toward essential cosmetic repairs and moving costs.

---

## Data Limitations

* **Single-Year Horizon:** Dataset covers sales only from May 2014 to May 2015; true multi-year seasonality cannot be completely decoupled from annual macro trends.
* **Inventory Constraints:** While winter provides favorable pricing, overall market listings decline during colder months, limiting total simultaneous choices.
* **Proxy Metrics:** "Social neighborhood" is estimated using neighborhood lot sizes (`sqft_lot15`) due to the absence of public transit, school district, and crime rate features in the dataset.

---

## Repository Structure

```text
├── 04_eda.ipynb                     # Master notebook combining data prep, H1, H2, and H3
├── 08_H1.ipynb                      # Hypothesis 1: Bedroom distributions and pricing
├── 08_H2.ipynb                      # Hypothesis 2: Geographic filtering, zip code selection, and social scores
├── 08_H3.ipynb                      # Hypothesis 3: Seasonality, timing analysis, and zero-based visual
├── cleandataset.csv                 # Cleaned King County dataset
├── pyproject.toml / uv.lock         # Project dependencies managed via uv
└── README.md                        # Project documentation and summary
