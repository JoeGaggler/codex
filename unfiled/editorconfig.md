
C# settings

```editorsettings
root = true

[*.cs]
indent_style = tab
tab_width = 4
insert_final_newline = true

# fix formatting (https://docs.microsoft.com/en-us/dotnet/fundamentals/code-analysis/style-rules/formatting-rules)
dotnet_diagnostic.IDE0055.severity = suggestion
dotnet_sort_system_directives_first = true
dotnet_separate_import_directive_groups = true
dotnet_separate_import_directive_groups = true
dotnet_style_namespace_match_folder = true
csharp_indent_case_contents = true
csharp_indent_case_contents_when_block = false
csharp_style_namespace_declarations = file_scoped:suggestion #NEW!

# always surround single-statement blocks with braces
dotnet_diagnostic.IDE0011.severity = warning
csharp_prefer_braces = true

# simplify string interpolation
dotnet_diagnostic.IDE0071.severity = warning
dotnet_style_prefer_simplified_interpolation = true

# use pattern matching
dotnet_diagnostic.IDE0078.severity = warning
csharp_style_prefer_pattern_matching = true

# use "not" pattern
dotnet_diagnostic.IDE0083.severity = warning
csharp_style_prefer_not_pattern = true

# use pattern matching instead of "as"
dotnet_diagnostic.IDE0019.severity = warning
csharp_style_pattern_matching_over_as_with_null_check = true

# use pattern matching instead of "is"
dotnet_diagnostic.IDE0020.severity = warning
csharp_style_pattern_matching_over_is_with_cast_check = true

# add accessibility modifiers
dotnet_diagnostic.IDE0040.severity = warning
dotnet_style_require_accessibility_modifiers = true

# turn off warning about missing ConfigureAwait 
dotnet_diagnostic.CA2007.severity = none

# quality
dotnet_diagnostic.CA2213.severity = error # disposable fields
dotnet_diagnostic.CA2215.severity = error # call base.Dispose()
dotnet_diagnostic.CA2245.severity = error # do not assign property to itself
dotnet_diagnostic.CA2247.severity = error # incorrect use of TaskCompletionSource

# unnecessary assignment
dotnet_diagnostic.IDE0059.severity = warning
csharp_style_unused_value_assignment_preference = discard_variable

# stop using object.ReferenceEquals(x, y)
dotnet_diagnostic.IDE0041.severity = warning
dotnet_style_prefer_is_null_check_over_reference_equality_method = true

# static local functions
dotnet_diagnostic.IDE0062.severity = warning
csharp_prefer_static_local_function = true

```


## to be reverified:

```editorconfig
[*.cs]
indent_style = tab
tab_width = 4

# member qualification
dotnet_style_qualification_for_field = true:silent
dotnet_style_qualification_for_property = true:silent
dotnet_style_qualification_for_method = true:silent
dotnet_style_qualification_for_event = true:silent

# use pattern matching
csharp_style_inlined_variable_declaration = true:warning
dotnet_diagnostic.IDE0018.severity = warning    #csharp_style_inlined_variable_declaration
dotnet_diagnostic.IDE0041.severity = warning    #dotnet_style_prefer_is_null_check_over_reference_equality_method
dotnet_style_prefer_is_null_check_over_reference_equality_method = true:error

# suggest adding "readonly" when fields appear immutable
dotnet_style_readonly_field = true:suggestion

# preferred shorthand
csharp_style_conditional_delegate_call = true:warning
csharp_prefer_simple_default_expression = true:suggestion
dotnet_diagnostic.IDE0034.severity = suggestion    #csharp_prefer_simple_default_expression
dotnet_diagnostic.IDE1005.severity = warning    #csharp_style_conditional_delegate_call


```

add this to the `.csproj` to enable build warnings:
```xml
<PropertyGroup>
    <EnforceCodeStyleInBuild>true</EnforceCodeStyleInBuild>
</PropertyGroup>
```

#todo what does `AnalysisMode` do again?
```xml
<PropertyGroup>
    <AnalysisMode>All</AnalysisMode>
</PropertyGroup>
```


the file that `dotnet/roslyn` uses: https://github.com/dotnet/roslyn/blob/main/.editorconfig