---
title: "Сохранение файлов в Azure Cloud Shell (предварительная версия) | Документация Майкрософт"
description: "Пошаговое руководство по сохранению файлов в Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="b0cba-103">Сохранение файлов в Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0cba-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="b0cba-104">Azure Cloud Shell использует преимущества хранилища файлов Azure для сохранения файлов между сеансами.</span><span class="sxs-lookup"><span data-stu-id="b0cba-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="b0cba-105">Настройка файлового ресурса `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0cba-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="b0cba-106">При первом запуске Azure Cloud Shell предлагает привязать новый или существующий файловый ресурс, чтобы сохранять файлы между сеансами.</span><span class="sxs-lookup"><span data-stu-id="b0cba-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="b0cba-107">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="b0cba-107">Create new storage</span></span>

<span data-ttu-id="b0cba-108">Если вы используете базовые параметры и выбрали только подписку, Cloud Shell создаст три ресурса от вашего имени в поддерживаемом регионе, находящемся ближе всего к вам:</span><span class="sxs-lookup"><span data-stu-id="b0cba-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="b0cba-109">группу ресурсов `cloud-shell-storage-<region>`;</span><span class="sxs-lookup"><span data-stu-id="b0cba-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="b0cba-110">учетную запись хранения `cs<uniqueGuid>`;</span><span class="sxs-lookup"><span data-stu-id="b0cba-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="b0cba-111">файловый ресурс `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Настройка подписки](media/basic-storage.png)

<span data-ttu-id="b0cba-113">Файловый ресурс подключается как `clouddrive` в вашем каталоге `$Home`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="b0cba-114">Он используется для хранения созданного образа размером 5 ГБ, который автоматически обновляет и сохраняет данные в каталоге `$Home`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="b0cba-115">Подключение выполняется один раз, и для последующих сеансов файловый ресурс подключается автоматически.</span><span class="sxs-lookup"><span data-stu-id="b0cba-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="b0cba-116">Использование существующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="b0cba-116">Use existing resources</span></span>

