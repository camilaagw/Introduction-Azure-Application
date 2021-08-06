# Lesson 4: Security and monitoring basics

This lesson focuses on:
- Azure Active Directory
- OAuth 2.0
- Microsoft Authentication Library (MSAL)
- Redirecting the logs of an app to a storage account and creating access alerts

##  Security responsibilities: cloud developers and cloud provider

![Azure security responsabilities](img/azure-security-responsabilities.png)
- IaaS: The security of physical hardware shifts to the cloud provider
- PaaS: The operating system security shifts to be the responsibility of the cloud provider, while network,
 application and identity security are a shared responsibility.
- SaaS: The network and application shift responsibility to the cloud provider, but identity stays as a shared responsibility.

Security responsibilities that always stay with the cloud developer:
- Account and access management
- Client endpoints
- Data Governance and Rights Management
To register your app and get the necessary app information for the next exercise:

## Security and monitoring services in Azure
Security options in Azure:
- **Azure Active Directory**: Provides single sign-on (SSO) and multi-factor authentication (MFA) capabilities, such as Sign in with Microsoft
- **App Configuration**: Stores application settings in one secure location
- **Key Vault API**: Stores application keys and secrets in one secure location
- **Managed Identities**: A part of Azure Active Directory; This helps streamline providing an app or app user access to other Azure resources
- **Shared Access Signatures**: Give external parties certain limited access (determined by you) to different Azure resources
- **Role-Based Access Controls (RBAC)**: Help internally manage who has access to what resources, and what they can do to said resources
- **Azure Monitor**: Provides a wide range of monitoring services such as log analytics, metrics, alerts, and much more
- **Application Insights**: Part of Azure Monitor; This helps monitor performance and other key metrics

Besides the security options, Azure gives developers the ability to:
- Monitor metrics, such as performance and service quotas
- Use App-based logging
- Send logs to storage
- Create alerts
There are other monitoring and logging options, such as Application Insights and Log Analytics using the Kusto query language.

## Oauth2 with Azure

Oauth2 is the industry-standard protocol for authorization. Instead of creating apps that each maintain their username and password information,
apps can delegate that responsibility to a centralized identity provider.
To implement Oauth2 with Azure, we can use:
- **Azure Active Directory** as the centralized identity provider in the cloud
- **Microsoft Authentication Library (MSAL)**, a Python library to implement “Sign in with Microsoft”

### Authorization process with MSAL:

1. User clicks the “Sign in with Microsoft” and this will cause a browser pop-up. The user signing in will request an authorization code, from the /oauth/v2.0/authorize endpoint.
2. The OAuth2 provider, Microsoft in this case, will return an authorization code and will redirect the user to a specified endpoint in the app.
3. The app will request an access token. To do so, it needs to provide the authorization code along with information like client ID and client secret, in the case of Azure Active Directory.
The app can also request a certain scope, such as USER.READ, which would allow the app to read the user’s profile information. This will hit the /oauth/v2.0/token endpoint.
5. If the token is granted, it can be used to hit some secure endpoint. The endpoint must validate the token sent by the app.
It then will return the requested secure data, if the token is validated.

[Complete workflow](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)



## Recommended resources

* Oauth2 in detail: https://tools.ietf.org/html/rfc6749
* [IaaS security best practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/iaas)
* [PaaS security best practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/paas-deployments)

## Glossary

A tenant is a representation of an organization.
What is authentication?
Authentication is the process of establishing the identity of a person or service that wants to access a resource. It involves the act of challenging a party for legitimate credentials and provides the basis for creating a security principal for identity and access control. It establishes whether the user is who they say they are.

What is authorization?
Authentication establishes the user's identity, but authorization is the process of establishing what level of access an authenticated person or service has. It specifies what data they're allowed to access and what they can do with it.

Single sign-on (SSO) enables a user to sign in one time and use that credential to access multiple resources and applications.
Conditional Access is a tool that Azure AD uses to allow or deny access to resources based on identity signals such as the user's location.