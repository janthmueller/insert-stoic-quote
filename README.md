# Insert Stoic Quote GitHub Action

[![GitHub Actions](https://github.com/janthmueller/insert-stoic-quote/actions/workflows/test.yml/badge.svg)](https://github.com/janthmueller/insert-stoic-quote/actions)

A GitHub Action to insert daily or random Stoic quotes into your markdown files using the [Kathekon](https://github.com/janthmueller/kathekon) Python CLI.

---

## Features

- Inserts **daily** or **random** Stoic quotes into any markdown file.
- Supports filtering by author.
- Supports multiple interpretation methods (`db`, `gpt`, `db+fixed`, `gpt+fallback`).

---

## Usage

To specify where the quote should be inserted in your file, add the following comment flags:

```markdown
<!--START_SECTION:quote-text-->
<!--END_SECTION:quote-text-->

<!--START_SECTION:quote-author-->
<!--END_SECTION:quote-author-->

<!--START_SECTION:quote-interpretation-->
<!--END_SECTION:quote-interpretation-->
```

The action will replace the content between these flags with the new quote.

Create or update your GitHub workflow `.github/workflows/update-quote.yml` like this:

```yaml
name: Update Stoic Quote

on:
  schedule:
    - cron: "0 0 * * *"  # daily at midnight
  workflow_dispatch:

jobs:
  update-readme:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v3

      - name: Insert Stoic Quote into README
        uses: janthmueller/insert-stoic-quote@v1
        with:
          type: "daily"                   # 'daily' or 'random'
          file: "README.md"               # file to update
          author: "Marcus Aurelius"      # optional: filter by author
          method: "gpt+fallback"         # optional: interpretation method
          openai_api_key: ${{ secrets.OPENAI_API_KEY }} # optional for GPT methods
```

---

## Inputs

| Name             | Description                                                               | Default     |
| ---------------- | ------------------------------------------------------------------------- | ----------- |
| `type`           | `'daily'` or `'random'` to select quote type                              | `daily`     |
| `file`           | File path to insert the quote into                                        | `README.md` |
| `author`         | (Optional) Filter quotes by author                                        | -           |
| `method`         | (Optional) Interpretation method: `db`, `gpt`, `db+fixed`, `gpt+fallback`.<br>Default: `db+fixed` for `daily`, `db` for `random`. | -           |
| `openai_api_key` | (Optional) OpenAI API key, needed for GPT interpretation                  | -           |

---

## License

MIT License © Jan Müller

---

## About Kathekon

This action uses the [Kathekon](https://github.com/janthmueller/kathekon) Python package to fetch and insert Stoic quotes.

---

## Contributing

Contributions and suggestions are welcome! Please open an issue or pull request.