# Data Factory V2

> see https://aka.ms/autorest

This is the AutoRest configuration file for Data Factory V2.



---
## Getting Started
To build the SDK for Data Factory V2, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`
---

## Configuration


### Basic Information
These are the global settings for the Data Factory V2 API.

``` yaml
title: DataFactoryManagementClient
description: The Azure Data Factory V2 management API provides a RESTful set of web services that interact with Azure Data Factory V2 services.
openapi-type: arm
tag: package-2018-06
```

### Tag: package-2018-06

These settings apply only when `--tag=package-2018-06` is specified on the command line.

``` yaml $(tag) == 'package-2018-06'
input-file:
- Microsoft.DataFactory/stable/2018-06-01/datafactory.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/DataFlow.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/Dataset.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/IntegrationRuntime.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/LinkedService.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/ManagedPrivateEndpoint.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/Pipeline.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/Trigger.json
- Microsoft.DataFactory/stable/2018-06-01/entityTypes/ChangeDataCapture.json
suppressions:
  - code: PropertiesTypeObjectNoDefinition
    reason: ADF parameterization feature is widely adopted and requires object type for most of the swagger properties.
  - code: AvoidAdditionalProperties
    reason: ADF feature is widely adopted and requires additionalProperties for most of the swagger properties.
  - code: MissingTypeObject
    reason: ADF feature is widely adopted and requires MissingTypeObject for most of the swagger properties.
  - code: IntegerTypeMustHaveFormat
    reason: ADF feature is widely adopted and requires IntegerTypeMustHaveFormat for most of the swagger properties.
  - code: RequiredPropertiesMissingInResourceModel
    reason: ADF feature is widely adopted and requires RequiredPropertiesMissingInResourceModel for most of the swagger properties.
  - code: BodyTopLevelProperties
    reason: ADF feature is widely adopted and requires BodyTopLevelProperties for most of the swagger properties.
  - code: TrackedResourcePatchOperation
    reason: ADF feature is widely adopted and requires TrackedResourcePatchOperation for most of the swagger properties.
  - code: XmsEnumValidation
    reason: ADF feature is widely adopted and requires XmsEnumValidation for most of the swagger properties.
  - code: NestedResourcesMustHaveListOperation
    reason: ADF feature is widely adopted and requires NestedResourcesMustHaveListOperation for most of the swagger properties.
```

### Tag: package-2017-09-preview

These settings apply only when `--tag=package-2017-09-preview` is specified on the command line.

``` yaml $(tag) == 'package-2017-09-preview'
input-file:
- Microsoft.DataFactory/preview/2017-09-01-preview/datafactory.json
```

---
# Code Generation


## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-net
  - repo: azure-sdk-for-python
  - repo: azure-sdk-for-java
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-js
  - repo: azure-sdk-for-node
  - repo: azure-cli-extensions
  - repo: azure-resource-manager-schemas
  - repo: azure-powershell
```


## Python

See configuration in [readme.python.md](./readme.python.md)

## Go

See configuration in [readme.go.md](./readme.go.md)

## Java

See configuration in [readme.java.md](./readme.java.md)


## Suppression

