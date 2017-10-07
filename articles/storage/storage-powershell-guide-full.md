---
title: "aaaUsing Azure PowerShell с хранилищем Azure | Документы Microsoft"
description: "Узнайте, как toouse hello командлеты Azure PowerShell для toocreate хранилища Azure и управление учетными записями хранения; Работа с BLOB-объектов, таблиц, очередей и файлов; Настройка и запросов аналитики хранилища и создания подписей общего доступа."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Использование Azure PowerShell со службой хранилища Azure
## <a name="overview"></a>Обзор
Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell. Это оболочка командной строки на основе задач и язык сценариев, разработанные для администрирования системы. С помощью PowerShell можно легко контроля и автоматизации администрирования hello служб Azure и приложений. Например, можно использовать hello командлеты tooperform hello же задачи, которые можно выполнять через hello [портал Azure](https://portal.azure.com).

В этом руководстве мы изучим как toouse hello [командлеты хранилища Azure](/powershell/module/azurerm.storage/#storage) tooperform различных задач разработки и администрирования хранилища Azure.

Предполагается, что у вас есть опыт работы со [службой хранилища Azure](https://azure.microsoft.com/documentation/services/storage/) и [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Hello руководство содержит ряд сценариев использования hello toodemonstrate PowerShell со службой хранилища Azure. Необходимо обновить переменные сценария hello на основе конфигурации перед выполнением каждого сценария.

Первый раздел Hello в данном руководстве предоставляет быстрый обзор хранилища Azure и PowerShell. Подробные сведения и инструкции, запуск из hello [предварительные требования для использования со службой хранилища Azure Azure PowerShell](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Приступая к работе со службой хранилища Azure и PowerShell в течение 5 минут
В этом разделе показано, как tooaccess хранилища Azure с помощью PowerShell в 5 минут.

**Новый tooAzure:** получить подписку Microsoft Azure и учетной записи Майкрософт, связанные с этой подпиской. Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).

Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).

**После создания подписки Microsoft Azure и учетной записи:**

1. Загрузите и установите последние hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Начало интегрированная среда Windows PowerShell сценариев (ISE): На локальном компьютере перейдите toohello **запустить** меню. Тип **Администрирование** и нажмите кнопку toorun его. В hello **Администрирование** окно, щелкните правой кнопкой мыши **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **Запуск от имени администратора**.
3. В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта.
4. Теперь мы указываем, простой сценарий, который показывает основные tooaccess команд PowerShell хранилища Azure. сценарий Hello сначала запросит tooadd учетные данные вашей учетной записи Azure toohello учетная запись Azure локальной среде PowerShell. Затем сценарий hello присвоить значение по умолчанию hello подписки Azure и создать новую учетную запись хранения в Azure. Затем сценарий hello создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob). После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, создает новый каталог назначения на своем локальном компьютере и загрузите файл изображения hello.
5. В следующий раздел кода hello, выберите сценарий hello между hello примечания **#begin** и **#end**. Нажмите клавиши CTRL + C toocopy его toohello буфер обмена.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. В **интегрированной среды Сценариев Windows PowerShell**, нажмите клавиши CTRL + V toocopy hello скрипта. Щелкните **Файл** > **Сохранить**. В hello **Сохранить как** диалоговое окно, имя типа hello hello файла скрипта, такие как «mystoragescript». Щелкните **Сохранить**.
7. Теперь требуется переменных сценария hello tooupdate на основании параметров конфигурации. Необходимо обновить hello **$SubscriptionName** переменных с собственной подписки. Можно сохранить hello другие переменные, как указано в скрипте hello или обновлять их по своему усмотрению.
   
   * Необходимо обновить переменную **$SubscriptionName**, используя данные собственной подписки. Выполните одно из следующих трех способов toolocate hello именем подписки hello.
     
    а. В **интегрированной среды Сценариев Windows PowerShell**, нажмите кнопку **файл** > **New** toocreate новый файл скрипта. Следующие hello копирования сценариев toohello новый файл скрипта и нажмите кнопку **отладки** > **запуска**. Hello следующий сценарий будет запросить учетные данные вашей учетной записи Azure tooadd toohello учетная запись Azure локальной среде PowerShell и отобразите все подписки hello, подключенных toohello локальный сеанс PowerShell. Запишите имя hello hello подписки, которые должны toouse, однако при этом учебнике:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. Имя toolocate и скопируйте подписки в hello [портал Azure](https://portal.azure.com)в hello концентратора меню hello слева, нажмите кнопку **подписки**. Скопируйте имя hello подписку, которую нужно toouse при выполнении скриптов hello в данном руководстве.
     
     ![Портал Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. Имя toolocate и скопируйте подписки в hello [классический портал Azure](https://manage.windowsazure.com/), прокрутите список вниз и нажмите кнопку **параметры** на hello левая сторона hello портала. Нажмите кнопку **подписки** toosee список подписок. Скопируйте hello имя подписки на toouse во время выполнения получает скрипты hello в данном руководстве.
     
     ![классическом портале Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** использовать hello с заданным именем в скрипте hello, или введите новое имя для вашей учетной записи. **Важно:** hello имя учетной записи хранения hello должно быть уникальным в Azure. и состоять из символов нижнего регистра.
   * **$Location:** заданному «West US» hello в скрипте hello, или выберите другие расположения Azure, например Восток США, Северной Европе и т. д.
   * **$ContainerName:** использовать hello с заданным именем в скрипте hello, или введите новое имя для контейнера.
   * **$ImageToUpload:** введите рисунок tooa путь на локальном компьютере, например: «C:\Images\HelloWorld.png».
   * **$DestinationFolder:** файлы toostore путь локального каталога tooa загружаются из хранилища Azure, такие как ввод: «C:\DownloadImages».
8. После обновления с помощью переменных сценария hello в файле «mystoragescript.ps1» hello, нажмите кнопку **файл** > **Сохранить**. Нажмите кнопку **отладки** > **запуска** или нажмите клавишу **F5** toorun hello скрипта.  

После запуска сценария hello должно быть локальную целевую папку, которая содержит файл изображения загружаются hello. Следующий снимок экрана приветствия показан пример выходных данных:

![Загрузка BLOB-объектов](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hello «Приступая к работе с хранилища Azure и PowerShell, в течение 5 минут» предоставляемые краткие сведения о том, как toouse Azure PowerShell со службой хранилища Azure. Подробные сведения и инструкции мы рекомендуем вам hello tooread следующих разделах.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Предварительные требования для использования Azure PowerShell со службой хранилища Azure
Необходимо подписки и учетной записи toorun hello командлеты PowerShell Azure в данном руководстве, как описано выше.

Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell. Сведения об установке и настройке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Рекомендуется загрузить и установить или обновить последнюю версию модуля Azure PowerShell toohello перед использованием в этом руководстве.

Можно запускать командлеты hello в консоли Windows PowerShell hello или hello Сценариев Windows PowerShell интегрированной среде (). Например, tooopen **интегрированной среды Сценариев Windows PowerShell**откройте меню "Пуск" toohello, введите Администрирование и щелкните toorun его. В "Администрирование" hello щелкните правой кнопкой мыши интегрированной среды Сценариев Windows PowerShell, запуск от имени администратора.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Как toomanage хранилища учетных записей в Azure

Давайте рассмотрим процесс управления учетными записями хранения в Azure с помощью PowerShell.

### <a name="how-tooset-a-default-azure-subscription"></a>Как tooset значение по умолчанию подписки Azure
toomanage хранилища Azure с помощью Azure PowerShell, необходимо tooauthenticate средой клиента в Azure через Azure Active Directory или проверку подлинности на основе сертификатов. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) учебника. В этом руководстве используется проверка подлинности Azure Active Directory hello.

1. В интегрированной среде Сценариев Windows PowerShell введите следующие команды tooadd hello toohello учетная запись Azure локальной среде PowerShell:

    ```powershell
    Add-AzureAccount
    ```

2. В окне «Вход tooMicrosoft Azure» hello, тип hello адрес электронной почты и пароль, связанный с вашей учетной записью. Azure выполняет проверку подлинности и сохраняет hello учетные данные и затем закрывает окно приветствия.

3. Затем выполните hello, следующая команда tooview hello Azure учетные записи в локальной среде PowerShell и убедитесь, что ваша учетная запись:
   
    ```powershell
    Get-AzureAccount
    ```
4. Затем запустите следующий командлет tooview hello все подписки hello, подключенных toohello локальный сеанс PowerShell и убедитесь, что подписки:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset значение по умолчанию подписка Azure, выполните командлет Select-AzureSubscription hello:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Проверьте имя hello подписки по умолчанию hello, выполнив командлет Get-AzureSubscription hello:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee все hello доступных командлетов PowerShell для хранилища Azure, выполните:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Как toocreate новую учетную запись хранилища Azure
toouse хранилища Azure, потребуется учетная запись хранения. После настройки подписки tooyour tooconnect компьютера, можно создать новую учетную запись хранилища Azure.

1. Выполните все hello доступные расположения toofind командлет Get-AzureLocation hello:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Затем запустите toocreate командлет New-AzureStorageAccount hello новой учетной записи хранения. Hello следующий пример создает новую учетную запись хранилища в центре обработки данных «West US» hello.
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> Hello имя учетной записи должно быть уникальным в Azure и должны быть строчными. Соглашения об именовании и ограничениях см. в статьях [Об учетных записях хранения Azure](storage-create-storage-account.md) и [Именование контейнеров, больших двоичных объектов, метаданных и ссылка на них](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Как tooset учетную запись хранилища Azure по умолчанию
В подписке может иметься несколько учетных записей хранения. Можно выбрать один из них и задать его значение как hello учетной записи хранения по умолчанию для всех hello хранилища команды в hello же сеанс PowerShell. Это позволяет toorun hello Azure PowerShell хранения команд без указания контекста хранилища hello явным образом.

1. tooset учетной записи хранения по умолчанию для вашей подписки, запустите командлет Set-AzureSubscription hello.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Затем запустите tooverify командлет Get-AzureSubscription hello, учетной записи хранилища hello связан с вашей учетной записи подписки по умолчанию. Эта команда возвращает свойства подписки hello на hello текущей подписке, включая его текущей учетной записи хранилища.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Как toolist все Azure учетных записей хранения в подписке
Каждая подписка Azure может содержать до too100 учетные записи хранения. Hello наиболее актуальные сведения об ограничениях см. в разделе [подписки Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md).

Выполните следующий командлет toofind hello имя и состояние hello учетных записей хранения в текущей подписке hello hello.

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Как toocreate контекст хранилища Azure
Контекст хранилища Azure — это объект в учетные данные хранилища hello tooencapsulate PowerShell. Контекст хранилища во время выполнения все последующие командлет благодаря использованию вы tooauthenticate запрос без указания явно hello учетной записи хранилища и ключа доступа. Контекст хранилища можно создать несколькими способами, например с помощью имени и ключа доступа учетной записи хранения, токена подписи общего доступа, строки подключения или анонимно. Дополнительные сведения см. в описании [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Используйте один из следующих трех способов toocreate hello контекст хранилища.

* Запустите hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind командлет out hello ключ доступа основного хранилища для вашей учетной записи хранилища Azure. Затем вызовите hello [New AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate командлет контекст хранилища:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Создать маркер подписи общего доступа для контейнера хранилища Azure и использовать его toocreate контекст хранилища:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Дополнительные сведения см. в статьях [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) и [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* В некоторых случаях может потребоваться конечных точек службы hello toospecify при создании нового контекста хранилища. Это может потребоваться при вы зарегистрировали доменное имя для вашей учетной записи хранения со службой BLOB-объектов hello, или требуется toouse подписанный URL-адрес для доступа к ресурсам хранилища. Набор конечных точек службы hello в строку подключения и использовать его toocreate новый контекст хранилища, как показано ниже:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Дополнительные сведения о том, как tooconfigure строки подключения хранилища, в разделе [Настройка строк подключения](storage-configure-connection-string.md).

Теперь, когда вы настроили на компьютере и узнали, как toomanage подписками и учетными записями хранения, с помощью Azure PowerShell, перейдите в следующий раздел toolearn toohello как большие двоичные объекты toomanage Azure и больших двоичных объектов моментальные снимки.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Как tooretrieve и повторное создание ключей хранилища Azure
Учетная запись хранилища Azure предоставляется с двумя ключами учетной записи. Можно использовать следующий командлет tooretrieve hello ключей.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Используйте следующий командлет tooretrieve определенного ключа hello. Допустимые значения: Primary и Secondary  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Если вы хотите tooregenerate ключи, используйте следующий командлет hello. Допустимые значения параметра -KeyType: Primary и Secondary

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Как большие двоичные объекты toomanage Azure
Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS. В этом разделе предполагается, что вы уже знакомы с основными понятиями hello Azure Blob Storage Service. Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md) и [Понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Как toocreate контейнера
Каждый BLOB-объект в хранилище Azure должен находиться в контейнере. Можно создать с помощью командлета New-AzureStorageContainer hello закрытый контейнер:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**. tooprevent анонимный доступ к tooblobs параметр разрешения hello набора слишком**Off**. По умолчанию hello новый контейнер является закрытым и может осуществляться только владельцем учетной записи hello. анонимные открытый tooallow чтения tooblob доступ к ресурсам, но не toocontainer метаданные или toohello список больших двоичных объектов в контейнере hello, параметру hello разрешение слишком**большого двоичного объекта**. полный открытый tooallow чтения tooblob доступ к ресурсам, метаданные контейнера и hello список больших двоичных объектов в контейнере hello, задайте параметр разрешение hello слишком**контейнер**. Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Как tooupload большого двоичного объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты. Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).

tooupload большие двоичные объекты в контейнере tooa, можно использовать hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) командлета. По умолчанию эта команда передает hello локальные файлы tooa блочного большого двоичного объекта. Тип hello toospecify для hello большого двоичного объекта, вы можете использовать параметр - BlobType hello.

Hello следующем примере выполняется hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget командлет hello все файлы в указанной папке hello и передает их toohello следующий командлет с помощью оператора конвейера hello. Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) командлет отправляет hello локальные файлы tooyour контейнера:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Как toodownload большие двоичные объекты из контейнера
Привет, в следующем примере показано, как toodownload большие двоичные объекты из контейнера. пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее первичный ключ доступа. Затем пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета. Затем пример hello использует hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) командлет toodownload BLOB-объектов в hello локальной целевой папки.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Как toocopy большие двоичные объекты из одной tooanother контейнер хранилища
Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями. Hello следующем примере показано, как toocopy большие двоичные объекты из одного места хранения tooanother контейнера в двух разных учетных записей хранения. пример Hello сначала задает переменные для источника и назначения учетных записей хранилища, а затем создает контекст хранилища для каждой учетной записи. Далее пример hello копирует BLOB-объектов из hello исходный контейнер toohello конечный контейнер с помощью hello [AzureStorageBlobCopy начала](/powershell/module/azure.storage/start-azurestorageblobcopy) командлета. пример Hello предполагается, что hello источника и назначения и учетных записей хранилища контейнеры уже существуют.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Обратите внимание, что этот пример выполняет асинхронное копирование. Можно отслеживать состояние hello каждой копии, выполнив hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) командлета.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Как toocopy большие двоичные объекты из дополнительного расположения
Большие двоичные объекты можно скопировать из дополнительного расположения hello поддержкой RA-GRS учетной записи.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Как toodelete большого двоичного объекта
toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать командлет Remove-AzureStorageBlob hello на нем. Привет, следующий пример удаляет все большие двоичные объекты hello в данном контейнере. пример Hello сначала задает переменные для учетной записи хранения, а затем создает контекст хранилища. Далее пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета и запускает hello [AzureStorageBlob удаление](/powershell/module/azure.storage/remove-azurestorageblob) командлет tooremove BLOB-объекты из контейнера в хранилище Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Как toomanage Azure BLOB-объектов моментальные снимки
Azure позволяет создать моментальный снимок BLOB-объекта. Моментальный снимок — это версия BLOB-объекта только для чтения, сделанная в определенный момент времени. После создания моментального снимка его можно читать, копировать или удалять, но нельзя изменять. Моментальные снимки обеспечивают tooback способом копирования большого двоичного объекта, как оно отображается в момент времени. Дополнительные сведения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Как toocreate снимка большого двоичного объекта
toocreate snaphot большого двоичного объекта, сначала нужно получить ссылку на большой двоичный объект, а затем вызвать hello `ICloudBlob.CreateSnapshot` метода. Hello в примере сначала устанавливается переменных для учетной записи хранилища, а затем создает контекст хранилища. Затем пример hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello командлета и выполняется [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate метод моментальный снимок.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Как моментальные снимки toolist большого двоичного объекта в
Можно создать любое количество моментальных снимков для BLOB-объекта. Можно перечислить hello моментальных снимков, связанных с вашей tootrack большого двоичного объекта вашей текущей моментальные снимки. Hello следующий пример использует предопределенные hello BLOB-объекта и вызывает метод [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлет toolist hello моментальные снимки большого двоичного объекта.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Как toocopy моментальный снимок большого двоичного объекта
Можно скопировать моментальный снимок hello toorestore моментального снимка большого двоичного объекта. Подробные сведения и ограничения см. в статье [Создание моментального снимка большого двоичного объекта](http://msdn.microsoft.com/library/azure/hh488361.aspx). Hello в примере сначала устанавливается переменных для учетной записи хранилища, а затем создает контекст хранилища. Затем пример hello определяет переменные имя контейнера и больших двоичных объектов hello. пример Hello извлекает ссылку BLOB-объекта с помощью hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) командлета и запускает hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate метод моментального снимка. Затем пример hello запускает hello [AzureStorageBlobCopy начала](/powershell/module/azure.storage/start-azurestorageblobcopy) командлет toocopy hello моментальный снимок большого двоичного объекта, используя объект ICloudBlob hello для hello исходного большого двоичного объекта. Убедитесь, что переменные hello tooupdate исходя из имеющейся конфигурации перед рабочего примера hello. Обратите внимание, что, hello, в следующем примере предполагается, что hello источника и назначения контейнеров и hello исходный большой двоичный объект уже существует.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Теперь, когда вы узнали, как большие двоичные объекты toomanage Azure и больших двоичных объектов моментальные снимки с помощью Azure PowerShell, перейдите toohello Далее раздел toolearn как toomanage таблиц, очередей и файлов.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Как toomanage Azure таблицы и таблицы сущностей
Служба хранилища Azure таблицы — в хранилище данных NoSQL, который можно использовать toostore и запрос большого набора нереляционных структурированных данных. Основные компоненты службы hello Hello являются таблицы, сущности и свойства. Таблица представляет собой коллекцию сущностей. Сущность — это набор свойств. Каждая сущность может содержать до too252 свойства, которые являются все пары имя значение. В этом разделе предполагается, что вы уже знакомы с основными понятиями hello службы хранилища таблиц Azure. Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx) и [приступить к работе с хранилищем таблиц Azure, с помощью .NET](storage-dotnet-how-to-use-tables.md).

В следующих подразделах hello вы узнаете, как toomanage хранилище таблиц Azure службы с помощью Azure PowerShell. Hello сценарии включают **создание**, **удаление**, и **получение** **таблиц**, а также **добавление**, **запрос**, и **удаления сущностей таблицы**.

### <a name="how-toocreate-a-table"></a>Как toocreate таблицы
Каждая таблица должна находиться в учетной записи хранения Azure. Hello следующем примере показано, как toocreate таблица в хранилище Azure. пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем он использует hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate командлет таблица в хранилище Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Как tooretrieve таблицы
Можно запрашивать и получить одну или все таблицы в учетной записи хранения. Hello следующем примере показано, как в данной таблице с помощью tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Если вызвать командлет Get-AzureStorageTable hello без параметров, он получает все таблицы хранилища для учетной записи хранения.

### <a name="how-toodelete-a-table"></a>Как toodelete таблицы
Можно удалить таблицу из учетной записи хранилища с помощью hello [AzureStorageTable удаление](/powershell/module/azure.storage/remove-azurestoragetable) командлета.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Как toomanage таблицу сущностей
В настоящее время Azure PowerShell предоставляет командлеты сущностей таблицы toomanage непосредственно. tooperform операций в табличных объектах, можно использовать классы hello в hello [клиентская библиотека хранилища Azure для .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Как tooadd таблицу сущностей
tooadd таблица tooa объекта, сначала создайте объект, который определяет свойства сущности. Сущность может иметь свойства too255, включая 3 системные свойства: **PartitionKey**, **RowKey**, и **Timestamp**. Вы несете ответственность за вставки и обновления значения hello **PartitionKey** и **RowKey**. Hello server управляет значение hello **Timestamp**, которую нельзя вносить изменения. Hello вместе **PartitionKey** и **RowKey** уникально идентифицируют каждую сущность в таблицу.

* **PartitionKey**: Определяет hello секции, хранящиеся в сущности hello.
* **RowKey**: однозначно определяет сущность hello в секции hello.

Вы можете определить too252 пользовательские свойства для сущности. Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello следующем примере показано, как таблицы tooa tooadd сущностей. пример Hello показано, как tooretrieve hello таблицы сотрудников и добавить в нее несколько сущностей. Во-первых, он устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем он извлекает hello таблицы с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета. Здравствуйте, если таблица hello не существует, [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) командлета — toocreate используется таблица в хранилище Azure. Далее пример hello определяет пользовательскую функцию добавить сущность tooadd сущностей toohello таблицы путем указания каждой секции и ключ строки. hello вызовов функции Hello добавить сущность [New-Object](http://technet.microsoft.com/library/hh849885.aspx) командлет hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate класс объекта сущности. Позже, пример hello вызывает hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) метод для этой сущности объекта tooadd его tooa таблицы.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Как tooquery таблицу сущностей
tooquery таблицы, используйте hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) класса. Hello в примере предполагается, что вы уже запускали hello скрипта, данного в hello, как tooadd сущностей разделах данного руководства. пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста hello хранилища, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем она попытается таблицы tooretrieve hello ранее созданные «сотрудники», с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета. Вызов hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) на hello Microsoft.WindowsAzure.Storage.Table.TableQuery класс создает новый объект запроса. пример Hello ищет hello сущностей, которые имеют столбец «ID», значение которого равно 1, как указано в фильтр строк. Дополнительные сведения см. в статье [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Запросы к таблицам и сущностям). При выполнении этот запрос возвращает все сущности, которые соответствуют критериям фильтра hello.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Как toodelete таблицу сущностей
Сущность можно удалить с помощью ее ключей раздела и строки. Hello в примере предполагается, что вы уже запускали hello скрипта, данного в hello, как tooadd сущностей разделах данного руководства. пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста hello хранилища, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем она попытается таблицы tooretrieve hello ранее созданные «сотрудники», с помощью hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) командлета. Если hello таблица существует, пример hello вызывает hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve метод сущностью, основанной на значениях ключей секций и строк. Затем передайте hello сущности toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete метод.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Как toomanage Azure помещает в очередь и очередь сообщений
Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS. В этом разделе предполагается, что вы уже знакомы с основными понятиями hello службы хранилища очередей Azure. Дополнительные сведения см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](storage-dotnet-how-to-use-queues.md).

В этом разделе будет показано, как toomanage хранилища очередей Azure службы с помощью Azure PowerShell. Hello сценарии включают **Вставка** и **удаление** очередь сообщений, а также **создание**, **удаление**и **Получение очередей**.

### <a name="how-toocreate-a-queue"></a>Как toocreate очереди
Hello следующий пример сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем он вызывает [New AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate командлет очередь с именем «queuename».

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Сведения о соглашениях об именовании для службы очередей Azure см. в статье [Именование очередей и метаданных](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Как tooretrieve очереди
Можно запрашивать и определенной очереди или список всех очередей hello в учетной записи хранения. Hello следующем примере показано, как hello в указанной очереди с помощью tooretrieve [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) командлета.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Если вы вызываете hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) командлет без параметров возвращает список всех очередей hello.

### <a name="how-toodelete-a-queue"></a>Как toodelete очереди
toodelete очередь и все сообщения hello содержащихся в ней командлет Remove-AzureStorageQueue hello вызова. Hello в следующем примере показано, как в указанной очереди с помощью toodelete hello командлет Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Как tooinsert сообщения в очереди
tooinsert сообщения в существующую очередь, сначала создайте новый экземпляр hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) класса. Затем вызовите hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) метод. Для создания CloudQueueMessage можно использовать строку (в формате UTF-8) или массив байтов.

Hello в следующем примере показано, как очередь tooa tooadd сообщений. пример Hello сначала устанавливает соединение tooAzure хранилища с помощью контекста учетной записи хранилища hello, который включает в себя имя учетной записи хранения hello и ее ключа доступа. Затем он извлекает hello указанной очереди с помощью hello [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) командлета. Если hello очередь существует, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) командлета — используется toocreate экземпляр hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) класса. Более поздней версии, пример hello вызывает hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) метод tooadd объекта этого сообщения оно tooa очереди. Ниже приведен код, который извлекает очереди и вставляет приветственное сообщение «MessageInfo».

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Как toode в очередь на hello следующего сообщения
Код удаляет сообщение из очереди в два этапа. При вызове hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) метода, вы получаете следующее сообщение hello в очереди. Сообщение, возвращенное из **GetMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди. toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) метод. Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку. Вызовы кода **DeleteMessage** сразу после обработки сообщения hello.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Как toomanage Azure файла, папки и файлы
Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB hello. Виртуальные машины Microsoft Azure и облачных служб можно совместно использовать данные файлов между компонентами приложения с помощью монтируемых хранилищ и локальных приложений можно открыть файл данных в общей папке посредством API хранилища файлов hello или Azure PowerShell.

