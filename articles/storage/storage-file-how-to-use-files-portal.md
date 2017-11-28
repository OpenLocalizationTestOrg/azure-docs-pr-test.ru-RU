---
title: "aaaHow toomanage хранилища Azure File с hello портал Azure | Документы Microsoft"
description: "Узнайте хранилища Azure File toouse hello Azure toomanage портала."
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
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="658f6-103">Как toouse хранилища Azure File с hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="658f6-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="658f6-104">Hello [портал Azure](https://portal.azure.com) предоставляет пользовательский интерфейс для управления хранилищем файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="658f6-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="658f6-105">Вы можете выполнять hello, выполнив действия из веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="658f6-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="658f6-106">Создание файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="658f6-106">Create a File Share</span></span>
* <span data-ttu-id="658f6-107">Отправка и загрузка файлов tooand из файлового ресурса.</span><span class="sxs-lookup"><span data-stu-id="658f6-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="658f6-108">Наблюдение за hello фактического потребления ресурсов для каждой общей папки.</span><span class="sxs-lookup"><span data-stu-id="658f6-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="658f6-109">Измените размер квоты для hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="658f6-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="658f6-110">Скопируйте hello команды mount toouse toomount вашей общей папки из клиента Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="658f6-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="658f6-111">Создание общей папки</span><span class="sxs-lookup"><span data-stu-id="658f6-111">Create file share</span></span>
1. <span data-ttu-id="658f6-112">Войдите в систему toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="658f6-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="658f6-113">Hello навигации в меню **учетные записи хранения** или **учетные записи хранения (классические)**.</span><span class="sxs-lookup"><span data-stu-id="658f6-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="658f6-115">Выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="658f6-115">Choose your storage account.</span></span>

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="658f6-117">Выберите службу "Файлы".</span><span class="sxs-lookup"><span data-stu-id="658f6-117">Choose "Files" service.</span></span>

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="658f6-119">Выберите «Общие папки» и следуйте hello toocreate связи, совместно использовать первый файл.</span><span class="sxs-lookup"><span data-stu-id="658f6-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="658f6-121">Введите имя общей папки hello и hello размер общей папки (вверх ГБ too5120) toocreate hello файл первый файлового ресурса.</span><span class="sxs-lookup"><span data-stu-id="658f6-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="658f6-122">После создания общей папки hello можно подключить ее из какой файловой системы, который поддерживает SMB 2.1 или SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="658f6-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="658f6-123">Можно щелкнуть на **квоты** на hello toochange hello размер общего файлового ресурса файла hello too5120 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="658f6-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="658f6-124">См. слишком[калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello хранилища стоимость использования хранилища Azure File.</span><span class="sxs-lookup"><span data-stu-id="658f6-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="658f6-126">Отправка и загрузка файлов</span><span class="sxs-lookup"><span data-stu-id="658f6-126">Upload and download files</span></span>
1. <span data-ttu-id="658f6-127">Выберите ранее созданную общую папку.</span><span class="sxs-lookup"><span data-stu-id="658f6-127">Choose one file share your have already created.</span></span>

    ![Снимок экрана, показывающий, как tooupload и загрузки файлов с hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="658f6-129">Нажмите кнопку **отправить** Открытие hello пользовательский интерфейс для передачи файлов.</span><span class="sxs-lookup"><span data-stu-id="658f6-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Снимок экрана, показывающий, как tooupload файлы с портала hello](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="658f6-131">Подключение toofile общей папки</span><span class="sxs-lookup"><span data-stu-id="658f6-131">Connect toofile share</span></span>
-  <span data-ttu-id="658f6-132">Нажмите кнопку **Connect** для получения hello командной строки для монтажа hello общей папки из Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="658f6-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="658f6-133">Для пользователей Linux можно также ссылаться слишком[как toouse хранилища Azure File с Linux](storage-how-to-use-files-linux.md) для получения дополнительных инструкций подключение для других дистрибутивах Linux.</span><span class="sxs-lookup"><span data-stu-id="658f6-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Снимок экрана, показывающий, каким образом toomount hello общей папки](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="658f6-135">Можно скопировать hello команды для подключения файла делиться на Windows или Linux и запустите его из вы виртуальной Машины Azure или в локальной машины.</span><span class="sxs-lookup"><span data-stu-id="658f6-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Снимок экрана, показывающий команды присоединения hello для Windows и Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="658f6-137">**Подсказка.**</span><span class="sxs-lookup"><span data-stu-id="658f6-137">**Tip:**</span></span>  
<span data-ttu-id="658f6-138">Щелкните ключ доступа учетной записи хранения hello toofind для монтажа, **доступ для просмотра ключи для этой учетной записи хранения** внизу hello hello страница подключения.</span><span class="sxs-lookup"><span data-stu-id="658f6-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="658f6-139">См. также</span><span class="sxs-lookup"><span data-stu-id="658f6-139">See also</span></span>
<span data-ttu-id="658f6-140">Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="658f6-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="658f6-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="658f6-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="658f6-142">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="658f6-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)