# Deployment Configuration

The deployment configuration is generated by the [compiler](./compiler). It represents a desired state of a deployment and contains all required information to achieve that state via [./workflows](workflows.md). Manual changes to a deployment configuration should be avoided where ever possible to retain the ability to reproduce each deployment. If you need the deployment configuration modified, write a [compiler plugin] instead.

# Format
The format of the deployment configuration is optimized for easy processing in code. Where the various [manifests](architecture.md) have different intents, the deployment configuration is the combination of all information, enriched and modified by plugins.

## `target`
The `target` property is copied from the [deployment manifest](deployment_manifest.md).

## `services`
`services` are resolved from the `globalServices` in the [release manifest](release_manifest.md) and all `serviceBinding`s declared in the [application manifests](application_manifest.md). The `type` and `plan` information is resolved from the `serviceMapping` information from the [deployment manifest](deployment_manifest.md).

## `apps`
`apps` are the result of the `applicationDefaults` and `apps` in the [deployment manifest](deployment_manifest.md), the `source` from the [release manifest](release_manifest.md) and the specified values in the `deployment` property of the [application manifest](application_manifest.md).

## `envVars`
The `envVars` are the result of env var substitutions in the [compiler](compiler.md). Input for the substitutions are taken from the `applicationDefaults` and `apps` in the [deployment manifest](deployment_manifest.md) and the [application manifest](application_manifest.md) itself.

## `serviceBindings`
`serviceBindings` are generated from the `serviceBinding` property in the [application manifest](application_manifest.md).


## `routes`
`routes` are a combination of information in the [deployment manifest](deployment_manifest.md). Domains are specified in the `domain` property and the specific hostnames are described in the `apps` property per app and domain.