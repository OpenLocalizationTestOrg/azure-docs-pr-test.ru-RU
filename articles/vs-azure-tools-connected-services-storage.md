---
title: "aaaAdd хранилища Azure с помощью подключенных служб в Visual Studio | Документы Microsoft"
description: "Добавить приложение tooyour хранилища Azure с помощью диалогового окна Visual Studio Добавление подключенных служб hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="52542-103">Добавление хранилища Azure с использованием подключенных служб Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52542-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="52542-104">С помощью Visual Studio можно подключиться любой из следующих tooAzure хранилища с помощью hello hello **Добавление подключенных служб** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="52542-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="52542-105">облачную службу C#;</span><span class="sxs-lookup"><span data-stu-id="52542-105">C# cloud service</span></span>
- <span data-ttu-id="52542-106">серверную мобильную службу .NET;</span><span class="sxs-lookup"><span data-stu-id="52542-106">.NET backend mobile service</span></span>
- <span data-ttu-id="52542-107">веб-сайт или службу ASP.NET;</span><span class="sxs-lookup"><span data-stu-id="52542-107">ASP.NET website or service</span></span>
- <span data-ttu-id="52542-108">службу ASP.NET Core;</span><span class="sxs-lookup"><span data-stu-id="52542-108">ASP.NET Core service</span></span>
- <span data-ttu-id="52542-109">службу веб-заданий Azure.</span><span class="sxs-lookup"><span data-stu-id="52542-109">Azure WebJob service</span></span> 

<span data-ttu-id="52542-110">Hello подключенной службы функции добавляет все hello необходимые ссылки и проект tooyour кода подключения и соответствующим образом изменяет файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="52542-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="52542-111">После завершения hello **Добавление подключенных служб** автоматически отображает диалоговое окно открытия документации с подробными сведениями о необходимых toostart hello действия работа с хранилище больших двоичных объектов, очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="52542-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="52542-112">Подключения tooAzure хранилища hello подключенных служб с помощью диалогового окна</span><span class="sxs-lookup"><span data-stu-id="52542-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="52542-113">Откройте проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52542-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="52542-114">В **обозреватель решений**, щелкните правой кнопкой мыши hello **подключенные службы** узел и из hello контекстное меню и выберите **добавление подключенной службы**.</span><span class="sxs-lookup"><span data-stu-id="52542-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Добавление подключенной службы Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="52542-116">В hello **подключенные службы** выберите **облачного хранилища с хранилищем Azure**.</span><span class="sxs-lookup"><span data-stu-id="52542-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Добавление учетной записи хранения Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="52542-118">В hello **хранилища Azure** диалоговое окно, выберите существующую учетную запись хранилища и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="52542-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="52542-119">Если вам требуется toocreate учетной записи хранилища, перейдите toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="52542-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="52542-120">В противном случае пропустите toostep 6.</span><span class="sxs-lookup"><span data-stu-id="52542-120">Otherwise, skip toostep 6.</span></span>
    
    ![Добавление существующих tooproject учетной записи хранилища](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="52542-122">toocreate учетную запись хранилища:</span><span class="sxs-lookup"><span data-stu-id="52542-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="52542-123">Выберите **создать новую учетную запись хранения** внизу hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="52542-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="52542-124">Заполните hello **создать учетную запись хранилища** диалогового окна, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="52542-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Новая учетная запись хранения Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="52542-126">Здравствуйте, когда **хранилища Azure** отображается диалоговое окно, hello новой учетной записи хранения отображается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="52542-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="52542-127">Выберите новую учетную запись хранения hello hello списка и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="52542-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="52542-128">Здравствуйте, подключенная служба хранилища отображается под hello **ссылки на службу** узле проекта.</span><span class="sxs-lookup"><span data-stu-id="52542-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="52542-129">Какие изменения произойдут в проекте</span><span class="sxs-lookup"><span data-stu-id="52542-129">How your project is modified</span></span>
<span data-ttu-id="52542-130">Завершив диалоговое окно приветствия, Visual Studio добавляет ссылки и изменяет определенные файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="52542-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="52542-131">Hello конкретные изменения зависят от типа проекта hello:</span><span class="sxs-lookup"><span data-stu-id="52542-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="52542-132">Проекты ASP.NET: ознакомьтесь со статьей [Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)](http://go.microsoft.com/fwlink/p/?LinkId=513126).</span><span class="sxs-lookup"><span data-stu-id="52542-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="52542-133">Проекты ASP.NET Core: ознакомьтесь со статьей [Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (ASP.NET 5)](http://go.microsoft.com/fwlink/p/?LinkId=513124).</span><span class="sxs-lookup"><span data-stu-id="52542-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="52542-134">Проекты облачной службы (веб-роли и рабочие роли): ознакомьтесь со статьей [Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (проектами облачных служб)](http://go.microsoft.com/fwlink/p/?LinkId=516965).</span><span class="sxs-lookup"><span data-stu-id="52542-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="52542-135">Проекты веб-заданий: ознакомьтесь со статьей [Что произошло с моим проектом веб-заданий (подключенными к службе хранилища Azure службами Visual Studio)?](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="52542-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="52542-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52542-136">Next steps</span></span>
- [<span data-ttu-id="52542-137">Форум MSDN: хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="52542-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="52542-138">Блог команды разработчиков службы хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="52542-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="52542-139">Документация по службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="52542-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
