# Internyl Program Discovery Agent

Internyl Website Repo: https://github.com/internyl-dev/internyl-frontend<br>
Internyl Data Acquisition Repo: https://github.com/internyl-dev/internyl-ai-wrapper/tree/refactor<br>
Internyl Website: https://internyl.org

## Table of Contents
1. [How to use](#how-to-use)
    - [Add API Keys](#add-api-keys)
    - [Run main](#run-main)
2. [How it works](#how-it-works)
    - [Models](#models)
    - [Tools](#tools)

## How to use
### Add API Keys
1. Navigate to .env and input any API keys you may have there

### Run main
```
# 1. Create a virtual environment
python -m venv .venv

# 2. Activate the virtual environment
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
.venv/scripts/activate

# 3. Install requirements
pip install -r requirements.txt
playwright install

# 4. Run run.py
python run.py
```

## How it works
The augmentor agent utilizes a LangChain agent execution chain to perform the agentic behavior. All it does is take a specific set of instructions, utilizing internet search APIs to populate missing information in a given schema.

### Prompt

```
src/
└── prompts/
    ├── assets/
    │   └── prompt.py
    └── prompt_create.py
```

The model query aims at prioritizing the following:
1. Following the schema exactly
    - Never adding new sections to the schema
    - Assuming the already added information is true
    - Completely follow the directions of the structure and where to put the necessary data
2. Completely populating all fields
    - Only inputting "not provided" if truly no information can be found
3. Accuracy
    - Don't infer information
4. Efficient search methods

### Tools

```
src/
└── tools/
    ├── content_scraper.py
    ├── ddgs_run.py
    └── links_scraper.py
```

**Search** - `search (search_term:str, max_results:int)`<br>
Using the DDGS search module, return the search results given a search term.<br><br>
**Visit URL** - `visit_url (url:str)`<br>
Using Playwright return the parsed webpage contents of a URL.<br><br>
**Get All Links** - `get_all_links (url:str)`<br>
Using Playwright return all URLs found within a webpage.
