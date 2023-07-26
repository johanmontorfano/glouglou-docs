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
You can see that GlouGlou doesn't support HTTPS at all. However, this limitation will be overcame. Until an update for HTTPS support is release, you can try to find other solutions to use GlouGlou as an HTTPS service, one of them is using the [Efficient Progammed Router (EPR)](https://github.com/franndjoo/epr-go).

| Attribute         | Type   | Optionnal | Description                               |
| ----------------- | ------ | --------- | ----------------------------------------- |
| `http_port`       | `u16`  | No        | The port used by the HTTP server.         |


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

<br>
<br>

<h3 style="color: var(--accent); opacity: .9;">DKIM configuration</h3>

Nowadays, emails are the best way for anyone to reach out to people. Sadly, there are a lot of spammers, hackers, etc... who targets emails transactions. That's why we came up with the DKIM standard, which is used to certify an email hasn't been opened nor modified when going from the sender to the recipient. DKIM acts as a sealed enveloppe.

You can add a DKIM configuration to GlouGlou, it will be used to encrypt emails and sign them.

| Attribute          | Type   | Optional | Description                                                                      |
|--------------------|--------|----------|----------------------------------------------------------------------------------|
| `domain`           | String | no       | Domain targeted by the DKIM key pair.                                            |
| `selector`         | String | no       | The selector the DKIM key pair is stored under.                                  |
| `private_key_path` | String | no       | Path to the DKIM RSA private key.                                                |
| `expiration`       | u32    | no       | You can set this to 0, and don't bother with this value, it will go away sooner. |

Such a configuration should be stored under the `dkim` table. There is an example of a TOML DKIM configuration:

```toml
[dkim]
domain = "abc.xyz"
selector = "gg1main"
private_key_path = "/path/to/key"
expiration = 0
```


