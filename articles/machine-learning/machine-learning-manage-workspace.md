---
title: "Управление рабочей областью в службе машинного обучения | Документация Майкрософт"
description: "Управление доступом к рабочим областям Машинного обучения Azure, а также развертывание веб-служб API ML и управление ими"
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
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="d6fc4-103">Управление рабочей областью машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="d6fc4-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="d6fc4-104">Сведения об управлении веб-службами на портале веб-служб машинного обучения см. в разделе [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="d6fc4-105">Рабочими областями машинного обучения можно управлять с помощью портала Azure или классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="d6fc4-106">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="d6fc4-106">Use the Azure portal</span></span>

<span data-ttu-id="d6fc4-107">Вот как можно управлять рабочей областью на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="d6fc4-108">Войдите на [портал Azure](https://portal.azure.com/), используя учетную запись администратора подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="d6fc4-109">В поле поиска в верхней части страницы введите "machine learning workspaces" и выберите **Machine Learning Workspaces** (Рабочие области машинного обучения).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="d6fc4-110">Щелкните рабочую область, которой нужно управлять.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="d6fc4-111">Помимо стандартной информации об управлении ресурсами и параметров вам доступны следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="d6fc4-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="d6fc4-112">Страница **Свойства**. На ней отображаются сведения о рабочей области и ресурсах. Кроме того, на этой странице можно изменить подписку и группу ресурсов, с которым и связана эта рабочая область.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="d6fc4-113">**Повторная синхронизация ключей хранилища**. Рабочая область хранит ключи в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="d6fc4-114">Если учетная запись хранения изменила ключи, то можно щелкнуть **Повторно синхронизировать ключи**, чтобы синхронизировать ключи с рабочей областью.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="d6fc4-115">Для управления веб-службами, связанными с этой рабочей областью, используйте портал веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="d6fc4-116">Полные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="d6fc4-117">Для развертывания новых веб-служб или управления ими необходимо назначить роль участника или администратора той подписке, в которую развертывается веб-служба.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="d6fc4-118">Чтобы пригласить в рабочую область машинного обучения других пользователей, необходимо назначить им роли участников или администраторов подписки, чтобы они могли развертывать веб-службы или управлять ими.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="d6fc4-119">Дополнительные сведения о настройке прав доступа см. в статье [Просмотр назначенных прав доступа для пользователей и групп на портале Azure (общедоступная предварительная версия)](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="d6fc4-120">Использование классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="d6fc4-120">Use the Azure classic portal</span></span>

<span data-ttu-id="d6fc4-121">С помощью классического портала Azure можно управлять рабочими областями машинного обучения для следующего:</span><span class="sxs-lookup"><span data-stu-id="d6fc4-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="d6fc4-122">мониторинга использования рабочей области;</span><span class="sxs-lookup"><span data-stu-id="d6fc4-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="d6fc4-123">настройки рабочей области для предоставления или запрета доступа к ней;</span><span class="sxs-lookup"><span data-stu-id="d6fc4-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="d6fc4-124">управления веб-службами, созданными в рабочей области;</span><span class="sxs-lookup"><span data-stu-id="d6fc4-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="d6fc4-125">удаления рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-125">Delete the workspace</span></span>

<span data-ttu-id="d6fc4-126">Кроме того, вкладка панели мониторинга предоставляет общую информацию об использовании рабочей области и позволяет просмотреть сводку данных о ней.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="d6fc4-127">В студии машинного обучения Azure на вкладке **Веб-службы** можно добавлять, обновлять или удалять веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="d6fc4-128">Вот как можно управлять рабочей областью на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="d6fc4-129">Войдите в учетную запись Microsoft Azure на [классическом порталe Azure](https://manage.windowsazure.com/) (используйте учетную запись, связанную с подпиской Azure).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="d6fc4-130">На панели служб Microsoft Azure выберите **МАШИННОЕ ОБУЧЕНИЕ**.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="d6fc4-131">Щелкните рабочую область, которой нужно управлять.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="d6fc4-132">На странице рабочей области содержится три вкладки:</span><span class="sxs-lookup"><span data-stu-id="d6fc4-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="d6fc4-133">**ПАНЕЛЬ МОНИТОРИНГА** — позволяет просматривать данные об использовании рабочей области и информацию о ней;</span><span class="sxs-lookup"><span data-stu-id="d6fc4-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="d6fc4-134">**НАСТРОЙКА** — позволяет управлять доступом к рабочей области;</span><span class="sxs-lookup"><span data-stu-id="d6fc4-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="d6fc4-135">**Веб-службы** — позволяет управлять веб-службами, опубликованными из этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="d6fc4-136">Мониторинг использования рабочей области</span><span class="sxs-lookup"><span data-stu-id="d6fc4-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="d6fc4-137">Щелкните вкладку **ПАНЕЛЬ МОНИТОРИНГА** .</span><span class="sxs-lookup"><span data-stu-id="d6fc4-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="d6fc4-138">На панели мониторинга можно просмотреть данные общего использования рабочей области и сводку информации о ней.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="d6fc4-139">На диаграмме **Вычисления** отображаются вычислительные ресурсы, которые использует рабочая область.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="d6fc4-140">Вы можете изменить представление для отображения относительных или абсолютных величин. Кроме того, можно изменить промежуток времени, отображаемый на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="d6fc4-141">**Обзор использования** отображает данные службы хранилища Azure, которое использует рабочая область.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="d6fc4-142">**Сводка** предоставляет сведенную информацию о рабочей области и полезные ссылки.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="d6fc4-143">Ссылка **Войти в студию машинного обучения** позволяет открыть Студию машинного обучения Microsoft Azure, используя учетную запись Майкрософт, в которою вы вошли.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="d6fc4-144">Для учетной записи Майкрософт, использованной для входа на классический портал Azure для создания рабочей области, не предусмотрено автоматическое предоставление разрешений на открытие этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="d6fc4-145">Чтобы открыть рабочую область, необходимо войти в учетную запись Майкрософт, определенную в качестве учетной записи владельца рабочей области, или получить приглашение присоединиться к рабочей области от владельца.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="d6fc4-146">Предоставление или приостановка доступа для пользователей</span><span class="sxs-lookup"><span data-stu-id="d6fc4-146">To grant or suspend access for users</span></span>
<span data-ttu-id="d6fc4-147">Выберите вкладку **НАСТРОЙКА** .</span><span class="sxs-lookup"><span data-stu-id="d6fc4-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="d6fc4-148">На вкладке конфигурации можно:</span><span class="sxs-lookup"><span data-stu-id="d6fc4-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="d6fc4-149">Приостановить доступ к рабочей области машинного обучения, щелкнув «ОТКЛОНИТЬ».</span><span class="sxs-lookup"><span data-stu-id="d6fc4-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="d6fc4-150">Пользователи больше не смогут открыть рабочую область в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="d6fc4-151">Чтобы восстановить доступ, щелкните «РАЗРЕШИТЬ».</span><span class="sxs-lookup"><span data-stu-id="d6fc4-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="d6fc4-152">Чтобы управлять дополнительными учетными записями с доступом к рабочей области в Студии машинного обучения, нажмите **Войти в Студию машинного обучения** на вкладке **Панель мониторинга** (см. приведенное выше примечание о ссылке **Войти в студию машинного обучения**).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="d6fc4-153">Рабочая область откроется в Студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="d6fc4-154">Здесь щелкните вкладку **Параметры**, а затем — **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="d6fc4-155">Вы можете щелкнуть **Пригласить больше пользователей**, чтобы предоставить пользователям доступ к рабочей области, или выбрать пользователя и щелкнуть **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="d6fc4-156">Управление веб-службами в рабочей области</span><span class="sxs-lookup"><span data-stu-id="d6fc4-156">To manage web services in this workspace</span></span>
<span data-ttu-id="d6fc4-157">Щелкните вкладку **ВЕБ-СЛУЖБЫ** .</span><span class="sxs-lookup"><span data-stu-id="d6fc4-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="d6fc4-158">Отобразится список веб-служб, опубликованных из этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="d6fc4-159">Для управления веб-службами щелкните соответствующее имя в списке, чтобы открыть страницу веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="d6fc4-160">Для веб-службы может быть определена одна или несколько конечных точек.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="d6fc4-161">Кроме конечной точки «По умолчанию», вы можете определить дополнительные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="d6fc4-162">Чтобы добавить конечную точку, щелкните **Управление конечными точками** в нижней части панели мониторинга для открытия портала веб-служб машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="d6fc4-163">Чтобы удалить конечную точку (конечную точку по умолчанию нельзя удалить), щелкните флажок в начале строки конечной точки, а затем нажмите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="d6fc4-164">Это удалит конечную точку из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d6fc4-165">Если приложение использует конечную точку веб-службы, а конечная точка удалена, при следующей попытке получить доступ к службе в приложении отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="d6fc4-166">Чтобы открыть конечную точку веб-службы, щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="d6fc4-167">На панели мониторинга можно просмотреть общие сведения об использовании веб-службы за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="d6fc4-168">Период для отображения можно выбрать с помощью раскрывающегося меню "Period" (Период) в правом верхнем углу диаграммы использования.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="d6fc4-169">На панели мониторинга отображаются следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="d6fc4-170">**Requests Over Time** (Запросы за период времени): отображает ступенчатую диаграмму с количеством запросов за выбранный период времени.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="d6fc4-171">Помогает выявить всплески в использовании веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="d6fc4-172">**Request-Response Requests** (Вызовы "запрос-ответ"): отображает общее число вызовов "запрос-ответ", которые служба получила за выбранный период времени, а также сколько из них было неудавшихся.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="d6fc4-173">**Average Request-Response Compute Time** (Среднее время вычисления "запрос-ответ"): отображает среднее время, необходимое для обработки полученных запросов.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="d6fc4-174">**Batch Requests** (Пакетные запросы): отображает общее число пакетных запросов, которые служба получила за выбранный период времени, а также сколько из них было неудавшихся.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="d6fc4-175">**Average Job Latency** (Средняя задержка задания): отображает среднее время, необходимое для обработки полученных запросов.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="d6fc4-176">**Errors** (Ошибки): отображает общее число ошибок, произошедших при вызовах к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="d6fc4-177">**Services Costs** (Затраты на службу): отображает сведения о затратах согласно плану выставления счетов, связанному с данной службой.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="d6fc4-178">На странице конфигурации можно обновить следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="d6fc4-179">**Description** (Описание): позволяет ввести описание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="d6fc4-180">Описание является обязательным полем.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-180">Description is a required field.</span></span>
* <span data-ttu-id="d6fc4-181">**Logging** (Ведение журнала): позволяет включить или отключить ведение журнала ошибок на конечной точке.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="d6fc4-182">Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обученияя](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="d6fc4-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="d6fc4-183">**Enable Sample data** (Включить образцы данных): позволяет добавлять образцы данных, которые можно использовать для тестирования службы "запрос — ответ".</span><span class="sxs-lookup"><span data-stu-id="d6fc4-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="d6fc4-184">Если вы создали веб-службу в Студии машинного обучения, то образец данных берется из данных, с помощью которых вы обучали модель.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="d6fc4-185">Если служба создана программным путем, то данные берутся из данных примеров, которые вы предоставили в составе пакета JSON.</span><span class="sxs-lookup"><span data-stu-id="d6fc4-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

