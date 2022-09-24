Google and Facebook are known to have humungous knowledge graphs; and so does Airbnb. So, what are they? and how are they designed?

Knowledge Graphs are just super-structured information collated from all different data sources. At Airbnb, they power Search, Discovery, and Trip Planner products.

Knowledge Graphs power sophisticated queries like

- find cities that host football matches in July and August and are known for para-gliding
- find a neighborhood in LA where Huts or Private Islands are available in the upcoming summer.

## Key Components

The knowledge graph system has three critical components: Storage, API, and Storage Mutator.

### Graph Storage

Airbnb collates all the structured information and stores it in a relational database having one table to store all the nodes and another table to store all the edges.

Each node in the graph could have a different schema. For example, the location could have a name and GPS coordinates, while the Event would have a title, data, and venue.

Each edge in the graph will hold the types of nodes it can connect to which ensures strong data integrity. For example, an edge "landmark-in-a-city" can connect a landmark and a city.

Airbnb chose to not use GraphDB because of its operational overhead. The team had much higher confidence in relational databases and their capability in managing them.

### Graph API

Query API layer exposes a JSON-based query structure that can be used by clients to interact with the Knowledge Graph.

The JSON query is converted to SQL and fired on the database to get the desired information.

### Storage Mutator

We may think the best way for the Knowledge Graph to remain updated with any changes happening in other systems is to expose an updated API. But that would be too slow and expensive.

Hence, a better way to design this is to ingest bulk updates through Kafka. Updates coming from other systems are put in the Kafka and then the mutator updates the knowledge graph by consuming the events.

## Offline Processing

Not every service wants to synchronously query the graph, for example, the search might want to run an offline ranking job. Querying the graph every time will be inefficient and hence there is a periodic job that exports the entire graph database.

This export is then consumed by the services for offline processing.