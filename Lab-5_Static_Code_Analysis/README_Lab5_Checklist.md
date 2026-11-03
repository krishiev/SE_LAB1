# Lab 5 — Static Code Analysis checklist

The handout requires analysis of the assigned Python script using Pylint, Bandit and Flake8; fix at least four issues, handle Bandit findings and Flake8 formatting, target Pylint score above 9.5, retain before/after reports, and make three separate commits for tool-driven fixes.

## Required inputs
- [ ] Instructor-assigned repository URL
- [ ] Exact Python script path
- [ ] Initial code version/commit

## Required deliverables
- [ ] Updated Python script with at least four genuine issues fixed
- [ ] Completed issue table (`Issue_Log.csv`)
- [ ] Reflection answers (`Reflection_Template.md`)
- [ ] `pylint_report_before.txt` and `pylint_report_after.txt`
- [ ] `bandit_report_before.txt` and `bandit_report_after.txt`
- [ ] `flake8_report_before.txt` and `flake8_report_after.txt`
- [ ] Three commits: Pylint-related fixes, Bandit-related fixes, Flake8-related fixes
- [ ] Re-run tools and preserve actual output

## Local setup (macOS/Linux)
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install pylint bandit flake8
```

Replace `your_python_script.py` with the actual assigned file path:
```bash
pylint your_python_script.py > pylint_report_before.txt
bandit -r your_python_script.py > bandit_report_before.txt
flake8 your_python_script.py > flake8_report_before.txt
```

Do not fabricate report output or issue line numbers. Run the tools on the assigned source file, fix genuine findings, then rerun and save the after reports.
