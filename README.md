RPT6000 — Advanced Table Lookups & Data Internalization

Continues building upon the sales report, this time eliminating hard-coded values.

A collaborative COBOL project by Aidan Dunbar

Overview
RPT6000 is an enterprise-grade COBOL reporting application that builds on earlier iterations of the sales report by replacing hard-coded data with dynamic table lookups and externalized record definitions. The program reads customer sales data, cross-references a secondary SALESREP file to resolve representative names at runtime, and produces a polished, multi-level summary report complete with financial metrics.

What It Does
FeatureDescriptionDynamic Table LookupsReads the SALESREP file into an internal table at startup; resolves rep names by ID during report generation - no hard-coded name lists.Multi-Level ReportingOutput sorted by branch, then by sales representative, with nested subtotals at each level for granular performance analysis.Financial MetricsComputes Year-To-Date (YTD) change amounts and percentages to track account growth or decline across periods.Overflow / N/A HandlingUses REDEFINES to display OVRFLW or N/A whenever a calculation overflows or a division-by-zero condition is detected.Professional FormattingManages report headers, branch totals, rep totals, and page breaks with standardized COBOL output conventions.

New COBOL Concepts Introduced
This version introduces several advanced, enterprise-level COBOL techniques not present in earlier iterations:
Table Processing & Search
Internal tables are defined with the OCCURS clause and an INDEXED BY phrase. The SEARCH verb performs efficient sequential lookup against the loaded SALESREP table, replacing what would otherwise be a hard-coded series of condition checks.
Data Internalization via COPY Members
External record layouts for CUSTMAST and SALESREP are pulled into the program using COPY statements. This promotes modularity - record definitions live in one authoritative place and can be reused across multiple programs without duplication.
Packed-Decimal Storage (COMP-3)
Numeric fields are declared as PACKED-DECIMAL (also written COMP-3). This mainframe-native storage format packs two decimal digits per byte, reducing storage footprint and improving arithmetic performance on IBM Z-series hardware.
Proactive Error Handling

INITIALIZE resets group items to clean starting values before each processing cycle, preventing stale data from corrupting totals.
ON SIZE ERROR clauses guard all arithmetic statements; when a result would overflow its receiving field or a divisor is zero, control branches to safe fallback logic instead of abending.

Evaluate TRUE Structures
Nested IF chains are replaced with EVALUATE TRUE blocks, making multi-condition branching easier to read, maintain, and extend - a widely adopted pattern in modern COBOL shops.

Program Output
Final Report
The main report lists customers grouped by branch and sales representative, showing current-period sales, prior-year sales, YTD change amount, and YTD change percentage. Branch and rep subtotals print automatically at each control break.
Unknown Representative Validation
If a customer record references a rep ID not found in the SALESREP table, the program flags the entry in the output rather than silently dropping the row or abending — demonstrating the SEARCH/WHEN OTHER fallback path.

File Inventory
RPT6000/

├── RPT6000.cbl        # Main program source

├── CUSTMAST.cpy       # COPY member — customer master record layout

├── SALESREP.cpy       # COPY member — sales representative record layout

├── SALESREP.dat       # Sales representative data file (runtime input)

├── CUSTMAST.dat       # Customer master data file (runtime input)

└── README.md

