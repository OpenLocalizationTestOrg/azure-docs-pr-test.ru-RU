---
title: "Сведения об управлении веб-службами AzureML с помощью управления API | Документация Майкрософт"
description: "Руководство по управлению веб-службами AzureML с помощью управления API."
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="7b813-104">Сведения об управлении веб-службами AzureML с помощью управления API</span><span class="sxs-lookup"><span data-stu-id="7b813-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="7b813-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="7b813-105">Overview</span></span>
<span data-ttu-id="7b813-106">Это руководство поможет быстро начать работу с управлением API, чтобы управлять веб-службами AzureML.</span><span class="sxs-lookup"><span data-stu-id="7b813-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="7b813-107">Что собой представляет управление Azure API</span><span class="sxs-lookup"><span data-stu-id="7b813-107">What is Azure API Management?</span></span>
<span data-ttu-id="7b813-108">Управление API Azure — это служба Azure, которая позволяет управлять конечными точками REST API, настраивая доступ пользователей, регулирование использования и мониторинг панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7b813-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="7b813-109">Сведения об управлении API Azure см. [здесь](https://azure.microsoft.com/services/api-management/).</span><span class="sxs-lookup"><span data-stu-id="7b813-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="7b813-110">Руководство по началу работы с управлением API Azure находится [здесь](../api-management/api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b813-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="7b813-111">Это руководство, на котором основана данная статья, содержит больше разделов, включая информацию о конфигурациях оборудования, ценовых категориях, обработке ответов, проверке подлинности пользователей, создании продуктов, подписках разработчика и компактном отображении данных об использовании.</span><span class="sxs-lookup"><span data-stu-id="7b813-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="7b813-112">Что такое AzureML</span><span class="sxs-lookup"><span data-stu-id="7b813-112">What is AzureML?</span></span>
<span data-ttu-id="7b813-113">AzureML — это служба Azure для машинного обучения, которая позволяет вам легко создавать и развертывать решения аналитики и предоставлять к ним доступ.</span><span class="sxs-lookup"><span data-stu-id="7b813-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="7b813-114">Сведения о службе AzureML см. [здесь](https://azure.microsoft.com/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="7b813-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b813-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7b813-115">Prerequisites</span></span>
<span data-ttu-id="7b813-116">Вот что вам нужно, чтобы выполнить инструкции, приведенные в этом руководстве:</span><span class="sxs-lookup"><span data-stu-id="7b813-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="7b813-117">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7b813-117">An Azure account.</span></span> <span data-ttu-id="7b813-118">Если у вас нет учетной записи Azure, щелкните [здесь](https://azure.microsoft.com/pricing/free-trial/) , чтобы узнать, как создать бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7b813-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="7b813-119">Учетная запись AzureML.</span><span class="sxs-lookup"><span data-stu-id="7b813-119">An AzureML account.</span></span> <span data-ttu-id="7b813-120">Если у вас нет учетной записи AzureML, щелкните [здесь](https://studio.azureml.net/) , чтобы узнать, как создать бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="7b813-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="7b813-121">Рабочая область, служба и ключ API для эксперимента AzureML, развернутого в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="7b813-122">Сведения о том, как создать эксперимент AzureML, см. [здесь](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="7b813-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="7b813-123">Сведения о том, как развернуть эксперимент AzureML в качестве веб-службы, см. [здесь](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="7b813-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="7b813-124">Инструкции по созданию и тестированию простого эксперимента AzureML и его развертывания в качестве веб-службы содержатся также в дополнении А.</span><span class="sxs-lookup"><span data-stu-id="7b813-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="7b813-125">Создание экземпляра API Management</span><span class="sxs-lookup"><span data-stu-id="7b813-125">Create an API Management instance</span></span>
<span data-ttu-id="7b813-126">Ниже приведены основные действия, которые нужно выполнить, чтобы управлять веб-службой AzureML с помощью управления API.</span><span class="sxs-lookup"><span data-stu-id="7b813-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="7b813-127">Сначала создайте экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-127">First create a service instance.</span></span> <span data-ttu-id="7b813-128">Войдите на [классический портал](https://manage.windowsazure.com/) и щелкните **Создать** > **Службы приложений** > **Управление API** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7b813-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="7b813-130">Укажите уникальное значение в поле **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="7b813-130">Specify a unique **URL**.</span></span> <span data-ttu-id="7b813-131">В этом руководстве используется значение **demoazureml** , но вам нужно будет указать другое.</span><span class="sxs-lookup"><span data-stu-id="7b813-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="7b813-132">Выберите необходимые значения в поле **Подписка** и **Регион** для своего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="7b813-133">После выбора нажмите кнопку "Далее".</span><span class="sxs-lookup"><span data-stu-id="7b813-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="7b813-135">Укажите значение в поле **Название организации**.</span><span class="sxs-lookup"><span data-stu-id="7b813-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="7b813-136">В этом руководстве используется значение **demoazureml** , но вам нужно будет указать другое.</span><span class="sxs-lookup"><span data-stu-id="7b813-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="7b813-137">В поле **Адрес электронной почты администратора** введите свой адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7b813-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="7b813-138">Этот адрес электронный почты используется для получения уведомлений от системы API Management.</span><span class="sxs-lookup"><span data-stu-id="7b813-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="7b813-140">Установите флажок для создания экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="7b813-141">*Создание службы занимает до 30 минут*.</span><span class="sxs-lookup"><span data-stu-id="7b813-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="7b813-142">Создание API</span><span class="sxs-lookup"><span data-stu-id="7b813-142">Create the API</span></span>
<span data-ttu-id="7b813-143">После создания службы нужно создать API.</span><span class="sxs-lookup"><span data-stu-id="7b813-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="7b813-144">API представляет набор операций, которые могут быть вызваны клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="7b813-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="7b813-145">Операции API передаются существующей веб-службе.</span><span class="sxs-lookup"><span data-stu-id="7b813-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="7b813-146">В этом руководстве продемонстрировано создание интерфейсов API, которые играют роль посредников между вами и существующими веб-службами AzureML RRS и BES.</span><span class="sxs-lookup"><span data-stu-id="7b813-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="7b813-147">Интерфейсы API создаются и настраиваются на издательском портале API, который доступен на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7b813-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="7b813-148">Чтобы открыть издательский портал, выберите экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="7b813-150">На классическом портале Azure щелкните **Управление** для вашей службы управления API.</span><span class="sxs-lookup"><span data-stu-id="7b813-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="7b813-152">В меню слева **Управление API** щелкните**Интерфейсы API** и **Добавить API**.</span><span class="sxs-lookup"><span data-stu-id="7b813-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="7b813-154">В поле **Имя веб-API** введите текст **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="7b813-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="7b813-155">Введите **https://ussouthcentral.services.azureml.net** в поле **URL-адрес веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="7b813-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="7b813-156">Введите **azureml-demo** в поле **Web API URL suffix** (Суффикс URL-адреса веб-API).</span><span class="sxs-lookup"><span data-stu-id="7b813-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="7b813-157">Установите флажок **HTTPS** для параметра **Web API URL** (URL-адрес веб-API).</span><span class="sxs-lookup"><span data-stu-id="7b813-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="7b813-158">Выберите **Starter** (Начальный комплект) в поле **Продукты**.</span><span class="sxs-lookup"><span data-stu-id="7b813-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="7b813-159">Чтобы после этого создать интерфейс API, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b813-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="7b813-161">Добавление операций</span><span class="sxs-lookup"><span data-stu-id="7b813-161">Add the operations</span></span>
<span data-ttu-id="7b813-162">Чтобы добавить операции в созданный API, щелкните **Добавить операцию** .</span><span class="sxs-lookup"><span data-stu-id="7b813-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="7b813-164">Появится окно **New operation** (Новая операция), а вкладка **Signature** (Сигнатура) будет выбрана по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7b813-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="7b813-165">Добавление операции RRS</span><span class="sxs-lookup"><span data-stu-id="7b813-165">Add RRS Operation</span></span>
<span data-ttu-id="7b813-166">Сначала создайте операцию для службы AzureML RRS.</span><span class="sxs-lookup"><span data-stu-id="7b813-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="7b813-167">Выберите значение **POST** в поле **HTTP verb** (HTTP-команда).</span><span class="sxs-lookup"><span data-stu-id="7b813-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="7b813-168">В поле **URL template** (Шаблон URL-адреса) введите текст **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="7b813-169">В поле **Отображаемое имя** введите текст **RRS Execute**.</span><span class="sxs-lookup"><span data-stu-id="7b813-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="7b813-171">Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7b813-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="7b813-172">Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="7b813-174">Добавление операций BES</span><span class="sxs-lookup"><span data-stu-id="7b813-174">Add BES Operations</span></span>
<span data-ttu-id="7b813-175">К инструкциям по добавлению операций BES снимки экрана не прилагаются, так как они схожи со снимками, которые использованы в инструкциях по добавлению операции RRS.</span><span class="sxs-lookup"><span data-stu-id="7b813-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="7b813-176">Отправка (но не запуск) задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="7b813-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="7b813-177">Чтобы добавить к API операцию AzureML BES, щелкните **Добавить операцию** .</span><span class="sxs-lookup"><span data-stu-id="7b813-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="7b813-178">Выберите значение **POST** в поле **HTTP verb** (HTTP-команда).</span><span class="sxs-lookup"><span data-stu-id="7b813-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="7b813-179">В поле **URL template** (Шаблон URL-адреса) введите текст **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="7b813-180">Введите текст **BES Submit** (Отправка BES) в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="7b813-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="7b813-181">Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7b813-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="7b813-182">Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="7b813-183">Запуск задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="7b813-183">Start a Batch Execution job</span></span>
<span data-ttu-id="7b813-184">Чтобы добавить к API операцию AzureML BES, щелкните **Добавить операцию** .</span><span class="sxs-lookup"><span data-stu-id="7b813-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="7b813-185">Выберите значение **POST** в поле **HTTP verb** (HTTP-команда).</span><span class="sxs-lookup"><span data-stu-id="7b813-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="7b813-186">В поле **URL template** (Шаблон URL-адреса) введите текст **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="7b813-187">Введите текст **BES Start** (Запуск BES) в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="7b813-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="7b813-188">Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7b813-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="7b813-189">Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="7b813-190">Получение состояния или результата задания пакетного выполнения</span><span class="sxs-lookup"><span data-stu-id="7b813-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="7b813-191">Чтобы добавить к API операцию AzureML BES, щелкните **Добавить операцию** .</span><span class="sxs-lookup"><span data-stu-id="7b813-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="7b813-192">Выберите значение **GET** в поле **HTTP verb** (HTTP-команда).</span><span class="sxs-lookup"><span data-stu-id="7b813-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="7b813-193">В поле **URL template** (Шаблон URL-адреса) введите текст **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="7b813-194">Введите текст **BES Status** (Статус BES) в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="7b813-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="7b813-195">Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7b813-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="7b813-196">Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="7b813-197">Удаление задачи выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="7b813-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="7b813-198">Чтобы добавить к API операцию AzureML BES, щелкните **Добавить операцию** .</span><span class="sxs-lookup"><span data-stu-id="7b813-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="7b813-199">Выберите значение **DELETE** в поле **HTTP verb** (HTTP-команда).</span><span class="sxs-lookup"><span data-stu-id="7b813-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="7b813-200">В поле **URL template** (Шаблон URL-адреса) введите текст **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="7b813-201">В поле **Отображаемое имя** введите текст **BES Delete**.</span><span class="sxs-lookup"><span data-stu-id="7b813-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="7b813-202">Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7b813-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="7b813-203">Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="7b813-204">Вызов операции с портала разработчика</span><span class="sxs-lookup"><span data-stu-id="7b813-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="7b813-205">Операции могут быть вызваны из портала разработчика, где предоставляется удобный способ для просмотра и проверки операций API.</span><span class="sxs-lookup"><span data-stu-id="7b813-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="7b813-206">Следуя инструкциям, приведенным в этом разделе руководства, вы сможете вызвать метод **RRS Execute**, добавленный в элемент **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="7b813-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="7b813-207">Выберите **Портал разработчика** в правом верхнем меню на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="7b813-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="7b813-209">Щелкните **Интерфейсы API** в меню сверху, а затем щелкните **AzureML Demo API** (Демонстрационный API AzureML), чтобы отобразились доступные операции.</span><span class="sxs-lookup"><span data-stu-id="7b813-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="7b813-211">Выберите операцию **RRS Execute** .</span><span class="sxs-lookup"><span data-stu-id="7b813-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="7b813-212">Щелкните **Попробовать**.</span><span class="sxs-lookup"><span data-stu-id="7b813-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="7b813-214">В разделе "Параметры запроса" введите значения в полях **workspace** (рабочая область) и **service** (служба). В поле **apiversion** (версия API) введите значение **2.0**, а в поле **details** (сведения) — **true**.</span><span class="sxs-lookup"><span data-stu-id="7b813-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="7b813-215">Название ваших **рабочей области** и **службы** отображается на панели мониторинга веб-службы AzureML (см. раздел **Тестирование веб-службы** в приложении A).</span><span class="sxs-lookup"><span data-stu-id="7b813-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="7b813-216">В разделе Request headers (Заголовки запросов) щелкните **Добавить заголовок** и введите текст **Content-Type** и **application/json**. Затем щелкните **Добавить заголовок** и введите текст **Authorization** и **Bearer<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="7b813-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="7b813-217">Название вашего **ключа API** отображается на панели мониторинга веб-службы AzureML (см. раздел **Тестирование веб-службы** в приложении A).</span><span class="sxs-lookup"><span data-stu-id="7b813-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="7b813-218">В поле "Текст запроса" введите **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": "This is a good day"}}, "GlobalParameters": {}}**.</span><span class="sxs-lookup"><span data-stu-id="7b813-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="7b813-220">Нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="7b813-220">Click **Send**.</span></span>

![Отправить](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="7b813-222">После вызова операции портал разработчика выводит **запрошенный URL-адрес** от фоновой службы, **состояние ответа**, **заголовки ответа** и **содержимое ответа**.</span><span class="sxs-lookup"><span data-stu-id="7b813-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="7b813-224">Дополнение А — создание и тестирование простой веб-службы AzureML</span><span class="sxs-lookup"><span data-stu-id="7b813-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="7b813-225">Создание эксперимента</span><span class="sxs-lookup"><span data-stu-id="7b813-225">Creating the experiment</span></span>
<span data-ttu-id="7b813-226">Ниже описаны действия, которые нужно выполнить, чтобы создать простой эксперимент AzureML и развернуть его в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="7b813-227">Веб-служба принимает столбец случайного текста и возвращает набор функций в виде целых чисел.</span><span class="sxs-lookup"><span data-stu-id="7b813-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="7b813-228">Например:</span><span class="sxs-lookup"><span data-stu-id="7b813-228">For example:</span></span>

| <span data-ttu-id="7b813-229">текст</span><span class="sxs-lookup"><span data-stu-id="7b813-229">Text</span></span> | <span data-ttu-id="7b813-230">Хэшированный текст</span><span class="sxs-lookup"><span data-stu-id="7b813-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="7b813-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="7b813-231">This is a good day</span></span> |<span data-ttu-id="7b813-232">1 1 2 2 0 0 2 1</span><span class="sxs-lookup"><span data-stu-id="7b813-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="7b813-233">Сначала перейдите на веб-сайт [https://studio.azureml.net/](https://studio.azureml.net/) и, чтобы выполнить вход, введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7b813-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="7b813-234">Затем создайте пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="7b813-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="7b813-236">Измените его имя на **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="7b813-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="7b813-237">Разверните список **Saved Datasets** (Сохраненные наборы данных) и перетащите элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="7b813-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="7b813-239">Разверните списки **Преобразование данных** и **Manipulation** (Работа с данными) и перетащите элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="7b813-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="7b813-240">Соедините элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) с элементом **Select Columns in Dataset** (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="7b813-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="7b813-242">Последовательно щелкните **Select Columns in Dataset** (Выбор столбцов в наборе данных), **Launch column selector** (Запустить средство выбора столбцов), а затем выберите **Col2**.</span><span class="sxs-lookup"><span data-stu-id="7b813-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="7b813-243">Чтобы изменения вступили в силу, щелкните значок флажка.</span><span class="sxs-lookup"><span data-stu-id="7b813-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="7b813-245">Разверните список **Text Analytics** (Аналитика текста) и перетащите элемент **Feature Hashing** (Хеширование признаков) в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="7b813-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="7b813-246">Соедините элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) с элементом **Feature Hashing** (Хэширование признаков).</span><span class="sxs-lookup"><span data-stu-id="7b813-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="7b813-248">В поле **Hashing bitsize** (Размер бита хеширования) укажите значение **3**.</span><span class="sxs-lookup"><span data-stu-id="7b813-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="7b813-249">Будет создано 8 столбцов (23).</span><span class="sxs-lookup"><span data-stu-id="7b813-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="7b813-251">На этом этапе рекомендуется протестировать эксперимент, нажав кнопку **Запустить** .</span><span class="sxs-lookup"><span data-stu-id="7b813-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Запустить](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="7b813-253">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="7b813-253">Create a web service</span></span>
<span data-ttu-id="7b813-254">Теперь создайте веб-службу.</span><span class="sxs-lookup"><span data-stu-id="7b813-254">Now create a web service.</span></span> <span data-ttu-id="7b813-255">Разверните список **Веб-служба** и перетащите элемент **Входные данные** в свой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="7b813-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="7b813-256">Соедините элемент **Входные данные** с элементом **Feature Hashing** (Хеширование признаков).</span><span class="sxs-lookup"><span data-stu-id="7b813-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="7b813-257">Перетащите в свой эксперимент также элемент **Вывод** .</span><span class="sxs-lookup"><span data-stu-id="7b813-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="7b813-258">Соедините элемент **Вывод** с элементом **Feature Hashing** (Хеширование признаков).</span><span class="sxs-lookup"><span data-stu-id="7b813-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="7b813-260">Щелкните **Опубликовать веб-службу**.</span><span class="sxs-lookup"><span data-stu-id="7b813-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="7b813-262">Чтобы опубликовать веб-службу, щелкните **Да** .</span><span class="sxs-lookup"><span data-stu-id="7b813-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="7b813-264">Тестирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="7b813-264">Test the web service</span></span>
<span data-ttu-id="7b813-265">Веб-служба AzureML состоит из конечных точек RSS (служба запросов и ответов) и BES (служба выполнения пакетов).</span><span class="sxs-lookup"><span data-stu-id="7b813-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="7b813-266">Конечные точки RSS предназначены для синхронного выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="7b813-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="7b813-267">Конечные точки BES — для асинхронного.</span><span class="sxs-lookup"><span data-stu-id="7b813-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="7b813-268">Чтобы протестировать веб-службу с помощью приведенного ниже примера кода на языке Python, вам может понадобиться скачать и установить пакет Azure SDK для Python (см. статью [Способы установки Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="7b813-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="7b813-269">Для примера кода ниже потребуется указать также **рабочую область**, **службу** и **ключ API** вашего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="7b813-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="7b813-270">Вы можете узнать название рабочей области и службы, щелкнув **Запрос-ответ** или **Выполнение пакета** для своего эксперимента на панели мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="7b813-272">Чтобы отобразился **ключ API**, щелкните свой эксперимент на панели мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="7b813-274">Тестирование конечной точки RRS</span><span class="sxs-lookup"><span data-stu-id="7b813-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="7b813-275">Кнопка тестирования</span><span class="sxs-lookup"><span data-stu-id="7b813-275">Test button</span></span>
<span data-ttu-id="7b813-276">Простой способ протестировать конечную точку RRS — это нажать кнопку **Тестировать** на панели мониторинга веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7b813-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="7b813-278">В поле **col2** введите текст **This is a good day**.</span><span class="sxs-lookup"><span data-stu-id="7b813-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="7b813-279">Щелкните значок флажка.</span><span class="sxs-lookup"><span data-stu-id="7b813-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="7b813-281">Отобразится примерно такой текст:</span><span class="sxs-lookup"><span data-stu-id="7b813-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="7b813-283">Пример кода</span><span class="sxs-lookup"><span data-stu-id="7b813-283">Sample Code</span></span>
<span data-ttu-id="7b813-284">Протестировать конечную точку RRS вы можете также с помощью клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="7b813-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="7b813-285">Если на панели мониторинга щелкнуть **Запрос-ответ** и прокрутить страницу до самого низа, отобразится образец кода для C#, Python и R. Отобразится также и синтаксис запроса RRS, в том числе URI, заголовки и текст запроса.</span><span class="sxs-lookup"><span data-stu-id="7b813-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="7b813-286">В этом руководстве приведен рабочий экземпляр кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="7b813-286">This guide shows a working Python example.</span></span> <span data-ttu-id="7b813-287">В нем нужно будет изменить название **рабочей области**, **службы** и **ключа API** эксперимента.</span><span class="sxs-lookup"><span data-stu-id="7b813-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="7b813-288">Тестирование конечной точки BES</span><span class="sxs-lookup"><span data-stu-id="7b813-288">Test BES endpoint</span></span>
<span data-ttu-id="7b813-289">На панели мониторинга щелкните **Выполнение пакета** и прокрутите страницу до самого низа.</span><span class="sxs-lookup"><span data-stu-id="7b813-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="7b813-290">Отобразится пример кода на языках C#, Python и R. Отобразится также синтаксис запроса BES на отправку задачи, запуск задачи, получение статуса или результата выполнения задачи и на удаление задачи.</span><span class="sxs-lookup"><span data-stu-id="7b813-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="7b813-291">В этом руководстве приведен рабочий экземпляр кода на языке Python.</span><span class="sxs-lookup"><span data-stu-id="7b813-291">This guide shows a working Python example.</span></span> <span data-ttu-id="7b813-292">В нем нужно изменить название **рабочей области**, **службы** и **ключа API** эксперимента.</span><span class="sxs-lookup"><span data-stu-id="7b813-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="7b813-293">Кроме того, нужно изменить **имя учетной записи хранения**, **ключ учетной записи хранения** и **имя контейнера хранилища**.</span><span class="sxs-lookup"><span data-stu-id="7b813-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="7b813-294">Наконец, вам понадобится изменить расположение **входного файла** и **выходного файла**.</span><span class="sxs-lookup"><span data-stu-id="7b813-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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
