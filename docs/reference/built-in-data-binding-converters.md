---
description: REFERENCE
---

# Built-in Data Binding Converters

_Avalonia UI_ includes a number of built-in data binding converters for common scenarios:

| Converter                           | Description                                                                                                                         |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Negation Operator                   | The ! operator can be placed in front of the data binding path to return the inversion of a Boolean value. See also the note below. |
| `StringConverters.IsNullOrEmpty`    | Returns `true` if the input string is null or empty                                                                                 |
| `StringConverters.IsNotNullOrEmpty` | Returns `false` if the input string is null or empty                                                                                |
| `ObjectConverters.IsNull`           | Returns `true` if the input is null                                                                                                 |
| `ObjectConverters.IsNotNull`        | Returns `false` if the input is null                                                                                                |
| `BoolConverters.And`                | A multi-value converter that returns `true` if all inputs are true.                                                                 |
| `BoolConverters.Or`                 | A multi-value converter that returns `true` if any input is true.                                                                   |

## Negation Operator Examples

This example shows the text block when the bound value is false:

```markup
<StackPanel>
  <TextBox Name="input" IsEnabled="{Binding AllowInput}"/>
  <TextBlock IsVisible="{Binding !AllowInput}">Input is not allowed</TextBlock>
</StackPanel>
```

Negation also works when you bind to a non-Boolean value. This works because the bound value is first converted to a Boolean (using the function `Convert.ToBoolean` ) and then the result is negated.&#x20;

For example, as the integer zero is converted to false (by the the function `Convert.ToBoolean`) and all other integer values are converted to true, you can use the negation operator to show a message when a collection is empty, like this:

```markup
<Panel>
  <ListBox Items="{Binding Items}"/>
  <TextBlock IsVisible="{Binding !Items.Count}">No results found</TextBlock>
</Panel>
```

You can also use the negation operator twice. For example, where you want to perform the conversion from integer to Boolean, and then negate that value.&#x20;

You can use this to hide a control when a collection is empty (count is zero), like this:

```markup
<Panel>
  <ListBox Items="{Binding Items}" IsVisible="{Binding !!Items.Count}"/>
</Panel>
```

## Other Conversion Examples

This example binding will hide the text block if its bound text is null or empty:

```markup
<TextBlock Text="{Binding MyText}"
           IsVisible="{Binding MyText, 
                       Converter={x:Static StringConverters.IsNotNullOrEmpty}}"/>
```

And this example will hide the content control if the bound object is null or empty:

```markup
<ContentControl Content="{Binding MyContent}"
                IsVisible="{Binding MyContent, 
                            Converter={x:Static ObjectConverters.IsNotNull}}"/>
```

## More Information


:::info
You can follow the Avalonia UI value converter sample, [here](https://github.com/AvaloniaUI/Avalonia.Samples/tree/main/src/Avalonia.Samples/MVVM/ValueConversionSample).
:::
