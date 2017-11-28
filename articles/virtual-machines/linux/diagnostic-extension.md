---
title: "Вычислений aaaAzure - диагностического расширения для Linux | Документы Microsoft"
description: "Как tooconfigure hello toocollect метрики диагностики расширение Azure Linux (LAD) и вести журнал из виртуальных машин Linux, работающих в Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="d8e5c-103">Использовать журналы и показатели toomonitor диагностического расширения для Linux</span><span class="sxs-lookup"><span data-stu-id="d8e5c-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="d8e5c-104">В этом документе описывается версии 3.0 и более поздних из hello диагностического расширения для Linux.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8e5c-105">Сведения о версии 2.3 и более ранних см. в [этом документе](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="d8e5c-106">Введение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-106">Introduction</span></span>

<span data-ttu-id="d8e5c-107">Hello диагностического расширения для Linux помогает пользователю монитор hello работоспособности виртуальной машины Linux в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="d8e5c-108">Он имеет hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="d8e5c-109">Сбор метрик производительности системы hello виртуальной Машины и сохраняет их в конкретную таблицу в учетной записи указанного хранилища.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="d8e5c-110">Получает журнал событий из системного журнала и сохраняет их в конкретную таблицу в hello, назначенные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="d8e5c-111">Позволяет пользователям toocustomize hello данных метрик, которые собраны и отправлены.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="d8e5c-112">Позволяет средств syslog hello toocustomize пользователей и степени серьезности событий, которые собраны и отправлены.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="d8e5c-113">Позволяет пользователям tooupload указанного журнала файлов tooa указанного хранилища таблицы.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="d8e5c-114">Поддержка отправки метрики журнала событий tooarbitrary EventHub конечных точек и и большие двоичные объекты в формате JSON в hello назначить учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="d8e5c-115">Это расширение работает с обеими моделями развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="d8e5c-116">Установка расширения hello в виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="d8e5c-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="d8e5c-117">Это расширение можно включить с помощью командлетов Azure PowerShell hello, скрипты Azure CLI или шаблоны развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="d8e5c-118">Дополнительные сведения см. в статье [Обзор расширений](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="d8e5c-119">Hello портал Azure нельзя использовать tooenable или настроить LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="d8e5c-120">С его помощью устанавливается и настраивается версия 2.3.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="d8e5c-121">Оповещения Azure портала диаграмм и работать с данными из обеих версий расширения hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="d8e5c-122">С помощью этих инструкций по установке и [доступного для скачивания образца конфигурации](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) можно настроить LAD 3.0 для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="d8e5c-123">Создайте и сохраните hello одинаковых метрик как предоставил LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="d8e5c-124">записи полезных метрик системы файл, новый tooLAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="d8e5c-125">записать включаемые LAD 2.3; сбора syslog по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="d8e5c-126">Включите hello взаимодействие с портала Azure для построения графиков и оповещениями на метрики виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="d8e5c-127">Конфигурация, загружаемая Hello всего лишь пример; изменить его toosuit потребностями.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d8e5c-128">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d8e5c-128">Prerequisites</span></span>

