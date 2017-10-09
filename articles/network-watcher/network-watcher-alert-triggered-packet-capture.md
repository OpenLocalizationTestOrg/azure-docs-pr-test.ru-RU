---
title: "aaaUse toodo захват пакетов упреждающего мониторинга с оповещениями и функциями Azure сети | Документы Microsoft"
description: "В этой статье описывается, как toocreate оповещение запускается захват пакетов с Наблюдатель сети Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="021ae-103">Использование записи пакетов для упреждающего мониторинга сети с помощью оповещений и функций Azure</span><span class="sxs-lookup"><span data-stu-id="021ae-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="021ae-104">Захват пакетов Наблюдатель сети создает сеансы регистрации tootrack трафика и из него виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="021ae-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="021ae-105">Hello файл записи может иметь фильтр, который определяется tootrack hello только трафик, что требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="021ae-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="021ae-106">Эти данные затем сохраняются в хранилище BLOB-объекта или локально на гостевой машине hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="021ae-107">Эта возможность допускает удаленный запуск из других сценариев службы автоматизации, таких как функции Azure.</span><span class="sxs-lookup"><span data-stu-id="021ae-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="021ae-108">Предоставляет захват пакетов hello упреждающего получает возможность toorun на основе определенных аномалий сети.</span><span class="sxs-lookup"><span data-stu-id="021ae-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="021ae-109">Они также помогают выполнять сбор сетевой статистики, получать сведения о сетевых вторжениях, выполнять отладку передачи данных между клиентом и сервером и другие операции.</span><span class="sxs-lookup"><span data-stu-id="021ae-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="021ae-110">Развернутые в Azure ресурсы работают круглосуточно и без выходных.</span><span class="sxs-lookup"><span data-stu-id="021ae-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="021ae-111">Вам и вашим сотрудникам не может отслеживать активно hello все ресурсы 24/7.</span><span class="sxs-lookup"><span data-stu-id="021ae-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="021ae-112">К примеру, что вы будете делать, если сбой произойдет в два часа ночи?</span><span class="sxs-lookup"><span data-stu-id="021ae-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="021ae-113">С использованием Наблюдатель сети, предупреждения и функции из hello Azure экосистемы можно заранее ответить hello данными и средствами toosolve проблем в сети.</span><span class="sxs-lookup"><span data-stu-id="021ae-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Сценарий][scenario]

## <a name="prerequisites"></a><span data-ttu-id="021ae-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="021ae-115">Prerequisites</span></span>

