---
title: Use Copilot Connectors with Work IQ APIs
description: Learn how Copilot connectors provide connected enterprise context through Work IQ MCP, A2A, and REST APIs.
author: jasonjoh
ms.author: jasonjoh
ms.topic: concept-article
ms.localizationpriority: medium
ms.date: 11/18/2026
---

<!-- markdownlint-disable MD024 -->
<!-- cSpell:ignore Rovo workiq COSWEP -->

# Use Copilot Connectors with Work IQ APIs

[Work IQ](/microsoft-365/copilot/extensibility/work-iq) is a workplace intelligence layer that helps agents reason over organizational and business data, context, and tools. It builds semantic understanding across Microsoft 365 and external systems, with permission-aware governance. By combining chat, context, tools, and workspaces, Work IQ supports high-volume, multistep interactions across frameworks and runtimes through standard protocols, including MCP, A2A, and REST.

**Copilot Connectors extend Microsoft 365 workplace intelligence to connected enterprise sources, enabling agents to access and reason over business information across an organization’s digital estate.** Copilot Connectors configured in Microsoft 365 Copilot automatically participate in Work IQ APIs.

> [!NOTE]
> Not every Copilot Connector configured in Microsoft 365 Copilot is available through Work IQ. Connector participation might be limited by data sensitivity requirements or partner agreements.

## Prerequisites

- [Enable Work IQ for your organization.](/microsoft-365/copilot/extensibility/work-iq/enable-work-iq)
- Set up [synced connectors](prebuilt-connectors-overview.md) or [federated connectors](federated-connectors-overview.md) in Microsoft 365 Copilot.

## How Copilot Connectors work with Work IQ

Copilot Connectors, both synced and federated, participate in Work IQ APIs when they’re available to the signed-in user and connected by that user as data sources in Microsoft 365 Copilot Chat. No additional user setup for Work IQ is required.

The following image shows an example of connectors enabled by a user in Microsoft 365 Copilot chat.

:::image type="content" source="media/connectors-in-work-iq-apis/copilot-chat-sources.png" alt-text="Screenshot of the Sources settings in Microsoft 365 Copilot Chat, showing Confluence, Rovo, and Salesforce among the available sources.":::

Copilot Connectors participate in Work IQ through the interface your agent or application uses. The following sections describe connector support and show request and response examples for each interface.

## Work IQ MCP

[Work IQ MCP](/microsoft-365/copilot/extensibility/work-iq/mcp/overview) provides tools that enable agents to read, create, update, and delete entities across Microsoft 365 and enterprise systems connected through Copilot Connectors, invoke Microsoft 365 Copilot for natural-language reasoning, retrieve grounding content, and discover API schemas through a single MCP endpoint.

### Ask

Use `ask` when your application needs a synthesized answer from Microsoft 365 Copilot. Include the connector source related information you want Copilot to consider in the `question`.

#### Example

This example asks Copilot to summarize work that needs your attention, including relevant information from connected enterprise sources.

##### Request

