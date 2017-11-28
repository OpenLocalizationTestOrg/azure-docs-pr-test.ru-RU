---
title: "aaaMonitoring ВМ Linux с расширением ВМ | Документы Microsoft"
description: "Узнайте, как toouse hello производительности hello toomonitor диагностического расширения для Linux и диагностических данных виртуальной машины Linux в Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="90826-103">Используйте hello диагностического расширения для Linux toomonitor hello производительности и диагностики данных виртуальной Машины Linux</span><span class="sxs-lookup"><span data-stu-id="90826-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="90826-104">В этом документе описываются версии 2.3 hello диагностического расширения для Linux.</span><span class="sxs-lookup"><span data-stu-id="90826-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90826-105">Эта версия не рекомендуется к использованию, и ее публикация может быть отменена в любой момент после 30 июня 2018 г.</span><span class="sxs-lookup"><span data-stu-id="90826-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="90826-106">Она была заменена версией 3.0.</span><span class="sxs-lookup"><span data-stu-id="90826-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="90826-107">Дополнительные сведения см. в разделе hello [документации для версии 3.0 hello диагностического расширения для Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="90826-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="90826-108">Введение</span><span class="sxs-lookup"><span data-stu-id="90826-108">Introduction</span></span>

<span data-ttu-id="90826-109">(**Примечание**: hello диагностического расширения для Linux открытый исходный код на [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) где hello самые последние сведения о расширения hello первой публикации.</span><span class="sxs-lookup"><span data-stu-id="90826-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="90826-110">Может потребоваться toocheck hello [странице GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) первого.)</span><span class="sxs-lookup"><span data-stu-id="90826-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="90826-111">Hello диагностического расширения для Linux помогает hello монитор пользователя виртуальных машин Linux, которые работают на платформе Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90826-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="90826-112">Он имеет hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="90826-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="90826-113">Собирает и отправляет сведения о производительности системы hello из таблицы хранилища пользователя toohello hello виртуальных Машин Linux, включая сведения о диагностике и syslog.</span><span class="sxs-lookup"><span data-stu-id="90826-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="90826-114">Позволяет пользователям toocustomize hello данных метрик, которые будут собраны и отправлены.</span><span class="sxs-lookup"><span data-stu-id="90826-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="90826-115">Позволяет пользователям tooupload указанного журнала файлов tooa указанного хранилища таблицы.</span><span class="sxs-lookup"><span data-stu-id="90826-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="90826-116">В текущей версии hello 2.3 hello данные включают следующее:</span><span class="sxs-lookup"><span data-stu-id="90826-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="90826-117">все журналы Rsyslog Linux, включая системный журнал, журналы безопасности и приложений;</span><span class="sxs-lookup"><span data-stu-id="90826-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="90826-118">Все данные системы, которые указаны на [hello решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="90826-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="90826-119">файлы журналов, выбранные пользователем.</span><span class="sxs-lookup"><span data-stu-id="90826-119">User-specified log files.</span></span>

<span data-ttu-id="90826-120">Этот модуль работает с классической hello и модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90826-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="90826-121">Текущая версия расширения hello и прекращении старых версий</span><span class="sxs-lookup"><span data-stu-id="90826-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="90826-122">Последняя версия расширения hello Hello — **2.3**, и **все старые версии (2.0, 2.1 и 2.2) будут устаревшими и неопубликованных концу этого года (2017 г.)**.</span><span class="sxs-lookup"><span data-stu-id="90826-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="90826-123">При установке расширения диагностики Linux hello автоматического дополнительный номер версии обновления отключена настоятельно рекомендуется удалить расширение hello и переустановите его с включено обновление автоматического дополнительный номер версии.</span><span class="sxs-lookup"><span data-stu-id="90826-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="90826-124">На виртуальных машинах классический (ASM) можно добиться этого, указав «2.*» в качестве hello версию при установке расширения hello с помощью Azure XPLAT-CLI или Powershell.</span><span class="sxs-lookup"><span data-stu-id="90826-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="90826-125">На виртуальных машинах ARM, этого можно достичь, включая "«autoUpgradeMinorVersion»: true" в шаблон развертывания виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="90826-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="90826-126">Кроме того любой новой установки расширения hello должен иметь дополнительный номер версии hello автоматического обновления включен параметр.</span><span class="sxs-lookup"><span data-stu-id="90826-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="90826-127">Включить расширение hello</span><span class="sxs-lookup"><span data-stu-id="90826-127">Enable hello extension</span></span>

<span data-ttu-id="90826-128">Это расширение можно включить с помощью hello [портал Azure](https://portal.azure.com/#), Azure PowerShell или Azure CLI скриптов.</span><span class="sxs-lookup"><span data-stu-id="90826-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="90826-129">tooview и настроить систему hello и данные о производительности непосредственно из hello портал Azure, выполните [эти действия на hello блог Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="90826-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="90826-130">В этой статье основное внимание уделено tooenable и настройка hello расширения с помощью команды Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="90826-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="90826-131">Это позволяет tooread и представление данных hello непосредственно из таблицы хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="90826-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="90826-132">Обратите внимание, что методы настройки hello, описанные здесь не будет работать для hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="90826-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="90826-133">tooview и настроить hello производительности системы и данных непосредственно из hello портал Azure, необходимо включить расширение hello через портал hello.</span><span class="sxs-lookup"><span data-stu-id="90826-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90826-134">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90826-134">Prerequisites</span></span>

* <span data-ttu-id="90826-135">**Агент Linux для Azure 2.0.6 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="90826-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="90826-136">Обратите внимание на то, что большинство образов в коллекции виртуальных машин Azure на базе Linux включает версию 2.0.6 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="90826-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="90826-137">Можно запустить **WAAgent-версии** tooconfirm, какая версия установлена на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="90826-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="90826-138">Если hello виртуальная машина работает под управлением версии, более ранняя, чем 2.0.6, можно выполнить [эти инструкции на сайте GitHub](https://github.com/Azure/WALinuxAgent "инструкции") tooupdate его.</span><span class="sxs-lookup"><span data-stu-id="90826-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="90826-139">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="90826-139">**Azure CLI**.</span></span> <span data-ttu-id="90826-140">Выполните [это руководство по установке CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI среды на компьютере.</span><span class="sxs-lookup"><span data-stu-id="90826-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="90826-141">После установки Azure CLI можно использовать hello **azure** команду из командной строки (Bash, терминалов или командной строки) tooaccess hello Azure CLI команды.</span><span class="sxs-lookup"><span data-stu-id="90826-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="90826-142">Например:</span><span class="sxs-lookup"><span data-stu-id="90826-142">For example:</span></span>

  * <span data-ttu-id="90826-143">Выполните команду **azure vm extension set --help** , чтобы получить более подробные справочные сведения.</span><span class="sxs-lookup"><span data-stu-id="90826-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="90826-144">Запустите **входа azure** toosign в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="90826-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="90826-145">Запустите **список виртуальных машин azure** toolist все hello виртуальных машин, имеющих в Azure.</span><span class="sxs-lookup"><span data-stu-id="90826-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="90826-146">Данные учетной записи хранилища toostore hello.</span><span class="sxs-lookup"><span data-stu-id="90826-146">A storage account toostore hello data.</span></span> <span data-ttu-id="90826-147">Потребуется имя учетной записи хранения, который был создан ранее и хранения данных tooyour доступа ключа tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="90826-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="90826-148">Используйте hello Azure CLI команда tooenable hello диагностического расширения для Linux</span><span class="sxs-lookup"><span data-stu-id="90826-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="90826-149">Сценарий 1.</span><span class="sxs-lookup"><span data-stu-id="90826-149">Scenario 1.</span></span> <span data-ttu-id="90826-150">Включить расширение hello с набором данных по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="90826-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="90826-151">В 2.3 или более поздней версии содержит данные по умолчанию hello, которые будут собираться.</span><span class="sxs-lookup"><span data-stu-id="90826-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="90826-152">все данные Rsyslog (включая системный журнал, журналы безопасности и приложений);</span><span class="sxs-lookup"><span data-stu-id="90826-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="90826-153">базовый набор основных данных о системе.</span><span class="sxs-lookup"><span data-stu-id="90826-153">A core set of basis system data.</span></span> <span data-ttu-id="90826-154">Обратите внимание, что hello полный набор данных, описанное на hello [решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="90826-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="90826-155">Если требуется, чтобы tooenable дополнительные данные, выполните шаги hello в сценарии 2 и 3.</span><span class="sxs-lookup"><span data-stu-id="90826-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="90826-156">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="90826-156">Step 1.</span></span> <span data-ttu-id="90826-157">Создайте файл privateconfig.JSON с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="90826-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="90826-158">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="90826-158">Step 2.</span></span> <span data-ttu-id="90826-159">Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="90826-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="90826-160">Сценарий 2.</span><span class="sxs-lookup"><span data-stu-id="90826-160">Scenario 2.</span></span> <span data-ttu-id="90826-161">Настройка метрик мониторинга производительности hello</span><span class="sxs-lookup"><span data-stu-id="90826-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="90826-162">В этом разделе описывается, как toocustomize hello производительности и диагностики данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="90826-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="90826-163">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="90826-163">Step 1.</span></span> <span data-ttu-id="90826-164">Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1.</span><span class="sxs-lookup"><span data-stu-id="90826-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="90826-165">Создайте также файл PublicConfig.json.</span><span class="sxs-lookup"><span data-stu-id="90826-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="90826-166">Укажите hello требуется toocollect данных.</span><span class="sxs-lookup"><span data-stu-id="90826-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="90826-167">Для всех поддерживаемых поставщиков и переменных, ссылки hello [решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="90826-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="90826-168">Можно иметь несколько запросов и сохранять их в несколько таблиц путем добавления скрипта toohello дополнительные запросы.</span><span class="sxs-lookup"><span data-stu-id="90826-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="90826-169">По умолчанию hello Rsyslog данных собираются всегда.</span><span class="sxs-lookup"><span data-stu-id="90826-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="90826-170">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="90826-170">Step 2.</span></span> <span data-ttu-id="90826-171">Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="90826-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="90826-172">Сценарий 3.</span><span class="sxs-lookup"><span data-stu-id="90826-172">Scenario 3.</span></span> <span data-ttu-id="90826-173">Передача файлов журнала</span><span class="sxs-lookup"><span data-stu-id="90826-173">Upload your own log files</span></span>

<span data-ttu-id="90826-174">В этом разделе описывается, как toocollect и передача определенных журналах tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="90826-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="90826-175">Требуется toospecify оба hello путь tooyour журнала файла и hello имя таблицы hello место toostore входа.</span><span class="sxs-lookup"><span data-stu-id="90826-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="90826-176">Можно создать несколько файлов журналов, добавив несколько сценариев toohello записи файла или таблицы.</span><span class="sxs-lookup"><span data-stu-id="90826-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="90826-177">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="90826-177">Step 1.</span></span> <span data-ttu-id="90826-178">Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1.</span><span class="sxs-lookup"><span data-stu-id="90826-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="90826-179">Затем создайте другой файл с именем PublicConfig.json с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="90826-179">Then create another file named PublicConfig.json with hello following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="90826-180">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="90826-180">Step 2.</span></span> <span data-ttu-id="90826-181">Запустите `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="90826-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="90826-182">Обратите внимание, что этот параметр на hello расширение версии предыдущих too2.3, все журналы записываются слишком`/var/log/mysql.err` может дублироваться слишком`/var/log/syslog` (или `/var/log/messages` в зависимости от hello дистрибутив Linux) также.</span><span class="sxs-lookup"><span data-stu-id="90826-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="90826-183">Если вы хотите tooavoid полученную копию ведения журнала, можно исключить ведение журнала `local6` средство входит в конфигурацию rsyslog.</span><span class="sxs-lookup"><span data-stu-id="90826-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="90826-184">Зависит от hello дистрибутив Linux, но системе Ubuntu 14.04 является hello файл toomodify `/etc/rsyslog.d/50-default.conf` и может заменить строку hello `*.*;auth,authpriv.none -/var/log/syslog` слишком`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="90826-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="90826-185">Эта проблема исправлена в hello последние исправления версии 2.3 (2.3.9007), поэтому если у вас есть расширение hello версии 2.3, эта проблема не должно произойти.</span><span class="sxs-lookup"><span data-stu-id="90826-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="90826-186">Если по-прежнему не даже после перезапуска ВМ, свяжитесь с нами и помочь нам определить причину hello последнюю версию исправления не устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="90826-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="90826-187">Сценарий 4.</span><span class="sxs-lookup"><span data-stu-id="90826-187">Scenario 4.</span></span> <span data-ttu-id="90826-188">Остановить расширения hello сбор никаких записей журнала</span><span class="sxs-lookup"><span data-stu-id="90826-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="90826-189">В этом разделе описывается, как в журналах расширений hello toostop сбор.</span><span class="sxs-lookup"><span data-stu-id="90826-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="90826-190">Обратите внимание, что процесс агента мониторинга hello будет по-прежнему запущен и работает, даже при наличии перенастройки.</span><span class="sxs-lookup"><span data-stu-id="90826-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="90826-191">Если вы хотите toostop hello полностью контролирует процесс агента, это можно сделать путем отключения расширения hello.</span><span class="sxs-lookup"><span data-stu-id="90826-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="90826-192">— расширение hello Hello команды toodisable `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="90826-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="90826-193">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="90826-193">Step 1.</span></span> <span data-ttu-id="90826-194">Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1.</span><span class="sxs-lookup"><span data-stu-id="90826-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="90826-195">Создайте другой файл с именем PublicConfig.json с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="90826-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="90826-196">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="90826-196">Step 2.</span></span> <span data-ttu-id="90826-197">Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="90826-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="90826-198">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="90826-198">Review your data</span></span>

<span data-ttu-id="90826-199">производительность Hello и диагностические данные хранятся в таблице хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="90826-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="90826-200">Просмотрите [как toouse табличного хранилища Azure из Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn как tooaccess hello данных в хранилище hello таблицу с помощью сценариев Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="90826-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="90826-201">Кроме того можно использовать следующий пользовательский Интерфейс средства tooaccess hello данных:</span><span class="sxs-lookup"><span data-stu-id="90826-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="90826-202">Обозреватель сервера Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90826-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="90826-203">Go tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="90826-203">Go tooyour storage account.</span></span> <span data-ttu-id="90826-204">После выполнения hello ВМ около пяти минут, вы увидите hello четырех таблиц по умолчанию: «LinuxCpu», «LinuxDisk», «LinuxMemory» и «Linuxsyslog».</span><span class="sxs-lookup"><span data-stu-id="90826-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="90826-205">Дважды щелкните hello таблицы имен tooview hello данных.</span><span class="sxs-lookup"><span data-stu-id="90826-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="90826-206">[Обозреватель хранилищ Azure](https://azurestorageexplorer.codeplex.com/ "Обозреватель хранилищ Azure").</span><span class="sxs-lookup"><span data-stu-id="90826-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![изображение](./media/diagnostic-extension/no1.png)

<span data-ttu-id="90826-208">Если вы включили функцию fileCfg или perfCfg (как описано в сценарии 2 и 3), можно использовать обозреватель серверов Visual Studio и обозреватель хранилища Azure данные tooview не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="90826-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="90826-209">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="90826-209">Known issues</span></span>

* <span data-ttu-id="90826-210">Здравствуйте, Rsyslog сведения и клиента указан файл журнала может осуществляться только путем выполнения сценария.</span><span class="sxs-lookup"><span data-stu-id="90826-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
