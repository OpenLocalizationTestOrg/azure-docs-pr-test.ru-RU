---
title: "как toomanage AzureML web services с помощью API управления aaaLearn | Документы Microsoft"
description: "Руководство, показывающий, как toomanage AzureML web services с помощью API управления."
keywords: "машинное обучение, управление api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="d13ca-104">Узнайте, как toomanage AzureML web services с помощью API-Интерфейс управления</span><span class="sxs-lookup"><span data-stu-id="d13ca-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="d13ca-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d13ca-105">Overview</span></span>
<span data-ttu-id="d13ca-106">В этом руководстве показано, как tooquickly приступить к работе с API управления toomanage AzureML веб-служб.</span><span class="sxs-lookup"><span data-stu-id="d13ca-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="d13ca-107">Что собой представляет управление Azure API</span><span class="sxs-lookup"><span data-stu-id="d13ca-107">What is Azure API Management?</span></span>
<span data-ttu-id="d13ca-108">Управление API Azure — это служба Azure, которая позволяет управлять конечными точками REST API, настраивая доступ пользователей, регулирование использования и мониторинг панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d13ca-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="d13ca-109">Сведения об управлении API Azure см. [здесь](https://azure.microsoft.com/services/api-management/).</span><span class="sxs-lookup"><span data-stu-id="d13ca-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="d13ca-110">Нажмите кнопку [здесь](../api-management/api-management-get-started.md) руководство о том, как tooget работы с API управления Azure.</span><span class="sxs-lookup"><span data-stu-id="d13ca-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="d13ca-111">Это руководство, на котором основана данная статья, содержит больше разделов, включая информацию о конфигурациях оборудования, ценовых категориях, обработке ответов, проверке подлинности пользователей, создании продуктов, подписках разработчика и компактном отображении данных об использовании.</span><span class="sxs-lookup"><span data-stu-id="d13ca-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="d13ca-112">Что такое AzureML</span><span class="sxs-lookup"><span data-stu-id="d13ca-112">What is AzureML?</span></span>
<span data-ttu-id="d13ca-113">AzureML — это служба Azure, для машинного обучения, которая позволяет tooeasily построения, развертывания и совместно использовать решениями углубленной аналитики.</span><span class="sxs-lookup"><span data-stu-id="d13ca-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="d13ca-114">Сведения о службе AzureML см. [здесь](https://azure.microsoft.com/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="d13ca-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d13ca-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d13ca-115">Prerequisites</span></span>
<span data-ttu-id="d13ca-116">toocomplete этого руководства требуется:</span><span class="sxs-lookup"><span data-stu-id="d13ca-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="d13ca-117">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d13ca-117">An Azure account.</span></span> <span data-ttu-id="d13ca-118">Если у вас нет учетной записи Azure, щелкните [здесь](https://azure.microsoft.com/pricing/free-trial/) подробные сведения о том, как toocreate бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d13ca-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="d13ca-119">Учетная запись AzureML.</span><span class="sxs-lookup"><span data-stu-id="d13ca-119">An AzureML account.</span></span> <span data-ttu-id="d13ca-120">Если нет AzureML учетную запись, нажмите кнопку [здесь](https://studio.azureml.net/) подробные сведения о том, как toocreate бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d13ca-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="d13ca-121">Рабочая область Hello, службы и api_key для эксперимента машинного обучения Azure, развернутые как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="d13ca-122">Нажмите кнопку [здесь](machine-learning-create-experiment.md) сведения о как поэкспериментировать toocreate AzureML.</span><span class="sxs-lookup"><span data-stu-id="d13ca-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="d13ca-123">Нажмите кнопку [здесь](machine-learning-publish-a-machine-learning-web-service.md) сведения о как toodeploy AzureML поэкспериментировать веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="d13ca-124">Кроме того приложение A имеет инструкции toocreate и тестирования простых AzureML поэкспериментировать и развернуть его как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="d13ca-125">Создание экземпляра API Management</span><span class="sxs-lookup"><span data-stu-id="d13ca-125">Create an API Management instance</span></span>
<span data-ttu-id="d13ca-126">Ниже приведены шаги использования API управления toomanage hello веб-службу машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d13ca-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="d13ca-127">Сначала создайте экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-127">First create a service instance.</span></span> <span data-ttu-id="d13ca-128">Войдите в toohello [классический портал](https://manage.windowsazure.com/) и нажмите кнопку **New** > **службы приложений** > **управления API**  >  **Создания**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="d13ca-130">Укажите уникальное значение в поле **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-130">Specify a unique **URL**.</span></span> <span data-ttu-id="d13ca-131">В этом руководстве используется **demoazureml** — вам потребуется toochoose другим.</span><span class="sxs-lookup"><span data-stu-id="d13ca-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="d13ca-132">Выберите требуемого hello **подписки** и **область** для вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="d13ca-133">После выделения нужных элементов, нажмите кнопку "Далее" hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="d13ca-135">Укажите значение для hello **название организации**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="d13ca-136">В этом руководстве используется **demoazureml** — вам потребуется toochoose другим.</span><span class="sxs-lookup"><span data-stu-id="d13ca-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="d13ca-137">Введите адрес электронной почты в hello **адрес электронной почты администратора** поля.</span><span class="sxs-lookup"><span data-stu-id="d13ca-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="d13ca-138">Этот адрес электронной почты используется для получения уведомлений из системы управления API hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="d13ca-140">Щелкните флажок toocreate hello вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="d13ca-141">*Он занимает toothirty минут для новой службы toobe создан*.</span><span class="sxs-lookup"><span data-stu-id="d13ca-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="d13ca-142">Создать hello API</span><span class="sxs-lookup"><span data-stu-id="d13ca-142">Create hello API</span></span>
<span data-ttu-id="d13ca-143">После создания экземпляра службы hello hello следующим шагом является toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="d13ca-144">API представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="d13ca-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="d13ca-145">Операции API-интерфейса — tooexisting через прокси веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="d13ca-146">В этом руководстве создает интерфейсы API, toohello прокси существующих записей Ресурсов AzureML и BES веб-служб.</span><span class="sxs-lookup"><span data-stu-id="d13ca-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="d13ca-147">API-интерфейсы создаются и настраиваются с портала издателя hello API, который можно получить с помощью hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d13ca-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="d13ca-148">tooreach hello портала, выберите издателя вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="d13ca-150">Нажмите кнопку **управление** в hello классический портал Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="d13ca-152">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **добавить API**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="d13ca-154">Тип **AzureML демонстрация API** как hello **имя веб-API**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="d13ca-155">Тип **https://ussouthcentral.services.azureml.net** как hello **веб-URL-адрес службы**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="d13ca-156">Тип **azureml Демонстрация** как hello **суффикс URL-адрес API**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="d13ca-157">Проверьте **HTTPS** как hello **URL-адрес API** схемы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="d13ca-158">Выберите **Starter** (Начальный комплект) в поле **Продукты**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="d13ca-159">По завершении нажмите кнопку **Сохранить** toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="d13ca-161">Добавьте операции hello</span><span class="sxs-lookup"><span data-stu-id="d13ca-161">Add hello operations</span></span>
<span data-ttu-id="d13ca-162">Нажмите кнопку **операция добавления** toothis tooadd операции API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="d13ca-164">Hello **новую операцию** окна будут отображены и hello **подписи** вкладка будет выбран по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d13ca-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="d13ca-165">Добавление операции RRS</span><span class="sxs-lookup"><span data-stu-id="d13ca-165">Add RRS Operation</span></span>
<span data-ttu-id="d13ca-166">Сначала создайте операцию для hello службы AzureML записи Ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d13ca-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="d13ca-167">Выберите **POST** как hello **HTTP-команду**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="d13ca-168">Тип **/services/ /workspaces/ {рабочей} {службы} / execute? api-version = {apiversion} & сведения = {сведения}** как hello **URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="d13ca-169">Тип **выполнение записи Ресурсов** как hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="d13ca-171">Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="d13ca-172">Нажмите кнопку **Сохранить** toosave этой операции.</span><span class="sxs-lookup"><span data-stu-id="d13ca-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="d13ca-174">Добавление операций BES</span><span class="sxs-lookup"><span data-stu-id="d13ca-174">Add BES Operations</span></span>
<span data-ttu-id="d13ca-175">Снимки экрана, не включаются в hello BES операций, как они являются очень похожа toothose для добавления записей Ресурсов операции hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="d13ca-176">Отправка (но не запуск) задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="d13ca-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="d13ca-177">Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="d13ca-178">Выберите **POST** для hello **HTTP-команду**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="d13ca-179">Тип **/services/ /workspaces/ {рабочей} {службы} / заданий? api-version = {apiversion}** для hello **URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="d13ca-180">Тип **отправить BES** для hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="d13ca-181">Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="d13ca-182">Нажмите кнопку **Сохранить** toosave этой операции.</span><span class="sxs-lookup"><span data-stu-id="d13ca-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="d13ca-183">Запуск задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="d13ca-183">Start a Batch Execution job</span></span>
<span data-ttu-id="d13ca-184">Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="d13ca-185">Выберите **POST** для hello **HTTP-команду**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="d13ca-186">Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid} / start? api-version = {apiversion}** для hello **URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="d13ca-187">Тип **запуск BES** для hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="d13ca-188">Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="d13ca-189">Нажмите кнопку **Сохранить** toosave этой операции.</span><span class="sxs-lookup"><span data-stu-id="d13ca-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="d13ca-190">Получить состояние hello или результат выполнения пакетного задания</span><span class="sxs-lookup"><span data-stu-id="d13ca-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="d13ca-191">Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="d13ca-192">Выберите **получить** для hello **HTTP-команду**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="d13ca-193">Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid}? api-version = {apiversion}** для hello **URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="d13ca-194">Тип **состояние BES** для hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="d13ca-195">Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="d13ca-196">Нажмите кнопку **Сохранить** toosave этой операции.</span><span class="sxs-lookup"><span data-stu-id="d13ca-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="d13ca-197">Удаление задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="d13ca-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="d13ca-198">Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API.</span><span class="sxs-lookup"><span data-stu-id="d13ca-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="d13ca-199">Выберите **удаление** для hello **HTTP-команду**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="d13ca-200">Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid}? api-version = {apiversion}** для hello **URL-адрес шаблона**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="d13ca-201">Тип **удалить BES** для hello **отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="d13ca-202">Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="d13ca-203">Нажмите кнопку **Сохранить** toosave этой операции.</span><span class="sxs-lookup"><span data-stu-id="d13ca-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="d13ca-204">Вызов операции из hello портал разработчиков</span><span class="sxs-lookup"><span data-stu-id="d13ca-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="d13ca-205">Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d13ca-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="d13ca-206">На этом шаге руководства вы будете вызывать hello **выполнение записи Ресурсов** метода, который был добавлен toohello **AzureML демонстрация API**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="d13ca-207">Нажмите кнопку **портал разработчиков** меню hello hello верхнему правому углу hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="d13ca-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="d13ca-209">Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **AzureML демонстрация API** доступные операции toosee hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="d13ca-211">Выберите **выполнение записи Ресурсов** для операции hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="d13ca-212">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="d13ca-214">Параметры запроса, введите ваш **рабочей**, **службы**, **2.0** для hello **apiversion**, и **true**для hello **сведения**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="d13ca-215">Можно найти на **рабочей** и **службы** в мониторинга hello AzureML веб-службы (см. **проверить веб-службу hello** в приложении А).</span><span class="sxs-lookup"><span data-stu-id="d13ca-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="d13ca-216">В разделе Request headers (Заголовки запросов) щелкните **Добавить заголовок** и введите текст **Content-Type** и **application/json**. Затем щелкните **Добавить заголовок** и введите текст **Authorization** и **Bearer<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="d13ca-217">Можно найти на **ключ api** в мониторинга hello AzureML веб-службы (см. **проверить веб-службу hello** в приложении А).</span><span class="sxs-lookup"><span data-stu-id="d13ca-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="d13ca-218">Тип **{«Входные данные»: {«input1»: {«ColumnNames»: [«Col2»] «значения»: [[«это хороший день»]]}}, «GlobalParameters»: {}}** для hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="d13ca-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="d13ca-220">Нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-220">Click **Send**.</span></span>