Подробнее о хранилище файлов Azure см. в статьях [Приступая к работе с хранилищем файлов Azure в Windows](storage-dotnet-how-to-use-files.md) и [API REST службы файлов](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Как tooset и запросов аналитики хранилища
Можно использовать [аналитики хранилища Azure](storage-analytics.md) показатели toocollect учетных записей хранилища Azure, а также данные журналов о запросах, отправляемых tooyour учетной записи хранилища. Можно использовать работоспособность hello toomonitor метрик хранилища учетной записи хранилища и toodiagnose ведения журнала хранилища и неполадок, связанных с вашей учетной записи хранилища. Вы можете настроить отслеживание с помощью hello портал Azure или Windows PowerShell или программным путем с помощью клиентской библиотеки хранилища hello. Ведение журнала хранилища происходит на стороне сервера, а также позволяет toorecord подробные сведения об успешных и неудачных запросов в вашей учетной записи хранилища. Эти журналы включить сведения о toosee операций delete от вашей таблицы, очереди и больших двоичных объектов а также hello причин для невыполненных запросов, чтения и записи.

toolearn tooenable и просмотр метрик хранилища данных, с помощью PowerShell, в статье [как tooenable метрик хранилища с помощью PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn tooenable и извлечь ведения журнала хранилища данных с помощью PowerShell, в статье [как tooenable хранилища ведение журнала с помощью PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) и [поиск данных ведения журнала хранилища журнала](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Подробные сведения по использованию метрик хранилищ и ведению журналов хранилища проблемы tootroubleshoot хранилища см. в разделе [мониторинг, диагностика и устранение неполадок хранилища Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Способ совместного использования toomanage URL-адреса (SAS) и хранимой политикой доступа
Подписи общего доступа являются важной частью hello модель безопасности для всех приложений, использующих хранилище Azure. Они могут использоваться для предоставления tooclients учетной записи хранилища tooyour ограниченные разрешения, не следует hello ключ учетной записи. По умолчанию только владелец hello hello учетной записи хранения может обращаться к BLOB-объектов, таблиц и очередей в этой учетной записи. Если служба или приложение, должен toomake эти ресурсы доступны tooother клиенты без предоставления ключа доступа, у вас есть три варианта:

* Задайте контейнер разрешения toopermit анонимный доступ для чтения toohello контейнера и BLOB-объектов. Такие разрешения нельзя задать для таблиц и очередей.
* Используйте подпись общего доступа, которая предоставляет ограниченный доступ toocontainers права, большие двоичные объекты, очереди и таблицы для определенного интервала времени.
* Используйте tooobtain политики доступа дополнительный уровень контроля над подписями общего доступа к контейнеру и его большие двоичные объекты, очереди или таблицы. Hello хранимая политика доступа позволяет время начала toochange hello, истечение срока действия и разрешения для подписи, или toorevoke ее после ее выдачи.

Подписанный URL-адрес может быть в одной из двух следующих форм.

* **Ad hoc SAS**: при создании нерегламентированного SAS, hello время начала, время окончания срока действия, и разрешения для hello SAS указаны на hello универсальный код Ресурса SAS. Этот тип подписанного URL-адреса можно создать для контейнера, большого двоичного объекта, таблицы или очереди, и его невозможно отозвать.
* **SAS с хранимой политикой доступа**: определенной хранимой политики доступа на контейнер ресурсов контейнер больших двоичных объектов, таблицы или очереди - и его можно использовать toomanage ограничения для одного или нескольких подписей общего доступа. При связывании подписанный URL-адрес с хранимой политикой доступа hello SAS наследует ограничения hello - hello время начала, время окончания и разрешения -, определенные для hello хранимые политики доступа. Подписанный URL-адрес этого типа можно отозвать.

Дополнительные сведения см. в разделе [с помощью общего доступа подписи (SAS)](storage-dotnet-shared-access-signature-part-1.md) и [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md).

В следующих разделах hello, вы узнаете, как toocreate политику доступа маркера и хранимые подпись общего доступа для таблиц Azure. Azure PowerShell предоставляет одинаковые командлеты для контейнеров, больших двоичных объектов и очередей. hello загрузки сценариев hello toorun в этом разделе [Azure PowerShell версии 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) или более поздней версии.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Как токен SAS toocreate на основе политик
Используйте toocreate командлет New-AzureStorageTableStoredAccessPolicy hello новой хранимой политики доступа. Затем вызовите метод hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate командлет новый маркер подписи общего доступа на основе политик для таблицы хранилища Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Как toocreate нерегламентированных (без отзыва) токена подписи коллективного доступа
Используйте hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate командлет новый нерегламентированных (без отзыва) токена подписи коллективного доступа для таблицы хранилища Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Как toocreate хранимой политики доступа
Используйте toocreate командлет hello AzureStorageTableStoredAccessPolicy создать новую политику доступа для таблицы хранилища Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Как tooupdate хранимой политики доступа
Используйте tooupdate командлета Set-AzureStorageTableStoredAccessPolicy hello существующую политику доступа для таблицы хранилища Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Как toodelete хранимой политики доступа
Используйте toodelete командлет Remove-AzureStorageTableStoredAccessPolicy hello хранимой политики доступа в таблице хранилища Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Как toouse хранилища Azure для государственных организаций США и Azure China
Среда Azure — это независимое развертывание Microsoft Azure, такое как [Azure для государственных организаций в правительстве США](https://azure.microsoft.com/features/gov/), [AzureCloud для глобального Azure](https://portal.azure.com) и [AzureChinaCloud для Azure под управлением 21Vianet в Китае](http://www.windowsazure.cn/). Можно выполнить развертывание новых сред Azure для правительства США и Китая.

toouse хранилища Azure с AzureChinaCloud необходимо toocreate контекст хранилища, которая связана с AzureChinaCloud. Выполните эти шаги tooget, которого вы начали.

1. Запустите hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee командлет hello доступных сред Azure:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Добавьте tooWindows учетная запись Azure China PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Создаете контекст хранилища для учетной записи AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse хранилища Azure с [США ](https://azure.microsoft.com/features/gov/)следует определить новую среду и затем создать новый контекст хранилища с данной средой:

1. Запустите hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee командлет hello доступных сред Azure:

    ```powershell
    Get-AzureEnvironment
    ```

2. Добавьте правительства США учетной записи tooWindows PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Создайте контекст хранилища для учетной записи AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Дополнительные сведения можно найти в разделе 

* [Руководство для разработчиков Microsoft Azure для государственных организаций](../azure-government-developer-guide.md)
* [Обзор отличий при создании приложения в службе в Китае](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве вы узнали, каким образом toomanage хранилища Azure с помощью Azure PowerShell. Ниже приведены некоторые связанные статьи и ресурсы для их изучения.

* [Документация по хранилищу Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Командлеты PowerShell службы хранилища Azure](/powershell/module/azurerm.storage/#storage)
* [Справочник по Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
