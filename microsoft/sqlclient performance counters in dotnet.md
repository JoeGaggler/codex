```cs
public class PerformanceCounterListener : EventListener
{
	private const string SqlClientEventSourceName = "Microsoft.Data.SqlClient.EventSource";

	protected override void OnEventSourceCreated(EventSource eventSource)
	{
		if (eventSource?.Name is not String name) { return;	}

		// Only enable events from SqlClientEventSource.
		if (name.Equals(SqlClientEventSourceName, StringComparison.InvariantCultureIgnoreCase))
		{
			var options = new Dictionary<string, string>
			{
				// define time interval 60 seconds
				// without defining this parameter event counters will not enabled
				{ "EventCounterIntervalSec", "60" }
			};

			EnableEvents(eventSource, EventLevel.Informational, EventKeywords.None, options);
		}
	}

	// This callback runs whenever an event is written by SqlClientEventSource.
	// Event data is accessed through the EventWrittenEventArgs parameter.
	protected override void OnEventWritten(EventWrittenEventArgs eventData)
	{
		if (eventData?.Payload?.FirstOrDefault(payloadItem => payloadItem is IDictionary<String, Object> payloadMap && payloadMap.ContainsKey("Name")) is not IDictionary<String, Object> counterMap) { return; }
		if (!counterMap.TryGetValue("Name", out Object? oName) || oName is not string counterName) { return; }
		if (!counters.TryGetValue("Mean", out Object value) && value is double counterValue) { return; }
		// TODO: log name and value
	}
}
```
