# IoTeX HTTP gRPC-JSON transcoder

A docker compose file that starts two gRPC-JSON transcoder servers. One pointing to IoTeX testnet and another pointing to IoTeX mainnet.  

## Usage

### Launching the server

Install docker and docker-compose.  
Clone the repository and run `docker-compose up` from the root directory.  
Wait for the two containers to start, then in a different terminal run `docker ps` to find out which each container exposed port:  

```terminal
$ docker ps
CONTAINER ID   IMAGE                                                           COMMAND                  CREATED          STATUS          PORTS                      NAMES
ed508ae9cd5a   envoyproxy/envoy-dev                                            "/docker-entrypoint.…"   6 minutes ago    Up 5 minutes    0.0.0.0:59584->10000/tcp   http-transcoder_testnet_1
1d4280ca545a   envoyproxy/envoy-dev                                            "/docker-entrypoint.…"   6 minutes ago    Up 5 minutes    0.0.0.0:59583->10000/tcp   http-transcoder_mainnet_1
```

In the example above, we see that we can access the testnet server at port 59584 of the docker host, and the mainnet server at port 59583.  

### Querying the server

See below is an example of how to query the account metadata for an account:  

```terminal
$ curl --location --request POST 'http://localhost:59584/GetAccount' \
--header 'Content-Type: application/json' \
--data-raw '{"address":"io18g7frw4t8x0hvm2amgpfyg5cyqr60gs9d60dx6"}'
{
 "accountMeta": {
  "address": "io18g7frw4t8x0hvm2amgpfyg5cyqr60gs9d60dx6",
  "balance": "997711804000000000000",
  "nonce": "0",
  "pendingNonce": "15",
  "numActions": "15",
  "isContract": false,
  "contractByteCode": ""
 },
 "blockIdentifier": {
  "hash": "4f5649019b2cc3aea038e164d09fee69e674077bcad5fbc52af8fcf043e44d02",
  "height": "15596661"
 }
}
```
