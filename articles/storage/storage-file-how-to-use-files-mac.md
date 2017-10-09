---
title: "aaaMount Azure общей папки по протоколу SMB на macOS | Документы Microsoft"
description: "Узнайте, как toomount файл Azure предоставить доступ по протоколу SMB macOS."
services: storage
documentationcenter: 
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="19640-103">Подключение общей папки Azure через протокол SMB с помощью macOS</span><span class="sxs-lookup"><span data-stu-id="19640-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="19640-104">[Хранилище Azure файл](storage-dotnet-how-to-use-files.md) службы корпорации Майкрософт, позволяющая toocreate и использование общих сетевых папок hello Azure использует отраслевой стандарт hello.</span><span class="sxs-lookup"><span data-stu-id="19640-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="19640-105">Файловые ресурсы Azure можно подключить в macOS Sierra (10.12) и El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="19640-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="19640-106">В этой статье показано toomount двумя различными способами Azure файловый ресурс на macOS с hello Finder пользовательского интерфейса и с помощью hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="19640-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="19640-107">Перед подключением общей папки Azure через протокол SMB, мы рекомендуем отключить подпись SMB-пакета.</span><span class="sxs-lookup"><span data-stu-id="19640-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="19640-108">Если этого не сделать может привести снижению производительности при обращении к hello Azure общей папки из macOS.</span><span class="sxs-lookup"><span data-stu-id="19640-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="19640-109">Подключение SMB шифруется, поэтому это не влияет на безопасность hello подключения.</span><span class="sxs-lookup"><span data-stu-id="19640-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="19640-110">Из hello терминалов hello следующие команды отключит подписи SMB-пакетов, как описано в данном [статья службы поддержки Apple на отключение подписи SMB-пакетов](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="19640-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="19640-111">Предварительные требования для подключения общей папки Azure в macOS</span><span class="sxs-lookup"><span data-stu-id="19640-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="19640-112">**Имя учетной записи хранения**: toomount Azure общей папки, будет необходимо hello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="19640-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="19640-113">**Ключ учетной записи хранения**: toomount Azure общей папки, будет необходимо hello ключ хранилища первичный (или вторичная).</span><span class="sxs-lookup"><span data-stu-id="19640-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="19640-114">В настоящее время ключи SAS для подключения не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="19640-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="19640-115">**Откройте порт 445**: взаимодействие SMB выполняется через TCP-порт 445.</span><span class="sxs-lookup"><span data-stu-id="19640-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="19640-116">На клиентском компьютере (hello Mac) Проверьте toomake том, что брандмауэр не блокирует порт 445 TCP.</span><span class="sxs-lookup"><span data-stu-id="19640-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="19640-117">Подключение общей папки Azure через систему поиска</span><span class="sxs-lookup"><span data-stu-id="19640-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="19640-118">**Открыть в средстве поиска**: поиска должен быть открыт на macOS по умолчанию, но можно сделать это hello выбранного приложения, щелкнув hello» macOS сталкиваются значок» на закрепление hello:</span><span class="sxs-lookup"><span data-stu-id="19640-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="19640-119">![значок сталкиваются Hello macOS](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="19640-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="19640-120">**Выберите «Подключиться tooServer» из меню «Go» hello**: с помощью UNC-путь hello из hello [необходимые компоненты](#preq), преобразовать две обратные косые черты hello начало (`\\`) слишком`smb://` и все другие символы обратной косой черты (`\`) tooforwards символы косой черты (`/`).</span><span class="sxs-lookup"><span data-stu-id="19640-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="19640-121">Ссылка должна выглядеть hello следующим образом: ![диалоговое окно «Подключиться tooServer» hello](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="19640-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="19640-122">**Используйте hello папки имя и хранения ключ учетной записи при появлении запроса имени пользователя и пароля**: при нажатии кнопки «Подключить» в диалоговом окне «Подключиться tooServer» hello, появится для hello имя пользователя и пароль, (это будет autopopulated с вашей macOS имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="19640-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="19640-123">У вас есть возможность hello размещения ключ учетной записи имя/хранилище общей папки hello в вашей macOS цепочки ключей.</span><span class="sxs-lookup"><span data-stu-id="19640-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="19640-124">**Используйте hello Azure общую папку в случае необходимости**: после замены hello папки имя и хранения ключ учетной записи в hello имени пользователя и пароля, будет подключен hello общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="19640-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="19640-125">Можно использовать это как обычно используются локальной папки или общей папки, включая перетаскивание файлов в общей папке hello:</span><span class="sxs-lookup"><span data-stu-id="19640-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Снимок подключенной общей папки Azure](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="19640-127">Подключение общей папки Azure через терминал</span><span class="sxs-lookup"><span data-stu-id="19640-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="19640-128">Замените `<storage-account-name>` с именем hello вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="19640-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="19640-129">При появлении запроса укажите ключ учетной записи хранения в качестве пароля.</span><span class="sxs-lookup"><span data-stu-id="19640-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="19640-130">**Используйте hello Azure общую папку в случае необходимости**: hello Azure общей папки будет подключен в точке монтирования hello заданные hello предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="19640-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Моментальный снимок hello подключить Azure общей папки](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="19640-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19640-132">Next steps</span></span>
<span data-ttu-id="19640-133">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="19640-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="19640-134">Статья службы поддержки Apple - как tooconnect общий доступ к файлам на компьютере Mac</span><span class="sxs-lookup"><span data-stu-id="19640-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="19640-135">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="19640-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="19640-136">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="19640-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)