* <span data-ttu-id="d8e5c-129">**Агент Linux для Azure 2.2.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="d8e5c-130">Большинство образов в коллекции виртуальных машин Azure на базе Linux включает версию 2.2.7 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="d8e5c-131">Запустите `/usr/sbin/waagent -version` tooconfirm hello версию, установленную на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="d8e5c-132">Если hello виртуальная машина работает под управлением более старой версии hello гостевого агента, выполните [эти инструкции](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate его.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="d8e5c-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-133">**Azure CLI**.</span></span> <span data-ttu-id="d8e5c-134">[Настройка hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) среды на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="d8e5c-135">Здравствуйте wget команду, если вы его еще нет: запустите `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="d8e5c-136">Существующая подписка Azure и существующее хранилище учетной записи в него данных toostore hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="d8e5c-137">Пример установки</span><span class="sxs-lookup"><span data-stu-id="d8e5c-137">Sample installation</span></span>

<span data-ttu-id="d8e5c-138">Заполните hello правильные параметры на hello первые три строки, а затем выполнить этот скрипт как корневой элемент:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="d8e5c-139">URL-адрес Hello hello пример конфигурации и его содержимое, toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="d8e5c-140">Загрузите копию параметров портала hello JSON-файл и настроить его для потребностей.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="d8e5c-141">Все создаваемые вами шаблоны или средства автоматизации должны использовать вашу собственную копию, а не скачивать каждый раз файл по этому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="d8e5c-142">Обновление параметров расширения hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-142">Updating hello extension settings</span></span>

<span data-ttu-id="d8e5c-143">После изменения Protected или открытых параметров, разверните их toohello виртуальной Машины, выполнив hello в одной команде.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="d8e5c-144">Если что-либо изменен в параметрах hello, hello обновлены параметры отправляются toohello расширения.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="d8e5c-145">LAD перезагружает конфигурации hello и перезапускает сам.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="d8e5c-146">Миграция с предыдущих версий расширения hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="d8e5c-147">Последняя версия расширения hello Hello — **3.0**.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="d8e5c-148">**Все предыдущие версии (2.x) не рекомендуются к использованию, и их публикация может быть отменена 31 июля 2018 г. или позднее**.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8e5c-149">Этот модуль предоставляет критические изменения toohello конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="d8e5c-150">Один такой изменения безопасности hello tooimprove hello расширения; в результате обратной совместимости с 2.x может не поддерживаться.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="d8e5c-151">Кроме того hello издателя расширения для этого расширения отличается от издателя hello для версий 2.x hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="d8e5c-152">toomigrate из новой версии 2.x toothis hello расширения необходимо удалить старым расширением hello (под hello старое имя издателя), а затем установить версию 3 hello расширения.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="d8e5c-153">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d8e5c-153">Recommendations:</span></span>

* <span data-ttu-id="d8e5c-154">Установите расширение hello включено обновление автоматического дополнительный номер версии.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="d8e5c-155">В классической модели развертывания виртуальных машин укажите «3.*» hello версии при установке расширения hello с помощью Azure XPLAT-CLI или Powershell.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="d8e5c-156">На развертывания диспетчера ресурсов Azure модель виртуальных машин, включают "«autoUpgradeMinorVersion»: true" в шаблон развертывания виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="d8e5c-157">Используйте новую или другую учетную запись хранения для LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="d8e5c-158">Между LAD 2.3 и LAD 3.0 есть несколько небольших несовместимостей, которые затрудняют использование одной и той же учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="d8e5c-159">LAD 3.0 сохраняет события системного журнала в таблице с другим именем.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="d8e5c-160">Hello counterSpecifier строки для `builtin` метрики различаются LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="d8e5c-161">Защищенные параметры</span><span class="sxs-lookup"><span data-stu-id="d8e5c-161">Protected settings</span></span>

<span data-ttu-id="d8e5c-162">Этот набор данных конфигурации включает в себя конфиденциальные сведения, которые не должны быть общедоступными, например учетные данные для доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="d8e5c-163">Эти параметры используются передаваемых tooand хранятся по расширению hello в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="d8e5c-164">Имя</span><span class="sxs-lookup"><span data-stu-id="d8e5c-164">Name</span></span> | <span data-ttu-id="d8e5c-165">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-165">Value</span></span>
---- | -----
<span data-ttu-id="d8e5c-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="d8e5c-166">storageAccountName</span></span> | <span data-ttu-id="d8e5c-167">Имя учетной записи хранения hello, в котором данные записываются с помощью расширения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="d8e5c-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="d8e5c-168">storageAccountEndPoint</span></span> | <span data-ttu-id="d8e5c-169">Идентификация hello облака, в которой hello учетная запись хранения существует конечная точка hello (необязательно).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="d8e5c-170">Если этот параметр отсутствует, LAD по умолчанию toohello общедоступное облако Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="d8e5c-171">toouse учетной записи хранения в Германии Azure, Azure для государственных или Azure China это значение соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="d8e5c-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="d8e5c-172">storageAccountSasToken</span></span> | <span data-ttu-id="d8e5c-173">[Маркер SAS для учетной записи](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) для службы BLOB-объектов и таблиц (`ss='bt'`), соответствующий toocontainers и объекты (`srt='co'`), добавить какие-либо права, создать, список, обновления и разрешения на запись (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="d8e5c-174">Сделать *не* включают hello первый вопросительный знак (?).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="d8e5c-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="d8e5c-175">mdsdHttpProxy</span></span> | <span data-ttu-id="d8e5c-176">(необязательно) Прокси-сервер HTTP сведения, необходимые hello tooenable расширения toohello tooconnect указан учетной записи хранилища и конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="d8e5c-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="d8e5c-177">sinksConfig</span></span> | <span data-ttu-id="d8e5c-178">(необязательно) Сведения об альтернативных назначения toowhich метрики и события может быть доставлено.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="d8e5c-179">Hello подробные сведения для каждого поддерживаемого расширением hello приемник данных описаны в последующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="d8e5c-180">Легко можно создать токен SAS hello необходимые через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="d8e5c-181">Выберите toowhich учетной записи хранилища общего назначения hello, требуется расширение toowrite hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="d8e5c-182">Выберите «Подписанном URL-адресе» из части левого меню hello параметры hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="d8e5c-183">Сделать hello соответствующих разделов в соответствии с указаниями</span><span class="sxs-lookup"><span data-stu-id="d8e5c-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="d8e5c-184">Нажмите кнопку «Создать SAS» hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-184">Click hello "Generate SAS" button.</span></span>

![изображение](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="d8e5c-186">Hello копирования созданы SAS в поле storageAccountSasToken hello; Удалите hello начальные вопросительным знаком (»?»).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="d8e5c-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="d8e5c-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="d8e5c-188">Этот дополнительный раздел определяет дополнительные назначения, отправляемую расширения hello toowhich hello сведения, полученные.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="d8e5c-189">Массив «приемник» Hello содержит объект для каждого приемника дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="d8e5c-190">Здравствуйте, определяет атрибут «type» hello других атрибутов в hello объекта.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="d8e5c-191">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-191">Element</span></span> | <span data-ttu-id="d8e5c-192">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-192">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-193">name</span><span class="sxs-lookup"><span data-stu-id="d8e5c-193">name</span></span> | <span data-ttu-id="d8e5c-194">Строка, используемое приемник toothis toorefer в другом месте в конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="d8e5c-195">type</span><span class="sxs-lookup"><span data-stu-id="d8e5c-195">type</span></span> | <span data-ttu-id="d8e5c-196">тип приемника определяемой Hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-196">hello type of sink being defined.</span></span> <span data-ttu-id="d8e5c-197">Определяет hello другие значения (если таковые имеются) в экземплярах этого типа.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="d8e5c-198">Версии 3.0 hello диагностического расширения для Linux поддерживает два типа приемника: EventHub и JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="d8e5c-199">приемник EventHub Hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="d8e5c-200">запись «sasURL» Hello содержит полный URL-адрес, включая маркер SAS, для hello toowhich данных концентратора событий должны публиковаться приветствия.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="d8e5c-201">LAD требует именования политики, которая включает утверждение отправки hello SAS.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="d8e5c-202">Пример:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-202">An example:</span></span>

* <span data-ttu-id="d8e5c-203">Создание пространства имен концентраторов событий с именем `contosohub`</span><span class="sxs-lookup"><span data-stu-id="d8e5c-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="d8e5c-204">Создать концентратор событий в hello пространство имен`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="d8e5c-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="d8e5c-205">Создать политику общего доступа для концентратора событий с именем hello `writer` hello, позволяет отправлять утверждения</span><span class="sxs-lookup"><span data-stu-id="d8e5c-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="d8e5c-206">Если вы создали подписанный URL-адрес хорошо до полуночи 1 января 2018, UTC hello sasURL значение может быть:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="d8e5c-207">Дополнительные сведения о создании токенов SAS для концентраторов событий см. на [этой веб-странице](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="d8e5c-208">приемник JsonBlob Hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="d8e5c-209">Данные направлены приемник JsonBlob tooa хранится в BLOB-объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="d8e5c-210">Каждый экземпляр LAD каждый час создает BLOB-объект для каждого имени приемника.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="d8e5c-211">Каждый BLOB-объект всегда содержит синтаксически правильный массив JSON объекта.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="d8e5c-212">Массив toohello атомарным образом добавляются новые записи.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="d8e5c-213">Большие двоичные объекты хранятся в контейнере с точно такое же имя в качестве приемника hello hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="d8e5c-214">Здравствуйте правила хранилища Azure имена контейнеров больших двоичных объектов относиться имена toohello JsonBlob приемников: от 3 до 63 строчные буквенно-цифровые символы ASCII или дефисы.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="d8e5c-215">Общедоступные параметры</span><span class="sxs-lookup"><span data-stu-id="d8e5c-215">Public settings</span></span>

<span data-ttu-id="d8e5c-216">Эта структура содержит различные блоки параметры, определяющие hello сведения, собранные с помощью расширения hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="d8e5c-217">Все параметры являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-217">Each setting is optional.</span></span> <span data-ttu-id="d8e5c-218">При указании `ladCfg` также необходимо указать `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="d8e5c-219">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-219">Element</span></span> | <span data-ttu-id="d8e5c-220">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-220">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="d8e5c-221">StorageAccount</span></span> | <span data-ttu-id="d8e5c-222">Имя учетной записи хранения hello, в котором данные записываются с помощью расширения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="d8e5c-223">Должны быть одинаковые имена, как указано в hello hello [защищенные параметры](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="d8e5c-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="d8e5c-224">mdsdHttpProxy</span></span> | <span data-ttu-id="d8e5c-225">(необязательно) Отличается от используемого hello [защищенные параметры](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="d8e5c-226">значение открытого Hello переопределяется значение частного hello, если задать.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="d8e5c-227">Поместите параметры прокси-сервера, которые содержат секрета, например пароль в hello [защищенные параметры](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="d8e5c-228">остальные элементы Hello подробно описываются в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="d8e5c-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="d8e5c-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="d8e5c-230">Приемники метрик и журналов для доставки toohello службы и tooother данные метрик Azure сборе данных hello необязательно структуры элементов управления.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="d8e5c-231">Необходимо указать `performanceCounters`, `syslogEvents` или и то, и другое.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="d8e5c-232">Необходимо указать hello `metrics` структуры.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="d8e5c-233">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-233">Element</span></span> | <span data-ttu-id="d8e5c-234">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-234">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="d8e5c-235">eventVolume</span></span> | <span data-ttu-id="d8e5c-236">(необязательно) Элементы управления hello число секций, создаваемых в таблицу хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="d8e5c-237">Должно иметь значение `"Large"`, `"Medium"` или `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="d8e5c-238">Если не указан, значение по умолчанию hello — `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="d8e5c-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="d8e5c-239">sampleRateInSeconds</span></span> | <span data-ttu-id="d8e5c-240">Интервал по умолчанию (необязательно) hello между сбор метрик raw (необъединенных).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="d8e5c-241">частота выборки наименьшее Hello поддерживается составляет 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="d8e5c-242">Если не указан, значение по умолчанию hello — `15`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="d8e5c-243">Метрики</span><span class="sxs-lookup"><span data-stu-id="d8e5c-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="d8e5c-244">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-244">Element</span></span> | <span data-ttu-id="d8e5c-245">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-245">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="d8e5c-246">resourceId</span></span> | <span data-ttu-id="d8e5c-247">Идентификатор ресурса диспетчера ресурсов Azure Hello hello виртуальной Машины или масштабирования виртуальных машин hello задать toowhich hello, к которому относится виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="d8e5c-248">Этот параметр должен быть также указан, если любой приемник JsonBlob используется в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="d8e5c-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="d8e5c-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="d8e5c-250">Hello частоту, с которой статистические показатели, toobe вычисляемые столбцы и передаются tooAzure метрик, выраженное как 8601 — интервал времени.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="d8e5c-251">Наименьший период передачи Hello составляет 60 секунд, то есть PT1M.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="d8e5c-252">Необходимо указать по крайней мере одно значение scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="d8e5c-253">Образцы приветствия показатели, указанные в разделе performanceCounters hello собираются каждые 15 секунд или скоростью образец hello, явно определенные для счетчика "hello".</span><span class="sxs-lookup"><span data-stu-id="d8e5c-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="d8e5c-254">Если несколько частот scheduledTransferPeriod отображается (как в примере hello), каждое статистическое выражение вычисляется независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="d8e5c-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="d8e5c-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="d8e5c-256">Этот дополнительный раздел управляет hello сбор метрик.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="d8e5c-257">Образцы необработанные вычисляются для каждого [scheduledTransferPeriod](#metrics) tooproduce следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="d8e5c-258">mean</span><span class="sxs-lookup"><span data-stu-id="d8e5c-258">mean</span></span>
* <span data-ttu-id="d8e5c-259">minimum</span><span class="sxs-lookup"><span data-stu-id="d8e5c-259">minimum</span></span>
* <span data-ttu-id="d8e5c-260">maximum</span><span class="sxs-lookup"><span data-stu-id="d8e5c-260">maximum</span></span>
* <span data-ttu-id="d8e5c-261">последнее собранное значение;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-261">last-collected value</span></span>
* <span data-ttu-id="d8e5c-262">Количество необработанных выборок используется статистическая функция toocompute hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="d8e5c-263">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-263">Element</span></span> | <span data-ttu-id="d8e5c-264">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-264">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-265">sinks</span><span class="sxs-lookup"><span data-stu-id="d8e5c-265">sinks</span></span> | <span data-ttu-id="d8e5c-266">(необязательно) Список разделенных запятыми имен приемников toowhich LAD отправляет агрегированных результатов метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="d8e5c-267">Все статистические показатели являются приемник опубликованных tooeach в списке.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="d8e5c-268">См. [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="d8e5c-269">Пример: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="d8e5c-270">type</span><span class="sxs-lookup"><span data-stu-id="d8e5c-270">type</span></span> | <span data-ttu-id="d8e5c-271">Определяет поставщика фактическое hello hello метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="d8e5c-272">class</span><span class="sxs-lookup"><span data-stu-id="d8e5c-272">class</span></span> | <span data-ttu-id="d8e5c-273">Вместе с «счетчик» определяет конкретную метрику hello в пространство имен поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="d8e5c-274">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-274">counter</span></span> | <span data-ttu-id="d8e5c-275">Вместе с «класс» определяет конкретную метрику hello в пространство имен поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="d8e5c-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="d8e5c-276">counterSpecifier</span></span> | <span data-ttu-id="d8e5c-277">Определяет конкретную метрику hello в пределах пространства имен метрики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="d8e5c-278">condition</span><span class="sxs-lookup"><span data-stu-id="d8e5c-278">condition</span></span> | <span data-ttu-id="d8e5c-279">(необязательно) Выбирает экземпляр hello объекта toowhich hello метрики применяет или выбирает hello статистической обработки для всех экземпляров этого объекта.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="d8e5c-280">Дополнительные сведения см. в разделе hello [ `builtin` определения показателей](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="d8e5c-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="d8e5c-281">sampleRate</span></span> | <span data-ttu-id="d8e5c-282">— 8601 интервала, который задает скорость hello собранные необработанные образцов для этой метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="d8e5c-283">Если не задан, интервал сбора hello задается значение hello [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="d8e5c-284">Hello кратчайший поддерживаемых дискретизации составляет 15 секунд (PT15S).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="d8e5c-285">unit</span><span class="sxs-lookup"><span data-stu-id="d8e5c-285">unit</span></span> | <span data-ttu-id="d8e5c-286">Значением должна быть одна из следующих строк: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="d8e5c-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="d8e5c-287">Определяет единицу hello hello метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="d8e5c-288">Потребители данных, собранных hello ожидается, что hello собранные данные значения toomatch это устройство.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="d8e5c-289">LAD игнорирует это поле.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-289">LAD ignores this field.</span></span>
<span data-ttu-id="d8e5c-290">displayName</span><span class="sxs-lookup"><span data-stu-id="d8e5c-290">displayName</span></span> | <span data-ttu-id="d8e5c-291">toobe метки (в hello язык, заданный параметром hello параметр соответствующий языковой стандарт) Hello присоединенного toothis данных в Azure метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="d8e5c-292">LAD игнорирует это поле.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-292">LAD ignores this field.</span></span>

<span data-ttu-id="d8e5c-293">Hello counterSpecifier представляет произвольный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="d8e5c-294">Потребители показателей, как hello Azure портала построения графиков и компонента, предупреждения об изменении counterSpecifier служит hello «ключ», который определяет метрики или экземпляра метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="d8e5c-295">Для метрик `builtin` рекомендуется использовать значения counterSpecifier, начинающиеся с `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="d8e5c-296">При сборе экземпляр метрики, рекомендуется присоединить идентификатор hello значения counterSpecifier toohello экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="d8e5c-297">Некоторые примеры</span><span class="sxs-lookup"><span data-stu-id="d8e5c-297">Some examples:</span></span>

* <span data-ttu-id="d8e5c-298">`/builtin/Processor/PercentIdleTime` — среднее время простоя всех ядер;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="d8e5c-299">`/builtin/Disk/FreeSpace(/mnt)`-Свободного пространства для файловой системы/mnt hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="d8e5c-300">`/builtin/Disk/FreeSpace` — средний объем свободного пространства для всех подключенных файловых систем.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="d8e5c-301">LAD ни hello портал Azure предполагает, что значение toomatch hello counterSpecifier любой шаблон.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="d8e5c-302">При формировании значений counterSpecifier соблюдайте единообразие.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="d8e5c-303">При указании `performanceCounters`, LAD всегда записывает tooa таблицы данных в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="d8e5c-304">Вы может иметь hello же данные, записанные tooJSON больших двоичных объектов и/или концентраторов событий, но не удается отключить таблицу tooa хранение данных.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="d8e5c-305">Все экземпляры toouse диагностического расширения, настроенного hello hello учетную запись хранения имени и конечной точки добавьте свои журналы и показатели toohello одной таблицы.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="d8e5c-306">Если записи слишком много виртуальных машин toohello, которые могут привести к перегрузке секции таблицы, Azure записывает toothat секции.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="d8e5c-307">параметр toobe записи причины eventVolume Hello распределены 1 (маленький), 10 (средний) или 100 (крупный) различных секций.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="d8e5c-308">Как правило, «Средний» достаточно tooensure трафик не регулируется.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="d8e5c-309">компонент Azure метрики Hello hello портал Azure использует hello данные в этой таблице tooproduce диаграмм или tootrigger предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="d8e5c-310">Имя таблицы Hello-hello объединение этих строк:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="d8e5c-311">Hello «scheduledTransferPeriod» для hello статистическая обработка значений, хранящихся в таблице hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="d8e5c-312">Даты в форме hello «ГГГГММДД», изменяется в течение 10 дней</span><span class="sxs-lookup"><span data-stu-id="d8e5c-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="d8e5c-313">Примеры: `WADMetricsPT1HP10DV2S20170410` и `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="d8e5c-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="d8e5c-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="d8e5c-315">Этот дополнительный раздел управляет hello коллекции журналов событий из системного журнала.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="d8e5c-316">Если раздел hello опущен, события syslog вообще не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="d8e5c-317">Коллекция syslogEventConfiguration Hello содержит одну запись для каждого средства syslog, представляющие интерес.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="d8e5c-318">Если minSeverity является «Нет» для определенной территории или этого средства не отображаются в элементе hello, события из этого устройства не регистрируются.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="d8e5c-319">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-319">Element</span></span> | <span data-ttu-id="d8e5c-320">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-320">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-321">sinks</span><span class="sxs-lookup"><span data-stu-id="d8e5c-321">sinks</span></span> | <span data-ttu-id="d8e5c-322">Список разделенных запятыми имен приемников toowhich отдельный журнал событий публикуются.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="d8e5c-323">Всех журналов событий, соответствующих ограничений hello в syslogEventConfiguration являются приемник опубликованных tooeach в списке.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="d8e5c-324">Пример: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="d8e5c-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="d8e5c-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="d8e5c-325">facilityName</span></span> | <span data-ttu-id="d8e5c-326">Имя субъекта системного журнала (например, "LOG\_USER" или "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="d8e5c-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="d8e5c-327">Обратитесь к разделу «средства» hello hello [syslog справочную страницу](http://man7.org/linux/man-pages/man3/syslog.3.html) для полного списка hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="d8e5c-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="d8e5c-328">minSeverity</span></span> | <span data-ttu-id="d8e5c-329">Уровень серьезности системного журнала (например, "LOG\_ERR" или "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="d8e5c-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="d8e5c-330">Обратитесь к разделу «уровень» hello hello [syslog справочную страницу](http://man7.org/linux/man-pages/man3/syslog.3.html) для полного списка hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="d8e5c-331">расширение Hello захватывает toohello события, отправляемые на первом или выше hello указанный уровень.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="d8e5c-332">При указании `syslogEvents`, LAD всегда записывает tooa таблицы данных в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="d8e5c-333">Вы может иметь hello же данные, записанные tooJSON больших двоичных объектов и/или концентраторов событий, но не удается отключить таблицу tooa хранение данных.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="d8e5c-334">Здравствуйте Hello секционирование поведение для этой таблицы, так же, как описано для `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="d8e5c-335">Имя таблицы Hello-hello объединение этих строк:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="d8e5c-336">Даты в форме hello «ГГГГММДД», изменяется в течение 10 дней</span><span class="sxs-lookup"><span data-stu-id="d8e5c-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="d8e5c-337">Примеры: `LinuxSyslog20170410` и `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="d8e5c-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="d8e5c-338">perfCfg</span></span>

<span data-ttu-id="d8e5c-339">Этот необязательный раздел управляет выполнением произвольных запросов [OMI](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="d8e5c-340">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-340">Element</span></span> | <span data-ttu-id="d8e5c-341">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-341">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-342">пространство_имен</span><span class="sxs-lookup"><span data-stu-id="d8e5c-342">namespace</span></span> | <span data-ttu-id="d8e5c-343">(необязательно) hello OMI пространство имен, в какие hello должен выполняться запрос.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="d8e5c-344">Если не указан, значение по умолчанию hello — «корневой/scx», реализуемый hello [поставщики кросс платформенных System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="d8e5c-345">query</span><span class="sxs-lookup"><span data-stu-id="d8e5c-345">query</span></span> | <span data-ttu-id="d8e5c-346">выполнен запрос toobe OMI Hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="d8e5c-347">таблица</span><span class="sxs-lookup"><span data-stu-id="d8e5c-347">table</span></span> | <span data-ttu-id="d8e5c-348">(необязательно) hello хранилища Azure таблицы в hello, назначенные учетной записи хранения (в разделе [защищенные параметры](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="d8e5c-349">frequency</span><span class="sxs-lookup"><span data-stu-id="d8e5c-349">frequency</span></span> | <span data-ttu-id="d8e5c-350">количество секунд между выполнением запроса hello hello (необязательно).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="d8e5c-351">Значение по умолчанию — 300 (5 минут); минимальное значение — 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="d8e5c-352">sinks</span><span class="sxs-lookup"><span data-stu-id="d8e5c-352">sinks</span></span> | <span data-ttu-id="d8e5c-353">(необязательно) Список разделенных запятыми имен результатов метрики необработанные образец toowhich дополнительных приемники необходимо опубликовать.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="d8e5c-354">Ни один агрегат в этих примерах необработанные вычисляемым модулем hello Azure метрик.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="d8e5c-355">Необходимо указать либо table, либо sinks, либо оба эти элемента.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="d8e5c-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="d8e5c-356">fileLogs</span></span>

<span data-ttu-id="d8e5c-357">Элементы управления hello записи файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-357">Controls hello capture of log files.</span></span> <span data-ttu-id="d8e5c-358">LAD захватывает новые строки текста, как они записываются в файл toohello и записывает их tootable строк и/или любой указанной приемники (JsonBlob или EventHub).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="d8e5c-359">Элемент</span><span class="sxs-lookup"><span data-stu-id="d8e5c-359">Element</span></span> | <span data-ttu-id="d8e5c-360">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-360">Value</span></span>
------- | -----
<span data-ttu-id="d8e5c-361">file</span><span class="sxs-lookup"><span data-stu-id="d8e5c-361">file</span></span> | <span data-ttu-id="d8e5c-362">Hello полным путем к toobe файла журнала hello наблюдали и записи.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="d8e5c-363">Hello путь должен указывать имя одного файла, он не имя каталога или содержать подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="d8e5c-364">таблица</span><span class="sxs-lookup"><span data-stu-id="d8e5c-364">table</span></span> | <span data-ttu-id="d8e5c-365">(необязательно) hello хранилища Azure таблицы в назначенный hello хранилища учетной записи (как указано в конфигурации hello защищенный), в какие новые строки hello «с префиксом tail «hello файла записи.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="d8e5c-366">sinks</span><span class="sxs-lookup"><span data-stu-id="d8e5c-366">sinks</span></span> | <span data-ttu-id="d8e5c-367">(необязательно) Список разделенных запятыми имен строк журнала toowhich дополнительных приемники отправлено.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="d8e5c-368">Необходимо указать либо table, либо sinks, либо оба эти элемента.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="d8e5c-369">Метрики, поддерживаемых поставщиком builtin hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="d8e5c-370">Hello builtin метрики поставщик является источником метрики наиболее интересные tooa широкого набора пользователей.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="d8e5c-371">Эти метрики делятся на пять основных классов:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="d8e5c-372">Процессор</span><span class="sxs-lookup"><span data-stu-id="d8e5c-372">Processor</span></span>
* <span data-ttu-id="d8e5c-373">Память</span><span class="sxs-lookup"><span data-stu-id="d8e5c-373">Memory</span></span>
* <span data-ttu-id="d8e5c-374">Сеть</span><span class="sxs-lookup"><span data-stu-id="d8e5c-374">Network</span></span>
* <span data-ttu-id="d8e5c-375">Файловая система</span><span class="sxs-lookup"><span data-stu-id="d8e5c-375">Filesystem</span></span>
* <span data-ttu-id="d8e5c-376">Диск</span><span class="sxs-lookup"><span data-stu-id="d8e5c-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="d8e5c-377">показатели Builtin hello класса процессора</span><span class="sxs-lookup"><span data-stu-id="d8e5c-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="d8e5c-378">Hello класса процессора метрик сведения о загрузке процессора в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="d8e5c-379">При статистической обработке проценты, hello результат — hello среднее для всех процессоров.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="d8e5c-380">В двух основных виртуальных Машин Если одно ядро был занят 100%, а hello других — 100% простоя, hello сообщила, что PercentIdleTime будет равно 50.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="d8e5c-381">Если каждое ядро был занят для 50% hello же период, hello сообщил, что результат также будет равно 50.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="d8e5c-382">В четырех основных компонентов виртуальной Машины, занят одно ядро 100% и hello простоя, другие hello сообщила, что PercentIdleTime бы 75.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="d8e5c-383">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-383">counter</span></span> | <span data-ttu-id="d8e5c-384">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-384">Meaning</span></span>
------- | -------
<span data-ttu-id="d8e5c-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-385">PercentIdleTime</span></span> | <span data-ttu-id="d8e5c-386">Процент времени, во время периода hello статистической обработки, что процессоров выполнялись hello ядра пустых циклов</span><span class="sxs-lookup"><span data-stu-id="d8e5c-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="d8e5c-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-387">PercentProcessorTime</span></span> | <span data-ttu-id="d8e5c-388">Процент времени, который был затрачен на выполнение всех потоков, кроме бездействующего.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="d8e5c-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-389">PercentIOWaitTime</span></span> | <span data-ttu-id="d8e5c-390">Процент времени ожидания toocomplete операций ввода-ВЫВОДА</span><span class="sxs-lookup"><span data-stu-id="d8e5c-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="d8e5c-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-391">PercentInterruptTime</span></span> | <span data-ttu-id="d8e5c-392">Процент времени, затраченный на выполнение аппаратных и программных прерываний и отложенных вызовов процедур.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="d8e5c-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-393">PercentUserTime</span></span> | <span data-ttu-id="d8e5c-394">Простаивающего время окно агрегата hello hello процент времени, затраченный на пользователя более с обычным приоритетом</span><span class="sxs-lookup"><span data-stu-id="d8e5c-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="d8e5c-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-395">PercentNiceTime</span></span> | <span data-ttu-id="d8e5c-396">Времени hello процент затраченного снижения приоритетом (хорошо)</span><span class="sxs-lookup"><span data-stu-id="d8e5c-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="d8e5c-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="d8e5c-398">Времени hello процент затраченного в привилегированном режиме</span><span class="sxs-lookup"><span data-stu-id="d8e5c-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="d8e5c-399">Hello первые четыре счетчики сумма должна составлять too100%.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="d8e5c-400">Hello последние три счетчики также сумма too100%; они разделить сумму hello PercentProcessorTime, PercentIOWaitTime и PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="d8e5c-401">задать один показатель статистически обрабатываются для всех процессоров tooobtain `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="d8e5c-402">tooobtain метрики для конкретного процессора, так как второй логический процессор hello из четырех основных виртуальных Машин, установите `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="d8e5c-403">Номера логических процессоров находятся в диапазоне hello `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="d8e5c-404">показатели Builtin hello класс памяти</span><span class="sxs-lookup"><span data-stu-id="d8e5c-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="d8e5c-405">Hello класса памяти метрик предоставляет сведения об использовании памяти, разбиение по страницам и замены.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="d8e5c-406">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-406">counter</span></span> | <span data-ttu-id="d8e5c-407">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-407">Meaning</span></span>
------- | -------
<span data-ttu-id="d8e5c-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="d8e5c-408">AvailableMemory</span></span> | <span data-ttu-id="d8e5c-409">Доступный объем физической памяти в МиБ.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-409">Available physical memory in MiB</span></span>
<span data-ttu-id="d8e5c-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="d8e5c-410">PercentAvailableMemory</span></span> | <span data-ttu-id="d8e5c-411">Доступный объем физической памяти в процентах от общего объема памяти.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="d8e5c-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="d8e5c-412">UsedMemory</span></span> | <span data-ttu-id="d8e5c-413">Используемый объем физической памяти (МиБ).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="d8e5c-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="d8e5c-414">PercentUsedMemory</span></span> | <span data-ttu-id="d8e5c-415">Используемый объем физической памяти в процентах от общего объема памяти.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="d8e5c-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="d8e5c-416">PagesPerSec</span></span> | <span data-ttu-id="d8e5c-417">Общее количество операций подкачки (чтения и записи).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-417">Total paging (read/write)</span></span>
<span data-ttu-id="d8e5c-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="d8e5c-418">PagesReadPerSec</span></span> | <span data-ttu-id="d8e5c-419">Число страниц, считанных из резервного хранилища (файла подкачки, файла программы, сопоставленного файла и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="d8e5c-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="d8e5c-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="d8e5c-421">Страниц, записанных toobacking хранения (файл подкачки, сопоставленный файл, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="d8e5c-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="d8e5c-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="d8e5c-422">AvailableSwap</span></span> | <span data-ttu-id="d8e5c-423">Размер неиспользуемой области подкачки (МиБ).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="d8e5c-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="d8e5c-424">PercentAvailableSwap</span></span> | <span data-ttu-id="d8e5c-425">Размер неиспользуемой области подкачки в процентах от общего размера области подкачки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="d8e5c-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="d8e5c-426">UsedSwap</span></span> | <span data-ttu-id="d8e5c-427">Размер используемой области подкачки (МиБ).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="d8e5c-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="d8e5c-428">PercentUsedSwap</span></span> | <span data-ttu-id="d8e5c-429">Размер используемой области подкачки в процентах от общего размера области подкачки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="d8e5c-430">Этот класс метрик имеет только один экземпляр.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="d8e5c-431">атрибут «условие» Hello не имеет полезных параметров и должен быть опущен.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="d8e5c-432">встроенные метрики для класса сети hello</span><span class="sxs-lookup"><span data-stu-id="d8e5c-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="d8e5c-433">Hello класса сети метрик сведения о сетевой активности для отдельных сетевых интерфейсов с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="d8e5c-434">LAD не предоставляет метрики пропускной способности, которые можно получить из метрик узла.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="d8e5c-435">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-435">counter</span></span> | <span data-ttu-id="d8e5c-436">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-436">Meaning</span></span>
------- | -------
<span data-ttu-id="d8e5c-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="d8e5c-437">BytesTransmitted</span></span> | <span data-ttu-id="d8e5c-438">Общее количество байт, отправленное с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-438">Total bytes sent since boot</span></span>
<span data-ttu-id="d8e5c-439">Получено байт</span><span class="sxs-lookup"><span data-stu-id="d8e5c-439">BytesReceived</span></span> | <span data-ttu-id="d8e5c-440">Общее количество байт, полученное с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-440">Total bytes received since boot</span></span>
<span data-ttu-id="d8e5c-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="d8e5c-441">BytesTotal</span></span> | <span data-ttu-id="d8e5c-442">Общее количество байт, отправленное или полученное с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="d8e5c-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="d8e5c-443">PacketsTransmitted</span></span> | <span data-ttu-id="d8e5c-444">Общее количество пакетов, отправленных с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-444">Total packets sent since boot</span></span>
<span data-ttu-id="d8e5c-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="d8e5c-445">PacketsReceived</span></span> | <span data-ttu-id="d8e5c-446">Общее количество пакетов, полученных с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-446">Total packets received since boot</span></span>
<span data-ttu-id="d8e5c-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="d8e5c-447">TotalRxErrors</span></span> | <span data-ttu-id="d8e5c-448">Количество ошибок приема с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-448">Number of receive errors since boot</span></span>
<span data-ttu-id="d8e5c-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="d8e5c-449">TotalTxErrors</span></span> | <span data-ttu-id="d8e5c-450">Количество ошибок передачи с момента загрузки.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="d8e5c-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="d8e5c-451">TotalCollisions</span></span> | <span data-ttu-id="d8e5c-452">Число конфликтов, о которых сообщили hello сетевые порты с момента загрузки</span><span class="sxs-lookup"><span data-stu-id="d8e5c-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="d8e5c-453">Хотя экземпляры этого класса создаются, LAD не поддерживает сбор совокупных метрик сети по всем сетевым устройствам.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="d8e5c-454">задать tooobtain hello метрики для определенного интерфейса, такие как eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="d8e5c-455">показатели Builtin hello класса файловой системы</span><span class="sxs-lookup"><span data-stu-id="d8e5c-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="d8e5c-456">Класс файловой системы показателей Hello содержит сведения об использовании файловой системы.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="d8e5c-457">Абсолютное и процентное значения выводятся как отображаемых tooan обычного пользователя (не root).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="d8e5c-458">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-458">counter</span></span> | <span data-ttu-id="d8e5c-459">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-459">Meaning</span></span>
------- | -------
<span data-ttu-id="d8e5c-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="d8e5c-460">FreeSpace</span></span> | <span data-ttu-id="d8e5c-461">Доступное дисковое пространство в байтах.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-461">Available disk space in bytes</span></span>
<span data-ttu-id="d8e5c-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="d8e5c-462">UsedSpace</span></span> | <span data-ttu-id="d8e5c-463">Используемое дисковое пространство в байтах.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-463">Used disk space in bytes</span></span>
<span data-ttu-id="d8e5c-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="d8e5c-464">PercentFreeSpace</span></span> | <span data-ttu-id="d8e5c-465">Процент свободного пространства.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-465">Percentage free space</span></span>
<span data-ttu-id="d8e5c-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="d8e5c-466">PercentUsedSpace</span></span> | <span data-ttu-id="d8e5c-467">Процент используемого пространства.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-467">Percentage used space</span></span>
<span data-ttu-id="d8e5c-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="d8e5c-468">PercentFreeInodes</span></span> | <span data-ttu-id="d8e5c-469">Процент неиспользуемых inode.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-469">Percentage of unused inodes</span></span>
<span data-ttu-id="d8e5c-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="d8e5c-470">PercentUsedInodes</span></span> | <span data-ttu-id="d8e5c-471">Процент выделенных (используемых) inode по всем файловым системам.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="d8e5c-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-472">BytesReadPerSecond</span></span> | <span data-ttu-id="d8e5c-473">Число прочитанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-473">Bytes read per second</span></span>
<span data-ttu-id="d8e5c-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="d8e5c-475">Число записанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-475">Bytes written per second</span></span>
<span data-ttu-id="d8e5c-476">Байт/с</span><span class="sxs-lookup"><span data-stu-id="d8e5c-476">BytesPerSecond</span></span> | <span data-ttu-id="d8e5c-477">Число прочитанных или записанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-477">Bytes read or written per second</span></span>
<span data-ttu-id="d8e5c-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-478">ReadsPerSecond</span></span> | <span data-ttu-id="d8e5c-479">Число операций чтения за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-479">Read operations per second</span></span>
<span data-ttu-id="d8e5c-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-480">WritesPerSecond</span></span> | <span data-ttu-id="d8e5c-481">Число операций записи за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-481">Write operations per second</span></span>
<span data-ttu-id="d8e5c-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-482">TransfersPerSecond</span></span> | <span data-ttu-id="d8e5c-483">Число операций чтения или записи за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-483">Read or write operations per second</span></span>

<span data-ttu-id="d8e5c-484">Совокупные значения по всем файловым системам можно получить, задав `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="d8e5c-485">Значения для определенной подключенной файловой системы, например "/mnt", можно получить, задав `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="d8e5c-486">показатели Builtin hello класса диск</span><span class="sxs-lookup"><span data-stu-id="d8e5c-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="d8e5c-487">Hello класса диск метрик предоставляет сведения об использовании диска устройства.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="d8e5c-488">Эти статистические данные применяются ко всему диску toohello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="d8e5c-489">В случае нескольких файловых систем на устройстве, hello счетчики для этого устройства являются, по сути, статистически обрабатываются по всем из них.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="d8e5c-490">Счетчик</span><span class="sxs-lookup"><span data-stu-id="d8e5c-490">counter</span></span> | <span data-ttu-id="d8e5c-491">Значение</span><span class="sxs-lookup"><span data-stu-id="d8e5c-491">Meaning</span></span>
------- | -------
<span data-ttu-id="d8e5c-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-492">ReadsPerSecond</span></span> | <span data-ttu-id="d8e5c-493">Число операций чтения за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-493">Read operations per second</span></span>
<span data-ttu-id="d8e5c-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-494">WritesPerSecond</span></span> | <span data-ttu-id="d8e5c-495">Число операций записи за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-495">Write operations per second</span></span>
<span data-ttu-id="d8e5c-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-496">TransfersPerSecond</span></span> | <span data-ttu-id="d8e5c-497">Общее число операций за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-497">Total operations per second</span></span>
<span data-ttu-id="d8e5c-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-498">AverageReadTime</span></span> | <span data-ttu-id="d8e5c-499">Среднее число секунд на операцию чтения.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-499">Average seconds per read operation</span></span>
<span data-ttu-id="d8e5c-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-500">AverageWriteTime</span></span> | <span data-ttu-id="d8e5c-501">Среднее число секунд на операцию записи.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-501">Average seconds per write operation</span></span>
<span data-ttu-id="d8e5c-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="d8e5c-502">AverageTransferTime</span></span> | <span data-ttu-id="d8e5c-503">Среднее число секунд на операцию.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-503">Average seconds per operation</span></span>
<span data-ttu-id="d8e5c-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="d8e5c-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="d8e5c-505">Среднее число операций с диском, помещенных в очередь.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-505">Average number of queued disk operations</span></span>
<span data-ttu-id="d8e5c-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="d8e5c-507">Количество прочитанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-507">Number of bytes read per second</span></span>
<span data-ttu-id="d8e5c-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="d8e5c-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="d8e5c-509">Количество записанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-509">Number of bytes written per second</span></span>
<span data-ttu-id="d8e5c-510">Байт/с</span><span class="sxs-lookup"><span data-stu-id="d8e5c-510">BytesPerSecond</span></span> | <span data-ttu-id="d8e5c-511">Количество прочитанных или записанных байт за секунду.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="d8e5c-512">Совокупные значения по всем дискам можно получить, задав `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="d8e5c-513">задать сведения о tooget для конкретного устройства (например, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="d8e5c-514">Установка и настройка LAD 3.0 с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="d8e5c-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="d8e5c-515">При условии, что защищенный параметры находятся в файле hello PrivateConfig.json открытой конфигурации данные имеют PublicConfig.json, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="d8e5c-516">Hello предполагается, что вы используете режим управления ресурсами Azure hello (arm) hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="d8e5c-517">tooconfigure LAD для классического развертывания модель виртуальных машин (ASM), слишком переключения режима «asm» (`azure config mode asm`) и не указывайте имя группы ресурсов hello в команде hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="d8e5c-518">Дополнительные сведения см. в разделе hello [документации CLI кросс платформенных](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="d8e5c-519">Пример конфигурации LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="d8e5c-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="d8e5c-520">На основании предшествующий определений, здесь в образце конфигурации расширения LAD 3.0 с некоторыми пояснениями hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="d8e5c-521">tooapply tooyour этот образец варианта, следует использовать имя учетной записи хранилища, учесть маркер SAS и маркеры EventHubs SAS.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="d8e5c-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="d8e5c-522">PrivateConfig.json</span></span>

<span data-ttu-id="d8e5c-523">Эти закрытые параметры настраивают:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-523">These private settings configure:</span></span>

* <span data-ttu-id="d8e5c-524">учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-524">a storage account</span></span>
* <span data-ttu-id="d8e5c-525">соответствующий токен SAS учетной записи;</span><span class="sxs-lookup"><span data-stu-id="d8e5c-525">a matching account SAS token</span></span>
* <span data-ttu-id="d8e5c-526">несколько приемников (JsonBlob или EventHubs с токенами SAS).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="d8e5c-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="d8e5c-527">PublicConfig.json</span></span>

<span data-ttu-id="d8e5c-528">Эти общедоступные параметры обеспечивают выполнение расширением LAD следующих действий:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="d8e5c-529">Отправка toohello метрик процент загруженности процессора и использовать дискового пространства `WADMetrics*` таблицы</span><span class="sxs-lookup"><span data-stu-id="d8e5c-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="d8e5c-530">Отправка сообщения системного журнала toohello средство «user» и серьезности «info» `LinuxSyslog*` таблицы</span><span class="sxs-lookup"><span data-stu-id="d8e5c-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="d8e5c-531">Передать необработанные OMI запроса результаты (PercentProcessorTime и PercentIdleTime) toohello с именем `LinuxCPU` таблицы</span><span class="sxs-lookup"><span data-stu-id="d8e5c-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="d8e5c-532">Отправка строк, добавленных в файле `/var/log/myladtestlog` toohello `MyLadTestLog` таблицы</span><span class="sxs-lookup"><span data-stu-id="d8e5c-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="d8e5c-533">В каждом случае данные также передаются в следующие места:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="d8e5c-534">Хранилище больших двоичных объектов Azure (имя контейнера — как определено в приемник hello JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="d8e5c-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="d8e5c-535">Конечная точка EventHubs (как указано в приемник hello EventHubs)</span><span class="sxs-lookup"><span data-stu-id="d8e5c-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="d8e5c-536">Hello `resourceId` в hello конфигурации должны совпадать, масштабирования виртуальных машин виртуальной Машины или hello hello набора.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="d8e5c-537">Метрики платформы Azure построения графиков и предупреждений об изменении знает resourceId hello объекта hello виртуальной Машины, над которыми вы работаете.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="d8e5c-538">Ожидается, что toofind hello данных для виртуальной Машины с помощью hello resourceId hello Уточняющий запрос ключа.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="d8e5c-539">При использовании автомасштабирования Azure resourceId hello в настройки автомасштабирования hello должно соответствовать используемой LAD resourceId hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="d8e5c-540">Hello resourceId встроено в написанном LAD JsonBlobs имена hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="d8e5c-541">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="d8e5c-541">View your data</span></span>

<span data-ttu-id="d8e5c-542">Используйте данные о производительности Azure портала tooview hello или настроить оповещения:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![изображение](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="d8e5c-544">Hello `performanceCounters` данные всегда хранятся в таблице хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="d8e5c-545">Интерфейсы API службы хранилища Azure доступны для множества языков и платформ.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="d8e5c-546">Данные, отправляемые приемники tooJsonBlob хранится в BLOB-объектов в hello учетной записи хранилища с именем в hello [защищенные параметры](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="d8e5c-547">Вы можете использовать hello данных blob при помощи любого API хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="d8e5c-548">Кроме того можно использовать эти данные hello tooaccess средства пользовательского интерфейса в службе хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="d8e5c-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="d8e5c-549">Обозреватель сервера Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="d8e5c-550">[Обозреватель хранилищ Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Обозреватель хранилищ Azure").</span><span class="sxs-lookup"><span data-stu-id="d8e5c-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="d8e5c-551">Этот моментальный снимок сеанса Microsoft Azure Storage Explorer показывает hello созданные таблицы хранилища Azure и контейнеры из правильно настроенной расширения LAD 3.0 на тестовой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="d8e5c-552">Hello изображения не соответствует точно hello [LAD 3.0 пример конфигурации](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="d8e5c-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![изображение](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="d8e5c-554">См. соответствующие hello [EventHubs документации](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn как tooconsume сообщений опубликованные конечной точки EventHubs tooan.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8e5c-555">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8e5c-555">Next steps</span></span>

* <span data-ttu-id="d8e5c-556">Создание метрики оповещений в [монитора Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) для сбора метрик hello.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="d8e5c-557">Создайте [диаграммы мониторинга](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) для метрик.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="d8e5c-558">Узнайте, каким образом слишком[создания набора масштабирования виртуальных машин](/azure/virtual-machines/linux/tutorial-create-vmss) автомасштабирования о toocontrol метрики.</span><span class="sxs-lookup"><span data-stu-id="d8e5c-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
