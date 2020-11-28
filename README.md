# API Reference for Venteamer

Below you will find basic information about APIs exposed by Venteamer platform.

## Venteamer URL

Current URL to Venteamer APIs: http://159.122.179.244

## Venteamer application APIs

Application APIs are exposed through the following port: http://159.122.179.244:30003


| FunctionNo | FunctionId | Type | Component | Parameters |
| ---------- | ---------- | ---------- | ---------- | ---------- |
| FUN04 | createContract | POST | Blockchain API | ContractId,ContractTemplateId, ContractParameter,ContractState,ContractOwner |
| FUN05 | appendContract | POST | Blockchain API | ContractId,ContractParameter |
| FUN06 | signContract | POST | Blockchain API | ContractId,ContractState |
| FUN07 | changeOwner | POST | Blockchain API | ContractId,ContractOwner |
| FUN08 | queryContract | GET | Blockchain API | ContractId |
| FUN09 | queryContracts | GET | Blockchain API | ContractId,ContractTemplateId, ContractParameter,ContractState,ContractOwner |

### FUN04: createContract

The objective of this function is to register an uniquely identifiable contract in Venteamer platform. The Contract object holds basic information about the following attributes:

| Attribute Name | Attribute description |
| ---------- | ---------- |
| contracttemplateid | Unique Identifier of the Contract Template used by the registered contract |
| contractparameter | Contract parameter |
| contractstate | State of the contract |
| contractowner | Owner of the contract |

API invocation example:

```
    curl -s -X POST \
-H 'Content-type: application/json' \
-d '{"contracttemplateid":"TPL01","contractparameter":"1000","contractstate":"ACTIVE","contractowner":"Maciej Jedrzejczyk"}' \
http://159.122.179.244:30003/createContract
```

Result:

```
{"msg":"createContract Transaction has been submitted"}%
```

### FUN05: appendContract
### FUN06: signContract
### FUN07: changeOwner
### FUN08: queryContract
### FUN09: queryContracts

## Venteamer ledger APIs

Application APIs are exposed through the following port: http://159.122.179.244:30004


