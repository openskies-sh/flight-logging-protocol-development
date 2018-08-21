# README 

This is the development version of the GUTMA protocol. The aim of this repository is to develop and build on the on the published flight logging protocol. 


## Read First
The [published](https://github.com/gutma-org/flight-logging-protocol) protocol takes a longer time to update since it has to go through the review cycle. The goal of this repository is to advance the published protocol by doing more tests and providing a flexible way to address new and existing concerns as the UTM ecosystem develops. The best way to engage with this is to review the protocol document, the goals and differences and open issues in this repository.

### Key Differences 

This protocol is backwards-compatible so entities using the production version protocol will not need to make any changes to their software. This protocol however, introduces a new component that is a additional output in GeoJSON. This GeoJSON component is called "Standard Log" and the original log format introduced in the production version is kept as is called "Extended Log". In addition to the Latitude / Longitude that is specified in GeoJSON, the standard log asks that additional attributes such as ground speed, altitude and a timestamp be written in the properties. Any other information can be added as properties and is left to the operator. 

### Background

The [published](https://github.com/gutma-org/flight-logging-protocol) "production" version of GUTMA protocol is a terrific start. However, there are some open questions still. These issues (detailed below) are complicated and dont have a clear answer at the moment. Therefore, this development version of the protocol was created to provide a platform to iterate, debate and test ideas to move the protocol forward as the requirements from drone operations and operators evolve.

1. _Flexibility_: A common comment upon review of the production version of the protocol is that it is too flexible. In that, the protocol does not enforce any requirement on how logging should be done the data units and formats to be used. This has led to individual companies extending the protocol to suit their use case, which is to be expected and encouraged. Since there is no instructions on how to log and what to log, we have a situation where two operators logging the same data log in different formats and fashion. This opens up a difficult set of questions around understanding of what is logged, who will make the interpretations, interoperability etc. 
2. _Use Case_ : Flight logging is actually two different set of things: 1) In-flight live / realtime telemetry and 2) Post-flight logging. These are two different use cases. Realtime telemetry might be used during operations by the operator but post-flight logging could be used to share the flight data externally. These are different use cases and the production protocol does not handle it well. 
3. _Standardization_: The production version of the protocol simply has one block to log any information the operator wants to keep track of. This is  problematic especially in a scenario where parts (but not all) of the log have to be shared with third parties (public or private). Therefore, this development version specifies splitting the log into 1) Standard logging 2) Extended / capability specific logging. The Standard logging is a GeoJSON FeatureCollection with additional properties. By making the distinction between standard logging (in GeoJSON) and extended logging as specified in the production version, we are ensuring that standard logs can be shared widely using a OGC standard and the extended logs can still be used. The goal of the the standard log is to be used for "post-flight" sharing while the extended log used for in-flight telemetry. 
4. _Public Vs Private data_: The production version protocol does not differentiate on the nature of the data. It is very difficult to split data once logged. "Standard log" and "Extended log" solves this problem. The Standard log is GeoJSON so at the very least a set of latitude longtiude is required and any other additional information that the operator may want to share publicly. Additionally, the "standard log" is a GeoJSON object which means that there are a number of existing tools that be used with it (e.g. [awesome-geojson](https://github.com/tmcw/awesome-geojson)). 
5. _Partial and Batch logging_: "Standard log" and "Extended log" is compatible with partial and batch logging, in case of partial or batch logging, as long as the GeoJSON object is valid, the protocol does not mandate what is to be logged so a series of points can be logged between a time duration. 
6. _Compliance_: By adopting a minimal "standard logging" in GeoJSON, operators implementing this protocol can pre-empt any future legislation around standardization of protocols by adopting a widely accepted format of reporting. 
