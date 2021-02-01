# Using MSG SDKs with MSG Server

To use a MSG SDK with MSG Server, change the server URL to your MSG API URL. For example, if you have MSG Server running locally mounted at /parse:

**iOS / OS X / watchOS / tvOS**

_Swift_

```swift
let configuration = ParseClientConfiguration {
    $0.applicationId = "YOUR_APP_ID"
    $0.clientKey = ""
    $0.server = "http://localhost:1337/parse"
}
Parse.initialize(with: configuration)
```

_Objective-C_

```objc
[Parse initializeWithConfiguration:[ParseClientConfiguration configurationWithBlock:^(id<ParseMutableClientConfiguration> configuration) {
   configuration.applicationId = @"YOUR_APP_ID";
   configuration.clientKey = @"";
   configuration.server = @"http://localhost:1337/parse";
}]];
```

**Android**

```java
Parse.initialize(new MSG.Configuration.Builder(myContext)
    .applicationId("YOUR_APP_ID")
    .server("http://localhost:1337/parse/")
    ...
    .build()
);
```

**JavaScript**

```js
Parse.initialize("YOUR_APP_ID");
Parse.serverURL = 'http://localhost:1337/parse'
```

**.NET**

```csharp
ParseClient.initialize(new ParseClient.Configuration {
    ApplicationId = "YOUR_APP_ID",
    Server = "http://localhost:1337/parse/"
});
```

**PHP**

```php
ParseClient::initialize('YOUR_APP_ID', 'YOUR_CLIENT_KEY', 'YOUR_MASTER_KEY');
ParseClient::setServerURL('http://localhost:1337', 'parse'); // server url & mount path passed separately
```
