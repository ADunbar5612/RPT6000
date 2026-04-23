# RPT 6000 — Advanced Table Lookups & Data Internalization
The **Report 6000** application adds sophisticated COBOL "bells and whistles" to create a polished, enterprise-grade reporting tool. This program utilizes advanced data structures and memory management to process customer sales data, performing dynamic table lookups to pair sales representative IDs with their names for a comprehensive final report.
 
## What it does
 
* **Dynamic Table Lookups:** Implements a secondary data file (`SALESREP`) that is read into an internal table, allowing the program to dynamically find and display rep names by their ID.
* **Multi-Level Reporting:** Sorted by branch and representative, providing nested subtotals for a granular view of sales performance.
* **Calculated Financial Metrics:** Automatically computes Year-To-Date (YTD) change amounts and percentages, tracking growth or decline across customer accounts.
* **Robust Memory Redefinition:** Utilizes the `REDEFINES` clause to handle special cases, such as displaying "OVRFLW" or "N/A" when numeric calculations aren't possible.
* **Professional Output Formatting:** Manages complex report headers, branch totals, and sales rep totals with standardized COBOL coding syntax.
## New COBOL Concepts Implemented
Compared to previous iterations, this version introduces advanced enterprise features:
 
* **Table Processing & Search:** Implementation of internal tables using the `OCCURS` clause and optimized retrieval via the `SEARCH` verb and `INDEXED BY`.
* **Data Internalization (COPY Members):** Use of `COPY` statements to pull in external record definitions for `CUSTMAST` and `SALESREP`, promoting modularity and code reusability.
* **Advanced Data Types:** Implementation of `PACKED-DECIMAL` (`COMP-3`) for field definitions to optimize mainframe storage and computational performance.
* **Proactive Error Handling:** Use of the `INITIALIZE` verb for group items and `ON SIZE ERROR` logic to manage numeric overflows and division-by-zero during calculations.
* **Flexible Logic Control:** Transition to `EVALUATE TRUE` structures for more readable and robust program control compared to standard nested IF statements.
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

