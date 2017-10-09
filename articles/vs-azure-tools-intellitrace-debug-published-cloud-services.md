---
title: "aaaDebugging, опубликованных в Azure облачной службы в Visual Studio и IntelliTrace | Документы Microsoft"
description: "Узнайте, как toodebug облачной службы в Visual Studio и IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="27236-103">Отладка опубликованной облачной службы Azure с помощью Visual Studio и IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="27236-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="27236-104">С помощью IntelliTrace можно записывать в журнал расширенные отладочные сведения для экземпляра роли при его запуске в Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="27236-105">При необходимости toofind hello причину проблемы, можно использовать toostep журналы IntelliTrace hello по коду из Visual Studio, как если бы оно было запущено в Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="27236-106">По сути записей код клавиши выполнения и среде данные IntelliTrace при приложение Azure работает как облачной службы в Azure, а также позволяет воспроизвести hello записанные данные в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27236-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="27236-107">IntelliTrace можно использовать, если ваше приложение Azure предназначено для .NET Framework 4 или более поздней версии и если у вас установлена среда разработки Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="27236-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="27236-108">IntelliTrace собирает сведения для ваших ролей Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="27236-109">Hello виртуальных машин для этих ролей всегда запускать 64-разрядных операционных системах.</span><span class="sxs-lookup"><span data-stu-id="27236-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="27236-110">В качестве альтернативы можно использовать [удаленной отладки](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach непосредственно tooa облачной службе, запущенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27236-111">IntelliTrace предназначена только для отладки и не должна использоваться в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="27236-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="27236-112">Настройка приложения Azure для IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="27236-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="27236-113">tooenable IntelliTrace для приложения Azure необходимо создать и опубликовать приложение hello из проекта Visual Studio Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="27236-114">Перед публикацией tooAzure, необходимо настроить IntelliTrace для приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="27236-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="27236-115">Если опубликовать приложение без настройки IntelliTrace, необходимо toorepublish hello проекта.</span><span class="sxs-lookup"><span data-stu-id="27236-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="27236-116">Дополнительные сведения см. в статье [Публикация облачной службы с помощью инструментов Azure](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="27236-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="27236-117">Когда вы будете готовы toodeploy приложения Azure, убедитесь, что целевых объектов построения задано слишком**отладки**.</span><span class="sxs-lookup"><span data-stu-id="27236-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="27236-118">В **обозревателе решений**, щелкните правой кнопкой мыши проект и hello контекстном меню, выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="27236-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="27236-119">В hello **публикации приложения Azure** диалоговое окно, выберите hello подписки Azure и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="27236-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="27236-120">В hello **параметры** страницу, выберите hello **Дополнительные параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="27236-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="27236-121">Включите hello **включить IntelliTrace** параметр toocollect журналы IntelliTrace для приложения после его публикации в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="27236-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="27236-122">toocustomize hello основную конфигурацию IntelliTrace, выберите **параметры** Далее слишком**включить IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="27236-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Ссылка на "Параметры IntelliTrace"](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="27236-124">В hello **параметры IntelliTrace** диалоговое окно, можно указать какие события toolog, ли toocollect сведений о вызовах, какие toocollect модулей и процессов в журналах и о том, сколько места tooallocate toohello записи.</span><span class="sxs-lookup"><span data-stu-id="27236-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="27236-125">Дополнительные сведения об IntelliTrace см. в разделе [Отладка с помощью IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="27236-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Параметры IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="27236-127">Журнал IntelliTrace Hello представляет собой кольцевой файл журнала hello максимальный размер, указанный в параметрах IntelliTrace hello (размер по умолчанию hello составляет 250 МБ).</span><span class="sxs-lookup"><span data-stu-id="27236-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="27236-128">Журналы IntelliTrace, собранные tooa файл в файловой системе hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="27236-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="27236-129">Когда вы запрашиваете журналы hello, моментальный снимок берется на момент времени и загрузить tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="27236-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="27236-130">После hello облачной службы Azure опубликованных tooAzure, можно определить, включен ли IntelliTrace из hello Azure узла в **обозревателя серверов**, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="27236-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Обозреватель сервера: IntelliTrace включен](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="27236-132">Скачивание журналов IntelliTrace для экземпляра роли</span><span class="sxs-lookup"><span data-stu-id="27236-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="27236-133">С помощью Visual Studio можно скачать журналы IntelliTrace для экземпляра роли, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="27236-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="27236-134">В **обозревателя серверов**, разверните hello **облачные службы** узел и найдите экземпляр роли, журналы которых нужно toodownload.</span><span class="sxs-lookup"><span data-stu-id="27236-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="27236-135">Щелкните правой кнопкой мыши экземпляр роли hello и hello s контекстном меню, выберите **Просмотр журналов IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="27236-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Пункт меню "Просмотр журналов IntelliTrace"](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="27236-137">журналы IntelliTrace Hello являются tooa загруженного файла в каталоге на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="27236-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="27236-138">При каждом запросе журналов IntelliTrace hello, создается новый моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="27236-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="27236-139">Во время загрузки журналов hello, Visual Studio отображает ход выполнения операции hello hello в hello **журнал действий Azure** окна.</span><span class="sxs-lookup"><span data-stu-id="27236-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="27236-140">Как показано на следующий рисунок hello, можно развернуть элемент строку hello для hello операции toosee более подробно.</span><span class="sxs-lookup"><span data-stu-id="27236-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="27236-142">Вы можете продолжить toowork в Visual Studio во время загрузки журналов IntelliTrace hello.</span><span class="sxs-lookup"><span data-stu-id="27236-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="27236-143">После завершения загрузки журнала hello он открывается в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27236-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="27236-144">Hello журналы IntelliTrace могут содержать исключения, платформа hello создает и обрабатывает позже.</span><span class="sxs-lookup"><span data-stu-id="27236-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="27236-145">Эти исключения формируются внутренним кодом платформы при обычном запуске роли, поэтому на них можно не обращать внимания.</span><span class="sxs-lookup"><span data-stu-id="27236-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27236-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27236-146">Next steps</span></span>
- [<span data-ttu-id="27236-147">Параметры отладки облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="27236-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="27236-148">Публикация облачной службы с помощью инструментов Azure</span><span class="sxs-lookup"><span data-stu-id="27236-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)