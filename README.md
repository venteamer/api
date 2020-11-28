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
| contractParameter | Contract parameter |
| contractState | State of the contract |
| ContractOwner  | Owner of the contract |

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

TBD

### FUN06: signContract

TBD

### FUN07: changeOwner

The objective of this function is to change the ownership of the owner of a contract in Venteamer platform. This event takes place when a contract draft proposed by one party is transfered for consideration to another party:

| Attribute Name | Attribute description |
| ---------- | ---------- |
| ContractId | Unique Identifier of the Contract |
| ContractOwner  | Owner of the contract |

API invocation example:

```
    curl -s -X POST \
-H 'Content-type: application/json' \
-d '{"key":"DOC1","newOwner":"Maciej"}' \
http://159.122.179.244:30003/changeOwner
```

Result:

```
{"msg":"changeOwner Transaction has been submitted"}%
```

### FUN08: queryContract

The objective of this function is to check the status of a contract called by its unique identifier.

| Attribute Name | Attribute description |
| ---------- | ---------- |
| ContractId | Unique Identifier of the Contract |

API invocation example:

```
curl -s -X GET -H 'Content-type: application/json' http://159.122.179.244:30003/queryContract?key=DOC0
```

Result:

```
{"contractowner":"User1","contractparameter":"1000","contractstate":"ACTIVE","contracttemplateid":"1234567890","docType":"doc"}%
```

### FUN09: queryContracts

The objective of this function is to check the status of all contracts registered in Venteamer.

API invocation example:

```
curl -s -X GET -H 'Content-type: application/json' http://159.122.179.244:30003/queryContracts
```

Result:

```
[{"Key":"DOC0","Record":{"contractowner":"User1","contractparameter":"1000","contractstate":"ACTIVE","contracttemplateid":"1234567890","docType":"doc"}},{"Key":"DOC1","Record":{"contractowner":"Maciej","contractparameter":"1000","contractstate":"ACTIVE","contracttemplateid":"TPL01","docType":"doc"}},{"Key":"DOC2","Record":{"contractowner":"Maciej Jedrzejczyk","contractparameter":"1000","contractstate":"ACTIVE","contracttemplateid":"TPL01","docType":"doc"}},{"Key":"DOC3","Record":{"contractowner":"Maciej Jedrzejczyk","contractparameter":"1000","contractstate":"ACTIVE","contracttemplateid":"TPL01","docType":"doc"}}]%
```

## Venteamer ledger APIs

Venteamer Ledger APIs leverage Hyperledger Explorer, a simple, powerful, easy-to-use, well maintained, open source utility to browse activity on the underlying blockchain network.

- Hyperledger Explorer UI: http://159.122.179.244:30005/
- Hyperledger Explorer APIs (Swagger): http://159.122.179.244:30005/api-docs/

### Logging to the UI

Below are listed usernames and passwords needed to log in to Hyperledger Explorer UI:

| Profile        | Login       | Password  | Description |
| ------------- |-------------| -----| -----|
| org1-network      | org1admin | org1adminpw | Blockchain network seen from the perspective of `org1` | 
| org2-network      | org2admin | org2adminpw | Blockchain network seen from the perspective of `org2` | 

The same login and password can be used to log in to consume APIs. For instance, this is an example of logging as ```org1```:
```
curl -X POST "http://159.122.179.244:30005/auth/login" -H  "accept: */*" -H  "Content-Type: application/json" -d "{\"user\":\"org1admin\",\"password\":\"org1adminpw\",\"network\":\"org1-network\"}"
```

In exchange, the following message should be shown:

```{"success":true,"message":"You have successfully logged in!","token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY","user":{"message":"logged in","name":"org1admin"}}```

This transaction provides a token that is used to authorize into API server: ```eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY```.

### Query about the number of channels in the network

```curl -X GET "http://159.122.179.244:30005/api/channels" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```

Result:

```
{
  "status": 200,
  "channels": [
    "channel1"
  ]
}
```
### Detailed information about the channel

```curl -X GET "http://159.122.179.244:30005/api/channels/info" -H  "accept: */*" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```

Result:

```
{
  "status": 200,
  "channels": [
    {
      "id": 4,
      "channelname": "channel1",
      "blocks": 19,
      "channel_genesis_hash": "383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86",
      "transactions": 19,
      "createdat": "2020-09-16T10:51:26.000Z",
      "channel_hash": ""
    }
  ]
}
```

### Detailed information about channel genesis block

```curl -X GET "http://159.122.179.244:30005/api/status/383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```

Result:

```
{
  "chaincodeCount": "2",
  "txCount": "19",
  "latestBlock": "19",
  "peerCount": "1"
}
```

### Information about smart contracts installed in the network

```curl -X GET "http://159.122.179.244:30005/api/chaincode/383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```

Result:

```
{
  "status": 200,
  "chaincode": [
    {
      "chaincodename": "fabcar",
      "channelName": "channel1",
      "path": "/Users/sstone1/go/src/github.com/hyperledger/fabric-samples/chaincode/fabcar/javascript",
      "version": "1.0.0",
      "txCount": 0,
      "channel_genesis_hash": "383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86"
    },
    {
      "chaincodename": "assetscc",
      "channelName": "channel1",
      "path": "github.com/assetscc",
      "version": "1.0",
      "txCount": 13,
      "channel_genesis_hash": "383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86"
    }
  ]
}
```

### Block exploration

```curl -X GET "http://159.122.179.244:30005/api/block/383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86/1" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```

### List of all transactions saved in a block

```curl -X GET "http://159.122.179.244:30005/api/blockAndTxList/383c685b318b4705575b2b62107db3ecb35b4d0e57cc83172d409092604b8f86/1" -H  "accept: */*" -H  "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoib3JnMWFkbWluIiwibmV0d29yayI6Im9yZzEtbmV0d29yayIsImlhdCI6MTYwMDI5MjEyOCwiZXhwIjoxNjAwMjk5MzI4fQ.GpslydyGMPJPn1rZ6s-J0NIoP9HSJWDKtw4mOxJynkY"```


