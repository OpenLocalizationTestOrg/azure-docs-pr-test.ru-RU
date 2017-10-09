---
title: "aaaHow toouse хранилища больших двоичных объектов Azure с iOS | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: ios
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: df188021-86fc-4d31-a810-1b0e7bcd814b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: objective-c
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 474c4263a4bfbd61bfa39e4fdb01ddd9c3829c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a><span data-ttu-id="fea94-103">Как toouse хранилища BLOB-объектов из операций ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="fea94-103">How toouse Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="fea94-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fea94-104">Overview</span></span>
<span data-ttu-id="fea94-105">В этой статье будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fea94-105">This article will show you how tooperform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="fea94-106">Hello примеры написаны на Objective-C и использовать hello [клиентская библиотека хранилища Azure для операций ввода-вывода](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="fea94-106">hello samples are written in Objective-C and use hello [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="fea94-107">Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-107">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="fea94-108">Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="fea94-108">For more information on blobs, see hello [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="fea94-109">Можно также загрузить hello [пример приложения](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly разделе hello использование хранилища Azure в приложении iOS.</span><span class="sxs-lookup"><span data-stu-id="fea94-109">You can also download hello [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly see hello use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="fea94-110">Импортировать приложение библиотеки iOS hello хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fea94-110">Import hello Azure Storage iOS library into your application</span></span>
<span data-ttu-id="fea94-111">Вы можете импортировать библиотеки iOS hello хранилища Azure в приложение с помощью hello [CocoaPod хранилища Azure](https://cocoapods.org/pods/AZSClient) или путем импорта hello **Framework** файла.</span><span class="sxs-lookup"><span data-stu-id="fea94-111">You can import hello Azure Storage iOS library into your application either by using hello [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing hello **Framework** file.</span></span> <span data-ttu-id="fea94-112">CocoaPod — hello, рекомендуется способом, так как он упрощает интеграции библиотеки hello, однако импорт из файла framework hello меньше вмешивается в существующем проекте.</span><span class="sxs-lookup"><span data-stu-id="fea94-112">CocoaPod is hello recommended way as it makes integrating hello library easier, however importing from hello framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="fea94-113">toouse эту библиотеку необходимо hello следующие:</span><span class="sxs-lookup"><span data-stu-id="fea94-113">toouse this library, you need hello following:</span></span>
- <span data-ttu-id="fea94-114">iOS 8 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="fea94-114">iOS 8+</span></span>
- <span data-ttu-id="fea94-115">XCode 7 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="fea94-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="fea94-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="fea94-116">CocoaPod</span></span>
1. <span data-ttu-id="fea94-117">Если вы еще не сделали этого, [установить CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) на компьютере, открыв окно терминала и выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="fea94-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running hello following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="fea94-118">В каталоге проекта hello (hello каталог, содержащий ваш xcodeproj-файл), создайте новый файл с именем _Podfile_(без расширения файла).</span><span class="sxs-lookup"><span data-stu-id="fea94-118">Next, in hello project directory (hello directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="fea94-119">Добавьте следующие too_Podfile_ hello и сохраните.</span><span class="sxs-lookup"><span data-stu-id="fea94-119">Add hello following too_Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="fea94-120">В окне терминала hello перейдите toohello каталог проекта и выполнения hello следующую команду</span><span class="sxs-lookup"><span data-stu-id="fea94-120">In hello terminal window, navigate toohello project directory and run hello following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="fea94-121">Если XCODEPROJ-файл открыт в Xcode, закройте его.</span><span class="sxs-lookup"><span data-stu-id="fea94-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="fea94-122">В файле проекта откройте hello только что созданный каталог проекта, который будет иметь расширение .xcworkspace hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-122">In your project directory open hello newly created project file which will have hello .xcworkspace extension.</span></span> <span data-ttu-id="fea94-123">Это файл hello, мы будем работать с для теперь на.</span><span class="sxs-lookup"><span data-stu-id="fea94-123">This is hello file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="fea94-124">FRAMEWORK</span><span class="sxs-lookup"><span data-stu-id="fea94-124">Framework</span></span>
<span data-ttu-id="fea94-125">Hello способом, который toouse hello библиотека — платформа hello toobuild вручную:</span><span class="sxs-lookup"><span data-stu-id="fea94-125">hello other way toouse hello library is toobuild hello framework manually:</span></span>

1. <span data-ttu-id="fea94-126">First, загрузки или клон hello [репозитория хранилища azure ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="fea94-126">First, download or clone hello [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="fea94-127">Перейдите в *azure-storage-ios* -> *Lib*(Библиотеки) -> *Azure Storage Client Library* (Клиентская библиотека службы хранилища Azure) и откройте файл `AZSClient.xcodeproj` в программе Xcode.</span><span class="sxs-lookup"><span data-stu-id="fea94-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="fea94-128">В hello верхней левой части Xcode изменение hello active схему из «Клиентская библиотека хранилища Azure» слишком «Framework».</span><span class="sxs-lookup"><span data-stu-id="fea94-128">At hello top-left of Xcode, change hello active scheme from "Azure Storage Client Library" too"Framework".</span></span>
4. <span data-ttu-id="fea94-129">Построение проекта hello (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="fea94-129">Build hello project (⌘+B).</span></span> <span data-ttu-id="fea94-130">На рабочем столе будет создан файл `AZSClient.framework`.</span><span class="sxs-lookup"><span data-stu-id="fea94-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="fea94-131">Затем можно импортировать файл framework hello в приложение, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="fea94-131">You can then import hello framework file into your application by doing hello following:</span></span>

1. <span data-ttu-id="fea94-132">Создайте новый проект или откройте существующий проект в Xcode.</span><span class="sxs-lookup"><span data-stu-id="fea94-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="fea94-133">Перетаскивание hello `AZSClient.framework` в навигаторе вашего проекта Xcode.</span><span class="sxs-lookup"><span data-stu-id="fea94-133">Drag and drop hello `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="fea94-134">Выберите *Copy items if needed* (Копировать элементы при необходимости), а затем щелкните *Finish* (Готово).</span><span class="sxs-lookup"><span data-stu-id="fea94-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="fea94-135">Щелкните проект в левой навигационной hello и выберите команду hello *Общие* вкладку вверху hello редактор проекта hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-135">Click on your project in hello left-hand navigation and click hello *General* tab at hello top of hello project editor.</span></span>
5. <span data-ttu-id="fea94-136">В разделе hello *связанные платформы и библиотеки* статьи, нажмите кнопку Добавить hello (+).</span><span class="sxs-lookup"><span data-stu-id="fea94-136">Under hello *Linked Frameworks and Libraries* section, click hello Add button (+).</span></span>
6. <span data-ttu-id="fea94-137">В список библиотек, предоставляемых уже hello, поиск `libxml2.2.tbd` и добавить его в проект tooyour.</span><span class="sxs-lookup"><span data-stu-id="fea94-137">In hello list of libraries already provided, search for `libxml2.2.tbd` and add it tooyour project.</span></span>

## <a name="import-hello-library"></a><span data-ttu-id="fea94-138">Импорт библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="fea94-138">Import hello Library</span></span> 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="fea94-139">При использовании Swift, может потребоваться toocreate мост заголовок и импортировать < AZSClient/AZSClient.h > существует:</span><span class="sxs-lookup"><span data-stu-id="fea94-139">If you are using Swift, you will need toocreate a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="fea94-140">Создать файл заголовка `Bridging-Header.h`и добавить hello выше инструкции import.</span><span class="sxs-lookup"><span data-stu-id="fea94-140">Create a header file `Bridging-Header.h`, and add hello above import statement.</span></span>
2. <span data-ttu-id="fea94-141">Go toohello *параметры построения* и найдите *заголовка мост Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="fea94-141">Go toohello *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="fea94-142">Дважды щелкните в поле hello *заголовка мост Objective-C* и добавьте файл заголовка tooyour hello путь:`ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="fea94-142">Double-click on hello field of *Objective-C Bridging Header* and add hello path tooyour header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="fea94-143">Сборки hello проекта (⌘ + B) tooverify, hello мост заголовок был принят Xcode.</span><span class="sxs-lookup"><span data-stu-id="fea94-143">Build hello project (⌘+B) tooverify that hello bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="fea94-144">Начните использовать hello библиотеки непосредственно в любой Swift файл, нет необходимости в инструкциях импорта.</span><span class="sxs-lookup"><span data-stu-id="fea94-144">Start using hello library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="fea94-145">Асинхронные операции</span><span class="sxs-lookup"><span data-stu-id="fea94-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="fea94-146">Все методы для выполнения запроса к службе hello это асинхронные операции.</span><span class="sxs-lookup"><span data-stu-id="fea94-146">All methods that perform a request against hello service are asynchronous operations.</span></span> <span data-ttu-id="fea94-147">В образцах кода hello вы найдете, что эти методы имеют обработчик завершения.</span><span class="sxs-lookup"><span data-stu-id="fea94-147">In hello code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="fea94-148">Код в обработчике завершения hello будет выполняться **после** hello запрос завершается.</span><span class="sxs-lookup"><span data-stu-id="fea94-148">Code inside hello completion handler will run **after** hello request is completed.</span></span> <span data-ttu-id="fea94-149">Код после запустится обработчик завершения hello **при** был выполнен запрос hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-149">Code after hello completion handler will run **while** hello request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="fea94-150">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="fea94-150">Create a container</span></span>
<span data-ttu-id="fea94-151">Каждый BLOB-объект в хранилище Azure должен располагаться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="fea94-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="fea94-152">Hello следующий пример показывает, как toocreate контейнера, вызывать *newcontainer*, в учетной записи, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="fea94-152">hello following example shows how toocreate a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="fea94-153">При выборе имени для контейнера, следует учитывать hello, упомянутых выше правила именования.</span><span class="sxs-lookup"><span data-stu-id="fea94-153">When choosing a name for your container, be mindful of hello naming rules mentioned above.</span></span>

```objc
-(void)createContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"newcontainer"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="fea94-154">Убедитесь, что все работает, просмотрев hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) и проверки того, что *newcontainer* в hello список контейнеров для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="fea94-154">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in hello list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="fea94-155">Назначение разрешений контейнера</span><span class="sxs-lookup"><span data-stu-id="fea94-155">Set Container Permissions</span></span>
<span data-ttu-id="fea94-156">Разрешения контейнера, настраиваемые по умолчанию, — это разрешения на **закрытый** доступ.</span><span class="sxs-lookup"><span data-stu-id="fea94-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="fea94-157">При этом контейнеры предоставляют и другие возможности доступа.</span><span class="sxs-lookup"><span data-stu-id="fea94-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="fea94-158">**Закрытый**: hello только владельцем учетной записи могут считываться данные контейнера и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-158">**Private**: Container and blob data can be read by hello account owner only.</span></span>
* <span data-ttu-id="fea94-159">**BLOB-объект**: хотя данные BLOB-объекта, содержащиеся в контейнере, могут быть прочитаны через анонимный запрос, данные самого контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="fea94-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="fea94-160">Клиенты не могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос.</span><span class="sxs-lookup"><span data-stu-id="fea94-160">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="fea94-161">**Контейнер**: данные контейнера и BLOB-объекта могут быть прочитаны через анонимный запрос.</span><span class="sxs-lookup"><span data-stu-id="fea94-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="fea94-162">Клиенты могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-162">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="fea94-163">Hello следующий пример показывает, как toocreate в контейнер с **контейнера** доступ к разрешений, которые будет разрешать доступ открытым и доступным только для чтения для всех пользователей на hello Интернет:</span><span class="sxs-lookup"><span data-stu-id="fea94-163">hello following example shows you how toocreate a container with **Container** access permissions, which will allow public, read-only access for all users on hello Internet:</span></span>

```objc
-(void)createContainerWithPublicAccess{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create container in your Storage account if hello container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="fea94-164">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="fea94-164">Upload a blob into a container</span></span>
<span data-ttu-id="fea94-165">Как упоминалось в hello [больших двоичных объектов основные понятия службы](#blob-service-concepts) раздел, хранилище BLOB-объектов предлагает три различных типа больших двоичных объектов: блочные большие двоичные объекты, добавлять большие двоичные объекты и страничные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="fea94-165">As mentioned in hello [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="fea94-166">библиотеки iOS Hello хранилища Azure поддерживает все три типа больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-166">hello Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="fea94-167">В большинстве случаев блочного BLOB-объекта — hello, рекомендуется toouse типа.</span><span class="sxs-lookup"><span data-stu-id="fea94-167">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="fea94-168">Hello в следующем примере показано, как tooupload блок больших двоичных объектов из NSString.</span><span class="sxs-lookup"><span data-stu-id="fea94-168">hello following example shows how tooupload a block blob from an NSString.</span></span> <span data-ttu-id="fea94-169">Если большой двоичный объект с таким же именем уже существует в этом контейнере hello hello содержимое этого большого двоичного объекта будет перезаписано.</span><span class="sxs-lookup"><span data-stu-id="fea94-169">If a blob with hello same name already exists in this container, hello contents of this blob will be overwritten.</span></span>

```objc
-(void)uploadBlobToContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists)
        {
            if (error){
                NSLog(@"Error in creating container.");
            }
            else{
                // Create a local blob object
                AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

                // Upload blob tooStorage
                [blockBlob uploadFromText:@"This text will be uploaded tooBlob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="fea94-170">Убедитесь, что все работает, просмотрев hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) и проверке этого контейнера hello *containerpublic*, содержит большой двоичный объект hello, *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="fea94-170">You can confirm that this works by looking at hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that hello container, *containerpublic*, contains hello blob, *sampleblob*.</span></span> <span data-ttu-id="fea94-171">В этом примере мы использовали открытого контейнера, вы можете убедиться, что это приложение работает с переходом toohello большие двоичные объекты URI:</span><span class="sxs-lookup"><span data-stu-id="fea94-171">In this sample, we used a public container so you can also verify that this application worked by going toohello blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="fea94-172">В дополнение к этому toouploading большой двоичный объект блока из NSString существуют аналогичные методы NSData, NSInputStream или локальный файл.</span><span class="sxs-lookup"><span data-stu-id="fea94-172">In addition toouploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="fea94-173">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="fea94-173">List hello blobs in a container</span></span>
<span data-ttu-id="fea94-174">Hello следующем примере показано, как toolist все большие двоичные объекты в контейнере.</span><span class="sxs-lookup"><span data-stu-id="fea94-174">hello following example shows how toolist all blobs in a container.</span></span> <span data-ttu-id="fea94-175">При выполнении этой операции, следует учитывать hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="fea94-175">When performing this operation, be mindful of hello following parameters:</span></span>     

* <span data-ttu-id="fea94-176">**continuationToken** -hello представляет токен продолжения, начала операции перечисления hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-176">**continuationToken** - hello continuation token represents where hello listing operation should start.</span></span> <span data-ttu-id="fea94-177">Если токен не предоставлен, он будет перечисление больших двоичных объектов с начала hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-177">If no token is provided, it will list blobs from hello beginning.</span></span> <span data-ttu-id="fea94-178">Может быть указано любое количество больших двоичных объектов от нуля вверх tooa максимального.</span><span class="sxs-lookup"><span data-stu-id="fea94-178">Any number of blobs can be listed, from zero up tooa set maximum.</span></span> <span data-ttu-id="fea94-179">Даже если этот метод возвращает нулевой результат, если `results.continuationToken` имеет родителя, возможно, имеются большие двоичные объекты в службе hello, не перечислены.</span><span class="sxs-lookup"><span data-stu-id="fea94-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on hello service that have not been listed.</span></span>
* <span data-ttu-id="fea94-180">**префикс** -можно указать toouse hello префикс для списка больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-180">**prefix** - You can specify hello prefix toouse for blob listing.</span></span> <span data-ttu-id="fea94-181">Перечислены будут только BLOB-объекты, начинающиеся с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="fea94-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="fea94-182">**useFlatBlobListing** — как упоминалось в hello [именование и ссылки на контейнеры и большие двоичные объекты](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) раздел, несмотря на то, что hello службы BLOB-объектов является схеме плоского хранилища, можно создать виртуальной иерархии больших двоичных объектов с путем к именованию сведения.</span><span class="sxs-lookup"><span data-stu-id="fea94-182">**useFlatBlobListing** - As mentioned in hello [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although hello Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="fea94-183">Однако неплоское перечисление в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fea94-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="fea94-184">Эта функция станет доступной в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="fea94-184">This feature is coming soon.</span></span> <span data-ttu-id="fea94-185">Сейчас же это значение должно быть **YES** (Да).</span><span class="sxs-lookup"><span data-stu-id="fea94-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="fea94-186">**blobListingDetails** -tooinclude какие элементы можно указать при перечислении больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fea94-186">**blobListingDetails** - You can specify which items tooinclude when listing blobs</span></span>
  * <span data-ttu-id="fea94-187">_AZSBlobListingDetailsNone_: вывод списка только зафиксированных больших двоичных объектов без возвращения их метаданных.</span><span class="sxs-lookup"><span data-stu-id="fea94-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="fea94-188">_AZSBlobListingDetailsSnapshots_: вывод списка зафиксированных больших двоичных объектов и их моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="fea94-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="fea94-189">_AZSBlobListingDetailsMetadata_: получить метаданные большого двоичного объекта для каждого большого двоичного объекта возвращается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in hello listing.</span></span>
  * <span data-ttu-id="fea94-190">_AZSBlobListingDetailsUncommittedBlobs_: вывод списка зафиксированных и незафиксированных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="fea94-191">_AZSBlobListingDetailsCopy_: копировался свойства в списке hello.</span><span class="sxs-lookup"><span data-stu-id="fea94-191">_AZSBlobListingDetailsCopy_: Include copy properties in hello listing.</span></span>
  * <span data-ttu-id="fea94-192">_AZSBlobListingDetailsAll_: вывод списка всех доступных зафиксированных больших двоичных объектов, незафиксированных больших двоичных объектов и моментальных снимков, а также возвращение всех метаданных и состояния копий этих объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="fea94-193">**maxResults** -hello максимальное количество результатов tooreturn для этой операции.</span><span class="sxs-lookup"><span data-stu-id="fea94-193">**maxResults** - hello maximum number of results tooreturn for this operation.</span></span> <span data-ttu-id="fea94-194">Ограничить toonot используйте -1.</span><span class="sxs-lookup"><span data-stu-id="fea94-194">Use -1 toonot set a limit.</span></span>
* <span data-ttu-id="fea94-195">**completionHandler** -hello блок кода tooexecute результатами "hello" hello операции перечисления.</span><span class="sxs-lookup"><span data-stu-id="fea94-195">**completionHandler** - hello block of code tooexecute with hello results of hello listing operation.</span></span>

<span data-ttu-id="fea94-196">В этом примере вспомогательный метод способ используется toorecursively вызов hello список больших двоичных объектов каждый раз, возвращается токен продолжения.</span><span class="sxs-lookup"><span data-stu-id="fea94-196">In this example, a helper method is used toorecursively call hello list blobs method every time a continuation token is returned.</span></span>

```objc
-(void)listBlobsInContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    //List all blobs in container
    [self listBlobsInContainerHelper:blobContainer continuationToken:nil prefix:nil blobListingDetails:AZSBlobListingDetailsAll maxResults:-1 completionHandler:^(NSError *error) {
        if (error != nil){
            NSLog(@"Error in creating container.");
        }
    }];
}

//List blobs helper method
-(void)listBlobsInContainerHelper:(AZSCloudBlobContainer *)container continuationToken:(AZSContinuationToken *)continuationToken prefix:(NSString *)prefix blobListingDetails:(AZSBlobListingDetails)blobListingDetails maxResults:(NSUInteger)maxResults completionHandler:(void (^)(NSError *))completionHandler
{
    [container listBlobsSegmentedWithContinuationToken:continuationToken prefix:prefix useFlatBlobListing:YES blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:^(NSError *error, AZSBlobResultSegment *results) {
        if (error)
        {
            completionHandler(error);
        }
        else
        {
            for (int i = 0; i < results.blobs.count; i++) {
                NSLog(@"%@",[(AZSCloudBlockBlob *)results.blobs[i] blobName]);
            }
            if (results.continuationToken)
            {
                [self listBlobsInContainerHelper:container continuationToken:results.continuationToken prefix:prefix blobListingDetails:blobListingDetails maxResults:maxResults completionHandler:completionHandler];
            }
            else
            {
                completionHandler(nil);
            }
        }
    }];
}
```

## <a name="download-a-blob"></a><span data-ttu-id="fea94-197">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="fea94-197">Download a blob</span></span>
<span data-ttu-id="fea94-198">Следующий пример показывает как Hello toodownload объект NSString tooa больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fea94-198">hello following example shows how toodownload a blob tooa NSString object.</span></span>

```objc
-(void)downloadBlobToString{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob"];

    // Download blob
    [blockBlob downloadToTextWithCompletionHandler:^(NSError *error, NSString *text) {
        if (error) {
            NSLog(@"Error in downloading blob");
        }
        else{
            NSLog(@"%@",text);
        }
    }];
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="fea94-199">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="fea94-199">Delete a blob</span></span>
<span data-ttu-id="fea94-200">Следующий пример показывает как Hello toodelete большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="fea94-200">hello following example shows how toodelete a blob.</span></span>

```objc
-(void)deleteBlob{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Create a local blob object
    AZSCloudBlockBlob *blockBlob = [blobContainer blockBlobReferenceFromName:@"sampleblob1"];

    // Delete blob
    [blockBlob deleteWithCompletionHandler:^(NSError *error) {
        if (error) {
            NSLog(@"Error in deleting blob.");
        }
    }];
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="fea94-201">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="fea94-201">Delete a blob container</span></span>
<span data-ttu-id="fea94-202">Следующий пример показывает как Hello toodelete контейнера.</span><span class="sxs-lookup"><span data-stu-id="fea94-202">hello following example shows how toodelete a container.</span></span>

```objc
-(void)deleteContainer{
    NSError *accountCreationError;

    // Create a storage account object from a connection string.
    AZSCloudStorageAccount *account = [AZSCloudStorageAccount accountFromConnectionString:@"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here" error:&accountCreationError];

    if(accountCreationError){
        NSLog(@"Error in creating account.");
    }

    // Create a blob service client object.
    AZSCloudBlobClient *blobClient = [account getBlobClient];

    // Create a local container object.
    AZSCloudBlobContainer *blobContainer = [blobClient containerReferenceFromName:@"containerpublic"];

    // Delete container
    [blobContainer deleteContainerIfExistsWithCompletionHandler:^(NSError *error, BOOL success) {
        if(error){
            NSLog(@"Error in deleting container");
        }
    }];
}
```

## <a name="next-steps"></a><span data-ttu-id="fea94-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fea94-203">Next steps</span></span>
<span data-ttu-id="fea94-204">Теперь, когда вы узнали, как toouse хранилища BLOB-объектов из iOS, выполните следующие дополнительные сведения о библиотеке iOS hello toolearn ссылки и hello службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="fea94-204">Now that you've learned how toouse Blob Storage from iOS, follow these links toolearn more about hello iOS library and hello Storage service.</span></span>

* [<span data-ttu-id="fea94-205">Клиентская библиотека хранилища Azure для iOS</span><span class="sxs-lookup"><span data-stu-id="fea94-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="fea94-206">Справочная документация по использованию службы хранилища Azure в iOS</span><span class="sxs-lookup"><span data-stu-id="fea94-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="fea94-207">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fea94-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="fea94-208">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fea94-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="fea94-209">При наличии вопросов относительно этой библиотеки чувствовать себя свободного toopost tooour [форум MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) или [переполнения стека](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="fea94-209">If you have questions regarding this library, feel free toopost tooour [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="fea94-210">Если у вас есть предложения компонентов для службы хранилища Azure, опубликуйте слишком[отзывы хранилища Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="fea94-210">If you have feature suggestions for Azure Storage, please post too[Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

