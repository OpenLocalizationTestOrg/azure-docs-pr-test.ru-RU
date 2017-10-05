---
title: "Мониторинг виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Инструкции по мониторингу диагностических данных загрузки и метрик производительности на виртуальных машинах Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f9bb3-103">Мониторинг виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="f9bb3-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="f9bb3-104">Чтобы убедиться в правильной работе виртуальных машин в Azure, можно просмотреть диагностические данные загрузки и метрики производительности.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="f9bb3-105">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9bb3-106">Включение диагностики загрузки на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="f9bb3-107">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="f9bb3-107">View boot diagnostics</span></span>
> * <span data-ttu-id="f9bb3-108">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-108">View host metrics</span></span>
> * <span data-ttu-id="f9bb3-109">Включение расширения системы диагностики на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="f9bb3-110">Просмотр метрик виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-110">View VM metrics</span></span>
> * <span data-ttu-id="f9bb3-111">Создание оповещений на основе метрик диагностики.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="f9bb3-112">Настройка расширенного мониторинга</span><span class="sxs-lookup"><span data-stu-id="f9bb3-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f9bb3-113">Если вы решили установить и использовать интерфейс командной строки локально, для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f9bb3-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="f9bb3-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="f9bb3-116">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f9bb3-116">Create VM</span></span>

<span data-ttu-id="f9bb3-117">Чтобы увидеть данные диагностики и метрики в действии, необходима виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="f9bb3-118">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f9bb3-119">В следующем примере создается группа ресурсов с именем *myResourceGroupMonitor* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="f9bb3-120">Теперь создайте виртуальную машину командой [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="f9bb3-121">В следующем примере создается виртуальная машина с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="f9bb3-122">Включение диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="f9bb3-122">Enable boot diagnostics</span></span>

