---
title: "Соединитель aaaDropbox в приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите tooDropbox toomanage файлов. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="8ecc7-105">Приступая к работе с Dropbox соединитель hello</span><span class="sxs-lookup"><span data-stu-id="8ecc7-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="8ecc7-106">Подключите tooDropbox toomanage файлов.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="8ecc7-107">Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="8ecc7-108">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="8ecc7-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8ecc7-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="8ecc7-110">Подключение tooDropbox</span><span class="sxs-lookup"><span data-stu-id="8ecc7-110">Connect tooDropbox</span></span>
<span data-ttu-id="8ecc7-111">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="8ecc7-112">Таким образом вы установите соединение между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="8ecc7-113">Например, в порядке tooconnect tooDropbox, необходимо сначала Dropbox *соединения*.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="8ecc7-114">toocreate соединение, потребовалось бы hello tooprovide учетные данные, обычно используемые службы hello tooaccess которых надо tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="8ecc7-115">Таким образом в примере hello общего банка данных, потребовалось бы tooyour hello учетные данные учетной записи общего банка данных в порядке toocreate hello соединения tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> <span data-ttu-id="8ecc7-116">Дополнительные сведения о подключениях см. [здесь]().</span><span class="sxs-lookup"><span data-stu-id="8ecc7-116">[Learn more about connections]()</span></span>

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="8ecc7-117">Создание tooDropbox подключения</span><span class="sxs-lookup"><span data-stu-id="8ecc7-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="8ecc7-118">Использование триггера Dropbox</span><span class="sxs-lookup"><span data-stu-id="8ecc7-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="8ecc7-119">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="8ecc7-120">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8ecc7-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="8ecc7-121">В этом примере мы будем использовать hello **при создании файла** триггера.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="8ecc7-122">В случае триггера назовем hello **получить содержимое файла, используя путь** действие общего банка данных.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="8ecc7-123">Введите *dropbox* в поле поиска hello в конструкторе логики приложения hello, затем выберите hello **Dropbox - при создании файла** триггера.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="8ecc7-124">Выберите папку hello, в котором tootrack создания файла.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="8ecc7-125">Выберите... (определенное в поле hello красный) и папки toohello обзора нужно входных tooselect для триггера hello.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="8ecc7-126">Использование действия Dropbox</span><span class="sxs-lookup"><span data-stu-id="8ecc7-126">Use a Dropbox action</span></span>
<span data-ttu-id="8ecc7-127">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8ecc7-128">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8ecc7-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="8ecc7-129">Теперь, когда hello триггер был добавлен, выполните эти действия tooadd действия, которые помогут начать hello новый файл содержимого.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="8ecc7-130">Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при создании нового файла.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="8ecc7-131">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-131">Select **Add an action**.</span></span> <span data-ttu-id="8ecc7-132">Открывает окна поиска hello поиска для любого действия вы хотели бы tootake.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="8ecc7-133">Введите *dropbox* toosearch для tooDropbox связанные действия.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="8ecc7-134">Выберите **Dropbox - получение содержимого файла, используя путь** hello tootake действие создания нового файла в hello выбираются общего банка данных.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="8ecc7-135">Открывает блок управления действие Hello.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-135">hello action control block opens.</span></span> <span data-ttu-id="8ecc7-136">Вам будет запрашиваемые tooauthorize вашей tooaccess логику приложения, учетной записи Dropbox, если вы еще не сделали это.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="8ecc7-137">Выберите... (расположенный в правой стороне hello hello **путь к файлу** управления) и найдите путь к файлу toohello хотелось бы toouse.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="8ecc7-138">Также можно использовать hello **путь к файлу** маркера toospeed вверх на создание логики приложения.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="8ecc7-139">Сохраните данные и создать новый файл в общий банк данных tooactivate рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="8ecc7-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="8ecc7-140">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="8ecc7-140">Connector-specific details</span></span>

<span data-ttu-id="8ecc7-141">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="8ecc7-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8ecc7-142">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="8ecc7-142">More connectors</span></span>
<span data-ttu-id="8ecc7-143">Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8ecc7-143">Go back toohello [APIs list](apis-list.md).</span></span>
