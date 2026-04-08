---
ms.date: 10/08/2019
title: "Troubleshooting the Enterprise Websites cloud connector"
ms.author: vivg
author: vivg
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: troubleshooting-general
ms.service: copilot-connectors
ms.localizationpriority: medium
description: "Troubleshooting the Enterprise Websites Cloud Microsoft 365 Copilot connector."
---

# Troubleshooting the Enterprise Websites Cloud connector

## Common errors

The following common errors are observed while configuring the connector, or during crawling and their possible reasons.

Detailed Error code | Error message
|:--- |:---|
|6001 | The site that's being tried to index isn't reachable.|
|6005 | The source webpage being tried to index is blocked by robots.txt configuration.|
|6008 | Unable to resolve the DNS.|
|6009 | For all client-side errors (except HTTP 404, 408), refer to HTTP 4xx error codes for details.|
|6013 | The source page that's being tried to index couldn't be found. (HTTP 404 error).|
|6018 | The source page isn't responding, and the request is timing out. (HTTP 408 error).|
|6021 | The source page that's being tried to index has no textual content on the page.|
|6023 | The source page that's being tried to index is unsupported (not an HTML page).|
|6024 | The source page that's being tried to index has unsupported content.|

* Errors 6001-6013 occur when the data source isn't reachable due to a network issue or when the data source itself is deleted, moved, or renamed. Check if the data source details provided are still valid.
* Errors 6021-6024 occur when the data source contains nontextual content on the page or when the page isn't HTML. Check the data source and add this page to the exclusion list or ignore the error.

## Steps to Test Website Access (via API Client)

1. Install the tool.

    - Download and install `Postman` or `Insomnia` or any API client tool of choice on your machine.

2. Create a New Request.
    1. Open the app and click New Request.
    1. Set the HTTP method to GET.
    1. Enter the full website URL (for example, https://example.com/robots.txt).

3. Configure Authentication (if necessary)

    If the site requires authentication:
  
    1. Go to the **Auth** tab.
    1. Select the appropriate type (for example, Basic Auth, OAuth).
    1. Enter credentials or token.

    If no authentication is needed, set Auth to **None**.

4. Add Headers (optional)

    If the connector uses custom headers (User-Agent), replicate them. Click Headers and add:
    - User-Agent
    - Any other headers your connector sends.

5. Send the Request
    1. Click **Send**.
    2. Observe the Status Code and Response Body.

6. Interpret Results
   - 200 OK → The site is accessible.
   - 403 Forbidden → Likely an IP or bot-blocking issue.

    If you get 403 here too, the restriction isn't connector-specific.
    
    If you get 200 here, the site may be blocking the connector's crawler.

## Steps to Test Website redirect loop

### Option 1: Use a Browser (Quick & No Tools)
**Steps**: 
1. Open the URL in a browser (Chrome / Edge / Firefox).
2. Open Developer Tools (F12).
3. Go to the Network tab.
4. Check Preserve log (important).
5. Reload the page.

**What to look for**:
* Multiple entries for the same page with status codes like: 301, 302, 307, 308
* Count how many times the request is redirected before it settles (or errors).

If you see more than 5 redirects, this explains why the crawler stops processing.

### Option 2: Use an API Client (Postman / Insomnia / REST client)
**Steps**: 
1. Create a new GET request to the webpage URL.
2. Turn off automatic redirect following:
    * Postman: Settings → General → Follow redirects = OFF
    * Insomnia: Disable Follow Redirects
3. Send the request.

**What to look for**:
* Each response will return a Location header.
* Manually follow the Location URL step by step.
* Count how many hops are needed before a final 200 OK (or failure).


If you have issues or want to provide feedback, contact [Microsoft Graph | Support](https://developer.microsoft.com/en-us/graph/support).
