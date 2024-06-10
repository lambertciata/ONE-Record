# Requirements
From a *paper* perspective the Air Waybill requirements are described in Cargo Services Conference Resolutions Manual (CSCRM) in Resolution 600a. Especially all boxes of the paper Waybill are identified with details on how to properly fill in information.

From an *electronic* perspective the Air Waybill relies on (deprecated) Cargo-IMP FWB message and Cargo-XML XFWB message. Discrepancies exist between FWB and XFWB essentially because Cargo-IMP was discontinued in 2014 and context has evolved.

 <p align="center">
<img src="https://user-images.githubusercontent.com/58464775/161540275-fd1d910c-4c5e-420c-a47a-be118ee1ab2e.png"></p>

 
# Chosen approach
Approach needs to be two-fold:
- Firstly we take into account the *paper* requirements, this leads to a mapping that is presented below.
- Secondly the *electronic* requirements lead to a mapping that has been done between XFWB and ONE Record in the corresponding section in the Data Orchestration tab [link]  

## *Paper* Waybill mapping

(to be updated)

|box|Air Waybill requirements|Description/Comment|Data Model mapping|
|---|---|---|---|
|1a|Airline Code Number||in Waybill/waybillPrefix|
|1b|Serial Number||in Waybill/waybillNumber|
|1|Airport of departure||in TransportSegment|
|1c|Issuing Carrier's name and address||in Company details of Carrier|
|1d|Reference to originals|not to be completed||
|1e|Reference to conditions of contracts|up to carrier||
|2|Shipper's name and address||in Company details of Shipper|
|3|Shipper's account number|up to carrier||
|4|Consignee's name and address||in Company details of Consignee|
|5|Consignee's account number|up to carrier||
|6|Issuing Carrier's Agent name and city|Issuing carrier's IATA Cargo Agent |in Company details of Carrier's agent|
|7|Agent's IATA code|IATA code of Cargo Agent. 7-digit IATA code or 7-digit IATA code followed by 3-digit CASS address code and check digit.|in Company details of Carrier's agent|
|8|Account number|up to carrier||
|9|Airport of departure and requested routing||"in TransportSegment| duplicate with 1 "|
|11a|To (by 1st carrier)|IATA 3-letter code of aiport of destination or first transfer point|in TransportSegment/arrivalLocation|
|11b|By 1st carrier|"Name of 1st carrier| full name or IATA 2-character code"|in Company details of Carrier|
|11c|To (by 2nd carrier)|IATA 3-letter code of aiport of destination or second transfer point|in TransportSegment/arrivalLocation|
|11d|By 2nd carrier|"Name of 2nd carrier| full name or IATA 2-character code"|in Company details of Carrier|
|11e|To (by 3rd carrier)|IATA 3-letter code of aiport of destination or third transfer point|in TransportSegment/arrivalLocation|
|11f|By 3rd carrier|"Name of 3rd carrier| full name or IATA 2-character code"|in Company details of Carrier|
|18|Airport of destination|Airport of destination of the last carrier|in Contractual level TransportSegment/arrivalLocation|
|19a/19b|Requested Flight/Date||in Contractual level TransportSegment/transportIdentifier|
|10|Accounting information|Only accounting information required by carriers||
|12|Currency|ISO 3-letter currency code of country of departure|in Price/grandTotal as Unit|
|13|Charge codes - Carrier|Charges codes for carrier|in Price/carrierChargeCode|
|14a/14b|Weight/Valuation charges|Prepaid or Collect|in Shipment/weightValuationIndicator|
|15a/15b|Other charges at Origin|Prepaid or Collect|in Shipment/otherChargesIndicator|
|16|Declared Value for Carriage||in Piece/declaredValueForCarriage|
|17|Declared Value for Customs||in Piece/declaredValueForCustoms|
|20|Insurance||in Shipment/Insurance|
|21|Handling information||"Covered by SpecialHandling| DGD| Live Animals certification| etc."|
|21a|Special Customs Information (SCI)||To be integrated in OCI discussion|
|22a|Number of pieces||derived from Piece|
|22a|Rate combination point (RCP)|IATA 3-letter code of the RCP|Deprecated|
|22b|Gross weight||in Piece/grossWeight|
|22c|kg/lb||in Piece/grossWeight|
|22z|Service Code|up to carrier||
|22d|Rate class||in Ranges/rateClassCode|
|22e|Commodity Item number||in Product/commodityItemNumber|
|22f|Chargeable weight||in Piece/volumetricWeight or Shipment/volumetricWeight|
|22g|Rate/Charge|Applicable rate or charge|in Ranges/amount|
|22h|Total charge|Total charge or discount for each line entry|Calculated value|
|22i|Nature and quantity of goods||"Derived from Piece| Product| Item| or special cargo objects"|
|22j|Total number of pieces||Derived from Piece|
|22k|Total gross weight||Derived from Piece|
|22l|Total||Derived from Piece|
|23|Other charges||in Ratings|
|24a|Prepaid weight charge|"Weight/Volume charge| should correspond to total in 22h or 22l"|Derived from total charge|
|25a|Prepaid valuation charge|Assessment of a valuation charge is dependent on the value declared for carriage|in Ratings|
|26a|Prepaid Tax||in Ratings|
|27a|Due Agent|Used only if agreed locally||
|28a|Due Carrier|Total of prepaid other charges du to carrier||
|29a|Untitled box|||
|30a|Total prepaid|Total of all the prepaid charges above||
|24b|Collect weight charge|"Weight/Volume charge| should correspond to total in 22h or 22l"|Derived/calculated value|
|25b|Collect valuation charge|Assessment of a valuation chargeis dependent on the value declared for carriage|in Ratings|
|26b|Collect Tax||in Ratings|
|27b|Collect charges Due Agent|Total disbursements due to agent|in Ratings|
|28b|Collect charges Due Carrier|Total disbursements due to carrier|in Ratings|
|29b|Untitled box|||
|30b|Total collect|Total of all collect charges above||
|31|Shipper's certification box|"Signature of the shipper (printed| signed or stamped)"|?|
|32a|Carrier executed on|Date of execution of the air waybill |in Waybill Event - Waybill execution (+ Memento trigger)|
|32b|Carrier executed at|Name of the place of execution (airport or city) of the air waybill|in Waybill Event - Waybill execution (+ Memento trigger)|
|32c|Signature of Issuing carrier or its agent|||
|33|For carriers use only at destination|||
|33a|Collect charges in destination current - currency conversion code||in Waybill/destinationCurrencyCode|
|33a|Collect charges in destination current - currency conversion rate||in Waybill/destinationCurrencyRate|
|33b|Collect charges in destination current - amount|"Amount from 30b| converted in destination currency"|Derived from 30b and converted|
|33c|Charges at destination|Charges levied at destination accruing to the last carrier in destination currency|in Waybill/destinationCharges|
|33d|Total collect charges|Sum of 33b and 33c|Sum of other charges|
|34a|Optional shipping information - Reference number|Reference number as per shipper/agent/issuing carrier agreement|in Waybill/optionalShippingRefNb|
|34b|Optional shipping information - Untitled box|up to carrier|in Waybill/optionalShippingInfo|
|34c|Optional shipping information - Untitled box|up to carrier||

