# How to animate the items appearing in .NET MAUI ListView (SfListView)?

The [.NET MAUI ListView ](https://www.syncfusion.com/maui-controls/maui-listView) allows you to animate items as they come into view by overriding the [OnItemAppearing](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.ListView.ListViewItem.html#Syncfusion_Maui_ListView_ListViewItem_OnItemAppearing) method of [ListViewItem](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.ListView.ListViewItem.html). This method is raised when an item appears in the view, allowing for animation customization.

This can be achieved by extending the [ItemsGenerator](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.ListView.ItemsGenerator.html) class, applying animation for the listview items using the OnItemAppearing method and aborting animation for the collapsed item using the PropertyChanged event.

```
public class Behaviours: Behavior<SfListView>
{
   private SfListView listView;

   protected override void OnAttachedTo(BindableObject bindable)
   {

      listView = bindable as SfListView;

      listView.ItemsGenerator = new ItemGeneratorExt(listView);

      base.OnAttachedTo(bindable);
   }
}
```
 

Extending the ItemsGenerator class:

```
public class ItemGeneratorExt: ItemsGenerator
{
   public SfListView ListView { get; set; }

   public ItemGeneratorExt(SfListView listview): base(listview)
   {
      ListView = listview;
   }

   protected override ListViewItem OnCreateListViewItem(int itemIndex, ItemType type, object data = null)
   {

      if (type == ItemType.Record)

         return new ListViewItemExt(ListView);

      return base.OnCreateListViewItem(itemIndex, type, data);
   }
}
```
 

Customize ListViewItem to apply animations when an item appears.

```
public class ListViewItemExt: ListViewItem
{

   private SfListView _listView;

        

   public ListViewItemExt(SfListView listView)
   {

      _listView = listView;
   }

   protected override void OnItemAppearing()
   {

      this.Opacity = 0;

      this.FadeTo(1, 400, Easing.SinInOut);              

      base.OnItemAppearing();
   }

}
```


**Conclusion:**

I hope you enjoyed learning how to animate items in .NET MAUI ListView.

You can refer to our [.NET MAUI ListView feature tour](https://www.syncfusion.com/maui-controls/maui-listView) page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/maui/listview/getting-started), and how to quickly get started with configuration specifications. 

Check out our components from the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page for current customers. If you are new to Syncfusion®, try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

Please let us know in the comments section if you have any queries or require clarification. You can also contact us through our [support forums](https://www.syncfusion.com/forums/), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!
