# JsonStreamLogger

[![Build Status](https://dev.azure.com/misuzilla/JsonStreamLogger/_apis/build/status/mayuki.JsonStreamLogger?branchName=master)](https://dev.azure.com/misuzilla/JsonStreamLogger/_build/latest?definitionId=17&branchName=master) 
[![NuGet](https://img.shields.io/nuget/v/JsonStreamLogger?style=plastic)](https://www.nuget.org/packages/JsonStreamLogger)

JSON Stream logger provider implementation for Microsoft.Extensions.Logging.

## Requirements
- Compatible with .NET Standard 2.0
    - .NET Core 3.0 (Windows, Linux, macOS)
    - .NET Core 2.2 (Windows, Linux, macOS)
    - .NET Framework 4.6.1

## Install
https://www.nuget.org/packages/JsonStreamLogger

```
dotnet add package JsonStreamLogger
```

## Usage and output samples

```csharp
serviceCollection.AddLogging(options =>
{
    // Enable JsonStreamLogger logger provider
    // By default, logger writes JSON to stdout stream.
    options.AddJsonStream(); 
});
```

```csharp
logger.Log(LogLevel.Information, "[{Id}] is {Hello}", 12345, "Konnnichiwa");
logger.Log(LogLevel.Warning, new EventId(987, "NanikaEvent"), "[{Id}] is {Hello}", 67890, "Nya-n");
logger.LogError(ex, "[{Id}] is {ExceptionType}: {ExceptionMessage}", 77777, ex.GetType().FullName, ex.Message);
```

### Outputs
```json
{"Category":"Test","LogLevel":2,"EventId":{"Id":0,"Name":null},"State":{"Id":12345,"Hello":"Konnnichiwa"},"Exception":null,"Message":"[12345] is Konnnichiwa"}
{"Category":"Test","LogLevel":3,"EventId":{"Id":987,"Name":"NanikaEvent"},"State":{"Id":67890,"Hello":"Nya-n"},"Exception":null,"Message":"[67890] is Nya-n"}
{"Category":"Test","LogLevel":4,"EventId":{"Id":0,"Name":null},"State":{"Id":77777,"ExceptionType":"System.Exception","ExceptionMessage":"Yabai"},"Exception":{"Name":"System.Exception","Message":"Yabai","StackTrace":"(snip)","InnerException":null}},"Message":"[77777] is System.Exception: Yabai"}
```
