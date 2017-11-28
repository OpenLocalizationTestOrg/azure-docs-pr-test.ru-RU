---
title: "Подключение общей папки Azure через протокол SMB с помощью macOS | Документация Майкрософт"
description: "Узнайте, как подключить общую папку Azure через протокол SMB с помощью macOS."
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
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="af887-103">Подключение общей папки Azure через протокол SMB с помощью macOS</span><span class="sxs-lookup"><span data-stu-id="af887-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="af887-104">[Хранилище файлов Azure](storage-dotnet-how-to-use-files.md) — это служба Майкрософт, которая позволяет создавать и использовать сетевые файловые ресурсы в Azure, применяя отраслевой стандарт.</span><span class="sxs-lookup"><span data-stu-id="af887-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="af887-105">Файловые ресурсы Azure можно подключить в macOS Sierra (10.12) и El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="af887-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="af887-106">В этой статье описываются два разных способа подключения общей папки Azure в macOS: с помощью пользовательского интерфейса поиска и терминала.</span><span class="sxs-lookup"><span data-stu-id="af887-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="af887-107">Перед подключением общей папки Azure через протокол SMB, мы рекомендуем отключить подпись SMB-пакета.</span><span class="sxs-lookup"><span data-stu-id="af887-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="af887-108">Если этого не сделать, это может вызвать снижение производительности при получении доступа к общей папке Azure из macOS.</span><span class="sxs-lookup"><span data-stu-id="af887-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="af887-109">Ваше подключение SMB будет зашифровано, поэтому на безопасность подключения это не повлияет.</span><span class="sxs-lookup"><span data-stu-id="af887-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="af887-110">Выполнив следующие команды из терминала, вы отключите подпись SMB-пакетов, как описано на странице об [отключении подписи пакета для подключений протоколов SMB 2 и SMB 3](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="af887-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="af887-111">Предварительные требования для подключения общей папки Azure в macOS</span><span class="sxs-lookup"><span data-stu-id="af887-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="af887-112">**Имя учетной записи хранения**: чтобы подключить общую папку Azure, вам потребуется имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="af887-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="af887-113">**Ключ учетной записи хранения**: чтобы подключить общую папку Azure, вам потребуется первичный (или вторичный) ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="af887-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="af887-114">В настоящее время ключи SAS для подключения не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="af887-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="af887-115">**Откройте порт 445**: взаимодействие SMB выполняется через TCP-порт 445.</span><span class="sxs-lookup"><span data-stu-id="af887-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="af887-116">Проверьте, чтобы брандмауэр не блокировал TCP-порт 445 с клиентского компьютера (Mac).</span><span class="sxs-lookup"><span data-stu-id="af887-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="af887-117">Подключение общей папки Azure через систему поиска</span><span class="sxs-lookup"><span data-stu-id="af887-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="af887-118">**Откройте систему поиска**: она открыта в macOS по умолчанию, но вы можете открыть ее для текущего выбранного приложения. Щелкните значок распознавания лиц macOS на панели закрепления:</span><span class="sxs-lookup"><span data-stu-id="af887-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="af887-119">![Значок распознавания лиц macOS](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="af887-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="af887-120">**Выберите "Подключение к серверу" в меню "Перейти"**: использование UNC-пути, описанного в [предварительных требованиях](#preq), преобразует первую двойную обратную косую черту (`\\`) в `smb://`, а также все другие обратные косые черты (`\`) в косые черты с направлением вправо (`/`).</span><span class="sxs-lookup"><span data-stu-id="af887-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="af887-121">Ссылка должна выглядеть следующим образом: ![диалоговое окно "Подключение к серверу"](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="af887-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="af887-122">**Используйте имя общей папки и ключ учетной записи хранения при появлении запроса имени пользователя и пароля**: когда вы щелкнете "Подключиться" в диалоговом окне "Подключение к серверу", вы получите запрос имени пользователя и пароля (значения будут заполнены автоматически именем пользователя macOS).</span><span class="sxs-lookup"><span data-stu-id="af887-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="af887-123">Вы также можете разместить ключ учетной записи хранения и имя общей папки в цепочке ключей macOS.</span><span class="sxs-lookup"><span data-stu-id="af887-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="af887-124">**Выберите общую папку Azure**: после замены имени общей папки, а также ключа учетной записи хранения именем пользователя и паролем, общая папка будет подключена.</span><span class="sxs-lookup"><span data-stu-id="af887-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="af887-125">Вы можете использовать ее обычным образом, как вы обычно использовали локальные файловые ресурсы, а также можете перетаскивать в нее файлы и удалять их:</span><span class="sxs-lookup"><span data-stu-id="af887-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Снимок подключенной общей папки Azure](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="af887-127">Подключение общей папки Azure через терминал</span><span class="sxs-lookup"><span data-stu-id="af887-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="af887-128">Замените `<storage-account-name>` именем своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="af887-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="af887-129">При появлении запроса укажите ключ учетной записи хранения в качестве пароля.</span><span class="sxs-lookup"><span data-stu-id="af887-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="af887-130">**Выберите общую папку Azure**: общая папка Azure будет подключена в точке подключения, указанной предыдущей командой.</span><span class="sxs-lookup"><span data-stu-id="af887-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Моментальный снимок подключенной общей папки Azure](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="af887-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af887-132">Next steps</span></span>
<span data-ttu-id="af887-133">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="af887-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="af887-134">Использование функции общего доступа к файлам на компьютере Mac</span><span class="sxs-lookup"><span data-stu-id="af887-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="af887-135">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="af887-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="af887-136">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="af887-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)