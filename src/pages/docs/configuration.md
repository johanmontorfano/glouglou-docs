---
title: GlouGlou - Configuration
layout: ../../../layouts/documentation.astro
---

# The configuration file

<br>

<h2 style="color: var(--accent)">The file</h2>
<hr>
<br>

As you may expect, GlouGlou needs a configuration file to work properly. This file should be present on the same directory the executable is, otherwise GlouGlou will not be able to find it.

The configuration file is named `glouglou.conf.toml`.

This is an example of what your directory shoud look like after creating the configuration file:

```
glouglou_executable
glouglou.conf.toml
```

<br>
<br>

<h2 style="color: var(--accent)">The configuration</h2>

The GlouGlou configuration file is composed of two categories of configurations: the server behaviors, the used email address configuration.

It's recommended to have a minimal understanding of how Toml works before continuing.

<br>
<br>

<h3 style="color: var(--accent); opacity: .9;">Let start with the server behavior configuration</h3>
<hr>

Every configuration that concerns the server is set under the `server` table, there is below the attributes used for the server configuration.

| Attribute         | Type   | Optionnal | Description                               |
| ----------------- | ------ | --------- | ----------------------------------------- |
| `http_port`       | `u16`  | No        | The port used by the HTTP server.         |
| `https_port`      | `u16`  | Yes       | The port used by the HTTPS server.        |
| `https_cert_path` | String | Yes       | The certificate used by the HTTPS server. |
| `https_key_path`  | String | Yes       | The key paired with the certificate.      |

<br>

Considering this, a fully configured GlouGlou instance server should look like the following:

```toml
[server]
http_port = 3000
https_port = 5000
https_cert_path = "path/to/cert"
https_key_path = "path/to/key"
```

<br>
<br>

<h3 style="color: var(--accent); opacity: .9;">Dive deep into the email address configuration.</h3>
<hr>

To send emails, the GlouGlou instance will have to be granted access to an email address of your own. The only things it needs are the credentials of this email address. The email address configuration attributes are set under the `email` table.

| Attribute  | Type     | Optionnal | Description                                                                                                                                                                                     |
| ---------- | -------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `address`  | `String` | No        | The email address to use such as `abc@xyz.com`                                                                                                                                                  |
| `password` | `String` | No        | The password to access this email address, please take in consideration that some email providers (Gmail, iCloud, ...) only allows third-party services to connect via an application password. |
| `host`     | `String` | No        | GlouGlou only support SMTP connections, please provide your email provider SMTP domain such as `smtp.xyz.com`                                                                                   |
| `port`     | `u32`    | No        | The port opened for incoming SMTP requests by your email provider, it's often `587`                                                                                                             |

<br>

Considering this, a fully configured GlouGlou instance email should look like the following:

```toml
[email]
address = "abc@xyz.com"
password = "example123"
host = "smtp.xyz.com"
port = 587
```