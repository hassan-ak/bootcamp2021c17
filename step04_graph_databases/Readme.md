# Step04 - Graph Database

## Class Notes

### Introduction

- [Graph Databases for Dummies Book](https://neo4j.com/graph-databases-for-dummies/)

  - Relational Database

    - In relational database there are tables and each table is connected to other table using foreign keys. In order to do a query we join tables using foreign key. Relational databases are nor scaleable enough and they are not suitable for internet scale applications.

  - noSQL database

    - To overcome the issue of scalabilty with relational datbase noSQL databases were developed where complete row is stored as a single entity but it lost the connection between different data items.

  - Graph Database
    - In modern applications data is interconnected and that is the reason for Graph databases.
    - A graph database uses highly inter-linked data structures built from nodes, relationships, and properties.

- [Cyper Queries](https://neo4j.com/developer/cypher/querying/)

  - (p:Person) such that () represents a node, p a variable and Person a label
  - [:LIKES] such that [] is arelation and LIKES a label
    - -> is used for direction
  - For storing data `CREATE (p:Person)-[:LIKES]->(t:Technology)`
  - For quering data `MATCH (p:Person)-[:LIKES]->(t:Technology)` if direction unknown dont add -> just simple -
  - When Nodes and relations has labels `(p:Person {name: "Jennifer"})-[rel:LIKES]->(g:Technology {type: "Graphs"})`
  - To query data with out speciying node properties and limits

    ```
    MATCH (p:Person)
    RETURN p
    LIMIT 1
    ```

  - To query data with speciying node properties

    ```
    MATCH (tom:Person {name: 'Tom Hanks'})
    RETURN tom
    ```

  - To query data along with relations

    ```
    MATCH (:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie)
    RETURN movie
    ```

  - To query data along with relations with only few properties

    ```
    MATCH (:Person {name: 'Tom Hanks'})-[:DIRECTED]->(movie:Movie)
    RETURN movie.title
    ```

  - We can rename output data as we chose

    ```
    MATCH (tom:Person {name:'Tom Hanks'})-[rel:DIRECTED]-(movie:Movie)
    RETURN tom.name, tom.born, movie.title, movie.released
    ```

    can be modified as

    ```
    MATCH (tom:Person {name:'Tom Hanks'})-[rel:DIRECTED]-(movie:Movie)
    RETURN tom.name AS name, tom.born AS `Year Born`, movie.title AS title, movie.released AS `Year Released`
    ```

  - Example

    ```
    MATCH (p:Person {name: "Tom Hanks"})-[:DIRECTED]->(m:Movie)
    RETURN m.title, m.released
    ```

  - Working with queries we can exclude few results and also increase the loop for search

    ```
    MATCH (a:Person {name:'Alice'})-[:FRIEND_OF*1..2]->(p:Person)
    WHERE a <> p
    RETURN p
    ```

  - Working with queries we can exclude the loop for search

    ```
    MATCH (a:Person {name:'Alice'})-[:FRIEND_OF*2]->(p:Person)
    WHERE a <> p
    RETURN p
    ```

  - Working with queries we can build bigger patterns

    ```
    MATCH (a:Person {name:'Alice'})-[:FRIEND_OF*1..2]->(p:Person)-[:BOUGHT]->(prod:Product)
    WHERE a <> p
    RETURN prod
    ```

- [Cyper Updates](https://neo4j.com/developer/cypher/updating/)

- [Sandbox to do practice on Movie Database](https://neo4j.com/sandbox/)
