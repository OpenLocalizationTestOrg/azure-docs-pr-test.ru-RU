---
title: "aaaLearn как toouse hello соединителя SFTP в приложениях для логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите toosend tooSFTP API и получать файлы. Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="7ffb9-105">Начало работы с соединителем SFTP hello</span><span class="sxs-lookup"><span data-stu-id="7ffb9-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="7ffb9-106">Используйте hello SFTP соединитель tooaccess toosend SFTP учетной записи и получать файлы.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="7ffb9-107">Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="7ffb9-108">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="7ffb9-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7ffb9-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="7ffb9-110">Подключение tooSFTP</span><span class="sxs-lookup"><span data-stu-id="7ffb9-110">Connect tooSFTP</span></span>
<span data-ttu-id="7ffb9-111">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="7ffb9-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="7ffb9-113">Создание tooSFTP подключения</span><span class="sxs-lookup"><span data-stu-id="7ffb9-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="7ffb9-114">Использование триггера SFTP</span><span class="sxs-lookup"><span data-stu-id="7ffb9-114">Use an SFTP trigger</span></span>
<span data-ttu-id="7ffb9-115">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="7ffb9-116">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7ffb9-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="7ffb9-117">В этом примере hello **SFTP - при добавлении или изменении файла** триггер является tooinitiate используется логика приложения рабочего процесса, при добавлении файла, или изменить на SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="7ffb9-118">Можно также добавить условие, которое проверяет содержимое hello hello нового или измененного файла и устанавливает файл hello tooextract принятия решений, если его содержимое указывает, должно быть извлечено перед использованием hello содержимое.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="7ffb9-119">Наконец добавьте действие tooextract hello содержимое файла и поместить в папку на SFTP-сервере hello hello извлечь содержимое.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="7ffb9-120">В пример enterprise можно использовать этот триггер toomonitor папки SFTP для новых файлов, которые представляют заказы клиента.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="7ffb9-121">Затем можно использовать действие соединителя SFTP, таких как **получение содержимого файла**, содержимое hello tooget hello заказа для дальнейшей обработки и хранения в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="7ffb9-122">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="7ffb9-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="7ffb9-123">Использование действия SFTP</span><span class="sxs-lookup"><span data-stu-id="7ffb9-123">Use an SFTP action</span></span>
<span data-ttu-id="7ffb9-124">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="7ffb9-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="7ffb9-125">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7ffb9-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="7ffb9-126">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="7ffb9-126">Connector-specific details</span></span>

<span data-ttu-id="7ffb9-127">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="7ffb9-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7ffb9-128">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="7ffb9-128">More connectors</span></span>
<span data-ttu-id="7ffb9-129">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7ffb9-129">Go back toohello [APIs list](apis-list.md).</span></span>
