---
layout: bt_wiki
title: ARIA Plugin
category: Plugins
draft: false
weight: 2
6
weight: 10000
---
{{% gsSummary %}} {{% /gsSummary %}}

Plugin Description



# Plugin Requirements



# Compatibility



{{% gsNote title="Note" %}}
 .
{{% /gsNote %}}





# Terminology


# Types

This section describes the [node type]({{< relref "blueprints/spec-node-types.md" >}}) definitions. Nodes describe resources in your Cloud infrastructure. For more information, see [node type]({{< relref "blueprints/spec-node-types.md" >}}).


# Relationships

See the [relationships]({{< relref "blueprints/spec-relationships.md" >}}) section.

# Examples

This example demonstrates how to use the cloudify-aria-plugin. The example sets a path to a TOSCA CSAR package. The package is located in path relative to the blueprint.

```yaml

tosca_definitions_version: cloudify_dsl_1_3

imports:
  - http://www.getcloudify.org/spec/cloudify/4.2/types.yaml
  - https://raw.githubusercontent.com/cloudify-cosmo/cloudify-aria-plugin/master/plugin.yaml

node_templates:
  aria_node:
    type: cloudify.aria.nodes.Service
    properties:
      csar_path: resources/hello-world.csar

outputs:
  http_endpoint:
    description: Web server external endpoint
    value: { get_attribute: [aria_node, port] }
