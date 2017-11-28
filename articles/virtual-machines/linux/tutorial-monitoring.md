---
title: "aaaMonitor виртуальных машин Linux в Azure | Документы Microsoft"
description: "Узнайте, как toomonitor загружается диагностики и метрики производительности на виртуальной машине Linux в Azure"
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
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="2e574-103">Как toomonitor виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="2e574-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="2e574-104">tooensure виртуальных машин (ВМ) в Azure работают правильно, можно просмотреть Диагностика загрузки и метрики производительности.</span><span class="sxs-lookup"><span data-stu-id="2e574-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="2e574-105">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="2e574-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e574-106">Включить диагностику загрузки на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="2e574-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="2e574-107">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="2e574-107">View boot diagnostics</span></span>
> * <span data-ttu-id="2e574-108">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="2e574-108">View host metrics</span></span>
> * <span data-ttu-id="2e574-109">Включить расширение диагностики в hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="2e574-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="2e574-110">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2e574-110">View VM metrics</span></span>
> * <span data-ttu-id="2e574-111">Создание оповещений на основе метрик диагностики.</span><span class="sxs-lookup"><span data-stu-id="2e574-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="2e574-112">Настройка расширенного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2e574-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2e574-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2e574-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2e574-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2e574-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2e574-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="2e574-116">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2e574-116">Create VM</span></span>