<span data-ttu-id="b0cba-117">С помощью расширенных параметров можно привязать существующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b0cba-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="b0cba-118">Когда появится запрос на настройку хранилища, щелкните **Показать дополнительные настройки**, чтобы просмотреть дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="b0cba-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="b0cba-119">Существующие файловые ресурсы получают образ размером 5 ГБ для сохранения каталога `$Home`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="b0cba-120">Раскрывающиеся меню фильтруются с учетом региона Cloud Shell и учетных записей локально избыточного и геоизбыточного хранилищ.</span><span class="sxs-lookup"><span data-stu-id="b0cba-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![Настройка группы ресурсов](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="b0cba-122">Ограничение создания ресурсов с помощью политик ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="b0cba-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="b0cba-123">Учетные записи хранения, создаваемые в Cloud Shell, помечаются тегом `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="b0cba-124">Если вы хотите запретить пользователям создавать учетные записи хранения в Cloud Shell, создайте [политику ресурсов Azure на основе тегов](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) для этого конкретного тега.</span><span class="sxs-lookup"><span data-stu-id="b0cba-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="b0cba-125">Как работает Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0cba-125">How Cloud Shell works</span></span>
<span data-ttu-id="b0cba-126">Cloud Shell сохраняет файлы с помощью обоих приведенных ниже методов.</span><span class="sxs-lookup"><span data-stu-id="b0cba-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="b0cba-127">Создание образа диска для каталога `$Home` для хранения всего содержимого этого каталога.</span><span class="sxs-lookup"><span data-stu-id="b0cba-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="b0cba-128">Этот образ диска сохраняется как `acc_<User>.img` в `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, и для него выполняется автоматическая синхронизация изменений.</span><span class="sxs-lookup"><span data-stu-id="b0cba-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="b0cba-129">Подключение выбранного файлового ресурса как `clouddrive` в каталоге `$Home`. Это позволяет взаимодействовать с ним напрямую.</span><span class="sxs-lookup"><span data-stu-id="b0cba-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="b0cba-130">`/Home/<User>/clouddrive` сопоставляется с `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="b0cba-131">Все файлы в каталоге `$Home`, такие как ключи SSH, сохраняются в образе диска пользователя, который хранится в подключенном файловом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="b0cba-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="b0cba-132">Соблюдайте рекомендации при сохранении информации в каталоге `$Home` и подключенном файловом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="b0cba-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="b0cba-133">Использование команды `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0cba-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="b0cba-134">В Cloud Shell можно выполнить команду `clouddrive`, что позволит вручную обновить файловый ресурс, подключенный к Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="b0cba-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="b0cba-135">![Выполнение команды clouddrive](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="b0cba-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="b0cba-136">Подключение нового `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0cba-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="b0cba-137">Предварительные требования для подключения вручную</span><span class="sxs-lookup"><span data-stu-id="b0cba-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="b0cba-138">Можно обновить файловый ресурс, который связан с Cloud Shell, с помощью команды `clouddrive mount`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="b0cba-139">При подключении имеющегося файлового ресурса учетные записи хранения должны:</span><span class="sxs-lookup"><span data-stu-id="b0cba-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="b0cba-140">Относиться к локально избыточному или геоизбыточному хранилищу, чтобы обеспечить поддержку файловых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0cba-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="b0cba-141">Находиться в назначенном вам регионе.</span><span class="sxs-lookup"><span data-stu-id="b0cba-141">Located in your assigned region.</span></span> <span data-ttu-id="b0cba-142">При подключении назначенный вам регион указывается в имени группы ресурсов `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="b0cba-143">Поддерживаемые регионы хранилища</span><span class="sxs-lookup"><span data-stu-id="b0cba-143">Supported storage regions</span></span>
<span data-ttu-id="b0cba-144">Файлы Azure должны находиться в том же регионе, что и компьютер Cloud Shell, к которому вы их подключаете.</span><span class="sxs-lookup"><span data-stu-id="b0cba-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="b0cba-145">Кластеры Cloud Shell находятся в следующих регионах:</span><span class="sxs-lookup"><span data-stu-id="b0cba-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="b0cba-146">Область</span><span class="sxs-lookup"><span data-stu-id="b0cba-146">Area</span></span>|<span data-ttu-id="b0cba-147">Регион</span><span class="sxs-lookup"><span data-stu-id="b0cba-147">Region</span></span>|
|---|---|
|<span data-ttu-id="b0cba-148">Северная и Южная Америка</span><span class="sxs-lookup"><span data-stu-id="b0cba-148">Americas</span></span>|<span data-ttu-id="b0cba-149">Восточная часть США, юго-центральный регион США, западная часть США</span><span class="sxs-lookup"><span data-stu-id="b0cba-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="b0cba-150">Европа</span><span class="sxs-lookup"><span data-stu-id="b0cba-150">Europe</span></span>|<span data-ttu-id="b0cba-151">Северная Европа, Западная Европа</span><span class="sxs-lookup"><span data-stu-id="b0cba-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="b0cba-152">Азиатско-Тихоокеанский регион</span><span class="sxs-lookup"><span data-stu-id="b0cba-152">Asia Pacific</span></span>|<span data-ttu-id="b0cba-153">Центральная Индия, Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="b0cba-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="b0cba-154">Команда `clouddrive mount`</span><span class="sxs-lookup"><span data-stu-id="b0cba-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="b0cba-155">При подключении нового файлового ресурса будет создан новый пользовательский образ для каталога `$Home`, так как предыдущий образ `$Home` хранится в предыдущем файловом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="b0cba-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="b0cba-156">Выполните команду `clouddrive mount` со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="b0cba-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="b0cba-157">Чтобы просмотреть дополнительные сведения, выполните `clouddrive mount -h`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b0cba-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Выполнение команды clouddrive mount](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="b0cba-159">Отключение `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0cba-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="b0cba-160">Файловый ресурс, подключенный к Cloud Shell, можно отключить в любое время.</span><span class="sxs-lookup"><span data-stu-id="b0cba-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="b0cba-161">После отключения файлового ресурса вам будет предложено подключить новый файловый ресурс до следующего сеанса.</span><span class="sxs-lookup"><span data-stu-id="b0cba-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="b0cba-162">Чтобы удалить общую папку из Cloud Shell, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b0cba-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="b0cba-163">Запустите `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="b0cba-164">Подтвердите запросы.</span><span class="sxs-lookup"><span data-stu-id="b0cba-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="b0cba-165">Файловый ресурс будет существовать до его удаления вручную.</span><span class="sxs-lookup"><span data-stu-id="b0cba-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="b0cba-166">Cloud Shell больше не будет искать эту общую папку для последующих сеансов.</span><span class="sxs-lookup"><span data-stu-id="b0cba-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="b0cba-167">Чтобы просмотреть дополнительные сведения, выполните `clouddrive unmount -h`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b0cba-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Выполнение команды clouddrive unmount](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="b0cba-169">При выполнении этой команды ресурсы не удаляются.</span><span class="sxs-lookup"><span data-stu-id="b0cba-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="b0cba-170">Однако в результате ручного удаления группы ресурсов, учетной записи хранения или общего файлового ресурса, сопоставленных с Cloud Shell, каталог образов `$Home` и другие файлы в общем файловом ресурсе будут безвозвратно удалены.</span><span class="sxs-lookup"><span data-stu-id="b0cba-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="b0cba-171">Это действие невозможно отменить.</span><span class="sxs-lookup"><span data-stu-id="b0cba-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="b0cba-172">Вывод списка файловых ресурсов `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0cba-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="b0cba-173">Чтобы узнать, какой файловый ресурс подключается как `clouddrive`, выполните приведенную ниже команду `df`.</span><span class="sxs-lookup"><span data-stu-id="b0cba-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="b0cba-174">В пути к каталогу clouddrive указано имя учетной записи хранения и файловый ресурс в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="b0cba-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="b0cba-175">Например, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="b0cba-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="b0cba-176">Передача локальных файлов в Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0cba-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="b0cba-177">Каталог `clouddrive` синхронизируется c колонкой хранилища на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b0cba-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="b0cba-178">Используйте эту колонку для перемещения локальных файлов в файловый ресурс и из него.</span><span class="sxs-lookup"><span data-stu-id="b0cba-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="b0cba-179">Обновленные файлы в Cloud Shell отобразятся в графическом пользовательском интерфейсе хранилища файлов после обновления колонки.</span><span class="sxs-lookup"><span data-stu-id="b0cba-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="b0cba-180">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="b0cba-180">Download files</span></span>

![Вывод списка локальных файлов](media/download.png)
1. <span data-ttu-id="b0cba-182">На портале Azure перейдите к подключенному файловому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="b0cba-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="b0cba-183">Выберите целевой файл.</span><span class="sxs-lookup"><span data-stu-id="b0cba-183">Select the target file.</span></span>
3. <span data-ttu-id="b0cba-184">Нажмите кнопку **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="b0cba-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="b0cba-185">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="b0cba-185">Upload files</span></span>

![Локальные файлы для передачи](media/upload.png)
1. <span data-ttu-id="b0cba-187">Перейдите к подключенному файловому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="b0cba-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="b0cba-188">Нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="b0cba-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="b0cba-189">Выберите файл или файлы, которые необходимо передать.</span><span class="sxs-lookup"><span data-stu-id="b0cba-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="b0cba-190">Подтвердите передачу.</span><span class="sxs-lookup"><span data-stu-id="b0cba-190">Confirm the upload.</span></span>

<span data-ttu-id="b0cba-191">Теперь эти файлы должны появиться в каталоге `clouddrive` в Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="b0cba-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0cba-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0cba-192">Next steps</span></span>
[<span data-ttu-id="b0cba-193">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0cba-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="b0cba-194">
[Хранилище файлов](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="b0cba-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="b0cba-195">
[Использование тегов для организации ресурсов в Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="b0cba-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
