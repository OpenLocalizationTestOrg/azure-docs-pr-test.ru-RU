---
title: "Как использовать соединитель SFTP в приложениях логики | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключитесь к API SFTP, чтобы отправлять и получать файлы. Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы."
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
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="128de-105">Начало работы с соединителем SFTP</span><span class="sxs-lookup"><span data-stu-id="128de-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="128de-106">Используйте соединитель SFTP, чтобы получить доступ к учетной записи SFTP для отправки и получения файлов.</span><span class="sxs-lookup"><span data-stu-id="128de-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="128de-107">Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы.</span><span class="sxs-lookup"><span data-stu-id="128de-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="128de-108">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="128de-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="128de-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="128de-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="128de-110">Подключение к SFTP</span><span class="sxs-lookup"><span data-stu-id="128de-110">Connect to SFTP</span></span>
<span data-ttu-id="128de-111">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="128de-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="128de-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="128de-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="128de-113">Создание подключения к SFTP</span><span class="sxs-lookup"><span data-stu-id="128de-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="128de-114">Использование триггера SFTP</span><span class="sxs-lookup"><span data-stu-id="128de-114">Use an SFTP trigger</span></span>
<span data-ttu-id="128de-115">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="128de-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="128de-116">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="128de-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="128de-117">В этом примере триггер **SFTP - When a file is added or modified** (SFTP — при добавлении или изменении файла) используется для запуска рабочего процесса приложения логики при добавлении или изменении файла на SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="128de-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="128de-118">Также вы добавите условие, которое проверяет содержимое нового или измененного файла, и принимает решение извлечь файл, если содержимое файла указывает, что он должен быть извлечен перед использованием содержимого.</span><span class="sxs-lookup"><span data-stu-id="128de-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="128de-119">Наконец, вы добавите действие, которое извлекает содержимое файла и помещает извлеченное содержимое в папку на SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="128de-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="128de-120">В контексте предприятия можно использовать этот триггер, чтобы отслеживать в папке SFTP новые файлы, представляющие заказы клиентов.</span><span class="sxs-lookup"><span data-stu-id="128de-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="128de-121">Также вы можете использовать действие соединителя SFTP **Получить содержимое файла**, чтобы получить содержимое заказа для дальнейшей обработки и хранения в базе данных заказов.</span><span class="sxs-lookup"><span data-stu-id="128de-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="128de-122">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="128de-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="128de-123">Использование действия SFTP</span><span class="sxs-lookup"><span data-stu-id="128de-123">Use an SFTP action</span></span>
<span data-ttu-id="128de-124">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="128de-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="128de-125">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="128de-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="128de-126">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="128de-126">Connector-specific details</span></span>

<span data-ttu-id="128de-127">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="128de-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="128de-128">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="128de-128">More connectors</span></span>
<span data-ttu-id="128de-129">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="128de-129">Go back to the [APIs list](apis-list.md).</span></span>