---
title: "Подключение к локальной системе SAP в Azure Logic Apps | Документация Майкрософт"
description: "Использование локального шлюза данных для подключения к локальной системе SAP в рабочем процессе приложения логики"
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
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="0f765-103">Подключение к локальной системе SAP из приложения логики с помощью соединителя SAP</span><span class="sxs-lookup"><span data-stu-id="0f765-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="0f765-104">Локальный шлюз данных позволяет управлять данными и безопасно обращаться к ресурсам, расположенным в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="0f765-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="0f765-105">В этом разделе показано, как приложения логики могут подключаться к локальной системе SAP.</span><span class="sxs-lookup"><span data-stu-id="0f765-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="0f765-106">В этом примере приложение логики запрашивает IDOC по протоколу HTTP и отправляет ответ обратно.</span><span class="sxs-lookup"><span data-stu-id="0f765-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="0f765-107">Текущие ограничения:</span><span class="sxs-lookup"><span data-stu-id="0f765-107">Current limitations:</span></span> 
> - <span data-ttu-id="0f765-108">Время ожидания приложения логики истекает, если все действия, необходимые для ответа, не завершаются в течение [времени ожидания запроса](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="0f765-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="0f765-109">В этом сценарии запросы могут быть заблокированы.</span><span class="sxs-lookup"><span data-stu-id="0f765-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="0f765-110">Средство выбора файлов не отображает все доступные поля.</span><span class="sxs-lookup"><span data-stu-id="0f765-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="0f765-111">В этом случае пути можно добавить вручную.</span><span class="sxs-lookup"><span data-stu-id="0f765-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f765-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0f765-112">Prerequisites</span></span>

- <span data-ttu-id="0f765-113">Установите и настройте последнюю версию [локального шлюза данных](https://www.microsoft.com/download/details.aspx?id=53127) или версию не ниже 1.15.6150.1.</span><span class="sxs-lookup"><span data-stu-id="0f765-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="0f765-114">Инструкция см. в статье [Подключение к локальному шлюзу данных для приложений логики](http://aka.ms/logicapps-gateway).</span><span class="sxs-lookup"><span data-stu-id="0f765-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="0f765-115">Шлюз нужно установить на локальном компьютере, прежде чем продолжать процесс.</span><span class="sxs-lookup"><span data-stu-id="0f765-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="0f765-116">Скачайте последнюю версию клиентской библиотеки SAP и установите ее на компьютере, на котором установлен шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="0f765-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="0f765-117">Можно использовать любую из следующих версий SAP:</span><span class="sxs-lookup"><span data-stu-id="0f765-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="0f765-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="0f765-118">SAP Server</span></span>
        - <span data-ttu-id="0f765-119">Любой сервер SAP, поддерживающий соединитель .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="0f765-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="0f765-120">SAP Client</span><span class="sxs-lookup"><span data-stu-id="0f765-120">SAP Client</span></span>
        - <span data-ttu-id="0f765-121">Соединитель SAP .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="0f765-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="0f765-122">Добавление триггеров и действий для подключения к системе SAP</span><span class="sxs-lookup"><span data-stu-id="0f765-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="0f765-123">В соединителе SAP доступны действия, но не триггеры.</span><span class="sxs-lookup"><span data-stu-id="0f765-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="0f765-124">Таким образом, в начале рабочего процесса необходимо использовать другой триггер.</span><span class="sxs-lookup"><span data-stu-id="0f765-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="0f765-125">Добавьте триггер запроса и ответа, а затем выберите **Новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="0f765-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="0f765-126">Выберите **Добавить действие**, а затем выберите нужный соединитель SAP. Для этого введите `SAP` в поле поиска:</span><span class="sxs-lookup"><span data-stu-id="0f765-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Выберите сервер приложений SAP или сервер сообщений SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="0f765-128">Выберите [**сервер приложений SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) или [**сервер сообщений SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm) в зависимости от конфигурации SAP.</span><span class="sxs-lookup"><span data-stu-id="0f765-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="0f765-129">Если у вас нет существующего подключения, то вам будет предложено создать его.</span><span class="sxs-lookup"><span data-stu-id="0f765-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="0f765-130">Выберите **подключение через локальный шлюз данных** и введите сведения о системе SAP:</span><span class="sxs-lookup"><span data-stu-id="0f765-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Добавление строки подключения к SAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="0f765-132">В разделе **Шлюз** выберите существующий шлюз или, чтобы установить новый шлюз, выберите **Установить шлюз**.</span><span class="sxs-lookup"><span data-stu-id="0f765-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Установка нового шлюза](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="0f765-134">Введите все нужные сведения и нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f765-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="0f765-135">Logic Apps настраивает и проверяет подключение, гарантируя, что оно работает правильно.</span><span class="sxs-lookup"><span data-stu-id="0f765-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="0f765-136">Введите имя для подключения SAP.</span><span class="sxs-lookup"><span data-stu-id="0f765-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="0f765-137">Теперь вам будут доступны параметры SAP.</span><span class="sxs-lookup"><span data-stu-id="0f765-137">The different SAP options are now available.</span></span> <span data-ttu-id="0f765-138">Чтобы найти категорию IDOC, выберите ее в списке.</span><span class="sxs-lookup"><span data-stu-id="0f765-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="0f765-139">Также можно вручную ввести путь и выбрать ответ HTTP в поле **body** (текст):</span><span class="sxs-lookup"><span data-stu-id="0f765-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![Действие SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="0f765-141">Добавьте действие по созданию **HTTP-ответа**.</span><span class="sxs-lookup"><span data-stu-id="0f765-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="0f765-142">Сообщение ответа должно передавать выходные данные SAP.</span><span class="sxs-lookup"><span data-stu-id="0f765-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="0f765-143">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="0f765-143">Save your logic app.</span></span> <span data-ttu-id="0f765-144">Проверьте его, отправив IDOC с помощью URL-адреса триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f765-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="0f765-145">После отправки IDOC дождитесь ответа от приложения логики:</span><span class="sxs-lookup"><span data-stu-id="0f765-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="0f765-146">Узнайте о возможностях [мониторинга приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="0f765-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="0f765-147">Теперь соединитель SAP добавлен в приложение логики, и вы можете ознакомиться с другими функциями.</span><span class="sxs-lookup"><span data-stu-id="0f765-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="0f765-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="0f765-148">BAPI</span></span>
- <span data-ttu-id="0f765-149">RFC</span><span class="sxs-lookup"><span data-stu-id="0f765-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="0f765-150">Получение справки</span><span class="sxs-lookup"><span data-stu-id="0f765-150">Get help</span></span>

<span data-ttu-id="0f765-151">Чтобы задать вопросы, помочь другим пользователям и узнать, что делают другие пользователи, посетите [форум по Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0f765-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="0f765-152">Чтобы улучшить Azure Logic Apps и соединители, голосуйте за идеи или предлагайте собственные на [сайте обратной связи Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0f765-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f765-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f765-153">Next steps</span></span>

- <span data-ttu-id="0f765-154">Проверка, преобразование и другие функции в стиле BizTalk для [пакета интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f765-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="0f765-155">[Подключение к локальным данным](../logic-apps/logic-apps-gateway-connection.md) из приложений логики</span><span class="sxs-lookup"><span data-stu-id="0f765-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
