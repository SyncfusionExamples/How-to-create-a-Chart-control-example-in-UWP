# Getting Started with UWP Sparkline (SfSparkline)

This sample demonstrates how to create a UWP Sparkline chart using the Syncfusion `SfLineSparkline` control.

## Prerequisites

- Visual Studio 2019 or later
- Windows 10 SDK (10.0.17763.0 or later)
- [Syncfusion.SfChart.UWP](https://www.nuget.org/packages/Syncfusion.SfChart.UWP) NuGet package (latest)

## Adding Assembly Reference

### Option 1: Via NuGet Package Manager

1. Right-click on the project in **Solution Explorer** and select **Manage NuGet Packages**.
2. Search for `Syncfusion.SfChart.UWP` and install it.

### Option 2: Via Extension Reference

1. Open the **Add Reference** window from your project.
2. Choose **Windows > Extensions > Syncfusion Controls for UWP XAML**.

## Adding Namespace

After adding the reference, include the following namespace in your `MainPage.xaml`:

```xml
xmlns:syncfusion="using:Syncfusion.UI.Xaml.Charts"
```

## Creating the Data Model

Create a `UserProfile` model class (`ViewModel/Model.cs`) to hold the data:

```csharp
using System;

namespace GettingStarted
{
    public class UserProfile
    {
        public DateTime TimeStamp { get; set; }
        public double NoOfUsers { get; set; }
    }
}
```

## Creating the ViewModel

Create a `UsersViewModel` class (`ViewModel/ViewModel.cs`) with sample data:

```csharp
using System;
using System.Collections.ObjectModel;

namespace GettingStarted
{
    public class UsersViewModel
    {
        public UsersViewModel()
        {
            this.UsersList = new ObservableCollection<UserProfile>();
            DateTime date = DateTime.Today;
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = 3000 });
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = 5000 });
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = -3000 });
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = -4000 });
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = 2000 });
            UsersList.Add(new UserProfile { TimeStamp = date.AddHours(0.5), NoOfUsers = 3000 });
        }

        public ObservableCollection<UserProfile> UsersList { get; set; }
    }
}
```

## Initializing the Sparkline (XAML)

In `MainPage.xaml`, set the `DataContext` to `UsersViewModel`, then initialize `SfLineSparkline` by binding `ItemsSource` to the data collection and setting `YBindingPath` to the data property:

```xml
<Page
    x:Class="GettingStarted.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:GettingStarted"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:syncfusion="using:Syncfusion.UI.Xaml.Charts"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <Grid.DataContext>
            <local:UsersViewModel/>
        </Grid.DataContext>

        <syncfusion:SfLineSparkline Interior="#4a4a4a"
                                    BorderThickness="1"
                                    ItemsSource="{Binding UsersList}"
                                    BorderBrush="DarkGray"
                                    YBindingPath="NoOfUsers">
        </syncfusion:SfLineSparkline>
    </Grid>
</Page>
```

## Initializing the Sparkline (Code-Behind)

Alternatively, you can create the sparkline entirely in C# code-behind:

```csharp
using Syncfusion.UI.Xaml.Charts;
using Windows.UI;
using Windows.UI.Xaml.Media;

// Creating the ViewModel
UsersViewModel viewModel = new UsersViewModel();

// Assigning the data context
this.DataContext = viewModel;

// Initializing the sparkline
SfLineSparkline sfLineSparkline = new SfLineSparkline();

// Setting ItemsSource and YBindingPath
sfLineSparkline.ItemsSource = viewModel.UsersList;
sfLineSparkline.YBindingPath = "NoOfUsers";

// Customizing appearance
sfLineSparkline.Interior = new SolidColorBrush(Color.FromArgb(255, 74, 74, 74));
sfLineSparkline.BorderBrush = new SolidColorBrush(Colors.DarkGray);
sfLineSparkline.BorderThickness = new Thickness(1);

// Adding sparkline to the Grid
grid.Children.Add(sfLineSparkline);
```

![Getting started with uwp chart](gettingstarted.png)

## Reference

- [Syncfusion UWP Sparkline Getting Started Documentation](https://help.syncfusion.com/uwp/sparkline/getting-started)