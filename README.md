# how-to-animate-items-in-.net-maui-listview

This repository contains a sample demonstrating how to animate items in .NET MAUI ListView (SfListView).

## Sample

```xaml
<ContentPage.Behaviors>
    <local:Behaviours />
</ContentPage.Behaviors>

<SearchBar
    x:Name="filterText"
    Grid.Row="0"
    HeightRequest="50"
    Placeholder="Search here to filter" />

<listView:SfListView
    x:Name="listView"
    Grid.Row="1"
    AllowGroupExpandCollapse="True"
    ItemSize="60"
    ItemsSource="{Binding CustomerDetails}">

    <listView:SfListView.ItemTemplate>
        <DataTemplate>
            <Grid x:Name="grid">
                <Grid.RowDefinitions>
                    <RowDefinition Height="*" />
                    <RowDefinition Height="1" />
                </Grid.RowDefinitions>

                <Grid
                    Grid.Column="0"
                    Padding="0,5,0,0"
                    RowSpacing="1"
                    VerticalOptions="Start">
                    <Grid.RowDefinitions>
                        <RowDefinition Height="*" />
                        <RowDefinition Height="*" />
                    </Grid.RowDefinitions>

                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="*" />
                        <ColumnDefinition Width="Auto" />
                    </Grid.ColumnDefinitions>

                    <Label
                        Grid.Row="0"
                        Grid.Column="0"
                        FontAttributes="Bold"
                        FontSize="18"
                        LineBreakMode="NoWrap"
                        Text="{Binding ContactName}"
                        TextColor="Teal"
                        VerticalOptions="Start" />
                    <Label
                        Grid.Row="1"
                        Grid.Column="0"
                        FontSize="12"
                        LineBreakMode="NoWrap"
                        Text="{Binding ContactNumber}"
                        TextColor="Teal" />
                    <Label
                        Grid.Row="0"
                        Grid.Column="1"
                        Margin="5"
                        Padding="0,0,10,0"
                        FontSize="10"
                        LineBreakMode="NoWrap"
                        Text="{Binding ContactType}"
                        TextColor="Teal"
                        VerticalOptions="End"
                        VerticalTextAlignment="End" />
                </Grid>
                <StackLayout
                    Grid.Row="1"
                    BackgroundColor="Gray"
                    HeightRequest="1" />
            </Grid>
        </DataTemplate>
    </listView:SfListView.ItemTemplate>
</listView:SfListView>
```

```c#
private bool FilterContacts(object obj)
{
    if (searchBar == null || searchBar.Text == null)
        return true;

    var contacts = obj as Contacts;
    if (contacts.ContactName.ToLower().Contains(searchBar.Text.ToLower())
        || contacts.ContactName.ToLower().Contains(searchBar.Text.ToLower()))
        return true;
    else
        return false;
}

private void SearchBar_TextChanged(object sender, TextChangedEventArgs e)
{
    searchBar = (sender as SearchBar);
    if (listView.DataSource != null)
    {
        this.listView.DataSource.Filter = FilterContacts;
        this.listView.DataSource.RefreshFilter();
    }
}

public class ItemGeneratorExt : ItemsGenerator
{        
    public ItemGeneratorExt(SfListView listview) : base(listview)
    {
        
    }
    protected override ListViewItem OnCreateListViewItem(int itemIndex, ItemType type, object data = null)
    {
        if (type == ItemType.Record)
            return new ListViewItemExt();
        return base.OnCreateListViewItem(itemIndex, type, data);
    }
}
public class ListViewItemExt : ListViewItem
{        
    public ListViewItemExt()
    {            
    }
    protected override void OnItemAppearing()
    {
        this.Opacity = 0;
        this.FadeTo(1, 400, Easing.SinInOut);
        base.OnItemAppearing();
    }       
}
```

## Requirements to run the demo

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) or [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)
* Xamarin add-ons for Visual Studio (available via the Visual Studio installer).

## Troubleshooting

### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.
