---
title: "aaaUse hello .NET SDK toodevelop приложения в хранилище Озера данных Azure | Документы Microsoft"
description: "Использование пакета SDK .NET хранилища Озера данных Azure toocreate учетной записи хранилища Озера данных и выполнения основных операций в hello хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET
> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Узнайте, как toouse hello [пакета SDK .NET хранилища Озера данных Azure](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform основных операций, таких как создание папок, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).

## <a name="prerequisites"></a>Предварительные требования
* **Visual Studio 2013, 2015 или 2017**. Приведенные ниже инструкции Hello использовать Visual Studio 2015 с обновлением 2.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Учетная запись хранилища озера данных Azure**. Дополнительные сведения о toocreate учетную запись, в разделе [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)

* **Создание приложения Azure Active Directory**. Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD. Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Создание приложения .NET
1. Откройте Visual Studio и создайте консольное приложение.
2. Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.
3. Из **новый проект**введите или выберите hello следующие значения:

   | Свойство | Значение |
   | --- | --- |
   | Категория |Templates/Visual C#/Windows |
   | Шаблон |Консольное приложение |
   | Имя |CreateADLApplication |
4. Нажмите кнопку **ОК** toocreate hello проекта.
5. Добавьте проект tooyour пакеты Nuget hello.

   1. Щелкните правой кнопкой мыши имя проекта hello в обозревателе решений hello и нажмите кнопку **управление пакетами NuGet**.
   2. В hello **диспетчера пакетов Nuget** , убедитесь, что **источник пакета** задано слишком**nuget.org** и что **включить предварительный выпуск** флажок выбран.
   3. Поиск и установка hello следующие пакеты NuGet:

      * `Microsoft.Azure.Management.DataLake.Store`. В этом руководстве используется предварительная версия 2.1.3.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication`. В этом руководстве используется версия 2.2.12.

        ![Добавление источника Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Создание учетной записи Azure Data Lake")
   4. Закрыть hello **диспетчера пакетов Nuget**.
6. Откройте **Program.cs**, удаление существующего кода hello и затем добавьте следующие инструкции tooadd ссылки toonamespaces hello.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Объявления переменных hello, как показано ниже и укажите значения hello для хранилища Озера данных имя и имя группы ресурсов hello, которая уже существует. Кроме того убедитесь, что hello локальный путь и имя файла здесь должен существовать на компьютере hello. Добавьте следующий фрагмент кода после объявления пространств имен hello hello.

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

В оставшихся разделах статьи hello hello вы увидите, как toouse hello доступные операции tooperform методы .NET, такие как проверку подлинности, передачу файла, и т. д.

## <a name="authentication"></a>Аутентификация

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>При использовании проверки подлинности пользователя (рекомендуется для этого руководства)

Используется с существующие tooauthenticate собственное приложение Azure AD приложения **интерактивно**, который означает, будет предложено tooenter учетные данные Azure.

Для удобства использования в приведенном ниже фрагменте hello использует значения по умолчанию для идентификатора клиента и URI, который будет работать с любой подписке Azure перенаправления. toohelp быстрее завершить этот учебник, мы рекомендуем использовать этот подход. В приведенном ниже фрагменте hello просто укажите hello значение свой идентификатор клиента. Можно получить с помощью hello инструкций, приведенных в [создать приложение Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Несколько вещей tooknow об этом примере, приведенном выше:

* использует этот фрагмент toohelp ускорить hello учебник, в Azure AD и клиентского идентификатор, который доступен по умолчанию для всех подписок Azure. Таким образом, вы можете **использовать в приложении этот фрагмент в исходном виде**.
* Тем не менее если требуется toouse ваш домен Azure AD, а код клиента приложения, необходимо создать собственное приложение Azure AD и затем используйте hello Azure AD идентификатор, идентификатор клиента, клиента и URI перенаправления для приложения hello вы создали. Инструкции см. в статье [Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>При использовании проверки подлинности через секрет клиента со взаимодействием между службами
Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения **не в интерактивном режиме**, с помощью секрет клиента hello / ключ для приложения / службы-участника. Примените этот фрагмент кода к существующему веб-приложению Azure AD. Инструкции по статье toocreate hello Azure AD веб-приложение и как tooretrieve hello идентификатор клиента и секрет клиента, необходимые в следующем фрагменте hello [создать приложение для проверки подлинности службы для службы Active Directory с данными Хранилище Озера](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>При использовании проверки подлинности с помощью сертификата со взаимодействием между службами

Как третий вариант, hello следующий фрагмент кода может быть используется tooauthenticate приложения **не в интерактивном режиме**, с помощью hello сертификат для приложения Azure Active Directory / участника службы. Примените этот фрагмент кода к существующему [приложению Azure AD с помощью сертификатов](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Создание клиентских объектов
Hello следующий фрагмент кода создает учетную запись хранилища Озера данных hello и файловой системы объектов клиента, которые используются tooissue запросов toohello службой.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Получение списка всех учетных записей Data Lake Store в рамках подписки
Hello следующий фрагмент кода перечисляет все учетные записи хранилища Озера данных в рамках данной подписки Azure.

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a>Создайте каталог
Привет, в следующем фрагменте кода показан `CreateDirectory` метода, которые можно использовать toocreate каталогу в учетной записи хранилища Озера данных.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Отправить файл.
Привет, в следующем фрагменте кода показан `UploadFile` метода, которые можно использовать tooupload файлов учетная запись tooa хранилища Озера данных.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Hello SDK поддерживает рекурсивное отправка и загрузка между путь локального файла и путь к файлу хранилища Озера данных.    

## <a name="get-file-or-directory-info"></a>Получение сведений о файле или каталоге
Привет, в следующем фрагменте кода показан `GetItemInfo` метод, можно использовать tooretrieve сведения о файла или каталога доступен в хранилище Озера данных.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Получение списка файлов или каталогов
Привет, в следующем фрагменте кода показан `ListItem` метод, который можно использовать toolist hello файлов и каталогов в учетной записи хранилища Озера данных.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Сцепление файлов
Привет, в следующем фрагменте кода показан `ConcatenateFiles` использовать файлы tooconcatenate метод.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Добавить файл tooa
Привет, в следующем фрагменте кода показан `AppendToFile` используемого метода добавления файла данных tooa уже хранится в хранилище Озера данных учетной записи.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Скачивание файла
Привет, в следующем фрагменте кода показан `DownloadFile` метод используется toodownload файл из учетной записи хранилища Озера данных.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Дальнейшие действия
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store .NET Reference (Справочник по пакету SDK .NET для Data Lake Store)](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST Reference (Справочник по REST для Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
