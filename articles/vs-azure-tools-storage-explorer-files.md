---
title: "aaaUsing обозреватель хранилищ (Предварительная версия) с помощью хранилища Azure File | Документы Microsoft"
description: "Узнайте, как узнать, как toouse toowork обозреватель хранилищ (Предварительная версия) с файла, папки и файлы."
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
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="65018-103">Использование обозревателя хранилищ (предварительная версия) с хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="65018-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="65018-104">Файл Azure хранилища — это служба, предоставляющая файл общие файлы с помощью облака hello hello стандартный протокол Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="65018-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="65018-105">Поддерживаются версии SMB 2.1 и SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="65018-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="65018-106">При хранении файлов Azure можно перенести старых приложений, использующих на файл tooAzure общих папок, быстро и без дорогостоящей излишнего копирования.</span><span class="sxs-lookup"><span data-stu-id="65018-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="65018-107">Файл хранилища tooexpose данные можно использовать публично world toohello или toostore данные приложения в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="65018-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="65018-108">В этой статье вы узнаете, как toouse toowork обозреватель хранилищ (Предварительная версия) с файла, папки и файлы.</span><span class="sxs-lookup"><span data-stu-id="65018-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65018-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="65018-109">Prerequisites</span></span>

<span data-ttu-id="65018-110">в этой статье инструкциям toocomplete hello, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="65018-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="65018-111">Скачайте и установите обозреватель службы хранилища (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="65018-112">Подключите tooa учетной записи хранилища Azure или службы</span><span class="sxs-lookup"><span data-stu-id="65018-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="65018-113">Создание файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="65018-113">Create a File Share</span></span>

