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

The Air Waybill document can be re-created at any moment as all required information are within the data model and can be retrieved using the linked data (see the conceptual data model in the Design Principles documentation). 
 <p align="center">
 <img src="https://user-images.githubusercontent.com/58464775/161540123-7ca41e43-775d-4f1e-a31f-e7c2ae79551b.png">
</p>

 
# Data model

Naturally the `Waybill` object is at the center of the data model when the Air Waybill is concerned, whether we refer to the *paper* or *electronic* waybill.

The `WaybillLineItem` object is also necessary, linked to `Waybill` object, to properly record the information at Air Waybill level. The line items as used in the Air Waybill cannot always be linked to actual `Piece` objects as the level of information required does not always reflect the physical goods. This is because we can have discrepancy between actual goods transported and rates as they are defined.

Also it is possible that all accurate piece details are available at the the Waybill.
