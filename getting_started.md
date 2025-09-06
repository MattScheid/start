# Getting Started: Data Science Workflow

This guide sets up a clean and reproducible data science workflow on a MacBook using VS Code, Python virtual environments, GitHub, and dependency management with `pip-tools`.

---

## 🎯 Goals

- **Reproducibility**: Every project runs in its own isolated environment with pinned dependencies.  
- **Version Control**: Source code, notebooks, and configuration are tracked in GitHub. Generated files, virtual environments, and caches are excluded.  
- **Productivity**: VS Code provides a smooth workflow with Python and Jupyter integration.  

---

## 1. Install Prerequisites

### Install Homebrew
Homebrew is the package manager for macOS.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
source ~/.zshrc
```

### Install Python
Make sure you have a modern version of Python 3.

```bash
brew install python
python3 --version
```

### Install VS Code
Download from [https://code.visualstudio.com/](https://code.visualstudio.com/) or use Homebrew:

```bash
brew install --cask visual-studio-code
```

---

## 2. Create Project and Virtual Environment

```bash
mkdir ~/projects/my_ds_project
cd ~/projects/my_ds_project
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
```

Install common data science libraries:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn jupyterlab ipykernel
```

---

## 3. GitHub Setup

### Create Repository on GitHub
- Go to GitHub and create a new repository.  
- **Do not** initialize with README or `.gitignore`.  

### Initialize Git Locally

```bash
git init
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
echo "# My Data Science Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### Connect to GitHub and Push

```bash
git remote add origin https://github.com/your-username/your-repo.git
git branch -M main
git push -u origin main
```

---

## 4. Configure `.gitignore`

Create a `.gitignore` file to avoid committing unnecessary files:

```bash
echo ".venv/
__pycache__/
.ipynb_checkpoints/
*.pyc
.DS_Store
" > .gitignore
```

Remove anything already tracked that should be ignored:

```bash
git rm -r --cached .
git add .
git commit -m "Apply .gitignore rules"
git push
```

---

## 5. Dependency Management with pip-tools

Install `pip-tools` inside your virtual environment:

```bash
pip install pip-tools
```

Create a `requirements.in` file with only top-level dependencies:

```bash
echo "numpy
pandas
matplotlib
scikit-learn
seaborn
jupyterlab
" > requirements.in
```

Compile all dependencies into a pinned `requirements.txt`:

```bash
pip-compile requirements.in
```

Commit both files:

```bash
git add requirements.in requirements.txt
git commit -m "Add dependency management with pip-tools"
git push
```

---

## 6. Setup Instructions in README

Update your `README.md` with instructions for others:

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   ```

2. Create a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. Open the project in VS Code and use the built-in Jupyter extension to run notebooks.
---

## 7. Configure VS Code

1. Open the project folder in VS Code.  
2. Install extensions: **Python**, **Jupyter**, **Pylance**.  
3. Select the interpreter: `Cmd+Shift+P` → “Python: Select Interpreter” → choose `.venv/bin/python`.  
4. For Jupyter notebooks, add kernel:

```bash
python -m ipykernel install --user --name=my_ds_project
```

Then select `my_ds_project` as the kernel in VS Code.  

---