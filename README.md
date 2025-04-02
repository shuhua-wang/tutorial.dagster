# tutorial.dagster
Tutorial on how to use dagster to build a data pipeline

## Main Concepts

- **Asset**: a logical unit of data such as a table, dataset, or machine learning model.
- **Job**: a subset of **assets**.
- **Config**: a set schema applied to a Dagster object that is input at the time of execution.
- **Resource**: a configurable external dependency, used to manage connections to external systems.
- **IO Manager**: defines how data is stored and retrieved between the execution of **assets** and **ops**.
- **Schedule**: a way to automate **assets** or **jobs** to occur on a specified interval.
- **Sensor**: a way to trigger **assets** or **jobs** when an event occurs.
- **Definitions**: a top-level construct that contains references to all the objects of a Dagster project, including
  - assets
  - jobs
  - resource
  - io manager
  - schedule
  - sensor
- **Code Location**: a collection of **Definitions** deployed in a specific environment.


The relation maps of Dagster concepts:

```mermaid
flowchart TD
id1(Config) -- used by --> id2 & id3 & id4 & id5

subgraph "`**CORE ASSETS**`"
id4(Asset):::assetclass -- a selection of assets --> id5(Job):::jobclass
classDef assetclass fill:#f96
classDef jobclass fill:#f96
end

subgraph "`**TRIGGERS**`"
id5 -- referenced by --> id2(Sensor):::sensorclass & id3(Schedule):::scheduleclass
classDef sensorclass fill:#0f0
classDef scheduleclass fill:#0f0
end

subgraph "`**RESOURCES**`"
id6(Resource):::resourceclass & id7(IO Manager):::iomgr -- used by --> id4
classDef resourceclass fill:#ffccbc
classDef iomgr fill:#ffccbc
end

id2 & id3 & id4 & id5 & id6 & id7 -- defined in --> id8(Definitions):::definitionclass
classDef definitionclass fill:#b6e1ff
id8 -- deployed into --> id9(Code Location)
```
