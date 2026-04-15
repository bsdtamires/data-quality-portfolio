# 01_sql_dq_framework - SQL-Based Data Quality Framework

🚧 Work in Progress 🚧

## Goal
A pure SQL-based data quality framework focused on practical, database-agnostic validations. This project demonstrates how to build comprehensive data quality checks using only SQL, making it portable across different database platforms and easy to version control.

## Overview
this framework implements the six dimensions of data quality (6D model):
- **Completeness**: NULL detection and missing data validation
- **Uniqueness**: Duplicate detection for PKs and natural keys
- **Validity**: Format, range, and domain constraint validation
- **Consistency**: Referential integrity and cross-table business rules
- **Accuracy**: Business logic validation and calculation verification
- **Timeliness**: Data freshness and date anomaly detection

Plus advanced capabilities:
- Window function-based statistical anomaly detection
- Percentile and standard deviation analysis
- Comprehensive DQ scoring and reporting

## Project Structure

```
01_sql_dq_framework/
├── schema/
│   ├── create_tables.sql         # DDL for your dataset
│   └── seed_data.sql             # Sample data with intentional quality issues
├── checks/
│   ├── 01_completeness.sql       # NULL checks by column and table
│   ├── 02_uniqueness.sql         # Duplicate detection: PKs, natural keys
│   ├── 03_validity.sql           # Format/range/domain validation
│   ├── 04_consistency.sql        # Referential integrity, cross-table rules
│   ├── 05_accuracy.sql           # Business logic validation
│   └── 06_timeliness.sql         # Freshness checks, date anomalies
├── advanced/
│   ├── window_anomalies.sql      # Window functions for outlier detection
│   ├── statistical_profiling.sql # Mean, stddev, percentiles via SQL
│   └── dq_summary_report.sql     # Master query: DQ score per table
├── ai_workflow/
│   ├── prompts_used.md           # ⬡ Prompts that generated the initial versions
│   └── ai_vs_human_changes.md    # ⬡ What you changed and why
└── README.md                      # This file
```

## Features

### 1. **Six-Dimension Data Quality Checks**
Complete coverage of the industry-standard data quality dimensions:
- All checks implemented in pure SQL (no external dependencies)
- Comments with example implementations
- Easy to adapt to your datasets and platforms
- Threshold values clearly marked for customization

### 2. **Completeness Validation** (`01_completeness.sql`)
- Identifies NULL values across tables
- Calculates percentage of missing data
- Groups results by column for easy analysis
- Validates required field constraints

### 3. **Uniqueness / Deduplication** (`02_uniqueness.sql`)
- Primary key duplicate detection
- Natural key violation identification
- Email, user ID, and other business-critical uniqueness checks
- Output includes record counts and sample IDs

### 4. **Validity / Format Checks** (`03_validity.sql`)
- Email format validation (regex patterns)
- Phone number format verification
- Numeric range validation (e.g., amounts > 0)
- Domain validation (valid values for status fields)
- Multiple validation rules with clear error categorization

### 5. **Consistency / Referential Integrity** (`04_consistency.sql`)
- Foreign key relationship validation
- Cross-table business rule enforcement
- Hierarchical data consistency checks
- Reports orphaned records and constraint violations

