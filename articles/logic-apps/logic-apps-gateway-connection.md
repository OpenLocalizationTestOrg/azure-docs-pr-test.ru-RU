---
title: "Источники данных aaaAccess на локальном компьютере для приложения логики Azure | Документы Microsoft"
description: "Настройка hello локальный шлюз данных необходимо для доступа к источникам данных на локальном компьютере из приложений логики"
keywords: "доступ к данным, локальный, передача данных, шифрование, источники данных"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="352d4-104">Доступ к источникам данных на локальном компьютере из логики приложений с помощью hello локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="352d4-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="352d4-105">Источники данных tooaccess на локальном компьютере от логики приложений, настроить шлюз данных в локальной среде, можно использовать логику приложения с помощью поддерживаемых соединителей.</span><span class="sxs-lookup"><span data-stu-id="352d4-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="352d4-106">Hello шлюза действует как мост, который обеспечивает передачу данных для быстрого и шифрование между источниками данных на локальном компьютере и логику приложения.</span><span class="sxs-lookup"><span data-stu-id="352d4-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="352d4-107">шлюз Hello передает данные из локальных источников шифрованные каналы через hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="352d4-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="352d4-108">Весь трафик поступает как безопасный исходящий трафик от агента hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="352d4-109">Дополнительные сведения о [как работает шлюз данных hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="352d4-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="352d4-110">Hello шлюз поддерживает источники данных toothese подключений на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="352d4-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="352d4-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="352d4-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="352d4-112">DB2</span><span class="sxs-lookup"><span data-stu-id="352d4-112">DB2</span></span>  
*   <span data-ttu-id="352d4-113">Файловая система</span><span class="sxs-lookup"><span data-stu-id="352d4-113">File System</span></span>
*   <span data-ttu-id="352d4-114">Informix</span><span class="sxs-lookup"><span data-stu-id="352d4-114">Informix</span></span>
*   <span data-ttu-id="352d4-115">Магический квадрант</span><span class="sxs-lookup"><span data-stu-id="352d4-115">MQ</span></span>
*   <span data-ttu-id="352d4-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="352d4-116">MySQL</span></span>
*   <span data-ttu-id="352d4-117">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="352d4-117">Oracle Database</span></span>
*   <span data-ttu-id="352d4-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="352d4-118">PostgreSQL</span></span>
*   <span data-ttu-id="352d4-119">сервер приложений SAP;</span><span class="sxs-lookup"><span data-stu-id="352d4-119">SAP Application Server</span></span> 
*   <span data-ttu-id="352d4-120">сервер сообщений SAP;</span><span class="sxs-lookup"><span data-stu-id="352d4-120">SAP Message Server</span></span>
*   <span data-ttu-id="352d4-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="352d4-121">SharePoint</span></span>
*   <span data-ttu-id="352d4-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="352d4-122">SQL Server</span></span>
*   <span data-ttu-id="352d4-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="352d4-123">Teradata</span></span>

<span data-ttu-id="352d4-124">Следующие шаги показывают, как tooset копирование hello локальной toowork шлюз данных вместе со своими приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="352d4-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="352d4-125">Дополнительные сведения о поддерживаемых соединителях см. статье [Список соединителей](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="352d4-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="352d4-126">Сведения о том, как toouse hello шлюза с другими службами см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="352d4-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="352d4-127">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="352d4-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="352d4-128">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="352d4-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="352d4-129">Управление локальным шлюзом данных в Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="352d4-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="352d4-130">Управление локальным шлюзом данных в PowerApps</span><span class="sxs-lookup"><span data-stu-id="352d4-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="352d4-131">Требования</span><span class="sxs-lookup"><span data-stu-id="352d4-131">Requirements</span></span>

* <span data-ttu-id="352d4-132">Необходимо иметь уже [установить шлюз данных hello на локальном компьютере](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="352d4-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="352d4-133">При входе в toohello портал Azure, у вас есть toouse hello та же самая или рабочей учетной записи, который был использован слишком[установить шлюз данных в локальной среде hello](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="352d4-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="352d4-134">Ваша учетная запись входа должен быть toouse подписки Azure при создании ресурса шлюза в hello портал Azure для установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="352d4-135">Не должно быть заявок на доступ к этой установке шлюза от другого ресурса шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="352d4-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="352d4-136">Можно связать шлюза tooonly один шлюз Azure источнику установки.</span><span class="sxs-lookup"><span data-stu-id="352d4-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="352d4-137">Утверждение происходит при создании ресурса шлюза hello, чтобы установка hello недоступен для других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="352d4-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="352d4-138">Настройка подключения шлюза данных hello</span><span class="sxs-lookup"><span data-stu-id="352d4-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="352d4-139">1. Установить шлюз данных в локальной среде hello</span><span class="sxs-lookup"><span data-stu-id="352d4-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="352d4-140">Если это еще не сделано, выполните hello [tooinstall действия hello на локальный шлюз данных](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="352d4-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="352d4-141">Прежде чем продолжить hello другие действия, убедитесь в установке hello шлюз данных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="352d4-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="352d4-142">2. Создать ресурс Azure для hello локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="352d4-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="352d4-143">После установки шлюза hello на локальном компьютере, необходимо создать шлюз данных как ресурс в Azure.</span><span class="sxs-lookup"><span data-stu-id="352d4-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="352d4-144">На этом шаге также связывается ресурс шлюза с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="352d4-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="352d4-145">Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="352d4-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="352d4-146">Убедитесь, что toouse hello одинаковых операций Azure или использовать адрес электронной почты school tooinstall hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="352d4-147">В левом меню hello в Azure, выберите **New** > **интеграцию** > **локального шлюза данных** как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="352d4-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Поиск элемента "Локальный шлюз данных"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="352d4-149">На hello **создать шлюз подключения** колонки, предоставляют эти сведения toocreate ресурс шлюза данных:</span><span class="sxs-lookup"><span data-stu-id="352d4-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="352d4-150">**Имя.** Введите имя для вашего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="352d4-151">**Подписки**: выберите hello tooassociate подписки Azure с этим ресурсом шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="352d4-152">Это подписка должна быть той же подписке, логика приложения hello.</span><span class="sxs-lookup"><span data-stu-id="352d4-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="352d4-153">Подписка по умолчанию Hello основан на hello учетная запись Azure, который использовался toosign в.</span><span class="sxs-lookup"><span data-stu-id="352d4-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="352d4-154">**Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся для развертывания своего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="352d4-155">Группы ресурсов помогают управлять связанными ресурсами Azure в качестве коллекции.</span><span class="sxs-lookup"><span data-stu-id="352d4-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="352d4-156">**Расположение**: Azure ограничивает это расположение toohello же регионе, который был выбран для hello шлюз облачной службы во время [установку шлюза](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="352d4-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="352d4-157">Убедитесь, что соответствует, расположение ресурса шлюза hello расположение hello шлюз облачной службы.</span><span class="sxs-lookup"><span data-stu-id="352d4-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="352d4-158">В противном случае установки шлюза могут не отображаться в списке hello установлены шлюзы для вас tooselect в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="352d4-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="352d4-159">Вы можете выбрать разные регионы для ресурса шлюза и вашего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="352d4-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="352d4-160">**Установка имя**: Если установки шлюза еще не выбрана, выберите hello шлюза, установленного ранее.</span><span class="sxs-lookup"><span data-stu-id="352d4-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="352d4-161">Выберите tooadd hello шлюза ресурсов tooyour панель мониторинга Azure, **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="352d4-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="352d4-162">Когда все будет готово, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="352d4-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="352d4-163">Например:</span><span class="sxs-lookup"><span data-stu-id="352d4-163">For example:</span></span>

    ![Укажите сведения toocreate локального шлюза данных](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="352d4-165">слишком toofind или представления перейдите шлюз данных в любое время hello в главном меню Azure левой, **более служб** > **интеграцию** > **локальных данных Шлюзы**.</span><span class="sxs-lookup"><span data-stu-id="352d4-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Слишком перейдите в раздел «Дополнительные службы», «Интеграция предприятия», «Локальные данные шлюзов»](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="352d4-167">3. Подключения на логику приложения toohello на локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="352d4-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="352d4-168">Создания ресурса шлюза данных и связанные с этим ресурсом подписки Azure, необходимо создайте подключение между логику приложения и hello шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="352d4-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="352d4-169">Расположение подключения шлюза должен существовать в hello же регионе, что логика приложения, но можно использовать шлюз данных, который существует в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="352d4-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="352d4-170">В hello портал Azure создайте или откройте приложение логики в конструкторе логики приложения.</span><span class="sxs-lookup"><span data-stu-id="352d4-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="352d4-171">Добавьте соединитель, который поддерживает локальные подключения, например SQL Server.</span><span class="sxs-lookup"><span data-stu-id="352d4-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="352d4-172">Выберите следующие порядке hello, **подключиться через локальный шлюз данных**, укажите имя уникального соединения hello необходимые сведения и выберите ресурс шлюза данных hello, что требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="352d4-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="352d4-173">Когда все будет готово, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="352d4-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="352d4-174">Уникальное имя подключения позволяет легко идентифицировать подключение позже, особенно при создании нескольких подключений.</span><span class="sxs-lookup"><span data-stu-id="352d4-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="352d4-175">Если это применимо, также включать hello доменного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="352d4-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Создание подключения между логическим приложением и шлюзом данных](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="352d4-177">Итак, теперь подключения шлюза готова к вашей toouse логику приложения.</span><span class="sxs-lookup"><span data-stu-id="352d4-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="352d4-178">Изменение параметров подключения к шлюзу</span><span class="sxs-lookup"><span data-stu-id="352d4-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="352d4-179">После создания подключения шлюза для логики приложения, может потребоваться параметры hello toolater обновления для конкретных подключений.</span><span class="sxs-lookup"><span data-stu-id="352d4-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="352d4-180">подключение к шлюзу hello toofind:</span><span class="sxs-lookup"><span data-stu-id="352d4-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="352d4-181">В колонке логику приложения hello под **средства разработки**выберите **подключений API**.</span><span class="sxs-lookup"><span data-stu-id="352d4-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="352d4-182">Hello **подключений API** области отображаются все соединения API, связанные с логики приложения, включая подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Перейдите в приложение логики tooyour, выберите «API соединения»](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="352d4-184">Hello в главном меню Azure левой, также можно найти слишком **более служб** > **веб-приложений и мобильных служб** > **подключений API** для всех подключений API включая подключения шлюза, которые связаны с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="352d4-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="352d4-185">Hello главного меню Azure левой, также можно найти слишком**все ресурсы** для всех подключений, API-Интерфейс, включая подключения через шлюз, которые связаны с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="352d4-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="352d4-186">Выберите подключение к шлюзу hello tooview или изменить и выберите **соединение изменить API**.</span><span class="sxs-lookup"><span data-stu-id="352d4-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="352d4-187">Если изменения не вступили в силу, попробуйте [остановка и перезапуск службы Windows шлюза hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="352d4-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="352d4-188">Переключение или ресурса локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="352d4-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="352d4-189">toocreate ресурс другой шлюз связать шлюза на другой ресурс, или удалить ресурс шлюза hello, hello шлюза ресурс можно удалить, не затрагивая hello установку шлюза.</span><span class="sxs-lookup"><span data-stu-id="352d4-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="352d4-190">Hello в главном меню Azure левой, go слишком**все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="352d4-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="352d4-191">Найдите и выберите ресурс шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="352d4-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="352d4-192">Выберите **локального шлюза данных**и на панели инструментов hello ресурса, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="352d4-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="352d4-193">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="352d4-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="352d4-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="352d4-194">Next steps</span></span>

* [<span data-ttu-id="352d4-195">Защита приложений логики</span><span class="sxs-lookup"><span data-stu-id="352d4-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="352d4-196">Распространенные примеры и сценарии использования приложений логики</span><span class="sxs-lookup"><span data-stu-id="352d4-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
