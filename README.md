NOTE: THIS PRIZE HAS ALREADY BEEN CLAIMED. The Breakpoint event was held in 2021. 

# rpc-oauth-client
A "headless" Oauth client (PKCE) for Solana RPC services.

Web3 operates on a principal of user anonymity. However, this anonymity creates a vector for bad actors to abuse backend systems. It is currently too easy to spoof an origin header and gain access to free RPC services.

An important point of distinction is that the user does not need to reveal their identity to use the service. This is headless OAuth in the sense that the user is not asked to identify themselves with the more familiar OAuth services offered by Github, Twitter, etc. The RPC-OAuth-Client allows a dApp to prove that RPC requests originate from their approved website.

## Solana Breakpoint Hackathon RPC OAuth Client Prize
NOTE: THIS PRIZE HAS ALREADY BEEN CLAIMED. The Breakpoint event was held in 2021. We offered a 5,000 USDC prize for the person or team who completes a working headless OAuth client during the Solana Breakpoint Hackathon. The team who takes the challenge will also be eligible for the overall prize of 10,000 USDC (based solely on the opinion of the Solana Breakpoint Hackathon judges).

Your Oauth client needs to be able to support a PKCE Oauth2 flow. There is a sample that you can use for inspiration at https://auth0.com/docs/libraries/auth0-single-page-app-sdk.

The final solution needs to work with the current Solana Web3.js library (https://github.com/solana-labs/solana-web3.js). The solution can be implemented as a plugin, wrapper, or incorporated directly into the solana-web3.js library via PR. The final solution is to be determined by the contributors.

The final solution should include a sample frontend that demonstrates the use of the authentication framework and use of the Solana web3.js library to make an authenticated RPC request.

The final solution must be open source (MIT license). It must be based on original work, but you are free to rely upon existing MIT-licensed libraries and code.

The final solution must be secure with no obvious vectors for abuse.

Eligibility for the Prize is determined by our judges: Brian Long & Linus Kendall.

## Features

The integration should support:
  - Configuration of the parameters of an oauth2 pkce flow using custom auth/token urls along with custom requested scopes (sample ones below for testing)
  - Code verifier generation and validation for PKCE flow
  - Callback for receiving the initial authorization token and turning into a permanent token
  - Tracking expiry time of tokens received 
  - Renewal of tokens using a renewal token
  - Providing callbacks/information to the on issuance/expiry/renewal of tokens 

## Backend Servers

We are providing backend servers and Solana RPC access to use for the competition. We will set up VMs for your development and deploys as required.

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

