// P02 - Arrange handover from Shipper

Process where all preparations are made on Shipper's end and on Forwarder's end to handover the shipment to Forwarder.

# 01. Arrange Pick up or Self Delivery of Freight

Forwarder validates data of the TransportMovement, a PATCH can be done if necessary.

# 02. Commercial invoice and packing lists and any certificates

# 03. Labelling freight

Human action, can be done by the shipper, by the trucker on pickup or by the forwarder on arrival at warehouse. UPID is defined for each piece.

# 04. Associate unique piece level information with forwarding order

Piece are udpated with UPID information and any additional details

## API interaction

| 1R Server | Stakeholder | API Calls | LogiticsObject | Details |
| --- | --- | --- | --- | --- |
| Shipper or Forwarder | Forwarder | PATCH | Piece | Update UPID property on Piece |


