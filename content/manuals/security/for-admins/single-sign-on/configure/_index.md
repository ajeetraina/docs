---
description: Learn how to configure single sign-on for your organization or company.
keywords: configure, sso, docker hub, hub, docker admin, admin, security 
title: Configure single sign-on
linkTitle: Configure
aliases:
- /docker-hub/domains/
- /docker-hub/sso-connection/
- /docker-hub/enforcing-sso/
- /single-sign-on/configure/
- /admin/company/settings/sso-configuration/
- /admin/organization/security-settings/sso-configuration/
---

Get started creating a single sign-on (SSO) connection for your organization or company.

The steps to set up your SSO configuration are:

1. [Add and verify the domain or domains](#step-one-add-and-verify-your-domain) that your members use to sign in to Docker.
2. [Create your SSO connection](#step-two-create-an-sso-connection-in-docker) in Docker.
3. [Configure your IdP](./configure-idp.md) to work with Docker.
4. [Complete your SSO connection](../connect/_index.md) in Docker.

This page walks through steps 1 and 2 using Docker Hub or the Admin Console.

## Step one: Add and verify your domain

{{< tabs >}}
{{< tab name="Admin Console" >}}

{{< include "admin-early-access.md" >}}

{{% admin-domains product="admin" %}}

{{< /tab >}}
{{< tab name="Docker Hub" >}}

{{% admin-domains product="hub" %}}

{{< /tab >}}
{{< /tabs >}}

## Step two: Create an SSO connection in Docker

{{< tabs >}}
{{< tab name="Admin Console" >}}

{{< include "admin-early-access.md" >}}

{{% admin-sso-config product="admin" %}}

{{< /tab >}}
{{< tab name="Docker Hub" >}}

{{% admin-sso-config product="hub" %}}

{{< /tab >}}
{{< /tabs >}}

## More resources

The following videos walk through verifying your domain to create your SSO connection in Docker.

- [Video: Verify your domain for SSO with Okta](https://youtu.be/c56YECO4YP4?feature=shared&t=529)
- [Video: Verify your domain for SSO with Azure AD (OIDC)](https://youtu.be/bGquA8qR9jU?feature=shared&t=496)

## What's next?

[Continue configuration in your IdP](./configure-idp.md).
