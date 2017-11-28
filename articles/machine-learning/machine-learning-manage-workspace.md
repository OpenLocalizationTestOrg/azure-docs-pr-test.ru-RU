---
title: "aaaManage рабочей области машинного обучения | Документы Microsoft"
description: "Рабочие области машинного обучения tooAzure доступа, развертывание и управление веб-службы API машинного Обучения"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="49e29-103">Управление рабочей областью машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="49e29-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="49e29-104">Сведения об управлении веб-службы на портале веб-службы обучения машины hello. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="49e29-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="49e29-105">Можно управлять рабочих областей машинного обучения в любом hello портал Azure или hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="49e29-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="49e29-106">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="49e29-106">Use hello Azure portal</span></span>

<span data-ttu-id="49e29-107">toomanage рабочей hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="49e29-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="49e29-108">Войдите в toohello [портал Azure](https://portal.azure.com/) с учетной записью администратора подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="49e29-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="49e29-109">В поле поиска hello вверху hello страницы приветствия, введите «машинного обучения рабочие области» и выберите **рабочие области обучения машинного**.</span><span class="sxs-lookup"><span data-stu-id="49e29-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="49e29-110">Щелкните рабочую область hello требуется toomanage.</span><span class="sxs-lookup"><span data-stu-id="49e29-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="49e29-111">В дополнение к этому toohello стандартные управления сведениями о ресурсах и доступные параметры, можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="49e29-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="49e29-112">Представление **свойства** — на этой странице отображаются сведения о рабочей области и ресурсах hello, и вы можете изменить подписку hello и группы ресурсов, связанный с этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="49e29-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="49e29-113">**Повторная синхронизация ключей хранилища** -hello рабочая область поддерживает ключи учетной записи хранилища toohello.</span><span class="sxs-lookup"><span data-stu-id="49e29-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="49e29-114">Если учетная запись хранения hello изменений ключи, то можно щелкнуть **Resync ключей** toosynchronize hello ключи с рабочей областью hello.</span><span class="sxs-lookup"><span data-stu-id="49e29-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="49e29-115">toomanage hello веб-служб, связанных с этой рабочей области с помощью портала hello машины обучения веб-служб.</span><span class="sxs-lookup"><span data-stu-id="49e29-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="49e29-116">В разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md) полные сведения.</span><span class="sxs-lookup"><span data-stu-id="49e29-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="49e29-117">toodeploy или управлять новый веб-служб, пользователь должен иметь роль участника или развертывании роли администратора hello подписки toowhich hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="49e29-118">Если вы пригласить другого пользователя tooa рабочей области машинного обучения, необходимо назначить их tooa участника или администратора в подписке hello для развертывания и управления веб-службами.</span><span class="sxs-lookup"><span data-stu-id="49e29-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="49e29-119">Дополнительные сведения о задании разрешений доступа см. в разделе [Просмотр назначений доступ для пользователей и групп в hello портал Azure — общедоступная Предварительная версия](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="49e29-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="49e29-120">Hello используйте классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="49e29-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="49e29-121">Hello классического портала Azure вы можете управлять рабочими областями машинного обучения для:</span><span class="sxs-lookup"><span data-stu-id="49e29-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="49e29-122">Отслеживать использование hello рабочей области</span><span class="sxs-lookup"><span data-stu-id="49e29-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="49e29-123">Настройка рабочей области tooallow hello или отказ в доступе</span><span class="sxs-lookup"><span data-stu-id="49e29-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="49e29-124">Управление веб-службы, созданные в рабочей области hello</span><span class="sxs-lookup"><span data-stu-id="49e29-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="49e29-125">Удалить рабочую область hello</span><span class="sxs-lookup"><span data-stu-id="49e29-125">Delete hello workspace</span></span>

