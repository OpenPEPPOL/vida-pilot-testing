# NW-HP-002

File `NW-HP-002.PeppolBIS.xml` implements a testing scenario for a **Reverse Charge** transaction of services, where the VAT rate indicated is `0%` because the tax responsibility is shifted to the buyer.

## Purpose of the test scenario

This test scenario serves to execute the basic **network "happy path"** for a **service-based invoice** involving reverse charge mechanisms.

The scenario simulates a standard B2B transaction where the seller is located in Sweden (`SE`) and the buyer is located in Slovakia (`SK`). Because the services are subject to the reverse charge mechanism, the seller does not charge VAT, and the tax responsibility is shifted to the buyer.  
The document uses the Peppol BIS Billing 3.0 profile.

## Details of the test scenario:

### The Participants
*   **Seller (Accounting Supplier Party):** `SSB` (Sverige Seller Business AB), located in **Sweden** (`SE`).
*   **Buyer (Accounting Customer Party):** `SP sro` (Slovenský Príklad s.r.o.), located in **Slovakia** (`SK`).
*   **Context:** The parties are registered in different EU member states, and the invoice covers services where the reverse charge mechanism applies.

### VAT Character of Line Items
The invoice contains two line items, both characterized by a **0% VAT rate** using the specific tax category **"AE"**:
*   **Line Item 1:** 16 units of "Super Service" at 124 SEK each (Total: 1984 SEK).
*   **Line Item 2:** 32 units of "More Super Service" at 124 SEK each (Total: 3968 SEK).

**Key VAT Details:**
*   **Tax Category ID:** `AE` (indicates the reverse charge category).
*   **Tax Exemption Reason:** `VATEX-EU-AE` (indicates that reverse charge applies).
*   **Total Tax Amount:** The total tax amount for the entire invoice is `0` SEK, as the supply is subject to reverse charge.

## Choreography of Transaction

### Outbound / sell-side handling:
* C1 sends invoice data to C2 (not in scope of this test scenario).
* C2 generates the source invoice based on the received data (file `NW-HP-002.PeppolBIS.xml`).
* C2 validates the generated source invoice against applicable schematrons (files `supporting-files/NW-HP-002.PeppolBIS-validation.xml`)
* C2 generates the supply-side TDD (file `sample-results/NW-HP-002.PeppolBIS.TDD-C2.xml`)
* C2 validates the generated supply-side TDD against applicable schematrons (files `supporting-files/NW-HP-002.PeppolBIS.TDD-C2.validation.xml`)

### Transmission process (1/2):

* C2 sends the validated invoice to C3.
* C2 sends the validated supply-side TDD to C5 (according to supplier's VAT ID issuer).

### Inbound / buy-side handling of invoice

* C3 receives inbound invoice from C2 (file `NW-HP-002.PeppolBIS.xml`).
* C3 validates the received invoice against applicable schematrons (files `supporting-files/NW-HP-002.PeppolBIS-validation.xml`)
* C3 generates the buy-side TDD (file `sample-results/NW-HP-002.PeppolBIS.TDD-C3.xml`)
* C3 validates the generated buy-side TDD against applicable schematrons (files `supporting-files/NW-HP-002.PeppolBIS.TDD-C3.validation.xml`)

### Transmission process (2/2):

* C3 sends the validated buy-side TDD to C5 (according to buyer's VAT ID issuer).

### Inbound / Tax Authority handling of TDD
Inbound TDD handling is same at C5A from C2 and at C5B from C3.

* C5 receives inbound TDD from C2/C3, files
  * `sample-results/NW-HP-002.PeppolBIS.TDD-C2.xml` resp.
  * `sample-results/NW-HP-002.PeppolBIS.TDD-C3.xml`.
* C5 validates the received TDD against applicable schematrons, files
  * `supporting-files/NW-HP-002.PeppolBIS.TDD-C2.validation.xml` and
  * `supporting-files/NW-HP-002.PeppolBIS.TDD-C3.validation.xml`.

### Message-level status

* C3 sends positive MLS to C2 (file `sample-results/NW-HP-002.PeppolBIS.MLS-C3.xml`)
* C5A sends positive MLS to C2 (file `sample-results/NW-HP-002.PeppolBIS.MLS-C5A.xml`)
* C5B sends positive MLS to C3 (file `sample-results/NW-HP-002.PeppolBIS.MLS-C5B.xml`)

### Make results available to C1/C4/C6 (out of scope of Testing Scenario)

* Invoice receiver's side
    * C3 generates and sends invoice data available to C4.
    * C3 makes received invoice and TDD available to C4.
    * C3 makes results as confirmed available to C4
* Invoice sender's side
    * C2 makes generated invoice and TDD available to C1.
    * C2 makes received outcome of transmissions available to C1.
* Tax Administration's side
    * C5 makes received TDD available to C6.
    * C5 makes results as confirmed available to C6