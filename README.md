# Bias in Generative AI for Loan Approval in Financial Evaluation

This repository contains the code required to reprdouce the findings of the master's thesis.

The collected and analyzed data can be found in the `data` folder.

Jupyter notebooks used for data preprocessing and analysis are available in the `notebooks` folder.
Descriptions of each notebook are provided in the Notebooks section below.

## Data

This directory is where inputs, intermediaries, and outputs are saved.

To generate new loan applications or candidate rankings, an active and funded API key is required for each respective model. For GPT models, set the `OPENAI_API_KEY` environment variable after registering with OpenAI. Similarly, access to other models requires setting the appropriate environment variables: `GOOGLE_API_KEY` for Gemini models, `ANTHROPIC_API_KEY` for Claude models, `DEEPSEEK_API_KEY` for DeepSeek models, and either `SWISSAI_API_KEY` or `OPENROUTER_API_KEY` for Llama models.

```
data

├── input
|       ├── age_groups.json
|       ├── civil_status_de.json
|       ├── civil_status_en.json
|       ├── top_mens_names.json
|       ├── top_surnames.json
|       └── top_womens_names.json
├── intermediary
│   ├── application_ranking
│   |    ├── claude-3-5-haiku-20241022
│   |    ├── deepseek-chat
│   |    ├── gemini-2.0-flash-lite
│   |    ├── gpt-4o-mini
│   |    └── meta-llama
│   ├── creditprofiles_to_rank_de_age.json
│   ├── creditprofiles_to_rank_de_civil_status.json
│   ├── creditprofiles_to_rank_de_gender.json
│   ├── creditprofiles_to_rank_de_nationality.json
│   ├── creditprofiles_to_rank_de.json
│   ├── creditprofiles_to_rank_en_age.json
│   ├── creditprofiles_to_rank_en_civil_status.json
│   ├── creditprofiles_to_rank_en_gender.json
│   ├── creditprofiles_to_rank_en_nationality.json
│   └── creditprofiles_to_rank_en.json
└── output
        ├── application_ranking_for_graphics.csv
        ├── graphics_bw_performance_ranking.csv
        ├── performance_ranking.csv
        └── top1_input_match_distribution_by_feature.xlsx
        └── top1_input_match_distribution.csv

```

Here's an explanation of some of the more important files.

| file                                         | description                                                                                                                                                                                                                                                                                       |
|:---------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `data/input/top_mens_names.json`             | Demographically-distinct names (see also `data/input/top_womens_names.json`, `data/input/top_surnames.json`, and `data/input/top_surnames.json`) gathered from [Bundesamt für Statistik](https://www.bfs.admin.ch/bfs/de/home/statistiken/bevoelkerung/geburten-todesfaelle/namen-schweiz.html) and [Forebears.io](https://forebears.io/).                                                                                                                                       |
| `data/intermediary/creditprofiles_to_rank_de.json`     | Equally-qualified loan application profiles see also (`data/intermediary/creditprofiles_to_rank_de_age.json`, `data/intermediary/creditprofiles_to_rank_de_civil_status.json`, `data/intermediary/creditprofiles_to_rank_de_gender.json`, `data/intermediary/creditprofiles_to_rank_de_nationality.json`, `data/intermediary/creditprofiles_to_rank_en.json`, `data/intermediary/creditprofiles_to_rank_en_age.json`, `data/intermediary/creditprofiles_to_rank_en_civil_status.json`, `data/intermediary/creditprofiles_to_rank_en_gender.json`, `data/intermediary/creditprofiles_to_rank_en_nationality.json`) generated from GPT-4o and edited. It also includes credit type descriptions used to evaluate each application. The profiles and credit descriptions are based on publicly available loan application forms from the following sources: [Migros Bank - Online Mortgage](https://www.migrosbank.ch/onlinemortgage?lang=de), [BMW Financial Services - Leasing](https://www.bmw.ch/de/topics/angebote-und-services/financial-services/bmw-leasing.html?utm_source=chatgpt.com#leasingpakete), [Migros Bank Credit Calculator](https://www.migrosbank.ch/de/privatpersonen/kredite/kreditrechner.html#calculator), [AMAG Leasing - Budget Calculator](https://www.amag-leasing.ch/de/leasingbudget.vehicle.html), [Cembra Money Bank - Credit Request](https://www3.cembra.ch/de/kredit/anfragen/kreditbetrag)                                                                                                                                                                    |
| `data/intermediary/application_ranking`           | Data from the loan application ranking experiment collected from multiple generative AI models, including Claude Haiku 3.5, DeepSeek-Chat, Gemini 2.0 Flash-Lite, GPT-4o-mini, Llama-3.3 70B-Instruct. Organized by model version > loan type > feature.                                                                                                                                                                           |
| `data/output/performance_ranking.csv`        | Aggregated results from application ranking experiment.                                                                                                                                                                                                                                                |

Shorthand is used to denote gender, where `M` represents male and `W` represents female. In the file `data/output/performance_ranking.csv`, intersectional demographic groups are indicated in the demo column using the format `{nationality}_{gender}`. For example, `Swiss_W` refers to Swiss women.

## Installation
### Python
Make sure you have Python 3.11+ installed.

Then install the Python packages:
```pip install -r requirements.txt```

## Notebooks

Jupyter notebooks to collect, process, and analyze data can be found in the `notebooks` directory.
Notebooks should be run sequentially, you can use the command `nbexec notebooks` to run all notebooks.

### 1-rank-credit-applicant-profiles.ipynb
Utilize the APIs of different models to rank 12 near-identical loan applications thousands of times, covering hundreds of names across four distinct credit types.

### 2-analysis-ranking-discrimination.ipynb
Analyze ranking experiment data to test for discrimination.
