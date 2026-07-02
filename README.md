# Building a Real Time Trader Grid App with .NET MAUI.

In this article, we will show you how to build a Real-Time Trader Grid application using Syncfusion .NET MAUI DataGrid (SfDataGrid). This sample demonstrates how to display stock market information in a highly customizable and responsive tabular view. The grid presents essential trading data such as stock symbols, company names, prices, market changes, volume, bid and ask values, market capitalization, and timestamp information. Template columns are used to provide custom cell rendering, including dynamic text coloring for positive and negative market movements and formatted market capitalization values through value converters. The DataGrid is configured with manual column generation, fill mode column sizing, multiple row selection, and built-in scrolling support, making it suitable for financial dashboards and trading applications. For more information, refer to the documentation: [.NET MAUI DataGrid Overview](https://www.syncfusion.com/maui-controls/maui-datagrid) and [Getting Started with .NET MAUI DataGrid](https://help.syncfusion.com/maui/datagrid/getting-started).

## xaml

```xml
<ContentPage.BindingContext>
    <local:StockViewModel x:Name="viewModel" />
</ContentPage.BindingContext>

<sfgrid:SfDataGrid x:Name="dataGrid"
                   ItemsSource="{Binding Stocks}"
                   AutoGenerateColumnsMode="None"
                   ColumnWidthMode="Fill"
                   HeaderRowHeight="58"
                   RowHeight="52"
                   SelectionMode="Multiple">

    <sfgrid:SfDataGrid.Columns>

        <sfgrid:DataGridTextColumn MappingName="Symbol"
                                   HeaderText="Symbol" />

        <sfgrid:DataGridTextColumn MappingName="CompanyName"
                                   HeaderText="Company Name" />

        <sfgrid:DataGridNumericColumn MappingName="Price"
                                      HeaderText="Price"
                                      Format="F2" />

        <sfgrid:DataGridTemplateColumn MappingName="Change"
                                       HeaderText="Change">
            <sfgrid:DataGridTemplateColumn.CellTemplate>
                <DataTemplate>
                    <Label Text="{Binding Change, StringFormat='{0:F2}'}"
                           TextColor="{Binding Change,
                           Converter={StaticResource textForegroundConverter}}" />
                </DataTemplate>
            </sfgrid:DataGridTemplateColumn.CellTemplate>
        </sfgrid:DataGridTemplateColumn>

    </sfgrid:SfDataGrid.Columns>

</sfgrid:SfDataGrid>
```

The page uses a `StockViewModel` as its BindingContext and binds the DataGrid's `ItemsSource` to a collection of stock records. Text, numeric, date, and template columns are combined to display trading information in a clean and structured layout. Template columns allow custom UI elements such as Labels with conditional formatting, making stock gains and losses easier to identify visually.

## C#

The following converter is used to dynamically change the text color based on stock performance values.

```csharp
internal class TextForegroundConverter : IValueConverter
{
        object? IValueConverter.Convert(object? value, Type targetType, object? parameter, CultureInfo info)
        {
            if (value is double numericValue) // Ensure value is a double
            {
                if (numericValue > 1 && numericValue <= 2)
                    return Colors.Green;
                else if (numericValue >= 0 && numericValue <= 1)
                    return Colors.Black;
                else
                    return Colors.Red;
            }

            return Colors.Gray; // Default color for invalid values
        }

        object? IValueConverter.ConvertBack(object? value, Type targetType, object? parameter, CultureInfo info)
        {
            throw new NotImplementedException();
        }
}
```

This converter helps traders quickly identify market trends by displaying positive values in green and negative values in red. Similar converters can also be used to format market capitalization, volume, or other financial indicators.

## Real-Time Trading Dashboard Features

- Display stock symbols, company names, and live pricing information.
- Highlight gains and losses using color-coded template columns.
- Format market capitalization values through custom converters.
- Enable multiple row selection for comparative stock analysis.
- Support horizontal and vertical scrolling for large datasets.
- Customize row height, header appearance, and column sizing for enhanced readability.
- Extend the ViewModel with timer-based or service-based updates to refresh stock values in real time.

##### Conclusion

I hope you enjoyed learning about how to build a Real-Time Trader Grid application using .NET MAUI DataGrid (SfDataGrid).

You can refer to our [.NET MAUI DataGrid’s feature tour](https://www.syncfusion.com/maui-controls/maui-datagrid) page to learn about its other groundbreaking feature representations. You can also explore our [.NET MAUI DataGrid Documentation](https://help.syncfusion.com/maui/datagrid/getting-started) to understand how to present and manipulate data. 
For current customers, you can check out our .NET MAUI components on the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page. If you are new to Syncfusion, you can try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to explore our .NET MAUI DataGrid and other .NET MAUI components.
 
If you have any queries or require clarifications, please let us know in the comments below. You can also contact us through our [support forums](https://www.syncfusion.com/forums), [Direct-Trac](https://support.syncfusion.com/create) or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sfdatagrid), or the feedback portal. We are always happy to assist you!
