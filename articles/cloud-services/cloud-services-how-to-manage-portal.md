---
title: "задачи управления aaaCommon облачные службы | Документы Microsoft"
description: "Узнайте, как toomanage облачных служб в hello портал Azure. В этих примерах используются hello портал Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="ca8cd-104">Как tooManage облачных служб</span><span class="sxs-lookup"><span data-stu-id="ca8cd-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca8cd-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ca8cd-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="ca8cd-106">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="ca8cd-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="ca8cd-107">В hello **облачные службы (классические)** области hello Azure портала, можно обновить роли службы или развертывание, повышение уровня tooproduction промежуточное развертывание, связать ресурсы tooyour облачной службы, чтобы вы могли видеть hello ресурсов зависимости и масштаб hello ресурсы вместе и удалите облачной службы или типа развертывания.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="ca8cd-108">Дополнительные сведения о том, как tooscale облачной службы доступны [здесь](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="ca8cd-109">Практическое руководство. Обновление роли облачной службы или развертывания</span><span class="sxs-lookup"><span data-stu-id="ca8cd-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="ca8cd-110">Если код приложения hello tooupdate требуется для облачной службы, используйте **обновление** hello облачной службы колонке.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="ca8cd-111">Одновременно можно обновить как одну, так и все роли.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-111">You can update a single role or all roles.</span></span> <span data-ttu-id="ca8cd-112">tooupdate, можно отправить новый пакет служб или файл конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="ca8cd-113">В hello [портал Azure][Azure portal], выберите облачную службу hello требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="ca8cd-114">Это действие открывает hello облачной службы экземпляра колонку.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="ca8cd-115">В колонке hello щелкните hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-115">In hello blade, click hello **Update** button.</span></span>

    ![Кнопка «Обновить»](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="ca8cd-117">Обновление развертывания hello новый файл пакета службы (cspkg-файл) и файл конфигурации службы (cscfg).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![Обновление развертывания](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="ca8cd-119">**При необходимости** обновить метку развертывания hello и hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="ca8cd-120">Если ни одной роли имеет только один экземпляр роли, выберите hello **развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** обновления tooproceed tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="ca8cd-121">Служба Azure гарантирует доступность облачной службы в течение 99,95 % времени, только если для каждой роли определены как минимум два экземпляра (виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="ca8cd-122">Двух экземпляров роли во время обновления hello других одну виртуальную машину для обработки клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="ca8cd-123">Проверьте **запустить развертывание** toohave hello исправления после завершения отправки hello hello пакета.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="ca8cd-124">Нажмите кнопку **ОК** toobegin обновление службы hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="ca8cd-125">Как: замены развертываний toopromote tooproduction поэтапного развертывания</span><span class="sxs-lookup"><span data-stu-id="ca8cd-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="ca8cd-126">При решить toodeploy новый выпуск облачной службы, этап и тестирование нового выпуска в облачной среде размещения службы.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="ca8cd-127">Используйте **замены** tooswitch hello URL-адреса, рассматриваются два развертывания какие hello и повышения уровня нового tooproduction выпуска.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="ca8cd-128">Можно менять развертываний hello **облачные службы** страницы или hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="ca8cd-129">В hello [портал Azure][Azure portal], выберите облачную службу hello требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="ca8cd-130">Это действие открывает hello облачной службы экземпляра колонку.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="ca8cd-131">В колонке hello щелкните hello **замены** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-131">In hello blade, click hello **Swap** button.</span></span>

    ![Переключение облачных служб](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="ca8cd-133">Hello следующий запрос подтверждения открывается.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-133">hello following confirmation prompt opens.</span></span>

    ![Переключение облачных служб](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="ca8cd-135">После проверки информации о hello развертывания, нажмите кнопку **ОК** tooswap hello развертываний.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="ca8cd-136">Hello переключения развертывания происходит быстро, так как hello единственное, что изменения — hello виртуальных IP-адресов (VIP) для развертываний hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="ca8cd-137">toosave расходы, можно удалить промежуточное развертывание, когда вы убедитесь, что рабочее развертывание работает надлежащим образом hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="ca8cd-138">Часто задаваемые вопросы о переключении развертываний</span><span class="sxs-lookup"><span data-stu-id="ca8cd-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="ca8cd-139">**Что такое hello необходимые условия для замены развертываний**</span><span class="sxs-lookup"><span data-stu-id="ca8cd-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="ca8cd-140">Существует два ключевых требования для успешного переключения развертываний.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="ca8cd-141">Если вы хотите toouse статический IP-адрес для вашего производственный слот, необходимо зарезервировать для промежуточного слота также.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="ca8cd-142">В противном случае происходит сбой замены hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="ca8cd-143">Все экземпляры роли должна быть запущена перед выполнением переключения hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="ca8cd-144">Можно проверить состояние hello ваших экземпляров в колонке Обзор hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="ca8cd-145">Кроме того, можно использовать hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="ca8cd-146">Обратите внимание, что обновлений гостевой ОС и восстановления операции службы также может привести к развертывания меняет toofail.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="ca8cd-147">Дополнительные сведения см. в статье [Устранение неполадок, которые могут возникнуть при развертывании облачной службы](cloud-services-troubleshoot-deployment-problems.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="ca8cd-148">**Увеличивают ли переключения время простоя приложения? Что делать в этом случае?**</span><span class="sxs-lookup"><span data-stu-id="ca8cd-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="ca8cd-149">Как описано в последнем разделе hello переключения развертывания обычно быстрый, так как она является только изменение конфигурации в подсистеме балансировки нагрузки Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="ca8cd-150">В некоторых случаях, однако, это может занять около десяти секунд и привести к временному сбою подключения.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="ca8cd-151">toolimit влияние tooyour клиентов, рассмотрите возможность реализации [логику повторных попыток клиента](../best-practices-retry-general.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="ca8cd-152">Как: связать tooa ресурсов облачной службы</span><span class="sxs-lookup"><span data-stu-id="ca8cd-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="ca8cd-153">Hello портал Azure не содержит ссылок на ресурсы вместе, как и hello текущего классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="ca8cd-154">Вместо этого развертывайте дополнительные ресурсы toohello же группе ресурсов, используемых hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="ca8cd-155">Практическое руководство. Удаление развертываний и облачной службы</span><span class="sxs-lookup"><span data-stu-id="ca8cd-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="ca8cd-156">До удаления облачной службы необходимо удалить все текущие развертывания.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="ca8cd-157">toosave расходы, можно удалить промежуточное развертывание, когда вы убедитесь, что рабочее развертывание работает надлежащим образом hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="ca8cd-158">Вам выставляются счета за вычислительные ресурсы развернутых экземпляров роли, которые остановлены.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="ca8cd-159">Используйте следующие процедуры toodelete hello развертывания или облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="ca8cd-160">В hello [портал Azure][Azure portal], выберите облачную службу hello требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="ca8cd-161">Это действие открывает hello облачной службы экземпляра колонку.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="ca8cd-162">В колонке hello щелкните hello **удалить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-162">In hello blade, click hello **Delete** button.</span></span>

    ![Переключение облачных служб](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="ca8cd-164">Можно удалить hello всей облачной службы путем проверки **облачная служба и ее развертывания** или выберите либо hello **рабочего развертывания** или hello **промежуточное развертывание**.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Переключение облачных служб](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="ca8cd-166">Нажмите кнопку hello **удалить** кнопку в нижней части hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="ca8cd-167">toodelete hello облачной службы, нажмите кнопку **удаления облачной службы**.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="ca8cd-168">Щелкните в hello подтверждения **Да**.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="ca8cd-169">При удалении облачной службы и подробный мониторинг был настроен, необходимо вручную удалить hello данные из вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="ca8cd-170">Сведения о toofind Здравствуйте таблицах метрик, где содержатся [это](cloud-services-how-to-monitor.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="ca8cd-171">Практическое руководство: поиск дополнительных сведений об ошибках развертывания</span><span class="sxs-lookup"><span data-stu-id="ca8cd-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="ca8cd-172">Hello **Обзор** колонке используется строка состояния вверху hello.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="ca8cd-173">Если щелкнуть панель hello, Новая колонка открывает и отображает сведения о любых ошибках.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="ca8cd-174">Если развертывание hello не содержит ошибок, колонки сведений hello пусто.</span><span class="sxs-lookup"><span data-stu-id="ca8cd-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Переключение облачных служб](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="ca8cd-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca8cd-176">Next steps</span></span>
* <span data-ttu-id="ca8cd-177">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="ca8cd-178">Узнайте, каким образом слишком[развертывание облачной службы](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="ca8cd-179">Настройте [пользовательское доменное имя](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="ca8cd-180">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ca8cd-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