[Open this example in the Interactive Demo](https://aka.ms/copilot.dev?page=%2Fwork-iq%2Fmcp&server=workiq-remote&tool=ask&args=%7B%22question%22%3A%22Catch+me+up+on+the+work+items+I+need+to+address%2C+including+relevant+information+from+my+connected+enterprise+sources.%22%7D)

```json
{
  "method": "tools/call",
  "params": {
    "name": "ask",
    "arguments": {
      "question": "Catch me up on the work items I need to address, including relevant information from my connected enterprise sources."
    }
  }
}
```

##### Response

The following response is illustrative. The answer and any source references are shortened for readability.

```json
{
  "response": "Two Jira issues are still open. An email from the project lead says one is blocking release testing, and a Teams discussion notes that the fix is expected this week. ...",
  "conversationId": "cc7d6f5202cb4c5b814b120440e48ede"
}
```

### Retrieve

Use `retrieve` when your agent needs source content and metadata to analyze, compare, or summarize. Set `strategy` to `copilot` to search connected enterprise sources. The default `grounding` strategy searches only Microsoft 365 indexed content.

#### Example

In this example, the `query` parameter asks Work IQ to find work items that need attention and gather relevant context from connected sources.

[▶ Open this example in the Interactive Demo](https://aka.ms/copilot.dev?page=%2Fwork-iq%2Fmcp&server=workiq-remote&tool=retrieve&args=%7B%22query%22%3A%22Find+work+items+that+need+attention%2C+including+Jira+issues+and+follow-ups+in+emails+and+chat.%22%2C%22strategy%22%3A%22copilot%22%7D)

##### Request

```json
{
  "method": "tools/call",
  "params": {
    "name": "retrieve",
    "arguments": {
      "query": "Find work items that need attention, including Jira issues and follow-ups in emails and chat.",
      "strategy": "copilot"
    }
  }
}
```

##### Response

The following excerpt shows selected results. Content and source metadata are shortened for readability.

```json
{
  "content": [],
  "structuredContent": {
    "application/vnd.ms-workiq.retrieval": {
      "results": [
        {
          "id": "h1",
          "markdown": "- **Re: Follow-up on bulk import issue** ... The customer agreed to receive an update by November 20 and plans a technical review on November 24. ...",
          "webUrl": "https://outlook.office.com/mail/..",
          "entityType": "Emails",
          "resourceMetadata": {
            "email": {
              "subject": "Re: Follow-up on bulk import issue",
              "sentTime": "11/11/2026"
            }
          }
        },
        {
          "id": "h5",
          "markdown": "- **Fabrikam issues followup** ... The bulk-import duplicate-record issue is tracked in Jira as COSWEP-246. The fix is undergoing validation, and a customer-safe workaround hasn't been confirmed. ...",
          "entityType": "Chats",
          "resourceMetadata": {
            "chat": {
              "title": "Fabrikam issues followup"
            }
          }
        },
        {
          "id": "h9",
          "markdown": "- **Rovo** ... COSWEP-246: Duplicate records created when bulk import requests are retried. Status: In Progress. ...",
          "entityType": "ThirdParty"
        }
      ],
      "resultCount": 9,
      "stoppedReason": "completed"
    }
  },
  "isError": false
}
```

The payload returns grounding content and source metadata in `results`. Use each `results[].markdown` value for model grounding, and use metadata from that same result to identify and link to the source.

### Entity and schema tools

Use MCP entity and schema tools when your agent needs to inspect a specific connected enterprise source record or perform a supported read or write operation, often as a follow-up to `retrieve`.

Use `search_paths` to discover available connector paths and operations, and `get_schema` to inspect the inputs for an operation.

Connector tool paths follow this pattern:

```text
/connectors/{connectorID}/tools/{tool-name}
```

Invoke `function` operations with `call_function` for reads and `action` operations with `do_action` for writes. See the [Work IQ MCP tool reference](/microsoft-365/copilot/extensibility/work-iq/mcp/tool-reference) for tool parameters and request and response formats.

#### Discover connector tools

This example searches for Jira issue tools.

##### Request

```json
{
  "method": "tools/call",
  "params": {
    "name": "search_paths",
    "arguments": {
      "query": "jira issues"
    }
  }
}
```

##### Response

```json
{
  "paths": [
    {
      "path": "/connectors/<connectorID>/tools/searchJiraIssuesUsingJql",
      "operations": ["function"]
    },
    {
      "path": "/connectors/<connectorID>/tools/editJiraIssue",
      "operations": ["action"]
    }
  ]
}
```

The preceding paths illustrate the response format. Tool names and supported operations depend on the connected source.

#### Read connector data

After discovering the path and inspecting its schema with `get_schema`, call `call_function` with the relative path and the required inputs. This example searches Jira issues assigned to the current user.

##### Request

```json
{
  "method": "tools/call",
  "params": {
    "name": "call_function",
    "arguments": {
      "functionUrl": "/connectors/<connectorID>/tools/searchJiraIssuesUsingJql",
      "jsonBody": {
        "cloudId": "<cloud-id>",
        "jql": "assignee = currentUser() ORDER BY updated DESC",
        "maxResults": 100,
        "fields": [
          "summary",
          "status",
          "priority",
          "assignee"
        ],
        "view": "compact"
      }
    }
  }
}
```

##### Response

The following excerpt shows the operation data returned for one issue. The response can include more issues and pagination information.

```json
{
  "key": "COSWEP-246",
  "fields": {
    "summary": "Duplicate records created when bulk import requests are retried",
    "status": {
      "name": "In Progress"
    },
    "assignee": {
      "displayName": "John Doe"
    },
    "priority": {
      "name": "High"
    }
  }
}
```

If the response includes a `nextPageToken`, use it to request the next page until `isLast` is `true`.

For a write operation, use `do_action` with a path whose supported operation is `action`. Inspect the schema first and provide the required inputs.

## Work IQ A2A

By using [Work IQ A2A](/microsoft-365/copilot/extensibility/work-iq/a2a/overview), an agent can delegate a task to Microsoft 365 Copilot. Copilot conversations through A2A can use Copilot Connector sources that the signed-in user can access and connect to in Microsoft 365 Copilot Chat. This functionality works like conversations through Work IQ MCP `ask`. Send the task as a user message and use the returned response in your agent.

## Work IQ REST API

By using [Work IQ REST API](/microsoft-365/copilot/extensibility/work-iq/rest/overview), an application can create and continue multiturn conversations with Microsoft 365 Copilot. These conversations can use Copilot Connector sources that the signed-in user can access and connect to in Microsoft 365 Copilot Chat. This functionality works like conversations through Work IQ MCP `ask`. Use the returned conversation messages and attributions in your application.

## Governance

Existing connector availability and administrative controls in the Microsoft 365 admin center continue to apply to Work IQ. Organizations have a consistent way to manage access to connected enterprise systems.

Administrators can manage which connectors are enabled and available to users through their existing Copilot connector management experiences, as described in [Manage federated connector availability](manage-federated-connectors.md) and [Deploy connectors in the Microsoft 365 admin center](deployment-overview.md).

In addition, Work IQ MCP provides [Rego-based policy governance](/microsoft-365/copilot/extensibility/work-iq/mcp/policy-governance-mcp) to control access to connectors through Work IQ APIs. Connector access is enabled by default. Administrators can explicitly enable or disable connector participation in Work IQ paths through tenant-level policies.

These controls complement existing authentication and user permissions, ensuring agents can access only the enterprise information and capabilities available to the user.

## Related content

- [Microsoft Work IQ API overview](/microsoft-365/copilot/extensibility/work-iq/api-overview)
- [Enable your tenant for Work IQ](/microsoft-365/copilot/extensibility/work-iq/enable-work-iq)
- [Work IQ MCP overview](/microsoft-365/copilot/extensibility/work-iq/mcp/overview)
- [Work IQ A2A quickstart](/microsoft-365/copilot/extensibility/work-iq/a2a/quickstart)
- [Try the APIs in the Interactive Demo](https://aka.ms/copilot.dev)
