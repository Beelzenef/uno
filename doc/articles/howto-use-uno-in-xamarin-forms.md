# How to use Uno Platform Controls in Xamarin.Forms

All Uno Platform UI controls inherit directly from native views, which makes for an easy way for its controls to be integrated in Xamarin.iOS and Xamarin.Android projects.

Xamarin.Forms [provides a way](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/platform/native-views/code) to use native-inheriting views to be added as part of its visual tree.

## Add Uno views in Xamarin Forms XAML

Xamarin.Forms support adding views directly in XAML documents, using platform specific namespaces: 

```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:UnoFormsApp"
             xmlns:ios="clr-namespace:Windows.UI.Xaml.Controls;assembly=Uno.UI;targetPlatform=iOS"
             x:Class="UnoFormsApp.MainPage">

    <StackLayout Margin="50">
        <!-- Place new controls here -->
        <Label Text="Xamarin.Forms Label"  />
        <ios:TextBlock Text="Uno Platform TextBlock" />
    </StackLayout>

</ContentPage>
```

## Add Uno Views from C# code

From the code-behind, it's possible to use a ContentView control to host the Uno Platform controls:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:UnoFormsApp"
             x:Class="UnoFormsApp.MainPage">

    <StackLayout Margin="50">
        <Label Text="Xamarin.Forms Label"  />
        <ContentView x:Name="myContent"/>
    </StackLayout>

</ContentPage>
```

... and the corresponding C# code:

```csharp
using Windows.UI.Xaml.Controls;
using Xamarin.Forms;
using Xamarin.Forms.Platform.iOS;

namespace UnoFormsApp
{
    public partial class MainPage : ContentPage
    {
        public MainPage()
        {
            InitializeComponent();

            // Initialize the Uno styling once
            global::Windows.UI.Xaml.GenericStyles.Initialize();

            myContent.Content = new ContentControl {
                Content = new Border {
                    BorderBrush = new Windows.UI.Xaml.Media.SolidColorBrush(Windows.UI.Colors.Gray),
                    BorderThickness = new Windows.UI.Xaml.Thickness(1),
                    Child = new Pivot {
                        Items=
                        {
                            new PivotItem
                            {
                                Header = "UWP Item 1",
                                Content = "Content 1"
                            },
                            new PivotItem
                            {
                                Header = "UWP Item 2",
                                Content = "Content 2"
                            }
                        }
                    }
                }
            }.ToView();
        }
    }
}
```

