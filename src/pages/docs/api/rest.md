---
title: GlouGlou - Rest API
layout: ../../../../layouts/documentation.astro
---

# Rest API Documentation
<br>

This REST API provides three routes for sending emails, checking the validity of the API key, and pinging the GlouGlou instance. 

<br>
<h2 style="color: var(--accent);">Route 1: /send</h2>
<hr>
<br>

The `/send` route is used to send an email. The route accepts the following query parameters:

- `api-key`: the API key used to authenticate the request (required)
- `to`: the email address of the recipient (required)
- `subject`: the subject of the email (required)
- `body`: the body of the email (required)

The typical response for this route contains only the result code. If the email failed to send, the reason for the failure is included in the response's status code.

### Request

```
GET /send?api-key={api-key}&to={to}&subject={subject}&body={body}
```

<br>
<h2 style="color: var(--accent);">Route 2: /access-ok</h2>
<hr>
<br>

The `/access-ok` route is used to check if the client API key is valid or not. The route accepts the following query parameter:

- `api-key`: the API key used to authenticate the request (required)

### Request

```
GET /access-ok?api-key={api-key}
```

### Response

The response will contain a JSON object with the following properties:

- `ok`: a boolean indicating the result of the request. Please note that if there is any issues with the request, `ok` will be also set to `false`.

<br>
<h2 style="color: var(--accent);">Route 3: /ping</h2>
<hr>
<br>

The `/ping` route is used to check if the GlouGlou instance is reachable or not.

### Request

```
GET /ping
```

### Response

If the server is reachable and works properly the response will be a `200` code, with a `OK`status and `pong` on the response's body.