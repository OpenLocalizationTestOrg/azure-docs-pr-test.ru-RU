---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью обозревателя хранилищ Microsoft Azure | Документы Microsoft"
description: "Отправка toolab файл виртуального жесткого диска учетной записи хранилища с помощью обозревателя хранилищ Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="f6ce1-103">Отправка toolab файл виртуального жесткого диска учетной записи хранилища с помощью обозревателя хранилищ Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f6ce1-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="f6ce1-104">В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="f6ce1-105">В этой статье показано, как toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) учетная запись хранения лаборатории tooa файлов tooupload виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="f6ce1-106">После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="f6ce1-107">См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="f6ce1-108">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="f6ce1-108">Step-by-step instructions</span></span>

<span data-ttu-id="f6ce1-109">Здравствуйте следующие обход действия можно выполнить с помощью Отправка VHD файлов tooDevTest лаборатории с использованием [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="f6ce1-110">[Загрузите и установите последнюю версию Microsoft Azure Storage Explorer hello hello](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="f6ce1-111">Получите имя hello hello лаборатории учетной записи хранилища с помощью портала Azure hello:</span><span class="sxs-lookup"><span data-stu-id="f6ce1-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="f6ce1-112">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="f6ce1-113">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="f6ce1-114">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="f6ce1-115">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="f6ce1-116">В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="f6ce1-117">На hello **пользовательских образов** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="f6ce1-118">На hello **настраиваемое изображение** колонке выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="f6ce1-119">На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Отправка VHD с помощью PowerShell][0]
    
    1. <span data-ttu-id="f6ce1-121">Hello **отправить изображение с помощью PowerShell** колонке отображает toohello вызов **Add-AzureVhd** командлета.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="f6ce1-122">Здравствуйте, первый параметр (*назначения*) содержит имя учетной записи хранения hello лаборатории hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="f6ce1-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="f6ce1-123">https://<имя_учетной_записи_хранения>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="f6ce1-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="f6ce1-124">Запишите имя учетной записи хранения hello как он используется в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="f6ce1-125">Подключите tooan учетной записи подписки Azure, с помощью обозревателя хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="f6ce1-126">Обозреватель хранилищ поддерживает несколько вариантов подключения.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="f6ce1-127">В этом разделе рассмотрены подключения учетную запись хранения tooa, связанную с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="f6ce1-128">toosee hello другие параметры соединения, поддерживаемые обозреватель хранилищ см. в статье toohello [Приступая к работе с обозреватель хранилищ](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="f6ce1-129">Откройте обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="f6ce1-130">В обозревателе хранилищ выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Параметры учетной записи Azure][1]
    
    1. <span data-ttu-id="f6ce1-132">Hello левая панель содержит учетные записи Microsoft hello, вход в систему.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="f6ce1-133">Учетная запись tooconnect tooanother, выберите **добавить учетную запись**и выполните toosign hello диалоговых окон, учетную запись Майкрософт, связанный с по крайней мере одну подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Добавить учетную запись][2]
    
    1. <span data-ttu-id="f6ce1-135">После успешной регистрации вход с учетной записью Microsoft hello левой заполняет hello Azure подписок, связанных с этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="f6ce1-136">Здравствуйте, выберите подписки Azure, с которыми вы хотите toowork, а затем выберите **применить**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="f6ce1-137">(При выборе **все подписки** переключает hello выделение всех или ни один из hello в списке подписок Azure.)</span><span class="sxs-lookup"><span data-stu-id="f6ce1-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Выбор подписок Azure][3]
    
    1. <span data-ttu-id="f6ce1-139">Hello левая панель отображает связанные с подписками Azure hello выбранные учетные записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Выбранные подписки Azure][4]

1. <span data-ttu-id="f6ce1-141">Найдите учетную запись хранения лаборатории hello:</span><span class="sxs-lookup"><span data-stu-id="f6ce1-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="f6ce1-142">В левой панели проводника хранилищ hello найдите и разверните узел hello hello подписки Azure, которой принадлежит hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="f6ce1-143">Разверните узел подписки hello **учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="f6ce1-144">Разверните узлы tooreveal узел учетной записи хранилища hello лаборатории для **контейнеров больших двоичных объектов**, **общие файловые ресурсы**, **очереди**, и **таблиц**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="f6ce1-145">Разверните hello **контейнеров больших двоичных объектов** узла.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="f6ce1-146">Выберите toodisplay контейнер больших двоичных объектов передачи hello его содержимое в правой области hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Каталог для отправки][5]

1. <span data-ttu-id="f6ce1-148">Отправьте VHD-файл hello, с помощью обозревателя хранилищ:</span><span class="sxs-lookup"><span data-stu-id="f6ce1-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="f6ce1-149">В правой панели обозревателя хранилищ hello, вы увидите список больших двоичных объектов hello в hello **отправляет** контейнер BLOB-объектов учетной записи хранения hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="f6ce1-150">На панели инструментов редактора hello больших двоичных объектов, выберите **отправки**</span><span class="sxs-lookup"><span data-stu-id="f6ce1-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Кнопка "Отправить"][6]
    
    1. <span data-ttu-id="f6ce1-152">Из hello **отправить** раскрывающееся меню, выберите **Отправка файлов...** .</span><span class="sxs-lookup"><span data-stu-id="f6ce1-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="f6ce1-153">На hello **передачи файлов** диалоговое окно, выберите hello кнопку с многоточием.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Выбор файла][8]  

    1. <span data-ttu-id="f6ce1-155">На hello **tooupload выберите файлов** диалогового окна обзора toohello требуемого файла виртуального жесткого диска, выберите его, а затем выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="f6ce1-156">При вернул toohello **передачи файлов** диалогового окна, изменение **больших двоичных объектов типа** слишком**страничного большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="f6ce1-157">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-157">Select **Upload**.</span></span>

        ![Выбор файла][9]  
    
    1. <span data-ttu-id="f6ce1-159">Обозреватель хранилищ Hello **журнал действий** области отображается состояние загрузки hello (а также отправить hello toocancel ссылки).</span><span class="sxs-lookup"><span data-stu-id="f6ce1-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="f6ce1-160">Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения.</span><span class="sxs-lookup"><span data-stu-id="f6ce1-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Статус отправки файлов][10]  

## <a name="next-steps"></a><span data-ttu-id="f6ce1-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6ce1-162">Next steps</span></span>

- [<span data-ttu-id="f6ce1-163">Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="f6ce1-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="f6ce1-164">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6ce1-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
