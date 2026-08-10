# NW-HP-008 - Credit Note for ICS of goods

Files `NW-HP-008.AA-BB.PeppolBIS.xml` implement a basic testing scenario for a credit note for a prior **Intra-Community Supply (ICS)** of goods, where the VAT rate indicated is 0% because the tax responsibility is shifted to the buyer.

`AA-BB` in the filename indicates the two tax jurisdictions of the seller and buyer, respectively.

## Purpose of the test scenario

This test scenario serves to execute the basic **network "happy path"** of a **cross-border credit note**.

The scenario simulates a standard credit note for a B2B cross-border transaction within the ViDA framework where the seller delivered physical goods to a buyer across their borders. The credit note does not include VAT because the responsibility for VAT reporting is shifted to the buyer (reverse charge/ICS mechanism).  
The credit note uses the Peppol BIS Billing 3.0 profile.

## Details of the test scenario

### The Participants
*   **Sellers (Accounting Supplier Party):** are available from all participating countries and indicated by the first country code in the filename (`AA`).
*   **Buyer (Accounting Customer Party):** are available from all participating countries and indicated by the first country code in the filename (`BB`).
*   **Context:** The parties are registered in different EU/EEA member states and the chargeable event is a supply of goods, the transaction is given as an intra-community supply.

### VAT Character of Line Items
The credit note contains two line items, both characterized by a **0% VAT rate** using the specific tax category **"K"**:
*   **Line Item 1:** 3 units of "Great Good" at 102 EUR each (Total: 306 EUR).
*   **Line Item 2:** 7 units of "Another Great Good" at 87 EUR each (Total: 609 EUR).

**Key VAT Details:**
*   **Tax Category ID:** `K` (indicates the VAT categories).
*   **Tax Exemption Reason:** `VATEX-EU-IC`, which explicitly refers to **"VAT exempt intra-community supply (Article 138 Directive 2006/112/EC)"**.
*   **Total Tax Amount:** The total tax amount for the entire credit note is `0` EUR, as the supply is exempt.

Note that deliveries of goods involving Norway (`NO`) are treated as import/export (`G` / `VATEX-EU-G`) as customs is relevant when shipping goods outside and into the borders of the EC.

## Choreography of Transaction

### Outbound / sell-side handling:
* C1 sends credit note data to C2 (not in scope of this test scenario).
* C2 generates the source credit note based on the received data (file `NW-HP-008.AA-BB.PeppolBIS.xml`).
* C2 validates the generated source credit note against applicable schematrons (files `supporting-files/NW-HP-008.AA-BB.PeppolBIS-validation.xml`)
* C2 generates the supply-side TDD (file `sample-results/NW-HP-008.AA-BB.PeppolBIS.TDD-C2.xml`)
* C2 validates the generated supply-side TDD against applicable schematrons (files `supporting-files/NW-HP-008.AA-BB.PeppolBIS.TDD-C2.validation.xml`)

### Transmission process (1/2):

* C2 sends the validated credit note to C3.
* C2 sends the validated supply-side TDD to C5 (according to supplier's VAT ID issuer).

### Inbound / buy-side handling of credit note

* C3 receives inbound credit note from C2 (file `NW-HP-008.AA-BB.PeppolBIS.xml`).
* C3 validates the received credit note against applicable schematrons (files `supporting-files/NW-HP-008.AA-BB.PeppolBIS-validation.xml`)
* C3 generates the buy-side TDD (file `sample-results/NW-HP-008.AA-BB.PeppolBIS.TDD-C3.xml`)
* C3 validates the generated buy-side TDD against applicable schematrons (files `supporting-files/NW-HP-008.AA-BB.PeppolBIS.TDD-C3.validation.xml`)

### Transmission process (2/2):

* C3 sends the validated buy-side TDD to C5 (according to buyer's VAT ID issuer).

### Inbound / Tax Authority handling of TDD
Inbound TDD handling is same at C5A from C2 and at C5B from C3.

* C5 receives inbound TDD from C2/C3, files
  * `sample-results/NW-HP-008.AA-BB.PeppolBIS.TDD-C2.xml` resp.
  * `sample-results/NW-HP-008.AA-BB.PeppolBIS.TDD-C3.xml`.
* C5 validates the received TDD against applicable schematrons, files
  * `supporting-files/NW-HP-008.AA-BB.PeppolBIS.TDD-C2.validation.xml` and
  * `supporting-files/NW-HP-008.AA-BB.PeppolBIS.TDD-C3.validation.xml`.

### Message-level status

* C3 sends positive MLS to C2 (file `sample-results/NW-HP-008.AA-BB.PeppolBIS.MLS-C3.xml`)
* C5A sends positive MLS to C2 (file `sample-results/NW-HP-008.AA-BB.PeppolBIS.MLS-C5A.xml`)
* C5B sends positive MLS to C3 (file `sample-results/NW-HP-008.AA-BB.PeppolBIS.MLS-C5B.xml`)

### Make results available to C1/C4/C6 (out of scope of Testing Scenario)

* credit note receiver's side
    * C3 generates and sends credit note data available to C4.
    * C3 makes received credit note and TDD available to C4.
    * C3 makes results as confirmed available to C4
* credit note sender's side
    * C2 makes generated credit note and TDD available to C1.
    * C2 makes received outcome of transmissions available to C1.
* Tax Administration's side
    * C5 makes received TDD available to C6.
    * C5 makes results as confirmed available to C6