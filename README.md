# rpc-oauth-client
A "headless" Oauth client (PKCE) for Solana RPC services.

Web3 operates on a principal of user anonymity. However, this anonymity creates a vector for bad actors to abuse backend systems. It is currently too easy to spoof an origin header and gain access to free RPC services.

An important point of distinction is that the user does not need to reveal their identity to use the service. This is headless OAuth in the sense that the user is not asked to identify themselves with the more familiar OAuth services offered by Github, Twitter, etc. The RPC-OAuth-Client allows a dApp to prove that RPC requests originate from their approved website.

## Solana Breakpoint Hackathon RPC OAuth Client Prize
We are offering a 5,000 USDC prize for the person or team who completes a working headless OAuth client during the Solana Breakpoint Hackathon. The team who takes the challenge will also be eligible for the overall prize of 10,000 USDC (based solely on the opinion of the Solana Breakpoint Hackathon judges).

Your oauth client needs to be able to support a PKCE Oauth flow. There is a sample that you can use for inspiration at https://auth0.com/docs/libraries/auth0-single-page-app-sdk.

The final solution needs to work with the current Solana Web3.js library (https://github.com/solana-labs/solana-web3.js). The solution can be implemented as a plugin, wrapper, or incorporated directly into the solana-web3.js library via PR. The final solution is to be determined by the contributors.

The final solution must be open source.

The final solution must be secure with no obvious vectors for abuse.

Eligibility for the Prize is determined by our judges: Brian Long & Linus Kendall.

## Backend Servers
We are providing backend servers to use for the competition.

### Credentials
To run this, you will need to have two pieces of credentials pre-registered:

 1. `client_id` - this is the client that maps
 2. `redirect_url` - the redirect URL that you will use

To get new credentials for testing e-mail support@triton.one.

### OAuth2 endpoints
For testing we provide two oauth endpoints:

 - Auth URL:  https://auth-fra1.rpcpool.com:8443/oauth2/auth
 - Token URL: https://auth-fra1.rpcpool.com:8443/oauth2/token
