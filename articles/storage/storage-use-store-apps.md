---
title: "Использование службы хранилища Azure в приложениях Магазина Windows | Документация Майкрософт"
description: "Узнайте, как создать приложение магазина Windows, которое использует BLOB-объекты, очереди, таблицы или хранилище файлов Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="92245-103">Использование службы хранилища Azure в приложениях Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="92245-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="92245-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="92245-104">Overview</span></span>
<span data-ttu-id="92245-105">В этом руководстве показано, как начать разработку приложения Магазина Windows, использующего хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="92245-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="92245-106">Скачивание необходимых средств</span><span class="sxs-lookup"><span data-stu-id="92245-106">Download required tools</span></span>
* <span data-ttu-id="92245-107">[Visual Studio](https://www.visualstudio.com/downloads/) упрощает процесс сборки, отладки, локализации, упаковки и развертывания приложений Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="92245-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="92245-108">Требуется Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="92245-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="92245-109">[Клиентская библиотека хранилища Microsoft Azure](https://www.nuget.org/packages/WindowsAzure.Storage) предоставляет библиотеку классов среды выполнения Windows для работы со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="92245-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="92245-110">[Инструменты служб данных WCF для приложений Магазина Windows](http://www.microsoft.com/download/details.aspx?id=30714) расширяют возможности добавления ссылки на службу за счет поддержки OData на стороне клиента для приложений Магазина Windows в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92245-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="92245-111">Разработка приложений</span><span class="sxs-lookup"><span data-stu-id="92245-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="92245-112">Подготовка</span><span class="sxs-lookup"><span data-stu-id="92245-112">Getting ready</span></span>
<span data-ttu-id="92245-113">Создайте новый проект приложения Магазина Windows в Visual Studio 2012 или более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="92245-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="92245-115">Затем добавьте ссылку на клиентскую библиотеку службы хранилища Azure. Для этого щелкните правой кнопкой мыши элемент **Ссылки**, выберите пункт **Добавить ссылку** и перейдите к скачанной клиентской библиотеке хранилища для среды выполнения Windows:</span><span class="sxs-lookup"><span data-stu-id="92245-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="92245-117">Использование библиотеки со службами BLOB-объектов и очередей</span><span class="sxs-lookup"><span data-stu-id="92245-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="92245-118">На этом этапе приложение готово к вызову служб BLOB-объектов и очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="92245-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="92245-119">Добавьте следующие операторы **using** , чтобы можно было напрямую ссылаться на типы хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="92245-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="92245-120">Далее, добавьте кнопку на страницу.</span><span class="sxs-lookup"><span data-stu-id="92245-120">Next, add a button to your page.</span></span> <span data-ttu-id="92245-121">Добавьте следующий код к ее событию **Click** и измените метод обработчика событий с помощью [ключевого слова async](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="92245-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="92245-122">В этом коде предполагается, что у вас есть две строковые переменные *accountName* и *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="92245-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="92245-123">Они представляют собой имя вашей учетной записи хранения и связанный ней ключ.</span><span class="sxs-lookup"><span data-stu-id="92245-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="92245-124">Создайте и запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="92245-124">Build and run the application.</span></span> <span data-ttu-id="92245-125">Нажав кнопку, вы сможете проверить свою учетную запись на наличие контейнера с именем *container1* и создать его в случае отсутствия.</span><span class="sxs-lookup"><span data-stu-id="92245-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="92245-126">Использование библиотеки со службой таблиц</span><span class="sxs-lookup"><span data-stu-id="92245-126">Using the library with the Table service</span></span>
<span data-ttu-id="92245-127">Типы, используемые для связи со службой таблиц Azure, зависят от служб данных WCF для библиотеки приложений Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="92245-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="92245-128">Добавьте ссылку на необходимые библиотеки WCF с помощью консоли диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="92245-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="92245-130">Используйте следующую команду для направление диспетчера пакетов к определенному месту в вашем компьютере:</span><span class="sxs-lookup"><span data-stu-id="92245-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="92245-131">Эта команда автоматически добавляет все необходимые ссылки на проект.</span><span class="sxs-lookup"><span data-stu-id="92245-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="92245-132">Кроме того, вы можете добавить папку NuGet служб данных WCF на локальном компьютере в список источников пакетов, а затем добавить ссылку через пользовательский интерфейс, как описано в разделе [Управление пакетами NuGet с помощью диалогового окна](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="92245-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="92245-133">После создания ссылки на NuGet-пакет службы данных WCF измените код события **Click** вашей кнопки:</span><span class="sxs-lookup"><span data-stu-id="92245-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="92245-134">Этот код позволяет проверить учетную запись на наличие таблицы с именем *table1* и создать ее в случае отсутствия.</span><span class="sxs-lookup"><span data-stu-id="92245-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="92245-135">Вы также можете добавить ссылку на библиотеку Microsoft.WindowsAzure.Storage.Table.dll, которая находится в том же скачанном пакете.</span><span class="sxs-lookup"><span data-stu-id="92245-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="92245-136">Она содержит дополнительные возможности, такие как сериализация на основе отражения и общие запросы.</span><span class="sxs-lookup"><span data-stu-id="92245-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="92245-137">Обратите внимание, что эта библиотека не поддерживает JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92245-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
