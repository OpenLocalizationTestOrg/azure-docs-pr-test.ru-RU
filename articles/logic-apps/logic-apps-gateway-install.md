---
title: "шлюз данных в локальной aaaInstall - приложения логики Azure | Документы Microsoft"
description: "Получить доступ к источникам данных на локальном компьютере, установка hello локального шлюза данных для передачи данных для быстрого и шифрования между источниками данных на локальном компьютере и логика приложения"
keywords: "доступ к данным, локальный, передача данных, шифрование, источники данных"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="692e8-104">Установить шлюз данных hello локальными для приложения логики Azure</span><span class="sxs-lookup"><span data-stu-id="692e8-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="692e8-105">Свои приложения логики можно получить доступ к источникам данных на локальном компьютере, необходимо установить и настроить hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="692e8-106">Hello шлюза действует как мост, который обеспечивает передачу данных быстрого и шифрование между локальными системами и логику приложения.</span><span class="sxs-lookup"><span data-stu-id="692e8-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="692e8-107">шлюз Hello передает данные из локальных источников шифрованные каналы через hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="692e8-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="692e8-108">Весь трафик поступает как безопасный исходящий трафик от агента hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="692e8-109">Дополнительные сведения о [как работает шлюз данных hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="692e8-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="692e8-110">Hello шлюз поддерживает источники данных toothese подключений на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="692e8-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="692e8-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="692e8-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="692e8-112">DB2</span><span class="sxs-lookup"><span data-stu-id="692e8-112">DB2</span></span>  
*   <span data-ttu-id="692e8-113">Файловая система</span><span class="sxs-lookup"><span data-stu-id="692e8-113">File System</span></span>
*   <span data-ttu-id="692e8-114">Informix</span><span class="sxs-lookup"><span data-stu-id="692e8-114">Informix</span></span>
*   <span data-ttu-id="692e8-115">Магический квадрант</span><span class="sxs-lookup"><span data-stu-id="692e8-115">MQ</span></span>
*   <span data-ttu-id="692e8-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="692e8-116">MySQL</span></span>
*   <span data-ttu-id="692e8-117">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="692e8-117">Oracle Database</span></span>
*   <span data-ttu-id="692e8-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="692e8-118">PostgreSQL</span></span>
*   <span data-ttu-id="692e8-119">сервер приложений SAP;</span><span class="sxs-lookup"><span data-stu-id="692e8-119">SAP Application Server</span></span> 
*   <span data-ttu-id="692e8-120">сервер сообщений SAP;</span><span class="sxs-lookup"><span data-stu-id="692e8-120">SAP Message Server</span></span>
*   <span data-ttu-id="692e8-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="692e8-121">SharePoint</span></span>
*   <span data-ttu-id="692e8-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="692e8-122">SQL Server</span></span>
*   <span data-ttu-id="692e8-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="692e8-123">Teradata</span></span>

