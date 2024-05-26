# CyberattackAzure
If you are having trouble with running the log query or displaying map query in the sentinel:

Run Log Query:
FAILED_RDP_WITH_GEO_CL
| parse RawData with * "latitude:" Latitude ",longitude:" Longitude ",destinationhost:" DestinationHost ",username:" Username ",sourcehost:" SourceHost ",state:" State ", country:" Country ",label:" Label ",timestamp:" Timestamp
| project Latitude, Longitude, DestinationHost, Username, SourceHost, State, Country, Label, Timestamp

Sentinel to display Map:
FAILED_RDP_WITH_GEO_CL
| parse RawData with * "latitude:" Latitude ",longitude:" Longitude ",destinationhost:" DestinationHost ",username:" Username ",sourcehost:" SourceHost ",state:" State ", country:" Country ",label:" Label ",timestamp:" Timestamp
| project Latitude, Longitude, DestinationHost, Username, SourceHost, State, Country, Label, Timestamp
| summarize event_count=count() by SourceHost, Latitude, Longitude, Country, Label, DestinationHost 
| where DestinationHost != "samplehost"
| where SourceHost != ""
