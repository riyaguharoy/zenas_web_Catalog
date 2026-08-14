# 👟 Zena's Amazing Athleisure Catalog

A simple Streamlit web app that connects to a Snowflake database and lets shoppers browse a sweatsuit catalog - pick a color/style from a dropdown and instantly see the product photo, price, available sizes, and an upsell suggestion pulled live from Snowflake.

Built as a proof of concept for **Snowflake Badge 4** (Streamlit + Snowflake integration).

---

## How it works

1. The app connects to Snowflake using credentials stored in Streamlit secrets.
2. It queries a `catalog_for_website` table to populate a dropdown of available colors/styles.
3. When a shopper selects an option, it runs a second query to fetch that product's image URL, price, size list, and upsell description.
4. The result - image, price, sizes, and upsell text - is displayed instantly on the page.

## Tech stack

- **Streamlit** - web app UI
- **Snowflake Connector for Python** - database connection and queries
- **pandas** - shaping query results into a usable list

## Project structure

```
.
├── streamlit_app.py     # the app: Snowflake connection, dropdown, product display
├── requirements.txt     # Python dependencies
└── .gitattributes
```

## Setup

1. Clone the repo:
   ```bash
   git clone https://github.com/riyaguharoy/zenas_web_Catalog.git
   cd zenas_web_Catalog
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Add your Snowflake credentials as Streamlit secrets. Create a file at `.streamlit/secrets.toml`:
   ```toml
   [snowflake]
   user = "YOUR_USERNAME"
   password = "YOUR_PASSWORD"
   account = "YOUR_ACCOUNT_IDENTIFIER"
   warehouse = "YOUR_WAREHOUSE"
   database = "YOUR_DATABASE"
   schema = "YOUR_SCHEMA"
   ```
   > ⚠️ Never commit `secrets.toml` to GitHub - add it to `.gitignore` to keep your credentials private.

4. Make sure a `catalog_for_website` table exists in your Snowflake schema with (at minimum) these columns: `color_or_style`, `direct_url`, `price`, `size_list`, `upsell_product_desc`.

5. Run the app:
   ```bash
   streamlit run streamlit_app.py
   ```

## Deployment

This app is a good fit for [Streamlit Community Cloud](https://streamlit.io/cloud) - connect this repo, add the same Snowflake credentials under the app's **Secrets** settings in the dashboard (instead of a local `secrets.toml`), and deploy.
