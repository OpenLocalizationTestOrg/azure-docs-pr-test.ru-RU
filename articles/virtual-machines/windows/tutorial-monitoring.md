---
title: "aaaAzure мониторинг и виртуальных машинах | Документы Microsoft"
description: "Руководство по мониторингу виртуальных машин Windows с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="cec2e-103">Мониторинг виртуальных машин Windows с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cec2e-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="cec2e-104">Мониторинг Azure использует агенты toocollect загрузки и данные о производительности из виртуальных машин Azure, сохранение этих данных в хранилище Azure и сделать доступными через портал, модуля Azure PowerShell hello и hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cec2e-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="cec2e-105">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="cec2e-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cec2e-106">Включение диагностики загрузки на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="cec2e-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="cec2e-107">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="cec2e-107">View boot diagnostics</span></span>
> * <span data-ttu-id="cec2e-108">Просмотр метрик узла виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-108">View VM host metrics</span></span>
> * <span data-ttu-id="cec2e-109">Установка расширения диагностики hello</span><span class="sxs-lookup"><span data-stu-id="cec2e-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="cec2e-110">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-110">View VM metrics</span></span>
> * <span data-ttu-id="cec2e-111">Создание оповещения</span><span class="sxs-lookup"><span data-stu-id="cec2e-111">Create an alert</span></span>
> * <span data-ttu-id="cec2e-112">Настройка расширенного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cec2e-112">Set up advanced monitoring</span></span>

<span data-ttu-id="cec2e-113">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="cec2e-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="cec2e-114">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="cec2e-115">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cec2e-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="cec2e-116">Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="cec2e-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="cec2e-117">Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="cec2e-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="cec2e-118">При работе в учебнике hello, замените hello группы ресурсов, имя виртуальной Машины и расположение при необходимости.</span><span class="sxs-lookup"><span data-stu-id="cec2e-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="cec2e-119">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="cec2e-119">View boot diagnostics</span></span>

<span data-ttu-id="cec2e-120">Как загрузиться виртуальных машинах агент диагностики загрузки hello захватывает экране, который можно использовать для устранения неполадок цели.</span><span class="sxs-lookup"><span data-stu-id="cec2e-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="cec2e-121">Эта возможность включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cec2e-121">This capability is enabled by default.</span></span> <span data-ttu-id="cec2e-122">Hello захвата экрана, снимки хранятся в учетной записи хранилища Azure, которая также создается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cec2e-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="cec2e-123">Можно получить данные диагностики загрузки hello с hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) команды.</span><span class="sxs-lookup"><span data-stu-id="cec2e-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="cec2e-124">В следующем примере hello, диагностика загрузки являются корнем загруженный toohello hello * c:\* диска.</span><span class="sxs-lookup"><span data-stu-id="cec2e-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="cec2e-125">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="cec2e-125">View host metrics</span></span>

