---
title: Service name
description: A short description (up to ~160 characters) of the service that should make sense out of context (like on a listing page).
---

<!-- 
When to use
  For all available services: https://docs.platform.sh/add-services.html

How to use
  1. Copy this template into /src/docs/add-services/.
  2. Rename it to match the title.
  3. Replace the following content with your own.
  4. Replace all instances of "<SERVICE_NAME>" in the examples with the service's name.
-->

A brief introduction (1--2 sentences) to what this service is used for.

## Supported versions

| **Grid** | **Dedicated** | **Dedicated Generation 3** |
|----------------------------------|---------------|---------------|
|  {{< image-versions image="<SERVICE_NAME>" status="supported" environment="grid" >}} | {{< image-versions image="<SERVICE_NAME>" status="supported" environment="dedicated" >}} | {{< image-versions image="<SERVICE_NAME>" status="supported" environment="dedicated-gen-3" >}} |

<!-- To automatically check any differences in the registry with legacy regions -->
{{< image-versions-legacy "<SERVICE_NAME>" >}}

<!-- If there are any deprecated versions. -->
{{% deprecated-versions %}}

| **Grid** | **Dedicated** | **Dedicated Generation 3** |
|----------------------------------|---------------|---------------|
|  {{< image-versions image="<SERVICE_NAME>" status="supported" environment="grid" >}} | {{< image-versions image="<SERVICE_NAME>" status="supported" environment="dedicated" >}} | {{< image-versions image="<SERVICE_NAME>" status="supported" environment="dedicated-gen-3" >}} |

## Usage example

<!--
  Include the general template for usage examples.
  Replace `<SERVICE_TYPE>` with the type.

  If the service allows multiple endpoints, also include following parameter:
  sectionLink="#<SECTION_ON_PAGE_WITH_DESCRIPTION>" multipleText="<NOUN_THAT_CAN_BE_MULTIPLE"
  Example for MariaDB:
  sectionLink="#multiple-databases" multipleText="databases" 

  If the service doesn't have examples of usage in an app taken from https://examples.docs.platform.sh/
  include the following parameter:
  noApp=true
-->
{{% endpoint-description type="<SERVICE_TYPE>" /%}}

{{< codetabs >}}

---
title=<LANGUAGE>
file=static/files/fetch/examples/<LANGUAGE_NAME>/<SERVICE_TYPE>
highlight=<LANGUAGE>
---

<--->
<!-- Repeat above for more languages -->
{{< /codetabs >}}

<!-- If the service has options in the `configuration` key -->
## Configuration options

You can configure your <SERVICE_NAME> service in the [services configuration](./_index.md) with the following options:

| Name   | Type     | Required | Description |
| ------ | -------- | -------- | ----------- |
| `type` | `string` | Yes      | What it does. |

## Relationship reference

Example information available through the [`$PLATFORM_RELATIONSHIPS` environment variable](/development/variables/use-variables.md#use-platformsh-provided-variables)
or by running `platform relationships`:

<!-- A yaml file taken from https://examples.docs.platform.sh/ that contains all the properties people need to access/use the service. -->
{{< relationship "<SERVICE_NAME>" >}}

## Any other functions specific to the service

Structure like [how to steps](./how-to.md#1-do-this-step-first).
Split each function into a separate section.
