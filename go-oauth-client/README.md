# Sample PKCE client

This directory contains a sample golang auth client. The auth client opens a webserver which has a Login link. Click this Login link and it will go through a "headless" PKCE flow, receive a token and turn this token into a permanent JWT which can be used to authenticate with RPC servers.

The client provides two urls

 * `/` - displays the login link 
 * `/callbacks` - callback to receive and convert a token 

## Run

Assuming that you have your callback and client ID pre-registered, you can run the client yourself:

```
$ go build .
$ ./go-auth-client -client-id myclient-pkce-tier1 -redirect-url https://auth-fra1.rpcpool.com/callbacks -oauth2-auth-url https://auth-fra1.rpcpool.com:8443/oauth2/auth -oauth2-token-url  https://auth-fra1.rpcpool.com:8443/oauth2/token -scopes tier1
```

## Test

There is a test version of this client running here:

https://auth-fra1.rpcpool.com/

Clicking the login link you will receive a new bearer token that you can use to authenticate with Triton One's staging RPC servers:

```
$ curl https://stage.mainnet.rpcpool.com/tier
free

$ curl -H "Authorization: Bearer <token>" https://stage.mainnet.rpcpool.com/tier 
tier1
```
