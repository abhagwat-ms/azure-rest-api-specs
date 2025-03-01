# Redis

> see https://aka.ms/autorest

This is the AutoRest configuration file for Redis.

---

## Getting Started

To build the SDK for Redis, simply [Install AutoRest](https://aka.ms/autorest/install) and in this folder, run:

> `autorest`

To see additional help and options, run:

> `autorest --help`

---

## Configuration

### Basic Information

These are the global settings for the Redis API.

``` yaml
openapi-type: arm
tag: package-2022-05
```


### Tag: package-2022-05

These settings apply only when `--tag=package-2022-05` is specified on the command line.

```yaml $(tag) == 'package-2022-05'
input-file:
  - Microsoft.Cache/stable/2022-05-01/redis.json
```
### Tag: package-2021-06

These settings apply only when `--tag=package-2021-06` is specified on the command line.

``` yaml $(tag) == 'package-2021-06'
input-file:
  - Microsoft.Cache/stable/2021-06-01/redis.json
```

### Tag: package-2020-12

These settings apply only when `--tag=package-2020-12` is specified on the command line.

``` yaml $(tag) == 'package-2020-12'
input-file:
  - Microsoft.Cache/stable/2020-12-01/redis.json
```

### Tag: package-2020-06

These settings apply only when `--tag=package-2020-06` is specified on the command line.

``` yaml $(tag) == 'package-2020-06'
input-file:
  - Microsoft.Cache/stable/2020-06-01/redis.json
```

### Tag: package-2019-07-preview

These settings apply only when `--tag=package-2019-07-preview` is specified on the command line.

``` yaml $(tag) == 'package-2019-07-preview'
input-file:
  - Microsoft.Cache/preview/2019-07-01/redis.json
```

### Tag: package-2018-03

These settings apply only when `--tag=package-2018-03` is specified on the command line.

``` yaml $(tag) == 'package-2018-03'
input-file:
- Microsoft.Cache/stable/2018-03-01/redis.json
```

### Tag: package-2017-10

These settings apply only when `--tag=package-2017-10` is specified on the command line.

``` yaml $(tag) == 'package-2017-10'
input-file:
- Microsoft.Cache/stable/2017-10-01/redis.json
```

### Tag: package-2017-02

These settings apply only when `--tag=package-2017-02` is specified on the command line.

``` yaml $(tag) == 'package-2017-02'
input-file:
- Microsoft.Cache/stable/2017-02-01/redis.json
```

### Tag: package-2016-04

These settings apply only when `--tag=package-2016-04` is specified on the command line.

``` yaml $(tag) == 'package-2016-04'
input-file:
- Microsoft.Cache/stable/2016-04-01/redis.json
```

### Tag: package-2015-08

These settings apply only when `--tag=package-2015-08` is specified on the command line.

``` yaml $(tag) == 'package-2015-08'
input-file:
- Microsoft.Cache/stable/2015-08-01/redis.json
```

---

# Code Generation

## Swagger to SDK

This section describes what SDK should be generated by the automatic system.
This is not used by Autorest itself.

``` yaml $(swagger-to-sdk)
swagger-to-sdk:
  - repo: azure-sdk-for-net-track2
  - repo: azure-sdk-for-python-track2
  - repo: azure-sdk-for-java
  - repo: azure-sdk-for-go
  - repo: azure-sdk-for-js
  - repo: azure-sdk-for-node
  - repo: azure-sdk-for-ruby
    after_scripts:
      - bundle install && rake arm:regen_all_profiles['azure_mgmt_redis']
  - repo: azure-sdk-for-python-track2
  - repo: azure-resource-manager-schemas
  - repo: azure-powershell
```

## C#

These settings apply only when `--csharp` is specified on the command line.
Please also specify `--csharp-sdks-folder=<path to "SDKs" directory of your azure-sdk-for-net clone>`.

``` yaml $(csharp)
csharp:
  # last generated with AutoRest.0.17.3
  azure-arm: true
  license-header: MICROSOFT_MIT_NO_VERSION
  namespace: Microsoft.Azure.Management.Redis
  output-folder: $(csharp-sdks-folder)/redis/Microsoft.Azure.Management.Redis/src/Generated
  clear-output-folder: true
```

## Python

See configuration in [readme.python.md](./readme.python.md)

## Go

See configuration in [readme.go.md](./readme.go.md)

## Java

See configuration in [readme.java.md](./readme.java.md)

# Validation

## Suppression

``` yaml
directive:
  - suppress: R3006  # Model definition 'RedisResource' has extra properties ['zones']."
    where:
      - $.definitions.RedisResource.properties
    from: redis.json
    reason: zones properties will be allowed in subsequent version of the linter tool
  - suppress: R3018  # Booleans are not descriptive and make them hard to use. Consider using string enums with allowed set of values defined. Property: enableNonSslPort."
    where:
      - $.definitions.RedisCommonProperties.properties.enableNonSslPort
    from: redis.json
    reason: this will result in breaking change
  - suppress: R3018  # Booleans are not descriptive and make them hard to use. Consider using string enums with allowed set of values defined. Property: isMaster."
    where:
      - $.definitions.RedisInstanceDetails.properties.isMaster
    from: redis.json
    reason: this will result in breaking change
  - suppress: R3018  # Booleans are not descriptive and make them hard to use. Consider using string enums with allowed set of values defined. Property: isPrimary"
    where:
      - $.definitions.RedisInstanceDetails.properties.isPrimary
    from: redis.json
    reason: this will result in breaking change
  - suppress: R3018  # Booleans are not descriptive and make them hard to use. Consider using string enums with allowed set of values defined. Property: isDataAction"
    where:
      - $.definitions.Operation.properties.isDataAction
    from: types.json
    reason: its per the RPC specification
  - suppress: R2017  # PUT request and response should be of same type "
    where:
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cache/Redis/{name}/linkedServers/{linkedServerName}"].put
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cache/Redis/{name}"].put
      - $.paths["/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Cache/Redis/{cacheName}/firewallRules/{ruleName}"].put
    from: redis.json
    reason: bug from sdk team
  - suppress: R3010  # The child tracked resource, 'linkedServers' with immediate parent 'RedisResource', must have a list by immediate parent operation."
    where:
      - $.definitions
    from: redis.json
    reason: This is false positive, 'linkedServers' is not a tracked resource.
```