<span data-ttu-id="65018-114">Все файлы должны находиться в общей папке. Это логическая группировка файлов.</span><span class="sxs-lookup"><span data-stu-id="65018-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="65018-115">Учетная запись может содержать неограниченное количество общих папок. В каждой папке может храниться неограниченное количество файлов.</span><span class="sxs-lookup"><span data-stu-id="65018-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="65018-116">Привет, следующие шаги показывают, как toocreate файловый ресурс в обозреватель хранилищ (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="65018-117">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-118">Hello левой панели разверните узел учетной записи хранилища hello, который требуется hello toocreate общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="65018-119">Щелкните правой кнопкой мыши **общие файловые ресурсы**и - контекстном меню hello - выберите **создать общую папку**.</span><span class="sxs-lookup"><span data-stu-id="65018-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Создание общей папки](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="65018-121">Текстовое поле отображается под hello **общие файловые ресурсы** папки.</span><span class="sxs-lookup"><span data-stu-id="65018-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="65018-122">Введите имя файлового ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="65018-122">Enter hello name for your file share.</span></span> <span data-ttu-id="65018-123">. В разделе hello [совместно использовать правила именования](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) раздел список правила и ограничения по именованию общие файловые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="65018-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Именование hello общей папки](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="65018-125">Нажмите клавишу **ввод** при done toocreate hello общей папки или **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="65018-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="65018-126">После успешного создания общей папки hello оно будет отображаться в списке hello **общие файловые ресурсы** выбрать папку для hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="65018-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![Новый общий ресурс Hello](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="65018-128">Просмотр содержимого общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-128">View a file share's contents</span></span>

<span data-ttu-id="65018-129">Общие папки содержат файлы и папки, которые также могут содержать файлы.</span><span class="sxs-lookup"><span data-stu-id="65018-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="65018-130">Hello ниже показано, как предоставить доступ tooview hello содержимое файла в обозревателе хранилища (Предварительная версия): +</span><span class="sxs-lookup"><span data-stu-id="65018-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="65018-131">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-132">Hello левой панели разверните содержащий hello общей папки нужно tooview учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="65018-133">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="65018-134">Щелкните правой кнопкой мыши hello общей папке правильно tooview и - контекстном меню hello - выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="65018-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="65018-135">Можно также дважды щелкнуть hello общей папки нужно tooview.</span><span class="sxs-lookup"><span data-stu-id="65018-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Открытие общей папки](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="65018-137">Hello главной панели отображается содержимое hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="65018-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Здравствуйте, содержимое общего ресурса](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="65018-139">Удаление общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-139">Delete a file share</span></span>

<span data-ttu-id="65018-140">Общие папки можно легко создавать и удалять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="65018-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="65018-141">(toosee как toodelete отдельных файлов, см. раздел toohello [управления файлами в общей папке](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="65018-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="65018-142">Привет, следующие шаги показывают, как toodelete файловый ресурс в обозреватель хранилищ (Предварительная версия):</span><span class="sxs-lookup"><span data-stu-id="65018-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="65018-143">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-144">Hello левой панели разверните содержащий hello общей папки нужно tooview учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="65018-145">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="65018-146">Щелкните правой кнопкой мыши hello общей папке правильно toodelete и - контекстном меню hello - выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="65018-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="65018-147">Можно также нажать **удаление** toodelete hello выбранного общей папки.</span><span class="sxs-lookup"><span data-stu-id="65018-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Удалить](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="65018-149">Выберите **Да** toohello диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="65018-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Диалоговое окно подтверждения](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="65018-151">Копирование общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-151">Copy a file share</span></span>

<span data-ttu-id="65018-152">Обозреватель хранилищ (Предварительная версия) позволяет toocopy буфер обмена toohello папки файла, а затем вставьте этого ресурса в другой учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="65018-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="65018-153">(toosee как toocopy отдельных файлов, см. раздел toohello [управления файлами в общей папке](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="65018-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="65018-154">Hello следующие шаги иллюстрируют, как файл toocopy общую папку из одного tooanother учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="65018-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="65018-155">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-156">Hello левой панели разверните содержащий hello общей папки нужно toocopy учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="65018-157">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="65018-158">Щелкните правой кнопкой мыши hello общей папке правильно toocopy и - контекстном меню hello - выберите **копирования общей папки**.</span><span class="sxs-lookup"><span data-stu-id="65018-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Копирование общей папки](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="65018-160">Щелкните правой кнопкой мыши нужный hello «target» учетной записи хранилища в который toopaste hello общей папки и - контекстном меню hello - выберите **вставить общая папка**.</span><span class="sxs-lookup"><span data-stu-id="65018-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Вставка общей папки](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="65018-162">Получить hello SAS для общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="65018-163">Объект [подписанного URL-адреса (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) предоставляет tooresources делегированный доступ в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="65018-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="65018-164">Это означает, что предоставлять клиент ограниченную tooobjects разрешения вашей учетной записи хранилища в течение заданного времени, используя указанный набор разрешений, без необходимости tooshare ключей доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="65018-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="65018-165">Hello ниже показано, как toocreate подписанный URL-адрес для файла общий доступ к: +</span><span class="sxs-lookup"><span data-stu-id="65018-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="65018-166">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-167">В левой области hello разверните содержащий hello общую папку, для которой вы хотите tooget подписанный URL-адрес учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="65018-168">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="65018-169">Щелкните правой кнопкой мыши hello требуемой общей папки, а - hello контекстное меню: выберите **получить подпись общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="65018-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Получение подписанного URL-адреса](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="65018-171">В hello **подписи общего доступа** диалогового окна, укажите политику hello, датами начала и окончания, часовой пояс, а для ресурсов hello уровни доступа.</span><span class="sxs-lookup"><span data-stu-id="65018-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Диалоговое окно SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="65018-173">По завершении параметров hello SAS, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="65018-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="65018-174">Второй **подписи общего доступа** списки hello общей папки hello URL-адресом, на который можно использовать tooaccess QueryStrings hello ресурса хранилища будет выведено диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="65018-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="65018-175">Выберите **копирования** Далее toohello URL-адрес, можно обратиться в буфер обмена toohello toocopy.</span><span class="sxs-lookup"><span data-stu-id="65018-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Второе диалоговое окно SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="65018-177">По завершении нажмите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="65018-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="65018-178">Управление политиками доступа для общей папки</span><span class="sxs-lookup"><span data-stu-id="65018-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="65018-179">Hello ниже показано, как toomanage (Добавление и удаление) политик доступа для общей папки: +.</span><span class="sxs-lookup"><span data-stu-id="65018-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="65018-180">Hello политик доступа используется для создания URL-адреса SAS, через который пользователи могут использовать hello tooaccess хранения файла ресурсов за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="65018-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="65018-181">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="65018-182">В левой области hello разверните содержащий hello общей папки, которого вы хотите toomanage политики доступа учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="65018-183">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="65018-184">Выберите hello требуемой общей папки, а - контекстном меню hello - **Управление политиками доступа**.</span><span class="sxs-lookup"><span data-stu-id="65018-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Контекстное меню для управления политиками доступа](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="65018-186">Hello **политики доступа** диалогового окна будут отображаться все политики доступа уже создан для hello выбранной общей папки.</span><span class="sxs-lookup"><span data-stu-id="65018-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Политики доступа](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="65018-188">Выполните следующие действия в зависимости от задачи управления политики доступа hello.</span><span class="sxs-lookup"><span data-stu-id="65018-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="65018-189">**Добавление новой политики доступа** — выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="65018-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="65018-190">После создания, hello **политики доступа** диалоговое окно, отображающее hello добавленным доступ к политике (с параметрами по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="65018-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="65018-191">**Изменение политики доступа** — внесите все необходимые изменения и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65018-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="65018-192">**Удалить политику доступа** — выберите **удалить** следующая политика доступа toohello, нужно tooremove.</span><span class="sxs-lookup"><span data-stu-id="65018-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="65018-193">Создайте новый URL-адрес SAS hello политики доступа, созданный ранее с помощью:</span><span class="sxs-lookup"><span data-stu-id="65018-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Получение SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Имя и свойства SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="65018-196">Управление файлами в общей папке</span><span class="sxs-lookup"><span data-stu-id="65018-196">Managing files in a file share</span></span>

<span data-ttu-id="65018-197">После создания общей папки, можно отправить файл toothat общей папки, загрузите файл tooyour локального компьютера, откройте файл на локальном компьютере и многое другое.</span><span class="sxs-lookup"><span data-stu-id="65018-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="65018-198">Hello ниже показано, как поделиться toomanage hello файлы (и папки) в файле.</span><span class="sxs-lookup"><span data-stu-id="65018-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="65018-199">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="65018-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="65018-200">Hello левой панели разверните содержащий hello общей папки нужно toomanage учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="65018-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="65018-201">Разверните узел учетной записи хранилища hello **общие файловые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="65018-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="65018-202">Дважды щелкните общую папку hello нужно tooview.</span><span class="sxs-lookup"><span data-stu-id="65018-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="65018-203">Hello главной панели отображается содержимое hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="65018-203">hello main pane will display hello file share's contents.</span></span>

    ![Здравствуйте, содержимое общего ресурса](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="65018-205">Hello главной панели отображается содержимое hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="65018-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="65018-206">Выполните следующие действия в зависимости от задачи hello нужно tooperform:</span><span class="sxs-lookup"><span data-stu-id="65018-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="65018-207">**Отправка файлов tooa общей папки**</span><span class="sxs-lookup"><span data-stu-id="65018-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="65018-208">а.</span><span class="sxs-lookup"><span data-stu-id="65018-208">a.</span></span>  <span data-ttu-id="65018-209">На hello главной панели инструментов выберите **отправить**, а затем **передача файлов** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="65018-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Отправка файлов](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="65018-211">b.</span><span class="sxs-lookup"><span data-stu-id="65018-211">b.</span></span> <span data-ttu-id="65018-212">В hello **передачи файлов** диалоговое окно, выберите hello кнопку с многоточием (**...** ) кнопку на правой стороне hello hello **файлы** текстовое поле tooselect hello файлы нужно tooupload.</span><span class="sxs-lookup"><span data-stu-id="65018-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Добавление файлов](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="65018-214">В.</span><span class="sxs-lookup"><span data-stu-id="65018-214">c.</span></span> <span data-ttu-id="65018-215">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="65018-215">Select **Upload**.</span></span>

    - <span data-ttu-id="65018-216">**Отправить папку tooa общей папки**</span><span class="sxs-lookup"><span data-stu-id="65018-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="65018-217">а.</span><span class="sxs-lookup"><span data-stu-id="65018-217">a.</span></span> <span data-ttu-id="65018-218">На hello главной панели инструментов выберите **отправить**, а затем **отправить папку** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="65018-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Меню для отправки папок](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="65018-220">b.</span><span class="sxs-lookup"><span data-stu-id="65018-220">b.</span></span> <span data-ttu-id="65018-221">В hello **папки загрузки** диалоговое окно, выберите hello кнопку с многоточием (**...** ) кнопку на правой стороне hello hello **папки** текстовое поле tooselect hello папки, содержимое которой нужно tooupload.</span><span class="sxs-lookup"><span data-stu-id="65018-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="65018-222">c.</span><span class="sxs-lookup"><span data-stu-id="65018-222">c.</span></span> <span data-ttu-id="65018-223">Дополнительно укажите папку, в какие hello будет отправлен содержимого выбранной папки.</span><span class="sxs-lookup"><span data-stu-id="65018-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="65018-224">Если hello целевая папка не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="65018-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="65018-225">d.</span><span class="sxs-lookup"><span data-stu-id="65018-225">d.</span></span> <span data-ttu-id="65018-226">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="65018-226">Select **Upload**.</span></span>

    - <span data-ttu-id="65018-227">**Загрузите файл tooyour локального компьютера**</span><span class="sxs-lookup"><span data-stu-id="65018-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="65018-228">а.</span><span class="sxs-lookup"><span data-stu-id="65018-228">a.</span></span> <span data-ttu-id="65018-229">Выберите файл hello нужно toodownload.</span><span class="sxs-lookup"><span data-stu-id="65018-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="65018-230">b.</span><span class="sxs-lookup"><span data-stu-id="65018-230">b.</span></span> <span data-ttu-id="65018-231">На hello главной панели инструментов выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="65018-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="65018-232">c.</span><span class="sxs-lookup"><span data-stu-id="65018-232">c.</span></span> <span data-ttu-id="65018-233">В hello **укажите, куда toosave hello загружен файл** диалогового окна, укажите расположение hello, где нужно скачать файл hello и hello имени toogive его.</span><span class="sxs-lookup"><span data-stu-id="65018-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="65018-234">d.</span><span class="sxs-lookup"><span data-stu-id="65018-234">d.</span></span> <span data-ttu-id="65018-235">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="65018-235">Select **Save**.</span></span>

    - <span data-ttu-id="65018-236">**Открытие файла на локальном компьютере**</span><span class="sxs-lookup"><span data-stu-id="65018-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="65018-237">а.</span><span class="sxs-lookup"><span data-stu-id="65018-237">a.</span></span>  <span data-ttu-id="65018-238">Выберите файл hello нужно tooopen.</span><span class="sxs-lookup"><span data-stu-id="65018-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="65018-239">b.</span><span class="sxs-lookup"><span data-stu-id="65018-239">b.</span></span>  <span data-ttu-id="65018-240">На hello главной панели инструментов выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="65018-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="65018-241">c.</span><span class="sxs-lookup"><span data-stu-id="65018-241">c.</span></span>  <span data-ttu-id="65018-242">файл Hello будут загружены и открыть с помощью приложения hello, связанные с hello базовый тип файла.</span><span class="sxs-lookup"><span data-stu-id="65018-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="65018-243">**Скопируйте файл toohello буфер обмена**</span><span class="sxs-lookup"><span data-stu-id="65018-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="65018-244">а.</span><span class="sxs-lookup"><span data-stu-id="65018-244">a.</span></span> <span data-ttu-id="65018-245">Выберите файл hello нужно toocopy.</span><span class="sxs-lookup"><span data-stu-id="65018-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="65018-246">b.</span><span class="sxs-lookup"><span data-stu-id="65018-246">b.</span></span> <span data-ttu-id="65018-247">На hello главной панели инструментов выберите **копирования**.</span><span class="sxs-lookup"><span data-stu-id="65018-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="65018-248">c.</span><span class="sxs-lookup"><span data-stu-id="65018-248">c.</span></span> <span data-ttu-id="65018-249">В левой области hello перейдите tooanother общую папку и дважды щелкните его tooview его в основной области hello.</span><span class="sxs-lookup"><span data-stu-id="65018-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="65018-250">d.</span><span class="sxs-lookup"><span data-stu-id="65018-250">d.</span></span> <span data-ttu-id="65018-251">На hello главной панели инструментов выберите **вставить** toocreate копию файла hello.</span><span class="sxs-lookup"><span data-stu-id="65018-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="65018-252">**Удаление файла**</span><span class="sxs-lookup"><span data-stu-id="65018-252">**Delete a file**</span></span>

        <span data-ttu-id="65018-253">а.</span><span class="sxs-lookup"><span data-stu-id="65018-253">a.</span></span> <span data-ttu-id="65018-254">Выберите файл hello нужно toodelete.</span><span class="sxs-lookup"><span data-stu-id="65018-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="65018-255">b.</span><span class="sxs-lookup"><span data-stu-id="65018-255">b.</span></span> <span data-ttu-id="65018-256">На hello главной панели инструментов выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="65018-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="65018-257">c.</span><span class="sxs-lookup"><span data-stu-id="65018-257">c.</span></span> <span data-ttu-id="65018-258">Выберите **Да** toohello диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="65018-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65018-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65018-259">Next steps</span></span>

- <span data-ttu-id="65018-260">Представление hello [последние заметки о выпуске обозреватель хранилищ (Предварительная версия) и видео](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="65018-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="65018-261">Узнайте, каким образом слишком[создания приложений с помощью Azure BLOB-объектов, таблиц, очередей и файлов](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="65018-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
