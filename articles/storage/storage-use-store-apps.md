---
title: "aaaUse хранилища Azure в приложениях для магазина Windows | Документы Microsoft"
description: "Узнайте, как toocreate для магазина Windows приложение, которое использует хранилище больших двоичных объектов Azure, очереди, таблицы или файла."
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
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="8c745-103">Как toouse хранилища Azure в приложениях для магазина Windows</span><span class="sxs-lookup"><span data-stu-id="8c745-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="8c745-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8c745-104">Overview</span></span>
<span data-ttu-id="8c745-105">В этом руководстве показано, как tooget работу с разработкой приложения магазина Windows, которое использует хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="8c745-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="8c745-106">Скачивание необходимых средств</span><span class="sxs-lookup"><span data-stu-id="8c745-106">Download required tools</span></span>
* <span data-ttu-id="8c745-107">[Visual Studio](https://www.visualstudio.com/downloads/) делает его легко toobuild отладки, локализации, упаковки и развертывания приложений для магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="8c745-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="8c745-108">Требуется Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8c745-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="8c745-109">Hello [клиентская библиотека хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage) предоставляет библиотеки классов среды выполнения Windows для работы со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8c745-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="8c745-110">[WCF данных службы средств для приложений магазина Windows](http://www.microsoft.com/download/details.aspx?id=30714) расширяет возможности добавления ссылки на службу hello с поддержкой OData клиентских приложений для магазина Windows в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c745-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="8c745-111">Разработка приложений</span><span class="sxs-lookup"><span data-stu-id="8c745-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="8c745-112">Подготовка</span><span class="sxs-lookup"><span data-stu-id="8c745-112">Getting ready</span></span>
<span data-ttu-id="8c745-113">Создайте новый проект приложения Магазина Windows в Visual Studio 2012 или более поздней версии:</span><span class="sxs-lookup"><span data-stu-id="8c745-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="8c745-115">Добавьте ссылку toohello клиентская библиотека хранилища Azure, щелкнув правой кнопкой мыши **ссылки**, а затем выбрав **добавить ссылку на**и просмотре toohello хранилища клиента библиотеки для среды выполнения Windows, которые загрузить:</span><span class="sxs-lookup"><span data-stu-id="8c745-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="8c745-117">С помощью библиотеки hello с hello больших двоичных объектов и службы очередей</span><span class="sxs-lookup"><span data-stu-id="8c745-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="8c745-118">На этом этапе приложение будет готово toocall hello больших двоичных объектов и очередей служб.</span><span class="sxs-lookup"><span data-stu-id="8c745-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="8c745-119">Добавьте следующее hello **с помощью** инструкции, чтобы может непосредственно ссылаться на типы хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="8c745-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="8c745-120">Добавьте кнопку tooyour страницы.</span><span class="sxs-lookup"><span data-stu-id="8c745-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="8c745-121">Добавьте следующий код tooits hello **щелкните** событий и измените метод обработчика событий с помощью hello [async-ключевое слово](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="8c745-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="8c745-122">В этом коде предполагается, что у вас есть две строковые переменные *accountName* и *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="8c745-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="8c745-123">Они представляют Привет имя вашей учетной записи и hello ключ учетной записи хранилища, связанный с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8c745-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="8c745-124">Постройте и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="8c745-124">Build and run hello application.</span></span> <span data-ttu-id="8c745-125">Щелкнув кнопку hello проверит ли контейнер с именем *container1* существует в вашей учетной записи, а затем создать его, если это не так.</span><span class="sxs-lookup"><span data-stu-id="8c745-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="8c745-126">Использование библиотеки hello с hello службы таблиц</span><span class="sxs-lookup"><span data-stu-id="8c745-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="8c745-127">Типы, используемые toocommunicate со службой таблиц Azure hello зависят от службы данных WCF для библиотеки приложения для магазина Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8c745-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="8c745-128">Далее следует добавьте toohello ссылка необходимые библиотеки WCF с помощью hello консоль диспетчера пакетов:</span><span class="sxs-lookup"><span data-stu-id="8c745-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="8c745-130">Используйте hello следующая команда toopoint toohello диспетчера пакетов расположение на компьютере:</span><span class="sxs-lookup"><span data-stu-id="8c745-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="8c745-131">Эта команда автоматически добавит все необходимые ссылки tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="8c745-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="8c745-132">Если вы не хотите toouse hello консоль диспетчера пакетов, можно добавить hello WCF Data Services NuGet папку на локальном компьютере toohello список источников пакетов и добавить ссылку hello через hello пользовательского интерфейса, как описано в [управление NuGet пакетов с помощью диалоговое окно приветствия](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="8c745-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="8c745-133">При ссылке на пакет WCF Data Services NuGet hello изменение кода hello в своей кнопки **щелкните** событий:</span><span class="sxs-lookup"><span data-stu-id="8c745-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="8c745-134">Этот код позволяет проверить учетную запись на наличие таблицы с именем *table1* и создать ее в случае отсутствия.</span><span class="sxs-lookup"><span data-stu-id="8c745-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="8c745-135">Также можно добавить ссылку tooMicrosoft.WindowsAzure.Storage.Table.dll, доступного в hello же пакет, загруженный.</span><span class="sxs-lookup"><span data-stu-id="8c745-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="8c745-136">Она содержит дополнительные возможности, такие как сериализация на основе отражения и общие запросы.</span><span class="sxs-lookup"><span data-stu-id="8c745-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="8c745-137">Обратите внимание, что эта библиотека не поддерживает JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8c745-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