<span data-ttu-id="2e574-117">Диагностика toosee и метрики в действии, необходимо виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2e574-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="2e574-118">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2e574-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2e574-119">Hello следующий пример создает группу ресурсов с именем *myResourceGroupMonitor* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="2e574-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="2e574-120">Теперь создайте виртуальную машину командой [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2e574-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="2e574-121">Hello следующий пример создает Виртуальную машину с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2e574-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="2e574-122">Включение диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="2e574-122">Enable boot diagnostics</span></span>

<span data-ttu-id="2e574-123">При загрузке виртуальных машин Linux, hello загрузки диагностического расширения записывает выходные данные для загрузки и сохраняет его в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="2e574-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="2e574-124">Эти данные могут быть ошибки при загрузке используется tootroubleshoot виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2e574-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="2e574-125">Диагностика загрузки не включается автоматически при создании ВМ Linux с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2e574-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="2e574-126">Перед включением Диагностика загрузки, учетную запись хранения должна toobe, созданные для хранения журналов загрузки.</span><span class="sxs-lookup"><span data-stu-id="2e574-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="2e574-127">Имена учетных записей хранения должны быть глобально уникальными, иметь длину от 3 до 24 символов и содержать только цифры и буквы в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="2e574-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="2e574-128">Создать учетную запись хранилища с hello [создания учетной записи хранилища az](/cli/azure/storage/account#create) команды.</span><span class="sxs-lookup"><span data-stu-id="2e574-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="2e574-129">В этом примере строка случайных — используется toocreate имя учетной записи хранилища с уникальным.</span><span class="sxs-lookup"><span data-stu-id="2e574-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="2e574-130">При включении Диагностика загрузки, необходим контейнер хранилища больших двоичных объектов toohello URI hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="2e574-131">Hello следующие запросы hello tooreturn учетной записи хранения этот URI.</span><span class="sxs-lookup"><span data-stu-id="2e574-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="2e574-132">значение URI Hello хранится в именах переменных *bloburi*, которое используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="2e574-133">Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="2e574-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="2e574-134">Hello `--storage` значение — hello больших двоичных объектов, собранные URI в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="2e574-135">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="2e574-135">View boot diagnostics</span></span>

<span data-ttu-id="2e574-136">Если Диагностика загрузки включены, каждый раз, останавливать и запускать hello виртуальной Машины, сведения о процессе загрузки hello записывается tooa файла журнала.</span><span class="sxs-lookup"><span data-stu-id="2e574-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="2e574-137">В этом примере сначала освободить hello виртуальной Машины с hello [ВМ az deallocate](/cli/azure/vm#deallocate) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="2e574-138">Теперь запустите hello виртуальной Машины с hello [запуска виртуальной машины az]( /cli/azure/vm#stop) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="2e574-139">Можно получить диагностические данные hello загрузки для *myVM* с hello [az ВМ Диагностика загрузки get загрузки журнал-](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="2e574-140">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="2e574-140">View host metrics</span></span>

<span data-ttu-id="2e574-141">Виртуальная машина Linux имеет выделенный узел в Azure, с которым она взаимодействует.</span><span class="sxs-lookup"><span data-stu-id="2e574-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="2e574-142">Метрики автоматически собираются для узла hello и могут быть просмотрены в hello портал Azure следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="2e574-143">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroupMonitor**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="2e574-144">toosee о выполнении hello узла виртуальной Машины, щелкните **метрики** hello колонке виртуальной Машины, затем выберите любой из hello *[узел]* метрики в списке **доступные метрики**.</span><span class="sxs-lookup"><span data-stu-id="2e574-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Просмотр метрик узла.](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="2e574-146">Установка расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="2e574-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e574-147">В этом документе описываются версии 2.3 hello диагностического расширения Linux, которое рекомендуется к использованию.</span><span class="sxs-lookup"><span data-stu-id="2e574-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="2e574-148">Версия 2.3 будет поддерживаться до 30 июня 2018 г.</span><span class="sxs-lookup"><span data-stu-id="2e574-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="2e574-149">Вместо этого можно включить версии 3.0 hello диагностического расширения для Linux.</span><span class="sxs-lookup"><span data-stu-id="2e574-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="2e574-150">Дополнительные сведения см. в разделе [hello документации](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2e574-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="2e574-151">Hello узла основные метрики доступны, но toosee более детального и метрики конкретной виртуальной Машины, вы tooneed tooinstall hello Azure расширение диагностики в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2e574-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="2e574-152">Hello расширения службы диагностики Azure позволяет дополнительные функции мониторинга и диагностики toobe данные, полученные из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2e574-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="2e574-153">Можно просматривать эти метрики производительности и создание предупреждений в зависимости от того, как выполняется hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2e574-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="2e574-154">Hello диагностического расширения устанавливаются с помощью портала Azure hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="2e574-155">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="2e574-156">Щелкните **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="2e574-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="2e574-157">Показывает, что список Hello *загрузки диагностики* уже включены в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="2e574-158">Установите флажок hello для *базовые показатели*.</span><span class="sxs-lookup"><span data-stu-id="2e574-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="2e574-159">В hello *учетной записи хранилища* перейдите выберите hello tooand *mydiagdata [1234]* учетную запись, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="2e574-160">Нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2e574-160">Click hello **Save** button.</span></span>

    ![Просмотр метрик диагностики](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="2e574-162">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2e574-162">View VM metrics</span></span>

<span data-ttu-id="2e574-163">Можно просмотреть метрики виртуальной Машины hello в hello просмотрены показателей виртуальной Машины узла hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e574-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="2e574-164">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="2e574-165">toosee о выполнении hello виртуальной Машины, щелкните **метрики** на hello колонки виртуальной Машины, а затем выберите любой из метрик hello диагностики в разделе **доступные метрики**.</span><span class="sxs-lookup"><span data-stu-id="2e574-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Просмотр метрик виртуальной машины](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="2e574-167">Создание оповещений</span><span class="sxs-lookup"><span data-stu-id="2e574-167">Create alerts</span></span>

<span data-ttu-id="2e574-168">На основе метрик производительности можно создавать оповещения.</span><span class="sxs-lookup"><span data-stu-id="2e574-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="2e574-169">Предупреждения может быть используется toonotify, когда средняя загрузка ЦП превышает пороговое значение или свободного дискового пространства падает ниже определенного, например.</span><span class="sxs-lookup"><span data-stu-id="2e574-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="2e574-170">Оповещения отображаются в hello портал Azure или могут отправляться по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="2e574-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="2e574-171">Вы можете запускать Runbook автоматизации Azure или логику приложения Azure в создаваемый tooalerts ответа.</span><span class="sxs-lookup"><span data-stu-id="2e574-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="2e574-172">Hello следующий пример создает оповещение о среднем использовании ЦП.</span><span class="sxs-lookup"><span data-stu-id="2e574-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="2e574-173">В hello портал Azure, щелкните **групп ресурсов**выберите **myResourceGroup**и выберите **myVM** в список ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="2e574-174">Нажмите кнопку **предупреждения правила** hello колонки виртуальной Машины, затем щелкните **добавить оповещение метрики** hello верхней части колонки hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="2e574-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="2e574-175">Укажите **имя** оповещения, например *myAlertRule*.</span><span class="sxs-lookup"><span data-stu-id="2e574-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="2e574-176">tootrigger предупреждение, если процент использования ЦП превышает 1.0 на пять минут, оставьте hello все остальные значения по умолчанию выбран.</span><span class="sxs-lookup"><span data-stu-id="2e574-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="2e574-177">При необходимости установите флажок "hello" для *электронной почты, владельцы, участники и читатели* toosend уведомление по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="2e574-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="2e574-178">Действие по умолчанию Hello — toopresent уведомления на портале hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="2e574-179">Нажмите кнопку hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2e574-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="2e574-180">Расширенный мониторинг</span><span class="sxs-lookup"><span data-stu-id="2e574-180">Advanced monitoring</span></span> 

<span data-ttu-id="2e574-181">Более сложный мониторинг виртуальной машины можно выполнить с помощью [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="2e574-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="2e574-182">Зарегистрируйтесь для получения [бесплатной пробной версии](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="2e574-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="2e574-183">При наличии портал OMS toohello доступа hello идентификатор рабочей области ключ и рабочей области можно найти в колонке параметров hello.</span><span class="sxs-lookup"><span data-stu-id="2e574-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="2e574-184">Замените < ключ рабочей области > и < идентификатор рабочей области > со значениями hello для из вашего OMS можно использовать рабочую область, а затем **набор расширения ВМ az** tooadd hello OMS расширения toohello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2e574-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

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

<span data-ttu-id="2e574-185">В колонке поиска журналов hello hello портала OMS, вы увидите *myVM* как элементы, отображаемые в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="2e574-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Колонка OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="2e574-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e574-187">Next steps</span></span>

<span data-ttu-id="2e574-188">В этом руководстве вы выполнили настройку и проверку виртуальных машин с помощью центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="2e574-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="2e574-189">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2e574-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e574-190">Включить диагностику загрузки на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="2e574-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="2e574-191">Просмотр диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="2e574-191">View boot diagnostics</span></span>
> * <span data-ttu-id="2e574-192">Просмотр метрик узла.</span><span class="sxs-lookup"><span data-stu-id="2e574-192">View host metrics</span></span>
> * <span data-ttu-id="2e574-193">Включить расширение диагностики в hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="2e574-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="2e574-194">Просмотр метрик виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2e574-194">View VM metrics</span></span>
> * <span data-ttu-id="2e574-195">Создание оповещений на основе метрик диагностики.</span><span class="sxs-lookup"><span data-stu-id="2e574-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="2e574-196">Настройка расширенного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="2e574-196">Set up advanced monitoring</span></span>

<span data-ttu-id="2e574-197">Переместить следующий учебник toolearn toohello относительно центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="2e574-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e574-198">Мониторинг защиты виртуальных машин с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="2e574-198">Manage VM security</span></span>](./tutorial-azure-security.md)