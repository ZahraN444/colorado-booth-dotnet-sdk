
# Client Class Documentation

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| AccessToken2 | `string` |  |
| Port | `string` | *Default*: `"80"` |
| Suites | `Models.SuiteCodeEnum` | *Default*: `SuiteCodeEnum.Hearts` |
| Environment | [`Environment`](../README.md#environments) | The API environment. <br> **Default: `Environment.Testing`** |
| Timeout | `TimeSpan` | Http client timeout.<br>*Default*: `TimeSpan.FromSeconds(100)` |
| HttpClientConfiguration | [`Action<HttpClientConfiguration.Builder>`](../doc/http-client-configuration-builder.md) | Action delegate that configures the HTTP client by using the HttpClientConfiguration.Builder for customizing API call settings.<br>*Default*: `new HttpClient()` |
| BasicAuthCredentials | [`BasicAuthCredentials`](auth/basic-authentication.md) | The Credentials Setter for Basic Authentication |
| ApiKeyCredentials | [`ApiKeyCredentials`](auth/custom-query-parameter.md) | The Credentials Setter for Custom Query Parameter |
| ApiHeaderCredentials | [`ApiHeaderCredentials`](auth/custom-header-signature.md) | The Credentials Setter for Custom Header Signature |
| OAuthCCGCredentials | [`OAuthCCGCredentials`](auth/oauth-2-client-credentials-grant.md) | The Credentials Setter for OAuth 2 Client Credentials Grant |
| OAuthACGCredentials | [`OAuthACGCredentials`](auth/oauth-2-authorization-code-grant.md) | The Credentials Setter for OAuth 2 Authorization Code Grant |
| OAuthROPCGCredentials | [`OAuthROPCGCredentials`](auth/oauth-2-resource-owner-credentials-grant.md) | The Credentials Setter for OAuth 2 Resource Owner Credentials Grant |
| OAuthBearerTokenCredentials | [`OAuthBearerTokenCredentials`](auth/oauth-2-bearer-token.md) | The Credentials Setter for OAuth 2 Bearer token |

The API client can be initialized as follows:

## Code-Based Initialization

```csharp
using MultiAuthSample.Standard;
using MultiAuthSample.Standard.Authentication;
using MultiAuthSample.Standard.Models;
using System.Collections.Generic;

namespace ConsoleApp;

MultiAuthSampleClient client = new MultiAuthSampleClient.Builder()
    .BasicAuthCredentials(
        new BasicAuthModel.Builder(
            "Username",
            "Password"
        )
        .Build())
    .ApiKeyCredentials(
        new ApiKeyModel.Builder(
            "token",
            "api-key"
        )
        .Build())
    .ApiHeaderCredentials(
        new ApiHeaderModel.Builder(
            "token",
            "api-key"
        )
        .Build())
    .OAuthCCGCredentials(
        new OAuthCCGModel.Builder(
            "OAuthClientId",
            "OAuthClientSecret"
        )
        .Build())
    .OAuthACGCredentials(
        new OAuthACGModel.Builder(
            "OAuthClientId",
            "OAuthClientSecret",
            "OAuthRedirectUri"
        )
        .OAuthScopes(
            new List<OAuthScopeOAuthACGEnum>
            {
                OAuthScopeOAuthACGEnum.ReadScope,
            })
        .Build())
    .OAuthROPCGCredentials(
        new OAuthROPCGModel.Builder(
            "OAuthClientId",
            "OAuthClientSecret",
            "OAuthUsername",
            "OAuthPassword"
        )
        .Build())
    .OAuthBearerTokenCredentials(
        new OAuthBearerTokenModel.Builder(
            "AccessToken"
        )
        .Build())
    .HttpClientConfig(httpClientConfig =>
        httpClientConfig.Timeout(TimeSpan.FromSeconds(100)))
    .AccessToken2("accessToken")
    .Environment(MultiAuthSample.Standard.Environment.Testing)
    .Port("80")
    .Suites(SuiteCodeEnum.Hearts)
    .Build();
```

## Configuration-Based Initialization

```csharp
using MultiAuthSample.Standard;
using Microsoft.Extensions.Configuration;

namespace ConsoleApp;

// Build the IConfiguration using .NET conventions (JSON, environment, etc.)
var configuration = new ConfigurationBuilder()
    .AddJsonFile("config.json")
    .AddEnvironmentVariables() // [optional] read environment variables
    .Build();

// Instantiate your SDK and configure it from IConfiguration
var client = MultiAuthSampleClient
    .FromConfiguration(configuration.GetSection("MultiAuthSample"));
```

See the [Configuration-Based Initialization](../doc/configuration-based-initialization.md) section for details.

## MultiAuth-SampleClient Class

The gateway for the SDK. This class acts as a factory for the Controllers and also holds the configuration of the SDK.

### Controllers

| Name | Description |
|  --- | --- |
| AuthenticationController | Gets AuthenticationController controller. |
| OAuthAuthorizationController | Gets OAuthAuthorizationController controller. |

### Properties

| Name | Description | Type |
|  --- | --- | --- |
| HttpClientConfiguration | Gets the configuration of the Http Client associated with this client. | [`IHttpClientConfiguration`](../doc/http-client-configuration.md) |
| Timeout | Http client timeout. | `TimeSpan` |
| AccessToken2 | - | `string` |
| Environment | Current API environment. | `Environment` |
| Port | Port value. | `string` |
| Suites | Suites value. | `Models.SuiteCodeEnum` |
| BasicAuthCredentials | Gets the credentials to use with BasicAuth. | [`IBasicAuthCredentials`](auth/basic-authentication.md) |
| ApiKeyCredentials | Gets the credentials to use with ApiKey. | [`IApiKeyCredentials`](auth/custom-query-parameter.md) |
| ApiHeaderCredentials | Gets the credentials to use with ApiHeader. | [`IApiHeaderCredentials`](auth/custom-header-signature.md) |
| OAuthCCGCredentials | Gets the credentials to use with OAuthCCG. | [`IOAuthCCGCredentials`](auth/oauth-2-client-credentials-grant.md) |
| OAuthACGCredentials | Gets the credentials to use with OAuthACG. | [`IOAuthACGCredentials`](auth/oauth-2-authorization-code-grant.md) |
| OAuthROPCGCredentials | Gets the credentials to use with OAuthROPCG. | [`IOAuthROPCGCredentials`](auth/oauth-2-resource-owner-credentials-grant.md) |
| OAuthBearerTokenCredentials | Gets the credentials to use with OAuthBearerToken. | [`IOAuthBearerTokenCredentials`](auth/oauth-2-bearer-token.md) |

### Methods

| Name | Description | Return Type |
|  --- | --- | --- |
| `GetBaseUri(Server alias = Server.Default)` | Gets the URL for a particular alias in the current environment and appends it with template parameters. | `string` |
| `ToBuilder()` | Creates an object of the MultiAuth-SampleClient using the values provided for the builder. | `Builder` |

## MultiAuth-SampleClient Builder Class

Class to build instances of MultiAuth-SampleClient.

### Methods

| Name | Description | Return Type |
|  --- | --- | --- |
| `HttpClientConfiguration(Action<`[`HttpClientConfiguration.Builder`](../doc/http-client-configuration-builder.md)`> action)` | Gets the configuration of the Http Client associated with this client. | `Builder` |
| `Timeout(TimeSpan timeout)` | Http client timeout. | `Builder` |
| `AccessToken2(string accessToken2)` | - | `Builder` |
| `Environment(Environment environment)` | Current API environment. | `Builder` |
| `Port(string port)` | Port value. | `Builder` |
| `Suites(Models.SuiteCodeEnum suites)` | Suites value. | `Builder` |
| `BasicAuthCredentials(Action<BasicAuthModel.Builder> action)` | Sets credentials for BasicAuth. | `Builder` |
| `ApiKeyCredentials(Action<ApiKeyModel.Builder> action)` | Sets credentials for ApiKey. | `Builder` |
| `ApiHeaderCredentials(Action<ApiHeaderModel.Builder> action)` | Sets credentials for ApiHeader. | `Builder` |
| `OAuthCCGCredentials(Action<OAuthCCGModel.Builder> action)` | Sets credentials for OAuthCCG. | `Builder` |
| `OAuthACGCredentials(Action<OAuthACGModel.Builder> action)` | Sets credentials for OAuthACG. | `Builder` |
| `OAuthROPCGCredentials(Action<OAuthROPCGModel.Builder> action)` | Sets credentials for OAuthROPCG. | `Builder` |
| `OAuthBearerTokenCredentials(Action<OAuthBearerTokenModel.Builder> action)` | Sets credentials for OAuthBearerToken. | `Builder` |

