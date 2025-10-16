# Python RAP Template

[![Build Status](https://github.com/ONS-Innovation/python-rap-template/actions/workflows/ci.yml/badge.svg)](https://github.com/ONS-Innovation/python-rap-template/actions/workflows/ci.yml)
[![License - MIT](https://img.shields.io/badge/licence%20-MIT-1ac403.svg)](https://github.com/ONS-Innovation/python-rap-template/blob/main/LICENSE)

This repository serves as a template for creating Reproducible Analytical Pipeline (RAP) Python projects, complete with fundamental tooling, CI/CD integration, and policy compliance. It is designed to help RAP developers and data engineers get started quickly with standardised tooling, letting them focus on writing analytical code. The template takes care of directory structures, tool configurations, automated testing, and compliance requirements.

This template is generated using [Copier](https://github.com/copier-org/copier), an open source tool for rendering
project from templates and natively supports updating projects as the original template matures.

See this [demo repository](https://github.com/ONSdigital/ons-python-template-demo) for an example created from this
template.

## Table of Contents

[//]: # (:TODO: Enable link checking once https://github.com/tcort/markdown-link-check/issues/250 is resolved.)
<!-- markdown-link-check-disable -->

- [Features](#features)
- [Getting Started](#getting-started)
    - [Using GitHub Template Feature](#using-github-template-feature)
    - [Using Copier Locally](#using-copier-locally)
    - [Post-Clone Steps](#post-clone-steps)
- [Updating Project with Template Changes][updating-project]
- [Structure](#structure)
- [Design Decisions](#design-decisions)
- [Alternatives Software/Tools][alternative-software-tools]
- [Future Plans](#future-plans)
- [Contributing](#contributing)
- [License](#license)

<!-- markdown-link-check-enable -->

## Features

This template includes comprehensive features to help you get started developing RAP Python projects quickly:

### 🐍 **Python 3.12+ with Poetry**
- Modern Python with [Poetry](https://python-poetry.org/) for dependency management
- Standardised on Poetry only for consistency across ONS projects
- Lockfile support for reproducible builds

### 🔧 **Sample RAP Code Structure**
- Modular ETL pipeline components (extract, transform, load)
- Example data processing workflows
- Comprehensive logging and error handling
- Configurable data transformation rules

### 🎯 **Code Quality & Testing**
- [Ruff](https://github.com/astral-sh/ruff) for fast linting and formatting
- [MyPy](https://mypy.readthedocs.io/) for static type checking
- [pytest](https://docs.pytest.org/en/stable/) with coverage reporting
- Pre-commit hooks for automated quality checks

### 🔒 **Security & Compliance**
- [Bandit](https://bandit.readthedocs.io/en/latest/) security scanning
- Secret detection with detect-secrets
- Enhanced .gitignore with security patterns
- **Full ONS Policy Compliance**:
  - GitHub Usage Policy compliance
  - Software Coding Policy adherence
  - Software Development Guidelines alignment

### 🚀 **CI/CD & Development**
- Comprehensive GitHub Actions workflows
- VS Code devcontainer with recommended extensions
- Automated testing, linting, security scanning, and type checking
- Branch protection and code review requirements

### 📚 **Documentation & Standards**
- Architectural Decision Records (ADRs) for significant choices
- Comprehensive documentation templates
- British spelling and ONS standards
- govcookiecutter alignment

## Getting Started

You have two options for project generation from this template:

- **GitHub Template Feature**: Utilise
  the [Use this template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)
  feature on GitHub to create a new repository based on this template directly from the web interface. While convenient
  and fast, this method offers limited customisation options compared to local generation.
- **Running Copier Locally**: Use Copier locally to tailor the template to your specific requirements. This method
  allows for further customisation according to your project's needs and automatically set up the repository and branch
  protection.

### Using GitHub Template Feature

> [!NOTE]
> **DO NOT FORK** this repository. Instead, use the
> **[Use this template](https://github.com/ONS-Innovation/ons-python-template-simple/generate)** feature.

To get started:

1. Click on **[Use this template](https://github.com/ONS-Innovation/ons-python-template-simple/generate)**
2. Name your new repository and provide a description, then click **Create repository**. *Note: the repository name
   should be lowercase and use hyphens (`-`) instead of underscores.*
3. GitHub will now copy the contents over and GitHub Actions will process the template and commit to your new repository
   shortly after you click **Create repository**.
4. **Wait until the "Rename Project from Template" job in GitHub Actions finished running!**
5. Once the **Rename Project from Template** action has run, you can clone your new repository and start working on your
   project. :rocket:

#### Known Limitations

- Some GitHub Actions workflows will fail on the first run post-clone since the repository will not be fully
  configured until the "Rename Project from Template" job has finished running. This is expected behaviour and can be
  safely ignored. Subsequent runs will not have this issue.

### Using Copier Locally

#### Prerequisites

1. **Python 3.10+**: We recommend using [pyenv](https://github.com/pyenv/pyenv) for managing Python versions.
2. **[Pip](https://pip.pypa.io/en/stable/installation/) or [Pipx](https://pipx.pypa.io/stable/)**
3. **[Copier](https://github.com/copier-org/copier)**: Install Copier using pip or pipx.

   ```bash
   pip install --user copier
   # OR
   # Install pipx and add it to your PATH and then install Copier
   pip install --user pipx && pipx ensurepath
   pipx install copier
   ```

4. **Operation System**: Ubuntu/MacOS
5. **[Git](https://git-scm.com/)**: Ensure Git is installed and configured.
6. **[GitHub CLI](https://cli.github.com/)**: [OPTIONAL] Ensure GitHub CLI is installed and you are
   authenticated (`gh auth login`) if you would like to automate the repository creation and configuration like branch
   protection.

#### Generate Project from Template

Copier will ask you a series of questions to customise the project to your needs. Once you have answered all the
questions, Copier will generate the project for you.

To generate the project run:

```bash
copier copy --trust gh:ONS-Innovation/python-rap-template /path/to/your/new/project
```

Replace `/path/to/your/new/project` with the path to the directory where you want to create your new project. This
directory should match the name of the repository you want to create.

#### Initialising a Git Repository and Pushing to GitHub

**This step is only required if you answered `No` to the `Do you want to set up the git repository?` question.
Otherwise, this would
have been automatically done for you.**

1. Go to your project directory, and initialise a git repository and make the initial commit

   ```bash
   cd /path/to/your/new/project
   git init -b main
   git add .
   git commit -m "Initial commit"
   ```

2. Create a new repo in GitHub.
   See [GitHub How-to](<https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories>]

3. Push your project to the repository on GitHub:

   ```bash
   git remote add origin https://github.com/<repository_owner>/<repository_name>.git
   git push -u origin main
   ```

Now you can start working on your project. :rocket:

To update your project when the template changes,
see [Updating Project with Template Changes][updating-project]

### Post-Clone Steps

There are a few steps you should take after cloning your new repository to ensure it is fully configured and ready for
use.

#### 1. Private Internal Reasoning Record (PIRR)

If your repository is private/internal, you should update the `PIRR.md` file in the root of your repository with the
reasoning for the private/internal status of the repository.

#### 2. Repository Settings

Familiarise yourself with the [ONS GitHub Policy](https://github.com/ONSdigital/ons-template/wiki#github-policy) and
ensure your repository is compliant with the policy.
Few key points to note are:

- **[Branch Protection](https://github.com/ONSdigital/ons-template/wiki/5.7-Branch-Protection-rules)**: Ensure
  the `main` or any other primary branch is protected.
- **[Signed Commits](https://github.com/ONSdigital/ons-template/wiki/5.8-Signed-Commits)**: Use GPG keys to sign your
  commits.
- **[Security Alerts](https://github.com/ONSdigital/ons-template/wiki/6.2-Security)**: Make use of Secret scanning and
  Push protection. Dependabot alerts will be enabled by default when using this template.

If you answered `Yes` to the `Do you want to set up the git repository?` question, then these settings would have been
automatically configured for you. However, it is recommended to review these settings to ensure they meet your
requirements.

#### 3. GitHub Usage Policy Compliance

This template helps ensure compliance with the ONS GitHub Usage Policy by automatically including:

- **CODEOWNERS file**: Automatically created with the specified code owners for the repository
- **Repository naming validation**: Enforces lowercase, hyphen/underscore naming conventions
- **Private/Internal Repository Reasoning Record (PIRR)**: Generated for non-public repositories with guidance for completion
- **Compliance checklist**: Added to the generated README to guide developers through required steps
- **Enhanced .gitignore**: Includes patterns to prevent accidental commit of sensitive files

### Updating Project with Template Changes

> [!CAUTION]
> **CURRENTLY UNSUPPORTED**: This is currently unsupported due to
> an [upstream issue](https://github.com/copier-org/copier/issues/240) with Copier.
> Once the issue is resolved, this section will be updated with instructions on how to update your project with changes.

<details>
  <summary>View Details</summary>

You can update your project with changes made to the template since you generated your project. This is useful to keep
your project up to date with the latest tooling and configuration.

If you always used Copier with this project, getting last updates with Copier is simple:

```bash
cd ~/path/to/your/project
make copier-update
```

Copier will ask you all questions again, but default values will be those you answered last time. Just hit Enter to
accept those defaults, or change them if needed or you can use `poetry run copier update --force` instead to avoid
answering the questions again.

For more see [Copier docs](https://copier.readthedocs.io/en/stable/updating/) and `poetry run copier --help-all`.
</details>

## Structure

The structure of the templated repo is as follows:

<!-- markdownlint-disable MD013 -->

```plaintext
├── .github                           # Contains GitHub-specific configurations, including Actions workflows for CI/CD processes.
│   ├── workflows                     # Directory for GitHub Actions workflows.
│   │   ├── ci.yml                    # Workflow for Continuous Integration, running tests and other checks on commits to `main` and on pull requests.
│   │   ├── codeql.yml                # CodeQL workflow for automated identification of security vulnerabilities in the codebase. (Public Repos Only)
│   │   ├── security-scan.yml         # Security scan workflow for running Bandit on the project.
│   ├── dependabot.yml                # Configuration for Dependabot, which automatically checks for outdated dependencies and creates pull requests to update them.
│   ├── ISSUE_TEMPLATE.md             # Template for issues raised in the repository.
│   ├── PULL_REQUEST_TEMPLATE.md      # Template for pull requests raised in the repository.
│   └── release.yml                   # Configuration on how to categorise changes into a structured changelog when using 'Generate release notes' feature.
├── {module_name}/                    # Main Python package directory containing RAP pipeline code.
│   ├── __init__.py                   # Initialises the directory as a Python package with ETLPipeline class.
│   ├── extract.py                    # Data extraction functionality with DataExtractor class.
│   ├── transform.py                  # Data transformation and cleaning with DataTransformer class.
│   └── load.py                       # Data loading and output functionality with DataLoader class.
└── tests                             # Contains all test files.
    ├── e2e                           # Directory for end-to-end tests.
    │   └── test_etl_workflow.py      # End-to-end tests for the ETL workflow.
    └── unit                          # Directory for unit tests, containing tests for individual components of the project.
        ├── test_extract.py           # Unit tests for the extract module.
        ├── test_transform.py         # Unit tests for the transform module.
        └── test_load.py              # Unit tests for the load module.
├── .copier-answers.yml               # Configuration file for Copier, specifying the answers to prompts when generating the project. Required for project updates.
├── .editorconfig                     # Configuration file for maintaining consistent coding styles for multiple developers working on the same project across various editors and IDEs.
├── .gitattributes                    # Git attributes file for defining attributes per path, such as line endings and merge strategies.
├── .gitignore                        # Specifies intentionally untracked files to ignore when using Git, like build outputs and temporary files.
├── .python-version                   # Specifies the Python version to be used with pyenv.
├── .pre-commit-config.yaml          # Configuration file for pre-commit hooks, used to run linting and formatting on the project.
├── CODE_OF_CONDUCT.md                # A code of conduct for the project, outlining the standards of behaviour for contributors.
├── CONTRIBUTING.md                   # Guidelines for contributing to the project, including information on how to raise issues and submit pull requests.
├── LICENSE                           # The license under which the project is made available.
├── Makefile                          # A script used with the make build automation tool, containing commands to automate common tasks.
├── PIRR.md                           # Private Internal Reasoning Record (PIRR) for the repository, documenting the reasoning for the private/internal status of the repository. (Private/Internal Repos Only)
├── poetry.lock                       # Lock file for Poetry, pinning exact versions of dependencies to ensure consistent builds.
├── pyproject.toml                    # Central project configuration file for Python, used by Poetry and tools like Ruff, MyPy, etc.
├── run_etl.py                        # Example script demonstrating RAP pipeline usage with multiple execution methods.
├── README.md                         # The main README file providing an overview of the project, setup instructions, and other essential information.
└── SECURITY.md                       # A security policy for the project, providing information on how to report security vulnerabilities.
```

<!-- markdownlint-enable MD013 -->

## Design Decisions

Although this template is opinionated, there are many alternatives to the tools used in this template which you may
prefer. See the [Alternatives Software/Tools][alternative-software-tools] section for more information.

*1. Why use Poetry exclusively?*

- *Poetry is a modern Python package management tool that simplifies dependency management and packaging. It is also
  a build tool that can be used to package your project into a distributable format.*
- *Poetry provides robust dependency resolution, lockfile support, and integrated virtual environment management.*
- *By standardising on Poetry only, we ensure consistency across all ONS RAP projects and eliminate configuration complexity.*
- *Poetry aligns with modern Python best practices and is increasingly adopted in the data science community.*

*2. What is Ruff and why use Ruff?*

- *Ruff is a newer all-in-one alternative to tools such as flake8, isort, pydocstyle, pyupgrade, and autoflake. It is
  designed to be a more modern and user-friendly alternative to these tools while being extremely fast since it is
  written in Rust.*
- *Ruff is also designed to be more extensible and configurable than the tools it replaces.*

*4. Why use pytest for testing instead of unittest?*

- *pytest is a modern testing framework for Python that is designed to be easy to use and understand.*
- *pytest is more developer-friendly than unittest and has a more extensive ecosystem of plugins and extensions.*

*5. Why is MegaLinter not used for Python?*

- *While MegaLinter provides convenience by bundling multiple linters into a single package, opting for individual
  tools allows for greater flexibility and customisation to match project-specific requirements and coding
  standards.*
- *You are not able to control the versions of the linters used in MegaLinter, which can lead to issues with
  compatibility and consistency.*
- *Although it can easily run in CI, it requires Docker to run locally. For a basic repository with small amounts of
  Python it might be sufficient, but for more complex projects, tooling managed via your chosen package manager is
  encouraged.*

*6. Why not use SuperLinter?*

- *SuperLinter is a similar tool to MegaLinter, but it is not as developer-friendly and does not have as extensive
  documentation.*
- *SuperLinter does not allow auto-fixing of issues, which is a feature of MegaLinter.*

*7. Why does this focus on RAP/ETL patterns rather than web applications?*

- *This template is specifically designed for Reproducible Analytical Pipeline (RAP) development, which is the primary use case for data analysis projects at ONS.*
- *The included sample code demonstrates common data processing patterns: extraction, transformation, and loading of data.*
- *For web applications, other ONS templates or frameworks like Flask/FastAPI would be more appropriate.*
- *The RAP focus ensures that data analysts and researchers have a solid foundation for analytical work.*

*8. My projects do not have a CodeQL workflow. Why?*

- *CodeQL is only available for public repositories. If your repository is private/internal, the CodeQL workflow will
  not be included as it requires GitHub Advanced Security Enterprise plan which is currently not available for our
  organisation.*
- *CodeQL will attempt to run when you first clone the repo, however it will fail if the repo is private/internal.
  You can safely ignore this failure and or remove the CodeQL workflows run from your repo*

*9. Why is Secret Scanning and Push Protection not enabled?*

- *Secret scanning and push protection are enabled for public repositories.*
- *Private/Internal repositories cannot use these without GitHub Advanced Security Enterprise plan which is currently
  not available for our organisation.*

## Future Plans

- Enhanced RAP-specific examples and workflows
- Additional data source connectors (databases, APIs, cloud storage)
- More comprehensive data validation and quality checks
- Integration with ONS data platforms and services
- Advanced statistical analysis templates
- Enhanced documentation and developer guidance
- Ability to update projects with the latest template changes

## Development

:TODO: Add instructions for development

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

See [LICENSE](LICENSE) for details.

---

[//]: # (:TODO: Enable link checking once https://github.com/tcort/markdown-link-check/issues/250 is resolved.)
<!-- markdown-link-check-disable -->

[alternative-software-tools]: #alternatives-softwaretools

[updating-project]: #updating-project-with-template-changes
<!-- markdown-link-check-enable -->