<span data-ttu-id="f9bb3-123">Во время загрузки виртуальных машин Linux расширение системы диагностики записывает выходные данные загрузки и сохраняет их в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="f9bb3-124">Эти данные можно использовать для устранения неполадок загрузки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="f9bb3-125">При создании виртуальной машины Linux с помощью Azure CLI диагностика загрузки не включается автоматически.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="f9bb3-126">Перед включением диагностики загрузки необходимо создать учетную запись хранения для хранения журналов загрузки.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="f9bb3-127">Имена учетных записей хранения должны быть глобально уникальными, иметь длину от 3 до 24 символов и содержать только цифры и буквы в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="f9bb3-128">Создайте учетную запись хранения с помощью команды [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="f9bb3-129">В этом примере для создания уникального имени учетной записи хранения используется случайная строка.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="f9bb3-130">При включении диагностики загрузки необходим URI контейнера хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="f9bb3-131">Следующая команда запрашивает URI учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="f9bb3-132">Значение URI хранится в именах переменных *bloburi*, которые используются на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="f9bb3-133">Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="f9bb3-134">Значение `--storage` — это URI BLOB-объекта, полученный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="f9bb3-135">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="f9bb3-135">View boot diagnostics</span></span>

<span data-ttu-id="f9bb3-136">Если включена диагностика загрузки, каждый раз при остановке и запуске виртуальной машины сведения о процессе загрузки записываются в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="f9bb3-137">В этом примере сначала освободите виртуальную машину с помощью команды [az vm deallocate](/cli/azure/vm#deallocate) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="f9bb3-138">Теперь запустите виртуальную машину с помощью команды [az vm start]( /cli/azure/vm#stop) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="f9bb3-139">Данные диагностики загрузки для *myVM* можно получить с помощью команды [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="f9bb3-140">Просмотр метрик узла</span><span class="sxs-lookup"><span data-stu-id="f9bb3-140">View host metrics</span></span>

<span data-ttu-id="f9bb3-141">Виртуальная машина Linux имеет выделенный узел в Azure, с которым она взаимодействует.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="f9bb3-142">Метрики узла собираются автоматически и их можно просмотреть на портале Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="f9bb3-143">На портале Azure щелкните **Группы ресурсов**, выберите **myResourceGroupMonitor**, а затем в списке ресурсов выберите **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="f9bb3-144">Чтобы увидеть, как работает узел виртуальной машины, в колонке виртуальной машины щелкните **Метрики**, а затем выберите любую метрику *узла* в группе **Доступные метрики**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![Просмотр метрик узла](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="f9bb3-146">Установка расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="f9bb3-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9bb3-147">В этом документе описывается версия 2.3 диагностического расширения для Linux, которая признана нерекомендуемой.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="f9bb3-148">Версия 2.3 будет поддерживаться до 30 июня 2018 г.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="f9bb3-149">Вместо нее можно включить диагностическое расширение для Linux версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="f9bb3-150">Дополнительные сведения см. в [документации](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="f9bb3-151">По умолчанию доступны основные метрики узла. Чтобы просмотреть более детальные метрики определенной виртуальной машины, требуется установить расширение системы диагностики Azure,</span><span class="sxs-lookup"><span data-stu-id="f9bb3-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="f9bb3-152">позволяющее получать дополнительные данные мониторинга и диагностики виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="f9bb3-153">С помощью этих метрик производительности можно создать уведомления с учетом работы виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="f9bb3-154">Расширение системы диагностики устанавливается на портале Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="f9bb3-155">На портале Azure щелкните **Группы ресурсов**, выберите **myResourceGroup**, а затем **myVM** в списке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="f9bb3-156">Щелкните **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="f9bb3-157">В списке будет указано, что *диагностика загрузки* уже включена в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="f9bb3-158">Установите флажок для параметра *Базовые метрики*.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="f9bb3-159">В разделе *Учетные записи хранения* найдите и выберите учетную запись *mydiagdata[1234]*, созданную при работе с предыдущим разделом.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="f9bb3-160">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f9bb3-160">Click the **Save** button.</span></span>

    ![Просмотр метрик диагностики](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="f9bb3-162">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f9bb3-162">View VM metrics</span></span>

<span data-ttu-id="f9bb3-163">Метрики виртуальной машины можно просмотреть аналогично метрикам узла виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="f9bb3-164">На портале Azure щелкните **Группы ресурсов**, выберите **myResourceGroup**, а затем **myVM** в списке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="f9bb3-165">Чтобы увидеть, как работает виртуальная машина, в колонке виртуальной машины щелкните **Метрики**, затем выберите любую метрику диагностики в группе **Доступные метрики**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Просмотр метрик виртуальной машины](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="f9bb3-167">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="f9bb3-167">Create alerts</span></span>

<span data-ttu-id="f9bb3-168">На основе метрик производительности можно создавать оповещения.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="f9bb3-169">Например, оповещения можно использовать для уведомления о том, что средняя загрузка ЦП превышает пороговое значение или свободное место на диске ниже определенного значения.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="f9bb3-170">Оповещения отображаются на портале Azure или могут быть отправлены по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="f9bb3-171">Вы также можете активировать модули Runbook службы автоматизации Azure или Azure Logic Apps в ответ на создаваемые оповещения.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="f9bb3-172">В следующем примере создается предупреждение на основе среднего показателя использования ЦП.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="f9bb3-173">На портале Azure щелкните **Группы ресурсов**, выберите **myResourceGroup**, а затем **myVM** в списке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="f9bb3-174">В колонке виртуальной машины щелкните **Правила оповещения**, а затем выберите **Добавить оповещение метрики**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="f9bb3-175">Укажите **имя** оповещения, например *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="f9bb3-176">Для активации оповещения о превышении процента использования ЦП на 1.0 в течение пяти минут оставьте все настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="f9bb3-177">При необходимости установите флажок возле параметра *Участники, читатели и владельцы электронной почты* для отправки уведомлений по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="f9bb3-178">Действие по умолчанию — предоставлять уведомления на портале.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="f9bb3-179">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="f9bb3-180">Расширенный мониторинг</span><span class="sxs-lookup"><span data-stu-id="f9bb3-180">Advanced monitoring</span></span> 

<span data-ttu-id="f9bb3-181">Более сложный мониторинг виртуальной машины можно выполнить с помощью [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="f9bb3-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="f9bb3-182">Зарегистрируйтесь для получения [бесплатной пробной версии](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="f9bb3-183">При наличии доступа к порталу OMS ключи и идентификатор рабочей области можно найти в колонке "Параметры".</span><span class="sxs-lookup"><span data-stu-id="f9bb3-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="f9bb3-184">Замените <workspace-key> и <workspace-id> значениями рабочей области OMS, а затем воспользуйтесь командой **az vm extension set**, чтобы добавить расширение OMS на виртуальную машину:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="f9bb3-185">В колонке "Поиск по журналу" на портале OMS вы увидите *myVM*, как на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![Колонка OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="f9bb3-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9bb3-187">Next steps</span></span>

<span data-ttu-id="f9bb3-188">В этом руководстве вы выполнили настройку и проверку виртуальных машин с помощью центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="f9bb3-189">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="f9bb3-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9bb3-190">Включение диагностики загрузки на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="f9bb3-191">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="f9bb3-191">View boot diagnostics</span></span>
> * <span data-ttu-id="f9bb3-192">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-192">View host metrics</span></span>
> * <span data-ttu-id="f9bb3-193">Включение расширения системы диагностики на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="f9bb3-194">Просмотр метрик виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-194">View VM metrics</span></span>
> * <span data-ttu-id="f9bb3-195">Создание оповещений на основе метрик диагностики.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="f9bb3-196">Настройка расширенного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-196">Set up advanced monitoring</span></span>

<span data-ttu-id="f9bb3-197">Перейдите к следующему руководству, чтобы узнать о центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bb3-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9bb3-198">Мониторинг защиты виртуальных машин с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="f9bb3-198">Manage VM security</span></span>](./tutorial-azure-security.md)