<span data-ttu-id="49e29-126">Кроме того вкладка сводки hello предоставляет обзор использования рабочей области и быстрый обзор рабочей области данных.</span><span class="sxs-lookup"><span data-stu-id="49e29-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="49e29-127">В студии машинного обучения Azure, на hello **веб-службы** вкладки, существует возможность добавления, обновления или удаления веб-машины обучения службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="49e29-128">toomanage рабочей hello классического портала Azure:</span><span class="sxs-lookup"><span data-stu-id="49e29-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="49e29-129">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) Microsoft Azure с помощью учетной записи — используйте hello учетной записи, связанной с hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="49e29-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="49e29-130">На панели служб Microsoft Azure hello щелкните **МАШИННОГО ОБУЧЕНИЯ**.</span><span class="sxs-lookup"><span data-stu-id="49e29-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="49e29-131">Щелкните рабочую область hello требуется toomanage.</span><span class="sxs-lookup"><span data-stu-id="49e29-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="49e29-132">Страница приветствия рабочей области содержит три вкладки:</span><span class="sxs-lookup"><span data-stu-id="49e29-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="49e29-133">**Панель МОНИТОРИНГА** -позволяет tooview использование рабочей области, а также сведения</span><span class="sxs-lookup"><span data-stu-id="49e29-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="49e29-134">**Настройка** -позволяет рабочей toohello toomanage доступа</span><span class="sxs-lookup"><span data-stu-id="49e29-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="49e29-135">**Веб-службы** -позволяет toomanage веб-служб, которые были опубликованы из этой рабочей области</span><span class="sxs-lookup"><span data-stu-id="49e29-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="49e29-136">Использование рабочей области hello toomonitor</span><span class="sxs-lookup"><span data-stu-id="49e29-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="49e29-137">Нажмите кнопку hello **МОНИТОРИНГА** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49e29-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="49e29-138">С панели мониторинга hello можно просмотреть общее использование рабочей области и получить быстрый обзор рабочей области сведений.</span><span class="sxs-lookup"><span data-stu-id="49e29-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="49e29-139">Hello **ВЫЧИСЛЕНИЙ** диаграмма отображает hello вычислительные ресурсы, используемые hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="49e29-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="49e29-140">Hello представление toodisplay относительные или абсолютные значения можно изменить, и можно изменить период hello, отображаемый на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="49e29-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="49e29-141">**Общие сведения об использовании** отображает хранилища Azure, используемый hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="49e29-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="49e29-142">**Сводка** предоставляет сведенную информацию о рабочей области и полезные ссылки.</span><span class="sxs-lookup"><span data-stu-id="49e29-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="49e29-143">Hello **входа tooML Studio** ссылке открывается студия машинного обучения с помощью hello в данный момент вы вошли в учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="49e29-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="49e29-144">Hello использовать toosign в toohello Azure классического портала toocreate рабочую учетную запись Майкрософт не поддерживает автоматически tooopen разрешение этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="49e29-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="49e29-145">tooopen рабочую область, необходимо войти в учетную запись Майкрософт, который был определен как hello владельца рабочей области hello toohello или tooreceive приглашение от toojoin hello hello владельца рабочей, необходимо установить.</span><span class="sxs-lookup"><span data-stu-id="49e29-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="49e29-146">toogrant или приостановить доступ для пользователей</span><span class="sxs-lookup"><span data-stu-id="49e29-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="49e29-147">Нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49e29-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="49e29-148">На вкладке настройки hello можно:</span><span class="sxs-lookup"><span data-stu-id="49e29-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="49e29-149">Приостановка доступа к рабочей области машинного обучения toohello, щелкнув DENY.</span><span class="sxs-lookup"><span data-stu-id="49e29-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="49e29-150">Пользователи больше не будет возможности tooopen рабочей hello в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="49e29-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="49e29-151">toorestore доступ, нажмите "Разрешить".</span><span class="sxs-lookup"><span data-stu-id="49e29-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="49e29-152">toomanage дополнительные учетные записи, обладающие рабочей toohello доступ в студии машинного обучения, нажмите кнопку **входа tooML Studio** в hello **МОНИТОРИНГА** вкладка (см. Примечание предшествующих hello в отношении  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="49e29-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="49e29-153">Откроется рабочая область hello в студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="49e29-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="49e29-154">Здесь щелкните hello **параметры** tab и затем **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="49e29-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="49e29-155">Можно щелкнуть **ПРИГЛАШЕНИЯ более пользователей** toogive пользователям доступ к рабочей области toohello, или выберите пользователя и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="49e29-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="49e29-156">toomanage веб-служб в этой рабочей области</span><span class="sxs-lookup"><span data-stu-id="49e29-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="49e29-157">Нажмите кнопку hello **веб-службы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="49e29-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="49e29-158">Отобразится список веб-служб, опубликованных из этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="49e29-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="49e29-159">toomanage веб-службы, щелкните имя hello в страницу приветствия список tooopen hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="49e29-160">Для веб-службы может быть определена одна или несколько конечных точек.</span><span class="sxs-lookup"><span data-stu-id="49e29-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="49e29-161">Можно определить несколько конечных точек в конечной точке сложения toohello «Default».</span><span class="sxs-lookup"><span data-stu-id="49e29-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="49e29-162">tooadd Здравствуйте конечной точки, нажмите кнопку **Управление конечными точками** внизу hello hello мониторинга tooopen hello веб-службы Azure Machine Learning портала.</span><span class="sxs-lookup"><span data-stu-id="49e29-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="49e29-163">toodelete конечной точки (нельзя удалить конечную точку «Default» hello), установите флажок hello в начале hello строку hello конечной точки и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="49e29-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="49e29-164">Эта функция удаляет hello конечной точки из hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="49e29-165">Если приложение использует hello конечной веб-службы при удалении конечной точки hello, приложение hello получат hello ошибка следующей предпринимается tooaccess hello службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="49e29-166">Щелкните имя hello tooopen конечной точки службы Web его.</span><span class="sxs-lookup"><span data-stu-id="49e29-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="49e29-167">С панели мониторинга hello можно просмотреть общее использование веб-службы за период времени.</span><span class="sxs-lookup"><span data-stu-id="49e29-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="49e29-168">Можно выбрать tooview периода hello hello периода раскрывающемся меню в правом верхнем углу hello hello использование диаграмм.</span><span class="sxs-lookup"><span data-stu-id="49e29-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="49e29-169">Hello панели мониторинга отображаются hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="49e29-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="49e29-170">**Запросы в динамике** отображается график шаг hello числа запросов за выбранный период времени hello.</span><span class="sxs-lookup"><span data-stu-id="49e29-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="49e29-171">Помогает выявить всплески в использовании веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="49e29-172">**Запрос-ответ запросов** отображает hello общее число вызовов запрос-ответ, полученных службой hello hello выбранного периода времени и сколько из них сбой.</span><span class="sxs-lookup"><span data-stu-id="49e29-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="49e29-173">**Среднее время вычислений запрос-ответ** отображает среднее время hello необходимости tooexecute hello полученных запросов.</span><span class="sxs-lookup"><span data-stu-id="49e29-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="49e29-174">**Пакетных запросов** отображает hello общее количество пакетных запросов службы hello получил за выбранный период времени hello и сколько из них сбой.</span><span class="sxs-lookup"><span data-stu-id="49e29-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="49e29-175">**Среднее время задержки задания** отображает среднее время hello необходимости tooexecute hello полученных запросов.</span><span class="sxs-lookup"><span data-stu-id="49e29-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="49e29-176">**Ошибки** отображает hello статистической обработки числа ошибок, произошедших на вызовы toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="49e29-177">**Стоимость служб** отображает hello плата за план выставления счетов hello, связанная со службой hello.</span><span class="sxs-lookup"><span data-stu-id="49e29-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="49e29-178">Из страницу "Настройка" hello можно обновить hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="49e29-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="49e29-179">**Описание** позволяет tooenter описание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="49e29-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="49e29-180">Описание является обязательным полем.</span><span class="sxs-lookup"><span data-stu-id="49e29-180">Description is a required field.</span></span>
* <span data-ttu-id="49e29-181">**Ведение журнала** позволяет tooenable или отключить ведение журнала на конечной точке hello ошибок.</span><span class="sxs-lookup"><span data-stu-id="49e29-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="49e29-182">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обученияя](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="49e29-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="49e29-183">**Разрешить демонстрационные данные** позволяет tooprovide образцы данных, можно воспользоваться службой tootest hello запроса-ответа.</span><span class="sxs-lookup"><span data-stu-id="49e29-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="49e29-184">При создании веб-службу hello в студии машинного обучения hello образец данных берется из данных hello вашей используется tootrain модели.</span><span class="sxs-lookup"><span data-stu-id="49e29-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="49e29-185">При программном создании службы hello hello данных берется из данных пример hello, предоставленные как часть пакета JSON hello.</span><span class="sxs-lookup"><span data-stu-id="49e29-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

