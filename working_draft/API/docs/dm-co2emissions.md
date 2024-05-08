# Requirements
CO2 Emissions transparency is an essential topic in order to move toward a more sustainable industry. IATA has been addressing CO2 Emissions measurement methodology, joint with ICAO, in the Recommended Practice 1678, more details can be found on IATA’s website dedicated page: https://www.iata.org/en/programs/cargo/sustainability/carbon-footprint/  
Our objective is to provide necessary information in the data model to be able to calculate or predict CO2 emissions for transport movements. Required information relate to:
- Typical CO2 coefficient 
- Distance of the transport movement, calculated and measured
- Fuel consumed, calculated and measured
- Method used for calculation of the CO2 emissions
# Chosen approach in the data model
To fulfil these requirements, it has been decided to add relevant data properties in the model on the Transport movement and Transport Means.
Details about the method used for calculation are to be managed outside of the data model. The data model needs to ensure that all required information are recorded and available.
# Impacts and updates on the data model
A few data properties are added on TransportMeans and TransportMovement. A new object CO2Emissions is added as well as depicted below:]

 <p align="center"><img src="https://user-images.githubusercontent.com/58464775/161542962-673fb079-7f30-44f8-9485-36a519b17e2b.png"></p>