<span data-ttu-id="692e8-124">Следующие шаги показывают, как hello toofirst установки локального шлюза данных, прежде чем [настроить подключение между шлюзом hello и приложениях для логики](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="692e8-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="692e8-125">Дополнительные сведения о поддерживаемых соединителях см. статье [Список соединителей](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="692e8-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="692e8-126">Сведения о том, как toouse hello шлюза с другими службами см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="692e8-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="692e8-127">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="692e8-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="692e8-128">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="692e8-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="692e8-129">Управление локальным шлюзом данных в Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="692e8-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="692e8-130">Управление локальным шлюзом данных в PowerApps</span><span class="sxs-lookup"><span data-stu-id="692e8-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="692e8-131">Требования</span><span class="sxs-lookup"><span data-stu-id="692e8-131">Requirements</span></span>

<span data-ttu-id="692e8-132">**Минимальные**:</span><span class="sxs-lookup"><span data-stu-id="692e8-132">**Minimum**:</span></span>

* <span data-ttu-id="692e8-133">.NET Framework 4.5;</span><span class="sxs-lookup"><span data-stu-id="692e8-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="692e8-134">64-разрядная версия Windows 7 или Windows Server 2008 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="692e8-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="692e8-135">**Рекомендуемые**:</span><span class="sxs-lookup"><span data-stu-id="692e8-135">**Recommended**:</span></span>

* <span data-ttu-id="692e8-136">8-ядерный ЦП;</span><span class="sxs-lookup"><span data-stu-id="692e8-136">8 Core CPU</span></span>
* <span data-ttu-id="692e8-137">8 ГБ ОЗУ;</span><span class="sxs-lookup"><span data-stu-id="692e8-137">8 GB Memory</span></span>
* <span data-ttu-id="692e8-138">64-разрядная версия Windows 2012 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="692e8-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="692e8-139">**Важные сведения**:</span><span class="sxs-lookup"><span data-stu-id="692e8-139">**Important considerations**:</span></span>

* <span data-ttu-id="692e8-140">Установите hello локального шлюза данных только на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="692e8-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="692e8-141">Hello шлюза нельзя установить на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="692e8-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="692e8-142">Нет шлюза hello tooinstall на hello же компьютере, что источник данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="692e8-143">Задержка toominimize шлюз можно установить hello закрытия от возможных tooyour источника данных или hello же компьютере, при условии, что имеются разрешения.</span><span class="sxs-lookup"><span data-stu-id="692e8-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="692e8-144">Не устанавливайте hello шлюза на компьютере, который отключает, становится toosleep или не подключиться toohello Интернета, так как шлюз hello не может работать в этих условиях.</span><span class="sxs-lookup"><span data-stu-id="692e8-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="692e8-145">Кроме того, может наблюдаться снижение производительности шлюза при использовании беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="692e8-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="692e8-146">Во время установки необходимо войти с помощью [рабочей или учебной учетной записи](https://docs.microsoft.com/azure/active-directory/sign-up-organization), управляемой Azure Active Directory, а не учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="692e8-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="692e8-147">У вас есть toouse hello та же самая или учебы позже в hello Azure учетная запись портала при создании и связать ресурс шлюза в установку шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="692e8-148">Затем выберите этот ресурс шлюза, при создании подключения hello между логику приложения и hello локального источника данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="692e8-149">Почему необходимо использовать рабочую или учебную учетную запись Azure AD?</span><span class="sxs-lookup"><span data-stu-id="692e8-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="692e8-150">Если вы зарегистрировались для использования предложения Office 365 и не предоставили действительный рабочий электронный адрес, то ваш адрес входа может выглядеть так: jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="692e8-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="692e8-151">При наличии существующего шлюза, который настраивается с установщиком, более ранняя, чем версия 14.16.6317.4 Невозможно изменить расположение шлюза установщиком выполняющегося hello последней.</span><span class="sxs-lookup"><span data-stu-id="692e8-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="692e8-152">Тем не менее можно использовать tooset последнюю установщика hello копирование новый шлюз с расположением hello, необходимо вместо этого.</span><span class="sxs-lookup"><span data-stu-id="692e8-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="692e8-153">Если установщик шлюза, более ранняя, чем версия 14.16.6317.4, но еще не установили шлюз еще, можно загрузить и использовать последние установщика hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="692e8-154">Установить шлюз данных hello</span><span class="sxs-lookup"><span data-stu-id="692e8-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="692e8-155">[Загрузите и запустите установщик шлюза hello на локальном компьютере](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="692e8-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="692e8-156">Просмотрите и примите условия использования и заявление о конфиденциальности hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="692e8-157">Укажите путь к hello на локальном компьютере место tooinstall hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="692e8-158">При появлении запроса войдите в Azure с рабочей или учебной учетной записью (но не с учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="692e8-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Войдите с помощью рабочей или учебной учетной записи Azure и](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="692e8-160">Зарегистрировать установленный шлюз с hello [облачной службе шлюза](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="692e8-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="692e8-161">Выберите **Регистрация нового шлюза на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="692e8-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="692e8-162">облачной службе шлюза Hello шифрует и сохраняет учетные данные источника данных и сведения о шлюзе.</span><span class="sxs-lookup"><span data-stu-id="692e8-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="692e8-163">Служба Hello также выполняет запросы и их результаты между логику приложения hello локального шлюза данных и источника данных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="692e8-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="692e8-164">Укажите имя установленного шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="692e8-165">Создайте ключ восстановления, а затем подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="692e8-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="692e8-166">Ключ восстановления должен содержать по крайней мере 8 знаков.</span><span class="sxs-lookup"><span data-stu-id="692e8-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="692e8-167">Убедитесь в том, сохранить и hello ключ должен оставаться в надежном месте.</span><span class="sxs-lookup"><span data-stu-id="692e8-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="692e8-168">Также этот ключ требуется при необходимости toomigrate, восстановление или перенос существующего шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="692e8-169">Выберите регион по умолчанию hello toochange для облачной службы шлюза hello и используемые установку шлюза Azure Service Bus **Смена региона**.</span><span class="sxs-lookup"><span data-stu-id="692e8-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Изменение региона](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="692e8-171">область по умолчанию Hello — hello регион, связанный с клиентом Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692e8-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="692e8-172">На следующей панели hello, откройте hello **Выбор региона** слишком выбрать другой регион.</span><span class="sxs-lookup"><span data-stu-id="692e8-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Выберите другой регион](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="692e8-174">Например, вы может выбрать hello же регионе, что логика приложения или выберите hello области ближайший tooyour локальных данных источника, можно снизить задержку.</span><span class="sxs-lookup"><span data-stu-id="692e8-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="692e8-175">Ресурс шлюза и приложение логики могут размещаться в разных расположениях.</span><span class="sxs-lookup"><span data-stu-id="692e8-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="692e8-176">После установки изменить выбранный регион будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="692e8-176">You can't change this region after installation.</span></span> <span data-ttu-id="692e8-177">Эта область также определяет и ограничивает hello расположение, где можно создать hello ресурсов Azure для шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="692e8-178">Поэтому при создании ресурса шлюза в Azure убедитесь, расположение ресурса hello соответствует hello регион, выбранный во время установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="692e8-179">Если требуется toouse другой регион для шлюза позже, необходимо настроить новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="692e8-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="692e8-180">Когда вы будете готовы, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="692e8-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="692e8-181">Теперь выполните следующие действия в hello портал Azure, вы можете [создать ресурс Azure для шлюза](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="692e8-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="692e8-182">Дополнительные сведения о [как работает шлюз данных hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="692e8-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="692e8-183">Перенос, восстановление или перехват существующего шлюза</span><span class="sxs-lookup"><span data-stu-id="692e8-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="692e8-184">tooperform этих задач, необходимо иметь hello ключ восстановления, который был указан при установке шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="692e8-185">В меню "Пуск" компьютера выберите **Локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="692e8-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="692e8-186">После hello Откроется установщик вход с помощью hello же Azure работать или рабочую учетную запись, которая была ранее используется tooinstall hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="692e8-187">Выберите **Migrate, restore, or take over an existing gateway** (Перенос, восстановление или перехват имеющегося шлюза).</span><span class="sxs-lookup"><span data-stu-id="692e8-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="692e8-188">Укажите hello имя и ключ восстановления для hello шлюза, который требуется к toomigrate, восстановление или получение.</span><span class="sxs-lookup"><span data-stu-id="692e8-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="692e8-189">Перезапустите шлюз hello</span><span class="sxs-lookup"><span data-stu-id="692e8-189">Restart hello gateway</span></span>

<span data-ttu-id="692e8-190">Hello шлюз работает как служба Windows.</span><span class="sxs-lookup"><span data-stu-id="692e8-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="692e8-191">Как любую другую службу Windows можно запустить и остановить службу hello, различными способами.</span><span class="sxs-lookup"><span data-stu-id="692e8-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="692e8-192">Например можно откройте командную строку с повышенными разрешениями на компьютере hello, где запущен шлюз hello и выполнения любой из этих команд:</span><span class="sxs-lookup"><span data-stu-id="692e8-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="692e8-193">toostop служба hello, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="692e8-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="692e8-194">toostart служба hello, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="692e8-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="692e8-195">Учетная запись службы Windows</span><span class="sxs-lookup"><span data-stu-id="692e8-195">Windows service account</span></span>

<span data-ttu-id="692e8-196">Hello локальный шлюз данных настроен toouse `NT SERVICE\PBIEgwService` учетные данные для входа службы hello Windows.</span><span class="sxs-lookup"><span data-stu-id="692e8-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="692e8-197">По умолчанию hello шлюза имеет права «Вход в качестве службы» hello машины hello где установить шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="692e8-198">Учетная запись службы Windows Hello отличается от hello учетная запись, используемая для подключения tooon локальные источники данных и от hello Azure на работе или рабочую учетную запись использовать toosign в toocloud служб.</span><span class="sxs-lookup"><span data-stu-id="692e8-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="692e8-199">Настройка брандмауэра или прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="692e8-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="692e8-200">Hello шлюз создает исходящее подключение слишком [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="692e8-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="692e8-201">см. сведения о прокси tooprovide для шлюза, [настроить параметры прокси-сервера](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="692e8-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="692e8-202">toocheck ли брандмауэр или прокси-сервера, могут блокировать подключения, подтвердить фактически подключения компьютера toohello Интернет» и «hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="692e8-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="692e8-203">В командной строке PowerShell выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="692e8-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="692e8-204">Эта команда проверяет только подключения к сети и подключения к toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="692e8-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="692e8-205">Поэтому команда hello не имеет ничего общего toodo со шлюзом hello или облачной службе hello шлюза, который шифрует и сохраняет учетные данные и сведения о шлюзе.</span><span class="sxs-lookup"><span data-stu-id="692e8-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="692e8-206">Кроме того, эта команда используется только в Windows Server 2012 R2 или более поздней версии и Windows 8.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="692e8-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="692e8-207">В более ранних версиях операционной системы, можно использовать Telnet слишком Проверка подключения.</span><span class="sxs-lookup"><span data-stu-id="692e8-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="692e8-208">Узнайте больше о [служебной шине Azure и гибридных решениях](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="692e8-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="692e8-209">Результаты должен выглядеть примерно toothis пример:</span><span class="sxs-lookup"><span data-stu-id="692e8-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="692e8-210">Если **TcpTestSucceeded** не задано слишком**True**, вам может быть заблокирован брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="692e8-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="692e8-211">Toobe комплексный, замените hello **ComputerName** и **порт** значения со значениями hello в списке [настроить порты](#configure-ports) в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="692e8-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="692e8-212">брандмауэр Hello также блокируют подключения, hello Azure Service Bus не делает toohello центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="692e8-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="692e8-213">Если это происходит, утверждение (разблокировать) все hello IP-адресов для этих центрах обработки данных в вашем регионе.</span><span class="sxs-lookup"><span data-stu-id="692e8-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="692e8-214">Для этих IP-адресов [get hello Azure список IP-адресов здесь](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="692e8-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="692e8-215">Настройка портов</span><span class="sxs-lookup"><span data-stu-id="692e8-215">Configure ports</span></span>

<span data-ttu-id="692e8-216">Hello шлюз создает исходящее подключение слишком[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) и осуществляет связь через исходящие порты: TCP-порт 443 (по умолчанию), 5671, 5672, 9350 до 9354.</span><span class="sxs-lookup"><span data-stu-id="692e8-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="692e8-217">шлюз Hello не требуются входящие порты.</span><span class="sxs-lookup"><span data-stu-id="692e8-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="692e8-218">Узнайте больше о [служебной шине Azure и гибридных решениях](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="692e8-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="692e8-219">ДОМЕННЫЕ ИМЕНА</span><span class="sxs-lookup"><span data-stu-id="692e8-219">DOMAIN NAMES</span></span> | <span data-ttu-id="692e8-220">ИСХОДЯЩИЕ ПОРТЫ</span><span class="sxs-lookup"><span data-stu-id="692e8-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="692e8-221">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="692e8-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="692e8-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="692e8-222">*.analysis.windows.net</span></span> | <span data-ttu-id="692e8-223">443</span><span class="sxs-lookup"><span data-stu-id="692e8-223">443</span></span> | <span data-ttu-id="692e8-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="692e8-224">HTTPS</span></span> | 
| <span data-ttu-id="692e8-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="692e8-225">*.login.windows.net</span></span> | <span data-ttu-id="692e8-226">443</span><span class="sxs-lookup"><span data-stu-id="692e8-226">443</span></span> | <span data-ttu-id="692e8-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="692e8-227">HTTPS</span></span> | 
| <span data-ttu-id="692e8-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="692e8-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="692e8-229">5671–5672</span><span class="sxs-lookup"><span data-stu-id="692e8-229">5671-5672</span></span> | <span data-ttu-id="692e8-230">Протокол AMQP</span><span class="sxs-lookup"><span data-stu-id="692e8-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="692e8-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="692e8-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="692e8-232">443, 9350–9354</span><span class="sxs-lookup"><span data-stu-id="692e8-232">443, 9350-9354</span></span> | <span data-ttu-id="692e8-233">Прослушиватели ретрансляции служебной шины по протоколу TCP (порт 443 требуется для получения маркера контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="692e8-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="692e8-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="692e8-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="692e8-235">443</span><span class="sxs-lookup"><span data-stu-id="692e8-235">443</span></span> | <span data-ttu-id="692e8-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="692e8-236">HTTPS</span></span> | 
| <span data-ttu-id="692e8-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="692e8-237">*.core.windows.net</span></span> | <span data-ttu-id="692e8-238">443</span><span class="sxs-lookup"><span data-stu-id="692e8-238">443</span></span> | <span data-ttu-id="692e8-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="692e8-239">HTTPS</span></span> | 
| <span data-ttu-id="692e8-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="692e8-240">login.microsoftonline.com</span></span> | <span data-ttu-id="692e8-241">443</span><span class="sxs-lookup"><span data-stu-id="692e8-241">443</span></span> | <span data-ttu-id="692e8-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="692e8-242">HTTPS</span></span> | 
| <span data-ttu-id="692e8-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="692e8-243">*.msftncsi.com</span></span> | <span data-ttu-id="692e8-244">443</span><span class="sxs-lookup"><span data-stu-id="692e8-244">443</span></span> | <span data-ttu-id="692e8-245">Подключение к Интернету tootest используется в том случае, когда hello шлюз недоступен для hello службы Power BI.</span><span class="sxs-lookup"><span data-stu-id="692e8-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="692e8-246">Если вместо hello tooapprove IP-адресов, можно загрузить и использовать hello [Microsoft Azure Datacenter диапазоны IP-список](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="692e8-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="692e8-247">В некоторых случаях hello Azure Service Bus подключения с IP-адреса вместо полных доменных имен.</span><span class="sxs-lookup"><span data-stu-id="692e8-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="692e8-248">Как работает hello шлюз данных?</span><span class="sxs-lookup"><span data-stu-id="692e8-248">How does hello data gateway work?</span></span>

<span data-ttu-id="692e8-249">шлюз данных Hello упрощающую быстрый и безопасный обмен данными между логики приложения, облачной службе шлюза hello и источника данных в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="692e8-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="692e8-251">Поэтому при hello пользователя в облаке hello взаимодействует с элементом, подключенный tooyour локального источника данных:</span><span class="sxs-lookup"><span data-stu-id="692e8-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="692e8-252">облачной службе шлюза Hello создает запрос, а также hello зашифрованные учетные данные для источника данных hello и отправляет очереди toohello hello запросов для шлюза tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="692e8-253">облачной службе шлюза Hello анализирует запрос hello и помещает toohello запрос hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="692e8-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="692e8-254">Hello локальный шлюз данных опрашивает hello Azure Service Bus для ожидающих запросов.</span><span class="sxs-lookup"><span data-stu-id="692e8-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="692e8-255">Hello шлюз получает запрос hello, расшифровывает учетные данные hello и подключается toohello источника данных с этими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="692e8-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="692e8-256">шлюз Hello отправляет источник данных toohello hello запросов для выполнения.</span><span class="sxs-lookup"><span data-stu-id="692e8-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="692e8-257">Hello результаты отправляются из источника данных hello, задней toohello шлюза и облачной службе шлюза toohello.</span><span class="sxs-lookup"><span data-stu-id="692e8-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="692e8-258">Hello облачной службе шлюза затем использует результаты hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="692e8-259">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="692e8-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="692e8-260">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="692e8-260">General</span></span>

<span data-ttu-id="692e8-261">**Q**: требуется использовать шлюз для источников данных в облаке hello, такие как SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="692e8-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="692e8-262">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="692e8-262">
**A**: No.</span></span> <span data-ttu-id="692e8-263">Шлюз соединяет локальные tooon только источники данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="692e8-264">**Q**: hello шлюза имеет toobe установлен на компьютер же, как источник данных hello hello?</span><span class="sxs-lookup"><span data-stu-id="692e8-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="692e8-265">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="692e8-265">
**A**: No.</span></span> <span data-ttu-id="692e8-266">toohello источника данных, используя сведения о соединении hello, предоставленный подключение шлюза Hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="692e8-267">Рассмотрим hello шлюза как клиентское приложение в этом смысле.</span><span class="sxs-lookup"><span data-stu-id="692e8-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="692e8-268">шлюз Hello достаточно hello возможность tooconnect toohello имя сервера, предоставленный.</span><span class="sxs-lookup"><span data-stu-id="692e8-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="692e8-269">**Q**: Почему необходимо ли использовать Azure рабочие или школьные toosign учетной записи в?</span><span class="sxs-lookup"><span data-stu-id="692e8-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="692e8-270">
**Объект**: только можно использовать Azure на работе или рабочую учетную запись при установке hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="692e8-271">Учетная запись для входа хранится в клиенте, которым управляет Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="692e8-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="692e8-272">Как правило учетной записи Azure AD имя участника-пользователя (UPN) соответствует адресу электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="692e8-273">**Вопрос**. Где хранятся мои учетные данные?</span><span class="sxs-lookup"><span data-stu-id="692e8-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="692e8-274">
**Объект**: зашифрованы и хранятся в облачной службе шлюза hello hello учетные данные, введенные для источника данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="692e8-275">Hello они расшифровываются hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="692e8-276">**Вопрос**. Есть ли какие-либо требования к пропускной способности сети?</span><span class="sxs-lookup"><span data-stu-id="692e8-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="692e8-277">
**Ответ**. Пропускная способность сети должна быть высокой.</span><span class="sxs-lookup"><span data-stu-id="692e8-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="692e8-278">Каждая среда имеет свои и hello объем отправляемых данных влияет на результаты hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="692e8-279">С помощью ExpressRoute может помочь tooguarantee определенную пропускную способность между локальной и hello центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="692e8-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="692e8-280">Можно использовать пропускную способность hello стороннего средства Azure скорость тестирования приложения toohelp датчика.</span><span class="sxs-lookup"><span data-stu-id="692e8-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="692e8-281">**Q**: что такое hello задержку для выполнения запросов источника данных tooa из шлюза hello?</span><span class="sxs-lookup"><span data-stu-id="692e8-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="692e8-282">Что такое hello оптимальная архитектура?</span><span class="sxs-lookup"><span data-stu-id="692e8-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="692e8-283">
**Объект**: tooreduce задержку в сети и установить шлюз hello закрыть toohello источник данных как можно.</span><span class="sxs-lookup"><span data-stu-id="692e8-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="692e8-284">При установке шлюза hello hello фактические данные источника этого выражения с учетом сводит к минимуму задержки hello, введенной.</span><span class="sxs-lookup"><span data-stu-id="692e8-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="692e8-285">Рассмотрим слишком hello центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-285">Consider hello datacenters too.</span></span> <span data-ttu-id="692e8-286">Например если служба использует hello Запад США центра обработки данных и сервер SQL Server, размещенных на виртуальной Машине Azure, ВМ Azure должны находиться в hello Запад США слишком.</span><span class="sxs-lookup"><span data-stu-id="692e8-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="692e8-287">Это выражение с учетом сводит к минимуму задержки и позволяет избежать расходов на исходящие данные на виртуальной Машине Azure hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="692e8-288">**Q**: как являются облачной серверной toohello набор результатов?</span><span class="sxs-lookup"><span data-stu-id="692e8-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="692e8-289">
**Объект**: результаты отправляются через hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="692e8-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="692e8-290">**Q**: существуют шлюза toohello все входящие подключения из облака hello?</span><span class="sxs-lookup"><span data-stu-id="692e8-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="692e8-291">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="692e8-291">
**A**: No.</span></span> <span data-ttu-id="692e8-292">шлюз Hello использует tooAzure исходящие подключения Service Bus.</span><span class="sxs-lookup"><span data-stu-id="692e8-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="692e8-293">**Вопрос**. Что делать, если мной заблокированы исходящие подключения?</span><span class="sxs-lookup"><span data-stu-id="692e8-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="692e8-294">Что делать мне tooopen?</span><span class="sxs-lookup"><span data-stu-id="692e8-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="692e8-295">
**Объект**: hello порты и узлы, которые использует шлюз hello. в разделе.</span><span class="sxs-lookup"><span data-stu-id="692e8-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="692e8-296">**Q**: как называется соответствующая служба Windows hello?</span><span class="sxs-lookup"><span data-stu-id="692e8-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="692e8-297">
**Объект**: В службах, hello шлюз указан под именем Power BI Enterprise Gateway Service.</span><span class="sxs-lookup"><span data-stu-id="692e8-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="692e8-298">**Q**: можно запускать с учетной записью Azure Active Directory служба Windows шлюза "hello"?</span><span class="sxs-lookup"><span data-stu-id="692e8-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="692e8-299">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="692e8-299">
**A**: No.</span></span> <span data-ttu-id="692e8-300">Служба Windows Hello должен иметь допустимую учетную запись Windows.</span><span class="sxs-lookup"><span data-stu-id="692e8-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="692e8-301">По умолчанию hello служба запускается с hello SID службы NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="692e8-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="692e8-302">Высокий уровень доступности и аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="692e8-302">High availability and disaster recovery</span></span>

<span data-ttu-id="692e8-303">**Вопрос**. Какие варианты доступны для аварийного восстановления?</span><span class="sxs-lookup"><span data-stu-id="692e8-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="692e8-304">
**Объект**: можно использовать toorestore ключа восстановления hello или переноса шлюза.</span><span class="sxs-lookup"><span data-stu-id="692e8-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="692e8-305">При установке шлюза hello, укажите ключ восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="692e8-306">**Q**: что такое преимущество hello hello ключ восстановления?</span><span class="sxs-lookup"><span data-stu-id="692e8-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="692e8-307">
**Объект**: hello ключ восстановления предоставляет toomigrate способом или восстановить параметры шлюза после сбоя.</span><span class="sxs-lookup"><span data-stu-id="692e8-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="692e8-308">**Q**: планируется ли для включения сценарии высокой доступности с hello шлюза?</span><span class="sxs-lookup"><span data-stu-id="692e8-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="692e8-309">
**Объект**: эти сценарии расположены на стратегия hello, но мы временная шкала еще нет.</span><span class="sxs-lookup"><span data-stu-id="692e8-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="692e8-310">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="692e8-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="692e8-311">**Q**: как я могу узнать, какие запросы отправляются toohello к локальному источнику данных?</span><span class="sxs-lookup"><span data-stu-id="692e8-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="692e8-312">
**Объект**: можно включить трассировку запроса, включая hello запросы, отправленные.</span><span class="sxs-lookup"><span data-stu-id="692e8-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="692e8-313">Не забывайте toochange запроса отслеживания в обратном toohello исходное значение после завершения устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="692e8-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="692e8-314">При включенной трассировке запросов создаются журналы большего размера.</span><span class="sxs-lookup"><span data-stu-id="692e8-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="692e8-315">Кроме того, можно рассмотреть инструменты трассировки запросов, доступные для вашего источника данных.</span><span class="sxs-lookup"><span data-stu-id="692e8-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="692e8-316">Например, можно использовать расширенные события или SQL Profiler для SQL Server и служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="692e8-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="692e8-317">**Q**: где находятся журналы шлюза hello?</span><span class="sxs-lookup"><span data-stu-id="692e8-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="692e8-318">
**Ответ**. См. раздел "Средства" далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="692e8-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="692e8-319">Последнюю версию обновления toohello</span><span class="sxs-lookup"><span data-stu-id="692e8-319">Update toohello latest version</span></span>

<span data-ttu-id="692e8-320">Многие проблемы могут возникать при устаревшей версии шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="692e8-321">В качестве общих рекомендаций убедитесь, что используется последняя версия hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="692e8-322">Hello шлюз не обновлялся в течение месяца или более, может рекомендуется установить последнюю версию шлюза hello hello и разделе, если можно воспроизвести проблему hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="692e8-323">: Ошибка toogroup tooadd пользователя.</span><span class="sxs-lookup"><span data-stu-id="692e8-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="692e8-324">(-2147463168 PBIEgwService Performance Log Users ) (-2147463168 пользователей журналов производительности PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="692e8-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="692e8-325">Эту ошибку можно получить, если при попытке tooinstall hello шлюз на контроллере домена, который не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="692e8-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="692e8-326">Убедитесь, что развертывании hello шлюза на компьютере, который не контроллер домена.</span><span class="sxs-lookup"><span data-stu-id="692e8-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="692e8-327">Средства</span><span class="sxs-lookup"><span data-stu-id="692e8-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="692e8-328">Собирать журналы из шлюза configurer hello</span><span class="sxs-lookup"><span data-stu-id="692e8-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="692e8-329">Вы можете собрать несколько журналов для шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="692e8-330">Всегда начинайте с журналами hello.</span><span class="sxs-lookup"><span data-stu-id="692e8-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="692e8-331">Журналы установщика</span><span class="sxs-lookup"><span data-stu-id="692e8-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="692e8-332">Журналы конфигурации</span><span class="sxs-lookup"><span data-stu-id="692e8-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="692e8-333">Журналы службы корпоративного шлюза</span><span class="sxs-lookup"><span data-stu-id="692e8-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="692e8-334">Журналы событий</span><span class="sxs-lookup"><span data-stu-id="692e8-334">Event logs</span></span>

<span data-ttu-id="692e8-335">Найти hello журналы шлюза управления данными и PowerBIGateway **журналы приложений и служб**.</span><span class="sxs-lookup"><span data-stu-id="692e8-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="692e8-336">Трассировки Fiddler</span><span class="sxs-lookup"><span data-stu-id="692e8-336">Fiddler Trace</span></span>

<span data-ttu-id="692e8-337">[Fiddler](http://www.telerik.com/fiddler) — это бесплатный инструмент от компании Telerik, который отслеживает трафик HTTP.</span><span class="sxs-lookup"><span data-stu-id="692e8-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="692e8-338">Вы увидите этот трафик с hello службы Power BI из hello клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="692e8-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="692e8-339">Эта служба позволит выявить ошибки и другие сопутствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="692e8-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="692e8-340">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="692e8-340">Next steps</span></span>
    
* [<span data-ttu-id="692e8-341">Подключение tooon локальные данные из приложения логики</span><span class="sxs-lookup"><span data-stu-id="692e8-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="692e8-342">Возможности интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="692e8-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="692e8-343">Список соединителей</span><span class="sxs-lookup"><span data-stu-id="692e8-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
