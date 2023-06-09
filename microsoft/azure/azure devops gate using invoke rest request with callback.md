```yaml
- job: gate
  pool: server
  steps:
    - task: InvokeRESTAPI@1
	  inputs:
	    connectionType: 'connectedServiceName'
	    serviceConnection: 'myconnection' # setup in Service Connections
	    method: 'POST' # 'OPTIONS' | 'GET' | 'HEAD' | 'POST' | 'PUT' | 'DELETE' | 'TRACE' | 'PATCH'. Required. Method. Default: POST.
	    #headers: # string. Headers. 
	    body:
		  {
		    "pr": "$(system.pullRequest.pullRequestId)"
		  }
	  urlSuffix: /myapi?something=true
	  waitForCompletion: 'true'
```

```c#
[Function("PrGateFunction")]
public static async Task<HttpResponseData> PrGateFunctionAsync([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = "prGate")] HttpRequestData req, FunctionContext executionContext)
{
	var logger = executionContext.GetLogger("HttpFunction");
	logger.LogInformation("message logged");
	try
	{
		logger.LogInformation($"HTTP TRIGGER: {req.Method} {req.Url}");
		String? planUrl = req.Headers.TryGetValues("planurl", out var planUrlValues) ? planUrlValues.FirstOrDefault() : null;
		String? projectId = req.Headers.TryGetValues("projectid", out var projectIdValues) ? projectIdValues.FirstOrDefault() : null;
		String? hubName = req.Headers.TryGetValues("hubname", out var hubNameValues) ? hubNameValues.FirstOrDefault() : null;
		String? planId = req.Headers.TryGetValues("planid", out var planIdValues) ? planIdValues.FirstOrDefault() : null;
		String? jobId = req.Headers.TryGetValues("jobid", out var jobIdValues) ? jobIdValues.FirstOrDefault() : null;
		String? timelineId = req.Headers.TryGetValues("timelineid", out var timelineIdValues) ? timelineIdValues.FirstOrDefault() : null;
		String? taskInstanceId = req.Headers.TryGetValues("taskinstanceid", out var taskInstanceIdValues) ? taskInstanceIdValues.FirstOrDefault() : null;
		String? authToken = req.Headers.TryGetValues("authtoken", out var authTokenValues) ? authTokenValues.FirstOrDefault() : null;

		var resp =  req.CreateResponse(HttpStatusCode.OK);
		resp.Headers.Add("Content-Type", "text/html; charset=utf-8");
		resp.WriteString(curl);

		// TODO: post success from some other polling process
		await Task.Run(async () =>
		{
			// These use captured values, but in reality would be retrieved as part of polling
			var url = $"{planUrl}/{projectId}/_apis/distributedtask/hubs/{hubName}/plans/{planId}/events?api-version=2.0-preview.1";
			var successBody = $$"""{ "name": "TaskCompleted", "taskId": "{{taskInstanceId}}", "jobId": "{{jobId}}", "result": "succeeded" }""";
		
			var client = new HttpClient();
			var content = new StringContent(successBody, Encoding.UTF8, "application/json");
			var response = await client.PostAsync(url, content);
			logger.LogInformation($"CALLBACK RESPONSE: {response.StatusCode}");
		});
		
		return resp;
	}
	catch (Exception exc)
	{
		logger.LogError("HTTP TRIGGER ERROR: " + exc.ToString());
		var response = req.CreateResponse(HttpStatusCode.OK);
		response.Headers.Add("Content-Type", "text/html; charset=utf-8");
		response.WriteString("HTTP TRIGGER ERROR: " + exc.ToString());
		return response;
	}
}
```
