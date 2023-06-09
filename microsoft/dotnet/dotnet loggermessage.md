code-generation for `LoggerMessage`

```cs
[LoggerMessage(EventId = 1, Level = LogLevel.Information, Message = "Getting secret: {secretName} from vault: {vaultAddress}")]
private static partial void LogGettingSecret(ILogger logger, String secretName, String vaultAddress);
```

# notes
message format string is ordered, the names are informational
