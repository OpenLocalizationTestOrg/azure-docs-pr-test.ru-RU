---
title: "Загрузка VHD-файла в Azure DevTest Labs с помощью обозревателя хранилищ Microsoft Azure | Документация Майкрософт"
description: "Загрузка VHD-файла в учетную запись хранения лаборатории с помощью обозревателя хранилищ Microsoft Azure"
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
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="1c2e6-103">Загрузка VHD-файла в учетную запись хранения лаборатории с помощью обозревателя хранилищ Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1c2e6-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="1c2e6-104">В Azure DevTest Labs можно использовать VHD-файлы для создания пользовательских образов, которые используются при подготовке виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="1c2e6-105">В этой статье описывается использование [обозревателя хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) для передачи VHD-файла в учетную запись хранения лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="1c2e6-106">Когда вы закончите скачивание VHD-файла, переходите к разделу [Дальнейшие действия](#next-steps), где перечислены несколько статей. В них описано, как создать пользовательский образ из скачанного VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="1c2e6-107">См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="1c2e6-108">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="1c2e6-108">Step-by-step instructions</span></span>

<span data-ttu-id="1c2e6-109">Следующие шаги показывают, как можно отправить VHD-файл в DevTest Labs с помощью [обозревателя хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="1c2e6-110">[Скачайте и установите последнюю версию обозревателя хранилищ Microsoft Azure](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="1c2e6-111">Получите имя учетной записи хранения лаборатории с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="1c2e6-112">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="1c2e6-113">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="1c2e6-114">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="1c2e6-115">В колонке лаборатории выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="1c2e6-116">В колонке **Configuration** (Конфигурация) лаборатории выберите **Custom images (VHDs)** (Пользовательские образы (VHD)).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="1c2e6-117">В колонке **Custom images** (Пользовательские образы) выберите **+Add** (+ Добавить).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="1c2e6-118">В колонке **Custom images** (Пользовательские образы) выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="1c2e6-119">В колонке **VHD** щелкните **Upload a VHD file using PowerShell** (Отправить VHD-файл с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Отправка VHD с помощью PowerShell][0]
    
    1. <span data-ttu-id="1c2e6-121">Колонка **Upload an image using PowerShell** (Отправка образа с помощью PowerShell) отображает вызов командлета **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="1c2e6-122">Первый параметр (*Destination* (Назначение)) содержит имя учетной записи хранения для лаборатории в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="1c2e6-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="1c2e6-123">https://<имя_учетной_записи_хранения>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="1c2e6-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="1c2e6-124">Запишите имя учетной записи хранения, оно понадобится вам дальше.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="1c2e6-125">Подключитесь к учетной записи подписки Azure с помощью обозревателя хранилищ.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="1c2e6-126">Обозреватель хранилищ поддерживает несколько вариантов подключения.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="1c2e6-127">В этом разделе показано подключение к учетной записи хранения, связанной с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="1c2e6-128">Другие варианты подключения, поддерживаемые обозревателем хранилищ, см. в статье [Приступая к работе с обозревателем службы хранилища (предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="1c2e6-129">Откройте обозреватель хранилищ.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="1c2e6-130">В обозревателе хранилищ выберите раздел **Параметры учетной записи Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Параметры учетной записи Azure][1]
    
    1. <span data-ttu-id="1c2e6-132">На панели слева отображаются учетные записи Майкрософт, в которые вы вошли.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="1c2e6-133">Чтобы подключиться к другой учетной записи, выберите **Добавить учетную запись**. Затем выполните инструкции в диалоговых окнах, чтобы войти в учетную запись Майкрософт, связанную минимум с одной активной подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Добавить учетную запись][2]
    
    1. <span data-ttu-id="1c2e6-135">Выполнив вход с помощью учетной записи Майкрософт, на панели слева вы увидите подписки Azure, связанные с этой учетной записью.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="1c2e6-136">Выберите подписки Azure, с которыми вы хотите работать, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="1c2e6-137">(Чтобы выбрать все подписки, установите флажок **Все подписки**. Чтобы отменить выбор, снимите этот флажок.)</span><span class="sxs-lookup"><span data-stu-id="1c2e6-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Выбор подписок Azure][3]
    
    1. <span data-ttu-id="1c2e6-139">На панели слева отобразятся все учетные записи хранения, связанные с выбранными подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Выбранные подписки Azure][4]

1. <span data-ttu-id="1c2e6-141">Найдите учетную запись хранения лаборатории:</span><span class="sxs-lookup"><span data-stu-id="1c2e6-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="1c2e6-142">На панели слева в обозревателе хранилищ найдите и разверните узел подписки Azure, которой принадлежит лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="1c2e6-143">В этом узле подписки разверните узел **Учетные записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="1c2e6-144">Разверните узел учетной записи хранения лаборатории, где вы увидите узлы **Контейнеры больших двоичных объектов**, **Общие файловые ресурсы**, **Очереди** и **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="1c2e6-145">Разверните узел **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="1c2e6-146">Выберите контейнер больших двоичных объектов uploads. В области справа отобразится его содержимое.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Каталог для отправки][5]

1. <span data-ttu-id="1c2e6-148">Отправьте VHD-файл с помощью обозревателя хранилищ.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="1c2e6-149">На панели справа в обозревателе хранилищ вы увидите список больших двоичных объектов, расположенных в соответствующем контейнере **uploads** в учетной записи хранения лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="1c2e6-150">На панели инструментов редактора больших двоичных объектов выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Кнопка "Отправить"][6]
    
    1. <span data-ttu-id="1c2e6-152">В раскрывающемся меню **отправки** выберите пункт **Отправка файлов**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="1c2e6-153">В диалоговом окне **Отправка файлов** нажмите кнопку с многоточием.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Выбор файла][8]  

    1. <span data-ttu-id="1c2e6-155">В диалоговом окне **Выбор файлов для отправки** перейдите к нужному VHD-файлу, выберите его и нажмите **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="1c2e6-156">Вы вернетесь в диалоговое окно **Отправка файлов**. Измените здесь **тип большого двоичного объекта**, указав значение **Страничный BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="1c2e6-157">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-157">Select **Upload**.</span></span>

        ![Выбор файла][9]  
    
    1. <span data-ttu-id="1c2e6-159">Обозреватель хранилищ отображает на панели **Журнал действий** состояние загрузки (а также ссылки для отмены отправки).</span><span class="sxs-lookup"><span data-stu-id="1c2e6-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="1c2e6-160">В зависимости от размера VHD-файла и скорости подключения отправка файла может быть продолжительной.</span><span class="sxs-lookup"><span data-stu-id="1c2e6-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Статус отправки файлов][10]  

## <a name="next-steps"></a><span data-ttu-id="1c2e6-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c2e6-162">Next steps</span></span>

- [<span data-ttu-id="1c2e6-163">Управление пользовательскими образами Azure DevTest Labs для создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="1c2e6-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="1c2e6-164">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c2e6-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
