
# Basic Authentication



Documentation for accessing and setting credentials for basicAuth.

## Auth Credentials

| Name | Type | Description | Setter | Getter |
|  --- | --- | --- | --- | --- |
| Username | `string` | The username to use with basic authentication | `Username` | `Username` |
| Password | `string` | The password to use with basic authentication | `Password` | `Password` |



**Note:** Auth credentials can be set using `BasicAuthCredentials` in the client builder and accessed through `BasicAuthCredentials` method in the client instance.

## Usage Example

### Client Initialization

You must provide credentials in the client as shown in the following code snippet.

```csharp
using MultiAuthSample.Standard;
using MultiAuthSample.Standard.Authentication;

namespace ConsoleApp;

MultiAuthSampleClient client = new MultiAuthSampleClient.Builder()
    .BasicAuthCredentials(
        new BasicAuthModel.Builder(
            "Username",
            "Password"
        )
        .Build())
    .Build();
```


