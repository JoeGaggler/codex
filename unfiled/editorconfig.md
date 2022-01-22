
C# settings

```editorconfig
[*.cs]
indent_style = tab
tab_width = 4

# display external references at the bottom
dotnet_sort_system_directives_first = true:warning

# switch cases are indented unless the contents are blocks
csharp_indent_case_contents = true:warning
csharp_indent_case_contents_when_block = false:warning

# always surround single-statement blocks with braces
csharp_prefer_braces = true:error
dotnet_diagnostic.IDE0011.severity = error    #csharp_prefer_braces

# require explicit access modifiers
dotnet_style_require_accessibility_modifiers = always:warning

# prefer file-scoped namespaces
csharp_style_namespace_declarations = file_scoped:suggestion

# member qualification
dotnet_style_qualification_for_field = true:silent
dotnet_style_qualification_for_property = true:silent
dotnet_style_qualification_for_method = true:silent
dotnet_style_qualification_for_event = true:silent

# use pattern matching
csharp_style_prefer_not_pattern = true:warning
csharp_style_prefer_pattern_matching = true:warning
csharp_style_pattern_matching_over_is_with_cast_check = true:warning
csharp_style_pattern_matching_over_as_with_null_check = true:warning
csharp_style_inlined_variable_declaration = true:warning
dotnet_diagnostic.IDE0018.severity = warning    #csharp_style_inlined_variable_declaration
dotnet_diagnostic.IDE0019.severity = warning    #csharp_style_pattern_matching_over_as_with_null_check
dotnet_diagnostic.IDE0020.severity = warning    #csharp_style_pattern_matching_over_is_with_cast_check
dotnet_diagnostic.IDE0041.severity = warning    #dotnet_style_prefer_is_null_check_over_reference_equality_method
dotnet_diagnostic.IDE0078.severity = warning    #csharp_style_prefer_pattern_matching
dotnet_diagnostic.IDE0083.severity = warning    #csharp_style_prefer_not_pattern
dotnet_style_prefer_is_null_check_over_reference_equality_method = true:error

# suggest adding "readonly" when fields appear immutable
dotnet_style_readonly_field = true:suggestion

# preferred shorthand
csharp_style_conditional_delegate_call = true:warning
csharp_prefer_simple_default_expression = true:suggestion
dotnet_diagnostic.IDE0034.severity = suggestion    #csharp_prefer_simple_default_expression
dotnet_diagnostic.IDE1005.severity = warning    #csharp_style_conditional_delegate_call

# CA2007: Consider calling ConfigureAwait on the awaited task
dotnet_diagnostic.CA2007.severity = none
```

add this to the `.csproj` to enable build warnings:
```xml
<PropertyGroup>
    <AnalysisMode>All</AnalysisMode>
    <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
</PropertyGroup>
```
