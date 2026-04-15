# Project Snowflake Data Quality

## Goal
This repo is a data quality tool for studying and portfolio purposes, currently 🚧 a WORK IN PROGRESS 🚧

Intended to be a comprehensive data quality framework for Snowflake-based analytics, demonstrating best practices in data testing, validation, and quality assurance.

## Project Structure
Below a project structure designed as I instructed GitHub Copilot
```
project_snowflake_dq/
├── dbt/
│   ├── models/
│   │   ├── staging/          # Raw data transformations with basic tests
│   │   └── marts/            # Business logic models with advanced tests
│   └── tests/
│       └── custom/           # Python-based custom data quality tests
├── great_expectations/
│   ├── expectations/         # GE validation suites organized by table
│   └── checkpoints/          # Checkpoint configurations for production runs
├── .github/workflows/
│   └── dq_ci.yml            # CI/CD pipeline for automated data quality checks
└── ai_workflow/
    └── prompts_used.md      # Documentation of AI-assisted development
```

## Features

### 1. Dataset
TDB

### 2. **dbt SQL Testing**
- **Staging Models**: Schema validations, null checks, referential integrity
- **Mart Models**: Business rule validations, completeness checks, update audits

### 3. **Great Expectations Validations**
- Automated data quality expectations per source table
- Production checkpoint runs before data consumption
- Comprehensive validation suite for quality assessment

### 4. **Custom Python Tests**
- Advanced data quality logic using Python
- Pytest-based testing framework
- Custom validation rules for complex business logic

### 5. **CI/CD Integration**
- Automated test execution on pull requests
- dbt test suite runs
- Great Expectations checkpoint validation
- Custom Python test execution

## Getting Started

### Prerequisites
- Python 3.11+
- dbt-snowflake
- Great Expectations
- Pytest
- Snowflake account credentials

### Installation

```bash
# Install dependencies
pip install dbt-snowflake great-expectations pydantic pytest

# Configure dbt profiles
dbt debug --profiles-dir ~/.dbt

# Initialize Great Expectations
great_expectations init

# Run tests
dbt test
great_expectations checkpoint run --checkpoint-name production_checkpoint
```

## Running Data Quality Checks

### dbt Tests
```bash
cd dbt
dbt test
dbt test --select models/staging  # Run tests for staging models
dbt test --select state:modified+ # Run tests for modified models
```

### Great Expectations
```bash
cd great_expectations
great_expectations checkpoint run --checkpoint-name production_checkpoint
great_expectations docs build
```

### Custom Tests
```bash
cd dbt/tests/custom
pytest . -v
```

## CI/CD Pipeline

The `.github/workflows/dq_ci.yml` file defines a multi-stage pipeline:

1. **dbt Testing** - Validates data transformations
2. **Great Expectations** - Runs production checkpoints
3. **Custom Tests** - Executes Python-based validations


## Best Practices

- ✅ Keep staging models simple and focused on data extraction
- ✅ Implement business logic validation in mart models
- ✅ Use Great Expectations for cross-cutting data validations
- ✅ Automate quality checks through CI/CD
- ✅ Document test purposes and expectations
- ✅ Version control all test configurations

## AI-Assisted Development

This project was developed with AI assistance using GitHub Copilot. See [ai_workflow/prompts_used.md](ai_workflow/prompts_used.md) for documentation of the AI-assisted development process and prompts used.

IN PROGRESS 🚧

## Contributing

1. Create a feature branch
2. Add or modify data quality tests
3. Ensure all tests pass locally
4. Submit a pull request
5. Verify CI/CD pipeline passes

## Monitoring & Logging

- dbt test outputs are logged during CI runs
- Great Expectations generates HTML reports for validation results
- Custom test logs are available in the workflow artifacts

## Support

For questions or issues:
1. Check the test documentation in model YAML files
2. Review Great Expectations expectations for validation rules
3. Consult custom test docstrings for implementation details

## License

This project is part of personal Data Quality Portfolio.

---

**Last Updated:** April 14, 2026  
**Version:** 1.0  
**Status:** Active Development