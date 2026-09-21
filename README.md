# oee-single-source-of-truth
A sanitized technical case study of a centralized manufacturing data architecture for OEE analytics.
 OEE Single Source of Truth
OEE Single Source of Truth
Centralized Manufacturing Data Architecture & OEE Analytics
Role: Manager — LeapX Coating
Domain: Data Engineering | Database Management | Manufacturing Analytics | SQL | Power BI

1. Technical Overview
The project involved designing a centralized manufacturing data architecture to establish a Single Source of Truth (SSOT) for Overall Equipment Effectiveness (OEE).
The existing operational reporting process relied on fragmented shift-level tracking of downtime, production output, and reject/quality data. This resulted in multiple versions of operational information and the possibility of inconsistent OEE figures between shifts and teams.
The solution addressed the problem at the data architecture and database layer, rather than treating dashboard development as the primary solution.
The architecture consolidated operational data into a centralized database, standardized the underlying data structure and OEE methodology, calculated the required performance metrics, and exposed the resulting analytical dataset through Power BI.

2. Technical Architecture
The solution followed a layered data architecture:
┌───────────────────────────────────────────────┐
│              SHOP-FLOOR DATA                 │
│                                               │
│  Downtime Logs │ Production Output │ Rejects │
└───────────────────────┬───────────────────────┘
                        │
                        ▼
┌───────────────────────────────────────────────┐
│       DATA CONSOLIDATION & STANDARDIZATION    │
│                                               │
│  • Data consolidation                         │
│  • Structural standardization                 │
│  • Data validation                             │
│  • Consistent definitions                     │
└───────────────────────┬───────────────────────┘
                        │
                        ▼
┌───────────────────────────────────────────────┐
│             CENTRAL DATABASE                  │
│                                               │
│          SINGLE SOURCE OF TRUTH               │
│                                               │
│  Standardized operational data                │
└───────────────────────┬───────────────────────┘
                        │
                        ▼
┌───────────────────────────────────────────────┐
│              OEE LOGIC LAYER                  │
│                                               │
│ Availability × Performance × Quality          │
└───────────────────────┬───────────────────────┘
                        │
                        ▼
┌───────────────────────────────────────────────┐
│             POWER BI SEMANTIC /               │
│              REPORTING LAYER                  │
│                                               │
│  KPI │ Trends │ Downtime │ Quality │ OEE      │
└───────────────────────┬───────────────────────┘
                        │
                        ▼
┌───────────────────────────────────────────────┐
│          MANAGEMENT & OPERATIONS              │
│                                               │
│       Monitoring • Analysis • Decisions       │
└───────────────────────────────────────────────┘

The documented approach specifically identifies SQL-based consolidation, a central database, standardized OEE calculations, and Power BI reporting.

3. Data Engineering Workflow
The technical workflow was designed as a controlled pipeline:
Stage 1 — Data Acquisition
Operational information was collected from shop-floor sources covering:
Downtime
Production output
Rejects / quality information
These represented the primary inputs required for OEE analysis.
Stage 2 — Data Consolidation
Data from different operational sources and production lines was consolidated into a common processing structure.
The objective was to remove fragmentation before analytical calculations were performed.
Stage 3 — Data Standardization
The consolidated records were standardized into a unified format across production lines and shifts.
This created consistent definitions and structures for downstream calculations.
Stage 4 — Data Validation
Operational records were checked for consistency before being used as the analytical source.
This step is particularly important in manufacturing analytics because incorrect downtime, output, or reject information directly affects OEE.
Stage 5 — Centralized Storage
The standardized dataset was stored within a centralized database.
The database became the authoritative source for OEE reporting, replacing independent shift-level spreadsheet calculations.
The source documentation explicitly identifies the central database as the "single version" of the truth.

4. Database Management Approach
The central database was positioned as the authoritative data layer between operational data collection and business intelligence.
Conceptually:
Operational Data
       │
       ▼
Data Standardization
       │
       ▼
Central Database
       │
       ├──────────────► Historical Analysis
       │
       ├──────────────► OEE Calculations
       │
       └──────────────► Power BI

This architecture provided an important separation between:
Data Storage → Data Processing → Business Logic → Visualization
Instead of allowing each reporting team to independently calculate OEE, the centralized data layer established a common foundation.
This reduced the risk of:
Duplicate calculations
Conflicting metrics
Different definitions
Shift-level reporting discrepancies
Manual spreadsheet dependency

5. OEE Calculation Algorithm
The OEE calculation was standardized using three primary components:
Availability
Availability =
Operating Time
────────────────────────
Planned Production Time

Performance
Performance =
Actual Output
────────────────
Theoretical Output

Quality
Quality =
Good Output
────────────────
Total Output

Final OEE
OEE =
Availability
     ×
Performance
     ×
Quality

