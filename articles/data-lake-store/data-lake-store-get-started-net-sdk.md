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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="e22a0-103">Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET</span><span class="sxs-lookup"><span data-stu-id="e22a0-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e22a0-104">Портал</span><span class="sxs-lookup"><span data-stu-id="e22a0-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="e22a0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e22a0-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="e22a0-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="e22a0-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="e22a0-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="e22a0-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="e22a0-108">REST API</span><span class="sxs-lookup"><span data-stu-id="e22a0-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="e22a0-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e22a0-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="e22a0-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="e22a0-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="e22a0-111">Python</span><span class="sxs-lookup"><span data-stu-id="e22a0-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="e22a0-112">Узнайте, как toouse hello [пакета SDK .NET хранилища Озера данных Azure](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform основных операций, таких как создание папок, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e22a0-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e22a0-113">Prerequisites</span></span>
* <span data-ttu-id="e22a0-114">**Visual Studio 2013, 2015 или 2017**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="e22a0-115">Приведенные ниже инструкции Hello использовать Visual Studio 2015 с обновлением 2.</span><span class="sxs-lookup"><span data-stu-id="e22a0-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="e22a0-116">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-116">**An Azure subscription**.</span></span> <span data-ttu-id="e22a0-117">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e22a0-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e22a0-118">**Учетная запись хранилища озера данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="e22a0-119">Дополнительные сведения о toocreate учетную запись, в разделе [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e22a0-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="e22a0-120">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="e22a0-121">Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e22a0-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="e22a0-122">Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="e22a0-123">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="e22a0-124">Создание приложения .NET</span><span class="sxs-lookup"><span data-stu-id="e22a0-124">Create a .NET application</span></span>
1. <span data-ttu-id="e22a0-125">Откройте Visual Studio и создайте консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="e22a0-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="e22a0-126">Из hello **файл** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="e22a0-127">Из **новый проект**введите или выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="e22a0-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="e22a0-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="e22a0-128">Property</span></span> | <span data-ttu-id="e22a0-129">Значение</span><span class="sxs-lookup"><span data-stu-id="e22a0-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e22a0-130">Категория</span><span class="sxs-lookup"><span data-stu-id="e22a0-130">Category</span></span> |<span data-ttu-id="e22a0-131">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="e22a0-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="e22a0-132">Шаблон</span><span class="sxs-lookup"><span data-stu-id="e22a0-132">Template</span></span> |<span data-ttu-id="e22a0-133">Консольное приложение</span><span class="sxs-lookup"><span data-stu-id="e22a0-133">Console Application</span></span> |
   | <span data-ttu-id="e22a0-134">Имя</span><span class="sxs-lookup"><span data-stu-id="e22a0-134">Name</span></span> |<span data-ttu-id="e22a0-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="e22a0-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="e22a0-136">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="e22a0-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="e22a0-137">Добавьте проект tooyour пакеты Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="e22a0-138">Щелкните правой кнопкой мыши имя проекта hello в обозревателе решений hello и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e22a0-139">В hello **диспетчера пакетов Nuget** , убедитесь, что **источник пакета** задано слишком**nuget.org** и что **включить предварительный выпуск** флажок выбран.</span><span class="sxs-lookup"><span data-stu-id="e22a0-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="e22a0-140">Поиск и установка hello следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="e22a0-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="e22a0-141">`Microsoft.Azure.Management.DataLake.Store`. В этом руководстве используется предварительная версия 2.1.3.</span><span class="sxs-lookup"><span data-stu-id="e22a0-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="e22a0-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication`. В этом руководстве используется версия 2.2.12.</span><span class="sxs-lookup"><span data-stu-id="e22a0-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="e22a0-143">![Добавление источника Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Создание учетной записи Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="e22a0-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="e22a0-144">Закрыть hello **диспетчера пакетов Nuget**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="e22a0-145">Откройте **Program.cs**, удаление существующего кода hello и затем добавьте следующие инструкции tooadd ссылки toonamespaces hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="e22a0-146">Объявления переменных hello, как показано ниже и укажите значения hello для хранилища Озера данных имя и имя группы ресурсов hello, которая уже существует.</span><span class="sxs-lookup"><span data-stu-id="e22a0-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="e22a0-147">Кроме того убедитесь, что hello локальный путь и имя файла здесь должен существовать на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="e22a0-148">Добавьте следующий фрагмент кода после объявления пространств имен hello hello.</span><span class="sxs-lookup"><span data-stu-id="e22a0-148">Add hello following code snippet after hello namespace declarations.</span></span>

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

<span data-ttu-id="e22a0-149">В оставшихся разделах статьи hello hello вы увидите, как toouse hello доступные операции tooperform методы .NET, такие как проверку подлинности, передачу файла, и т. д.</span><span class="sxs-lookup"><span data-stu-id="e22a0-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="e22a0-150">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="e22a0-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="e22a0-151">При использовании проверки подлинности пользователя (рекомендуется для этого руководства)</span><span class="sxs-lookup"><span data-stu-id="e22a0-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="e22a0-152">Используется с существующие tooauthenticate собственное приложение Azure AD приложения **интерактивно**, который означает, будет предложено tooenter учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="e22a0-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="e22a0-153">Для удобства использования в приведенном ниже фрагменте hello использует значения по умолчанию для идентификатора клиента и URI, который будет работать с любой подписке Azure перенаправления.</span><span class="sxs-lookup"><span data-stu-id="e22a0-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="e22a0-154">toohelp быстрее завершить этот учебник, мы рекомендуем использовать этот подход.</span><span class="sxs-lookup"><span data-stu-id="e22a0-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="e22a0-155">В приведенном ниже фрагменте hello просто укажите hello значение свой идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="e22a0-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="e22a0-156">Можно получить с помощью hello инструкций, приведенных в [создать приложение Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="e22a0-157">Несколько вещей tooknow об этом примере, приведенном выше:</span><span class="sxs-lookup"><span data-stu-id="e22a0-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="e22a0-158">использует этот фрагмент toohelp ускорить hello учебник, в Azure AD и клиентского идентификатор, который доступен по умолчанию для всех подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="e22a0-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="e22a0-159">Таким образом, вы можете **использовать в приложении этот фрагмент в исходном виде**.</span><span class="sxs-lookup"><span data-stu-id="e22a0-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="e22a0-160">Тем не менее если требуется toouse ваш домен Azure AD, а код клиента приложения, необходимо создать собственное приложение Azure AD и затем используйте hello Azure AD идентификатор, идентификатор клиента, клиента и URI перенаправления для приложения hello вы создали.</span><span class="sxs-lookup"><span data-stu-id="e22a0-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="e22a0-161">Инструкции см. в статье [Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="e22a0-162">При использовании проверки подлинности через секрет клиента со взаимодействием между службами</span><span class="sxs-lookup"><span data-stu-id="e22a0-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="e22a0-163">Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения **не в интерактивном режиме**, с помощью секрет клиента hello / ключ для приложения / службы-участника.</span><span class="sxs-lookup"><span data-stu-id="e22a0-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="e22a0-164">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e22a0-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="e22a0-165">Инструкции по статье toocreate hello Azure AD веб-приложение и как tooretrieve hello идентификатор клиента и секрет клиента, необходимые в следующем фрагменте hello [создать приложение для проверки подлинности службы для службы Active Directory с данными Хранилище Озера](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="e22a0-166">При использовании проверки подлинности с помощью сертификата со взаимодействием между службами</span><span class="sxs-lookup"><span data-stu-id="e22a0-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="e22a0-167">Как третий вариант, hello следующий фрагмент кода может быть используется tooauthenticate приложения **не в интерактивном режиме**, с помощью hello сертификат для приложения Azure Active Directory / участника службы.</span><span class="sxs-lookup"><span data-stu-id="e22a0-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="e22a0-168">Примените этот фрагмент кода к существующему [приложению Azure AD с помощью сертификатов](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e22a0-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="e22a0-169">Создание клиентских объектов</span><span class="sxs-lookup"><span data-stu-id="e22a0-169">Create client objects</span></span>
<span data-ttu-id="e22a0-170">Hello следующий фрагмент кода создает учетную запись хранилища Озера данных hello и файловой системы объектов клиента, которые используются tooissue запросов toohello службой.</span><span class="sxs-lookup"><span data-stu-id="e22a0-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="e22a0-171">Получение списка всех учетных записей Data Lake Store в рамках подписки</span><span class="sxs-lookup"><span data-stu-id="e22a0-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="e22a0-172">Hello следующий фрагмент кода перечисляет все учетные записи хранилища Озера данных в рамках данной подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="e22a0-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="e22a0-173">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="e22a0-173">Create a directory</span></span>
<span data-ttu-id="e22a0-174">Привет, в следующем фрагменте кода показан `CreateDirectory` метода, которые можно использовать toocreate каталогу в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="e22a0-175">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="e22a0-175">Upload a file</span></span>
<span data-ttu-id="e22a0-176">Привет, в следующем фрагменте кода показан `UploadFile` метода, которые можно использовать tooupload файлов учетная запись tooa хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="e22a0-177">Hello SDK поддерживает рекурсивное отправка и загрузка между путь локального файла и путь к файлу хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="e22a0-178">Получение сведений о файле или каталоге</span><span class="sxs-lookup"><span data-stu-id="e22a0-178">Get file or directory info</span></span>
<span data-ttu-id="e22a0-179">Привет, в следующем фрагменте кода показан `GetItemInfo` метод, можно использовать tooretrieve сведения о файла или каталога доступен в хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="e22a0-180">Получение списка файлов или каталогов</span><span class="sxs-lookup"><span data-stu-id="e22a0-180">List file or directories</span></span>
<span data-ttu-id="e22a0-181">Привет, в следующем фрагменте кода показан `ListItem` метод, который можно использовать toolist hello файлов и каталогов в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="e22a0-182">Сцепление файлов</span><span class="sxs-lookup"><span data-stu-id="e22a0-182">Concatenate files</span></span>
<span data-ttu-id="e22a0-183">Привет, в следующем фрагменте кода показан `ConcatenateFiles` использовать файлы tooconcatenate метод.</span><span class="sxs-lookup"><span data-stu-id="e22a0-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="e22a0-184">Добавить файл tooa</span><span class="sxs-lookup"><span data-stu-id="e22a0-184">Append tooa file</span></span>
<span data-ttu-id="e22a0-185">Привет, в следующем фрагменте кода показан `AppendToFile` используемого метода добавления файла данных tooa уже хранится в хранилище Озера данных учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e22a0-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="e22a0-186">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="e22a0-186">Download a file</span></span>
<span data-ttu-id="e22a0-187">Привет, в следующем фрагменте кода показан `DownloadFile` метод используется toodownload файл из учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="e22a0-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="e22a0-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e22a0-188">Next steps</span></span>
* [<span data-ttu-id="e22a0-189">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="e22a0-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e22a0-190">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="e22a0-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e22a0-191">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="e22a0-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="e22a0-192">Data Lake Store .NET Reference (Справочник по пакету SDK .NET для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="e22a0-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="e22a0-193">Data Lake Store REST Reference (Справочник по REST для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="e22a0-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
