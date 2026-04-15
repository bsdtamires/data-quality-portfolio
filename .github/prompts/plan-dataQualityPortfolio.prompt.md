# Data Quality Portfolio - Setup Plan

## Overview
Set up a comprehensive Data Quality Portfolio with 4 projects demonstrating various approaches to data quality, testing, and validation using modern tools and AI-assisted patterns.

## Projects Structure

### 1. **project_SQL_Testing_AI_dq** (To Create)
- **Description**: SQL+ AI-assisted test data & database generated data quality framework
- **Technologies**: SQL, AI/LLM, Data Generation, Testing Framework
- **Key Features**:
  - AI-assisted test case generation
  - Synthetic test data generation
  - SQL-based quality validations
  - Database-agnostic approach

### 2. **project_snowflake_dq** (Existing)
- **Description**: Comprehensive Snowflake data quality framework combining dbt, Great Expectations, and custom Python tests
- **Technologies**: Snowflake, dbt, Great Expectations, Python, GitHub Actions
- **Status**: Work in Progress
- **Key Features**: 
  - dbt SQL testing with staging and marts models
  - Great Expectations validation suites
  - Custom Python-based quality tests
  - CI/CD integration


### 3. **project_dagster_ai_quality_pipeline** (To Create)
- **Description**: Orchestration with DQ + AI monitoring using Dagster
- **Technologies**: Dagster, Data Quality, AI/ML Monitoring, Pipeline Orchestration
- **Key Features**:
  - Orchestrated data quality pipelines
  - AI-powered monitoring and alerting
  - Dagster asset definitions
  - Integration with quality frameworks

### 4. **project_LLM_output_quality_testing** (To Create)
- **Description**: DeepEval + PromptFlow + Snowflake for LLM output quality testing
- **Technologies**: DeepEval, PromptFlow, Snowflake, LLM/Generative AI, Prompt Engineering
- **Key Features**:
  - LLM output evaluation using DeepEval
  - Prompt flow management and testing
  - Integration with Snowflake for data storage
  - Quality metrics for generative AI models

## Tasks

### 1. Create Folder Structures
Create three new project directories at root level:
- [ ] `project01_SQL_Testing_AI_dq/`
- [ ] `project03_dagster_ai_quality_pipeline/`
- [ ] `project04_LLM_output_quality_testing/`

### 2. Create README Templates for New Projects
For each new project folder, create a `README.md` with:
- [ ] Project title and one-line description
- [ ] Goal/Purpose section
- [ ] Technologies/Tech Stack section
- [ ] Placeholder Project Structure section
- [ ] Features section (marked as TBD)
- [ ] Getting Started section (TBD)

### 3. Create Root README.md
Create `README.md` at portfolio root with:
- [ ] Portfolio title: "Data Quality Portfolio"
- [ ] Portfolio description and mission
- [ ] Projects table/list with:
  - Project name
  - Brief description (one-liner)
  - Key technologies
  - Links to project README
- [ ] Quick start / navigation section
- [ ] Contributing note

## File Structure After Implementation

```
data-quality-portfolio/
├── README.md (NEW - Portfolio overview)
├── project_snowflake_dq/ (existing - no action)
│   ├── README.md (existing)
│   ├── dbt/
│   ├── great_expectations/
│   └── ai_workflow/
├── project_SQL_Testing_AI_dq/ (NEW)
│   └── README.md (NEW)
├── project_dagster_ai_quality_pipeline/ (NEW)
│   └── README.md (NEW)
└── project_LLM_output_quality_testing/ (NEW)
    └── README.md (NEW)
```

## Content Specifications

### Root README Style
- **Format**: Minimal overview with one-liners per project
- **Tone**: Professional, portfolio-focused
- **Length**: Concise, scannable
- **Purpose**: Serve as entry point for portfolio, highlight all projects at a glance


## Implementation Order
1. Create the 3 new project folders
2. Create README.md for each new project following project_snowflake_dq README file template content
3. Create root portfolio README.md referencing all 4 projects
4. Verify all internal links and structure