| Box                                                    | 1R Objet              | Object Property                                    | Comment                                                                                                                                                                      |
| ------------------------------------------------------ | --------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1A - Airline Code Number                               | Waybill#waybillPrefix | waybillPrefix                                      |                                                                                                                                                                              |
| 1B - Serial Number                                     | Waybill               | waybillNumber                                      |                                                                                                                                                                              |
| 1 - Airport of Departure                               | Waybill               | departureLocation                                  |                                                                                                                                                                              |
| 1C - Issuing Carrier's Name and Address                | involvedParty         | Party                                              | From Party: use partyDetails to capture the carrier's name and address. Use ParticipantIdentifier to specifiy AIR for Airline                                                |
| 1D - Reference to Originals                            | \-                    | \-                                                 |                                                                                                                                                                              |
| 1E - Reference to Conditions of Contracts              | \-                    | \-                                                 |                                                                                                                                                                              |
| 2 - Shipper's Name and Address                         | Waybill               | involvedParty                                      | In Party: use partyDetails to capture the shipper's name and address. Use partyRole to specifiy SHP for Shipper or FFW for Freight Forwarder                                 |
| 3 - Shipper's Account Number                           | \-                    | \-                                                 |                                                                                                                                                                              |
| 4 - Consignee's Name and Address                       | Waybill               | involvedParty                                      | In Party: use partyDetails to capture the consignee's name and address. Use  partyRole to specifiy CNE for Consignee                                                         |
| 5 - Consignee's Account Number                         | \-                    | \-                                                 |                                                                                                                                                                              |
| 6 - Issuing Carrier's Agent Name and City              | Waybill               | involvedParty                                      | In Party: use partyDetails to capture the Issuing carrier's IATA Cargo Agent                                                                                                 |
| 7 - Agent's IATA Code                                  | Waybill               | involvedParty                                      | In Party: use partyDetails to capture the iataCargoAgentCode from Company                                                                                                    |
| 8 - Account Number                                     | \-                    | \-                                                 |                                                                                                                                                                              |
| 9 - Airport of Departure and Requested Routing         | TransportLegs         | departureLocation                                  | Where legNumber is '1'                                                                                                                                                       |
| 11A - To (by 1st carrier)                              | TransportLegs         | arrivalLocation                                    | Where legNumber is '1'                                                                                                                                                       |
| 11B - By 1st carrier                                   | \-                    | \-                                                 |                                                                                                                                                                              |
| 11C - To (by 2nd carrier)                              | TransportLegs         | arrivalLocation                                    | Where legNumber is '2'                                                                                                                                                       |
| 11D - By 2nd carrier                                   | \-                    | \-                                                 |                                                                                                                                                                              |
| 11E - To (by 3rd carrier)                              | TransportLegs         | arrivalLocation                                    | Where legNumber is '3'                                                                                                                                                       |
| 11F - By 3rd carrier                                   | \-                    | \-                                                 |                                                                                                                                                                              |
| 18 - Airport of Destination                            | TransportLegs         | arrivalLocation                                    | Where legNumber is 'greater'                                                                                                                                                 |
| 19A - Requested Flight                                 | TransportLegs         | transportIdentifier                                | Where legNumber is '1'                                                                                                                                                       |
| 19B - Requested Date                                   | TransportLegs         | departureDate                                      | Where legNumber is '1'                                                                                                                                                       |
| 10 - Accounting Information                            | Waybill               | accountingInformation                              |                                                                                                                                                                              |
| 12 - Currency                                          | \-                    | \-                                                 | extract from the currency used in the Waybill                                                                                                                                |
| 13 - Charges Codes - For Carrier Use Only              | Waybill               | carrierChargeCode                                  |                                                                                                                                                                              |
| 14A/14B - Weight/Valuation Charges                     | Waybill               | weightValuationIndicator                           |                                                                                                                                                                              |
| 15A/15B - Other Charges at Origin                      | Waybill               | otherChargesIndicator                              |                                                                                                                                                                              |
| 16 - Declared Value for Carriage                       | Waybill               | declaredValueForCarriage                           |                                                                                                                                                                              |
| 17 - Declared Value for Customs                        | Waybill               | declaredValueForCustoms                            |                                                                                                                                                                              |
| 20 - Insurance                                         | Shipment              | insurance                                          |                                                                                                                                                                              |
| 21 - Handling information                              | Shipment              | specialHandlingCodes + textualHandlingInstructions | Retrieve Handling Information captured for each piece of the shipment                                                                                                        |
| 21A - Special Customs Information (SCI)                | Shipment              | customsInformation                                 |                                                                                                                                                                              |
| 22A - Number of pieces and RCP                         | WaybillLineItem       | pieceCountforRate                                  | Manual data capture                                                                                                                                                          |
| 22B - Gross Weight                                     | WaybillLineItem       | grossWeightForRate                                 | Manual data capture                                                                                                                                                          |
| 22C - Kg/Lb                                            | WaybillLineItem       | grossWeightForRate                                 | Unit of measurement to be specified in unit of Value (see table 1.48 Measureement Unit Code)                                                                                 |
| 22Z - Service Code                                     | Waybill               | serviceCode                                        |                                                                                                                                                                              |
| 22D - Rate Class                                       | WaybillLineItem       | rateClassCode                                      |                                                                                                                                                                              |
| 22E - Commodity Item Number                            | WaybillLineItem       | commodityItemNumberForRate                         |                                                                                                                                                                              |
| 22F - Chargeable Weight                                | WaybillLineItem       | chargeableWeightForRate                            |                                                                                                                                                                              |
| 22G - Rate/Charge                                      | WaybillLineItem       | rateCharge                                         |                                                                                                                                                                              |
| 22H - Total                                            | \-                    | \-                                                 | Calculated value                                                                                                                                                             |
| 22I - Nature and Quantity of Goods                     | WaybillLineItem       | goodsDescriptionForRate + dimensionsForRate        |                                                                                                                                                                              |
| 22J - Total Number of Pieces                           | Shipment              | pieces                                             | Count of Pieces linked to Shipment                                                                                                                                           |
| 22K - Total Gross Weight                               | Shipment              | totalGrossWeight                                   |                                                                                                                                                                              |
| 22L - Total                                            | \-                    | \-                                                 | Calculated value                                                                                                                                                             |
| 23 - Other Charges                                     | Waybill               | otherCharges                                       |                                                                                                                                                                              |
| 24A - Prepaid Weight Charge                            | \-                    | \-                                                 | Calculated value                                                                                                                                                             |
| 25A - Prepaid Valuation Charge                         | Waybill               | declaredValueForCarriage                           |                                                                                                                                                                              |
| 26A - Prepaid Tax                                      | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'P' Prepaid Indicator (see code list 1.5) and otherChargeCode are tax codes related (see code list 1.2)                       |
| 27A - Due Agent                                        | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'P' Prepaid Indicator (see code list 1.5) and entitlement is 'A' Other Charges due Agent (see code list 1.3)                  |
| 28A - Due Carrier                                      | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'P' Prepaid Indicator (see code list 1.5) and entitlement is 'C' Other Charges due Carrier (see code list 1.3)                |
| 29A - Untitled box                                     | \-                    | \-                                                 |                                                                                                                                                                              |
| 30A - Total Prepaid                                    | \-                    | \-                                                 | calculated value: Weight Charge (prepaid) + Valuation Charge (prepaid) + Tax (prepaid) + Total Other Charges Due Agent (prepaid) + Total Other Charges Due Carrier (prepaid) |
| 24B - Collect Weight Charge                            | \-                    | \-                                                 | Calculated value                                                                                                                                                             |
| 25B - Collect Valuation Charge                         | Waybill               | declaredValueForCarriage                           |                                                                                                                                                                              |
| 26B - Collect Tax                                      | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'C' Collect Indicator (see code list 1.5) and otherChargeCode are tax codes related (see code list 1.2)                       |
| 27B - Due Agent                                        | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'C' Collect Indicator (see code list 1.5) and entitlement is 'A' Other Charges due Agent (see code list 1.3)                  |
| 28B - Due Carrier                                      | Waybill               | otherCharges                                       | Sum of otherCharges where chargePaymentType is 'C' Collect Indicator (see code list 1.5) and entitlement is 'C' Other Charges due Carrier (see code list 1.3)                |
| 29B - Untitled box                                     | \-                    | \-                                                 |                                                                                                                                                                              |
| 30B - Total Collect                                    | \-                    | \-                                                 | calculated value: Weight Charge (collect) + Valuation Charge (collect) + Tax (collect) + Total Other Charges Due Agent (collect) + Total Other Charges Due Carrier (collect) |
| 31 - Shipper's Certification Box                       | Waybill               | consignorDeclarationSignature                      |                                                                                                                                                                              |
| 32A - Executed on (Date)                               | Waybill               | carrierDeclarationDate                             |                                                                                                                                                                              |
| 32B - At (Place)                                       | Waybill               | carrierDeclarationPlace                            |                                                                                                                                                                              |
| 32C - Signature of Issuing Carrier or its Agent        | Waybill               | carrierDeclarationSignature                        |                                                                                                                                                                              |
| 33 - For carriers use only at destination              | \-                    | \-                                                 |                                                                                                                                                                              |
| 33A - Currency Conversion Rate                         | Waybill+CurrencyValue | destinationCurrencyRate+CurrencyUnit               |                                                                                                                                                                              |
| 33B - Collect Charges in Destination Currency          | \-                    | \-                                                 | Calculated value: 30A\*33B                                                                                                                                                   |
| 33C - Charges at Destination                           | Waybill               | destinationCharges                                 |                                                                                                                                                                              |
| 33D - Total Collect Charges                            | \-                    | \-                                                 | Calculated value: 33B+33C                                                                                                                                                    |
| 34A - Optional Shipping Information - Reference Number | Waybill               | shippingRefNo                                      |                                                                                                                                                                              |
| 34B - Optional Shipping Information - Untitled Box     | Waybill               | shippingInfo                                       |                                                                                                                                                                              |
| 34C - Optional Shipping Information - Untitled Box     |                       |                                                    |                                                                                                                                                                              |

The Air Waybill document can be re-created at any moment as all required information are within the data model and can be retrieved using the linked data (see the conceptual data model in the Design Principles documentation). 
 <p align="center">
 <img src="https://user-images.githubusercontent.com/58464775/161540123-7ca41e43-775d-4f1e-a31f-e7c2ae79551b.png">
</p>

 
# Data model

Naturally the `Waybill` object is at the center of the data model when the Air Waybill is concerned, whether we refer to the *paper* or *electronic* waybill.

The `WaybillLineItem` object is also necessary, linked to `Waybill` object, to properly record the information at Air Waybill level. The line items as used in the Air Waybill cannot always be linked to actual `Piece` objects as the level of information required does not always reflect the physical goods. This is because we can have discrepancy between actual goods transported and rates as they are defined.

Also it is possible that all accurate piece details are available at the the Waybill.
