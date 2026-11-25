# Humanoid Robots Database

An open dataset of humanoid robot models from manufacturers worldwide: manufacturer, country, height, mass, payload, degrees of freedom, speed, runtime, launch year, status, the source of the specification and links to the model pages in up to 54 languages.

Maintained by [MERA Robotics](https://merarobotics.com), a technology company from Warsaw, Poland. Licence: [CC BY 4.0](LICENSE). Please credit **"MERA Robotics, merarobotics.com"** and link to the [humanoid catalogue](https://merarobotics.com/blog/humanoids).

This describes the market. It is not a MERA offer or stock. The dataset contains **no prices** and **no manufacturer photos**. Specifications come from manufacturer pages and may change: confirm them with the manufacturer before you buy.

## Files

| File | What it is |
| --- | --- |
| [`data/humanoids.json`](data/humanoids.json) | The whole dataset: a `meta` block (licence, attribution, field descriptions) and a `models` array |
| [`data/humanoids.csv`](data/humanoids.csv) | The same models as one table (UTF-8, RFC 4180, empty cell = no value), with one `url_<language code>` column per language |
| [`data/robots.json`](data/robots.json) | All robot categories in one dataset (humanoid robots and quadruped robots, more categories as they are added): the humanoid fields plus `category`, `length_cm`, `width_cm`, `ip_rating` and `use` |
| [`data/robots.csv`](data/robots.csv) | The same as one table, with a `category` column and uses separated by semicolons |
| [`CITATION.cff`](CITATION.cff) | Citation metadata (GitHub shows a "Cite this repository" button) |
| [`huggingface/README.md`](huggingface/README.md) | Dataset card for Hugging Face |
| [`kaggle/dataset-metadata.json`](kaggle/dataset-metadata.json) | Metadata for Kaggle |

The files here are copied automatically from the production site by a [GitHub Action](.github/workflows/update-data.yml) once a day. The live versions are:

- JSON: <https://merarobotics.com/data/humanoids.json>
- CSV: <https://merarobotics.com/data/humanoids.csv>
- All categories, JSON: <https://merarobotics.com/data/robots.json>
- All categories, CSV: <https://merarobotics.com/data/robots.csv>
- Quadruped robot catalogue: <https://merarobotics.com/blog/quadrupeds>
- Data page in 54 languages: <https://merarobotics.com/en/data/>

## Fields

| Field | Meaning |
| --- | --- |
| `id` | Stable slug, also the last segment of the model page address |
| `name`, `manufacturer`, `model` | Display name, manufacturer, model name |
| `country`, `country_name` | ISO 3166-1 alpha-2 code and English name of the manufacturer country; `null` when not established |
| `status` | `shipping`, `preorder`, `research`, `in-development`, `unconfirmed` or `obsolete`; `status_label` is the English label |
| `release_year` | Year of the first public presentation or launch |
| `height_cm`, `weight_kg`, `payload_kg` | Height, mass and payload as stated by the manufacturer |
| `dof` | Degrees of freedom as stated by the manufacturer (configurations differ) |
| `speed_ms`, `runtime_h` | Speed in metres per second and battery runtime in hours |
| `manufacturer_url` | Manufacturer page of the model |
| `source` | Page the specifications were taken from |
| `verified` | Date (YYYY-MM-DD) of the last review of the entry by MERA Robotics |
| `pages` | Language code to the address of the model page on merarobotics.com, only for languages where the page exists (Polish and English for every model) |

Where the sources give no value, the field is `null` in JSON and empty in CSV. Nothing is guessed.

## Free API

No key, no registration, CORS open to all origins, `Cache-Control` and `ETag` set.

```bash
# list with filters (manufacturer, country, status, q, release_year, sort, fields, limit, offset, lang)
curl "https://merarobotics.com/api/humanoids?manufacturer=Unitree&lang=de"

# one model with its page addresses in every language
curl "https://merarobotics.com/api/humanoids/unitree-g1"

# all categories (category: humanoid or quadruped; also use, e.g. inspection)
curl "https://merarobotics.com/api/robots?category=quadruped&use=inspection"
curl "https://merarobotics.com/api/robots/boston-dynamics-spot"
```

The API is described in [OpenAPI 3.1](https://merarobotics.com/.well-known/openapi.json). The same data is available to AI assistants through the MERA Robotics MCP server (`https://merarobotics.com/mcp`, tools `search_humanoid_database` and `get_humanoid_model`, and for all categories `search_robot_database` and `get_robot_model`).

## Use the data

```python
import pandas as pd

df = pd.read_csv("https://raw.githubusercontent.com/ma1orek/humanoid-robots-database/main/data/humanoids.csv")
print(df[df.status == "shipping"][["name", "manufacturer", "height_cm", "weight_kg", "dof"]].head())
```

```js
const { meta, models } = await (await fetch("https://merarobotics.com/data/humanoids.json")).json();
console.log(meta.license, models.length);
```

## How to cite

> MERA Robotics (2026). Humanoid Robots Database. https://merarobotics.com/en/data/ (CC BY 4.0)

```bibtex
@misc{mera_humanoid_robots_database,
  author       = {{MERA Robotics}},
  title        = {Humanoid Robots Database},
  year         = {2026},
  url          = {https://merarobotics.com/en/data/},
  howpublished = {\url{https://github.com/ma1orek/humanoid-robots-database}},
  note         = {CC BY 4.0. Source: MERA Robotics, merarobotics.com}
}
```

## Found a mistake?

Write to contact@merarobotics.com with the model id and the correct value with its source. Corrections are made in the MERA Robotics catalogue and reach this repository with the next daily update.
