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
# <a name="how-toouse-blob-storage-from-xamarin"></a>Как toouse хранилища BLOB-объектов из Xamarin
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Обзор
Xamarin позволяет разработчикам toouse общего C# codebase toocreate iOS, Android и с их собственные пользовательские интерфейсы приложений для магазина Windows. В этом учебнике показано как toouse хранилища больших двоичных объектов Azure с помощью приложения Xamarin. Если вы хотите toolearn Дополнительные сведения о хранилище Azure, прежде чем углубляться в код hello, см. раздел [tooMicrosoft введение хранилища Azure](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Создание нового приложения Xamarin
В этом учебнике мы создадим приложение, нацеленное на Android, iOS и Windows. Это приложение просто создаст контейнер и передаст в него большой двоичный объект. Мы будем использовать Visual Studio на Windows, но hello же полученных данных, которые могут быть применены при создании приложения с помощью Xamarin Studio на macOS.

Выполните эти шаги toocreate приложения.

1. Если вы еще не сделали этого, скачайте и установите [Xamarin для Visual Studio](https://www.xamarin.com/download).
2. Откройте Visual Studio и создайте пустое приложение (Native Portable): **Файл > Создать > Проект > Кроссплатформенный > Пустое приложение (Native Portable)**.
3. Щелкните правой кнопкой мыши решение в hello на панели обозревателя решений и выберите **управление пакетами NuGet для решения**. Поиск **WindowsAzure.Storage** и установка hello последняя стабильная версия tooall проектов в решении.
4. Выполните сборку проекта и запустите его.

Вы добавили приложения, которое позволяет вам tooclick кнопку, которая увеличивает значение счетчика.

## <a name="create-container-and-upload-blob"></a>Создание контейнера и передача большого двоичного объекта
Затем в разделе вашей `(Portable)` проекта, вы добавите код слишком`MyClass.cs`. Этот код создает контейнер и передает в него большой двоичный объект. `MyClass.cs`должен выглядеть hello следующим образом:

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

Убедитесь, что tooreplace «your_account_name_here» и «your_account_key_here» с именем фактической учетной записи и ключ учетной записи. 

На iOS, Android и Windows Phone всех проектов имеют ссылки tooyour переносимого проекта - это означает, что можно написать весь общий код в одном поместите и используйте его для всех проектов. Теперь можно добавить hello, следующей строкой кода tooeach проекта toostart преимуществ:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

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

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

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

## <a name="run-hello-application"></a>Запустите приложение hello
Теперь можно запустить это приложение в эмуляторе Android или Windows Phone. Можно также запустить это приложение в эмуляторе iOS, но для этого потребуется Mac. Для получения инструкций по как toodo, прочитайте hello документации [подключение Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

После запуска приложения, он создаст контейнер hello `mycontainer` вашей учетной записи хранилища. Она должна содержать hello blob `myblob`, имеющий текста hello `Hello, world!`. Это можно проверить с помощью hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toocreate кросс платформенных приложений в Xamarin, использует хранилище Azure, в частности сосредоточиться на одном сценарии в хранилище больших двоичных объектов. Но его можно использовать не только для работы с хранилищем BLOB-объектов, но также с хранилищами таблиц, файлов и очередей. Проверьте out hello следующие дополнительные toolearn статьи:

* [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md)
* [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Приступая к работе с хранилищем очередей Azure с помощью .NET](../queues/storage-dotnet-how-to-use-queues.md)
* [Приступая к работе с хранилищем файлов Azure в Windows](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