### 6. **Accuracy / Business Logic** (`05_accuracy.sql`)
- Calculation verification (order total vs. line items)
- Business rule enforcement (inactive customers shouldn't have recent orders)
- Status consistency validation
- Derived field accuracy checks

### 7. **Timeliness / Freshness** (`06_timeliness.sql`)
- Data staleness detection (e.g., no updates in 30 days)
- Future date anomaly detection
- Historical data age analysis
- Last update timestamp validation

### 8. **Advanced Statistical Analysis** (`advanced/`)
- **Window Anomalies**: Detect outliers using 3-sigma rule or percentile-based methods
- **Statistical Profiling**: Calculate mean, median, std dev, percentiles for numeric columns
- **DQ Summary Report**: Aggregated quality score per table (Excellent/Good/Fair/Poor)

### 9. **AI-Assisted Development Documentation**
- `prompts_used.md`: Track which AI prompts generated each check
- `ai_vs_human_changes.md`: Document refinements and why they were made
- Learn from AI suggestions while maintaining human oversight

## Getting Started

### Prerequisites
- Access to a SQL database (Snowflake, PostgreSQL, MySQL, SQL Server, etc.)
- Your dataset loaded with sample data

### Quick Start

1. **Adapt the Schema**
   ```sql
   -- Edit: schema/create_tables.sql
   -- Define your table structures
   -- Run the script to create tables
   ```

2. **Load Test Data**
   ```sql
   -- Edit: schema/seed_data.sql
   -- Add sample data with intentional quality issues
   -- Run to populate tables with test data
   ```

3. **Run Basic Quality Checks**
   ```sql
   -- Start with individual checks
   -- Review the results
   -- checks/01_completeness.sql
   -- checks/02_uniqueness.sql
   -- ... etc
   ```

4. **Generate DQ Summary**
   ```sql
   -- Run the master report
   -- advanced/dq_summary_report.sql
   -- Review overall quality score
   ```

### Customization

Each check file includes:
- **Comments** explaining the logic
- **Example code** that you can uncomment and adapt
- **Threshold values** clearly marked for adjustment
- **Placeholders** for your specific table/column names

### SQL Dialect Compatibility

These checks are written in standard SQL with notes for platform-specific syntax:
- **Snowflake**: Ready to use with minimal adjustments
- **PostgreSQL**: Function names may need updating (e.g., `STRING_AGG`)
- **MySQL**: Some window functions or date functions may differ
- **SQL Server**: May need `CONVERT()` instead of `CAST()` in some cases

See `ai_workflow/ai_vs_human_changes.md` for documented dialect adaptations.

## Technologies

- **SQL** (primary language)
- **Data Warehouse**: Database-agnostic (Snowflake, PostgreSQL, MySQL, SQL Server, etc.)
- **Reporting**: SQL-native (visualize results with your BI tool)
- **Version Control**: Git (track SQL check evolution)
- **AI Assistance**: Code generation with human oversight

## Workflow

### Development Flow
1. **AI-Assisted Code Generation**: Use LLM to generate initial SQL checks
2. **Human Review**: Validate logic against business requirements
3. **Platform Adaptation**: Adjust for your specific database dialect
4. **Testing**: Run against real/sample data with expected quality issues
5. **Documentation**: Record changes and reasoning in `ai_workflow/` docs
6. **Deployment**: Version SQL checks, integrate into pipelines

### Team Collaboration
- Document AI usage in `prompts_used.md`
- Track manual changes in `ai_vs_human_changes.md`
- Use comments to explain complex business rules
- Keep thresholds configurable and version-controlled

## Example: Running a Complete DQ Check

```sql
-- 1. Create tables
.execute schema/create_tables.sql

-- 2. Load test data (with intentional faults)
.execute schema/seed_data.sql

-- 3. Run completeness check
.execute checks/01_completeness.sql
-- OUTPUT: 
-- | table_name | column_name | null_count | null_percentage |
-- | customers  | first_name  | 5          | 1.25            |
-- | customers  | email       | 2          | 0.50            |

-- 4. Run uniqueness check
.execute checks/02_uniqueness.sql
-- OUTPUT: 
-- | table_name | key_type         | email              | duplicate_count |
-- | customers  | email (natural)  | john@example.com   | 2               |

-- 5. Generate summary report
.execute advanced/dq_summary_report.sql
-- OUTPUT:
-- | table_name | checks_performed | overall_dq_score | dq_status |
-- | customers  | 6                | 92.50            | EXCELLENT |
-- | orders     | 6                | 78.33            | GOOD      |
```

## Key Concepts

### Why SQL-Only?
- ✓ Platform independent and portable
- ✓ No external dependencies or libraries
- ✓ Easy version control and code review
- ✓ Integrates directly into data pipelines
- ✓ Database-native performance
- ✓ Familiar to data engineers and analysts

### DQ Dimensions Explained

| Dimension | Definition | What We Check |
|-----------|-----------|---|
| **Completeness** | All required data is present | No unexpected NULLs |
| **Uniqueness** | No duplicate records | No duplicate PKs or natural keys |
| **Validity** | Data matches required format | Email formats, number ranges |
| **Consistency** | Data agrees across sources | Foreign keys exist, business rules hold |
| **Accuracy** | Data represents reality | Calculations correct, logic sound |
| **Timeliness** | Data is current | No stale data, dates in valid range |

### Scoring Methodology

The `dq_summary_report.sql` calculates an overall score:
```
EXCELLENT (≥95): All checks passing or minimal issues
GOOD      (≥85): Most checks passing, minor issues
FAIR      (≥70): Several checks failing, attention needed
POOR      (<70): Major quality issues, immediate action required
```

Customize these thresholds in the report query for your business.

## Best Practices

1. **Test with Intentional Faults**: Seed data with quality issues to validate checks work
2. **Document Assumptions**: In comments, explain what business rules you're validating
3. **Use Meaningful Names**: Column aliases like `null_percentage`, `duplicate_count` aid readability
4. **Version Your Checks**: Git commit each update with clear messages
5. **Track AI Changes**: Use `ai_vs_human_changes.md` for continuous improvement
6. **Customize Thresholds**: Adjust sensitivity based on your data domain
7. **Automate Regularly**: Schedule checks as part of your data pipeline
8. **Review Results**: Set up alerts for when DQ score drops below acceptable levels

## Next Steps

- [ ] Adapt schema files to your dataset structure
- [ ] Review and customize threshold values in checks
- [ ] Test with your actual data
- [ ] Document any platform-specific adjustments
- [ ] Integrate into your data pipeline
- [ ] Set up automated DQ reporting
- [ ] Refine checks based on domain knowledge
- [ ] Create custom metrics for your business

## Status

🚧 **Work in Progress**

This is a template framework showing all six DQ dimensions with SQL examples. The checks are ready to customize for your specific use cases and datasets.

## Resources

- [Data Quality Dimensions](https://en.wikipedia.org/wiki/Data_quality)
- SQL Window Functions
- Statistical Analysis in SQL
- Data Profiling Best Practices

---

**Last Updated**: April 2026  
**Framework Version**: 1.0  
**Database Platform**: Database-agnostic (Snowflake-optimized)
