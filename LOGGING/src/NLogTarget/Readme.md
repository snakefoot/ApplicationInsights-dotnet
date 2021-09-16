## NLog

[Microsoft.ApplicationInsights.NLogTarget](http://www.nuget.org/packages/Microsoft.ApplicationInsights.NLogTarget/)
[![Nuget](https://img.shields.io/nuget/vpre/Microsoft.ApplicationInsights.NLogTarget.svg)](https://www.nuget.org/packages/Microsoft.ApplicationInsights.NLogTarget/)

Application Insights NLog Target nuget package adds ApplicationInsights target in your web.config.

If your application does not have web.config then it can also be configured manually.

 * **Configure ApplicationInsightsTarget using NLog.config** :

```xml
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <extensions>
		<add assembly="Microsoft.ApplicationInsights.NLogTarget" />
    </extensions>
	<targets>
		<target xsi:type="ApplicationInsightsTarget" name="aiTarget">
			<instrumentationKey>Your_Resource_Key</instrumentationKey>	<!-- Only required if not using ApplicationInsights.config -->
			<contextproperty name="threadid" layout="${threadid}" />	<!-- Can be repeated with more context -->
		</target>
	</targets>
	<rules>
		<logger name="*" minlevel="Trace" writeTo="aiTarget" />
	</rules>
</nlog>
```

```csharp
// You need this only if you did not define InstrumentationKey in ApplicationInsights.config (Or in the NLog.config)
TelemetryConfiguration.Active.InstrumentationKey = "Your_Resource_Key";

Logger logger = LogManager.GetLogger("Example");

logger.Trace("trace log message");
```

* **Configure ApplicationInsightsTarget using NLog Config API** :
If you configure NLog programmatically with the [NLog Config API](https://github.com/nlog/NLog/wiki/Configuration-API), then create Application Insights target in code and add it to your other targets:

```csharp
var config = new LoggingConfiguration();

ApplicationInsightsTarget target = new ApplicationInsightsTarget();
// You need this only if you did not define InstrumentationKey in ApplicationInsights.config or want to use different instrumentation key
target.InstrumentationKey = "Your_Resource_Key";

LoggingRule rule = new LoggingRule("*", LogLevel.Trace, target);
config.LoggingRules.Add(rule);

LogManager.Configuration = config;

Logger logger = LogManager.GetLogger("Example");

logger.Trace("trace log message");
``` 