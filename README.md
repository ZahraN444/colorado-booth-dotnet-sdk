
# Getting Started with MultiAuth-Sample

## Introduction

API for Markdown Notes app.

## Install the Package

If you are building with .NET CLI tools then you can also use the following command:

```bash
dotnet add package ColoradoBoothSDK --version 1.1.3
```

You can also view the package at:
https://www.nuget.org/packages/ColoradoBoothSDK/1.1.3

## Test the SDK

The generated SDK also contain one or more Tests, which are contained in the Tests project. In order to invoke these test cases, you will need `NUnit 3.0 Test Adapter Extension` for Visual Studio. Once the SDK is complied, the test cases should appear in the Test Explorer window. Here, you can click `Run All` to execute these test cases.

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| AccessToken2 | `string` |  |
| Port | `string` | *Default*: `"80"` |
| Suites | `Models.SuiteCodeEnum` | *Default*: `SuiteCodeEnum.Hearts` |
| Environment | [`Environment`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/README.md#environments) | The API environment. <br> **Default: `Environment.Testing`** |
| Timeout | `TimeSpan` | Http client timeout.<br>*Default*: `TimeSpan.FromSeconds(100)` |
| HttpClientConfiguration | [`Action<HttpClientConfiguration.Builder>`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-client-configuration-builder.md) | Action delegate that configures the HTTP client by using the HttpClientConfiguration.Builder for customizing API call settings.<br>*Default*: `new HttpClient()` |
| BasicAuthCredentials | [`BasicAuthCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/basic-authentication.md) | The Credentials Setter for Basic Authentication |
| ApiKeyCredentials | [`ApiKeyCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/custom-query-parameter.md) | The Credentials Setter for Custom Query Parameter |
| ApiHeaderCredentials | [`ApiHeaderCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/custom-header-signature.md) | The Credentials Setter for Custom Header Signature |
| OAuthCCGCredentials | [`OAuthCCGCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-client-credentials-grant.md) | The Credentials Setter for OAuth 2 Client Credentials Grant |
| OAuthACGCredentials | [`OAuthACGCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-authorization-code-grant.md) | The Credentials Setter for OAuth 2 Authorization Code Grant |
| OAuthROPCGCredentials | [`OAuthROPCGCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-resource-owner-credentials-grant.md) | The Credentials Setter for OAuth 2 Resource Owner Credentials Grant |
| OAuthBearerTokenCredentials | [`OAuthBearerTokenCredentials`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-bearer-token.md) | The Credentials Setter for OAuth 2 Bearer token |

The API client can be initialized as follows:

### Code-Based Initialization

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

### Configuration-Based Initialization

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

See the [Configuration-Based Initialization](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/configuration-based-initialization.md) section for details.

## Environments

The SDK can be configured to use a different environment for making API calls. Available environments are:

### Fields

| Name | Description |
|  --- | --- |
| Production | - |
| Testing | **Default** |

## Authorization

This API uses the following authentication schemes.

* [`basicAuth (Basic Authentication)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/basic-authentication.md)
* [`apiKey (Custom Query Parameter)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/custom-query-parameter.md)
* [`apiHeader (Custom Header Signature)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/custom-header-signature.md)
* [`OAuthCCG (OAuth 2 Client Credentials Grant)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-client-credentials-grant.md)
* [`OAuthACG (OAuth 2 Authorization Code Grant)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-authorization-code-grant.md)
* [`OAuthROPCG (OAuth 2 Resource Owner Credentials Grant)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-resource-owner-credentials-grant.md)
* [`OAuthBearerToken (OAuth 2 Bearer token)`](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/auth/oauth-2-bearer-token.md)
* `CustomAuth (Custom Authentication)`

## List of APIs

* [Authentication](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/controllers/authentication.md)

## SDK Infrastructure

### Configuration

* [Configuration-Based Initialization](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/configuration-based-initialization.md)
* [HttpClientConfiguration](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-client-configuration.md)
* [HttpClientConfigurationBuilder](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-client-configuration-builder.md)
* [ProxyConfigurationBuilder](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/proxy-configuration-builder.md)

### HTTP

* [HttpCallback](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-callback.md)
* [HttpContext](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-context.md)
* [HttpRequest](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-request.md)
* [HttpResponse](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-response.md)
* [HttpStringResponse](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/http-string-response.md)

### Utilities

* [ApiException](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/api-exception.md)
* [ApiHelper](https://www.github.com/ZahraN444/colorado-booth-dotnet-sdk/tree/1.1.3/doc/api-helper.md)

