## Log4Net

[Microsoft.ApplicationInsights.Log4NetAppender](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Log4NetAppender/)
[![Nuget](https://img.shields.io/nuget/vpre/Microsoft.ApplicationInsights.Log4NetAppender.svg)](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Log4NetAppender/)

Application Insights Log4Net adapter nuget modifies web.config and adds Application Insights Appender.

For more information, see [Log4Net Configuration](https://logging.apache.org/log4net/release/manual/configuration.html)

```csharp
// You do not need this if you have instrumentation key in the ApplicationInsights.config
TelemetryConfiguration.Active.InstrumentationKey = "Your_Resource_Key";

log4net.Config.XmlConfigurator.Configure();
var logger = LogManager.GetLogger(this.GetType());

logger.Info("Message");
logger.Warn("A warning message");
logger.Error("An error message");