---
title: "aaaIntegrate облачной службы Azure с Azure CDN | Документы Microsoft"
description: "Узнайте, как toodeploy облачной службы, служит содержимое из конечной точке integrated Azure CDN"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="73c04-103"><a name="intro"></a>Интеграция облачной службы с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="73c04-104">Облачные службы могут интегрироваться с Azure CDN обслуживает все содержимое из расположения hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="73c04-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="73c04-105">Этот подход обеспечивает hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="73c04-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="73c04-106">Упрощение развертывания и обновления образов, скриптов и таблиц стилей в каталогах проекта облачной службы.</span><span class="sxs-lookup"><span data-stu-id="73c04-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="73c04-107">Легко обновите пакеты NuGet hello в облачной службе, например jQuery или начальной загрузки версии</span><span class="sxs-lookup"><span data-stu-id="73c04-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="73c04-108">Управление веб-приложения и обслуживаться CDN вашей содержимого всех hello же интерфейс Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73c04-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="73c04-109">Единый рабочий процесс развертывания для веб-приложения и контента, обслуживаемого CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="73c04-110">Интеграция объединения и минификации ASP.NET с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="73c04-111">Новые знания</span><span class="sxs-lookup"><span data-stu-id="73c04-111">What you will learn</span></span>
<span data-ttu-id="73c04-112">Из этого учебника вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="73c04-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="73c04-113">Интеграция конечной точки Azure CDN с облачной службой и обслуживание статического содержимого на веб-страницах из Azure CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="73c04-114">Настройка параметров кэша для статического содержимого в облачной службе</span><span class="sxs-lookup"><span data-stu-id="73c04-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="73c04-115">Обслуживание содержимого из действий контроллера с помощью Azure CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="73c04-116">Serve объединено и уменьшена содержимого с помощью Azure CDN, сохраняя hello сценария отладки в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73c04-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="73c04-117">Настройка резервирования сценариев и CSS, когда Azure CDN находится в автономном режиме</span><span class="sxs-lookup"><span data-stu-id="73c04-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="73c04-118">Что будет строиться</span><span class="sxs-lookup"><span data-stu-id="73c04-118">What you will build</span></span>
<span data-ttu-id="73c04-119">Развертывание веб-роли облачной службы с помощью hello шаблон по умолчанию ASP.NET MVC, добавлять содержимое tooserve код из интеграции CDN Azure, такие как изображения, результаты действий контроллера и файлы JavaScript и CSS по умолчанию hello и также написать код tooconfigure hello резервный механизм для пакетов, выполненных в событии hello, hello CDN находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="73c04-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="73c04-120">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="73c04-120">What you will need</span></span>
<span data-ttu-id="73c04-121">Этот учебник содержит hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="73c04-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="73c04-122">Активная [учетная запись Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="73c04-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="73c04-123">Наличие Visual Studio 2015 с [пакетом SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="73c04-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="73c04-124">Требуется учетная запись Azure toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="73c04-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="73c04-125">Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) -вы получаете кредиты можно использовать tootry out платных служб Azure и даже после того, они используются до можно защитить учетную запись hello и используйте освободить служб Azure, таких как веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="73c04-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="73c04-126">Вы имеете возможность [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты за службы Azure.</span><span class="sxs-lookup"><span data-stu-id="73c04-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="73c04-127">Развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="73c04-127">Deploy a cloud service</span></span>
<span data-ttu-id="73c04-128">В этом разделе развертывания по умолчанию hello шаблона приложения ASP.NET MVC в Visual Studio 2015 tooa облака службы веб-роли и затем интегрировать ее с новой конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="73c04-129">Выполните приведенные ниже инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="73c04-130">В Visual Studio 2015, создайте новой облачной службы Azure на панели меню hello выбрав слишком**файл > Создать > проект > облака > облачная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="73c04-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="73c04-131">Назначьте ей имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="73c04-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="73c04-132">Выберите **веб-роли ASP.NET** и нажмите кнопку hello  **>**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="73c04-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="73c04-133">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="73c04-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="73c04-134">Выберите **MVC** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="73c04-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="73c04-135">Теперь опубликуйте этот tooan роли Web облачной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="73c04-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="73c04-136">Щелкните правой кнопкой мыши проект облачной службы hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="73c04-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="73c04-137">Если вы еще не вошли в Microsoft Azure, щелкните hello **добавить учетную запись...**  hello раскрывающегося списка и нажмите кнопку **добавить учетную запись** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="73c04-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="73c04-138">В hello страницы входа войдите с использованием hello учетной записи Майкрософт, используемых tooactivate учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="73c04-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="73c04-139">После выполнения входа нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="73c04-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="73c04-140">Если облачная служба или учетная запись хранения еще не создана, Visual Studio поможет создать их.</span><span class="sxs-lookup"><span data-stu-id="73c04-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="73c04-141">В hello **Создание облачной службы и учетной записи** диалогового окна, требуемой службы имя типа hello и hello выберите нужный регион.</span><span class="sxs-lookup"><span data-stu-id="73c04-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="73c04-142">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="73c04-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="73c04-143">Hello страница параметров публикации, проверьте конфигурацию hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="73c04-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="73c04-144">процесс публикации Hello для облачных служб занимает много времени.</span><span class="sxs-lookup"><span data-stu-id="73c04-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="73c04-145">Hello включить веб-развертывание для всех ролей может сделать отладку намного быстрее, поскольку облачной службы, предоставляя tooyour быстрого (но временные) обновления веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="73c04-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="73c04-146">Дополнительные сведения об этом параметре см. в разделе [публикация облачной службы с помощью средства Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="73c04-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="73c04-147">Здравствуйте, когда **журнал действий Microsoft Azure** показывает, что состояние публикации **завершено**, создании конечной точки CDN, которое интегрировано с этой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="73c04-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="73c04-148">Если после публикации, hello развертывания облачной службы отображает экран ошибки, вполне вероятно, так как использует hello облачной службы после развертывания [гостевой ОС, которая не включает .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="73c04-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="73c04-149">Чтобы устранить эту проблему, [разверните .NET 4.5.2 в качестве задачи запуска](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="73c04-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="73c04-150">Создание нового профиля сети CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-150">Create a new CDN profile</span></span>
<span data-ttu-id="73c04-151">Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="73c04-152">Каждый профиль содержит одну или несколько конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="73c04-153">Вы можете toouse несколько профилей tooorganize конечными точками CDN с Интернет-домен, веб-приложения или некоторых других критериев.</span><span class="sxs-lookup"><span data-stu-id="73c04-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="73c04-154">Если уже имеется профиль CDN, что требуется toouse для этого учебника, перейдите в слишком[создания новой конечной точки CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="73c04-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="73c04-155">Создание новой конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="73c04-156">**toocreate новой конечной точки CDN для вашей учетной записи**</span><span class="sxs-lookup"><span data-stu-id="73c04-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="73c04-157">В hello [портала управления Azure](https://portal.azure.com), перейдите tooyour профиля CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="73c04-158">Может закрепленной его toohello панели мониторинга в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="73c04-159">Если вы не, можно найти его, нажав кнопку **Обзор**, затем **CDN профилей**, и щелкнув профиля hello планируется tooadd для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="73c04-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="73c04-160">Откроется колонка профиля CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-160">hello CDN profile blade appears.</span></span>
   
    ![Профиль сети CDN][cdn-profile-settings]
2. <span data-ttu-id="73c04-162">Нажмите кнопку hello **добавить конечную точку** кнопки.</span><span class="sxs-lookup"><span data-stu-id="73c04-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    <span data-ttu-id="73c04-164">Hello **добавить конечную точку** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="73c04-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. <span data-ttu-id="73c04-166">Введите **имя** конечной точки сети CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="73c04-167">Это имя будет использоваться tooaccess кэшированные ресурсы в домене hello `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="73c04-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="73c04-168">В hello **тип источника** раскрывающийся список, выберите *облачная служба*.</span><span class="sxs-lookup"><span data-stu-id="73c04-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="73c04-169">В hello **имя узла источника** раскрывающийся список, выберите вашу облачную службу.</span><span class="sxs-lookup"><span data-stu-id="73c04-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="73c04-170">Оставьте значения по умолчанию hello для **исходный путь**, **заголовок исходного узла**, и **порта протокола/источника**.</span><span class="sxs-lookup"><span data-stu-id="73c04-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="73c04-171">Необходимо указать хотя бы один протокол (HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="73c04-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="73c04-172">Нажмите кнопку hello **добавить** toocreate кнопку hello новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="73c04-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="73c04-173">После создания конечной точки hello, он отображается в списке конечных точек для профиля hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="73c04-174">представления списка Hello показывает, что tooaccess toouse hello URL-адрес в кэше содержимого, а также hello исходный домен.</span><span class="sxs-lookup"><span data-stu-id="73c04-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Конечная точка сети CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="73c04-176">Hello конечной точки не будет сразу же доступны для использования.</span><span class="sxs-lookup"><span data-stu-id="73c04-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="73c04-177">Он может занять too90 минут toopropagate hello регистрации через сеть CDN hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="73c04-178">Пользователям, пытающимся имени домена CDN hello toouse немедленно может появиться код состояния 404, пока не будет доступно через hello CDN hello содержимое.</span><span class="sxs-lookup"><span data-stu-id="73c04-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="73c04-179">Тест hello конечной точки CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="73c04-180">При hello, статус публикации **завершено**, откройте окно браузера и перейдите слишком**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="73c04-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="73c04-181">В моей настройке это следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="73c04-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="73c04-182">Соответствующий URL-адреса источника в конечной точке CDN hello toohello:</span><span class="sxs-lookup"><span data-stu-id="73c04-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="73c04-183">При переходе слишком**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, в зависимости от браузера будет toodownload запрос или откройте hello bootstrap.css, откуда опубликованных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="73c04-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="73c04-184">Аналогичным образом можно получать доступ к любому общедоступному URL-адресу в **http://*&lt;serviceName>*.cloudapp.net/** прямо из конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="73c04-185">Например:</span><span class="sxs-lookup"><span data-stu-id="73c04-185">For example:</span></span>

* <span data-ttu-id="73c04-186">JS-файла из пути/Script hello</span><span class="sxs-lookup"><span data-stu-id="73c04-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="73c04-187">Любой файл содержимого из hello /Content путь</span><span class="sxs-lookup"><span data-stu-id="73c04-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="73c04-188">к любому контроллеру или действию;</span><span class="sxs-lookup"><span data-stu-id="73c04-188">Any controller/action</span></span>
* <span data-ttu-id="73c04-189">Если строка запроса hello включен на конечную точку CDN, любой URL-адрес со строками запроса</span><span class="sxs-lookup"><span data-stu-id="73c04-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="73c04-190">На самом деле с hello выше конфигурации, можно разместить hello всей облачной службы из  **http://*&lt;cdnName >*.azureedge.net/**. Если после выхода слишком**http://camservice.azureedge.net/ ** получить результат действия hello из дома или индекса.</span><span class="sxs-lookup"><span data-stu-id="73c04-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="73c04-191">Это означает, тем не менее, что это всегда рекомендуется tooserve всей облачной службы через Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="73c04-192">CDN с оптимизацией статических доставки не обязательно ускорять доставки динамических средств, которые предназначены не кэшируются toobe или очень часто обновляются, поскольку hello CDN необходимо получить новую версию средств hello из исходного сервера hello очень часто.</span><span class="sxs-lookup"><span data-stu-id="73c04-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="73c04-193">В этом сценарии можно включить [динамического сайта ускорение](cdn-dynamic-site-acceleration.md) оптимизации (DSA) в вашей конечной точке CDN, который использует различные методы toospeed параметров представления кэширование динамических средств.</span><span class="sxs-lookup"><span data-stu-id="73c04-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="73c04-194">При наличии сайта с сочетание статического и динамического содержимого, вы можете tooserve статическое содержимое из CDN с типом статической оптимизации (например, доставка общие web) и динамического содержимого tooserve непосредственно из исходного сервера hello или через CDN Конечная точка с включенной по случая оптимизацией DSA.</span><span class="sxs-lookup"><span data-stu-id="73c04-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="73c04-195">конец toothat уже было показано, как содержимое отдельных tooaccess файлы из конечной точки CDN hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="73c04-196">Будет показано как tooserve действие конкретного контроллера до конкретной конечной точки CDN в стать содержимого из действия контроллера через Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="73c04-197">Hello альтернативой является toodetermine которого содержимого tooserve из сети доставки Содержимого Azure на основе случая в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="73c04-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="73c04-198">конец toothat уже было показано, как содержимое отдельных tooaccess файлы из конечной точки CDN hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="73c04-199">Будет показано как tooserve действие конкретному контроллеру через hello конечной точки CDN в [обслуживания содержимого из действия контроллера через Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="73c04-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="73c04-200">Настройка параметров кэширования для статических файлов в облачной службе</span><span class="sxs-lookup"><span data-stu-id="73c04-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="73c04-201">Благодаря интеграции Azure CDN в облачной службе можно указать способ статического содержимого toobe кэширования в конечной точке CDN hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="73c04-202">toodo, откройте *Web.config* из веб-роли проекта (например, WebRole1) и добавьте `<staticContent>` элемент слишком`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="73c04-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="73c04-203">Hello XML ниже настраивает tooexpire hello кэша через 3 дня.</span><span class="sxs-lookup"><span data-stu-id="73c04-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="73c04-204">После этого все статические файлы в облачной службе будет контролироваться hello же правило в кэше CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="73c04-205">Для более детального управления параметрами кэша добавьте файл *Web.config* в папку и добавьте в этом месте свои параметры.</span><span class="sxs-lookup"><span data-stu-id="73c04-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="73c04-206">Например, добавить *Web.config* файл toohello *\Content* папки и замены hello содержимое с hello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="73c04-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="73c04-207">Этот параметр вызывает все статические файлы из hello *\Content* toobe папки в кэше в течение 15 дней.</span><span class="sxs-lookup"><span data-stu-id="73c04-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="73c04-208">Дополнительные сведения о том, как tooconfigure hello `<clientCache>` элемент, в разделе [кэш клиента &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="73c04-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="73c04-209">В [обслуживания содержимого из действия контроллера через Azure CDN](#controller), будет также показано как можно настроить параметры кэша для результатов действий контроллера в hello кэша CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="73c04-210">Обслуживание содержимого из действий контроллера с помощью Azure CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="73c04-211">При интеграции веб-роли облачной службы с Azure CDN, это довольно просто tooserve содержимое из действия контроллера через hello Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="73c04-212">Кроме обслуживающий облачной службы напрямую с помощью сети доставки Содержимого Azure (показано выше), [Maarten Balliauw](https://twitter.com/maartenballiauw) показано, как toodo его с интересную MemeGenerator контроллера в [уменьшает задержку на веб-hello с hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="73c04-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="73c04-213">Я просто воспроизведу это здесь.</span><span class="sxs-lookup"><span data-stu-id="73c04-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="73c04-214">Предположим, что в облачную службу нужно на основе образа молодых Norris Чак memes toogenerate (фотографий с [свет Алан](http://www.flickr.com/photos/alan-light/218493788/)) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="73c04-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="73c04-215">У вас есть простой `Index` действие, которое позволяет клиентам hello toospecify hello superlatives в образе hello, затем создает мем hello после их toohello действий, выполняемых после.</span><span class="sxs-lookup"><span data-stu-id="73c04-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="73c04-216">Так как это Norris Чак, можно ожидать этой страницы toobecome очень популярных глобально.</span><span class="sxs-lookup"><span data-stu-id="73c04-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="73c04-217">Это хороший пример обслуживания полудинамического контента с помощью Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="73c04-218">Выполните действия hello выше toosetup этого действия контроллера.</span><span class="sxs-lookup"><span data-stu-id="73c04-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="73c04-219">В hello *\Controllers* папки, создайте новый файл с именем .cs *MemeGeneratorController.cs* и hello замены содержимого с hello следующий код.</span><span class="sxs-lookup"><span data-stu-id="73c04-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="73c04-220">Убедиться, что выделенный фрагмент hello tooreplace быть именем своего CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="73c04-221">Щелкните правой кнопкой мыши по умолчанию hello `Index()` , можно выбрать **добавить представление**.</span><span class="sxs-lookup"><span data-stu-id="73c04-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="73c04-222">Примите следующие параметры hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="73c04-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="73c04-223">Откройте hello новый *Views\MemeGenerator\Index.cshtml* и замените содержимое hello hello, следуя простой HTML для отправки hello superlatives:</span><span class="sxs-lookup"><span data-stu-id="73c04-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="73c04-224">Снова опубликовать облачную службу hello и перейдите слишком**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** в браузере.</span><span class="sxs-lookup"><span data-stu-id="73c04-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="73c04-225">При отправке значения формы hello слишком`/MemeGenerator/Index`, hello `Index_Post` метод действия возвращает toohello ссылку `Show` метод действия с hello соответствующий идентификатор входа.</span><span class="sxs-lookup"><span data-stu-id="73c04-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="73c04-226">Если щелкнуть ссылку hello, достигнете hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="73c04-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="73c04-227">Если ваш локальный отладчик подключен, вы получите hello интерфейса регулярного отладки с помощью локального перенаправления.</span><span class="sxs-lookup"><span data-stu-id="73c04-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="73c04-228">Если он выполняется в облачной службе hello, затем он будет перенаправить на:</span><span class="sxs-lookup"><span data-stu-id="73c04-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="73c04-229">Соответствующее toohello следующий URL-адрес источника в конечную точку CDN:</span><span class="sxs-lookup"><span data-stu-id="73c04-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="73c04-230">Затем можно использовать hello `OutputCacheAttribute` атрибут hello `Generate` toospecify метод кэширования hello результат действия, который будет поддерживать Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="73c04-231">Приведенный ниже код Hello задать истечение срока действия кэша 1 часа (3600 секунд).</span><span class="sxs-lookup"><span data-stu-id="73c04-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="73c04-232">Аналогичным образом вы может служить содержимое из любого действия контроллера в облачной службе через CDN Azure, с hello требуемого параметр кэширования.</span><span class="sxs-lookup"><span data-stu-id="73c04-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="73c04-233">В следующем разделе hello я покажу как tooserve hello объединенными и уменьшена скриптов и CSS через Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="73c04-234">Интеграция объединения и минификации ASP.NET с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="73c04-235">Таблицы стилей, сценарии и CSS подскажет и основной подходят для hello кэша Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="73c04-236">Обслуживание hello весь веб-роли через Azure CDN — самый простой способ toointegrate hello объединение и Минификация с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="73c04-237">Тем не менее как вы не можете toodo это, будет показано как toodo его сохранением hello требуемого develper взаимодействие с ASP.NET объединение и Минификация, такие как:</span><span class="sxs-lookup"><span data-stu-id="73c04-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="73c04-238">Отличное взаимодействие в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="73c04-238">Great debug mode experience</span></span>
* <span data-ttu-id="73c04-239">Упрощенное развертывание.</span><span class="sxs-lookup"><span data-stu-id="73c04-239">Streamlined deployment</span></span>
* <span data-ttu-id="73c04-240">Tooclients немедленного обновления для обновления версий скриптов и CSS</span><span class="sxs-lookup"><span data-stu-id="73c04-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="73c04-241">Резервный механизм на случай сбоя конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="73c04-242">Минимальное изменение кода.</span><span class="sxs-lookup"><span data-stu-id="73c04-242">Minimize code modification</span></span>

<span data-ttu-id="73c04-243">В hello **WebRole1** проекта, созданного в [интегрировать веб-сайте конечной точки Azure CDN и предоставления статического содержимого на веб-страницах из сети доставки Содержимого Azure](#deploy)откройте *App_Start\ BundleConfig.cs* и взгляните на hello `bundles.Add()` вызовы методов.</span><span class="sxs-lookup"><span data-stu-id="73c04-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="73c04-244">Здравствуйте, сначала `bundles.Add()` инструкция добавляет пакет скрипта в виртуальный каталог hello `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="73c04-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="73c04-245">Затем откройте *представления\общие\_Layout.cshtml* toosee просмотру hello тег пакета.</span><span class="sxs-lookup"><span data-stu-id="73c04-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="73c04-246">Необходимо будет toofind hello, следующей строкой кода Razor.</span><span class="sxs-lookup"><span data-stu-id="73c04-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="73c04-247">При выполнении этого кода Razor в hello Azure веб-роли, он будет отображать `<script>` тег для hello скрипт аналогичные toohello следующий пакет:</span><span class="sxs-lookup"><span data-stu-id="73c04-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="73c04-248">Тем не менее, при запуске в Visual Studio, введя `F5`, он будет отображать каждого файла скрипта в пакет hello по отдельности (в случае hello выше, только один файл скрипта находится в пакет hello):</span><span class="sxs-lookup"><span data-stu-id="73c04-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="73c04-249">Это позволит вам код JavaScript toodebug hello в среде разработки во время сократить число одновременных клиентских подключений (объединение) и файл повышение загрузки производительности (минификации) в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="73c04-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="73c04-250">Это прекрасная возможность toopreserve с интеграцией Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="73c04-251">Кроме того, так как к просмотру hello пакет уже содержит автоматически созданную версию строки, вы найдете tooreplicate, функциональные возможности hello, поэтому всякий раз при обновлении версии jQuery через NuGet, его можно обновить на стороне клиента hello как можно скорее невозможно.</span><span class="sxs-lookup"><span data-stu-id="73c04-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="73c04-252">Выполните действия hello ниже toointegration ASP.NET объединение и Минификация с конечной точкой CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="73c04-253">Обратно в *App_Start\BundleConfig.cs*, изменить hello `bundles.Add()` toouse методы другой [конструктор пакета](http://msdn.microsoft.com/library/jj646464.aspx), один задает адрес CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="73c04-254">toodo, замените hello `RegisterBundles` определения метода с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="73c04-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="73c04-255">Убедиться, что tooreplace быть `<yourCDNName>` с именем hello Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="73c04-256">Своими словами, вы настраиваете `bundles.UseCdn = true` и добавлен набор tooeach аккуратно созданные URL-адрес CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="73c04-257">Например hello первый конструктор в коде hello:</span><span class="sxs-lookup"><span data-stu-id="73c04-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="73c04-258">hello такой же, как:</span><span class="sxs-lookup"><span data-stu-id="73c04-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="73c04-259">Этот конструктор сообщает ASP.NET объединение и Минификация toorender конкретные файлы сценариев при отладке локально, но использование hello указан CDN адрес tooaccess hello скрипта в вопросе.</span><span class="sxs-lookup"><span data-stu-id="73c04-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="73c04-260">Однако отметим две важных характеристики этого тщательно созданного URL-адреса CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="73c04-261">Hello источник для этого URL-адрес CDN: `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, который является фактически hello виртуального каталога пакет сценария hello в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="73c04-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="73c04-262">Так как вы используете конструктор CDN, hello тега script CDN для пакета hello больше не содержит строку версии hello автоматически создается в hello, просмотру URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="73c04-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="73c04-263">Необходимо вручную создать строку уникальной версии каждый раз пакет сценария hello измененный tooforce промахом кэша в Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="73c04-264">AT hello же времени, эта строка уникальной версии должны оставаться постоянным объемах hello попаданий в кэш toomaximize hello развертывания в вашей сети доставки Содержимого Azure после развертывания пакета hello.</span><span class="sxs-lookup"><span data-stu-id="73c04-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="73c04-265">Здравствуйте, строки запроса v = < W.X.Y.Z > переносит из *Properties\AssemblyInfo.cs* в проект веб-роли.</span><span class="sxs-lookup"><span data-stu-id="73c04-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="73c04-266">Рабочий процесс развертывания, включающий увеличение версии сборки hello при каждой публикации tooAzure может иметь.</span><span class="sxs-lookup"><span data-stu-id="73c04-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="73c04-267">Либо можно просто изменить *Properties\AssemblyInfo.cs* в строке версии проекта tooautomatically приращения hello каждый раз при построении с помощью hello подстановочный знак "*".</span><span class="sxs-lookup"><span data-stu-id="73c04-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="73c04-268">Например:</span><span class="sxs-lookup"><span data-stu-id="73c04-268">For example:</span></span>
     
        <span data-ttu-id="73c04-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="73c04-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="73c04-270">Здесь будут работать другие toostreamline стратегии, создания уникальной строки для hello жизненного цикла развертывания.</span><span class="sxs-lookup"><span data-stu-id="73c04-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="73c04-271">Повторная публикация hello облачной службы и доступ hello домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="73c04-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="73c04-272">Здравствуйте, представление кода HTML для страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="73c04-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="73c04-273">Должно быть hello может toosee URL-адрес CDN к просмотру со строкой уникальной версии каждый раз при повторной публикации изменений tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="73c04-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="73c04-274">Например:</span><span class="sxs-lookup"><span data-stu-id="73c04-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="73c04-275">В Visual Studio отлаживать hello облачной службы в Visual Studio, введя `F5`.,</span><span class="sxs-lookup"><span data-stu-id="73c04-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="73c04-276">Здравствуйте, представление кода HTML для страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="73c04-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="73c04-277">Вы по-прежнему будете видеть каждый, индивидуально обработанный файл скрипта, так что можно получить последовательные возможности отладки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73c04-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="73c04-278">Резервный механизм для URL-адресов CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="73c04-279">Конечная точка Azure CDN завершается ошибкой по любой причине, их нужно вашей веб-странице toobe смарт-недостаточно tooaccess на исходном веб-сервере как hello резервный вариант для загрузки JavaScript или начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="73c04-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="73c04-280">Это достаточно серьезной toolose изображений на веб-сайт из-за недоступности tooCDN, но гораздо более серьезные toolose важные страницы, предоставляемой средой скриптов и таблиц стилей.</span><span class="sxs-lookup"><span data-stu-id="73c04-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="73c04-281">Hello [пакета](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) класс содержит свойство с именем [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) , которые позволяют tooconfigure hello резервный механизм для сбоя CDN.</span><span class="sxs-lookup"><span data-stu-id="73c04-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="73c04-282">toouse это свойство, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="73c04-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="73c04-283">В проекте веб-роли откройте *App_Start\BundleConfig.cs*, где вы добавили URL-адрес CDN в каждом [конструктор пакета](http://msdn.microsoft.com/library/jj646464.aspx)и сделать выделенный ниже hello изменяет toohello резервный механизм tooadd по умолчанию пакеты:</span><span class="sxs-lookup"><span data-stu-id="73c04-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="73c04-284">Когда `CdnFallbackExpression` — не равно null, скрипт вставляется в tootest hello HTML ли успешно загружен пакет hello и, в противном случае доступ к hello пакета непосредственно из hello исходном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="73c04-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="73c04-285">Это свойство должно toobe набор tooa выражение JavaScript, которое проверяет, является ли hello соответствующих CDN пакета загружается надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="73c04-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="73c04-286">выражение Hello необходимости tootest соответствующим toohello содержимого отличается в каждом пакете.</span><span class="sxs-lookup"><span data-stu-id="73c04-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="73c04-287">Для пакетов по умолчанию hello выше:</span><span class="sxs-lookup"><span data-stu-id="73c04-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="73c04-288">`window.jquery` задается в jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="73c04-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="73c04-289">`$.validator` задается в jquery.validate.js;</span><span class="sxs-lookup"><span data-stu-id="73c04-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="73c04-290">`window.Modernizr` задается в modernizer-{version}.js;</span><span class="sxs-lookup"><span data-stu-id="73c04-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="73c04-291">`$.fn.modal` задается в bootstrap.js.</span><span class="sxs-lookup"><span data-stu-id="73c04-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="73c04-292">Вы могли заметить, что я не задано CdnFallbackExpression для hello `~/Cointent/css` пакета.</span><span class="sxs-lookup"><span data-stu-id="73c04-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="73c04-293">Это, поскольку в настоящее время имеется [ошибку в System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) , внедряет `<script>` тег для hello ожидается резервной CSS вместо hello `<link>` тег.</span><span class="sxs-lookup"><span data-stu-id="73c04-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="73c04-294">Однако существует хорошая [резервная форма пакета стилей](https://github.com/EmberConsultingGroup/StyleBundleFallback), предлагаемая [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="73c04-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="73c04-295">возможное решение hello toouse для CSS, создайте новый CS-файл в проект веб-роли *App_Start* папку с именем *StyleBundleExtensions.cs*и замените его содержимое hello [код из GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="73c04-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="73c04-296">В *App_Start\StyleFundleExtensions.cs*, переименовать tooyour веб-приветствия имен роли (например **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="73c04-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="73c04-297">Возврат слишком`App_Start\BundleConfig.cs` и последнего изменения hello `bundles.Add` инструкции с hello следующий выделенный код:</span><span class="sxs-lookup"><span data-stu-id="73c04-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="73c04-298">Этот новый метод расширения используется hello же идеи tooinject сценария в DOM hello toocheck hello HTML для hello соответствующим именем класса, имя правила и значение правила, определенные в CSS пакета hello и Web приходится задней toohello исходного сервера в случае неудачи toofind hello соответствия.</span><span class="sxs-lookup"><span data-stu-id="73c04-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="73c04-299">Опубликуйте снова hello облачную службу и доступ hello домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="73c04-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="73c04-300">Здравствуйте, представление кода HTML для страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="73c04-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="73c04-301">Вы должны найти примерно следующие toohello подставляемого сценариев:</span><span class="sxs-lookup"><span data-stu-id="73c04-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="73c04-302">Обратите внимание, что внедренный сценарий для пакета hello CSS по-прежнему содержит hello умыслу оставшейся из hello `CdnFallbackExpression` свойства в строке приветствия:</span><span class="sxs-lookup"><span data-stu-id="73c04-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="73c04-303">Но, поскольку первая часть hello hello || выражение всегда будет возвращать значение true (в строке приветствия непосредственно над ней), функция document.write() hello никогда не будет работать.</span><span class="sxs-lookup"><span data-stu-id="73c04-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="73c04-304">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="73c04-304">More Information</span></span>
* [<span data-ttu-id="73c04-305">Общие сведения о hello Azure доставки содержимого сети (CDN)</span><span class="sxs-lookup"><span data-stu-id="73c04-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="73c04-306">Использование Azure CDN</span><span class="sxs-lookup"><span data-stu-id="73c04-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="73c04-307">Объединение и минификация ASP.NET</span><span class="sxs-lookup"><span data-stu-id="73c04-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
