
# Peppol ViDA Pilot Testing - Master Data

## Company Master Data

Generated invoices use a set of fictitious buying and selling entities from all jurisdicitions in the ViDA Pilot project.

Each company master data record uses a full set of syntactically valid (but fictitious) field values.

### Overview table
The following table is an overview of current companies used:


Role|VAT-ID|Business Name|Tax Jurisdiction|City|Participant ID (Peppol Playground)
----|------|-------------|----------------|----|--------------------
Seller|NL123456789B01|Verkoper Voorbeeldbedrijf B.V.|NL|Den Haag|9913:001109-vidapilot.NL123456789B01
Seller|SE556123456701|Sverige Seller Business AB|SE|Stockholm|9913:001109-vidapilot.5561234567
Seller|ATU99887766|AT-Verkauf GmbH|AT|Wien|9913:001109-vidapilot.ATU99887766
Seller|FI12345678|Suomi Myynti Oy|FI|Helsinki|9913:001109-vidapilot.FI12345678
Seller|NO123456785MVA|Norge Salg AS|NO|Oslo|9913:001109-vidapilot.NO123456785MVA
Seller|DK87654321|Danmark Salg A/S|DK|København V|9913:001109-vidapilot.DK87654321
Buyer|FI12345671|Ostaja Finland Oy|FI|Helsinki|9913:001110-vidapilot.FI12345671
Buyer|NO123456785MVA|Kjøper Norge AS|NO|Oslo|9913:001110-vidapilot.NO123456785MVA
Buyer|ATU12345679|Österr. Abnehmer GmbH|AT|Wien|9913:001110-vidapilot.ATU12345679
Buyer|DK12345674|Køber Danmark ApS|DK|København|9913:001110-vidapilot.DK12345674
Buyer|SK2021234567|Slovenský Príklad s.r.o.|SK|Bratislava|9913:001110-vidapilot.SK2021234567

### Scope of fields and records

Additionally, local identifiers (as required) are available.

For sellers, also payment information (SEPA IBANs) are generated.

The set of fields is expected to be extended as more test scnearios are implemented.

The set of records is expected to extend as more tax jurisdiction are added to the project.
