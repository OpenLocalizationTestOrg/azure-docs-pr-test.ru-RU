---
title: "файлы aaaPersist в оболочке облако Azure (Предварительная версия) | Документы Microsoft"
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
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="327fc-103">Сохранение файлов в Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="327fc-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="327fc-104">Оболочки облака использует файлы toopersist хранилища Azure файл во всех сеансах.</span><span class="sxs-lookup"><span data-stu-id="327fc-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="327fc-105">Настройка файлового ресурса `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="327fc-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="327fc-106">Для первоначального запуска оболочки облака предлагает tooassociate нового или существующего файла совместно использовать файлы toopersist между сеансами.</span><span class="sxs-lookup"><span data-stu-id="327fc-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="327fc-107">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="327fc-107">Create new storage</span></span>

<span data-ttu-id="327fc-108">При использовании основные параметры и выберите только подписки, облака оболочки создаются три ресурсы от вашего имени в регионе hello поддерживается ближайшем tooyou:</span><span class="sxs-lookup"><span data-stu-id="327fc-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="327fc-109">группу ресурсов `cloud-shell-storage-<region>`;</span><span class="sxs-lookup"><span data-stu-id="327fc-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="327fc-110">учетную запись хранения `cs<uniqueGuid>`;</span><span class="sxs-lookup"><span data-stu-id="327fc-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="327fc-111">файловый ресурс `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="327fc-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Подписка приветствия](media/basic-storage.png)

<span data-ttu-id="327fc-113">Подключает Hello общей папки как `clouddrive` в ваш `$Home` каталога.</span><span class="sxs-lookup"><span data-stu-id="327fc-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="327fc-114">Hello общая папка является также используется toostore образ размером 5 ГБ, который создается для вас и который автоматически обновляет и сохраняет вашей `$Home` каталога.</span><span class="sxs-lookup"><span data-stu-id="327fc-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="327fc-115">Это однократное действие, и автоматически подключает hello общей папки в последующих сеансах.</span><span class="sxs-lookup"><span data-stu-id="327fc-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="327fc-116">Использование существующих ресурсов</span><span class="sxs-lookup"><span data-stu-id="327fc-116">Use existing resources</span></span>

