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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Как toouse хранилища Azure в приложениях для магазина Windows
## <a name="overview"></a>Обзор
В этом руководстве показано, как tooget работу с разработкой приложения магазина Windows, которое использует хранилище Azure.

## <a name="download-required-tools"></a>Скачивание необходимых средств
* [Visual Studio](https://www.visualstudio.com/downloads/) делает его легко toobuild отладки, локализации, упаковки и развертывания приложений для магазина Windows. Требуется Visual Studio 2012 или более поздней версии.
* Hello [клиентская библиотека хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage) предоставляет библиотеки классов среды выполнения Windows для работы со службой хранилища Azure.
* [WCF данных службы средств для приложений магазина Windows](http://www.microsoft.com/download/details.aspx?id=30714) расширяет возможности добавления ссылки на службу hello с поддержкой OData клиентских приложений для магазина Windows в Visual Studio.

## <a name="develop-apps"></a>Разработка приложений
### <a name="getting-ready"></a>Подготовка
Создайте новый проект приложения Магазина Windows в Visual Studio 2012 или более поздней версии:

![store-apps-storage-vs-project][store-apps-storage-vs-project]

Добавьте ссылку toohello клиентская библиотека хранилища Azure, щелкнув правой кнопкой мыши **ссылки**, а затем выбрав **добавить ссылку на**и просмотре toohello хранилища клиента библиотеки для среды выполнения Windows, которые загрузить:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>С помощью библиотеки hello с hello больших двоичных объектов и службы очередей
На этом этапе приложение будет готово toocall hello больших двоичных объектов и очередей служб. Добавьте следующее hello **с помощью** инструкции, чтобы может непосредственно ссылаться на типы хранилища Azure:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Добавьте кнопку tooyour страницы. Добавьте следующий код tooits hello **щелкните** событий и измените метод обработчика событий с помощью hello [async-ключевое слово](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

В этом коде предполагается, что у вас есть две строковые переменные *accountName* и *accountKey*. Они представляют Привет имя вашей учетной записи и hello ключ учетной записи хранилища, связанный с этой учетной записи.

Постройте и запустите приложение hello. Щелкнув кнопку hello проверит ли контейнер с именем *container1* существует в вашей учетной записи, а затем создать его, если это не так.

### <a name="using-hello-library-with-hello-table-service"></a>Использование библиотеки hello с hello службы таблиц
Типы, используемые toocommunicate со службой таблиц Azure hello зависят от службы данных WCF для библиотеки приложения для магазина Windows hello. Далее следует добавьте toohello ссылка необходимые библиотеки WCF с помощью hello консоль диспетчера пакетов:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

Используйте hello следующая команда toopoint toohello диспетчера пакетов расположение на компьютере:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Эта команда автоматически добавит все необходимые ссылки tooyour проекта. Если вы не хотите toouse hello консоль диспетчера пакетов, можно добавить hello WCF Data Services NuGet папку на локальном компьютере toohello список источников пакетов и добавить ссылку hello через hello пользовательского интерфейса, как описано в [управление NuGet пакетов с помощью диалоговое окно приветствия](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

При ссылке на пакет WCF Data Services NuGet hello изменение кода hello в своей кнопки **щелкните** событий:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Этот код позволяет проверить учетную запись на наличие таблицы с именем *table1* и создать ее в случае отсутствия.

Также можно добавить ссылку tooMicrosoft.WindowsAzure.Storage.Table.dll, доступного в hello же пакет, загруженный. Она содержит дополнительные возможности, такие как сериализация на основе отражения и общие запросы. Обратите внимание, что эта библиотека не поддерживает JavaScript.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