* <span data-ttu-id="021ae-116">Hello последнюю версию [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="021ae-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="021ae-117">Существующий экземпляр службы "Наблюдатель за сетями".</span><span class="sxs-lookup"><span data-stu-id="021ae-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="021ae-118">Если у вас нет экземпляра этой службы, [создайте его](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="021ae-119">Существующую виртуальную машину в hello одном регионе Наблюдатель сети с hello [расширение Windows](../virtual-machines/windows/extensions-nwa.md) или [расширение виртуальной машины Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="021ae-120">Сценарий</span><span class="sxs-lookup"><span data-stu-id="021ae-120">Scenario</span></span>

<span data-ttu-id="021ae-121">В этом примере ВМ отправляет дополнительные TCP-сегментов, чем обычно, и требуется toobe оповещения.</span><span class="sxs-lookup"><span data-stu-id="021ae-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="021ae-122">TCP-сегменты используются только в качестве примера. Вы можете использовать любое условие оповещения.</span><span class="sxs-lookup"><span data-stu-id="021ae-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="021ae-123">Оповещения отображаются, их нужно toounderstand tooreceive данных на уровне пакета, почему увеличилось связи.</span><span class="sxs-lookup"><span data-stu-id="021ae-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="021ae-124">Затем можно предпринять шаги tooreturn hello виртуальной машины tooregular связи.</span><span class="sxs-lookup"><span data-stu-id="021ae-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="021ae-125">В этом сценарии предполагается, что у вас есть экземпляр службы "Наблюдатель за сетями", а также группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="021ae-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="021ae-126">После списка Hello приведен обзор hello рабочего процесса, который имеет место.</span><span class="sxs-lookup"><span data-stu-id="021ae-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="021ae-127">На виртуальной машине активируется оповещение.</span><span class="sxs-lookup"><span data-stu-id="021ae-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="021ae-128">Предупреждение Hello вызывает функцию Azure через веб-перехватчик.</span><span class="sxs-lookup"><span data-stu-id="021ae-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="021ae-129">Функции Azure обрабатывает предупреждения hello и запускает сеанс отслеживания пакетов Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="021ae-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="021ae-130">Захват пакетов Hello выполняется на ВМ hello и собирает трафика.</span><span class="sxs-lookup"><span data-stu-id="021ae-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="021ae-131">Hello пакет отслеживания передачи файла tooa учетной записи хранилища для их просмотра и диагностики.</span><span class="sxs-lookup"><span data-stu-id="021ae-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="021ae-132">tooautomate этого процесса она создана и подключиться оповещение на наш tootrigger виртуальной Машины при возникновении hello инцидента.</span><span class="sxs-lookup"><span data-stu-id="021ae-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="021ae-133">Также мы создадим toocall функции в Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="021ae-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="021ae-134">Этот сценарий hello следующие:</span><span class="sxs-lookup"><span data-stu-id="021ae-134">This scenario does hello following:</span></span>

* <span data-ttu-id="021ae-135">создает функцию Azure, которая запускает запись пакетов;</span><span class="sxs-lookup"><span data-stu-id="021ae-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="021ae-136">Создает правило генерации оповещений на виртуальной машине и настраивает hello правило оповещения toocall hello Azure функции.</span><span class="sxs-lookup"><span data-stu-id="021ae-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="021ae-137">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="021ae-137">Create an Azure function</span></span>

<span data-ttu-id="021ae-138">Первым шагом Hello toocreate tooprocess hello Azure функции оповещения и создать захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="021ae-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="021ae-139">В hello [портал Azure](https://portal.azure.com)выберите **New** > **вычислений** > **функции приложения**.</span><span class="sxs-lookup"><span data-stu-id="021ae-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Создание приложения-функции][1-1]

2. <span data-ttu-id="021ae-141">На hello **функции приложения** колонки, введите следующие значения hello, а затем выберите **ОК** приложение hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="021ae-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="021ae-142">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="021ae-142">**Setting**</span></span> | <span data-ttu-id="021ae-143">**Значение**</span><span class="sxs-lookup"><span data-stu-id="021ae-143">**Value**</span></span> | <span data-ttu-id="021ae-144">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="021ae-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="021ae-145">**Имя приложения**</span><span class="sxs-lookup"><span data-stu-id="021ae-145">**App name**</span></span>|<span data-ttu-id="021ae-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="021ae-146">PacketCaptureExample</span></span>|<span data-ttu-id="021ae-147">имя функции приложение hello Hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="021ae-148">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="021ae-148">**Subscription**</span></span>|<span data-ttu-id="021ae-149">[Подписки] hello подписки, для которых приложение функции hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="021ae-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="021ae-150">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="021ae-150">**Resource Group**</span></span>|<span data-ttu-id="021ae-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="021ae-151">PacketCaptureRG</span></span>|<span data-ttu-id="021ae-152">ресурс группы toocontain hello функция приложение Hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="021ae-153">**План размещения**</span><span class="sxs-lookup"><span data-stu-id="021ae-153">**Hosting Plan**</span></span>|<span data-ttu-id="021ae-154">План потребления</span><span class="sxs-lookup"><span data-stu-id="021ae-154">Consumption Plan</span></span>| <span data-ttu-id="021ae-155">Тип Hello плана ваша функция использует приложение.</span><span class="sxs-lookup"><span data-stu-id="021ae-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="021ae-156">Можно выбрать план потребления или план службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="021ae-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="021ae-157">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="021ae-157">**Location**</span></span>|<span data-ttu-id="021ae-158">Центральный регион США</span><span class="sxs-lookup"><span data-stu-id="021ae-158">Central US</span></span>| <span data-ttu-id="021ae-159">область какое приложение toocreate hello функции Hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="021ae-160">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="021ae-160">**Storage Account**</span></span>|<span data-ttu-id="021ae-161">{autogenerated}</span><span class="sxs-lookup"><span data-stu-id="021ae-161">{autogenerated}</span></span>| <span data-ttu-id="021ae-162">Учетная запись хранения Hello, требуются функции Azure для хранения общего назначения.</span><span class="sxs-lookup"><span data-stu-id="021ae-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="021ae-163">На hello **приложений-функций PacketCaptureExample** колонке выберите **функции** > **пользовательские функции**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="021ae-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="021ae-164">Выберите **HttpTrigger Powershell**, а затем введите hello оставшиеся сведения.</span><span class="sxs-lookup"><span data-stu-id="021ae-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="021ae-165">Наконец, toocreate функции hello, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="021ae-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="021ae-166">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="021ae-166">**Setting**</span></span> | <span data-ttu-id="021ae-167">**Значение**</span><span class="sxs-lookup"><span data-stu-id="021ae-167">**Value**</span></span> | <span data-ttu-id="021ae-168">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="021ae-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="021ae-169">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="021ae-169">**Scenario**</span></span>|<span data-ttu-id="021ae-170">Экспериментальная возможность</span><span class="sxs-lookup"><span data-stu-id="021ae-170">Experimental</span></span>|<span data-ttu-id="021ae-171">Тип сценария</span><span class="sxs-lookup"><span data-stu-id="021ae-171">Type of scenario</span></span>|
    |<span data-ttu-id="021ae-172">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="021ae-172">**Name your function**</span></span>|<span data-ttu-id="021ae-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="021ae-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="021ae-174">Имя функции hello</span><span class="sxs-lookup"><span data-stu-id="021ae-174">Name of hello function</span></span>|
    |<span data-ttu-id="021ae-175">**Уровень авторизации**</span><span class="sxs-lookup"><span data-stu-id="021ae-175">**Authorization level**</span></span>|<span data-ttu-id="021ae-176">Функция</span><span class="sxs-lookup"><span data-stu-id="021ae-176">Function</span></span>|<span data-ttu-id="021ae-177">Уровень авторизации для функции hello</span><span class="sxs-lookup"><span data-stu-id="021ae-177">Authorization level for hello function</span></span>|

![Пример функций][functions1]

> [!NOTE]
> <span data-ttu-id="021ae-179">шаблон PowerShell Hello является экспериментальной и не имеет полную поддержку.</span><span class="sxs-lookup"><span data-stu-id="021ae-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="021ae-180">Настройки требуются для этого примера и описаны в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="021ae-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="021ae-181">Добавление модулей</span><span class="sxs-lookup"><span data-stu-id="021ae-181">Add modules</span></span>

<span data-ttu-id="021ae-182">функция приложение hello последнюю PowerShell модуль toohello отправить toouse командлеты PowerShell Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="021ae-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="021ae-183">На локальном компьютере с hello установлены последние модули Azure PowerShell выполните следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="021ae-184">Это пример дает hello локальный путь к модули Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="021ae-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="021ae-185">Мы используем эти папки позже.</span><span class="sxs-lookup"><span data-stu-id="021ae-185">These folders are used in a later step.</span></span> <span data-ttu-id="021ae-186">Hello модули, используемые в этом сценарии являются:</span><span class="sxs-lookup"><span data-stu-id="021ae-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="021ae-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="021ae-187">AzureRM.Network</span></span>

    * <span data-ttu-id="021ae-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="021ae-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="021ae-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="021ae-189">AzureRM.Resources</span></span>

    ![Папки PowerShell][functions5]

1. <span data-ttu-id="021ae-191">Выберите **функции параметров приложения** > **Go tooApp редактор службы**.</span><span class="sxs-lookup"><span data-stu-id="021ae-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Параметры приложения-функции][functions2]

1. <span data-ttu-id="021ae-193">Щелкните правой кнопкой мыши hello **AlertPacketCapturePowershell** папки и создайте папку с именем **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="021ae-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="021ae-194">Создайте вложенную папку для каждого требуемого модуля.</span><span class="sxs-lookup"><span data-stu-id="021ae-194">Create a subfolder for each module that you need.</span></span>

    ![Папки и вложенные папки][functions3]

    * <span data-ttu-id="021ae-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="021ae-196">AzureRM.Network</span></span>

    * <span data-ttu-id="021ae-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="021ae-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="021ae-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="021ae-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="021ae-199">Щелкните правой кнопкой мыши hello **AzureRM.Network** вложенную папку, а затем выберите **передача файлов**.</span><span class="sxs-lookup"><span data-stu-id="021ae-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="021ae-200">Go tooyour Azure модули.</span><span class="sxs-lookup"><span data-stu-id="021ae-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="021ae-201">В локальной hello **AzureRM.Network** папку, выберите все файлы hello в папке hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="021ae-202">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="021ae-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="021ae-203">Повторите эти шаги для папок **AzureRM.Profile** и **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="021ae-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Отправка файлов][functions6]

1. <span data-ttu-id="021ae-205">После завершения, каждой папки должен быть hello файлы модуля PowerShell с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="021ae-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Файлы PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="021ae-207">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="021ae-207">Authentication</span></span>

<span data-ttu-id="021ae-208">командлеты PowerShell toouse hello, вы должны пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="021ae-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="021ae-209">Настройте проверку подлинности в приложении функции hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="021ae-210">tooconfigure проверки подлинности, необходимо настроить переменные среды и передачи приложения функции toohello зашифрованный файл ключа.</span><span class="sxs-lookup"><span data-stu-id="021ae-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="021ae-211">Этот сценарий обеспечивает лишь один пример того, как tooimplement проверки подлинности с помощью функций Azure.</span><span class="sxs-lookup"><span data-stu-id="021ae-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="021ae-212">Существуют другие способы toodo это.</span><span class="sxs-lookup"><span data-stu-id="021ae-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="021ae-213">Зашифрованные учетные данные</span><span class="sxs-lookup"><span data-stu-id="021ae-213">Encrypted credentials</span></span>

<span data-ttu-id="021ae-214">Следующий сценарий PowerShell Hello создает файл ключа с именем **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="021ae-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="021ae-215">Он также предоставляет зашифрованную версию пароля hello, входящую в.</span><span class="sxs-lookup"><span data-stu-id="021ae-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="021ae-216">Этот пароль — hello пароль, который определен для приложения hello Azure Active Directory, который используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="021ae-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="021ae-217">В hello редактор службы приложения hello функции приложения, создайте папку с именем **ключей** под **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="021ae-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="021ae-218">Затем отправьте hello **PassEncryptKey.key** файл, созданный в предыдущем примере PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Ключ для функций][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="021ae-220">Извлечение значений переменных среды</span><span class="sxs-lookup"><span data-stu-id="021ae-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="021ae-221">Hello окончательного требованием является tooset копирование hello переменные среды, которые являются значениями hello tooaccess, необходимые для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="021ae-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="021ae-222">Hello ниже перечислены hello переменные среды, которые создаются.</span><span class="sxs-lookup"><span data-stu-id="021ae-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="021ae-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="021ae-223">AzureClientID</span></span>

* <span data-ttu-id="021ae-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="021ae-224">AzureTenant</span></span>

* <span data-ttu-id="021ae-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="021ae-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="021ae-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="021ae-226">AzureClientID</span></span>

<span data-ttu-id="021ae-227">Идентификатор клиента Hello — hello код приложения в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="021ae-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="021ae-228">Если у вас еще нет toouse приложения, запустите приложение после toocreate пример hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="021ae-229">Hello пароль, используемый при создании приложения hello должно быть hello пароль, который был создан ранее, при сохранении файла ключа hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="021ae-230">В hello портал Azure, выберите **подписки**.</span><span class="sxs-lookup"><span data-stu-id="021ae-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="021ae-231">Выберите toouse hello подписки, а затем выберите **(IAM) управления доступом к**.</span><span class="sxs-lookup"><span data-stu-id="021ae-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![Функции (IAM)][functions9]

1. <span data-ttu-id="021ae-233">Выберите учетную запись toouse hello, а затем выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="021ae-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="021ae-234">Скопируйте hello идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="021ae-234">Copy hello Application ID.</span></span>

    ![Идентификатор приложений-функций][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="021ae-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="021ae-236">AzureTenant</span></span>

<span data-ttu-id="021ae-237">Получите идентификатор клиента hello, выполнив следующий пример скрипта PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="021ae-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="021ae-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="021ae-238">AzureCredPassword</span></span>

<span data-ttu-id="021ae-239">Hello значение переменной среды AzureCredPassword hello значение hello, получить запуск hello следующий пример скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="021ae-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="021ae-240">В этом примере hello же, что показано в предыдущем hello **зашифровал учетные данные** раздела.</span><span class="sxs-lookup"><span data-stu-id="021ae-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="021ae-241">Здравствуйте, значение, которое требуется представляет выходные данные hello hello `$Encryptedpassword` переменной.</span><span class="sxs-lookup"><span data-stu-id="021ae-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="021ae-242">Это основной пароль службы hello, который зашифрован с помощью сценария PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="021ae-243">Переменные среды hello хранилища</span><span class="sxs-lookup"><span data-stu-id="021ae-243">Store hello environment variables</span></span>

1. <span data-ttu-id="021ae-244">Go toohello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="021ae-244">Go toohello function app.</span></span> <span data-ttu-id="021ae-245">Затем последовательно выберите **Параметры приложения-функции** > **Настроить параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="021ae-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Настройка параметров приложения][functions11]

1. <span data-ttu-id="021ae-247">Добавьте hello переменных среды и их значения toohello приложение параметров, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="021ae-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Параметры приложения][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="021ae-249">Добавление функции toohello PowerShell</span><span class="sxs-lookup"><span data-stu-id="021ae-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="021ae-250">Это теперь время toomake вызывает Наблюдатель сети из внутри hello Azure функции.</span><span class="sxs-lookup"><span data-stu-id="021ae-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="021ae-251">Hello реализация этой функции могут различаться в зависимости от требований hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="021ae-252">Однако поток общие hello hello кода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="021ae-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="021ae-253">Обработка входных параметров.</span><span class="sxs-lookup"><span data-stu-id="021ae-253">Process input parameters.</span></span>
2. <span data-ttu-id="021ae-254">Существующий пакет записывает tooverify ограничения и разрешения конфликтов имен.</span><span class="sxs-lookup"><span data-stu-id="021ae-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="021ae-255">Создание записи пакетов с необходимыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="021ae-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="021ae-256">Периодический опрос процесса записи пакетов вплоть до его завершения.</span><span class="sxs-lookup"><span data-stu-id="021ae-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="021ae-257">Уведомите пользователя hello, что сеанс захвата hello пакета завершена.</span><span class="sxs-lookup"><span data-stu-id="021ae-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="021ae-258">Hello ниже приведен код PowerShell, который может использоваться в функции hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="021ae-259">Нет значения, которые необходимо заменить для toobe **subscriptionId**, **resourceGroupName**, и **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="021ae-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="021ae-260">Получить URL-адрес функции hello</span><span class="sxs-lookup"><span data-stu-id="021ae-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="021ae-261">После создания функции, настройте URL-адрес hello предупреждения toocall, связанной с функции hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="021ae-262">tooget это значение URL-адрес функции hello копирование из приложения функция.</span><span class="sxs-lookup"><span data-stu-id="021ae-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Поиск URL-адрес функции hello][functions13]

2. <span data-ttu-id="021ae-264">Скопируйте URL-адрес функции hello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="021ae-264">Copy hello function URL for your function app.</span></span>

    ![Копирование URL-адрес функции hello][2]

<span data-ttu-id="021ae-266">Если требуется пользовательских свойств в полезных данных запроса POST веб-перехватчика hello hello ссылаться слишком[настроить веб-перехватчика на оповещение Azure метрики](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="021ae-267">Настройка оповещения на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="021ae-267">Configure an alert on a VM</span></span>

<span data-ttu-id="021ae-268">Предупреждения может быть настроенный toonotify отдельных пользователей, когда конкретную метрику пересекает пороговое значение, которое назначается tooit.</span><span class="sxs-lookup"><span data-stu-id="021ae-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="021ae-269">В этом примере hello предупреждение включено hello TCP-сегментов, которые отправляются, но hello предупреждение можно запустить для многих других показателей.</span><span class="sxs-lookup"><span data-stu-id="021ae-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="021ae-270">В этом примере предупреждение — настроенное toocall функции hello toocall веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="021ae-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="021ae-271">Создание правила оповещения hello</span><span class="sxs-lookup"><span data-stu-id="021ae-271">Create hello alert rule</span></span>

<span data-ttu-id="021ae-272">Go tooan существующей виртуальной машины, а затем добавьте правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="021ae-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="021ae-273">Дополнительные сведения о настройке оповещений см. в статье [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="021ae-274">Введите следующие значения в hello hello **правило оповещения** колонки, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="021ae-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="021ae-275">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="021ae-275">**Setting**</span></span> | <span data-ttu-id="021ae-276">**Значение**</span><span class="sxs-lookup"><span data-stu-id="021ae-276">**Value**</span></span> | <span data-ttu-id="021ae-277">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="021ae-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="021ae-278">**Имя**</span><span class="sxs-lookup"><span data-stu-id="021ae-278">**Name**</span></span>|<span data-ttu-id="021ae-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="021ae-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="021ae-280">Имя правила оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="021ae-281">**Описание**</span><span class="sxs-lookup"><span data-stu-id="021ae-281">**Description**</span></span>|<span data-ttu-id="021ae-282">Число отправленных TCP-сегментов превысило пороговое значение</span><span class="sxs-lookup"><span data-stu-id="021ae-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="021ae-283">Описание правила оповещений hello Hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="021ae-284">**Метрика**</span><span class="sxs-lookup"><span data-stu-id="021ae-284">**Metric**</span></span>|<span data-ttu-id="021ae-285">Отправлено TCP-сегментов</span><span class="sxs-lookup"><span data-stu-id="021ae-285">TCP segments sent</span></span>| <span data-ttu-id="021ae-286">Hello метрики toouse tootrigger hello предупреждений.</span><span class="sxs-lookup"><span data-stu-id="021ae-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="021ae-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="021ae-287">**Condition**</span></span>|<span data-ttu-id="021ae-288">Больше</span><span class="sxs-lookup"><span data-stu-id="021ae-288">Greater than</span></span>| <span data-ttu-id="021ae-289">Hello toouse условия, при вычислении показателя hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="021ae-290">**Пороговое значение**.</span><span class="sxs-lookup"><span data-stu-id="021ae-290">**Threshold**</span></span>|<span data-ttu-id="021ae-291">100</span><span class="sxs-lookup"><span data-stu-id="021ae-291">100</span></span>| <span data-ttu-id="021ae-292">Hello значение для показателя hello hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="021ae-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="021ae-293">Это должно быть значение tooa допустимое значение для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="021ae-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="021ae-294">**Период**</span><span class="sxs-lookup"><span data-stu-id="021ae-294">**Period**</span></span>|<span data-ttu-id="021ae-295">За последние пять минут hello</span><span class="sxs-lookup"><span data-stu-id="021ae-295">Over hello last five minutes</span></span>| <span data-ttu-id="021ae-296">Определяет период hello в какие toolook для hello пороговое значение метрики hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="021ae-297">**webhook**</span><span class="sxs-lookup"><span data-stu-id="021ae-297">**Webhook**</span></span>|<span data-ttu-id="021ae-298">[URL-адрес веб-перехватчика из приложения-функции]</span><span class="sxs-lookup"><span data-stu-id="021ae-298">[webhook URL from function app]</span></span>| <span data-ttu-id="021ae-299">Hello веб-перехватчика URL-адрес из приложения функция hello, созданный на предыдущих этапах hello.</span><span class="sxs-lookup"><span data-stu-id="021ae-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="021ae-300">Метрика сегментов Hello TCP не включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="021ae-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="021ae-301">Дополнительные сведения о tooenable дополнительные метрики, посетив [включить наблюдение и диагностику](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="021ae-302">Просмотрите результаты hello</span><span class="sxs-lookup"><span data-stu-id="021ae-302">Review hello results</span></span>

<span data-ttu-id="021ae-303">После критерии hello для оповещения триггеры hello создается захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="021ae-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="021ae-304">Перейти tooNetwork наблюдателя, а затем выберите **захват пакетов**.</span><span class="sxs-lookup"><span data-stu-id="021ae-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="021ae-305">На этой странице можно выбрать hello записи файла ссылки toodownload hello пакетов захват пакетов.</span><span class="sxs-lookup"><span data-stu-id="021ae-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Просмотр записи пакетов][functions14]

<span data-ttu-id="021ae-307">Если файл записи hello хранится локально, его можно получить при входе в toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="021ae-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="021ae-308">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="021ae-309">Кроме того, можно использовать такое средство, как [обозреватель хранилищ](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="021ae-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="021ae-310">Когда вы скачаете нужную запись, ее можно просмотреть в любом средстве, поддерживающем формат **CAP**.</span><span class="sxs-lookup"><span data-stu-id="021ae-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="021ae-311">Ниже приведены ссылки tootwo этих средств:</span><span class="sxs-lookup"><span data-stu-id="021ae-311">Following are links tootwo of these tools:</span></span>

- <span data-ttu-id="021ae-312">[Анализатор сообщений (Майкрософт)](https://technet.microsoft.com/library/jj649776.aspx).</span><span class="sxs-lookup"><span data-stu-id="021ae-312">[Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)</span></span>
- <span data-ttu-id="021ae-313">[Wireshark](https://www.wireshark.org/).</span><span class="sxs-lookup"><span data-stu-id="021ae-313">[WireShark](https://www.wireshark.org/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="021ae-314">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="021ae-314">Next steps</span></span>

<span data-ttu-id="021ae-315">Узнайте, как tooview вашей снимки пакетов, посетив [анализ захват пакетов с помощью Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="021ae-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