![Отправить](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="d13ca-222">После вызова операции портал разработчиков hello отображает hello **запрошенный URL-адрес** внутренней службой hello hello **состояние ответа**, hello **заголовки ответа**, а также **содержимого отклика**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="d13ca-224">Дополнение А — создание и тестирование простой веб-службы AzureML</span><span class="sxs-lookup"><span data-stu-id="d13ca-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="d13ca-225">Создание экспериментов hello</span><span class="sxs-lookup"><span data-stu-id="d13ca-225">Creating hello experiment</span></span>
<span data-ttu-id="d13ca-226">Ниже перечислены основные шаги hello для создания простого эксперимента машинного обучения Azure и развертывания его как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="d13ca-227">Hello web service принимает в качестве входного столбца произвольного текста и возвращает набор возможностей, представленных в виде целых чисел.</span><span class="sxs-lookup"><span data-stu-id="d13ca-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="d13ca-228">Например:</span><span class="sxs-lookup"><span data-stu-id="d13ca-228">For example:</span></span>

| <span data-ttu-id="d13ca-229">текст</span><span class="sxs-lookup"><span data-stu-id="d13ca-229">Text</span></span> | <span data-ttu-id="d13ca-230">Хэшированный текст</span><span class="sxs-lookup"><span data-stu-id="d13ca-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="d13ca-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="d13ca-231">This is a good day</span></span> |<span data-ttu-id="d13ca-232">1 1 2 2 0 0 2 1</span><span class="sxs-lookup"><span data-stu-id="d13ca-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="d13ca-233">Во-первых, с помощью браузера по своему усмотрению, перейдите к: [https://studio.azureml.net/](https://studio.azureml.net/) и введите ваш toolog учетные данные в.</span><span class="sxs-lookup"><span data-stu-id="d13ca-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="d13ca-234">Затем создайте пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="d13ca-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="d13ca-236">Переименуйте ее слишком**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="d13ca-237">Разверните список **Saved Datasets** (Сохраненные наборы данных) и перетащите элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="d13ca-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="d13ca-239">Разверните списки **Преобразование данных** и **Manipulation** (Работа с данными) и перетащите элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="d13ca-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="d13ca-240">Подключение **рецензий из Amazon** слишком**Выбор столбцов в наборе данных**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="d13ca-242">Последовательно щелкните **Select Columns in Dataset** (Выбор столбцов в наборе данных), **Launch column selector** (Запустить средство выбора столбцов), а затем выберите **Col2**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="d13ca-243">Щелкните флажок tooapply hello эти изменения.</span><span class="sxs-lookup"><span data-stu-id="d13ca-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="d13ca-245">Разверните **анализа текста** и перетащите **хэширование признаков** на hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="d13ca-246">Подключение **Выбор столбцов в наборе данных** слишком**хэширование признаков**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="d13ca-248">Тип **3** для hello **разрядность хэширования**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="d13ca-249">Будет создано 8 столбцов (23).</span><span class="sxs-lookup"><span data-stu-id="d13ca-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="d13ca-251">На этом этапе вы можете tooclick **запуска** tootest hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Запустить](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="d13ca-253">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="d13ca-253">Create a web service</span></span>
<span data-ttu-id="d13ca-254">Теперь создайте веб-службу.</span><span class="sxs-lookup"><span data-stu-id="d13ca-254">Now create a web service.</span></span> <span data-ttu-id="d13ca-255">Разверните список **Веб-служба** и перетащите элемент **Входные данные** в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="d13ca-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="d13ca-256">Подключение **ввода** слишком**хэширование признаков**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="d13ca-257">Перетащите в свой эксперимент также элемент **Вывод** .</span><span class="sxs-lookup"><span data-stu-id="d13ca-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="d13ca-258">Подключение **вывода** слишком**хэширование признаков**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="d13ca-260">Щелкните **Опубликовать веб-службу**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="d13ca-262">Нажмите кнопку **Да** toopublish hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="d13ca-264">Проверить веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="d13ca-264">Test hello web service</span></span>
<span data-ttu-id="d13ca-265">Веб-служба AzureML состоит из конечных точек RSS (служба запросов и ответов) и BES (служба выполнения пакетов).</span><span class="sxs-lookup"><span data-stu-id="d13ca-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="d13ca-266">Конечные точки RSS предназначены для синхронного выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="d13ca-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="d13ca-267">Конечные точки BES — для асинхронного.</span><span class="sxs-lookup"><span data-stu-id="d13ca-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="d13ca-268">tootest веб-службы с источником Python образец hello ниже, может потребоваться toodownload и hello установки пакета Azure SDK для Python (см.: [как tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="d13ca-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="d13ca-269">Необходимо также hello **рабочей**, **службы**, и **api_key** из эксперимента для hello Образец исходного кода ниже.</span><span class="sxs-lookup"><span data-stu-id="d13ca-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="d13ca-270">Hello рабочей области и службы можно найти, выбрав **запрос-ответ** или **Пакетное выполнение** для эксперимента в hello мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="d13ca-272">Можно найти hello **api_key** , щелкнув эксперимента в hello мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="d13ca-274">Тестирование конечной точки RRS</span><span class="sxs-lookup"><span data-stu-id="d13ca-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="d13ca-275">Кнопка тестирования</span><span class="sxs-lookup"><span data-stu-id="d13ca-275">Test button</span></span>
<span data-ttu-id="d13ca-276">Конечная точка записей Ресурсов hello легко tootest — tooclick **тест** на hello мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d13ca-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="d13ca-278">В поле **col2** введите текст **This is a good day**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="d13ca-279">Нажмите кнопку Далее hello.</span><span class="sxs-lookup"><span data-stu-id="d13ca-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="d13ca-281">Отобразится примерно такой текст:</span><span class="sxs-lookup"><span data-stu-id="d13ca-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="d13ca-283">Пример кода</span><span class="sxs-lookup"><span data-stu-id="d13ca-283">Sample Code</span></span>
<span data-ttu-id="d13ca-284">Другой способ tootest вашей записи Ресурсов — в коде клиента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="d13ca-285">Если щелкнуть **запрос ответ** снизу hello панели мониторинга и прокрутки toohello, вы увидите пример кода для C#, Python и R. Также вы увидите hello синтаксис запроса записей Ресурсов hello, включая URI запроса hello, заголовки и текст.</span><span class="sxs-lookup"><span data-stu-id="d13ca-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="d13ca-286">В этом руководстве приведен рабочий экземпляр кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="d13ca-286">This guide shows a working Python example.</span></span> <span data-ttu-id="d13ca-287">Вам потребуется toomodify с hello **рабочей**, **службы**, и **api_key** из эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="d13ca-288">Тестирование конечной точки BES</span><span class="sxs-lookup"><span data-stu-id="d13ca-288">Test BES endpoint</span></span>
<span data-ttu-id="d13ca-289">Нажмите кнопку **Пакетное выполнение** нижней toohello панели мониторинга и прокрутите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="d13ca-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="d13ca-290">Вы увидите пример кода для C#, Python и R. Вы также увидите hello синтаксис hello toosubmit запросы BES задания, запуск задания, состояние hello или результатам задания и удалить задание.</span><span class="sxs-lookup"><span data-stu-id="d13ca-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="d13ca-291">В этом руководстве приведен рабочий экземпляр кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="d13ca-291">This guide shows a working Python example.</span></span> <span data-ttu-id="d13ca-292">Требуется toomodify его с hello **рабочей**, **службы**, и **api_key** из эксперимента.</span><span class="sxs-lookup"><span data-stu-id="d13ca-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="d13ca-293">Кроме того, вы должны toomodify hello **имя учетной записи хранения**, **ключ учетной записи хранения**, и **имя контейнера хранилища**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="d13ca-294">Наконец, необходимо будет расположение hello toomodify hello **входной файл** и расположение hello hello **выходной файл**.</span><span class="sxs-lookup"><span data-stu-id="d13ca-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
