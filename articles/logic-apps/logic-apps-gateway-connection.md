---
title: "Доступ к локальным источникам данных в Azure Logic Apps | Документация Майкрософт"
description: "Настройка локального шлюза данных для доступа к локальным источникам данных из приложений логики"
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="67848-104">Доступ к локальным источникам данных из приложений логики с помощью локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="67848-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="67848-105">Чтобы иметь доступ к локальным источникам данных из ваших приложений логики, настройте локальный шлюз данных, который могут использовать приложения логики с помощью поддерживаемых соединителей.</span><span class="sxs-lookup"><span data-stu-id="67848-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="67848-106">Этот шлюз используется в качестве моста для шифрования и быстрой передачи данных между локальными источниками данных и приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="67848-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="67848-107">Шлюз ретранслирует данные из локальных источников по шифрованным каналам через служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="67848-108">Весь трафик поступает как безопасный исходящий трафик от агента шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="67848-109">Дополнительные сведения см. в разделе [Как работает шлюз](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="67848-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="67848-110">Шлюз поддерживает подключения к таким локальным источникам данных:</span><span class="sxs-lookup"><span data-stu-id="67848-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="67848-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="67848-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="67848-112">DB2</span><span class="sxs-lookup"><span data-stu-id="67848-112">DB2</span></span>  
*   <span data-ttu-id="67848-113">Файловая система</span><span class="sxs-lookup"><span data-stu-id="67848-113">File System</span></span>
*   <span data-ttu-id="67848-114">Informix</span><span class="sxs-lookup"><span data-stu-id="67848-114">Informix</span></span>
*   <span data-ttu-id="67848-115">Магический квадрант</span><span class="sxs-lookup"><span data-stu-id="67848-115">MQ</span></span>
*   <span data-ttu-id="67848-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="67848-116">MySQL</span></span>
*   <span data-ttu-id="67848-117">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="67848-117">Oracle Database</span></span>
*   <span data-ttu-id="67848-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="67848-118">PostgreSQL</span></span>
*   <span data-ttu-id="67848-119">сервер приложений SAP;</span><span class="sxs-lookup"><span data-stu-id="67848-119">SAP Application Server</span></span> 
*   <span data-ttu-id="67848-120">сервер сообщений SAP;</span><span class="sxs-lookup"><span data-stu-id="67848-120">SAP Message Server</span></span>
*   <span data-ttu-id="67848-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="67848-121">SharePoint</span></span>
*   <span data-ttu-id="67848-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="67848-122">SQL Server</span></span>
*   <span data-ttu-id="67848-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="67848-123">Teradata</span></span>

<span data-ttu-id="67848-124">Далее представлена процедура настройки локального шлюза данных для работы с приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="67848-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="67848-125">Дополнительные сведения о поддерживаемых соединителях см. статье [Список соединителей](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="67848-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="67848-126">Сведения о том, как использовать шлюз с другими службами, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="67848-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="67848-127">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="67848-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="67848-128">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="67848-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="67848-129">Управление локальным шлюзом данных в Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="67848-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="67848-130">Управление локальным шлюзом данных в PowerApps</span><span class="sxs-lookup"><span data-stu-id="67848-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="67848-131">Требования</span><span class="sxs-lookup"><span data-stu-id="67848-131">Requirements</span></span>

