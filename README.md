# How to add nodes to bound mode TreeView in Xamarin.Forms (SfTreeView)

You can add nodes at runtime to bound mode [SfTreeView](https://help.syncfusion.com/xamarin/treeview/overview?)  in Xamarin.Forms by updating the bound collection from **ViewModel**.

You can also refer the following article.

https://www.syncfusion.com/kb/11487/how-to-add-nodes-to-bound-mode-treeview-in-xamarin-forms-sftreeview

**C#**

ViewModel bound collection updated in **OnAddItem** handler.
``` c#
public class FileManagerViewModel
{
    public Command OnAddItem { get; set; }
 
    public FileManagerViewModel()
    {
        GenerateSource();
        OnAddItem = new Command(OnAddItemMethod);
    }
    private void OnAddItemMethod(object obj)
    {
        Assembly assembly = typeof(MainPage).GetTypeInfo().Assembly;
        var game = new FileManager() { ItemName = "Game", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_folder.png", assembly) };
        var games = new FileManager() { ItemName = "Pubg.exe", ImageIcon = ImageSource.FromResource("TreeViewXamarin.Icons.treeview_exe.png", assembly) };
        game.SubFiles = new ObservableCollection<FileManager>
        {
            games
        };
        ImageNodeInfo.Add(game);
    }
}
```
**XAML**

ViewModel [command](https://docs.microsoft.com/en-us/dotnet/api/system.windows.input.icommand?view=netframework-4.8) bound to view to add item.
``` xml
<ContentPage.Content>
    <StackLayout Orientation="Vertical" Padding="5">
        <Button Text="Add Items" x:Name="addItem" HorizontalOptions="Fill" BackgroundColor="Blue" Command="{Binding OnAddItem}" />
        <syncfusion:SfTreeView x:Name="treeView" NotificationSubscriptionMode="CollectionChange,PropertyChange"  
                                ItemHeight="40"
                                Indentation="15"
                                ExpanderWidth="40"
                                ChildPropertyName="SubFiles"
                                ItemsSource="{Binding ImageNodeInfo}"
                                AutoExpandMode="AllNodesExpanded">
            <syncfusion:SfTreeView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <ViewCell.View>
                            <Grid x:Name="grid" RowSpacing="0" BackgroundColor="Transparent">
                                <Grid.RowDefinitions>
                                    <RowDefinition Height="*" />
                                    <RowDefinition Height="1" />
                                </Grid.RowDefinitions>
                                <Grid RowSpacing="0" Grid.Row="0">
                                    <Grid.ColumnDefinitions>
                                        <ColumnDefinition Width="40" />
                                        <ColumnDefinition Width="*" />
                                    </Grid.ColumnDefinitions>
                                    <Grid Padding="5,5,5,5">
                                        <Image
                                                Source="{Binding ImageIcon}"
                                                VerticalOptions="Center"
                                                HorizontalOptions="Center"
                                                HeightRequest="35" 
                                                WidthRequest="35"/>
                                    </Grid>
                                    <Grid Grid.Column="1"
                                                RowSpacing="1"
                                                Padding="1,0,0,0"
                                                VerticalOptions="Center">
                                        <Label LineBreakMode="NoWrap" TextColor="Black"
                                                    Text="{Binding ItemName}"
                                                    VerticalTextAlignment="Center">
                                        </Label>
                                    </Grid>
                                </Grid>
                                <StackLayout Grid.Row="1" HeightRequest="1"/>
                            </Grid>
                        </ViewCell.View>
                    </ViewCell>
                </DataTemplate>
            </syncfusion:SfTreeView.ItemTemplate>
        </syncfusion:SfTreeView>
    </StackLayout>
</ContentPage.Content>
```
