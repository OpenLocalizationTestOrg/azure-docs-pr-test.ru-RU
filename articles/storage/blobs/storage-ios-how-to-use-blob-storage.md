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
ms.openlocfilehash: cc08b76b682537a9a51e970c76bd76c7c06a4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ios"></a>Как toouse хранилища BLOB-объектов из операций ввода-вывода
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
В этой статье будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов Microsoft Azure. Hello примеры написаны на Objective-C и использовать hello [клиентская библиотека хранилища Azure для операций ввода-вывода](https://github.com/Azure/azure-storage-ios). Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов. Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#next-steps) раздела. Можно также загрузить hello [пример приложения](https://github.com/Azure/azure-storage-ios/tree/master/BlobSample) tooquickly разделе hello использование хранилища Azure в приложении iOS.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="import-hello-azure-storage-ios-library-into-your-application"></a>Импортировать приложение библиотеки iOS hello хранилища Azure
Вы можете импортировать библиотеки iOS hello хранилища Azure в приложение с помощью hello [CocoaPod хранилища Azure](https://cocoapods.org/pods/AZSClient) или путем импорта hello **Framework** файла. CocoaPod — hello, рекомендуется способом, так как он упрощает интеграции библиотеки hello, однако импорт из файла framework hello меньше вмешивается в существующем проекте.

toouse эту библиотеку необходимо hello следующие:
- iOS 8 или более поздней версии
- XCode 7 или более поздней версии

## <a name="cocoapod"></a>CocoaPod
1. Если вы еще не сделали этого, [установить CocoaPods](https://guides.cocoapods.org/using/getting-started.html#toc_3) на компьютере, открыв окно терминала и выполнив следующую команду hello
    
    ```shell   
    sudo gem install cocoapods
    ```

2. В каталоге проекта hello (hello каталог, содержащий ваш xcodeproj-файл), создайте новый файл с именем _Podfile_(без расширения файла). Добавьте следующие too_Podfile_ hello и сохраните.

    ```ruby
    platform :ios, '8.0'

    target 'TargetName' do
      pod 'AZSClient'
    end
    ```

3. В окне терминала hello перейдите toohello каталог проекта и выполнения hello следующую команду

    ```shell    
    pod install
    ```

4. Если XCODEPROJ-файл открыт в Xcode, закройте его. В файле проекта откройте hello только что созданный каталог проекта, который будет иметь расширение .xcworkspace hello. Это файл hello, мы будем работать с для теперь на.

## <a name="framework"></a>FRAMEWORK
Hello способом, который toouse hello библиотека — платформа hello toobuild вручную:

1. First, загрузки или клон hello [репозитория хранилища azure ios](https://github.com/azure/azure-storage-ios).
2. Перейдите в *azure-storage-ios* -> *Lib*(Библиотеки) -> *Azure Storage Client Library* (Клиентская библиотека службы хранилища Azure) и откройте файл `AZSClient.xcodeproj` в программе Xcode.
3. В hello верхней левой части Xcode изменение hello active схему из «Клиентская библиотека хранилища Azure» слишком «Framework».
4. Построение проекта hello (⌘ + B). На рабочем столе будет создан файл `AZSClient.framework`.

Затем можно импортировать файл framework hello в приложение, выполнив hello ниже:

1. Создайте новый проект или откройте существующий проект в Xcode.
2. Перетаскивание hello `AZSClient.framework` в навигаторе вашего проекта Xcode.
3. Выберите *Copy items if needed* (Копировать элементы при необходимости), а затем щелкните *Finish* (Готово).
4. Щелкните проект в левой навигационной hello и выберите команду hello *Общие* вкладку вверху hello редактор проекта hello.
5. В разделе hello *связанные платформы и библиотеки* статьи, нажмите кнопку Добавить hello (+).
6. В список библиотек, предоставляемых уже hello, поиск `libxml2.2.tbd` и добавить его в проект tooyour.

## <a name="import-hello-library"></a>Импорт библиотеки hello 
```objc
// Include hello following import statement toouse blob APIs.
#import <AZSClient/AZSClient.h>
```

При использовании Swift, может потребоваться toocreate мост заголовок и импортировать < AZSClient/AZSClient.h > существует:

1. Создать файл заголовка `Bridging-Header.h`и добавить hello выше инструкции import.
2. Go toohello *параметры построения* и найдите *заголовка мост Objective-C*.
3. Дважды щелкните в поле hello *заголовка мост Objective-C* и добавьте файл заголовка tooyour hello путь:`ProjectName/Bridging-Header.h`
4. Сборки hello проекта (⌘ + B) tooverify, hello мост заголовок был принят Xcode.
5. Начните использовать hello библиотеки непосредственно в любой Swift файл, нет необходимости в инструкциях импорта.

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="asynchronous-operations"></a>Асинхронные операции
> [!NOTE]
> Все методы для выполнения запроса к службе hello это асинхронные операции. В образцах кода hello вы найдете, что эти методы имеют обработчик завершения. Код в обработчике завершения hello будет выполняться **после** hello запрос завершается. Код после запустится обработчик завершения hello **при** был выполнен запрос hello.
> 
> 

## <a name="create-a-container"></a>Создание контейнера
Каждый BLOB-объект в хранилище Azure должен располагаться в контейнере. Hello следующий пример показывает, как toocreate контейнера, вызывать *newcontainer*, в учетной записи, если он еще не существует. При выборе имени для контейнера, следует учитывать hello, упомянутых выше правила именования.

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

Убедитесь, что все работает, просмотрев hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) и проверки того, что *newcontainer* в hello список контейнеров для учетной записи хранилища.

## <a name="set-container-permissions"></a>Назначение разрешений контейнера
Разрешения контейнера, настраиваемые по умолчанию, — это разрешения на **закрытый** доступ. При этом контейнеры предоставляют и другие возможности доступа.

* **Закрытый**: hello только владельцем учетной записи могут считываться данные контейнера и больших двоичных объектов.
* **BLOB-объект**: хотя данные BLOB-объекта, содержащиеся в контейнере, могут быть прочитаны через анонимный запрос, данные самого контейнера недоступны. Клиенты не могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос.
* **Контейнер**: данные контейнера и BLOB-объекта могут быть прочитаны через анонимный запрос. Клиенты могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.

Hello следующий пример показывает, как toocreate в контейнер с **контейнера** доступ к разрешений, которые будет разрешать доступ открытым и доступным только для чтения для всех пользователей на hello Интернет:

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

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Как упоминалось в hello [больших двоичных объектов основные понятия службы](#blob-service-concepts) раздел, хранилище BLOB-объектов предлагает три различных типа больших двоичных объектов: блочные большие двоичные объекты, добавлять большие двоичные объекты и страничные большие двоичные объекты. библиотеки iOS Hello хранилища Azure поддерживает все три типа больших двоичных объектов. В большинстве случаев блочного BLOB-объекта — hello, рекомендуется toouse типа.

Hello в следующем примере показано, как tooupload блок больших двоичных объектов из NSString. Если большой двоичный объект с таким же именем уже существует в этом контейнере hello hello содержимое этого большого двоичного объекта будет перезаписано.

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

Убедитесь, что все работает, просмотрев hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) и проверке этого контейнера hello *containerpublic*, содержит большой двоичный объект hello, *sampleblob*. В этом примере мы использовали открытого контейнера, вы можете убедиться, что это приложение работает с переходом toohello большие двоичные объекты URI:

    https://nameofyourstorageaccount.blob.core.windows.net/containerpublic/sampleblob

В дополнение к этому toouploading большой двоичный объект блока из NSString существуют аналогичные методы NSData, NSInputStream или локальный файл.

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
Hello следующем примере показано, как toolist все большие двоичные объекты в контейнере. При выполнении этой операции, следует учитывать hello следующие параметры:     

* **continuationToken** -hello представляет токен продолжения, начала операции перечисления hello. Если токен не предоставлен, он будет перечисление больших двоичных объектов с начала hello. Может быть указано любое количество больших двоичных объектов от нуля вверх tooa максимального. Даже если этот метод возвращает нулевой результат, если `results.continuationToken` имеет родителя, возможно, имеются большие двоичные объекты в службе hello, не перечислены.
* **префикс** -можно указать toouse hello префикс для списка больших двоичных объектов. Перечислены будут только BLOB-объекты, начинающиеся с этого префикса.
* **useFlatBlobListing** — как упоминалось в hello [именование и ссылки на контейнеры и большие двоичные объекты](#naming-and-referencing-containers-and-blobs) раздел, несмотря на то, что hello службы BLOB-объектов является схеме плоского хранилища, можно создать виртуальной иерархии больших двоичных объектов с путем к именованию сведения. Однако неплоское перечисление в настоящее время не поддерживается. Эта функция станет доступной в ближайшее время. Сейчас же это значение должно быть **YES** (Да).
* **blobListingDetails** -tooinclude какие элементы можно указать при перечислении больших двоичных объектов
  * _AZSBlobListingDetailsNone_: вывод списка только зафиксированных больших двоичных объектов без возвращения их метаданных.
  * _AZSBlobListingDetailsSnapshots_: вывод списка зафиксированных больших двоичных объектов и их моментальных снимков.
  * _AZSBlobListingDetailsMetadata_: получить метаданные большого двоичного объекта для каждого большого двоичного объекта возвращается в списке hello.
  * _AZSBlobListingDetailsUncommittedBlobs_: вывод списка зафиксированных и незафиксированных больших двоичных объектов.
  * _AZSBlobListingDetailsCopy_: копировался свойства в списке hello.
  * _AZSBlobListingDetailsAll_: вывод списка всех доступных зафиксированных больших двоичных объектов, незафиксированных больших двоичных объектов и моментальных снимков, а также возвращение всех метаданных и состояния копий этих объектов.
* **maxResults** -hello максимальное количество результатов tooreturn для этой операции. Ограничить toonot используйте -1.
* **completionHandler** -hello блок кода tooexecute результатами "hello" hello операции перечисления.

В этом примере вспомогательный метод способ используется toorecursively вызов hello список больших двоичных объектов каждый раз, возвращается токен продолжения.

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

## <a name="download-a-blob"></a>Загрузка BLOB-объектов
Следующий пример показывает как Hello toodownload объект NSString tooa больших двоичных объектов.

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

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
Следующий пример показывает как Hello toodelete большого двоичного объекта.

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

## <a name="delete-a-blob-container"></a>Удаление контейнера blob-объектов
Следующий пример показывает как Hello toodelete контейнера.

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

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали, как toouse хранилища BLOB-объектов из iOS, выполните следующие дополнительные сведения о библиотеке iOS hello toolearn ссылки и hello службы хранилища.

* [Клиентская библиотека хранилища Azure для iOS](https://github.com/azure/azure-storage-ios)
* [Справочная документация по использованию службы хранилища Azure в iOS](http://azure.github.io/azure-storage-ios/)
* [API-интерфейс REST служб хранилища Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage)

При наличии вопросов относительно этой библиотеки чувствовать себя свободного toopost tooour [форум MSDN Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=windowsazuredata) или [переполнения стека](http://stackoverflow.com/questions/tagged/windows-azure-storage+or+windows-azure-storage+or+azure-storage-blobs+or+azure-storage-tables+or+azure-table-storage+or+windows-azure-queues+or+azure-storage-queues+or+azure-storage-emulator+or+azure-storage-files).
Если у вас есть предложения компонентов для службы хранилища Azure, опубликуйте слишком[отзывы хранилища Azure](https://feedback.azure.com/forums/217298-storage/).

