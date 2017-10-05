---
title: "Как управлять хранилищем файлов Azure на портале Azure | Документация Майкрософт"
description: "Узнайте, как использовать портал Azure для управления хранилищем файлов Azure."
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
ms.openlocfilehash: d5ffa7cff0a31e36f5a96aaa4b2d477fa39333fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="b2a41-103">Как использовать хранилище файлов Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b2a41-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="b2a41-104">[Портал Azure](https://portal.azure.com) предоставляет пользовательский интерфейс для управления хранилищем файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a41-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="b2a41-105">Следующие действия можно выполнять в браузере:</span><span class="sxs-lookup"><span data-stu-id="b2a41-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="b2a41-106">Создание файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="b2a41-106">Create a File Share</span></span>
* <span data-ttu-id="b2a41-107">передавать файлы в общую папку и скачивать файлы из нее;</span><span class="sxs-lookup"><span data-stu-id="b2a41-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="b2a41-108">отслеживать фактическое использование каждой общей папки;</span><span class="sxs-lookup"><span data-stu-id="b2a41-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="b2a41-109">изменять квоты на размер общей папки;</span><span class="sxs-lookup"><span data-stu-id="b2a41-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="b2a41-110">копировать команду mount, которая позволит подключить общую папку с клиентского компьютера с Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="b2a41-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="b2a41-111">Создание общей папки</span><span class="sxs-lookup"><span data-stu-id="b2a41-111">Create file share</span></span>
1. <span data-ttu-id="b2a41-112">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a41-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="b2a41-113">В меню навигации щелкните **Учетные записи хранения** или **Учетные записи хранения (классика)**.</span><span class="sxs-lookup"><span data-stu-id="b2a41-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Снимок экрана, показывающий, как создать общую папку на портале](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="b2a41-115">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b2a41-115">Choose your storage account.</span></span>

    ![Снимок экрана, показывающий, как создать общую папку на портале](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="b2a41-117">Выберите службу "Файлы".</span><span class="sxs-lookup"><span data-stu-id="b2a41-117">Choose "Files" service.</span></span>

    ![Снимок экрана, показывающий, как создать общую папку на портале](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="b2a41-119">Щелкните "Общие папки" и перейдите по ссылке для создания первой общей папки.</span><span class="sxs-lookup"><span data-stu-id="b2a41-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Снимок экрана, показывающий, как создать общую папку на портале](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="b2a41-121">Чтобы завершить создание своей первой общей папки, укажите ее имя и размер (до 5120 ГБ).</span><span class="sxs-lookup"><span data-stu-id="b2a41-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="b2a41-122">После создания общей папки необходимо подключить ее из любой файловой системы, поддерживающей SMB 2.1 или SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="b2a41-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="b2a41-123">Вы можете щелкнуть **Квота** в общей папке, чтобы изменить размер файла до 5120 ГБ.</span><span class="sxs-lookup"><span data-stu-id="b2a41-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="b2a41-124">Используйте [калькулятор цен](https://azure.microsoft.com/pricing/calculator/), чтобы узнать стоимость использования хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a41-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Снимок экрана, показывающий, как создать общую папку на портале](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="b2a41-126">Отправка и загрузка файлов</span><span class="sxs-lookup"><span data-stu-id="b2a41-126">Upload and download files</span></span>
1. <span data-ttu-id="b2a41-127">Выберите ранее созданную общую папку.</span><span class="sxs-lookup"><span data-stu-id="b2a41-127">Choose one file share your have already created.</span></span>

    ![Снимок экрана, показывающий, как отправлять и скачивать файлы с помощью портала](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="b2a41-129">Щелкните **Загрузить** , чтобы открыть пользовательский интерфейс для отправки файлов.</span><span class="sxs-lookup"><span data-stu-id="b2a41-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Снимок экрана, показывающий, как отправлять файлы с помощью портала](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="b2a41-131">Подключение к общей папке</span><span class="sxs-lookup"><span data-stu-id="b2a41-131">Connect to file share</span></span>
-  <span data-ttu-id="b2a41-132">Щелкните **Подключить**, чтобы вызвать командную строку для подключения общей папки из Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="b2a41-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="b2a41-133">Дополнительные сведения о подключении для других дистрибутивов Linux см. в статье [Использование хранилища файлов Azure в Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b2a41-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Снимок экрана, показывающий, как подключить общую папку](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="b2a41-135">Вы можете скопировать команды для подключения общей папки в Windows или Linux, а также запустить их из виртуальной машины Azure или локально.</span><span class="sxs-lookup"><span data-stu-id="b2a41-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Снимок экрана, показывающий команды подключения для Windows и Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="b2a41-137">**Подсказка.**</span><span class="sxs-lookup"><span data-stu-id="b2a41-137">**Tip:**</span></span>  
<span data-ttu-id="b2a41-138">Чтобы получить ключ доступа учетной записи хранения для подключения, щелкните ссылку **View access keys for this storage account** (Просмотр ключей доступа для этой учетной записи хранения) в нижней области страницы подключения.</span><span class="sxs-lookup"><span data-stu-id="b2a41-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="b2a41-139">См. также</span><span class="sxs-lookup"><span data-stu-id="b2a41-139">See also</span></span>
<span data-ttu-id="b2a41-140">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="b2a41-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="b2a41-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="b2a41-141">FAQ</span></span>](../storage-files-faq.md)
* <span data-ttu-id="b2a41-142">[Troubleshoot Azure File storage problems in Windows](storage-troubleshoot-windows-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Windows)</span><span class="sxs-lookup"><span data-stu-id="b2a41-142">[Troubleshooting on Windows](storage-troubleshoot-windows-file-connection-problems.md)</span></span>      
* <span data-ttu-id="b2a41-143">[Troubleshoot Azure File storage problems in Linux](storage-troubleshoot-linux-file-connection-problems.md) (Устранение неполадок хранилища файлов Azure в Linux)</span><span class="sxs-lookup"><span data-stu-id="b2a41-143">[Troubleshooting on Linux](storage-troubleshoot-linux-file-connection-problems.md)</span></span>    