* <span data-ttu-id="67848-132">[Шлюз данных должен быть установлен на локальном компьютере](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="67848-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="67848-133">При входе на портал Azure необходимо использовать ту же рабочую или учебную запись, которая использовалась для [установки локального шлюза данных](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="67848-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="67848-134">Для установки шлюза у вашей учетной записи входа также должна быть подписка Azure, которая будет использоваться при создании ресурса шлюза на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="67848-135">Не должно быть заявок на доступ к этой установке шлюза от другого ресурса шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="67848-136">Вы можете связать установку шлюза только с одним ресурсом шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="67848-137">Заявка осуществляется при создании ресурса шлюза, поэтому установка недоступна для других ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67848-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="67848-138">Настройка подключения к шлюзу данных</span><span class="sxs-lookup"><span data-stu-id="67848-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="67848-139">1. Установка локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="67848-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="67848-140">Если это еще не сделано, выполните следующие [действия, чтобы установить локальный шлюз данных](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="67848-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="67848-141">Перед тем как продолжить, убедитесь, что шлюз данных установлен на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="67848-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="67848-142">2) Создание ресурса для локального шлюза данных Azure</span><span class="sxs-lookup"><span data-stu-id="67848-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="67848-143">После установки шлюза на локальном компьютере вам необходимо создать шлюз данных в качестве ресурса в Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="67848-144">На этом шаге также связывается ресурс шлюза с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="67848-145">Войдите на [портал Azure](https://portal.azure.com "Портал Azure").</span><span class="sxs-lookup"><span data-stu-id="67848-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="67848-146">Убедитесь, что используете тот же рабочий или учебный адрес электронной почты Azure, что и при установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="67848-147">В меню слева в Azure выберите **Создать** > **Интеграция с предприятием** > **Локальный шлюз данных**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="67848-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Поиск элемента "Локальный шлюз данных"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="67848-149">Чтобы создать ресурс шлюза данных, в колонке **Создание шлюза для подключения** укажите такие сведения:</span><span class="sxs-lookup"><span data-stu-id="67848-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="67848-150">**Имя.** Введите имя для вашего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="67848-151">**Подписка.** Выберите подписку Azure, связанную с вашим ресурсом шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="67848-152">Это должна быть та же подписка, которая использовалась для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="67848-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="67848-153">Подписка по умолчанию основана на учетной записи Azure, которая использовалась для входа.</span><span class="sxs-lookup"><span data-stu-id="67848-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="67848-154">**Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся для развертывания своего ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="67848-155">Группы ресурсов помогают управлять связанными ресурсами Azure в качестве коллекции.</span><span class="sxs-lookup"><span data-stu-id="67848-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="67848-156">**Расположение.** Azure ограничивает расположение тем же регионом, выбранным для облачной службы шлюза во время [установки шлюза](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="67848-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="67848-157">Убедитесь, что расположение ресурса шлюза совпадает с расположением облачной службы шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="67848-158">В противном случае установка вашего шлюза может не отобразиться в списке установленных шлюзов, который вы можете выбрать на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="67848-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="67848-159">Вы можете выбрать разные регионы для ресурса шлюза и вашего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="67848-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="67848-160">**Имя установки.** Если установка шлюза еще не выбрана, выберите шлюз, установленный ранее.</span><span class="sxs-lookup"><span data-stu-id="67848-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="67848-161">Чтобы добавить ресурс шлюза на панель мониторинга Azure, выберите **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="67848-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="67848-162">Когда все будет готово, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="67848-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="67848-163">Например:</span><span class="sxs-lookup"><span data-stu-id="67848-163">For example:</span></span>

    ![Предоставление сведений для создания локального шлюза данных](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="67848-165">Чтобы в любое время найти или просмотреть шлюз данных, из главного меню Azure слева перейдите на страницу **Больше служб**>**Интеграция с предприятием**>**Локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="67848-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Выбор элементов "Больше служб", "Интеграция с предприятием", "Локальный шлюз данных"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="67848-167">3. Подключение приложения логики к локальному шлюзу данных</span><span class="sxs-lookup"><span data-stu-id="67848-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="67848-168">Теперь, когда вы создали ресурс шлюза данных и связали свою подписку Azure с этим ресурсом, создайте подключение между приложением логики и шлюзом данных.</span><span class="sxs-lookup"><span data-stu-id="67848-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="67848-169">Расположение подключения шлюза должно находиться в том же регионе, что и приложение логики, но вы можете использовать шлюз данных из другого региона.</span><span class="sxs-lookup"><span data-stu-id="67848-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="67848-170">На портале Azure создайте приложение логики или откройте его в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="67848-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="67848-171">Добавьте соединитель, который поддерживает локальные подключения, например SQL Server.</span><span class="sxs-lookup"><span data-stu-id="67848-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="67848-172">Следуя указанному порядку, выберите **Connect via on-premises data gateway** (Подключиться через локальный шлюз данных), укажите уникальное имя соединения и необходимую информацию и выберите ресурс шлюза данных, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="67848-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="67848-173">Когда все будет готово, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="67848-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="67848-174">Уникальное имя подключения позволяет легко идентифицировать подключение позже, особенно при создании нескольких подключений.</span><span class="sxs-lookup"><span data-stu-id="67848-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="67848-175">При необходимости добавьте также имя домена для вашего имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="67848-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![Создание подключения между логическим приложением и шлюзом данных](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="67848-177">Поздравляем! Подключение шлюза теперь готово к использованию приложением логики.</span><span class="sxs-lookup"><span data-stu-id="67848-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="67848-178">Изменение параметров подключения к шлюзу</span><span class="sxs-lookup"><span data-stu-id="67848-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="67848-179">После того как вы создадите подключение шлюза для приложения логики, возможно, вам понадобится обновить параметры этого подключения.</span><span class="sxs-lookup"><span data-stu-id="67848-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="67848-180">Чтобы найти подключение шлюза, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="67848-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="67848-181">В колонке приложения логики в разделе **Средства разработки** выберите **Подключения API**.</span><span class="sxs-lookup"><span data-stu-id="67848-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="67848-182">В области **Подключения API** указаны все подключения API, связанные с вашим приложением логики, в том числе подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Переход к приложению логики, выбор "Подключения API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="67848-184">Выберите в главном меню Azure слева элементы **Больше служб** > **Веб-службы и мобильные службы** > **Подключения API** для всех подключений API, в том числе подключений, связанных с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="67848-185">А можно в главном меню Azure слева перейти к разделу **Все ресурсы** для всех подключений API, включая подключения шлюза, связанные с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="67848-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="67848-186">Выберите подключение шлюза, которое вы хотите просмотреть или изменить, и щелкните **Правка подключения API**.</span><span class="sxs-lookup"><span data-stu-id="67848-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="67848-187">Если ваши обновления не вступают в силу, попробуйте [остановить и перезапустить службу Windows шлюза](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="67848-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="67848-188">Переключение или ресурса локального шлюза данных</span><span class="sxs-lookup"><span data-stu-id="67848-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="67848-189">Чтобы создать другой ресурс шлюза, связать ваш шлюз с другим ресурсом или удалить ресурс шлюза, вы можете удалить его, не затрагивая установку шлюза.</span><span class="sxs-lookup"><span data-stu-id="67848-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="67848-190">В главном меню Azure слева щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="67848-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="67848-191">Найдите и выберите ресурс шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="67848-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="67848-192">Выберите **Локальный шлюз данных** и на панели инструментов ресурсов щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="67848-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="67848-193">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="67848-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="67848-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67848-194">Next steps</span></span>

* [<span data-ttu-id="67848-195">Защита приложений логики</span><span class="sxs-lookup"><span data-stu-id="67848-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="67848-196">Распространенные примеры и сценарии использования приложений логики</span><span class="sxs-lookup"><span data-stu-id="67848-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
