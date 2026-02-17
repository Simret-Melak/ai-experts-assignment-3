# AI Experts Assignment (Python)

This assignment evaluates your ability to:

- set up a small Python project to run reliably (locally + in Docker),
- pin dependencies for reproducible installs,
- write focused tests to reproduce a bug,
- implement a minimal, reviewable fix.

## What you will do

### 1) Dockerfile (required)

Create a `Dockerfile` so the project can run the test suite in a non-interactive, CI-style environment.

Requirements:

- requirements.txt exists and is used during build (pip install -r requirements.txt)
- pytest must be included/pinned in requirements.txt
- The image must run tests by default (use: `CMD ["python", "-m", "pytest", "-v"]`).
- The build must install dependencies from `requirements.txt`.

### 2) requirements.txt (required)

Create a `requirements.txt` with pinned versions, using this format:

- `package==x.y.z`

### 3) README updates (required)

Update this README to include:

## Running Tests Locally

### Prerequisites
- Python 3.9 or higher
- pip (Python package installer)

### Step-by-Step Instructions

**Step 1: Clone the repository** 
- git clone "your-repo-url"
- cd ai-experts-assignment-3

### Create virtual environment
    python3 -m venv venv

### Activate it
### On macOS/Linux:
source venv/bin/activate
### On Windows:
venv\Scripts\activate

### Install dependencies
pip install -r requirements.txt

### Run all tests with verbose output
pytest -v

### Deactivate virtual environment
deactivate

## Running with Docker

### Prerequisites
- Docker installed on your machine
- Docker daemon running (Docker Desktop on Mac/Windows)

### Step-by-Step Instructions

**Step 1: Build the Docker image**

docker build -t ai-experts-assignment .

**Step 2: Run all tests**

docker run --rm ai-experts-assignment

**Step 5: Clean up (when done)**

docker rmi ai-experts-assignment


### 4) Find + fix a bug (required)

There is a bug somewhere in this repository.

Your tasks:

- Identify the bug through reading code and/or running tests.
- Write tests that reproduce the bug (tests should fail on the current code).
- Apply the smallest possible fix to make the tests pass.
- Keep the change minimal and reviewable (no refactors).

## Constraints

- Keep changes minimal and reviewable.
- Do not refactor unrelated code.
- Do not introduce extra tooling unless required.
- You may add tests and the smallest code change needed to fix the bug.

### 5) EXPLANATION.md (required)

Create `EXPLANATION.md` (max 250 words) containing:

- **What was the bug?**
- **Why did it happen?**
- **Why does your fix solve it?**
- **One realistic case / edge case your tests still don’t cover**

## Submission

- Submit a public GitHub repository URL containing your solution to the Google form link provided.
