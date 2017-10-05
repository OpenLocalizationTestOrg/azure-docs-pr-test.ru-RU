---
title: "Как использовать хранилище BLOB-объектов Azure из iOS | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: cb2810636c8c23dbd476dc2adf58b17d1887d575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-blob-storage-from-ios"></a><span data-ttu-id="d847d-103">Использование хранилища BLOB-объектов из iOS</span><span class="sxs-lookup"><span data-stu-id="d847d-103">How to use Blob storage from iOS</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d847d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d847d-104">Overview</span></span>
<span data-ttu-id="d847d-105">В этой статье показано, как реализовать типичные сценарии с использованием хранилища BLOB-объектов Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d847d-105">This article will show you how to perform common scenarios using Microsoft Azure Blob storage.</span></span> <span data-ttu-id="d847d-106">Примеры написаны на Objective-C и используют [клиентскую библиотеку службы хранилища Azure для iOS](https://github.com/Azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="d847d-106">The samples are written in Objective-C and use the [Azure Storage Client Library for iOS](https://github.com/Azure/azure-storage-ios).</span></span> <span data-ttu-id="d847d-107">Здесь описаны такие сценарии, как **отправка**, **перечисление**, **скачивание** и **удаление** BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-107">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="d847d-108">Дополнительные сведения о больших двоичных объектах см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="d847d-108">For more information on blobs, see the [Next Steps](#next-steps) section.</span></span> <span data-ttu-id="d847d-109">Кроме того, можно загрузить [пример приложения](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample), чтобы просмотреть варианты использования службы хранилища Azure в приложении iOS.</span><span class="sxs-lookup"><span data-stu-id="d847d-109">You can also download the [sample app](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) to quickly see the use of Azure Storage in an iOS application.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="import-the-azure-storage-ios-library-into-your-application"></a><span data-ttu-id="d847d-110">Импорт библиотеки хранилища Azure для iOS в приложение</span><span class="sxs-lookup"><span data-stu-id="d847d-110">Import the Azure Storage iOS library into your application</span></span>
<span data-ttu-id="d847d-111">Можно импортировать библиотеку службы хранилища Azure для iOS в приложение, воспользовавшись библиотекой [CocoaPod для службы хранилища Azure](https://cocoapods.org/pods/AZSClient) или импортировав **FRAMEWORK** -файл.</span><span class="sxs-lookup"><span data-stu-id="d847d-111">You can import the Azure Storage iOS library into your application either by using the [Azure Storage CocoaPod](https://cocoapods.org/pods/AZSClient) or by importing the **Framework** file.</span></span> <span data-ttu-id="d847d-112">Рекомендуется использовать CocoaPod, так как это средство упрощает интеграцию библиотеки. Однако импорт из файла framework является более щадящим для существующего проекта.</span><span class="sxs-lookup"><span data-stu-id="d847d-112">CocoaPod is the recommended way as it makes integrating the library easier, however importing from the framework file is less intrusive for your existing project.</span></span>

<span data-ttu-id="d847d-113">Чтобы использовать эту библиотеку, потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="d847d-113">To use this library, you need the following:</span></span>
- <span data-ttu-id="d847d-114">iOS 8 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="d847d-114">iOS 8+</span></span>
- <span data-ttu-id="d847d-115">XCode 7 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="d847d-115">Xcode 7+</span></span>

## <a name="cocoapod"></a><span data-ttu-id="d847d-116">CocoaPod</span><span class="sxs-lookup"><span data-stu-id="d847d-116">CocoaPod</span></span>
1. <span data-ttu-id="d847d-117">Если вы еще этого не сделали, [установите CocoaPod](https://guides.cocoapods.org/using/getting-started.html#toc_3) на компьютере, открыв окно терминала и выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d847d-117">If you haven't done so already, [Install CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) on your computer by opening a terminal window and running the following command</span></span>
    
    ```shell   
    sudo gem install cocoapods
    ```

2. <span data-ttu-id="d847d-118">Затем в каталоге проекта (каталог, содержащий ваш XCODEPROJ-файл), создайте новый файл _Podfile_ (без расширения файла).</span><span class="sxs-lookup"><span data-stu-id="d847d-118">Next, in the project directory (the directory containing your .xcodeproj file), create a new file called _Podfile_(no file extension).</span></span> <span data-ttu-id="d847d-119">Добавьте следующий код в файл _Podfile_ и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="d847d-119">Add the following to _Podfile_ and save.</span></span>

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. <span data-ttu-id="d847d-120">В окне терминала перейдите в каталог проекта и выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="d847d-120">In the terminal window, navigate to the project directory and run the following command</span></span>

    ```shell    
    pod install
    ```

4. <span data-ttu-id="d847d-121">Если XCODEPROJ-файл открыт в Xcode, закройте его.</span><span class="sxs-lookup"><span data-stu-id="d847d-121">If your .xcodeproj is open in Xcode, close it.</span></span> <span data-ttu-id="d847d-122">В каталоге проекта откройте только что созданный файл проекта, который будет иметь расширение .xcworkspace.</span><span class="sxs-lookup"><span data-stu-id="d847d-122">In your project directory open the newly created project file which will have the .xcworkspace extension.</span></span> <span data-ttu-id="d847d-123">Это файл, с которым вы теперь будете работать.</span><span class="sxs-lookup"><span data-stu-id="d847d-123">This is the file you'll work from for now on.</span></span>

## <a name="framework"></a><span data-ttu-id="d847d-124">FRAMEWORK</span><span class="sxs-lookup"><span data-stu-id="d847d-124">Framework</span></span>
<span data-ttu-id="d847d-125">Другой способ использования библиотеки заключается в создании файла framework вручную.</span><span class="sxs-lookup"><span data-stu-id="d847d-125">The other way to use the library is to build the framework manually:</span></span>

1. <span data-ttu-id="d847d-126">Прежде всего загрузите или клонируйте [репозиторий azure-storage-ios](https://github.com/azure/azure-storage-ios).</span><span class="sxs-lookup"><span data-stu-id="d847d-126">First, download or clone the [azure-storage-ios repo](https://github.com/azure/azure-storage-ios).</span></span>
2. <span data-ttu-id="d847d-127">Перейдите в *azure-storage-ios* -> *Lib*(Библиотеки) -> *Azure Storage Client Library* (Клиентская библиотека службы хранилища Azure) и откройте файл `AZSClient.xcodeproj` в программе Xcode.</span><span class="sxs-lookup"><span data-stu-id="d847d-127">Go into *azure-storage-ios* -> *Lib* -> *Azure Storage Client Library*, and open `AZSClient.xcodeproj` in Xcode.</span></span>
3. <span data-ttu-id="d847d-128">В левой верхней части окна Xcode измените активную схему с Azure Storage Client Library (Клиентская библиотека хранилища Azure) на Framework (Платформа).</span><span class="sxs-lookup"><span data-stu-id="d847d-128">At the top-left of Xcode, change the active scheme from "Azure Storage Client Library" to "Framework".</span></span>
4. <span data-ttu-id="d847d-129">Выполните сборку проекта (⌘ + B).</span><span class="sxs-lookup"><span data-stu-id="d847d-129">Build the project (⌘+B).</span></span> <span data-ttu-id="d847d-130">На рабочем столе будет создан файл `AZSClient.framework`.</span><span class="sxs-lookup"><span data-stu-id="d847d-130">This will create an `AZSClient.framework` file on your Desktop.</span></span>

<span data-ttu-id="d847d-131">После этого можно импортировать файл платформы в приложение следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d847d-131">You can then import the framework file into your application by doing the following:</span></span>

1. <span data-ttu-id="d847d-132">Создайте новый проект или откройте существующий проект в Xcode.</span><span class="sxs-lookup"><span data-stu-id="d847d-132">Create a new project or open up your existing project in Xcode.</span></span>
2. <span data-ttu-id="d847d-133">Перетащите `AZSClient.framework` в навигатор проекта Xcode.</span><span class="sxs-lookup"><span data-stu-id="d847d-133">Drag and drop the `AZSClient.framework` into your Xcode project navigator.</span></span>
3. <span data-ttu-id="d847d-134">Выберите *Copy items if needed* (Копировать элементы при необходимости), а затем щелкните *Finish* (Готово).</span><span class="sxs-lookup"><span data-stu-id="d847d-134">Select *Copy items if needed*, and click on *Finish*.</span></span>
4. <span data-ttu-id="d847d-135">Щелкните проект на левой панели навигации и перейдите на вкладку *General* (Общие) в верхней части редактора проекта.</span><span class="sxs-lookup"><span data-stu-id="d847d-135">Click on your project in the left-hand navigation and click the *General* tab at the top of the project editor.</span></span>
5. <span data-ttu-id="d847d-136">В разделе *Linked Frameworks and Libraries* (Связанные платформы и библиотеки) нажмите кнопку добавления (+).</span><span class="sxs-lookup"><span data-stu-id="d847d-136">Under the *Linked Frameworks and Libraries* section, click the Add button (+).</span></span>
6. <span data-ttu-id="d847d-137">В списке уже предоставленных библиотек найдите библиотеку `libxml2.2.tbd` и добавьте ее в проект.</span><span class="sxs-lookup"><span data-stu-id="d847d-137">In the list of libraries already provided, search for `libxml2.2.tbd` and add it to your project.</span></span>

## <a name="import-the-library"></a><span data-ttu-id="d847d-138">Импорт библиотеки</span><span class="sxs-lookup"><span data-stu-id="d847d-138">Import the Library</span></span> 
```objc
// Include the following import statement to use blob APIs.
#import <AZSClient/AZSClient.h>
```

<span data-ttu-id="d847d-139">Если вы используете Swift, потребуется создать промежуточный заголовок и импортировать <AZSClient/AZSClient.h>:</span><span class="sxs-lookup"><span data-stu-id="d847d-139">If you are using Swift, you will need to create a bridging header and import <AZSClient/AZSClient.h> there:</span></span>

1. <span data-ttu-id="d847d-140">Создайте файл заголовка `Bridging-Header.h` и добавьте приведенный выше оператор импорта.</span><span class="sxs-lookup"><span data-stu-id="d847d-140">Create a header file `Bridging-Header.h`, and add the above import statement.</span></span>
2. <span data-ttu-id="d847d-141">Откройте вкладку *Параметры сборки* и найдите *Заголовок Objective-C*.</span><span class="sxs-lookup"><span data-stu-id="d847d-141">Go to the *Build Settings* tab, and search for *Objective-C Bridging Header*.</span></span>
3. <span data-ttu-id="d847d-142">Дважды щелкните поле *Заголовок Objective-C* и добавьте путь к файлу заголовка: `ProjectName/Bridging-Header.h`</span><span class="sxs-lookup"><span data-stu-id="d847d-142">Double-click on the field of *Objective-C Bridging Header* and add the path to your header file: `ProjectName/Bridging-Header.h`</span></span>
4. <span data-ttu-id="d847d-143">Выполните сборку проекта (⌘ + B), чтобы убедиться, что заголовок выбран в Xcode.</span><span class="sxs-lookup"><span data-stu-id="d847d-143">Build the project (⌘+B) to verify that the bridging header was picked up by Xcode.</span></span>
5. <span data-ttu-id="d847d-144">Начните использовать библиотеку непосредственно в любом файле Swift. Операторы импорта не требуются.</span><span class="sxs-lookup"><span data-stu-id="d847d-144">Start using the library directly in any Swift file, there is no need for import statements.</span></span>

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a><span data-ttu-id="d847d-145">Асинхронные операции</span><span class="sxs-lookup"><span data-stu-id="d847d-145">Asynchronous Operations</span></span>
> [!NOTE]
> <span data-ttu-id="d847d-146">Все методы, которые выполняют запрос к службе, являются асинхронными операциями.</span><span class="sxs-lookup"><span data-stu-id="d847d-146">All methods that perform a request against the service are asynchronous operations.</span></span> <span data-ttu-id="d847d-147">Из примеров кода понятно, что у этих методов есть завершающий обработчик.</span><span class="sxs-lookup"><span data-stu-id="d847d-147">In the code samples, you'll find that these methods have a completion handler.</span></span> <span data-ttu-id="d847d-148">Код внутри обработчика завершения выполняется **после** завершения запроса.</span><span class="sxs-lookup"><span data-stu-id="d847d-148">Code inside the completion handler will run **after** the request is completed.</span></span> <span data-ttu-id="d847d-149">Код за пределами обработчика завершения (следующий за ним) выполняется **во время** выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="d847d-149">Code after the completion handler will run **while** the request is being made.</span></span>
> 
> 

## <a name="create-a-container"></a><span data-ttu-id="d847d-150">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="d847d-150">Create a container</span></span>
<span data-ttu-id="d847d-151">Каждый BLOB-объект в хранилище Azure должен располагаться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="d847d-151">Every blob in Azure Storage must reside in a container.</span></span> <span data-ttu-id="d847d-152">В следующем примере показано, как в учетной записи хранения создать контейнер с именем *newcontainer*(если такового еще нет).</span><span class="sxs-lookup"><span data-stu-id="d847d-152">The following example shows how to create a container, called *newcontainer*, in your Storage account if it doesn't already exist.</span></span> <span data-ttu-id="d847d-153">При выборе имени для контейнера следует учитывать правила именования, упомянутые выше.</span><span class="sxs-lookup"><span data-stu-id="d847d-153">When choosing a name for your container, be mindful of the naming rules mentioned above.</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithCompletionHandler:^(NSError *error, BOOL exists) {
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

<span data-ttu-id="d847d-154">Убедиться, что все работает, можно в [обозревателе хранилищ Microsoft Azure](http://storageexplorer.com). Следует проверить, находится ли *newcontainer* в списке контейнеров вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d847d-154">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that *newcontainer* is in the list of containers for your Storage account.</span></span>

## <a name="set-container-permissions"></a><span data-ttu-id="d847d-155">Назначение разрешений контейнера</span><span class="sxs-lookup"><span data-stu-id="d847d-155">Set Container Permissions</span></span>
<span data-ttu-id="d847d-156">Разрешения контейнера, настраиваемые по умолчанию, — это разрешения на **закрытый** доступ.</span><span class="sxs-lookup"><span data-stu-id="d847d-156">A container's permissions are configured for **Private** access by default.</span></span> <span data-ttu-id="d847d-157">При этом контейнеры предоставляют и другие возможности доступа.</span><span class="sxs-lookup"><span data-stu-id="d847d-157">However, containers provide a few different options for container access:</span></span>

* <span data-ttu-id="d847d-158">**Закрытый**: данные контейнера и BLOB-объекта могут быть прочитаны только владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d847d-158">**Private**: Container and blob data can be read by the account owner only.</span></span>
* <span data-ttu-id="d847d-159">**BLOB-объект**: хотя данные BLOB-объекта, содержащиеся в контейнере, могут быть прочитаны через анонимный запрос, данные самого контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="d847d-159">**Blob**: Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="d847d-160">Клиенты не могут перечислять BLOB-объекты внутри с помощью анонимного запроса.</span><span class="sxs-lookup"><span data-stu-id="d847d-160">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="d847d-161">**Контейнер**: данные контейнера и BLOB-объекта могут быть прочитаны через анонимный запрос.</span><span class="sxs-lookup"><span data-stu-id="d847d-161">**Container**: Container and blob data can be read via anonymous request.</span></span> <span data-ttu-id="d847d-162">Клиенты могут перечислять BLOB-объекты внутри контейнера с помощью анонимного запроса, но не могут перечислять контейнеры в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d847d-162">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="d847d-163">В следующем примере показано, как создать контейнер с разрешениями на доступ к **контейнеру**, предоставляющими открытый доступ только на чтение всем пользователям Интернета:</span><span class="sxs-lookup"><span data-stu-id="d847d-163">The following example shows you how to create a container with **Container** access permissions, which will allow public, read-only access for all users on the Internet:</span></span>

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

    // Create container in your Storage account if the container doesn't already exist
    [blobContainer createContainerIfNotExistsWithAccessType:AZSContainerPublicAccessTypeContainer requestOptions:nil operationContext:nil completionHandler:^(NSError *error, BOOL exists){
        if (error){
            NSLog(@"Error in creating container.");
        }
    }];
}
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d847d-164">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="d847d-164">Upload a blob into a container</span></span>
<span data-ttu-id="d847d-165">Как упоминалось в разделе [Основные понятия службы BLOB-объектов](#blob-service-concepts) , хранилище BLOB-объектов может содержать три разных типа BLOB-объектов: блочные BLOB-объекты, BLOB-объекты добавления и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="d847d-165">As mentioned in the [Blob service concepts](#blob-service-concepts) section, Blob Storage offers three different types of blobs: block blobs, append blobs, and page blobs.</span></span> <span data-ttu-id="d847d-166">Библиотека iOS хранилища Azure поддерживает все три типа BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-166">The Azure Storage iOS library supports all three types of blobs.</span></span> <span data-ttu-id="d847d-167">В большинстве случаев рекомендуется использовать блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="d847d-167">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="d847d-168">В следующем примере показано, как отправить блочный BLOB-объект из NSString.</span><span class="sxs-lookup"><span data-stu-id="d847d-168">The following example shows how to upload a block blob from an NSString.</span></span> <span data-ttu-id="d847d-169">Если BLOB-объект с таким именем уже существует в этом контейнере, содержимое этого объекта будет перезаписано.</span><span class="sxs-lookup"><span data-stu-id="d847d-169">If a blob with the same name already exists in this container, the contents of this blob will be overwritten.</span></span>

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

                // Upload blob to Storage
                [blockBlob uploadFromText:@"This text will be uploaded to Blob Storage." completionHandler:^(NSError *error) {
                    if (error){
                        NSLog(@"Error in creating blob.");
                    }
                }];
            }
        }];
}
```

<span data-ttu-id="d847d-170">Убедиться, что все работает, можно в [обозревателе хранилищ Microsoft Azure](http://storageexplorer.com). Следует проверить, содержит ли контейнер *containerpublic* большой двоичный объект *sampleblob*.</span><span class="sxs-lookup"><span data-stu-id="d847d-170">You can confirm that this works by looking at the [Microsoft Azure Storage Explorer](http://storageexplorer.com) and verifying that the container, *containerpublic*, contains the blob, *sampleblob*.</span></span> <span data-ttu-id="d847d-171">В этом примере мы использовали открытый контейнер, поэтому проверку работы приложения также можно выполнить, перейдя к URI BLOB-объекта:</span><span class="sxs-lookup"><span data-stu-id="d847d-171">In this sample, we used a public container so you can also verify that this application worked by going to the blobs URI:</span></span>

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

<span data-ttu-id="d847d-172">Кроме отправки блочного BLOB-объекта из NSString существуют аналогичные методы для NSData, NSInputStream или локального файла.</span><span class="sxs-lookup"><span data-stu-id="d847d-172">In addition to uploading a block blob from an NSString, similar methods exist for NSData, NSInputStream, or a local file.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d847d-173">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="d847d-173">List the blobs in a container</span></span>
<span data-ttu-id="d847d-174">В следующем примере показано, как перечислить все BLOB-объекты в контейнере.</span><span class="sxs-lookup"><span data-stu-id="d847d-174">The following example shows how to list all blobs in a container.</span></span> <span data-ttu-id="d847d-175">При выполнении этой операции необходимо учитывать следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="d847d-175">When performing this operation, be mindful of the following parameters:</span></span>     

* <span data-ttu-id="d847d-176">**continuationToken** — маркер продолжения, который задает начало перечисления.</span><span class="sxs-lookup"><span data-stu-id="d847d-176">**continuationToken** - The continuation token represents where the listing operation should start.</span></span> <span data-ttu-id="d847d-177">Если маркер не указан, BLOB-объекты будут перечислены с самого начала.</span><span class="sxs-lookup"><span data-stu-id="d847d-177">If no token is provided, it will list blobs from the beginning.</span></span> <span data-ttu-id="d847d-178">Можно перечислить любое количество BLOB-объектов — от нуля до заданного максимума.</span><span class="sxs-lookup"><span data-stu-id="d847d-178">Any number of blobs can be listed, from zero up to a set maximum.</span></span> <span data-ttu-id="d847d-179">Даже если этот метод возвращает нулевые результаты, если `results.continuationToken` не равно нулю, это значит, что в службе могут быть дополнительные BLOB-объекты, которые не были перечислены.</span><span class="sxs-lookup"><span data-stu-id="d847d-179">Even if this method returns zero results, if `results.continuationToken` is not nil, there may be more blobs on the service that have not been listed.</span></span>
* <span data-ttu-id="d847d-180">**prefix** — можно указать префикс, который будет использоваться при перечислении BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-180">**prefix** - You can specify the prefix to use for blob listing.</span></span> <span data-ttu-id="d847d-181">Перечислены будут только BLOB-объекты, начинающиеся с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="d847d-181">Only blobs that begin with this prefix will be listed.</span></span>
* <span data-ttu-id="d847d-182">**useFlatBlobListing** — как упоминалось в разделе [Присвоение имен контейнерам и BLOB-объектам, а также создание ссылок на них](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) , хотя служба BLOB-объектов представляет собой плоскую схему хранилища, вы можете создать виртуальную иерархию, присваивая BLOB-объектам имена с информацией о пути.</span><span class="sxs-lookup"><span data-stu-id="d847d-182">**useFlatBlobListing** - As mentioned in the [Naming and referencing containers and blobs](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) section, although the Blob service is a flat storage scheme, you can create a virtual hierarchy by naming blobs with path information.</span></span> <span data-ttu-id="d847d-183">Однако неплоское перечисление в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d847d-183">However, non-flat listing is currently not supported.</span></span> <span data-ttu-id="d847d-184">Эта функция станет доступной в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="d847d-184">This feature is coming soon.</span></span> <span data-ttu-id="d847d-185">Сейчас же это значение должно быть **YES** (Да).</span><span class="sxs-lookup"><span data-stu-id="d847d-185">For now, this value should be **YES**.</span></span>

* <span data-ttu-id="d847d-186">**blobListingDetails** — вы можете указать, какие элементы будут включены при перечислении BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-186">**blobListingDetails** - You can specify which items to include when listing blobs</span></span>
  * <span data-ttu-id="d847d-187">_AZSBlobListingDetailsNone_: вывод списка только зафиксированных больших двоичных объектов без возвращения их метаданных.</span><span class="sxs-lookup"><span data-stu-id="d847d-187">_AZSBlobListingDetailsNone_: List only committed blobs, and do not return blob metadata.</span></span>
  * <span data-ttu-id="d847d-188">_AZSBlobListingDetailsSnapshots_: вывод списка зафиксированных больших двоичных объектов и их моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="d847d-188">_AZSBlobListingDetailsSnapshots_: List committed blobs and blob snapshots.</span></span>
  * <span data-ttu-id="d847d-189">_AZSBlobListingDetailsMetadata_: извлечение метаданных каждого большого двоичного объекта, возвращаемого при перечислении.</span><span class="sxs-lookup"><span data-stu-id="d847d-189">_AZSBlobListingDetailsMetadata_: Retrieve blob metadata for each blob returned in the listing.</span></span>
  * <span data-ttu-id="d847d-190">_AZSBlobListingDetailsUncommittedBlobs_: вывод списка зафиксированных и незафиксированных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-190">_AZSBlobListingDetailsUncommittedBlobs_: List committed and uncommitted blobs.</span></span>
  * <span data-ttu-id="d847d-191">_AZSBlobListingDetailsCopy_: добавление в список свойств копий.</span><span class="sxs-lookup"><span data-stu-id="d847d-191">_AZSBlobListingDetailsCopy_: Include copy properties in the listing.</span></span>
  * <span data-ttu-id="d847d-192">_AZSBlobListingDetailsAll_: вывод списка всех доступных зафиксированных больших двоичных объектов, незафиксированных больших двоичных объектов и моментальных снимков, а также возвращение всех метаданных и состояния копий этих объектов.</span><span class="sxs-lookup"><span data-stu-id="d847d-192">_AZSBlobListingDetailsAll_: List all available committed blobs, uncommitted blobs, and snapshots, and return all metadata and copy status for those blobs.</span></span>
* <span data-ttu-id="d847d-193">**maxResults** — максимальное количество результатов, возвращаемых этой операцией.</span><span class="sxs-lookup"><span data-stu-id="d847d-193">**maxResults** - The maximum number of results to return for this operation.</span></span> <span data-ttu-id="d847d-194">Значение -1 используется для снятия ограничения.</span><span class="sxs-lookup"><span data-stu-id="d847d-194">Use -1 to not set a limit.</span></span>
* <span data-ttu-id="d847d-195">**completionHandler** — блок кода, выполняемого с использованием результатов операции перечисления.</span><span class="sxs-lookup"><span data-stu-id="d847d-195">**completionHandler** - The block of code to execute with the results of the listing operation.</span></span>

<span data-ttu-id="d847d-196">В этом примере используется вспомогательный метод для рекурсивного вызова метода перечисления BLOB-объектов при каждом возврате маркера продолжения.</span><span class="sxs-lookup"><span data-stu-id="d847d-196">In this example, a helper method is used to recursively call the list blobs method every time a continuation token is returned.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="d847d-197">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="d847d-197">Download a blob</span></span>
<span data-ttu-id="d847d-198">В следующем примере показано, как загрузить BLOB-объект в объект NSString.</span><span class="sxs-lookup"><span data-stu-id="d847d-198">The following example shows how to download a blob to a NSString object.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="d847d-199">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="d847d-199">Delete a blob</span></span>
<span data-ttu-id="d847d-200">В следующем примере показано, как удалить BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="d847d-200">The following example shows how to delete a blob.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="d847d-201">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="d847d-201">Delete a blob container</span></span>
<span data-ttu-id="d847d-202">В следующем примере показано, как удалить контейнер.</span><span class="sxs-lookup"><span data-stu-id="d847d-202">The following example shows how to delete a container.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d847d-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d847d-203">Next steps</span></span>
<span data-ttu-id="d847d-204">Теперь, когда вы узнали, как использовать хранилище BLOB-объектов из iOS, используйте следующие ссылки, чтобы узнать больше о библиотеке iOS и службе хранилища.</span><span class="sxs-lookup"><span data-stu-id="d847d-204">Now that you've learned how to use Blob Storage from iOS, follow these links to learn more about the iOS library and the Storage service.</span></span>

* [<span data-ttu-id="d847d-205">Клиентская библиотека хранилища Azure для iOS</span><span class="sxs-lookup"><span data-stu-id="d847d-205">Azure Storage Client Library for iOS</span></span>](https://github.com/azure/azure-storage-ios)
* [<span data-ttu-id="d847d-206">Справочная документация по использованию службы хранилища Azure в iOS</span><span class="sxs-lookup"><span data-stu-id="d847d-206">Azure Storage iOS Reference Documentation</span></span>](http://azure.github.io/azure-storage-ios/)
* [<span data-ttu-id="d847d-207">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d847d-207">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="d847d-208">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d847d-208">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage)

<span data-ttu-id="d847d-209">Если у вас есть вопросы по данной библиотеке, вы можете опубликовать их на нашем [форуме MSDN по Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) или на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span><span class="sxs-lookup"><span data-stu-id="d847d-209">If you have questions regarding this library, feel free to post to our [MSDN Azure forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) or [Stack Overflow](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).</span></span>
<span data-ttu-id="d847d-210">Если у вас есть предложения по функциям службы хранилища Azure, вы можете опубликовать их на сайте [отзывов о службе хранилища Azure](https://feedback.azure.com/forums/217298-storage/).</span><span class="sxs-lookup"><span data-stu-id="d847d-210">If you have feature suggestions for Azure Storage, please post to [Azure Storage Feedback](https://feedback.azure.com/forums/217298-storage/).</span></span>

