# Purpose

# Master Operating Plan
Mention version of MOP used (CiQ current working version)

# the link between activities and ONE Record actions

## Shipper provides shpiment details
In this step the Shipper provides initial shipment details to its freight forwarder.

### ONE Record actions
As Shipper provides shipment details, it is the equivalent of the SLI. The Shipper or the Forwarder on its behalf, creates Product, Item and Piece objects, including ULD if relevant and any Special cargo subtype for Live Animals or Dangerous Goods to further describe goods to transport. SecurityDeclaration object can be created as well if relevant
Parties are created as well (if not already existing), are required at minimum the Consignee (Shipper) and Consignor details.

Are included as well: handling instructions directly in the Piece details, ExternalReference if applicable (for rerefence documents) 

If Shipper hosts a 1R server he needs to make sure teh Forwarder has proper access to data

*Values to declare for carriage and customs are not on Piece*

### API interaction

| 1R Server | Stakeholder | API Calls | LogiticsObject | Details |
| --- | --- | --- | --- | --- | --- |
| Shipper or Forwarder | Shipper or Forwarder | POST | Product | Minimum Product details, including HS codes: hsCode, description |

| Shipper or Forwarder | Shipper or Forwarder | POST | Item | Minimum Item details including link to Product: itemQuantity, ofProduct |
| Shipper or Forwarder | Shipper or Forwarder | POST | Piece | Minimum Piece details to define the goods. Includes link to Product or Item: contentProducts/containedItems, goodsDescription, slac, specialHandlingCodes, textualHandlingInstructions, declaredValue |
| Shipper or Forwarder | Shipper or Forwarder | POST | SecurityDeclaration | Security details available at this stage |
| Shipper or Forwarder | Shipper or Forwarder | POST | ULD | Optional, if relevant |
| Shipper or Forwarder | Shipper or Forwarder | PATCH | Product and/or Item | Add backlinks to relevant objects (to Piece or Item>Product) |

## Receive Forwarding Order from shipper & check security status
In this step the Forwarder receives data from the Shipper

### ONE Record actions
Forwarder creates the Waybill objects (House) and Shipments based on the details provided by the Shipper.

### API interaction

| 1R Server | Stakeholder | API Calls | LogiticsObject | Details |
| --- | --- | --- | --- | --- | --- |
| Forwarder | Forwarder | POST | Waybill | House Waybill object: arrivalLocation, departureLocation, involvedParties (Shipper and Forwarder), waybillType (House), waybillNumber, declaredValueForCustoms, declaredValueForCarriage |
| Forwarder | Forwarder | POST | Shipment | Shipments details and link to Waybill object: waybill, insurance, involvedParties, totalGrossWeight, totalDimensions, goodsDescription |
| Forwarder | Forwarder | PATCH | Waybill | Add backlink Waybill>Shipment |

