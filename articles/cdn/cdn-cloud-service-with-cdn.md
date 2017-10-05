---
title: "Интеграция облачной службы Azure с Azure CDN | Документация Майкрософт"
description: "Узнайте, как развернуть облачную службу, которая обслуживает содержимое из интегрированной конечной точки Azure CDN."
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="f0afa-103"><a name="intro"></a>Интеграция облачной службы с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="f0afa-104">Облачную службу можно интегрировать с сетью Azure CDN, которая обслуживает любое содержимое из расположения облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f0afa-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="f0afa-105">Такой подход обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="f0afa-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="f0afa-106">Упрощение развертывания и обновления образов, скриптов и таблиц стилей в каталогах проекта облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f0afa-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="f0afa-107">Облегчение обновления пакетов NuGet в облачной службе, например, версий jQuery или Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f0afa-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="f0afa-108">Управление веб-приложениями и контентом, обслуживаемым CDN, из одного интерфейса Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0afa-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="f0afa-109">Единый рабочий процесс развертывания для веб-приложения и контента, обслуживаемого CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="f0afa-110">Интеграция объединения и минификации ASP.NET с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f0afa-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f0afa-111">What you will learn</span></span>
<span data-ttu-id="f0afa-112">Из этого учебника вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="f0afa-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="f0afa-113">Интеграция конечной точки Azure CDN с облачной службой и обслуживание статического содержимого на веб-страницах из Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="f0afa-114">Настройка параметров кэша для статического содержимого в облачной службе</span><span class="sxs-lookup"><span data-stu-id="f0afa-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="f0afa-115">Обслуживание содержимого из действий контроллера с помощью Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="f0afa-116">Обслуживание объединенного в пакет и минифицированного содержимого через Azure CDN с поддержкой интерфейса отладки сценариев в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0afa-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="f0afa-117">Настройка резервирования сценариев и CSS, когда Azure CDN находится в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="f0afa-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="f0afa-118">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="f0afa-118">What you will build</span></span>
<span data-ttu-id="f0afa-119">Будет выполняться развертывание веб-роли облачной службы с помощью шаблона MVC ASP.NET по умолчанию, добавление кода для обслуживания контента из интегрированной Azure CDN, такого как образ, результаты действий контроллера, файлы JavaScript и CSS по умолчанию, а также создание кода для настройки резервного механизма обслуживаемых пакетов в случае, когда CDN находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="f0afa-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="f0afa-120">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="f0afa-120">What you will need</span></span>
<span data-ttu-id="f0afa-121">Для работы с этим учебником необходимы следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="f0afa-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="f0afa-122">Активная [учетная запись Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="f0afa-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="f0afa-123">Наличие Visual Studio 2015 с [пакетом SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="f0afa-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="f0afa-124">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afa-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="f0afa-125">Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) — вы получаете кредиты, которые можно использовать для опробования платных служб Azure, и даже после израсходования кредитов вы сохраняете учетную запись и возможность использовать бесплатные службы Azure, такие как веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="f0afa-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="f0afa-126">Вы имеете возможность [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты за службы Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afa-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="f0afa-127">Развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="f0afa-127">Deploy a cloud service</span></span>
<span data-ttu-id="f0afa-128">В этом разделе будет выполняться развертывание шаблона приложения MVC ASP.NET по умолчанию в Visual Studio 2015 в веб-роли облачной службы, после чего оно будет интегрировано с новой конечной точкой CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="f0afa-129">Выполните приведенные далее инструкции.</span><span class="sxs-lookup"><span data-stu-id="f0afa-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="f0afa-130">В Visual Studio 2015 создайте облачную службу Azure, последовательно выбрав **Файл > Создать > Проект > Облако > Облачная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="f0afa-131">Назначьте ей имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="f0afa-132">Выберите **веб-роль ASP.NET** и нажмите кнопку **>**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="f0afa-133">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="f0afa-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="f0afa-134">Выберите **MVC** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="f0afa-135">Теперь опубликуйте эту веб-роль в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afa-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="f0afa-136">Щелкните правой кнопкой мыши проект облачной службы и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="f0afa-137">Если вы еще не вошли в Microsoft Azure, щелкните раскрывающийся список **Добавить учетную запись** и выберите **Добавить учетную запись**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="f0afa-138">На странице входа войдите с учетной записью Майкрософт, которая использовалась для активации учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afa-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="f0afa-139">После выполнения входа нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="f0afa-140">Если облачная служба или учетная запись хранения еще не создана, Visual Studio поможет создать их.</span><span class="sxs-lookup"><span data-stu-id="f0afa-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="f0afa-141">В диалоговом окне **Создание облачной службы и учетной записи** введите нужное имя службы и выберите нужный регион.</span><span class="sxs-lookup"><span data-stu-id="f0afa-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="f0afa-142">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="f0afa-143">На странице параметров публикации проверьте конфигурацию и нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="f0afa-144">Процесс публикации для облачных служб занимает много времени.</span><span class="sxs-lookup"><span data-stu-id="f0afa-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="f0afa-145">Параметр включения веб-развертывания для всех ролей может значительно ускорить отладку облачной службы, обеспечивая быстрые (но временные) обновления веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="f0afa-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="f0afa-146">Дополнительные сведения об этом параметре см. в статье [Публикация облачной службы с помощью инструментов Azure](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0afa-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="f0afa-147">Когда в **журнале изменений Microsoft Azure** публикация отобразится с состоянием **Завершено**, будет создана конечная точка CDN, интегрированная с этой облачной службой.</span><span class="sxs-lookup"><span data-stu-id="f0afa-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f0afa-148">Если после публикации в развернутой облачной службе отображается экран сообщения об ошибке, вероятно, это связано с тем, что развернутая облачная служба использует [гостевую ОС без .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="f0afa-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="f0afa-149">Чтобы устранить эту проблему, [разверните .NET 4.5.2 в качестве задачи запуска](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f0afa-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="f0afa-150">Создание нового профиля сети CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-150">Create a new CDN profile</span></span>
<span data-ttu-id="f0afa-151">Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="f0afa-152">Каждый профиль содержит одну или несколько конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="f0afa-153">Вы можете использовать несколько профилей для упорядочения конечных точек сети CDN по домену Интернета, веб-приложению или согласно другим условиям.</span><span class="sxs-lookup"><span data-stu-id="f0afa-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="f0afa-154">Если у вас уже есть профиль CDN для работы, перейдите к разделу [Создание новой конечной точки сети CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f0afa-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="f0afa-155">Создание новой конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="f0afa-156">**Создание новой конечной точки CDN для учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="f0afa-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="f0afa-157">На [портале управления Azure](https://portal.azure.com)перейдите к профилю сети CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="f0afa-158">На предыдущем шаге вы могли прикрепить его к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f0afa-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="f0afa-159">Если профиль не прикреплен, найдите его, нажав кнопку **Обзор**, выбрав **Профили CDN** и щелкнув профиль, к которому нужно добавить конечную точку.</span><span class="sxs-lookup"><span data-stu-id="f0afa-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="f0afa-160">Появится колонка профиля сети CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-160">The CDN profile blade appears.</span></span>
   
    ![Профиль сети CDN][cdn-profile-settings]
2. <span data-ttu-id="f0afa-162">Нажмите кнопку **Добавить конечную точку** .</span><span class="sxs-lookup"><span data-stu-id="f0afa-162">Click the **Add Endpoint** button.</span></span>
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    <span data-ttu-id="f0afa-164">Появится колонка **Добавление конечной точки** .</span><span class="sxs-lookup"><span data-stu-id="f0afa-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. <span data-ttu-id="f0afa-166">Введите **имя** конечной точки сети CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="f0afa-167">Это имя будет использоваться для доступа к кэшированным ресурсам в домене `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="f0afa-168">В раскрывающемся списке **Тип источника** выберите *Облачная служба*.</span><span class="sxs-lookup"><span data-stu-id="f0afa-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="f0afa-169">В раскрывающемся списке **Имя узла источника** выберите облачную службу.</span><span class="sxs-lookup"><span data-stu-id="f0afa-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="f0afa-170">Оставьте значения по умолчанию для параметров **Путь к источнику**, **Заголовок узла источника** и **Протокол/Порт источника**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="f0afa-171">Необходимо указать хотя бы один протокол (HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="f0afa-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="f0afa-172">Нажмите кнопку **Создать** , чтобы создать новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="f0afa-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="f0afa-173">Созданная конечная точка отображается в списке конечных точек для профиля.</span><span class="sxs-lookup"><span data-stu-id="f0afa-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="f0afa-174">В режиме списка отображается URL-адрес для доступа к кэшированному содержимому, а также исходному домену.</span><span class="sxs-lookup"><span data-stu-id="f0afa-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![Конечная точка сети CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="f0afa-176">Конечная точка не сразу будет доступна для использования.</span><span class="sxs-lookup"><span data-stu-id="f0afa-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="f0afa-177">Распространение регистрации по сети CDN может занять 90 минут.</span><span class="sxs-lookup"><span data-stu-id="f0afa-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="f0afa-178">Если пользователь попытается незамедлительно воспользоваться именем домена CDN, он может столкнуться с кодом состояния 404, пока содержимое не станет доступно через CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="f0afa-179">Тестирование конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-179">Test the CDN endpoint</span></span>
<span data-ttu-id="f0afa-180">Когда публикация перейдет в состояние **Завершено**, откройте окно браузера и перейдите по адресу **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="f0afa-181">В моей настройке это следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="f0afa-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="f0afa-182">Он соответствует следующему исходному URL-адресу в конечной точке CDN:</span><span class="sxs-lookup"><span data-stu-id="f0afa-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="f0afa-183">При переходе по адресу **http://*&lt;имя_сети_CDN>*.azureedge.net/Content/bootstrap.css** в разных браузерах вам будет предложено скачать или открыть файл bootstrap.css из опубликованного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f0afa-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="f0afa-184">Аналогичным образом можно получать доступ к любому общедоступному URL-адресу в **http://*&lt;serviceName>*.cloudapp.net/** прямо из конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="f0afa-185">Например:</span><span class="sxs-lookup"><span data-stu-id="f0afa-185">For example:</span></span>

* <span data-ttu-id="f0afa-186">к JS-файлу в пути /Script;</span><span class="sxs-lookup"><span data-stu-id="f0afa-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="f0afa-187">к любому файлу контента в пути /Content;</span><span class="sxs-lookup"><span data-stu-id="f0afa-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="f0afa-188">к любому контроллеру или действию;</span><span class="sxs-lookup"><span data-stu-id="f0afa-188">Any controller/action</span></span>
* <span data-ttu-id="f0afa-189">если в конечной точке CDN включена строка запроса, то к любому URL-адресу со строкой запроса.</span><span class="sxs-lookup"><span data-stu-id="f0afa-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="f0afa-190">Фактически при использовании указанной выше конфигурации вы можете разместить всю облачную службу из **http://*&lt;cdnName>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="f0afa-191">Если я перейду по адресу **http://camservice.azureedge.net/**, то получу результат действия из Home/Index.</span><span class="sxs-lookup"><span data-stu-id="f0afa-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="f0afa-192">Но это не означает, что следует всегда обслуживать всю облачную службу через Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="f0afa-193">CDN со статической оптимизацией доставки не всегда ускоряет доставку динамических ресурсов, которые не должны кэшироваться или очень часто обновляются, поскольку CDN должна слишком часто получать новые версии ресурса с сервера-источника.</span><span class="sxs-lookup"><span data-stu-id="f0afa-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="f0afa-194">В этом сценарии вы можете включить [динамическое ускорение сайтов](cdn-dynamic-site-acceleration.md) (DSA) для конечной точки CDN, которая использует разные методы для ускорения доставки динамических активов, не подлежащих кэшированию.</span><span class="sxs-lookup"><span data-stu-id="f0afa-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="f0afa-195">Если у вас есть сайт, на котором есть и статическое, и динамическое содержимое, то для обслуживания статического содержимого вам лучше выбрать CDN со статической оптимизацией (например, общая веб-доставка), а динамическое содержимое доставлять либо напрямую с исходного сервера, либо через конечную точку CDN с оптимизацией DSA, включая ее отдельно для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f0afa-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="f0afa-196">В отношении этого вы уже видели, как получать доступ к отдельным файлам контента из конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="f0afa-197">Я покажу, как обслуживать определенное действие контроллера через конечную точку CDN, в разделе "Обслуживание содержимого из действий контроллера с помощью Azure CDN".</span><span class="sxs-lookup"><span data-stu-id="f0afa-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="f0afa-198">Альтернатива заключается в том, чтобы определить, какое содержимое должно обслуживаться из Azure CDN на индивидуальной основе в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="f0afa-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="f0afa-199">В отношении этого вы уже видели, как получать доступ к отдельным файлам контента из конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="f0afa-200">Я покажу, как обслуживать определенное действие контроллера посредством конечной точки CDN, в разделе [Обслуживание контента из действий контроллера посредством Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="f0afa-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="f0afa-201">Настройка параметров кэширования для статических файлов в облачной службе</span><span class="sxs-lookup"><span data-stu-id="f0afa-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="f0afa-202">С помощью интеграции Azure CDN в облачной службе можно указать, как статическое содержимое должно кэшироваться в конечной точке CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="f0afa-203">Для этого откройте файл *Web.config* из проекта веб-роли (например, WebRole1) и добавьте элемент `<staticContent>` в `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="f0afa-204">Следующий XML настраивает истечение срока годности кэша через 3 дня.</span><span class="sxs-lookup"><span data-stu-id="f0afa-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="f0afa-205">После этого все статические файлы в облачной службе будут соблюдать то же правило в кэше CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="f0afa-206">Для более детального управления параметрами кэша добавьте файл *Web.config* в папку и добавьте в этом месте свои параметры.</span><span class="sxs-lookup"><span data-stu-id="f0afa-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="f0afa-207">Например, добавьте файл *Web.config* в папку *\Content* и замените содержимое следующим XML.</span><span class="sxs-lookup"><span data-stu-id="f0afa-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="f0afa-208">Этот параметр приводит к кэшированию всех статических файлов из папки *\Content* на 15 дней.</span><span class="sxs-lookup"><span data-stu-id="f0afa-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="f0afa-209">Дополнительные сведения о настройке элемента `<clientCache>` см. в статье [Кэш клиента&lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="f0afa-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="f0afa-210">В разделе [Обслуживание контента из действий контроллера посредством Azure CDN](#controller)я также покажу, как можно настраивать параметры кэша для результатов действий контроллера в кэше CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="f0afa-211">Обслуживание содержимого из действий контроллера с помощью Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="f0afa-212">При интеграции веб-роли облачной службы с Azure CDN сравнительно легко обслуживать содержимое от действий контроллера, используя Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="f0afa-213">Помимо обслуживания облачной службы непосредственно через Azure CDN (показанного выше), в видео [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN) (Уменьшение задержки в Интернете с помощью Azure CDN) [Мартин Баллиау](https://twitter.com/maartenballiauw) (Maarten Balliauw) показывает, как это делать с помощью контроллера MemeGenerator.</span><span class="sxs-lookup"><span data-stu-id="f0afa-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="f0afa-214">Я просто воспроизведу это здесь.</span><span class="sxs-lookup"><span data-stu-id="f0afa-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="f0afa-215">Предположим, вы хотите создать в облачной службе мемы на основе образа молодого Чака Норриса (фото [Алана Лайта (Alan Light)](http://www.flickr.com/photos/alan-light/218493788/)):</span><span class="sxs-lookup"><span data-stu-id="f0afa-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="f0afa-216">Имеется простое действие `Index` , которое позволяет клиентам задавать гиперболы в образе, а затем создает мем, как только клиент отправит их в действие.</span><span class="sxs-lookup"><span data-stu-id="f0afa-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="f0afa-217">Поскольку это Чак Норрис, можно ожидать, что страница станет очень популярной по всему миру.</span><span class="sxs-lookup"><span data-stu-id="f0afa-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="f0afa-218">Это хороший пример обслуживания полудинамического контента с помощью Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="f0afa-219">Чтобы настроить это действие контроллера, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0afa-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="f0afa-220">В папке *\Controllers* создайте новый CS-файл с именем *MemeGeneratorController.cs* и замените содержимое следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="f0afa-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="f0afa-221">Не забудьте заменить выделенные фрагменты именем CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="f0afa-222">Щелкните правой кнопкой мыши действие `Index()` по умолчанию и выберите **Добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="f0afa-223">Примите параметры, показанные ниже, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="f0afa-224">Откройте новый файл *Views\MemeGenerator\Index.cshtml* и замените его содержимое следующим простым HTML для отправки гипербол.</span><span class="sxs-lookup"><span data-stu-id="f0afa-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="f0afa-225">Снова опубликуйте облачную службу и перейдите в браузере по адресу **http://*&lt;Имя_службы>*.cloudapp.net/MemeGenerator/Index**.</span><span class="sxs-lookup"><span data-stu-id="f0afa-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="f0afa-226">При отправке значений формы в `/MemeGenerator/Index` метод действия `Index_Post` возвращает ссылку на метод действия `Show` с соответствующим идентификатором ввода.</span><span class="sxs-lookup"><span data-stu-id="f0afa-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="f0afa-227">Если щелкнуть ссылку, появится следующий код:</span><span class="sxs-lookup"><span data-stu-id="f0afa-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="f0afa-228">Если подключен локальный отладчик, то вы получите обычный интерфейс отладки с локальным перенаправлением.</span><span class="sxs-lookup"><span data-stu-id="f0afa-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="f0afa-229">Если отладчик работает в облачной службе, то перенаправление будет выполняться на следующий адрес:</span><span class="sxs-lookup"><span data-stu-id="f0afa-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="f0afa-230">Он соответствует следующему исходному URL-адресу в конечной точке CDN:</span><span class="sxs-lookup"><span data-stu-id="f0afa-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="f0afa-231">Затем можно с помощью атрибута `OutputCacheAttribute` в методе `Generate` указать, как должен кэшироваться результат действия, которое будет выполнять Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="f0afa-232">В следующем коде задается срок годности кэша в 1 час (3 600 секунд).</span><span class="sxs-lookup"><span data-stu-id="f0afa-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="f0afa-233">Аналогично можно обслуживать контент из любого действия контроллера в облачной службе посредством Azure CDN с использованием нужного параметра кэширования.</span><span class="sxs-lookup"><span data-stu-id="f0afa-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="f0afa-234">В следующем разделе будет показано, как обслуживать объединенные в пакет и минифицированные скрипты и CSS посредством Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="f0afa-235">Интеграция объединения и минификации ASP.NET с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="f0afa-236">Скрипты и таблицы стилей CSS изменяются нечасто и являются основными кандидатами для кэша Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="f0afa-237">Обслуживание всей веб-роли посредством Azure CDN представляет простейший способ интеграции объединения и минификации с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="f0afa-238">Однако поскольку вы можете не хотеть это делать, я покажу, как это сделать, сохраняя желаемый интерфейс разработчика объединения и минификации ASP.NET со следующими характеристиками.</span><span class="sxs-lookup"><span data-stu-id="f0afa-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="f0afa-239">Отличное взаимодействие в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="f0afa-239">Great debug mode experience</span></span>
* <span data-ttu-id="f0afa-240">Упрощенное развертывание.</span><span class="sxs-lookup"><span data-stu-id="f0afa-240">Streamlined deployment</span></span>
* <span data-ttu-id="f0afa-241">Немедленные обновления клиентов при обновлении версий скриптов или CSS.</span><span class="sxs-lookup"><span data-stu-id="f0afa-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="f0afa-242">Резервный механизм на случай сбоя конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="f0afa-243">Минимальное изменение кода.</span><span class="sxs-lookup"><span data-stu-id="f0afa-243">Minimize code modification</span></span>

<span data-ttu-id="f0afa-244">В проекте **WebRole1**, созданном при изучении раздела [Интеграция конечной точки Azure CDN с веб-сайтом Azure и обслуживание статического содержимого на веб-страницах из Azure CDN](#deploy), откройте файл *App_Start\BundleConfig.cs* и взгляните на вызовы метода `bundles.Add()`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="f0afa-245">Первая инструкция `bundles.Add()` добавляет пакет скриптов в виртуальный каталог `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="f0afa-246">Затем откройте файл *Views\Shared\_Layout.cshtml*, чтобы просмотреть, как обрабатывается тег пакета скриптов.</span><span class="sxs-lookup"><span data-stu-id="f0afa-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="f0afa-247">Вы должны найти следующую строку кода Razor:</span><span class="sxs-lookup"><span data-stu-id="f0afa-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="f0afa-248">При запуске этого кода Razor в веб-роли Azure он будет обрабатывать тег `<script>` для пакета скриптов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f0afa-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="f0afa-249">Однако, когда этот код запускается в Visual Studio путем нажатия клавиши `F5`, он будет обрабатывать каждый файл скрипта в пакете индивидуально (в вышеприведенном случае в пакете имеется только один файл скрипта):</span><span class="sxs-lookup"><span data-stu-id="f0afa-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="f0afa-250">Это позволяет отлаживать код JavaScript в среде разработки, уменьшая число параллельных клиентских соединений (объединение) и улучшая производительность загрузки файлов (минификация) в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f0afa-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="f0afa-251">Это отличная возможность для сохранения с использованием интеграции Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="f0afa-252">Более того, поскольку обработанный пакет уже содержит автоматически созданную строку версии, имеет смысл реплицировать эту функциональность, чтобы при всяком обновлении версии jQuery с помощью NuGet она могла бы максимально быстро обновляться на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f0afa-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="f0afa-253">Выполните приведенные ниже действия для интеграции объединения и минификации ASP.NET с конечной точкой CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="f0afa-254">Вернитесь в файл *App_Start\BundleConfig.cs* и измените методы `bundles.Add()`, чтобы использовать другой [конструктор Bundle](http://msdn.microsoft.com/library/jj646464.aspx), который задает адрес CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="f0afa-255">Для этого замените определение метода `RegisterBundles` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="f0afa-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="f0afa-256">Не забудьте заменить `<yourCDNName>` своим именем Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="f0afa-257">Простыми словами, устанавливается `bundles.UseCdn = true` и добавляется тщательно созданный URL-адрес CDN в каждый пакет.</span><span class="sxs-lookup"><span data-stu-id="f0afa-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="f0afa-258">Например, первый конструктор в коде</span><span class="sxs-lookup"><span data-stu-id="f0afa-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="f0afa-259">тот же самый:</span><span class="sxs-lookup"><span data-stu-id="f0afa-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="f0afa-260">Этот конструктор указывает, что при локальной отладке с помощью объединения и минификации ASP.NET должна выполняться обработка отдельных файлов скриптов, но с использованием указанного адреса CDN для доступа к соответствующему скрипту.</span><span class="sxs-lookup"><span data-stu-id="f0afa-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="f0afa-261">Однако отметим две важных характеристики этого тщательно созданного URL-адреса CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="f0afa-262">Источником этого URL-адреса CDN служит адрес `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, который фактически является виртуальным каталогом пакета сценариев в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="f0afa-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="f0afa-263">Поскольку используется конструктор CDN, тег скрипта CDN для этого пакета больше не содержит автоматически созданную строку версии в обработанном URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="f0afa-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="f0afa-264">Необходимо вручную создавать уникальную строку версии каждый раз при изменении пакета скриптов, чтобы обеспечить промах кэша в Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="f0afa-265">В то же время эта уникальная строка версии должна оставаться постоянной в течение всего срока существования развертывания для максимального увеличения попаданий в кэш в Azure CDN после развертывания пакета.</span><span class="sxs-lookup"><span data-stu-id="f0afa-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="f0afa-266">Строка запросов v=<W.X.Y.Z> получена из файла *Properties\AssemblyInfo.cs* в проекте веб-роли.</span><span class="sxs-lookup"><span data-stu-id="f0afa-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="f0afa-267">Можно создать рабочий процесс развертывания, включающий увеличение версии сборки при каждой публикации в Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afa-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="f0afa-268">Вы также можете просто изменить файл *Properties\AssemblyInfo.cs* в проекте, задав автоматическое увеличение строки версии при каждом построении с помощью подстановочного знака "*".</span><span class="sxs-lookup"><span data-stu-id="f0afa-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="f0afa-269">Например:</span><span class="sxs-lookup"><span data-stu-id="f0afa-269">For example:</span></span>
     
        <span data-ttu-id="f0afa-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="f0afa-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="f0afa-271">Здесь будет работать любая другая стратегия упрощения создания уникальной строки на срок существования развертывания.</span><span class="sxs-lookup"><span data-stu-id="f0afa-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="f0afa-272">Повторно опубликуйте облачную службу и откройте домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="f0afa-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="f0afa-273">Просмотрите код HTML для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="f0afa-273">View the HTML code for the page.</span></span> <span data-ttu-id="f0afa-274">При каждой публикации изменений облачной службы вы должны видеть обработанный URL-адрес CDN с уникальной строкой версии.</span><span class="sxs-lookup"><span data-stu-id="f0afa-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="f0afa-275">Например:</span><span class="sxs-lookup"><span data-stu-id="f0afa-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="f0afa-276">Перейдите в режим отладки облачной службы в Visual Studio, нажав клавишу `F5`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="f0afa-277">Просмотрите код HTML для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="f0afa-277">View the HTML code for the page.</span></span> <span data-ttu-id="f0afa-278">Вы по-прежнему будете видеть каждый, индивидуально обработанный файл скрипта, так что можно получить последовательные возможности отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0afa-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="f0afa-279">Резервный механизм для URL-адресов CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="f0afa-280">Желательно, чтобы в случае сбоя конечной точки Azure CDN по какой-либо причине веб-страница могла использовать в качестве резервной возможности доступ к исходному веб-серверу для загрузки JavaScript или Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="f0afa-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="f0afa-281">Одно дело – потерять изображения на веб-сайте из-за недоступности CDN, и совсем другое – потерять критически важные функциональные возможности страницы, обеспечиваемые сценариями и таблицами стилей.</span><span class="sxs-lookup"><span data-stu-id="f0afa-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="f0afa-282">Класс [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) содержит свойство с именем [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx), которое позволяет настраивать резервный механизм на случай сбоя CDN.</span><span class="sxs-lookup"><span data-stu-id="f0afa-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="f0afa-283">Для использования этого свойства выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f0afa-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="f0afa-284">В проекте веб-роли откройте файл *App_Start\BundleConfig.cs*, где в каждом [конструкторе Bundle](http://msdn.microsoft.com/library/jj646464.aspx) добавен URL-адрес CDN, и внесите следующие выделенные изменения, чтобы добавить резервный механизм в пакеты по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f0afa-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="f0afa-285">Когда выражение `CdnFallbackExpression` не пустое, скрипт внедряется в HTML, чтобы проверить успешность загрузки пакета, и в случае неуспешной загрузки обеспечивает доступ к пакету непосредственно на исходном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="f0afa-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="f0afa-286">В этом свойстве необходимо устанавливать выражение JavaScript, проверяющее, загружен ли соответствующий пакет CDN должным образом.</span><span class="sxs-lookup"><span data-stu-id="f0afa-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="f0afa-287">Выражения для проверки каждого пакета отличаются в соответствии с контентом.</span><span class="sxs-lookup"><span data-stu-id="f0afa-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="f0afa-288">Для пакетов по умолчанию выше:</span><span class="sxs-lookup"><span data-stu-id="f0afa-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="f0afa-289">`window.jquery` задается в jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="f0afa-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="f0afa-290">`$.validator` задается в jquery.validate.js;</span><span class="sxs-lookup"><span data-stu-id="f0afa-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="f0afa-291">`window.Modernizr` задается в modernizer-{version}.js;</span><span class="sxs-lookup"><span data-stu-id="f0afa-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="f0afa-292">`$.fn.modal` задается в bootstrap.js.</span><span class="sxs-lookup"><span data-stu-id="f0afa-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="f0afa-293">Возможно, вы заметили, что я не установил CdnFallbackExpression для пакета `~/Cointent/css` .</span><span class="sxs-lookup"><span data-stu-id="f0afa-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="f0afa-294">Это объясняется тем, что в настоящее время имеется [ошибка в System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104), которая вставляет тег `<script>` для резервной CSS вместо ожидаемого тега `<link>`.</span><span class="sxs-lookup"><span data-stu-id="f0afa-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="f0afa-295">Однако существует хорошая [резервная форма пакета стилей](https://github.com/EmberConsultingGroup/StyleBundleFallback), предлагаемая [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="f0afa-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="f0afa-296">Чтобы использовать этот обходной путь для CSS, создайте в папке *App_Start* CS-файл *StyleBundleExtensions.cs* и замените его содержимое [кодом с сайта GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="f0afa-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="f0afa-297">В *App_Start\StyleFundleExtensions.cs* измените имя пространства имен на имя веб-роли (например, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="f0afa-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="f0afa-298">Вернитесь в файл `App_Start\BundleConfig.cs` и замените последний оператор `bundles.Add` следующим выделенным кодом:</span><span class="sxs-lookup"><span data-stu-id="f0afa-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="f0afa-299">Этот новый метод расширения использует ту же идею внедрения скрипта в HTML для поиска в модели DOM имени класса, имени правила и значения правила, соответствующих заданным в пакете CSS, и возвращения на исходный веб-сервер при отсутствии соответствия.</span><span class="sxs-lookup"><span data-stu-id="f0afa-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="f0afa-300">Снова опубликуйте облачную службу и откройте домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="f0afa-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="f0afa-301">Просмотрите код HTML для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="f0afa-301">View the HTML code for the page.</span></span> <span data-ttu-id="f0afa-302">Вы должны найти внедренные скрипты, аналогичные показанным ниже.</span><span class="sxs-lookup"><span data-stu-id="f0afa-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="f0afa-303">Обратите внимание, что внедренный скрипт для пакета CSS по-прежнему содержит ошибочный фрагмент из свойства `CdnFallbackExpression` в следующей строке:</span><span class="sxs-lookup"><span data-stu-id="f0afa-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="f0afa-304">Но поскольку первая часть выражения '||' будет всегда возвращать значение true (в строке прямо над этой), функция document.write() никогда не будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="f0afa-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="f0afa-305">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="f0afa-305">More Information</span></span>
* [<span data-ttu-id="f0afa-306">Общие сведения о сети доставки контента (CDN) Azure</span><span class="sxs-lookup"><span data-stu-id="f0afa-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="f0afa-307">Использование Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f0afa-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="f0afa-308">Объединение и минификация ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f0afa-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
