---
title: "Установка локального шлюза данных в Azure Logic Apps | Документация Майкрософт"
description: "Прежде чем получить доступ к локальным источникам данных, установите локальный шлюз данных для быстрой передачи и шифрования данных между локальными источниками данных и приложениями логики."
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
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="7bfd6-104">Установка локального шлюза данных для Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7bfd6-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="7bfd6-105">Чтобы приложения логики могли обращаться к локальным источникам данных, нужно установить и настроить локальный шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="7bfd6-106">Этот шлюз используется в качестве моста, обеспечивающего быструю передачу для шифрование данных между локальными системами и приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="7bfd6-107">Шлюз ретранслирует данные из локальных источников по шифрованным каналам через служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="7bfd6-108">Весь трафик поступает как безопасный исходящий трафик от агента шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="7bfd6-109">Дополнительные сведения см. в разделе [Как работает шлюз](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="7bfd6-110">Шлюз поддерживает подключения к таким локальным источникам данных:</span><span class="sxs-lookup"><span data-stu-id="7bfd6-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="7bfd6-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="7bfd6-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="7bfd6-112">DB2</span><span class="sxs-lookup"><span data-stu-id="7bfd6-112">DB2</span></span>  
*   <span data-ttu-id="7bfd6-113">Файловая система</span><span class="sxs-lookup"><span data-stu-id="7bfd6-113">File System</span></span>
*   <span data-ttu-id="7bfd6-114">Informix</span><span class="sxs-lookup"><span data-stu-id="7bfd6-114">Informix</span></span>
*   <span data-ttu-id="7bfd6-115">Магический квадрант</span><span class="sxs-lookup"><span data-stu-id="7bfd6-115">MQ</span></span>
*   <span data-ttu-id="7bfd6-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="7bfd6-116">MySQL</span></span>
*   <span data-ttu-id="7bfd6-117">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="7bfd6-117">Oracle Database</span></span>
*   <span data-ttu-id="7bfd6-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7bfd6-118">PostgreSQL</span></span>
*   <span data-ttu-id="7bfd6-119">сервер приложений SAP;</span><span class="sxs-lookup"><span data-stu-id="7bfd6-119">SAP Application Server</span></span> 
*   <span data-ttu-id="7bfd6-120">сервер сообщений SAP;</span><span class="sxs-lookup"><span data-stu-id="7bfd6-120">SAP Message Server</span></span>
*   <span data-ttu-id="7bfd6-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="7bfd6-121">SharePoint</span></span>
*   <span data-ttu-id="7bfd6-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="7bfd6-122">SQL Server</span></span>
*   <span data-ttu-id="7bfd6-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="7bfd6-123">Teradata</span></span>

<span data-ttu-id="7bfd6-124">Ниже описывается, как установить локальный шлюз данных перед [настройкой подключения между шлюзом и приложениями логики](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="7bfd6-125">Дополнительные сведения о поддерживаемых соединителях см. статье [Список соединителей](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="7bfd6-126">Сведения о том, как использовать шлюз с другими службами, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7bfd6-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="7bfd6-127">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="7bfd6-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="7bfd6-128">Локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="7bfd6-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="7bfd6-129">Управление локальным шлюзом данных в Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="7bfd6-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="7bfd6-130">Управление локальным шлюзом данных в PowerApps</span><span class="sxs-lookup"><span data-stu-id="7bfd6-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="7bfd6-131">Требования</span><span class="sxs-lookup"><span data-stu-id="7bfd6-131">Requirements</span></span>

<span data-ttu-id="7bfd6-132">**Минимальные**:</span><span class="sxs-lookup"><span data-stu-id="7bfd6-132">**Minimum**:</span></span>

* <span data-ttu-id="7bfd6-133">.NET Framework 4.5;</span><span class="sxs-lookup"><span data-stu-id="7bfd6-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="7bfd6-134">64-разрядная версия Windows 7 или Windows Server 2008 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="7bfd6-135">**Рекомендуемые**:</span><span class="sxs-lookup"><span data-stu-id="7bfd6-135">**Recommended**:</span></span>

* <span data-ttu-id="7bfd6-136">8-ядерный ЦП;</span><span class="sxs-lookup"><span data-stu-id="7bfd6-136">8 Core CPU</span></span>
* <span data-ttu-id="7bfd6-137">8 ГБ ОЗУ;</span><span class="sxs-lookup"><span data-stu-id="7bfd6-137">8 GB Memory</span></span>
* <span data-ttu-id="7bfd6-138">64-разрядная версия Windows 2012 R2 (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="7bfd6-139">**Важные сведения**:</span><span class="sxs-lookup"><span data-stu-id="7bfd6-139">**Important considerations**:</span></span>

* <span data-ttu-id="7bfd6-140">Локальный шлюз данных должен быть установлен только на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="7bfd6-141">Нельзя устанавливать его на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="7bfd6-142">Не нужно устанавливать шлюз на компьютере, на котором размещен источник данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="7bfd6-143">Чтобы свести к минимуму задержки, шлюз можно установить как можно ближе к источнику данных или даже на том же компьютере, если только у вас есть соответствующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="7bfd6-144">Не стоит устанавливать шлюз на компьютере, который может выключиться, перейти в спящий режим или не сможет подключиться к Интернету. Все эти обстоятельства помешают выполнению шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="7bfd6-145">Кроме того, может наблюдаться снижение производительности шлюза при использовании беспроводной сети.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="7bfd6-146">Во время установки необходимо войти с помощью [рабочей или учебной учетной записи](https://docs.microsoft.com/azure/active-directory/sign-up-organization), управляемой Azure Active Directory, а не учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="7bfd6-147">Ту же рабочую или учебную учетную запись необходимо использовать позже на портале Azure при создании и связывании ресурса шлюза с установкой шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="7bfd6-148">Затем выберите этот ресурс шлюза при создании подключения между своим приложением логики и локальным источником данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="7bfd6-149">Почему необходимо использовать рабочую или учебную учетную запись Azure AD?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="7bfd6-150">Если вы зарегистрировались для использования предложения Office 365 и не предоставили действительный рабочий электронный адрес, то ваш адрес входа может выглядеть так: jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="7bfd6-151">При наличии шлюза, который был настроен с помощью установщика версии ниже 14.16.6317.4, вы не сможете изменить расположение шлюза, запустив установщик более последней версии.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="7bfd6-152">Тем не менее, можно использовать последнюю версию установщика, чтобы настроить новый шлюз с требуемым расположением.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="7bfd6-153">Если у вас есть установщик шлюза версии ниже 14.16.6317.4, но вы еще не установили шлюз, можно скачать и использовать последнюю версию установщика.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="7bfd6-154">Установка шлюза данных</span><span class="sxs-lookup"><span data-stu-id="7bfd6-154">Install the data gateway</span></span>

1.  <span data-ttu-id="7bfd6-155">[Скачайте и запустите установщик шлюза на локальном компьютере](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="7bfd6-156">Просмотрите и примите условия использования и заявление о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="7bfd6-157">Укажите путь на локальном компьютере для установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="7bfd6-158">При появлении запроса войдите в Azure с рабочей или учебной учетной записью (но не с учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Войдите с помощью рабочей или учебной учетной записи Azure и](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="7bfd6-160">зарегистрируйте установленный шлюз с помощью [облачной службы шлюза](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="7bfd6-161">Выберите **Регистрация нового шлюза на этом компьютере**.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="7bfd6-162">Облачная служба шлюза шифрует и хранит учетные данные источников данных и сведения о шлюзах.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="7bfd6-163">Эта служба также передает запросы и их результаты между приложением логики, локальным шлюзом данных и локальными источниками данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="7bfd6-164">Укажите имя установленного шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="7bfd6-165">Создайте ключ восстановления, а затем подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="7bfd6-166">Ключ восстановления должен содержать по крайней мере 8 знаков.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="7bfd6-167">Сохраните его в надежном месте.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="7bfd6-168">Этот ключ потребуется также, когда возникнет необходимость перенести, восстановить или перехватить имеющийся шлюз.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="7bfd6-169">Чтобы изменить регион по умолчанию для облачной службы шлюза и служебной шины Azure, используемый для установки шлюза, выберите **Изменить регион**.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Изменение региона](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="7bfd6-171">По умолчанию используется регион, связанный с вашим клиентом Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="7bfd6-172">На следующей панели откройте **Выберите регион**, чтобы выбрать другой регион.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Выберите другой регион](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="7bfd6-174">Например, можно выбрать регион, в котором размещено ваше приложение логики, или регион, ближайший к локальному источнику данных, что позволит уменьшить задержки.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="7bfd6-175">Ресурс шлюза и приложение логики могут размещаться в разных расположениях.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="7bfd6-176">После установки изменить выбранный регион будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-176">You can't change this region after installation.</span></span> <span data-ttu-id="7bfd6-177">Данный регион также определяет и ограничивает расположение, в котором вы можете создать ресурс Azure для шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="7bfd6-178">Поэтому при создании ресурса шлюза в Azure убедитесь, что расположение этого ресурса соответствует региону, выбранному во время установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="7bfd6-179">Если в дальнейшем потребуется использовать для шлюза другой регион, необходимо будет настроить новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="7bfd6-180">Когда вы будете готовы, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="7bfd6-181">Теперь выполните приведенные ниже инструкции на портале Azure, чтобы [создать ресурс Azure для шлюза](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="7bfd6-182">Дополнительные сведения см. в разделе [Как работает шлюз](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="7bfd6-183">Перенос, восстановление или перехват существующего шлюза</span><span class="sxs-lookup"><span data-stu-id="7bfd6-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="7bfd6-184">Для выполнения этих задач необходим ключ восстановления, который был указан во время установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="7bfd6-185">В меню "Пуск" компьютера выберите **Локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="7bfd6-186">После открытия установщика войдите с помощью той же рабочей или учебной учетной записи Azure, которая использовалась при установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="7bfd6-187">Выберите **Migrate, restore, or take over an existing gateway** (Перенос, восстановление или перехват имеющегося шлюза).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="7bfd6-188">Укажите имя и ключ восстановления для шлюза, который вы хотите перенести, восстановить или перехватить.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="7bfd6-189">Перезапуск шлюза</span><span class="sxs-lookup"><span data-stu-id="7bfd6-189">Restart the gateway</span></span>

<span data-ttu-id="7bfd6-190">Шлюз работает как служба Windows.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="7bfd6-191">Как и любая другая служба Windows, служба шлюза может быть запущена и остановлена различными способами.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="7bfd6-192">Например, можно открыть командную строку с дополнительными разрешениями на компьютере, на котором выполняется шлюз, и выполнить одну из команд, приведенных ниже.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="7bfd6-193">Чтобы остановить службу, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="7bfd6-194">Чтобы запустить службу, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="7bfd6-195">Учетная запись службы Windows</span><span class="sxs-lookup"><span data-stu-id="7bfd6-195">Windows service account</span></span>

<span data-ttu-id="7bfd6-196">Локальный шлюз данных настроен для использования `NT SERVICE\PBIEgwService` в качестве учетных данных входа службы Windows.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="7bfd6-197">По умолчанию шлюзу предоставляется право "входа в качестве службы" для компьютера, на котором он установлен.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="7bfd6-198">Учетная запись службы Windows отличается от учетной записи, которая использовалась для подключения к локальным источникам данных, и от рабочей или учебной учетной записи, которая использовалась для входа в облачные службы.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="7bfd6-199">Настройка брандмауэра или прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="7bfd6-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="7bfd6-200">Шлюз создает исходящее подключение к [служебной шине Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="7bfd6-201">Сведения о том, как предоставить данные прокси-сервера для шлюза, см. в статье [Настройка параметров прокси-сервера для локального шлюза данных](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="7bfd6-202">Чтобы проверить, не блокирует ли брандмауэр или прокси-сервер подключения, проверьте, действительно ли компьютер может подключиться к Интернету и [служебной шине Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="7bfd6-203">В командной строке PowerShell выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="7bfd6-204">Эта команда только проверяет возможность подключения к сети и служебной шине Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="7bfd6-205">Поэтому данная команда не относится к шлюзу или облачной службе шлюза, которая шифрует и хранит учетные данные и сведения о шлюзах.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="7bfd6-206">Кроме того, эта команда используется только в Windows Server 2012 R2 или более поздней версии и Windows 8.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="7bfd6-207">В более ранних версиях ОС для проверки возможности подключения можно использовать Telnet.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="7bfd6-208">Узнайте больше о [служебной шине Azure и гибридных решениях](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="7bfd6-209">Результаты должны выглядеть примерно как в приведенном примере.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-209">Your results should look similar to this example:</span></span>

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

<span data-ttu-id="7bfd6-210">Если значение **TcpTestSucceeded** не равно **True**, возможно, подключения блокируются брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="7bfd6-211">Чтобы обеспечить исчерпывающие сведения, замените значения параметров **ComputerName** и **Port** значениями, приведенными ниже в подразделе [Настройка портов](#configure-ports).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="7bfd6-212">Брандмауэр может также блокировать подключения, устанавливаемые служебной шиной Azure с центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="7bfd6-213">В этом случае разрешите (разблокируйте) все IP-адреса этих центров обработки данных в своем регионе.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="7bfd6-214">Чтобы узнать эти IP-адреса, [получите список IP-адресов Azure здесь](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="7bfd6-215">Настройка портов</span><span class="sxs-lookup"><span data-stu-id="7bfd6-215">Configure ports</span></span>

<span data-ttu-id="7bfd6-216">Шлюз создает исходящее подключение к [служебной шине Azure](https://azure.microsoft.com/services/service-bus/) и осуществляет связь через исходящие порты: TCP-порты 443 (по умолчанию), 5671, 5672 и 9350–9354.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="7bfd6-217">Шлюзу не требуются входящие порты.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="7bfd6-218">Узнайте больше о [служебной шине Azure и гибридных решениях](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="7bfd6-219">ДОМЕННЫЕ ИМЕНА</span><span class="sxs-lookup"><span data-stu-id="7bfd6-219">DOMAIN NAMES</span></span> | <span data-ttu-id="7bfd6-220">ИСХОДЯЩИЕ ПОРТЫ</span><span class="sxs-lookup"><span data-stu-id="7bfd6-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="7bfd6-221">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="7bfd6-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7bfd6-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-222">*.analysis.windows.net</span></span> | <span data-ttu-id="7bfd6-223">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-223">443</span></span> | <span data-ttu-id="7bfd6-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfd6-224">HTTPS</span></span> | 
| <span data-ttu-id="7bfd6-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-225">*.login.windows.net</span></span> | <span data-ttu-id="7bfd6-226">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-226">443</span></span> | <span data-ttu-id="7bfd6-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfd6-227">HTTPS</span></span> | 
| <span data-ttu-id="7bfd6-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="7bfd6-229">5671–5672</span><span class="sxs-lookup"><span data-stu-id="7bfd6-229">5671-5672</span></span> | <span data-ttu-id="7bfd6-230">Протокол AMQP</span><span class="sxs-lookup"><span data-stu-id="7bfd6-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="7bfd6-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="7bfd6-232">443, 9350–9354</span><span class="sxs-lookup"><span data-stu-id="7bfd6-232">443, 9350-9354</span></span> | <span data-ttu-id="7bfd6-233">Прослушиватели ретрансляции служебной шины по протоколу TCP (порт 443 требуется для получения маркера контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="7bfd6-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="7bfd6-235">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-235">443</span></span> | <span data-ttu-id="7bfd6-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfd6-236">HTTPS</span></span> | 
| <span data-ttu-id="7bfd6-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7bfd6-237">*.core.windows.net</span></span> | <span data-ttu-id="7bfd6-238">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-238">443</span></span> | <span data-ttu-id="7bfd6-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfd6-239">HTTPS</span></span> | 
| <span data-ttu-id="7bfd6-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7bfd6-240">login.microsoftonline.com</span></span> | <span data-ttu-id="7bfd6-241">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-241">443</span></span> | <span data-ttu-id="7bfd6-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="7bfd6-242">HTTPS</span></span> | 
| <span data-ttu-id="7bfd6-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="7bfd6-243">*.msftncsi.com</span></span> | <span data-ttu-id="7bfd6-244">443</span><span class="sxs-lookup"><span data-stu-id="7bfd6-244">443</span></span> | <span data-ttu-id="7bfd6-245">Используется для проверки подключения к Интернету, если шлюз недоступен для службы Power BI.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="7bfd6-246">Если требуется утвердить IP-адреса, а не домены, то можно скачать и использовать [список диапазонов IP-адресов центров обработки данных Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="7bfd6-247">В некоторых случаях подключения к служебной шине Azure будут устанавливаться по IP-адресу, а не полному доменному имени.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="7bfd6-248">Как работает шлюз данных?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-248">How does the data gateway work?</span></span>

<span data-ttu-id="7bfd6-249">Шлюз данных обеспечивает быстрый и безопасный обмен данными между приложением логики, облачной службой шлюза и локальным источником данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="7bfd6-251">Когда пользователь в облаке взаимодействует с элементом, подключенным к локальному источнику данных, происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="7bfd6-252">Облачная служба шлюза создает запрос, а также зашифрованные учетные данные для источника данных, и отправляет запрос в очередь для обработки шлюзом.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="7bfd6-253">Облачная служба шлюза анализирует запрос и отправляет его в служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="7bfd6-254">Локальный шлюз данных опрашивает служебную шину Azure, чтобы проверить наличие ожидающих запросов.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="7bfd6-255">Шлюз получает запрос, расшифровывает учетные данные и подключается к источникам данных, используя эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="7bfd6-256">Затем шлюз отправляет запрос к источнику данных для выполнения.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="7bfd6-257">Результаты отправляются из источника данных обратно в шлюз, а затем — в облачную службу шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="7bfd6-258">Затем облачная служба шлюза использует эти результаты.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="7bfd6-259">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="7bfd6-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="7bfd6-260">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="7bfd6-260">General</span></span>

<span data-ttu-id="7bfd6-261">**Вопрос**. Нужно ли устанавливать шлюз для источников данных в облаке, например SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="7bfd6-262">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-262">
**A**: No.</span></span> <span data-ttu-id="7bfd6-263">Шлюз подключается только к локальным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="7bfd6-264">**Вопрос**. Нужно ли устанавливать шлюз на том же компьютере, на котором находится источник данных?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="7bfd6-265">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-265">
**A**: No.</span></span> <span data-ttu-id="7bfd6-266">Шлюз подключается к источнику данных, используя предоставленные сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="7bfd6-267">В этом смысле шлюз можно рассматривать как клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="7bfd6-268">Ему просто необходима возможность подключения к серверу, имя которого было предоставлено.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="7bfd6-269">**Вопрос**. Почему для входа необходимо использовать рабочую или учебную учетную запись Azure?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="7bfd6-270">
**Ответ**. При установке локального шлюза данных вы можете использовать только рабочую или учебную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="7bfd6-271">Учетная запись для входа хранится в клиенте, которым управляет Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bfd6-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7bfd6-272">Как правило, имя участника-пользователя учетной записи Azure AD совпадает с адресом электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="7bfd6-273">**Вопрос**. Где хранятся мои учетные данные?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="7bfd6-274">
**Ответ**. Учетные данные, введенные для источника данных, хранятся в облачной службе шлюза в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="7bfd6-275">Расшифровываются они в локальном шлюзе данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="7bfd6-276">**Вопрос**. Есть ли какие-либо требования к пропускной способности сети?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="7bfd6-277">
**Ответ**. Пропускная способность сети должна быть высокой.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="7bfd6-278">Все среды разные и объем отправляемых данных влияет на результаты.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="7bfd6-279">Гарантировать определенный уровень пропускной способности между локальной средой и центрами обработки данных Azure может помочь применение ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="7bfd6-280">Измерить текущую пропускную способность можно с помощью стороннего инструмента — приложения Azure Speed Test.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="7bfd6-281">**Вопрос**. Что такое задержка при выполнении запросов к источнику данных из шлюза?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="7bfd6-282">Какая архитектура подойдет лучше всего?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-282">What is the best architecture?</span></span> <br/><span data-ttu-id="7bfd6-283">
**Ответ**. Чтобы уменьшить задержки в сети, необходимо установить шлюз как можно ближе к источнику данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="7bfd6-284">Вы можете установить шлюз на фактический источник данных, что сведет к минимуму соответствующие задержки.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="7bfd6-285">Для этого также стоит рассмотреть центры обработки данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-285">Consider the datacenters too.</span></span> <span data-ttu-id="7bfd6-286">Например, если служба использует центр обработки данных в западной части США, а SQL Server размещен на виртуальной машине Azure, то эту виртуальную машину лучше также разместить в западной части США.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="7bfd6-287">Это позволит свести к минимуму задержки и избежать затрат на исходящий трафик виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="7bfd6-288">**Вопрос**. Как результаты отправляются обратно в облако?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="7bfd6-289">
**Ответ**. Результаты отправляются с помощью служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="7bfd6-290">**Вопрос**. Устанавливаются ли какие-либо входящие подключения к шлюзу из облака?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="7bfd6-291">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-291">
**A**: No.</span></span> <span data-ttu-id="7bfd6-292">Шлюз использует исходящие подключения к служебной шине Azure.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="7bfd6-293">**Вопрос**. Что делать, если мной заблокированы исходящие подключения?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="7bfd6-294">Что нужно открыть?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-294">What do I need to open?</span></span> <br/><span data-ttu-id="7bfd6-295">
**Ответ**. Проверьте порты и узлы, которые использует шлюз.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="7bfd6-296">**Вопрос**. Как на самом деле называется служба Windows?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="7bfd6-297">
**Ответ**. В списке служб шлюз называется "Служба Power BI Enterprise Gateway".</span><span class="sxs-lookup"><span data-stu-id="7bfd6-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="7bfd6-298">**Вопрос**. Может ли служба Windows шлюза работать с учетной записью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="7bfd6-299">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-299">
**A**: No.</span></span> <span data-ttu-id="7bfd6-300">Службе Windows требуется действительная учетная запись Windows.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="7bfd6-301">По умолчанию служба будет выполняться с идентификатором безопасности службы NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="7bfd6-302">Высокий уровень доступности и аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="7bfd6-302">High availability and disaster recovery</span></span>

<span data-ttu-id="7bfd6-303">**Вопрос**. Какие варианты доступны для аварийного восстановления?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="7bfd6-304">
**Ответ**. Вы можете использовать ключ восстановления для восстановления или переноса шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="7bfd6-305">Ключ восстановления указывается при установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="7bfd6-306">**Вопрос**. В чем заключается преимущество ключа восстановления?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="7bfd6-307">
**Ответ.** Он позволяет перенести шлюз или восстановить его параметры после аварии.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="7bfd6-308">**Вопрос**. Существуют ли какие-либо планы по реализации сценариев высокого уровня доступности с помощью шлюза?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="7bfd6-309">
**Ответ**. Это входит в наши планы, однако со сроками в этом отношении мы еще не определились.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7bfd6-310">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7bfd6-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="7bfd6-311">**Вопрос**. Как узнать, какие запросы отправляются к локальному источнику данных?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="7bfd6-312">
**Ответ**. Вы можете включить трассировку запросов, в том числе и отправляемых.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="7bfd6-313">Не забудьте вернуть исходное значение трассировки запросов после устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="7bfd6-314">При включенной трассировке запросов создаются журналы большего размера.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="7bfd6-315">Кроме того, можно рассмотреть инструменты трассировки запросов, доступные для вашего источника данных.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="7bfd6-316">Например, можно использовать расширенные события или SQL Profiler для SQL Server и служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="7bfd6-317">**Вопрос**. Где находятся журналы шлюза?</span><span class="sxs-lookup"><span data-stu-id="7bfd6-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="7bfd6-318">
**Ответ**. См. раздел "Средства" далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="7bfd6-319">Обновление до последней версии</span><span class="sxs-lookup"><span data-stu-id="7bfd6-319">Update to the latest version</span></span>

<span data-ttu-id="7bfd6-320">При использовании устаревшей версии шлюза может возникать ряд проблем.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="7bfd6-321">Рекомендуем убедиться, что используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="7bfd6-322">Если шлюз не обновлялся месяц или дольше, то можно установить его последнюю версию и проверить, получится ли воспроизвести проблему.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="7bfd6-323">Error: Failed to add user to group. (Ошибка: не удалось добавить пользователя в группу.)</span><span class="sxs-lookup"><span data-stu-id="7bfd6-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="7bfd6-324">(-2147463168 PBIEgwService Performance Log Users ) (-2147463168 пользователей журналов производительности PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="7bfd6-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="7bfd6-325">Эта ошибка появляется, если вы пытаетесь установить шлюз на контроллер домена, который не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="7bfd6-326">Убедитесь, что развертывание шлюза происходит на компьютере, который не является контроллером домена.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="7bfd6-327">Средства</span><span class="sxs-lookup"><span data-stu-id="7bfd6-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="7bfd6-328">Сбор журналов из конфигуратора шлюза</span><span class="sxs-lookup"><span data-stu-id="7bfd6-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="7bfd6-329">Вы можете собирать несколько журналов для шлюза.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="7bfd6-330">Всегда начинайте с журналов!</span><span class="sxs-lookup"><span data-stu-id="7bfd6-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="7bfd6-331">Журналы установщика</span><span class="sxs-lookup"><span data-stu-id="7bfd6-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="7bfd6-332">Журналы конфигурации</span><span class="sxs-lookup"><span data-stu-id="7bfd6-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="7bfd6-333">Журналы службы корпоративного шлюза</span><span class="sxs-lookup"><span data-stu-id="7bfd6-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="7bfd6-334">Журналы событий</span><span class="sxs-lookup"><span data-stu-id="7bfd6-334">Event logs</span></span>

<span data-ttu-id="7bfd6-335">Журналы шлюза управления данными и PowerBIGateway находятся в разделе **Журналы приложения и служб**.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="7bfd6-336">Трассировки Fiddler</span><span class="sxs-lookup"><span data-stu-id="7bfd6-336">Fiddler Trace</span></span>

<span data-ttu-id="7bfd6-337">[Fiddler](http://www.telerik.com/fiddler) — это бесплатный инструмент от компании Telerik, который отслеживает трафик HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="7bfd6-338">Вы можете просматривать данные с помощью службы Power BI с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="7bfd6-339">Эта служба позволит выявить ошибки и другие сопутствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="7bfd6-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bfd6-340">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bfd6-340">Next steps</span></span>
    
* [<span data-ttu-id="7bfd6-341">Подключение к локальным данным из приложений логики</span><span class="sxs-lookup"><span data-stu-id="7bfd6-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="7bfd6-342">Возможности интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="7bfd6-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="7bfd6-343">Список соединителей</span><span class="sxs-lookup"><span data-stu-id="7bfd6-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
