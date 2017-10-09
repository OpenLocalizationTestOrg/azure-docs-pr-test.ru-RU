---
title: "aaaHow toouse хранилища BLOB-объектов из Xamarin | Документы Microsoft"
description: "Hello клиентская библиотека хранилища Azure для Xamarin позволяет разработчикам toocreate iOS, Android и с их собственные пользовательские интерфейсы приложений для магазина Windows. В этом учебнике показано как toocreate Xamarin toouse приложение, использующее хранилище больших двоичных объектов Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="5abae-104">Как toouse хранилища BLOB-объектов из Xamarin</span><span class="sxs-lookup"><span data-stu-id="5abae-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="5abae-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="5abae-105">Overview</span></span>
<span data-ttu-id="5abae-106">Xamarin позволяет разработчикам toouse общего C# codebase toocreate iOS, Android и с их собственные пользовательские интерфейсы приложений для магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="5abae-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="5abae-107">В этом учебнике показано как toouse хранилища больших двоичных объектов Azure с помощью приложения Xamarin.</span><span class="sxs-lookup"><span data-stu-id="5abae-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="5abae-108">Если вы хотите toolearn Дополнительные сведения о хранилище Azure, прежде чем углубляться в код hello, см. раздел [tooMicrosoft введение хранилища Azure](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5abae-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="5abae-109">Создание нового приложения Xamarin</span><span class="sxs-lookup"><span data-stu-id="5abae-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="5abae-110">В этом учебнике мы создадим приложение, нацеленное на Android, iOS и Windows.</span><span class="sxs-lookup"><span data-stu-id="5abae-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="5abae-111">Это приложение просто создаст контейнер и передаст в него большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="5abae-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="5abae-112">Мы будем использовать Visual Studio на Windows, но hello же полученных данных, которые могут быть применены при создании приложения с помощью Xamarin Studio на macOS.</span><span class="sxs-lookup"><span data-stu-id="5abae-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="5abae-113">Выполните эти шаги toocreate приложения.</span><span class="sxs-lookup"><span data-stu-id="5abae-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="5abae-114">Если вы еще не сделали этого, скачайте и установите [Xamarin для Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="5abae-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="5abae-115">Откройте Visual Studio и создайте пустое приложение (Native Portable): **Файл > Создать > Проект > Кроссплатформенный > Пустое приложение (Native Portable)**.</span><span class="sxs-lookup"><span data-stu-id="5abae-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="5abae-116">Щелкните правой кнопкой мыши решение в hello на панели обозревателя решений и выберите **управление пакетами NuGet для решения**.</span><span class="sxs-lookup"><span data-stu-id="5abae-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="5abae-117">Поиск **WindowsAzure.Storage** и установка hello последняя стабильная версия tooall проектов в решении.</span><span class="sxs-lookup"><span data-stu-id="5abae-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="5abae-118">Выполните сборку проекта и запустите его.</span><span class="sxs-lookup"><span data-stu-id="5abae-118">Build and run your project.</span></span>

<span data-ttu-id="5abae-119">Вы добавили приложения, которое позволяет вам tooclick кнопку, которая увеличивает значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="5abae-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="5abae-120">Создание контейнера и передача большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="5abae-120">Create container and upload blob</span></span>
<span data-ttu-id="5abae-121">Затем в разделе вашей `(Portable)` проекта, вы добавите код слишком`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="5abae-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="5abae-122">Этот код создает контейнер и передает в него большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="5abae-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="5abae-123">`MyClass.cs`должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5abae-123">`MyClass.cs` should look like hello following:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="5abae-124">Убедитесь, что tooreplace «your_account_name_here» и «your_account_key_here» с именем фактической учетной записи и ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5abae-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="5abae-125">На iOS, Android и Windows Phone всех проектов имеют ссылки tooyour переносимого проекта - это означает, что можно написать весь общий код в одном поместите и используйте его для всех проектов.</span><span class="sxs-lookup"><span data-stu-id="5abae-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="5abae-126">Теперь можно добавить hello, следующей строкой кода tooeach проекта toostart преимуществ:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="5abae-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="5abae-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="5abae-127">XamarinApp.Droid > MainActivity.cs</span></span>

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="5abae-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="5abae-128">XamarinApp.iOS > ViewController.cs</span></span>

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="5abae-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="5abae-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="5abae-130">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="5abae-130">Run hello application</span></span>
<span data-ttu-id="5abae-131">Теперь можно запустить это приложение в эмуляторе Android или Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="5abae-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="5abae-132">Можно также запустить это приложение в эмуляторе iOS, но для этого потребуется Mac.</span><span class="sxs-lookup"><span data-stu-id="5abae-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="5abae-133">Для получения инструкций по как toodo, прочитайте hello документации [подключение Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="5abae-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="5abae-134">После запуска приложения, он создаст контейнер hello `mycontainer` вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="5abae-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="5abae-135">Она должна содержать hello blob `myblob`, имеющий текста hello `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="5abae-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="5abae-136">Это можно проверить с помощью hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5abae-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5abae-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5abae-137">Next steps</span></span>
<span data-ttu-id="5abae-138">В этом учебнике вы узнали, как toocreate кросс платформенных приложений в Xamarin, использует хранилище Azure, в частности сосредоточиться на одном сценарии в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5abae-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="5abae-139">Но его можно использовать не только для работы с хранилищем BLOB-объектов, но также с хранилищами таблиц, файлов и очередей.</span><span class="sxs-lookup"><span data-stu-id="5abae-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="5abae-140">Проверьте out hello следующие дополнительные toolearn статьи:</span><span class="sxs-lookup"><span data-stu-id="5abae-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="5abae-141">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="5abae-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="5abae-142">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="5abae-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="5abae-143">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="5abae-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="5abae-144">Приступая к работе с хранилищем файлов Azure в Windows</span><span class="sxs-lookup"><span data-stu-id="5abae-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

