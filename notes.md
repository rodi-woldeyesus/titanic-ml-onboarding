# Notes

## Environment Management

The existing `environment.yaml` file is quite complex because (1) it includes a bunch of OS-specific packages, (2) it uses `pip` (which doesn't always play nice with `conda`), and (3) it pins very specific version names. In general, you want to minimalize the `environment.yaml` file so that it will install nicely on other computers. (For example, I use [wsl2](https://learn.microsoft.com/en-us/windows/wsl/install) so my code is actually running on Linux even though I have a Windows machine.)

I looked through the notebooks to see what packages are actually needed, then created a new `environment.yaml` file with just the bare essentials. Here's what it looks like:

```yaml
name: titanic-ml
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.11
  - ipykernel
  - pandas
  - scikit-learn
  - catboost
```

Major changes:
1. Set `conda-forge` as the first channel (casts a wider net than the `defaults` channel)
2. No use of `pip`
3. No OS-specific dependencies
4. Nothing is pinned to a specific version (except Python itself)

Once I had this, I create the conda env on my system using: `conda env create -f environment.yaml`. I was then able to select `titanic-ml` as the kernel in VS Code and execute the notebooks.

Key takeaways:

1. When using `conda` in the future, install all packages that you can with `conda install...` and don't rely on `pip`.
2. When creating your `environment.yaml` file, use the command: `conda env export --from-history > environment.yaml`. This command generates a lean `environment.yaml` file by only including the packages that you explicitly installed with `conda install...`. It leaves all the dependencies alone and it doesn't pin specific versions.

## Notebook Structure

I recommend a specific structure for notebooks, which I've outlined below:

1. **Title** — a single H1 (`#`) in plain English. On the **next line**, the
   filename in italics, e.g. `_my_notebook.ipynb_`.
2. **`## Description`** — explain the goal of the notebook and anything a reader
   needs to understand it. Include links to external source data (where relevant)
   and explanations of non-standard algorithms/libraries.
3. **`## Imports`** — split into up to three separate cells, each led by a comment
   header, each **optional** (include only if non-empty):
   - `# System imports` (standard library)
   - `# Third-party imports`
   - `# Internal imports`
4. **`## Settings and Parameters`** — a cell for notebook-level constants, plus
   separate cells for library-wide settings grouped **one library per cell**
   (e.g. one pandas cell, one matplotlib cell). All optional.
5. **`## Functions`** — **optional**; include this section only if the notebook
   has ΓëÑ 1 function. Write **each function in its own cell**, with a docstring and
   type annotations.
6. **`## Execution`** — the main body. Group logic into distinct, logically
   separated cells. For long notebooks, use optional `### Execution Sub-Header`
   subheaders, which may carry explanatory text to guide the reader.
   - **Do not number** sub-headers (`1.`, `2.`, ΓÇª) ΓÇö ordering changes too often.
     Number them only in a final version expected to be read widely by others.
   - Interleave explanatory markdown cells where useful, including dedicated
     callouts for long-running cells or important findings/warnings.
7. **`## Conclusion`** — **optional**. Skip it when the logic is self-evident.
   Include it for training/knowledge-transfer notebooks, or when there's a special
   reason (e.g. links to downstream or related notebooks, notes on what happened
   with the analysis).

In addition, the notebook should be **reproducible** meaning that you should be able to run successful from top-to-bottom from a fresh kernel. To check this, do a Restart & Run All before the notebook is committed (as long as there aren't any cells that will run forever). 

## EDA (Exploratory Data Analysis)

One of the best uses of Jupyter notebooks is the in-line graphics (charts and such). Also, it's generally a good idea to always keep a separate Exploratory Data Analysis notebook in the repo. So I went ahead and created one for you, adhering to the Notebook Structure, and with some basic charts. 