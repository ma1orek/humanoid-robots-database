---
license: cc-by-4.0
pretty_name: Humanoid Robots Database
language:
  - en
tags:
  - robotics
  - humanoid-robots
  - robot-specifications
  - tabular
  - open-data
size_categories:
  - n<1K
configs:
  - config_name: default
    data_files:
      - split: train
        path: data/humanoids.csv
---

# Humanoid Robots Database

An open dataset of humanoid robot models from manufacturers worldwide, maintained by [MERA Robotics](https://merarobotics.com) (Warsaw, Poland).

Each row is one model: manufacturer, country, height, mass, payload, degrees of freedom, speed, runtime, launch year, status, the source of the specification, the date the entry was last reviewed and the address of the model page on merarobotics.com in each of up to 54 languages (`url_<language code>` columns).

## Dataset details

- **Curated by:** MERA Robotics
- **Language of labels:** English (model pages exist in up to 54 languages)
- **License:** CC BY 4.0. Credit "MERA Robotics, merarobotics.com" and link to https://merarobotics.com/blog/humanoids
- **Source of truth:** https://merarobotics.com/data/humanoids.json (JSON) and https://merarobotics.com/data/humanoids.csv (CSV); GitHub copy: https://github.com/ma1orek/humanoid-robots-database
- **Free API:** https://merarobotics.com/api/humanoids (no key, CORS open), described in OpenAPI 3.1 at https://merarobotics.com/.well-known/openapi.json

## Columns

`id`, `name`, `manufacturer`, `model`, `country` (ISO 3166-1 alpha-2), `country_name`, `status` (`shipping`, `preorder`, `research`, `in-development`, `unconfirmed`, `obsolete`), `status_label`, `release_year`, `height_cm`, `weight_kg`, `payload_kg`, `dof` (degrees of freedom), `speed_ms`, `runtime_h`, `manufacturer_url`, `source`, `verified` (date of the last review), and one `url_<language code>` column per language (empty where the model page does not exist in that language).

## Quality and limits

- An empty cell means the sources give no value. Nothing is guessed.
- The dataset describes the market, not MERA stock. It has no prices and no manufacturer photos.
- Specifications come from manufacturer pages and may change. Confirm them with the manufacturer before you buy.
- Degrees of freedom, payload and runtime depend on the configuration of the robot and are given as the manufacturer states them.

## Load it

```python
from datasets import load_dataset

ds = load_dataset("csv", data_files="https://merarobotics.com/data/humanoids.csv")["train"]
print(ds[0]["name"], ds[0]["height_cm"])
```

## Citation

MERA Robotics (2026). Humanoid Robots Database. https://merarobotics.com/en/data/ (CC BY 4.0)
