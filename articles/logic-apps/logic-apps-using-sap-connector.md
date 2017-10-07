---
title: "aaaConnect tooan локальной системы SAP в Azure Logic Apps | Документы Microsoft"
description: "Подключение tooan в локальной системе SAP из рабочего процесса логику приложения через hello локального шлюза данных"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="a25a9-103">Подключение из логики приложений с помощью соединителя SAP hello tooan в локальной системе SAP</span><span class="sxs-lookup"><span data-stu-id="a25a9-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="a25a9-104">Hello локального шлюза данных позволяет вам toomanage данных и безопасный доступ к ресурсам, которые являются локальными.</span><span class="sxs-lookup"><span data-stu-id="a25a9-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="a25a9-105">В этом разделе показывает способ подключения логики приложения tooan на локальной системе SAP.</span><span class="sxs-lookup"><span data-stu-id="a25a9-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="a25a9-106">В этом примере логика приложения запрашивает IDOC по протоколу HTTP и отправляет ответ hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="a25a9-107">Текущие ограничения:</span><span class="sxs-lookup"><span data-stu-id="a25a9-107">Current limitations:</span></span> 
> - <span data-ttu-id="a25a9-108">Приложения логики времени ожидания, если все действия, необходимые для ответа hello не завершается в течение hello [предельное время ожидания запроса](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="a25a9-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="a25a9-109">В этом сценарии запросы могут быть заблокированы.</span><span class="sxs-lookup"><span data-stu-id="a25a9-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="a25a9-110">Средство выбора файлов Hello не отображает все доступные поля hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="a25a9-111">В этом случае пути можно добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="a25a9-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a25a9-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a25a9-112">Prerequisites</span></span>

- <span data-ttu-id="a25a9-113">Установка и настройка hello последней [локального шлюза данных](https://www.microsoft.com/download/details.aspx?id=53127) версии 1.15.6150.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a25a9-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="a25a9-114">[Как tooconnect toohello локальный шлюз данных в приложении логику](http://aka.ms/logicapps-gateway) списки hello действия.</span><span class="sxs-lookup"><span data-stu-id="a25a9-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="a25a9-115">шлюз Hello должны устанавливаться на локальном компьютере, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="a25a9-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="a25a9-116">Загрузки и установки hello последнюю SAP клиентскую библиотеку на hello же компьютер, где установлен шлюз данных hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="a25a9-117">Выполните одно из следующих версий SAP hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="a25a9-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="a25a9-118">SAP Server</span></span>
        - <span data-ttu-id="a25a9-119">Любой сервер SAP, поддержка hello соединитель .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="a25a9-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="a25a9-120">SAP Client</span><span class="sxs-lookup"><span data-stu-id="a25a9-120">SAP Client</span></span>
        - <span data-ttu-id="a25a9-121">Соединитель SAP .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="a25a9-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="a25a9-122">Добавление триггеров и действий для подключения системы SAP tooyour</span><span class="sxs-lookup"><span data-stu-id="a25a9-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="a25a9-123">Соединитель SAP Hello имеет действия, но не триггеры.</span><span class="sxs-lookup"><span data-stu-id="a25a9-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="a25a9-124">Таким образом у нас есть toouse срабатывание другого триггера в начале hello hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="a25a9-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="a25a9-125">Добавить триггер hello запросов и ответов, а затем выберите **новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="a25a9-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="a25a9-126">Выберите **добавить действие**, а затем выберите соединитель SAP hello, введя `SAP` в поле поиска hello:</span><span class="sxs-lookup"><span data-stu-id="a25a9-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Выберите сервер приложений SAP или сервер сообщений SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="a25a9-128">Выберите [**сервер приложений SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) или [**сервер сообщений SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm) в зависимости от конфигурации SAP.</span><span class="sxs-lookup"><span data-stu-id="a25a9-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="a25a9-129">Если у вас нет существующего подключения, не запрошенные toocreate один.</span><span class="sxs-lookup"><span data-stu-id="a25a9-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="a25a9-130">Выберите **подключиться через локальный шлюз данных**и введите сведения о hello для вашей системы SAP:</span><span class="sxs-lookup"><span data-stu-id="a25a9-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Добавить tooSAP строки подключения](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="a25a9-132">В разделе **шлюза**выберите существующий шлюз или tooinstall новый шлюз, выберите **установить шлюз**.</span><span class="sxs-lookup"><span data-stu-id="a25a9-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Установка нового шлюза](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="a25a9-134">После ввода всех сведений о hello выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="a25a9-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="a25a9-135">Логика приложения настраивает и проверяет hello подключения, убедившись, что hello подключение работает правильно.</span><span class="sxs-lookup"><span data-stu-id="a25a9-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="a25a9-136">Введите имя для подключения SAP.</span><span class="sxs-lookup"><span data-stu-id="a25a9-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="a25a9-137">Теперь доступны различные варианты SAP Hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-137">hello different SAP options are now available.</span></span> <span data-ttu-id="a25a9-138">toofind категории IDOC, выберите из списка hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="a25a9-139">Или вручную ввести путь hello и выберите hello HTTP-ответ в hello **текст** поля:</span><span class="sxs-lookup"><span data-stu-id="a25a9-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Действие SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="a25a9-141">Добавить действие hello для создания **HTTP-ответа**.</span><span class="sxs-lookup"><span data-stu-id="a25a9-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="a25a9-142">приветственное сообщение ответа должно быть из выходных данных SAP hello.</span><span class="sxs-lookup"><span data-stu-id="a25a9-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="a25a9-143">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a25a9-143">Save your logic app.</span></span> <span data-ttu-id="a25a9-144">Протестируйте его путем отправки IDOC через URL-адрес триггера hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="a25a9-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="a25a9-145">После отправки IDOC приветствия ожидание hello ответа от приложения hello логики:</span><span class="sxs-lookup"><span data-stu-id="a25a9-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="a25a9-146">Узнать о возможностях слишком[Отслеживайте свои приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a25a9-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="a25a9-147">Теперь, когда соединитель SAP hello добавляется tooyour логику приложения, отправной точкой для других функций:</span><span class="sxs-lookup"><span data-stu-id="a25a9-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="a25a9-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="a25a9-148">BAPI</span></span>
- <span data-ttu-id="a25a9-149">RFC</span><span class="sxs-lookup"><span data-stu-id="a25a9-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="a25a9-150">Получение справки</span><span class="sxs-lookup"><span data-stu-id="a25a9-150">Get help</span></span>

<span data-ttu-id="a25a9-151">вопросы tooask ответить на вопросы и узнайте, какие другие логику приложения Azure пользователи делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a25a9-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a25a9-152">toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a25a9-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a25a9-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a25a9-153">Next steps</span></span>

- <span data-ttu-id="a25a9-154">Узнайте, как toovalidate, преобразования и других функций, аналогичных BizTalk в hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a25a9-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="a25a9-155">[Подключение к данным локальной tooon](../logic-apps/logic-apps-gateway-connection.md) из приложений логики</span><span class="sxs-lookup"><span data-stu-id="a25a9-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