<span data-ttu-id="cec2e-126">Виртуальная машина Windows имеет выделенный узел виртуальной машины в Azure, с которым она взаимодействует.</span><span class="sxs-lookup"><span data-stu-id="cec2e-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="cec2e-127">Метрики автоматически собираются для hello узла и могут просматриваться в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cec2e-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="cec2e-128">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="cec2e-129">Нажмите кнопку **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик узла hello под **доступные метрики** toosee, как работает hello виртуальной Машины для узла.</span><span class="sxs-lookup"><span data-stu-id="cec2e-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Просмотр метрик узла.](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="cec2e-131">Установка расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="cec2e-131">Install diagnostics extension</span></span>

<span data-ttu-id="cec2e-132">Hello узла основные метрики доступны, но toosee более детального и метрики конкретной виртуальной Машины, вы tooneed tooinstall hello Azure расширение диагностики в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cec2e-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="cec2e-133">Hello расширения службы диагностики Azure позволяет дополнительные функции мониторинга и диагностики toobe данные, полученные из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cec2e-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="cec2e-134">Можно просматривать эти метрики производительности и создание предупреждений в зависимости от того, как выполняется hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cec2e-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="cec2e-135">Hello диагностического расширения устанавливаются с помощью портала Azure hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cec2e-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="cec2e-136">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="cec2e-137">Щелкните **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="cec2e-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="cec2e-138">Показывает, что список Hello *загрузки диагностики* уже включены в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="cec2e-139">Установите флажок hello для *базовые показатели*.</span><span class="sxs-lookup"><span data-stu-id="cec2e-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="cec2e-140">Нажмите кнопку hello **Включите мониторинг на уровне гостя** кнопки.</span><span class="sxs-lookup"><span data-stu-id="cec2e-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Просмотр метрик диагностики](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="cec2e-142">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-142">View VM metrics</span></span>

<span data-ttu-id="cec2e-143">Можно просмотреть метрики виртуальной Машины hello в hello просмотрены показателей виртуальной Машины узла hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cec2e-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="cec2e-144">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="cec2e-145">toosee о выполнении hello виртуальной Машины, щелкните **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик hello диагностики в разделе **доступные метрики**.</span><span class="sxs-lookup"><span data-stu-id="cec2e-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Просмотр метрик виртуальной машины](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="cec2e-147">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="cec2e-147">Create alerts</span></span>

<span data-ttu-id="cec2e-148">На основе метрик производительности можно создавать оповещения.</span><span class="sxs-lookup"><span data-stu-id="cec2e-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="cec2e-149">Предупреждения может быть используется toonotify, когда средняя загрузка ЦП превышает пороговое значение или свободного дискового пространства падает ниже определенного, например.</span><span class="sxs-lookup"><span data-stu-id="cec2e-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="cec2e-150">Оповещения отображаются в hello портал Azure или могут отправляться по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="cec2e-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="cec2e-151">Вы можете запускать Runbook автоматизации Azure или логику приложения Azure в создаваемый tooalerts ответа.</span><span class="sxs-lookup"><span data-stu-id="cec2e-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="cec2e-152">Hello следующий пример создает оповещение о среднем использовании ЦП.</span><span class="sxs-lookup"><span data-stu-id="cec2e-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="cec2e-153">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="cec2e-154">Нажмите кнопку **предупреждения правила** hello колонки виртуальной Машины, затем щелкните **добавить оповещение метрики** hello верхней части колонки hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="cec2e-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="cec2e-155">Укажите **имя** оповещения, например *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="cec2e-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="cec2e-156">tootrigger предупреждение, если процент использования ЦП превышает 1.0 на пять минут, оставьте hello все остальные значения по умолчанию выбран.</span><span class="sxs-lookup"><span data-stu-id="cec2e-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="cec2e-157">При необходимости установите флажок "hello" для *электронной почты, владельцы, участники и читатели* toosend уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="cec2e-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="cec2e-158">Действие по умолчанию Hello — toopresent уведомления на портале hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="cec2e-159">Нажмите кнопку hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="cec2e-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="cec2e-160">Расширенный мониторинг</span><span class="sxs-lookup"><span data-stu-id="cec2e-160">Advanced monitoring</span></span> 

<span data-ttu-id="cec2e-161">Более сложный мониторинг виртуальной машины можно выполнить с помощью [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="cec2e-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="cec2e-162">Зарегистрируйтесь для получения [бесплатной пробной версии](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="cec2e-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="cec2e-163">При наличии портал OMS toohello доступа hello идентификатор рабочей области ключ и рабочей области можно найти в колонке параметров hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="cec2e-164">Используйте hello [набор AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) toohello cmmand tootooadd hello OMS расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cec2e-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="cec2e-165">Переменная hello обновления значений в hello ниже образце tooreflect вы рабочей идентификатор и ключ рабочей области OMS</span><span class="sxs-lookup"><span data-stu-id="cec2e-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="cec2e-166">Через несколько минут вы увидите hello новой виртуальной Машины в рабочей области OMS hello.</span><span class="sxs-lookup"><span data-stu-id="cec2e-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Колонка OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="cec2e-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cec2e-168">Next steps</span></span>
<span data-ttu-id="cec2e-169">В этом руководстве вы выполнили настройку и проверку виртуальных машин с помощью центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="cec2e-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="cec2e-170">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cec2e-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cec2e-171">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="cec2e-171">Create a virtual network</span></span>
> * <span data-ttu-id="cec2e-172">Создание группы ресурсов и виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="cec2e-173">Включить диагностику загрузки на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="cec2e-174">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="cec2e-174">View boot diagnostics</span></span>
> * <span data-ttu-id="cec2e-175">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="cec2e-175">View host metrics</span></span>
> * <span data-ttu-id="cec2e-176">Установка расширения диагностики hello</span><span class="sxs-lookup"><span data-stu-id="cec2e-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="cec2e-177">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cec2e-177">View VM metrics</span></span>
> * <span data-ttu-id="cec2e-178">Создание оповещения</span><span class="sxs-lookup"><span data-stu-id="cec2e-178">Create an alert</span></span>
> * <span data-ttu-id="cec2e-179">Настройка расширенного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cec2e-179">Set up advanced monitoring</span></span>

<span data-ttu-id="cec2e-180">Переместить следующий учебник toolearn toohello относительно центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="cec2e-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cec2e-181">Мониторинг защиты виртуальных машин с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="cec2e-181">Manage VM security</span></span>](./tutorial-azure-security.md)