<span data-ttu-id="327fc-117">С помощью hello дополнительный параметр, можно связать существующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="327fc-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="327fc-118">При появлении подсказки при установке хранилища hello выберите **Показывать дополнительные параметры** tooview Дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="327fc-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="327fc-119">Существующие общие папки приема toopersist изображения размером 5 ГБ пользователя вашего `$Home` каталога.</span><span class="sxs-lookup"><span data-stu-id="327fc-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="327fc-120">отфильтрованные Hello раскрывающиеся меню для своего региона оболочки облачной и локальной избыточности & географически избыточное хранилище учетных записей.</span><span class="sxs-lookup"><span data-stu-id="327fc-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![параметр группы ресурсов Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="327fc-122">Ограничение создания ресурсов с помощью политик ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="327fc-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="327fc-123">Учетные записи хранения, создаваемые в Cloud Shell, помечаются тегом `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="327fc-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="327fc-124">Toodisallow пользователям возможность создавать учетные записи хранения в облаке оболочки создать [политики ресурсов Azure для тегов](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) , активируемых этого конкретного тега.</span><span class="sxs-lookup"><span data-stu-id="327fc-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="327fc-125">Как работает Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="327fc-125">How Cloud Shell works</span></span>
<span data-ttu-id="327fc-126">Облако оболочки сохранится файлов с помощью обоих hello следующие методы:</span><span class="sxs-lookup"><span data-stu-id="327fc-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="327fc-127">Создание образа диска вашей `$Home` toopersist каталога все содержимое в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="327fc-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="327fc-128">образ диска Hello сохраняется в папке указанный файл как `acc_<User>.img` в `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, и он автоматически синхронизирует изменения.</span><span class="sxs-lookup"><span data-stu-id="327fc-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="327fc-129">Подключение выбранного файлового ресурса как `clouddrive` в каталоге `$Home`. Это позволяет взаимодействовать с ним напрямую.</span><span class="sxs-lookup"><span data-stu-id="327fc-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="327fc-130">`/Home/<User>/clouddrive`сопоставляется слишком`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="327fc-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="327fc-131">Все файлы в каталоге `$Home`, такие как ключи SSH, сохраняются в образе диска пользователя, который хранится в подключенном файловом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="327fc-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="327fc-132">Соблюдайте рекомендации при сохранении информации в каталоге `$Home` и подключенном файловом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="327fc-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="327fc-133">Используйте hello `clouddrive` команды</span><span class="sxs-lookup"><span data-stu-id="327fc-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="327fc-134">С оболочкой облака, можно выполнить команду, вызывается `clouddrive`, который позволяет вам toomanually обновления hello общей папки с подключенного tooCloud оболочки.</span><span class="sxs-lookup"><span data-stu-id="327fc-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="327fc-135">![Выполнив команду «clouddrive» hello](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="327fc-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="327fc-136">Подключение нового `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="327fc-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="327fc-137">Предварительные требования для подключения вручную</span><span class="sxs-lookup"><span data-stu-id="327fc-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="327fc-138">Вы можете обновить hello общий файловый ресурс, связанный с облачной оболочки с помощью hello `clouddrive mount` команды.</span><span class="sxs-lookup"><span data-stu-id="327fc-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="327fc-139">Если подключить существующий файловый ресурс, необходимо hello учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="327fc-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="327fc-140">Локально избыточное хранилище или геоизбыточное хранилище toosupport общих папок.</span><span class="sxs-lookup"><span data-stu-id="327fc-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="327fc-141">Находиться в назначенном вам регионе.</span><span class="sxs-lookup"><span data-stu-id="327fc-141">Located in your assigned region.</span></span> <span data-ttu-id="327fc-142">При адаптации hello регион назначения toois, перечисленные в имя группы ресурсов hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="327fc-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="327fc-143">Поддерживаемые регионы хранилища</span><span class="sxs-lookup"><span data-stu-id="327fc-143">Supported storage regions</span></span>
<span data-ttu-id="327fc-144">Hello Azure файлы должны находиться в hello же регионе, что машина оболочки облака hello, подключение их.</span><span class="sxs-lookup"><span data-stu-id="327fc-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="327fc-145">Кластеры оболочки облака в настоящее время существует в hello следующие области:</span><span class="sxs-lookup"><span data-stu-id="327fc-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="327fc-146">Область</span><span class="sxs-lookup"><span data-stu-id="327fc-146">Area</span></span>|<span data-ttu-id="327fc-147">Регион</span><span class="sxs-lookup"><span data-stu-id="327fc-147">Region</span></span>|
|---|---|
|<span data-ttu-id="327fc-148">Северная и Южная Америка</span><span class="sxs-lookup"><span data-stu-id="327fc-148">Americas</span></span>|<span data-ttu-id="327fc-149">Восточная часть США, юго-центральный регион США, западная часть США</span><span class="sxs-lookup"><span data-stu-id="327fc-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="327fc-150">Европа</span><span class="sxs-lookup"><span data-stu-id="327fc-150">Europe</span></span>|<span data-ttu-id="327fc-151">Северная Европа, Западная Европа</span><span class="sxs-lookup"><span data-stu-id="327fc-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="327fc-152">Азиатско-Тихоокеанский регион</span><span class="sxs-lookup"><span data-stu-id="327fc-152">Asia Pacific</span></span>|<span data-ttu-id="327fc-153">Центральная Индия, Юго-Восточная Азия</span><span class="sxs-lookup"><span data-stu-id="327fc-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="327fc-154">Hello `clouddrive mount` команды</span><span class="sxs-lookup"><span data-stu-id="327fc-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="327fc-155">Если подключение новую общую папку, создается новый пользовательский образ вашей `$Home` каталог, из-за предыдущих `$Home` изображение сохраняется в hello предыдущих общей папки.</span><span class="sxs-lookup"><span data-stu-id="327fc-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="327fc-156">Запустите hello `clouddrive mount` с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="327fc-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="327fc-157">tooview сведения, запустите `clouddrive mount -h`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="327fc-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Выполнение hello "clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="327fc-159">Отключение `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="327fc-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="327fc-160">Можно отключить общий файловый ресурс с подключенного tooCloud оболочки в любое время.</span><span class="sxs-lookup"><span data-stu-id="327fc-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="327fc-161">После файлового ресурса отключены, вы сможете запрашиваемые toomount новый tooyour предыдущего общую папку файл следующего сеанса.</span><span class="sxs-lookup"><span data-stu-id="327fc-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="327fc-162">tooremove файл для общей папки из облака оболочки:</span><span class="sxs-lookup"><span data-stu-id="327fc-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="327fc-163">Запустите `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="327fc-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="327fc-164">Подтверждаю и подтвердите hello приглашения.</span><span class="sxs-lookup"><span data-stu-id="327fc-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="327fc-165">Файлового ресурса по-прежнему tooexist пока не будут удалены вручную.</span><span class="sxs-lookup"><span data-stu-id="327fc-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="327fc-166">Cloud Shell больше не будет искать эту общую папку для последующих сеансов.</span><span class="sxs-lookup"><span data-stu-id="327fc-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="327fc-167">tooview сведения, запустите `clouddrive unmount -h`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="327fc-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Выполнение hello "clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="327fc-169">При выполнении этой команды ресурсы не удаляются.</span><span class="sxs-lookup"><span data-stu-id="327fc-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="327fc-170">Вручную удалить группу ресурсов, учетной записи хранилища или общую папку, сопоставленный tooCloud оболочки приведет к окончательному удалению вашей `$Home` directory изображения и другие файлы в папке файла.</span><span class="sxs-lookup"><span data-stu-id="327fc-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="327fc-171">Это действие невозможно отменить.</span><span class="sxs-lookup"><span data-stu-id="327fc-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="327fc-172">Вывод списка файловых ресурсов `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="327fc-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="327fc-173">какие общей папки подключается как toodiscover `clouddrive`, hello следующей `df` команды.</span><span class="sxs-lookup"><span data-stu-id="327fc-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="327fc-174">tooclouddrive путь файла Hello показывает, что имя учетной записи хранилища и файл общей папки в URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="327fc-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="327fc-175">Например, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="327fc-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="327fc-176">Перенос локальных файлов tooCloud оболочки</span><span class="sxs-lookup"><span data-stu-id="327fc-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="327fc-177">Hello `clouddrive` синхронизации каталогов с колонке hello портала хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="327fc-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="327fc-178">Используйте локальные файлы tooor с tootransfer этой колонке из файлового ресурса.</span><span class="sxs-lookup"><span data-stu-id="327fc-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="327fc-179">Обновление файлов из облака оболочки отражается в хранилище файлов hello графического пользовательского интерфейса при обновлении колонки hello.</span><span class="sxs-lookup"><span data-stu-id="327fc-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="327fc-180">Скачивание файлов</span><span class="sxs-lookup"><span data-stu-id="327fc-180">Download files</span></span>

![Вывод списка локальных файлов](media/download.png)
1. <span data-ttu-id="327fc-182">В hello портал Azure перейдите toohello подключенного общей папки.</span><span class="sxs-lookup"><span data-stu-id="327fc-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="327fc-183">Выберите целевой файл hello.</span><span class="sxs-lookup"><span data-stu-id="327fc-183">Select hello target file.</span></span>
3. <span data-ttu-id="327fc-184">Выберите hello **загрузки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="327fc-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="327fc-185">Отправка файлов</span><span class="sxs-lookup"><span data-stu-id="327fc-185">Upload files</span></span>

![Отправить toobe локальные файлы](media/upload.png)
1. <span data-ttu-id="327fc-187">Последовательно выберите tooyour подключить общую папку.</span><span class="sxs-lookup"><span data-stu-id="327fc-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="327fc-188">Выберите hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="327fc-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="327fc-189">Выберите файл hello или файлы, которые должны tooupload.</span><span class="sxs-lookup"><span data-stu-id="327fc-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="327fc-190">Подтверждение отправки hello.</span><span class="sxs-lookup"><span data-stu-id="327fc-190">Confirm hello upload.</span></span>

<span data-ttu-id="327fc-191">Теперь вы увидите hello файлы, доступные в вашей `clouddrive` каталог в облаке оболочки.</span><span class="sxs-lookup"><span data-stu-id="327fc-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="327fc-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="327fc-192">Next steps</span></span>
[<span data-ttu-id="327fc-193">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="327fc-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="327fc-194">
[Хранилище файлов](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="327fc-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="327fc-195">
[Использование тегов для организации ресурсов в Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="327fc-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
