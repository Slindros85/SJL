# Usage Guide

## Command Line Interface

### Basic Usage

Run all checks on the current directory:
```bash
python -m check_gpt.main --repo .
```

### Run Specific Checks

**Linting only:**
```bash
python -m check_gpt.main --repo . --check lint
```

**Verification only:**
```bash
python -m check_gpt.main --check verify
```

**Custom analysis only:**
```bash
python -m check_gpt.main --check custom
```

### Generate Reports

**JSON report:**
```bash
python -m check_gpt.main --repo . --report --format json --output report.json
```

**HTML report:**
```bash
python -m check_gpt.main --repo . --report --format html --output report.html
```

**Text report:**
```bash
python -m check_gpt.main --repo . --report --format text --output report.txt
```

### Options

- `--repo` - Repository path (default: current directory)
- `--config` - Configuration file path
- `--check` - Which checks to run: `all`, `lint`, `verify`, `custom` (default: all)
- `--report` - Generate formatted report
- `--format` - Report format: `json`, `html`, `text` (default: json)
- `--output` - Output file path (if not specified, prints to stdout)

## Programmatic Usage

Import Check GPT in your Python code:

```python
from check_gpt import CheckGPT

app = CheckGPT("/path/to/repo")
results = app.run_all_checks()

# Or run specific checks
linting = app.run_linting()
verification = app.run_verification()
custom = app.run_custom_analysis()
```

## GitHub Actions Integration

The Check GPT workflow runs automatically on:
- Push to `main` and `develop` branches
- Pull requests to `main` and `develop` branches

### Viewing Results

1. Go to the **Actions** tab in your GitHub repository
2. Click on the workflow run
3. View the check results and artifacts

### PR Comments

When a pull request is analyzed, Check GPT automatically comments with:
- Analysis status (PASS/FAIL)
- Summary of issues found
- Breakdown by category

## Configuration

Configure Check GPT using `check_gpt.yml`:

```yaml
linting:
  enabled: true
  tools:
    - pylint
    - flake8
  max_line_length: 100

verification:
  enabled: true
  min_coverage: 80
  run_tests: true
  check_types: true

custom:
  enabled: true
  security:
    check_secrets: true
  performance:
    warn_nested_loops: true
```

## Examples

### Example: Run analysis and exit with error code on failure

```bash
python -m check_gpt.main --repo . --check all
echo "Exit code: $?"
```

### Example: Run linting and save JSON report

```bash
python -m check_gpt.main --repo . --check lint --report --format json --output lint-report.json
```

### Example: Generate HTML report for presentation

```bash
python -m check_gpt.main --repo . --report --format html --output quality-report.html
```

## Troubleshooting

### Pylint/Flake8 not found

Install linting tools:
```bash
pip install pylint flake8 mypy
```

### Tests not running

Ensure pytest is installed and you have test files:
```bash
pip install pytest pytest-cov
```

### Permission denied

Make the script executable:
```bash
chmod +x check_gpt/main.py
```
