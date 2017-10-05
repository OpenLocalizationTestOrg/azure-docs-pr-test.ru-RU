---
title: "Использование обозревателя хранилищ (предварительная версия) с хранилищем файлов Azure | Документация Майкрософт"
description: "Сведения о том, как использовать обозреватель хранилищ (предварительная версия) для работы с общими папками и файлами."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="fa0e4-103">Использование обозревателя хранилищ (предварительная версия) с хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="fa0e4-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="fa0e4-104">Хранилище файлов Azure — это служба, которая предлагает доступ к общим папкам в облаке с использованием стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="fa0e4-105">Поддерживаются версии SMB 2.1 и SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="fa0e4-106">Хранилище файлов Azure позволяет быстро и без дорогостоящей перезаписи выполнить перенос приложений прежних версий, связанных с общими папками.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="fa0e4-107">Хранилища файлов можно использовать для предоставления данных в открытом доступе по всему миру или для хранения данных приложений в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="fa0e4-108">Эта статья посвящена использованию обозревателя хранилищ (предварительная версия) для работы с общими папками и файлами.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa0e4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fa0e4-109">Prerequisites</span></span>

<span data-ttu-id="fa0e4-110">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="fa0e4-111">Скачайте и установите обозреватель хранилищ (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="fa0e4-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- <span data-ttu-id="fa0e4-112">[Установите подключение к учетной записи хранения или службе хранилища Azure](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-112">[Connect to a Azure storage account or service](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)</span></span>

## <a name="create-a-file-share"></a><span data-ttu-id="fa0e4-113">Создание файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="fa0e4-113">Create a File Share</span></span>

<span data-ttu-id="fa0e4-114">Все файлы должны находиться в общей папке. Это логическая группировка файлов.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="fa0e4-115">Учетная запись может содержать неограниченное количество общих папок. В каждой папке может храниться неограниченное количество файлов.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="fa0e4-116">Чтобы создать общую папку в обозревателе хранилищ (предварительная версия), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="fa0e4-117">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-118">В левой области разверните учетную запись хранения, в которой нужно создать общую папку.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="fa0e4-119">Щелкните правой кнопкой мыши **Общие папки** и в контекстном меню выберите **Создать общую папку**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Создание общей папки](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="fa0e4-121">Под папкой **Общие папки** отобразится текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="fa0e4-122">Введите имя вашей общей папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-122">Enter the name for your file share.</span></span> <span data-ttu-id="fa0e4-123">Список правил и ограничений, действующих при присвоении имен общим папкам, см. в [этом разделе](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Присвоение имени общей папке](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="fa0e4-125">Нажмите клавишу **ВВОД**, чтобы создать общую папку, или **ESC** для отмены.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="fa0e4-126">После успешного создания общей папки она отображается в папке **Общие папки** для выбранной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![Новая общая папка](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="fa0e4-128">Просмотр содержимого общей папки</span><span class="sxs-lookup"><span data-stu-id="fa0e4-128">View a file share's contents</span></span>

<span data-ttu-id="fa0e4-129">Общие папки содержат файлы и папки, которые также могут содержать файлы.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="fa0e4-130">Чтобы просмотреть содержимое общей папки в обозревателе хранилищ (предварительная версия), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="fa0e4-131">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-132">В левой области разверните учетную запись хранения, содержащую общую папку, которую необходимо просмотреть.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="fa0e4-133">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="fa0e4-134">Щелкните правой кнопкой мыши общую папку, которую необходимо просмотреть, и в контекстном меню выберите **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="fa0e4-135">Также можно дважды щелкнуть общую папку, которую необходимо просмотреть.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-135">You can also double-click the file share you wish to view.</span></span>

    ![Открытие общей папки](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="fa0e4-137">В основной области отобразится содержимое общей папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-137">The main pane will display the file share's contents.</span></span>
    
    ![Содержимое общей папки](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="fa0e4-139">Удаление общей папки</span><span class="sxs-lookup"><span data-stu-id="fa0e4-139">Delete a file share</span></span>

<span data-ttu-id="fa0e4-140">Общие папки можно легко создавать и удалять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="fa0e4-141">(Сведения о том, как удалять отдельные файлы, см. в разделе об [управлении файлами в общей папке](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="fa0e4-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="fa0e4-142">Чтобы удалить общую папку в обозревателе хранилищ (предварительная версия), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="fa0e4-143">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-144">В левой области разверните учетную запись хранения, содержащую общую папку, которую необходимо просмотреть.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="fa0e4-145">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="fa0e4-146">Щелкните правой кнопкой мыши общую папку, которую необходимо удалить, и выберите в контекстном меню команду **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="fa0e4-147">Также можно нажать кнопку **Удалить**, чтобы удалить выбранную общую папку.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Удалить](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="fa0e4-149">Щелкните **Да** в диалоговом окне подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Диалоговое окно подтверждения](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="fa0e4-151">Копирование общей папки</span><span class="sxs-lookup"><span data-stu-id="fa0e4-151">Copy a file share</span></span>

<span data-ttu-id="fa0e4-152">Обозреватель хранилищ (предварительная версия) позволяет скопировать общую папку в буфер обмена и вставить ее в другую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="fa0e4-153">(Сведения о том, как копировать отдельные файлы, см. в разделе об [управлении файлами в общей папке](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="fa0e4-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="fa0e4-154">Чтобы скопировать общую папку из одной учетной записи хранения в другую, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="fa0e4-155">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-156">В левой области разверните учетную запись хранения, содержащую общую папку, которую необходимо скопировать.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="fa0e4-157">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="fa0e4-158">Щелкните правой кнопкой мыши общую папку, которую необходимо скопировать, и выберите в контекстном меню пункт **Copy File Share** (Копировать общую папку).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Копирование общей папки](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="fa0e4-160">Щелкните правой кнопкой мыши учетную запись хранения, в которую требуется вставить общую папку, и выберите в контекстном меню команду **Paste File Share** (Вставить общую папку).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Вставка общей папки](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="fa0e4-162">Получение SAS для общей папки</span><span class="sxs-lookup"><span data-stu-id="fa0e4-162">Get the SAS for a file share</span></span>

<span data-ttu-id="fa0e4-163">[Подписанный URL-адрес (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) обеспечивает делегированный доступ к ресурсам в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="fa0e4-164">Это означает, что клиенту можно предоставить ограниченное право на работу с объектами в вашей учетной записи хранения на определенный период времени и с определенным набором разрешений, не сообщая ему ключи доступа к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="fa0e4-165">Чтобы создать SAS для общей папки, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="fa0e4-166">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-167">В левой области разверните учетную запись хранения, содержащую общую папку, для которой необходимо получить SAS.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="fa0e4-168">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="fa0e4-169">Щелкните правой кнопкой мыши нужную общую папку и в контекстном меню выберите команду **Get Shared Access Signature** (Получить подписанный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Получение подписанного URL-адреса](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="fa0e4-171">В диалоговом окне **Shared Access Signature** (Подписанный URL-адрес) укажите политику, даты начала и окончания, часовой пояс и уровни доступа для ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![Диалоговое окно SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="fa0e4-173">Указав параметры SAS, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="fa0e4-174">Во втором диалоговом окне **Подписанный URL-адрес** отобразится общая папка вместе с URL-адресом и строками запросов, которые вы можете использовать для доступа к ресурсу хранилища.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="fa0e4-175">Выберите команду **Копировать** рядом с URL-адресом, который необходимо скопировать в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Второе диалоговое окно SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="fa0e4-177">По завершении нажмите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="fa0e4-178">Управление политиками доступа для общей папки</span><span class="sxs-lookup"><span data-stu-id="fa0e4-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="fa0e4-179">Чтобы управлять (добавлять и удалять) политиками доступа для общих папок, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="fa0e4-180">Политики доступа используются для создания URL-адресов SAS, которые пользователи могут использовать, чтобы получить доступ к файловому ресурсу хранилища в течение определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="fa0e4-181">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="fa0e4-182">В левой области разверните учетную запись хранения, содержащую общую папку, политиками которой необходимо управлять.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="fa0e4-183">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="fa0e4-184">Выберите нужную общую папку и в контекстном меню выберите пункт **Manage Access Policies** (Управление политиками доступа).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Контекстное меню для управления политиками доступа](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="fa0e4-186">В диалоговом окне **Политики доступа** будут отображаться все политики доступа, созданные для выбранной общей папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Политики доступа](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="fa0e4-188">Выполните описанные ниже действия в зависимости от задач управления политиками доступа.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="fa0e4-189">**Добавление новой политики доступа** — выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="fa0e4-190">Добавленная политика доступа отобразится в диалоговом окне **Политики доступа** сразу же после создания (при настройках по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="fa0e4-191">**Изменение политики доступа** — внесите все необходимые изменения и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="fa0e4-192">**Удаление политики доступа** — выберите **Удалить** рядом с политикой доступа, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="fa0e4-193">Создайте новый URL-адрес SAS с помощью созданной ранее политики доступа.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Получение SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Имя и свойства SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="fa0e4-196">Управление файлами в общей папке</span><span class="sxs-lookup"><span data-stu-id="fa0e4-196">Managing files in a file share</span></span>

<span data-ttu-id="fa0e4-197">После создания общей папки можно отправлять туда файлы, скачивать и открывать их на локальном компьютере, а также выполнять другие действия.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="fa0e4-198">Чтобы управлять файлами (и папками) в общей папке, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="fa0e4-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="fa0e4-199">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="fa0e4-200">В левой области разверните учетную запись хранения, содержащую общую папку, которой вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="fa0e4-201">Разверните папку **Общие папки** учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="fa0e4-202">Дважды щелкните общую папку, которую необходимо просмотреть.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="fa0e4-203">В основной области отобразится содержимое общей папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-203">The main pane will display the file share's contents.</span></span>

    ![Содержимое общей папки](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="fa0e4-205">В основной области отобразится содержимое общей папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="fa0e4-206">Следуйте приведенным ниже инструкциям в зависимости от задачи, которую необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="fa0e4-207">**Отправка файлов в общую папку**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="fa0e4-208">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-208">a.</span></span>  <span data-ttu-id="fa0e4-209">На панели инструментов в основной области нажмите кнопку **Отправить**, а затем выберите **Отправить файлы** в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Отправка файлов](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="fa0e4-211">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-211">b.</span></span> <span data-ttu-id="fa0e4-212">В диалоговом окне **Отправка файлов** нажмите кнопку с многоточием (**…**) справа от поля **Файлы**, чтобы выбрать файлы для отправки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Добавление файлов](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="fa0e4-214">В.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-214">c.</span></span> <span data-ttu-id="fa0e4-215">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-215">Select **Upload**.</span></span>

    - <span data-ttu-id="fa0e4-216">**Отправка папки в общую папку**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="fa0e4-217">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-217">a.</span></span> <span data-ttu-id="fa0e4-218">На панели инструментов в основной области нажмите кнопку **Отправить**, а затем выберите **Upload Folder** (Отправить папку) в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Меню для отправки папок](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="fa0e4-220">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-220">b.</span></span> <span data-ttu-id="fa0e4-221">В диалоговом окне **Отправить папку** (Отправка папки) нажмите кнопку с многоточием (**…**) справа от поля **Папка**, чтобы выбрать папку, содержимое которой необходимо отправить.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="fa0e4-222">c.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-222">c.</span></span> <span data-ttu-id="fa0e4-223">При необходимости укажите папку, в которую будут отправлено содержимое выбранной папки.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="fa0e4-224">Если такой папки не существует, она будет создана.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="fa0e4-225">d.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-225">d.</span></span> <span data-ttu-id="fa0e4-226">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-226">Select **Upload**.</span></span>

    - <span data-ttu-id="fa0e4-227">**Скачивание файла на локальный компьютер**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="fa0e4-228">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-228">a.</span></span> <span data-ttu-id="fa0e4-229">Выберите файл, который необходимо скачать.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="fa0e4-230">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-230">b.</span></span> <span data-ttu-id="fa0e4-231">На панели инструментов в основной области нажмите кнопку **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="fa0e4-232">c.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-232">c.</span></span> <span data-ttu-id="fa0e4-233">В диалоговом окне **Specify where to save the downloaded file** (Укажите расположение для сохранения загруженного файла) укажите расположение, в которое нужно скачать файл, а также имя, которое собираетесь ему присвоить.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="fa0e4-234">d.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-234">d.</span></span> <span data-ttu-id="fa0e4-235">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-235">Select **Save**.</span></span>

    - <span data-ttu-id="fa0e4-236">**Открытие файла на локальном компьютере**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="fa0e4-237">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-237">a.</span></span>  <span data-ttu-id="fa0e4-238">Выберите файл, который необходимо открыть.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="fa0e4-239">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-239">b.</span></span>  <span data-ttu-id="fa0e4-240">На панели инструментов в основной области нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="fa0e4-241">В.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-241">c.</span></span>  <span data-ttu-id="fa0e4-242">Файл будет скачан и открыт с помощью приложения, выбор которого зависит от типа файла.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="fa0e4-243">**Копирование файла в буфер обмена**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="fa0e4-244">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-244">a.</span></span> <span data-ttu-id="fa0e4-245">Выберите файл, который необходимо скопировать.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="fa0e4-246">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-246">b.</span></span> <span data-ttu-id="fa0e4-247">На панели инструментов в основной области нажмите кнопку **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="fa0e4-248">В.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-248">c.</span></span> <span data-ttu-id="fa0e4-249">В левой области перейдите в другую общую папку и дважды щелкните ее, чтобы она отобразилась в основной области.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="fa0e4-250">d.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-250">d.</span></span> <span data-ttu-id="fa0e4-251">На панели инструментов в основной области выберите **Вставить**, чтобы создать копию файла.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="fa0e4-252">**Удаление файла**</span><span class="sxs-lookup"><span data-stu-id="fa0e4-252">**Delete a file**</span></span>

        <span data-ttu-id="fa0e4-253">а.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-253">a.</span></span> <span data-ttu-id="fa0e4-254">Выберите файл, который необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="fa0e4-255">b.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-255">b.</span></span> <span data-ttu-id="fa0e4-256">На панели инструментов в основной области нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="fa0e4-257">c.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-257">c.</span></span> <span data-ttu-id="fa0e4-258">Щелкните **Да** в диалоговом окне подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fa0e4-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa0e4-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa0e4-259">Next steps</span></span>

- <span data-ttu-id="fa0e4-260">Просмотрите [последние заметки о выпуске обозревателя хранилищ (предварительная версия) и связанные с ним видео](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="fa0e4-261">Узнайте, как [создавать приложения с помощью больших двоичных объектов (BLOB), таблиц, очередей и файлов Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="fa0e4-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
