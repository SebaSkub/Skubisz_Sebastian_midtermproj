# Association Rule Mining – Midterm Project  
**Author:** Sebastian Skubisz  

---

## 1) Folder Layout
```
skubisz_sebastian_midtermproject/
│
├─ datasets/                              # input CSV files
│   ├─ amazon.csv
│   ├─ microcenter.csv
│   ├─ traderjoes.csv
│   ├─ target.csv
│   └─ stewleonards.csv
│
├─ outputs/                               # algorithm results
│   └─ <dataset>/
│       ├─ Brute-Force/
│       │  ├─ frequent_itemsets.csv
│       │  └─ association_rules.csv
│       ├─ Apriori/
│       │  ├─ frequent_itemsets.csv
│       │  └─ association_rules.csv
│       ├─ FP-Growth/
│       │  ├─ frequent_itemsets.csv
│       │  └─ association_rules.csv
│       └─ timings.csv
│
├─ algApp.py                              # main script
├─ README.md                              # this file
└─ requirements.txt                       # dependencies
```

### Why this layout?  
All datasets live under `datasets/`. Running `algApp.py` generates algorithm-specific results inside `outputs/<dataset>/…`, keeping everything organized.

---

## 2) Datasets (Input Format)
All five CSVs live in `datasets/` and must follow this simple structure:

| Column | Type | Description |
|--------|------|-------------|
| Transaction ID | string | *(Optional)* identifier for each transaction |
| Transaction | string | Comma-separated list of item names (e.g., `Milk, Bread, Eggs`) |

The script automatically detects whether the file uses commas, semicolons, or pipes (`|`) as separators.

---

## 3) Environment Setup
Use **Python 3.9–3.12**

### 🪟 Windows PowerShell
```bash
python -m venv .venv
.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

### 🐧 macOS/Linux
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

### requirements.txt
```
pandas
tabulate
mlxtend
```

---

## 4) How to Run (CLI)

Run the main script interactively from the project root:
```bash
python algApp.py
```

You will be prompted to:

1. Choose a dataset (`amazon`, `microcenter`, `traderjoes`, `target`, or `stewleonards`)
2. Enter **Minimum Support** (0–1 or 1–100)
3. Enter **Minimum Confidence** (0–1 or 1–100)

### Example Session
```
Choose a dataset:
  1. Amazon
  2. Microcenter
  3. Traderjoes
  4. Target
  5. Stewleonards
Enter number (1–5): 3
Minimum support (1–100 or 0..1) [20]: 40
Minimum confidence (1–100 or 0..1) [50]: 60
```

The script will:

- Run **Brute-Force**, **Apriori**, and **FP-Growth**
- Print frequent itemsets and rules in the terminal
- Save all results under `outputs/<dataset>/...`

---

## 5) Example Output
```
===== Microcenter =====
Loaded 10 transactions, 6 unique items.
Min Support 40% (>= 4/10), Min Confidence 60%

| Antecedent(s) | Consequent(s) | Support | Confidence |
|---------------|----------------|----------|-------------|
| Computer, TV  | Cable          | 0.40     | 0.80        |
...
Timing Summary:
| Algorithm    | Frequent Itemsets | Rules | Time (s) |
|--------------|-------------------|-------|-----------|
| Brute-Force  | 15                | 12    | 0.63      |
| Apriori      | 15                | 12    | 0.02      |
| FP-Growth    | 15                | 12    | 0.01      |
```

---

## 6) Output Structure
All results are automatically saved to:
```
outputs/<dataset>/
├─ Brute-Force/
│  ├─ frequent_itemsets.csv
│  └─ association_rules.csv
├─ Apriori/
│  ├─ frequent_itemsets.csv
│  └─ association_rules.csv
├─ FP-Growth/
│  ├─ frequent_itemsets.csv
│  └─ association_rules.csv
└─ timings.csv
```

---

## 7) Defensive Validation
- Detects missing or invalid datasets  
- Re-prompts if support/confidence ≤ 0  
- Auto-installs missing Python packages if needed  
- Handles multiple CSV structures and separators gracefully  

---

## 8) Key Concepts (Summary)
### Frequent Itemset Mining
Finds groups of items frequently bought together.  

### Association Rules
Derives relationships such as `{Milk, Bread} → {Butter}`.

| Algorithm | Description | Efficiency |
|------------|-------------|-------------|
| **Brute-Force** | Checks every possible item combination | Slowest (baseline) |
| **Apriori** | Uses pruning and level-wise search | Moderate |
| **FP-Growth** | Uses FP-tree for pattern compression | Fastest |

---

**End of README**
