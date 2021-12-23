# deno-neo4j-lite-client

This is an **unofficial** [Neo4j](https://neo4j.com/) driver/client for Deno.
It is derived from the official [`neo4j-driver-lite`](https://github.com/neo4j/neo4j-javascript-driver/tree/4.4/packages/neo4j-driver-lite),
and has mostly the same code with minor changes to the imports, and with some
dependencies swapped for versions from the Deno Standard Library.

This driver has no dependencies other than the Deno standard library.

## Usage example.

If you want to try this example, first start a Neo4j instance using Docker:

```
docker run --rm -p 7687:7687 -e NEO4J_AUTH=neo4j/driverdemo neo4j:4.4
```

You'll probably also want to create some data first.

Here is how to query data:

```typescript
import neo4j from "https://deno.land/x/neo4j_lite_client@4.4.1-preview/mod.ts";
const URI = "bolt://localhost:7687";
const driver: neo4j.Driver = neo4j.driver(URI, neo4j.auth.basic("neo4j", "driverdemo"));
const session = driver.session();

const results = await session.run("MATCH (n) RETURN n LIMIT 25");
console.log(results.records);

await session.close();
await driver.close();
```

## Auto-generation details

This driver was auto-generated. You can see the generation script at
https://github.com/bradenmacdonald/neo4j-javascript-driver/tree/deno-driver/packages/neo4j-driver-deno

I am discussing this with Neo4j to see if they want to make some or all of it
official and incorporate it into the upstream repository.
