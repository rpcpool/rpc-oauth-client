# rpc-oauth-client
Oauth clients for RPC servers.

Your oauth client needs to be able to support a PKCE Oauth flow.

## Credentials
To run this, you will need to have two pieces of credentials pre-registered:

 1. `client_id` - this is the client that maps
 2. `redirect_url` - the redirect URL that you will use 

To get new credentials for testing e-mail support@triton.one.

## OAuth2 endpoints

For testing we provide two oauth endpoints:

 - Auth URL:  https://auth-fra1.rpcpool.com:8443/oauth2/auth
 - Token URL: https://auth-fra1.rpcpool.com:8443/oauth2/token
        
