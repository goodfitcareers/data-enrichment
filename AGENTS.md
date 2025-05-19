Overview
This repository defines a LangGraph-based “data enrichment agent.”
The agent currently uses web search and site scraping tools to gather
information. We want to extend it so it ingests new documents and writes
structured results to a database.

Development Workflow
Run linters and formatters
Execute make lint before committing any changes.
This runs ruff (formatting & linting) and mypy for type checking.

Run tests
Execute make test (or python -m pytest) to run unit tests.
Integration tests are under tests/integration_tests; run them after
modifying the graph or tools.

Documentation
Update README.md whenever configuration options, prompts, or usage
instructions change.

Key Implementation Tasks
Add document ingestion and database update tools

In src/enrichment_agent/tools.py, implement
load_new_docs(directory: str) to read and return text from new documents.

Implement write_to_database(info: dict, conn_str: str, table: str) to
insert or update rows with the final info.

Extend configuration

Update src/enrichment_agent/configuration.py to include settings for
docs_directory and db_conn_str.

Revise prompts

Modify src/enrichment_agent/prompts.py to remove references to the
Search tool and describe the new document ingestion tool instead.

Update graph

In src/enrichment_agent/graph.py, bind the new tools
(load_new_docs, write_to_database) and update the ToolNode.

Insert a node that writes results to the database after reflection.

Adjust state if necessary

If document metadata or DB handles are required, extend
src/enrichment_agent/state.py accordingly.

Update tests

Add unit tests for the new tool functions.

Adapt tests/integration_tests/test_graph.py so the graph runs without
web search and confirms database writes.

Repository Structure
src/enrichment_agent/ – main agent code (graph.py, tools.py, etc.)

tests/ – unit and integration tests

langgraph.json – graph configuration for LangGraph Studio

Follow these guidelines and keep tests passing to maintain consistency
while implementing the new document-ingestion workflow.
