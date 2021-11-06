# Run


```
$ go build .
$ ./go-auth-client -client-id myclient-pkce-tier1 -redirect-url https://auth-fra1.rpcpool.com/callbacks -oauth2-auth-url https://auth-fra1.rpcpool.com:8443/oauth2/auth -oauth2-token-url  https://auth-fra1.rpcpool.com:8443/oauth2/token -scopes tier1
```

## Try it

https://auth-fra1.rpcpool.com/

```
$ curl -H https://stage.mainnet.rpcpool.com/tier
free

$ curl -H "Authorization: Bearer <token>" https://stage.mainnet.rpcpool.com/tier 
tier1
```
