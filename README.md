# Semantic layer using data governance application
Using a data governance application output, to use in a semantic layer, which can be used in a Model Context Protocol (MCP) server to have a Large-Language Model (LLM) answer questions on data in a database (PostgreSQL). In the situation that:
* the database is easily interpretable by humans and LLMs;
* the database has meaningless technical table- and column names, thereby is expected to be harder interpretable by humans and LLMs

## The database is easily interpretable by humans and LLMs.

!["Human oriented data model wrt technical table names."](./human/human%20oriented%20data%20model.png "Human oriented data model wrt technical table names.")

For implicity sake, the business- logical- and technical layer data objects are kept 1:1. Logical- or technical objects are aimed to be extended.

## The database is easily interpretable by humans and LLMs.

!["Technical oriented data model, with unclear table names."](./technical/technical%20data%20model.png "Technical oriented data model, with unclear table names.")

Here you see that 'customer' table is not existing. But the table is named 'kirstopher', which should make it meaningless or incorrect interpreted by a human or LLM if searching for customer (data).

# Running the MCP server
Mind the different `./publisher.config.<type>.json` used, since multi-project config file not well supported yet.

```bash
# Unix

# Human and LLM easy @ port 4040
docker run -p 4000:4000 -p 4040:4040 -v ./publisher.config.human.json:/publisher/publisher.config.json -v ./human:/publisher/human ms2data/malloy-publisher

# Harder, technical data objects / table- and columns @ 4041
docker run -p 4001:4000 -p 4041:4040 -v ./publisher.config.technical.json:/publisher/publisher.config.json -v ./technical:/publisher/technical ms2data/malloy-publisher

```