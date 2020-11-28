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
| FUN08 | queryContract | POST | Blockchain API | ContractId |
| FUN09 | queryContracts | POST | Blockchain API | ContractId,ContractTemplateId, ContractParameter,ContractState,ContractOwner |


## Venteamer ledger APIs

Application APIs are exposed through the following port: http://159.122.179.244:30004