``` yaml
directive:
  - suppress: R2001  # AvoidNestedProperties
    where:
      - $.definitions.IntegrationRuntimeResource.properties.properties
      - $.definitions.IntegrationRuntimeStatusResponse.properties.properties
      - $.definitions.TriggerResource.properties.properties
      - $.definitions.LinkedServiceResource.properties.properties
      - $.definitions.TriggerRun.properties.properties
      - $.definitions.DatasetResource.properties.properties
      - $.properties.properties.LinkedServiceResource.definitions
      - $.properties.properties.LinkedServiceResource.definitions
      - $.properties.properties.IntegrationRuntimeStatusResponse.definitions
      - $.properties.properties.IntegrationRuntimeStatusResponse.definitions
      - $.properties.properties.DatasetResource.definitions
      - $.properties.properties.DatasetResource.definitions
      - $.properties.properties.TriggerResource.definitions
      - $.properties.properties.TriggerResource.definitions
    from: datafactory.json
    reason:
      - Flattening does not work well with polymorphic models.
      - TriggerResource.properties is an arbitrary dictionary and cannot be flattened.
  - suppress: R2018  # XmsEnumValidation
    where:
      - $.definitions.Expression.properties.type
      - $.definitions.SecureString.properties.type
      - $.definitions.SecureString.properties.type
      - $.definitions.IntegrationRuntimeReference.properties.type
      - $.definitions.PipelineReference.properties.type
      - $.definitions.DatasetReference.properties.type
      - $.definitions.LinkedServiceReference.properties.type
      - $.type.properties.DatasetReference.definitions
      - $.type.properties.IntegrationRuntimeReference.definitions
      - $.type.properties.IntegrationRuntimeReference.definitions
    from: datafactory.json
    reason: Single-value enums are expressed to force the values to be used for de/serialization but should not be exposed or settable by the a client.
  - suppress: R3017  # GuidUsage
    where:
      - $.definitions.FactoryIdentity.properties.principalId
      - $.definitions.FactoryIdentity.properties.tenantId
    from: datafactory.json
    reason:
      - FactoryIdentity.properties.principalId should be a Guid, per MSI integration.
      - FactoryIdentity.properties.tenantId should be a Guid, per MSI integration.
  - suppress: R3010  # TrackedResourceListByImmediateParent
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}"]
    reason:
      - Pipeline runs are not listable. The operation PipelineRuns_QueryByFactory serves this purpose.
  - suppress: R1003  # ListInOperationName
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/monitoringData"].post.operationId
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/integrationRuntimes/{integrationRuntimeName}/monitoringData"].post.operationId
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns"].post.operationId
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns"].paths
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryTriggerRuns"].paths
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryPipelineRuns"].paths
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns"].paths
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryPipelineRuns"].post.operationId
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns"].post.operationId
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryTriggerRuns"].post.operationId
    from: datafactory.json
    reason:
      - QueryBy API-s are by-design not true list API-s; getting runs requires providing a filter that is part of the request body in a POST call.
  - suppress: R2066  # PostOperationIdContainsUrlVerb
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns"].post.operationId
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryPipelineRuns"].post.operationId
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryPipelineRuns"].paths
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns"].post.operationId
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/pipelineruns/{runId}/queryActivityruns"].paths
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryTriggerRuns"].post.operationId
      - $.operationId.post["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/queryTriggerRuns"].paths
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}/cancelpipelinerun/{runId}"].post.operationId
    from: datafactory.json
    reason:
      - PipelineRuns_QueryByFactory is placed in pipeline runs namespace fpr better user experience. The method name shows the scope.
      - ActivityRuns_QueryByPipelineRun is placed in activity runs namespace fpr better user experience. The method name shows the scope.
      - CancelPipelineRun API is fixed in our new API version
  - suppress: R3018  # EnumInsteadOfBoolean
    where:
      - $.definitions.OperationMetricDimension.properties.toBeExportedForShoebox
      - $.definitions.ActivityPolicy.properties.secureOutput
      - $.definitions.SSISPropertyOverride.properties.isSensitive
      - $.definitions.ForEachActivityTypeProperties.properties.isSequential
      - $.definitions.ExecutePipelineActivityTypeProperties.properties.waitOnCompletion
      - $.definitions.SelfHostedIntegrationRuntimeNode.properties.isActiveDispatcher
      - $.definitions.IntegrationRuntimeConnectionInfo.properties.isIdentityCertExprired
    reason:
      - toBeExportedForShoebox is property we send to Azure Monitor which requires the boolean type
      - The other properties are simple and self explanatory
  - suppress: OAV131  # EnumInsteadOfBoolean
    where:
      - $(this-folder)/Microsoft.DataFactory/stable/2018-06-01/entityTypes/LinkedService.json
    reason:
      - DataFlow add type required  
```



