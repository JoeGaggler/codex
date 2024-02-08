
# setup

install:
```bash
dotnet new console
dotnet add package BenchmarkDotNet
```
run:
```bash
dotnet build -c Release -f net8.0
dotnet bin/Release/net8.0/foobar.dll
```

# code
program:
```csharp
using BenchmarkDotNet.Running;
var summary = BenchmarkRunner.Run<TestCases>();

[MemoryDiagnoser]
public class TestCases
{
	public TestCases()
	{
		// setup
	}

	[Benchmark]
	public void NewGen()
	{
	}

	[Benchmark]
	public void OldGen()
	{
	}
}
```
