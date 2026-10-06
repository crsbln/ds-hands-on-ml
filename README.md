# Hands on Machine Learning

A hands-on introduction to core machine learning techniques. In the guided notebook you will scale features, tune hyperparameters, and compare models with cross-validation on Titanic data. In the exercise you apply the full workflow yourself: join a heart-related teaching dataset from a database, predict its binary label, and explain the limits of the evaluation. Finally, reload the saved Titanic pipeline, validate new inputs, and deliver predictions with an input-quality report.

## Learning Objectives

By the end of this repository, you should be able to:

- Follow the machine learning workflow from defining a goal to evaluating a model.
- Scale features with standardization and min-max scaling, and distinguish these from row normalization.
- Validate models reliably using K-fold cross-validation.
- Tune hyperparameters with grid search and randomized search.
- Fetch and join data from a SQL database to assemble a training set.
- Apply the full workflow end to end to build a classifier on a new problem.
- Save and reload a fitted pipeline, validate new inputs, and interpret batch predictions.

## Learning Path

> [!TIP]
> Start with the [**Machine Learning Workflow**](machine_learning_workflow.md) guide. It walks through every step of an ML project (define the goal, get the data, split, explore, model, evaluate) and gives you the map for what the notebooks practice.

The notebooks build on each other in order:

| File / Folder | Description |
|---|---|
| [**The Machine Learning Workflow**](machine_learning_workflow.md) | Step-by-step overview of an end-to-end ML project. Read this first. |
| [**1 - Scaling & Hyperparameter Tuning**](1_scaling_hyperparameter_tuning.ipynb) | Establish a majority-class baseline, compare unscaled and scaled models with the same CV folds, tune KNN, then evaluate once on test data. |
| [**2 - Exercise: Machine Learning**](2_exercise_machine_learning.ipynb) | Practice the workflow on data pulled from a database, with seven stages and expected results to guide your work. |
| [**3 - From Training to Predictions**](3_from_training_to_predictions.ipynb) | Reload the frozen Titanic pipeline, validate invented requests, predict by batch, investigate sensitivity, and prepare a handover. Includes six exercises. |

For notebook 3, run notebook 1 through **Export for Notebook 3** first.
The saved pipeline loads in a fresh kernel. Keep its configuration fixed;
the new invented requests have no true labels and cannot establish accuracy.

### Additional Folders and Files

| File / Folder | Description |
|---|---|
| [**Data**](data/) | Raw Titanic data, an invented prediction batch for notebook 3, and the older preprocessed CSV retained for reference only. |
| [**Assets**](assets/) | Images used in the notebooks and the workflow guide. |
| [**Solutions**](solutions/) | Reference solutions. |
| [**.env.example**](.env.example) | Template for the database credentials. Copy to `.env` and fill in your values. |
| [**pyproject.toml**](pyproject.toml) | Project configuration and dependencies. |
| [**uv.lock**](uv.lock) | Dependency lock file. |

The notebooks create a local, Git-ignored `artifacts/` directory for the saved
Titanic pipeline, metadata, prediction reports, and your model handover.
After completing the exercises, use the worked solutions for
[notebook 2](solutions/2_exercise_machine_learning.ipynb) and
[notebook 3](solutions/3_from_training_to_predictions.ipynb) to compare your choices.

## Setup

> [!NOTE]
> Throughout these steps, text in angle brackets like `<repo-name>` is a **placeholder**. Replace it including the `< >` brackets with your own value. For example, `cd <repo-name>` becomes `cd ds-hands-on-ml`.

### 1. Create the Repository from the Template

Click **Use this template** on GitHub.

When creating the repository:

- Set yourself as the **Owner**
- Choose a repository name
- Disable **Include all branches**
- Click **Create repository**

> [!IMPORTANT]
> If you are working in pairs or groups, only **one person** should complete this step.

---

### 2. Add Collaborators (Pairs/Groups Only)

If working with teammates:

1. Open the repository on GitHub
2. Go to **Settings → Collaborators**
3. Add your teammates as collaborators
4. Share the repository link with your team

Teammates should accept the invitation before continuing.

---

### 3. Clone the Repository

Copy the SSH URL from the **Code** button on GitHub, then run:

```bash
git clone <copied-ssh-url>
```

The copied SSH URL will look like `git@github.com:<your-username>/<repo-name>.git`.

---

### 4. Move into the Project Folder and Install Dependencies

This installs all dependencies and creates a virtual environment in (`.venv/`).

```bash
cd <repo-name>
uv sync
```

---

### 5. Set Up the Database Connection

Only notebook 2 and its solution require the shared PostgreSQL database.
Notebooks 1 and 3 use the included Titanic files. For notebook 2, ask
your coach for connection details and read access to the `heart` schema.
Copy the example file:

```bash
cp .env.example .env
```

Then open `.env` and fill in `DATABASE`, `USER_DB`, `PASSWORD`, `HOST`, and
`PORT` using the values from your coach. The notebooks build the connection
URL automatically; enter the password as-is, without URL encoding.
Existing `.env` files with a complete `DB_STRING` are also supported.
Do not copy credentials from an unrelated repository. If access is unavailable,
request a coach-approved dataset export; do not substitute real patient records.

The heart exercise uses a teaching database. Confirm source tags and target
coding with the coach; the column named `heart_attack` must not be interpreted
as calibrated future infarction risk.

> [!CAUTION]
> The `.env` file holds credentials and must never be committed. It is already listed in `.gitignore`. Only `.env.example`, with placeholders, belongs in the repo.

---

### 6. Open the Notebooks

> [!NOTE]
> Make sure you open VS Code from the project root so it automatically detects the environment created by `uv sync`.

Launch VS Code in the project root folder:

```bash
code .
```

Then open a notebook and select the Python environment created by `uv sync` as the kernel.

## References & Further Reading

- [**The Machine Learning Workflow**](machine_learning_workflow.md): The step-by-step guide in this repo, your starting point.
- [**Feature Engineering**](https://github.com/neuefische/ds-feature-engineering): Companion bootcamp repo to go deeper on feature engineering (imputation, encoding, binning, feature creation).
- [**Scikit-learn: Preprocessing data**](https://scikit-learn.org/stable/modules/preprocessing.html): Standardization, normalization, and other scaling methods.
- [**Scikit-learn: Cross-validation**](https://scikit-learn.org/stable/modules/cross_validation.html): Evaluating estimator performance and avoiding overfitting.
- [**Scikit-learn: Tuning hyperparameters**](https://scikit-learn.org/stable/modules/grid_search.html): Grid search, randomized search, and successive halving.
- [**Scikit-learn: Model persistence**](https://scikit-learn.org/stable/model_persistence.html): Saving and reloading fitted models and their environments.
