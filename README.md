# rpc-oauth-client
A "headless" Oauth client (PKCE) for Solana RPC services.

Web3 operates on a principal of user anonymity. However, this anonymity creates a vector for bad actors to abuse backend systems. It is currently too easy to spoof an origin header and gain access to free RPC services.

An important point of distinction is that the user does not need to reveal their identity to use the service. This is headless OAuth in the sense that the user is not asked to identify themselves with the more familiar OAuth services offered by Github, Twitter, etc. The RPC-OAuth-Client allows a dApp to prove that RPC requests originate from their approved website.

## How does it work?

This implements a version of standard oauth2 PKCE flow, but skips the actual authentication steps instead only authenticating the origin of the request. The origin can be authenticated in two ways:

 1) Only allow requests from a particular origin to initiate the request flow. This is easily spoofable from a command line, but not spoofable inside a standards compliant browser.
 2) Only do callbacks to a specific URL, meaning that at the end of the flow, we will redirect to that particular URL. This URL receives a temporary token that it will then interact with our service to replace with a permanent, timelimited access token.

This ensures that someone seeking to abuse an RPC endpoint which has oauth2 support will have to run an interactive browser to receive the actual token and they will also be required to regularly refresh these tokens.

## Integrating with your app/client
 
To integrate with your own set up you'll need to add support for the Oauth PKCE flow

In this repo we have included a sample `oauth.ts` that includes a TypeScript oauth client that can be used as a reference. An example of how to use this is given below:

```
  const endpoint = useMemo(() => clusterApiUrl(network), []);

  const [ connection, setConnection ] = useState<Connection>(new anchor.web3.Connection(rpcHost))

  useEffect(() => {
    (async () => {
      const accessToken = await getOAuthToken(
        "my-client-id", // This needs to be generated on the server side by us
        "http://localhost:8080", // This needs to be whitelisted by us on the server side
        "https://auth-fra1.rpcpool.com:8443/oauth2/auth",
        "https://auth-fra1.rpcpool.com:8443/oauth2/token",
      );

      setConnection(new anchor.web3.Connection(rpcHost, { httpHeaders: { 'Authorization': `Bearer ${accessToken}`}}));
    })()
  }, [])
```

We have also included sample golang source for an app that implements the oauth part. You can use this to write the custom integration with your app.

 
### Features

Your integration should feature:

  - Configuration of the parameters of an oauth2 pkce flow using custom auth/token urls along with custom requested scopes (sample ones below for testing)
  - Code verifier generation and validation for PKCE flow
  - Callback for receiving the initial authorization token and turning into a permanent token
  - Tracking expiry time of tokens received 
  - Renewal of tokens using a renewal token


### SDKs and other examples

A sample SDK is provided from auth0, which can be used as a baseline:

 - https://auth0.com/docs/libraries/auth0-single-page-app-sdk.

There has also been work integrating oauth support with web3.js/candy machine/metaplex:

 - https://github.com/metaplex-foundation/metaplex/pull/944
 - https://github.com/metaplex-foundation/metaplex/pull/1193 
 - https://github.com/solana-labs/solana/issues/21816


## Backend Servers

For testing, we currently have both a sample client and a set of backend servers set up. The sample client is given in this repo. To get oauth access credentials 

### Sample client

For the sample client you can visit https://auth-fra1.rpcpool.com  and click 'Login'. After the authentication flow you will be redirected back to a callback page on the same domain but with a token that you can use for RPC requests. 

You can use the token received in the following way:

```
curl -H "Authorization: Bearer <token>" https://stage.mainnet.rpcpool.com ... rpc call ...
```

To validate that the token has given you higher access permissions use the following:

```
curl -H "Authorization: Bearer <token>" https://stage.mainnet.rpcpool.com/tier 
```

The response should be `tier1,offline_access`. 

### OAuth2 Backend

For testing we provide an Oauth2 backend which offers the following two Oauth2 endpoints:

 - Auth URL:  https://auth-fra1.rpcpool.com:8443/oauth2/auth
 - Token URL: https://auth-fra1.rpcpool.com:8443/oauth2/token

Your solution should be successfully able to work with the above endpoints. 


### Oauth2 Credentials

To run this, you will need to have two pieces of credentials pre-registered with the Oauth2 backend above:

 1. `client_id` - this is the client id under which the credentials will be registered
 2. `redirect_url` - the redirect URL/callback URL that the Oauth2 server will use to send credentials at the end of the authentication flow

To get new credentials for testing e-mail support@triton.one. 


