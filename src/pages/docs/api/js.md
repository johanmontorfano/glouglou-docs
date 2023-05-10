---
title: GlouGlou - Javascript API
layout: ../../../../layouts/documentation.astro
---

# Javascript API Documentation
<br>

The Javascript API is a `types` enabled API used to communicate with a GlouGlou instance through a set of easy to use functions. Install it with your favorite NPM-based package manager, the pacakge name is `@johanmnto/glougloujs`

<br>
<h2 style="color: var(--accent);">Configuration</h2>
<hr>
<br>

The `Configuration` interface is a core concept of the GlouGlou Javascript API. It is needed to allow the API to send requests to the correct GlouGlou instance. Without a properly configured `Configuration` object, it will not be possible to communicate with any of your services.

<br>
<h3 style="color: var(--accent);">Interface Description</h3>
<hr>

The `Configuration` interface is defined as follows:

```typescript
export interface Configuration {
    apiKey: string;
    port?: number;
    domain: string;
    secure: boolean;
}
```

<br>
<h3 style="color: var(--accent);">Properties</h3>
<hr>

* `apiKey` - A string that represents the API key used to authenticate requests to the GlouGlou instance.
* `port` - An optional number that represents the port number of the GlouGlou instance. If not provided, the default port for HTTP or HTTPS will be used depending on the `secure` property.
* `domain` - A string that represents the domain name of the GlouGlou instance.
* `secure` - A boolean that indicates whether the GlouGlou instance should be accessed via HTTPS or not.

<br>
<br>
<h2 style="color: var(--accent);">Send Emails</h2>
<hr>
<br>

To send emails, you'll have to understand first how to build `Email` that can be sent by the `sendEmail` function.

<br>
<h3 style="color: var(--accent);">Email</h3>
<hr>

The `Email` interface is a TypeScript interface that represents the content of an email that can be sent to the GlouGlou instance.

<br>
<h4 style="color: var(--accent);">Interface Description</h4>
<hr>

The `Email` interface is defined as follows:

```typescript
export interface Email {
    recipient: {
        name: string,
        email: string
    },
    subject: string,
    body: string
}
```

<br>
<h4 style="color: var(--accent);">Properties</h4>
<hr>

* `recipient` - An object that represents the recipient of the email. It has two properties:
  * `name` - A string that represents the name of the recipient.
  * `email` - A string that represents the email address of the recipient.
* `subject` - A string that represents the subject of the email.
* `body` - A string that represents the body of the email.

<br>
<br>
<h3 style="color: var(--accent);">sendEmail</h3>
<hr>

The `sendEmail()` function is a TypeScript function used to send an email via the GlouGlou Javascript API. This function takes in a `Configuration` object and an `Email` object as arguments and returns a promise that resolves with the response data from the API.

<br>
<h4 style="color: var(--accent);">Description</h4>
<hr>

The `sendEmail()` function is defined as follows:

```typescript
export async function sendEmail(config: Configuration, email: Email) {
    const composedURL = composeURL(config, "send", {
        "api-key": config.apiKey,
        "to": `${email.recipient.name} <${email.recipient.email}>`,
        "subject": email.subject,
        "body": email.body
    });
    return await sendRequest(composedURL);
}
```

<br>
<h4 style="color: var(--accent);">Parameters</h4>
<hr>

* `config` - A `Configuration` object that contains the configuration needed to send requests to the GlouGlou instance.
* `email` - An `Email` object that represents the content of the email to be sent.

<br>
<br>
<h2 style="color: var(--accent);">Verify API key validity</h2>
<hr>
<br>

The `verifyAPIKey()` function is used to verify the validity of a given API key via the GlouGlou Javascript API. This function takes in a `Configuration` object as an argument and returns a promise that resolves with the response data from the API.

<br>
<h4 style="color: var(--accent);">Function description</h4>
<hr>

The `verifyAPIKey()` function is defined as follows:

```typescript
export async function verifyAPIKey(config: Configuration) {
    const composedURL = composeURL(config, "access-ok", { "api-key": config.apiKey });
    return await sendRequest(composedURL);
}
```

<br>
<h4 style="color: var(--accent);">Parameters</h4>
<hr>

* `config` - A `Configuration` object that contains the configuration needed to send requests to the GlouGlou instance.