The documented project explicitly defines OEE as Availability × Performance × Quality.

6. OEE Processing Algorithm
START
  │
  ▼
Collect Operational Data
  │
  ├── Downtime
  ├── Production Output
  └── Rejects
  │
  ▼
Consolidate Records
  │
  ▼
Standardize Data
  │
  ▼
Validate Data
  │
  ▼
Load / Maintain Central Database
  │
  ▼
Calculate Availability
  │
  ▼
Calculate Performance
  │
  ▼
Calculate Quality
  │
  ▼
Calculate OEE
  │
  ▼
Publish Standardized Metrics
  │
  ▼
Power BI Dashboard
  │
  ▼
Operational / Management Analysis
  │
  ▼
END


7. Data Quality & Standardization
A major technical consideration was ensuring that OEE was calculated from consistent operational definitions.
The standardization layer therefore served as a control point between raw operational information and analytical calculations.
The conceptual transformation was:
Fragmented Records
       ↓
Common Structure
       ↓
Standardized Definitions
       ↓
Validated Dataset
       ↓
Centralized Storage
       ↓
Consistent Metrics

This is important because the reliability of an analytical KPI depends on the consistency of the underlying data.

8. SQL Data Processing
SQL was used as the primary technology for the data consolidation layer.
The SQL processing conceptually supported:
Combining operational datasets
Standardizing records
Preparing data for centralized storage
Supporting consistent analytical calculations
Creating a reliable dataset for BI consumption
The documented project specifically identifies SQL-based consolidation of downtime, output, and reject data across production lines.

9. Business Intelligence Layer
Power BI consumed the standardized data layer rather than relying on independently maintained shift-level calculations.
The reporting architecture was:
Central Database
       │
       ▼
Standardized OEE Dataset
       │
       ▼
Power BI
       │
       ├── OEE KPI
       ├── Availability
       ├── Performance
       ├── Quality
       ├── Downtime Analysis
       └── Quality-Loss Analysis

This provided shared visibility across shifts and management.

10. Technical Decision: Why a Single Source of Truth?
The fundamental architectural decision was to move OEE calculations away from independently maintained spreadsheets and establish a centralized database-backed reporting model.
Previous Model
Shift A Spreadsheet ──► OEE A
Shift B Spreadsheet ──► OEE B
Shift C Spreadsheet ──► OEE C

                  ↓

        Conflicting Metrics

Centralized Model
            Operational Data
                    │
                    ▼
          Centralized Database
                    │
                    ▼
          Standardized OEE Logic
                    │
                    ▼
              One OEE Metric
                    │
                    ▼
                Power BI

This created a controlled and repeatable analytical process.

11. End-to-End Technical Algorithm
Input
Downtime Data
Production Output
Reject / Quality Data

Processing
Consolidate
     ↓
Standardize
     ↓
Validate
     ↓
Centralize
     ↓
Calculate

Calculation
Availability
Performance
Quality
     ↓
OEE

Output
Centralized OEE Dataset
          ↓
      Power BI
          ↓
Operational Insights
          ↓
Management Reporting


12. Key Engineering Outcomes
The architecture produced four important outcomes:
1. Metric Consistency
Different shifts and teams no longer relied on independent OEE figures.
2. Centralized Data Governance
A central database provided one authoritative analytical source.
3. Faster Root-Cause Analysis
The unified dataset made downtime and quality-loss drivers easier to identify.
4. Trusted Management Reporting
Management reporting could rely on one standardized OEE metric.
These outcomes are directly reflected in the documented case study.

13. Technical Skills Demonstrated
Data Engineering
Data consolidation
Data standardization
Data validation
Centralized data architecture
Analytical data pipelines
Database Management
Centralized data storage
Single Source of Truth architecture
Structured operational data
Metric consistency
Data governance
SQL
Operational data consolidation
Data transformation
Analytical data preparation
Manufacturing Analytics
OEE
Availability
Performance
Quality
Downtime analysis
Production-loss analysis
Business Intelligence
Power BI
KPI reporting
Operational dashboards
Management reporting

14. Architecture Summary
The final architecture can be summarized as:
SOURCE
Shop-floor operational data
↓
INGEST / CONSOLIDATE
SQL-based data consolidation
↓
STANDARDIZE
Unified structure across lines and shifts
↓
STORE
Central database / Single Source of Truth
↓
CALCULATE
Availability × Performance × Quality
↓
SERVE
Standardized OEE analytical dataset
↓
VISUALIZE
Power BI dashboard
↓
DECIDE
Operational and management decision-making

Portfolio Statement
Designed and implemented a centralized manufacturing data architecture to establish a Single Source of Truth for OEE, consolidating fragmented downtime, production output, and quality data through SQL-based processing into a centralized database, standardizing OEE calculations across production lines and shifts, and delivering a unified Power BI reporting layer for operational and management analytics.

