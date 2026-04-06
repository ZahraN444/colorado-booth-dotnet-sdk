
# Custom Header Signature



Documentation for accessing and setting credentials for apiHeader.

## Auth Credentials

| Name | Type | Description | Setter | Getter |
|  --- | --- | --- | --- | --- |
| Token | `string` | - | `Token` | `Token` |
| ApiKey | `string` | - | `ApiKey` | `ApiKey` |



**Note:** Auth credentials can be set using `ApiHeaderCredentials` in the client builder and accessed through `ApiHeaderCredentials` method in the client instance.

## Usage Example

### Client Initialization

You must provide credentials in the client as shown in the following code snippet.

```csharp
using MultiAuthSample.Standard;
using MultiAuthSample.Standard.Authentication;

namespace ConsoleApp;

MultiAuthSampleClient client = new MultiAuthSampleClient.Builder()
    .ApiHeaderCredentials(
        new ApiHeaderModel.Builder(
            "token",
            "api-key"
        )
        .Build())
    .Build();
```


