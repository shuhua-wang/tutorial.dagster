# tutorial.dagster
Tutorial on how to use dagster to build a data pipeline

## Main Concepts

- **Asset**: a logical unit of data such as a table, dataset, or machine learning model.
- **Job**: a subset of **assets**.
- **Resource**: a configurable external dependency, used to manage connections to external systems.
- **IO Manager**: defines how data is stored and retrieved between the execution of **assets** and **ops**.
- **Definitions**: a top-level construct that contains references to all the objects of a Dagster project, including
  - assets
  - jobs
  - resource
  - schedule
  - sensor
- **Code Location**: a collection of **Definitions** deployed in a specific environment.
- **Schedule**: a way to automate **assets** or **jobs** to occur on a specified interval.
- **Sensor**: a way to trigger **assets** or **jobs** when an event occurs.

The relation maps of Dagster concepts:

```mermaid
flowchart TD
id1(Asset) -- a selection of assets --> id2(Job)
id1 -- defined in --> id3(Definitions)
id2 -- defined in --> id3(Definitions)
id2 -- referenced by --> id4(Schedule)
id4 -- defined in --> id3(Definitions)
id2 -- referenced by --> id5(Sensor)
id5 -- defined in --> id3(Definitions)
id6(Resource) -- used by --> id1
id6 -- defined in --> id3(Definitions)
id3 -- deployed into --> id7(Code Location)
id8(IO Manager) -- used by --> id1
id8 -- defined in --> id3(Definitions)
```
