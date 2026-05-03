> ---snip-------------
> ## How to use this template directory
> The template text and sections are guidelines only; use only what makes sense and remove any unused text or files.
> 
> * Assign a Test Scenario ID
> * Place the original invoice file directly in this `.` test scenario directory
> * Update this README file as appropriate
>   * Use `TODO` markers and sample sections as guidance
>   * Remove sections/text if not applicable
> * Put "results" into the `./results` directory, including TDD and MLS files (as available - replace/remove template files, if not relevant)
>   * If "expected results" are available, put them into `./expected-results`
>   * If multiple test runs yield multiple sets of results, use a `[Test scenario Run ID]` and create subdirectories as appropriate
> * Put "other invoice format" renditions (if available) into the `./other-formats` directory.
> * If any, add supporting files into `./supporting-files` directory.
> * Remove this section on template description
>
> ---snap-------------



# [TODO: Test scenario ID]

File `[TODO Test scenario ID].PeppolBIS.xml` implements [TODO: describe scenario]




## Purpose of the test scenario

This test scenario serves to execute the **[TODO: test scenario name]**.

The scenario simulates [TODO: describe business scenario]  
The invoice uses the Peppol BIS Billing 3.0 profile.

## Details of the test scenario

### The Participants
*   **Seller (Accounting Supplier Party):** `[TODO: Seller Name]` ([TODO: Seller Legal Name]), located in the **[TODO: tax jurisdiction]** (`[TODO: country code]`).
*   **Buyer (Accounting Buyer Party):** `[TODO: Buyer Name]` ([TODO: Buyer Legal Name]), located in the **[TODO: tax jurisdiction]** (`[TODO: country code]`).
*   **Context:** [TODO: participant's VAT context]

### VAT Character of Line Items
[TODO: describe line item VAT]

## Choreography of Transaction

### Message Flows
[TODO: describe C1/2/3/4/5/6 message interactions]


### Message-level status
[TODO: describe MLS interactions]

### Make results available to C1/C4/C6 (out of scope of Testing Scenario)
[TODO: describe results from C1/C4/C6 point of view]
