---
title: "aaaManage ресурсы хранилища больших двоичных объектов с помощью обозревателя хранилища (Предварительная версия) | Документы Microsoft"
description: "Управление контейнерами BLOB-объектов и BLOB-объектами Azure с помощью обозревателя хранилищ (предварительная версия)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="1e7a7-103">Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="1e7a7-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="1e7a7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1e7a7-104">Overview</span></span>
<span data-ttu-id="1e7a7-105">[Хранилище больших двоичных объектов Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="1e7a7-106">Данные tooexpose хранилища больших двоичных объектов можно использовать публично world toohello или toostore данные приложения в частном порядке.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="1e7a7-107">В этой статье вы узнаете, как toouse toowork обозреватель хранилищ (Предварительная версия) с BLOB-контейнеры и большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e7a7-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e7a7-108">Prerequisites</span></span>
<span data-ttu-id="1e7a7-109">в этой статье инструкциям toocomplete hello, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="1e7a7-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="1e7a7-110">Скачайте и установите обозреватель службы хранилища (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="1e7a7-111">Подключите tooa учетной записи хранилища Azure или службы</span><span class="sxs-lookup"><span data-stu-id="1e7a7-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="1e7a7-112">Создание контейнера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-112">Create a blob container</span></span>
<span data-ttu-id="1e7a7-113">Все большие двоичные объекты должны находиться в контейнере. Это логическая группировка больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="1e7a7-114">Учетная запись может содержать неограниченное количество контейнеров. В каждом контейнере может храниться неограниченное количество больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="1e7a7-115">Hello ниже показано, как toocreate контейнер больших двоичных объектов в обозревателе хранилища (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="1e7a7-116">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-117">Hello левой панели разверните учетной записи хранилища hello, который требуется контейнер больших двоичных объектов toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="1e7a7-118">Щелкните правой кнопкой мыши **контейнеров больших двоичных объектов**и - контекстном меню hello - выберите **создать контейнер больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Контекстное меню для создания контейнеров BLOB-объектов][0]
4. <span data-ttu-id="1e7a7-120">Текстовое поле отображается под hello **контейнеров больших двоичных объектов** папки.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="1e7a7-121">Введите имя hello для контейнера большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="1e7a7-122">В разделе hello [правилах именования контейнеров](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) раздел список правила и ограничения по именованию контейнеров больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Текстовое поле для создания контейнеров BLOB-объектов][1]
5. <span data-ttu-id="1e7a7-124">Нажмите клавишу **ввод** после завершения контейнера больших двоичных объектов toocreate hello, или **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="1e7a7-125">После успешного создания контейнера больших двоичных объектов hello оно будет отображаться в списке hello **контейнеров больших двоичных объектов** выбрать папку для hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Контейнер BLOB-объектов создан][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="1e7a7-127">Просмотр содержимого контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-127">View a blob container's contents</span></span>
<span data-ttu-id="1e7a7-128">Контейнеры больших двоичных объектов содержат большие двоичные объекты и папки (которые также могут содержать большие двоичные объекты).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="1e7a7-129">Hello ниже показано, как содержимое hello tooview контейнер больших двоичных объектов в обозревателе хранилища (Предварительная версия):</span><span class="sxs-lookup"><span data-stu-id="1e7a7-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="1e7a7-130">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-131">Hello левой панели разверните содержащий hello контейнер больших двоичных объектов, нужно tooview учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="1e7a7-132">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-133">Щелкните правой кнопкой мыши контейнер больших двоичных объектов hello правильно tooview и - контекстном меню hello - выберите **открыть редактор контейнер больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="1e7a7-134">Можно также дважды щелкнуть hello контейнер больших двоичных объектов, нужно tooview.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Контекстное меню для открытия редактора контейнеров BLOB-объектов][19]
5. <span data-ttu-id="1e7a7-136">контейнер больших двоичных объектов hello содержимое будет выведено Hello главной панели.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-136">hello main pane will display hello blob container's contents.</span></span>

   ![Редактор контейнеров BLOB-объектов][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="1e7a7-138">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-138">Delete a blob container</span></span>
<span data-ttu-id="1e7a7-139">Контейнеры больших двоичных объектов можно легко создавать и удалять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="1e7a7-140">(toosee как toodelete отдельных больших двоичных объектов, см. раздел toohello [управление большими двоичными объектами в контейнер больших двоичных объектов](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="1e7a7-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="1e7a7-141">Hello ниже показано, как toodelete контейнер больших двоичных объектов в обозревателе хранилища (Предварительная версия):</span><span class="sxs-lookup"><span data-stu-id="1e7a7-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="1e7a7-142">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-143">Hello левой панели разверните содержащий hello контейнер больших двоичных объектов, нужно tooview учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="1e7a7-144">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-145">Щелкните правой кнопкой мыши контейнер больших двоичных объектов hello правильно toodelete и - контекстном меню hello - выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="1e7a7-146">Можно также нажать **удаление** toodelete hello выбранных больших двоичных объектов контейнера.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Контекстное меню для удаления контейнера BLOB-объектов][4]
5. <span data-ttu-id="1e7a7-148">Выберите **Да** toohello диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Подтверждение удаления контейнера BLOB-объектов][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="1e7a7-150">Копирование контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-150">Copy a blob container</span></span>
<span data-ttu-id="1e7a7-151">Обозреватель хранилищ (Предварительная версия) позволяет toocopy буфер обмена toohello контейнер больших двоичных объектов, а затем вставьте, который BLOB-объектов контейнера в другой учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="1e7a7-152">(toosee как toocopy отдельных больших двоичных объектов, см. раздел toohello [управление большими двоичными объектами в контейнер больших двоичных объектов](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="1e7a7-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="1e7a7-153">Привет, следующие шаги иллюстрируют tooanother учетной записи toocopy контейнер больших двоичных объектов из одного места хранения.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="1e7a7-154">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-155">Hello левой панели разверните содержащий hello контейнер больших двоичных объектов, нужно toocopy учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="1e7a7-156">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-157">Щелкните правой кнопкой мыши контейнер больших двоичных объектов hello правильно toocopy и - контекстном меню hello - выберите **контейнер больших двоичных объектов копирования**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Контекстное меню для копирования контейнера BLOB-объектов][6]
5. <span data-ttu-id="1e7a7-159">Щелкните правой кнопкой мыши нужный hello «target» учетной записи хранилища в который контейнер больших двоичных объектов toopaste hello и - контекстном меню hello - выберите **контейнер больших двоичных объектов для вставки**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Контекстное меню для вставки контейнера BLOB-объектов][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="1e7a7-161">Получить hello SAS для контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="1e7a7-162">Объект [подписанного URL-адреса (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) предоставляет tooresources делегированный доступ в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="1e7a7-163">Это означает, что предоставлять клиент ограниченную tooobjects разрешения вашей учетной записи хранилища в течение заданного времени, используя указанный набор разрешений, без необходимости совместное использование ключей доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="1e7a7-164">Hello ниже показано, как toocreate SAS для контейнера BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="1e7a7-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="1e7a7-165">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-166">В левой области hello разверните содержащий hello контейнер больших двоичных объектов, для которого вы хотите tooget подписанный URL-адрес учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="1e7a7-167">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-168">Щелкните правой кнопкой мыши требуемый BLOB-контейнере hello и - контекстном меню hello - выберите **получить подпись общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Контекстное меню для получения SAS][8]
5. <span data-ttu-id="1e7a7-170">В hello **подписи общего доступа** диалогового окна, укажите политику hello, датами начала и окончания, часовой пояс, а для ресурсов hello уровни доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Параметры получения SAS][9]
6. <span data-ttu-id="1e7a7-172">По завершении параметров hello SAS, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="1e7a7-173">Второй **подписи общего доступа** списки hello контейнер больших двоичных объектов hello URL-адресом, на который можно использовать tooaccess QueryStrings hello ресурса хранилища будет выведено диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="1e7a7-174">Выберите **копирования** Далее toohello URL-адрес, можно обратиться в буфер обмена toohello toocopy.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Копирование URL-адресов SAS][10]
8. <span data-ttu-id="1e7a7-176">По завершении нажмите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="1e7a7-177">Управление политиками доступа для контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="1e7a7-178">Hello ниже показано, как toomanage (Добавление и удаление) политик доступа для контейнера BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="1e7a7-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="1e7a7-179">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-180">Hello левой панели разверните учетной записи хранилища hello, содержащей контейнер больших двоичных объектов hello которого вы хотите toomanage политики доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="1e7a7-181">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-182">Выберите контейнер hello требуемый BLOB-объектов, а - контекстном меню hello - **Управление политиками доступа**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Контекстное меню для управления политиками доступа][11]
5. <span data-ttu-id="1e7a7-184">Hello **политики доступа** диалогового окна будут отображаться все политики доступа уже создан для контейнера hello выбранных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Параметры политик доступа][12]        
6. <span data-ttu-id="1e7a7-186">Выполните следующие действия в зависимости от задачи управления политики доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="1e7a7-187">**Добавление новой политики доступа** — выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="1e7a7-188">После создания, hello **политики доступа** диалоговое окно, отображающее hello добавленным доступ к политике (с параметрами по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="1e7a7-189">**Изменение политики доступа** — внесите все нужные изменения и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="1e7a7-190">**Удалить политику доступа** — выберите **удалить** следующая политика доступа toohello, нужно tooremove.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="1e7a7-191">Набор hello уровень общего доступа контейнера больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="1e7a7-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="1e7a7-192">По умолчанию каждый контейнер больших двоичных объектов значение слишком «Нет общего доступа».</span><span class="sxs-lookup"><span data-stu-id="1e7a7-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="1e7a7-193">Hello ниже показано, как toospecify открытого доступа уровня контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="1e7a7-194">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-195">Hello левой панели разверните учетной записи хранилища hello, содержащей контейнер больших двоичных объектов hello которого вы хотите toomanage политики доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="1e7a7-196">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-197">Выберите контейнер hello требуемый BLOB-объектов, а - контекстном меню hello - **задать уровень общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Контекстное меню для настройки уровня общего доступа][13]
5. <span data-ttu-id="1e7a7-199">В hello **задать уровень общего доступа контейнера** диалогового окна, укажите hello требуемого уровня доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Параметры настройки уровня общего доступа][14]
6. <span data-ttu-id="1e7a7-201">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="1e7a7-202">Управление большими двоичными объектами в контейнере</span><span class="sxs-lookup"><span data-stu-id="1e7a7-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="1e7a7-203">После создания контейнера больших двоичных объектов, можно отправить toothat большого двоичного объекта BLOB-контейнере, загрузить большой двоичный объект tooyour локального компьютера, откройте большого двоичного объекта на локальном компьютере и многое другое.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="1e7a7-204">Привет, следующие шаги иллюстрируют, как toomanage hello больших двоичных объектов (и папки) в контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="1e7a7-205">Откройте обозреватель хранилищ (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="1e7a7-206">Hello левой панели разверните содержащий hello контейнер больших двоичных объектов, нужно toomanage учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="1e7a7-207">Разверните узел учетной записи хранилища hello **контейнеров больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="1e7a7-208">Дважды щелкните контейнер больших двоичных объектов hello нужно tooview.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="1e7a7-209">контейнер больших двоичных объектов hello содержимое будет выведено Hello главной панели.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-209">hello main pane will display hello blob container's contents.</span></span>

   ![Просмотр контейнера BLOB-объектов][3]
6. <span data-ttu-id="1e7a7-211">контейнер больших двоичных объектов hello содержимое будет выведено Hello главной панели.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="1e7a7-212">Выполните следующие действия в зависимости от задачи hello нужно tooperform:</span><span class="sxs-lookup"><span data-stu-id="1e7a7-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="1e7a7-213">**Отправка файлов контейнер больших двоичных объектов tooa**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="1e7a7-214">На hello главной панели инструментов выберите **отправить**, а затем **передача файлов** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Меню для отправки файлов][15]
     2. <span data-ttu-id="1e7a7-216">В hello **передачи файлов** диалоговое окно, выберите hello кнопку с многоточием (**...** ) кнопку на правой стороне hello hello **файлы** текстовое поле tooselect hello файлы нужно tooupload.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Параметры отправки файлов][16]
     3. <span data-ttu-id="1e7a7-218">Укажите тип hello **больших двоичных объектов типа**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="1e7a7-219">статья Hello [приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) описываются hello отличия hello различных типов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="1e7a7-220">Дополнительно укажите папку, в которую будут отправлены hello выбранные файлы.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="1e7a7-221">Если hello целевая папка не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="1e7a7-222">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-222">Select **Upload**.</span></span>
   * <span data-ttu-id="1e7a7-223">**Отправить BLOB-контейнере tooa папки**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="1e7a7-224">На hello главной панели инструментов выберите **отправить**, а затем **отправить папку** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Меню для отправки папок][17]
     2. <span data-ttu-id="1e7a7-226">В hello **папки загрузки** диалоговое окно, выберите hello кнопку с многоточием (**...** ) кнопку на правой стороне hello hello **папки** текстовое поле tooselect hello папки, содержимое которой нужно tooupload.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Параметры отправки папок][18]
     3. <span data-ttu-id="1e7a7-228">Укажите тип hello **больших двоичных объектов типа**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="1e7a7-229">статья Hello [приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) описываются hello отличия hello различных типов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="1e7a7-230">Дополнительно укажите папку, в какие hello будет отправлен содержимого выбранной папки.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="1e7a7-231">Если hello целевая папка не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="1e7a7-232">Щелкните **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-232">Select **Upload**.</span></span>
   * <span data-ttu-id="1e7a7-233">**Загрузить большой двоичный объект tooyour локального компьютера**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="1e7a7-234">Выберите hello больших двоичных объектов, нужно toodownload.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="1e7a7-235">На hello главной панели инструментов выберите **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="1e7a7-236">В hello **укажите, куда toosave hello загружен большой двоичный объект** диалогового окна, укажите позицию hello, которую требуется загрузить blob hello и hello имени toogive его.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="1e7a7-237">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-237">Select **Save**.</span></span>
   * <span data-ttu-id="1e7a7-238">**Открытие большого двоичного объекта на локальном компьютере**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="1e7a7-239">Выберите hello больших двоичных объектов, нужно tooopen.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="1e7a7-240">На hello главной панели инструментов выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="1e7a7-241">Hello большого двоичного объекта будут загружены и открыть с помощью приложения hello, связанный с базовым типом файла hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="1e7a7-242">**Скопировать объект буфера обмена toohello больших двоичных объектов**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="1e7a7-243">Выберите hello больших двоичных объектов, нужно toocopy.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="1e7a7-244">На hello главной панели инструментов выберите **копирования**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="1e7a7-245">В левой области hello, перейдите в контейнер больших двоичных объектов tooanother и дважды щелкните его tooview его в основной области hello.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="1e7a7-246">На hello главной панели инструментов выберите **вставить** toocreate копию hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="1e7a7-247">**Удаление большого двоичного объекта**</span><span class="sxs-lookup"><span data-stu-id="1e7a7-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="1e7a7-248">Выберите hello больших двоичных объектов, нужно toodelete.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="1e7a7-249">На hello главной панели инструментов выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="1e7a7-250">Выберите **Да** toohello диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="1e7a7-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e7a7-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e7a7-251">Next steps</span></span>
* <span data-ttu-id="1e7a7-252">Представление hello [последние заметки о выпуске обозреватель хранилищ (Предварительная версия) и видео](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="1e7a7-253">Узнайте, каким образом слишком[создания приложений с помощью Azure BLOB-объектов, таблиц, очередей и файлов](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="1e7a7-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
