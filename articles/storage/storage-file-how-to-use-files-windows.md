---
title: "совместное использование aaaMount Azure файловый ресурс и hello доступа в Windows | Документы Microsoft"
description: "Подключите файлов Azure и общую папку hello доступа в Windows."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="4aba7-103">Подключить файлов Azure и общую папку hello доступа в Windows</span><span class="sxs-lookup"><span data-stu-id="4aba7-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="4aba7-104">[Хранилище Azure файл](storage-dotnet-how-to-use-files.md) корпорации Майкрософт легко toouse облака файловую систему.</span><span class="sxs-lookup"><span data-stu-id="4aba7-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="4aba7-105">Файловые ресурсы Azure можно подключить в Windows и Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4aba7-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="4aba7-106">В этой статье показано три разных способа toomount Azure файловый ресурс в Windows: с hello файл пользовательский Интерфейс через PowerShell, а также через командную строку hello.</span><span class="sxs-lookup"><span data-stu-id="4aba7-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="4aba7-107">В порядке toomount Azure файловый ресурс-вне hello регион Azure, которую она размещается в, например локально или в другом регионе Azure hello операционной системы должен поддерживать SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="4aba7-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="4aba7-108">В зависимости от версии операционной системы общую папку Azure можно подключить локально на компьютере под управлением Windows или на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="4aba7-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="4aba7-109">Приведенной ниже таблице указаны hello</span><span class="sxs-lookup"><span data-stu-id="4aba7-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="4aba7-110">Версия Windows</span><span class="sxs-lookup"><span data-stu-id="4aba7-110">Windows Version</span></span>        | <span data-ttu-id="4aba7-111">Версия SMB</span><span class="sxs-lookup"><span data-stu-id="4aba7-111">SMB Version</span></span> |<span data-ttu-id="4aba7-112">Возможность подключения на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-112">Mountable On Azure VM</span></span>|<span data-ttu-id="4aba7-113">Возможность подключения в локальной среде</span><span class="sxs-lookup"><span data-stu-id="4aba7-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="4aba7-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4aba7-114">Windows 7</span></span>              | <span data-ttu-id="4aba7-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="4aba7-115">SMB 2.1</span></span>     | <span data-ttu-id="4aba7-116">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-116">Yes</span></span>                 | <span data-ttu-id="4aba7-117">Нет</span><span class="sxs-lookup"><span data-stu-id="4aba7-117">No</span></span>                  |
| <span data-ttu-id="4aba7-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4aba7-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="4aba7-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="4aba7-119">SMB 2.1</span></span>     | <span data-ttu-id="4aba7-120">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-120">Yes</span></span>                 | <span data-ttu-id="4aba7-121">Нет</span><span class="sxs-lookup"><span data-stu-id="4aba7-121">No</span></span>                  |
| <span data-ttu-id="4aba7-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="4aba7-122">Windows 8</span></span>              | <span data-ttu-id="4aba7-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="4aba7-123">SMB 3.0</span></span>     | <span data-ttu-id="4aba7-124">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-124">Yes</span></span>                 | <span data-ttu-id="4aba7-125">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-125">Yes</span></span>                 |
| <span data-ttu-id="4aba7-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4aba7-126">Windows Server 2012</span></span>    | <span data-ttu-id="4aba7-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="4aba7-127">SMB 3.0</span></span>     | <span data-ttu-id="4aba7-128">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-128">Yes</span></span>                 | <span data-ttu-id="4aba7-129">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-129">Yes</span></span>                 |
| <span data-ttu-id="4aba7-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4aba7-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="4aba7-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="4aba7-131">SMB 3.0</span></span>     | <span data-ttu-id="4aba7-132">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-132">Yes</span></span>                 | <span data-ttu-id="4aba7-133">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-133">Yes</span></span>                 |
| <span data-ttu-id="4aba7-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4aba7-134">Windows 10</span></span>             | <span data-ttu-id="4aba7-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="4aba7-135">SMB 3.0</span></span>     | <span data-ttu-id="4aba7-136">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-136">Yes</span></span>                 | <span data-ttu-id="4aba7-137">Да</span><span class="sxs-lookup"><span data-stu-id="4aba7-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="4aba7-138">Мы всегда рекомендуем обратиться к самой последней КБ для используемой версии Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4aba7-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="4aba7-139"></a>Предварительные требования для подключения общей папки Azure с помощью Windows</span><span class="sxs-lookup"><span data-stu-id="4aba7-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="4aba7-140">**Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="4aba7-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="4aba7-141">**Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная).</span><span class="sxs-lookup"><span data-stu-id="4aba7-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="4aba7-142">В настоящее время ключи SAS для подключения не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4aba7-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="4aba7-143">**Откройте порт 445**: хранилище файлов Azure использует протокол SMB.</span><span class="sxs-lookup"><span data-stu-id="4aba7-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="4aba7-144">SMB устанавливает соединения через TCP-порт 445 - проверьте toosee, если ваш брандмауэр не блокирует порты TCP 445 с клиентского компьютера.</span><span class="sxs-lookup"><span data-stu-id="4aba7-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="4aba7-145">Подключить hello Azure общей папки с помощью проводника</span><span class="sxs-lookup"><span data-stu-id="4aba7-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="4aba7-146">Обратите внимание, что hello в соответствии с инструкциями, отображаются на Windows 10 и могут немного отличаться в предыдущих версиях.</span><span class="sxs-lookup"><span data-stu-id="4aba7-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="4aba7-147">**Откройте проводник**: это можно сделать путем открытия из меню "Пуск" hello, или нажатием сочетания Win + E.</span><span class="sxs-lookup"><span data-stu-id="4aba7-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="4aba7-148">**Перейдите в элемент «Этот PC» toohello hello левой стороны окна hello. Это приведет к изменению hello меню на ленте «hello». В меню "компьютер" hello, выберите «Подключение сетевого диска»**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Снимок экрана раскрывающегося меню «Подключение сетевого диска» hello](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="4aba7-150">**Копировать hello UNC-путь в hello портал Azure в области «Подключиться» hello**: как toofind эти сведения можно найти подробное описание [здесь](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="4aba7-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![UNC-путь Hello hello Azure хранилища Connect области файла](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="4aba7-152">**Выберите букву диска hello и введите UNC-путь hello.**</span><span class="sxs-lookup"><span data-stu-id="4aba7-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Снимок экрана: диалоговое окно «Подключение сетевого диска» hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="4aba7-154">**Используйте hello имя учетной записи хранилища, но с `Azure\` как имя пользователя hello и ключ учетной записи хранения, как пароль hello.**</span><span class="sxs-lookup"><span data-stu-id="4aba7-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Снимок экрана диалоговое окно приветствия сетевых учетных данных](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="4aba7-156">**Выберите общую папку Azure**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-156">**Use Azure File share as desired**.</span></span>
    
    ![Общая папка Azure теперь подключена](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="4aba7-158">**Когда вы готовы toodismount (или отключить) hello Azure общей папки, это можно сделать, щелкнув hello запись для общей папке hello под hello «сеть» в проводнике правой кнопкой мыши и выбрав пункт «Отключить»**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="4aba7-159">Подключить hello Azure общей папки с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4aba7-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="4aba7-160">**Используйте hello следующая команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` с hello соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="4aba7-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="4aba7-161">**Используйте hello Azure общую папку в случае необходимости**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="4aba7-162">**Когда вы закончите, отключите hello Azure общую hello следующую команду с помощью**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="4aba7-163">Вы можете использовать hello `-Persist` параметр на `New-PSDrive` toomake hello остальные видимым toohello общую папку файлов Azure hello операционной системы во время монтирования.</span><span class="sxs-lookup"><span data-stu-id="4aba7-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="4aba7-164">Подключить hello Azure общей папки с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="4aba7-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="4aba7-165">**Используйте hello следующая команда toomount hello Azure общей папки**: помните tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` с hello соответствующие сведения.</span><span class="sxs-lookup"><span data-stu-id="4aba7-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="4aba7-166">**Используйте hello Azure общую папку в случае необходимости**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="4aba7-167">**Когда вы закончите, отключите hello Azure общую hello следующую команду с помощью**.</span><span class="sxs-lookup"><span data-stu-id="4aba7-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="4aba7-168">Hello переподключение tooautomatically общую папку файлов Azure можно настроить при перезагрузке путем сохранения учетных данных hello в Windows.</span><span class="sxs-lookup"><span data-stu-id="4aba7-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="4aba7-169">Здравствуй, следующая команда будет сохраняться hello учетные данные:</span><span class="sxs-lookup"><span data-stu-id="4aba7-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="4aba7-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4aba7-170">Next steps</span></span>
<span data-ttu-id="4aba7-171">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="4aba7-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="4aba7-172">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="4aba7-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="4aba7-173">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="4aba7-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="4aba7-174">Тематические статьи и видео</span><span class="sxs-lookup"><span data-stu-id="4aba7-174">Conceptual articles and videos</span></span>
* <span data-ttu-id="4aba7-175">[Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Хранилище файлов Azure: удобная облачная файловая система SMB для Windows и Linux)</span><span class="sxs-lookup"><span data-stu-id="4aba7-175">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="4aba7-176">Как toouse хранилища Azure File с Linux</span><span class="sxs-lookup"><span data-stu-id="4aba7-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="4aba7-177">Поддержка средств для работы с хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="4aba7-178">Использование Azure PowerShell со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="4aba7-179">Как toouse AzCopy с хранилищем Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="4aba7-180">С помощью hello Azure CLI со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="4aba7-181">Устранение неполадок хранилища файлов Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="4aba7-182">Записи блога</span><span class="sxs-lookup"><span data-stu-id="4aba7-182">Blog posts</span></span>
* [<span data-ttu-id="4aba7-183">Хранилище файлов Azure стало общедоступным</span><span class="sxs-lookup"><span data-stu-id="4aba7-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* <span data-ttu-id="4aba7-184">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Хранилище файлов Azure: взгляд изнутри)</span><span class="sxs-lookup"><span data-stu-id="4aba7-184">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* [<span data-ttu-id="4aba7-185">Введение в службы файлов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4aba7-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="4aba7-186">Миграция данных tooAzure файла</span><span class="sxs-lookup"><span data-stu-id="4aba7-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="4aba7-187">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="4aba7-187">Reference</span></span>
* [<span data-ttu-id="4aba7-188">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="4aba7-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="4aba7-189">Справочник по REST API службы файлов</span><span class="sxs-lookup"><span data-stu-id="4aba7-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
