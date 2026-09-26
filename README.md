# tnymayaro.github.io

This repository is the source for my personal website, built with Quarto.
It includes a blog with two reproducible, computational posts: one written
in Python, one written in R, alongside static pages from earlier milestones.

## Requirements

Install these before building:

- [Quarto](https://quarto.org/docs/get-started/) — version 1.10.18 or later
- [uv](https://docs.astral.sh/uv/getting-started/installation/) — version 0.12.5 or later
- [R](https://cran.r-project.org/) — version 4.6.1 or later

`renv` bootstraps itself automatically on first render and does not need
to be installed separately.

No network access is required at render time. All data used by the two
computational posts is bundled with the R and Python packages installed
below.

## Build instructions

Run the following from a terminal, starting at the top level of the
cloned repository.

### 1. Clone the repository

```bash
git clone git@github.com:tnymayaro/tnymayaro.github.io.git
cd tnymayaro.github.io
```

### 2. Restore the Python environment

```bash
uv sync
```

This reads `pyproject.toml` and `uv.lock` and creates a `.venv/` with the
exact package versions used to build this site.

### 3. Restore the R environment

From the same terminal, at the top level of the repository, start R:

​```bash
R
​```

This opens an interactive R session. Confirm you're in the right place with:

​```r
getwd()
​```

It should print the path to the cloned repository. If it does not, quit R
(`q()`, choosing not to save the workspace) and `cd` into the repository
root before starting R again.

Then restore the environment:

​```r
renv::restore()
​```

This reads `renv.lock` and installs the exact package versions used to
build this site into a project-local library. Confirm at the prompt if
asked to proceed.

When it finishes, quit R:

​```r
q()
​```

Choose not to save the workspace when prompted.

### 4. Render the site

Back in the terminal, from the top level of the repository:

```bash
uv run quarto render
```

`uv run` ensures Quarto uses this project's Python environment for the
Python post. R's `renv` environment activates automatically via
`.Rprofile` whenever R is started from this directory, so no separate
wrapper is needed for the R post.

### 5. View the built site

The rendered site is written to the `docs/` folder. Open it locally with:

```bash
quarto preview
```

This starts a local server and opens the site in your default browser,
auto-reloading on changes. Alternatively, open `docs/index.html` directly
in a browser.

## Data sources

- **Python post** (`posts/gapminder-outliers/`): uses the Gapminder
  dataset bundled with `plotly.express` (`px.data.gapminder()`),
  installed via `uv sync`. Original data from the
  [Gapminder Foundation](https://www.gapminder.org/data/), released
  under CC0.
- **R post** (`posts/gapminder-life-gains/`): uses the
  [`gapminder` R package](https://cran.r-project.org/package=gapminder)
  by Jennifer Bryan, installed via `renv::restore()`. Also sourced from
  the [Gapminder Foundation](https://www.gapminder.org/data/), CC0.

Both datasets are installed as part of the package dependencies above;
no separate download step or network access is required at render time.

## Verifying this README

These instructions were tested by cloning into a separate, empty
directory and following the steps above without modification:

