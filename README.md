# Census and FEMA Risk Visualization
By Sam Jackowski  
  
This notebook loads processed Census ACS and FEMA county-level data and a U.S. counties GeoJSON file to create interactive maps and visualizations.


## Installation

Clone the repository:

```bash
git clone https://github.com/<username>/<repository>.git
cd <repository>
```

Create a virtual environment (recommended):

```bash
python -m venv venv
```

Activate it.

**Windows**

```bash
venv\Scripts\activate
```

**Mac/Linux**

```bash
source venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

or install manually:

```bash
pip install pandas numpy plotly pyarrow
```

---

## Updating the Project Directory

The notebook uses a variable called `PROJECT_DIR` to locate the data files.

You will likely need to change this line:

```python
PROJECT_DIR = Path(r"C:\SDSU_SCIL_CensusData")
```

Replace it with the location where **you saved the repository**.

### Example (Windows)

```python
PROJECT_DIR = Path(r"C:\Users\John\Documents\SDSU_SCIL_CensusData")
```

### Example (Mac)

```python
PROJECT_DIR = Path("/Users/john/Documents/SDSU_SCIL_CensusData")
```

### Example (Linux)

```python
PROJECT_DIR = Path("/home/john/SDSU_SCIL_CensusData")
```

---

## Verify the Paths

The notebook prints whether the required files are found:

```python
print("County panel exists:", COUNTY_PANEL_PATH.exists())
print("GeoJSON exists:", GEOJSON_PATH.exists())
```

If everything is configured correctly, the output should be:

```
County panel exists: True
GeoJSON exists: True
```

If either value is `False`, check:

- the repository location
- the `PROJECT_DIR`
- that the data files are in the expected folders

---

## Required Files

The notebook expects these files:

```
data/processed/acs_county_year_fema_risk.parquet
```

and

```
data/geo/us_counties_geojson.json
```

Do not rename these files unless you also update the corresponding file paths in the notebook.

---

## Running the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

or Jupyter Lab:

```bash
jupyter lab
```

Open the notebook and run the cells from top to bottom.

---

## Troubleshooting

### FileNotFoundError

This usually means `PROJECT_DIR` is pointing to the wrong location.

Double-check:

```python
PROJECT_DIR = Path("...")
```

### Missing Python Package

Install missing packages using:

```bash
pip install <package_name>
```

Example:

```bash
pip install plotly
```

### GeoJSON Not Found

Verify that:

```
data/geo/us_counties_geojson.json
```

exists.

### Parquet File Not Found

Verify that:

```
data/processed/acs_county_year_fema_risk.parquet
```

exists.

---

## Gemini API Setup

This project uses the Google Gemini API. Before running the notebook, you must create your own API key.

### 1. Create a Gemini API Key

Go to:

https://aistudio.google.com/app/apikey

Sign in with your Google account and generate a new API key.

---

### 2. Set the API Key as an Environment Variable

The notebook expects the API key to be stored as an environment variable named:

```
GEMINI_API_KEY
```

#### Windows (PowerShell)

```powershell
$env:GEMINI_API_KEY="YOUR_API_KEY"
```

#### Windows (Command Prompt)

```cmd
set GEMINI_API_KEY=YOUR_API_KEY
```

#### Mac/Linux

```bash
export GEMINI_API_KEY="YOUR_API_KEY"
```

---

### 3. Verify the Code

The notebook should contain:

```python
from google import genai
import os

gemini_client = genai.Client(
    api_key=os.getenv("GEMINI_API_KEY")
)
```

If you are not using an environment variable, you can replace it with your own API key:

```python
from google import genai

gemini_client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)
```


---

### 4. If You Receive an Authentication Error

Check that:

- Your Gemini API key is valid.
- The `GEMINI_API_KEY` environment variable is set correctly.
- You restarted Jupyter Notebook after setting the environment variable.
- You have installed the latest Google GenAI SDK:

```bash
pip install -U google-genai
```

Examples: 

<img width="1704" height="4080" alt="_C__SDSU_SCIL_CensusData_output_dashboard_median_age_tennessee_2024 html" src="https://github.com/user-attachments/assets/053a3fb6-8cff-436a-8f1e-509122c11afa" />

<img width="1704" height="4185" alt="USA_Income" src="https://github.com/user-attachments/assets/fd0fd034-0e02-4632-a23d-4aa9c6c6a9a3" />

<img width="1704" height="4185" alt="kansas_missouri" src="https://github.com/user-attachments/assets/46628af0-e09e-4206-b6d4-9c914e6ac38d" />

