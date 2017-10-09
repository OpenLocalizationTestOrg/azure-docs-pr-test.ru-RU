---
title: "aaaSet копирование промежуточных сред для веб-приложений в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как toouse промежуточное публикации для веб-приложений в службе приложений Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="85552-103">Настройка промежуточных сред в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="85552-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="85552-104">При развертывании вашего веб-приложения, веб-приложения на мобильных серверной части и приложения API Linux слишком[службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714), можно развернуть tooa отдельный слот развертывания вместо производственный слот по умолчанию hello при работе в hello **стандарт**или **Premium** режиме плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="85552-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="85552-105">Слоты развертывания фактически являются динамическими приложениями со своими собственными именами узлов.</span><span class="sxs-lookup"><span data-stu-id="85552-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="85552-106">Элементы содержимого и конфигурации приложения можно переключать между двумя слотами развертывания, включая производственный слот hello.</span><span class="sxs-lookup"><span data-stu-id="85552-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="85552-107">Развертывание ваш слот развертывания приложения tooa имеет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="85552-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="85552-108">Можно проверить изменения приложения в промежуточном слоте развертывания, прежде чем переключаться hello производственный слот.</span><span class="sxs-lookup"><span data-stu-id="85552-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="85552-109">Сначала развертывание разъем tooa приложения и переключаться на производственный гарантирует активированию перед идет переключение в рабочей среде все экземпляры слота hello.</span><span class="sxs-lookup"><span data-stu-id="85552-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="85552-110">Это позволит вам избежать простоя при развертывании приложения.</span><span class="sxs-lookup"><span data-stu-id="85552-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="85552-111">Hello перенаправление трафика не вызывает затруднений, а запросы не теряются в результате операций переключения.</span><span class="sxs-lookup"><span data-stu-id="85552-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="85552-112">Весь этот рабочий процесс можно автоматизировать, настроив функцию [автоматического переноса](#Auto-Swap) , когда проверка перед переносом не требуется.</span><span class="sxs-lookup"><span data-stu-id="85552-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="85552-113">После переключения hello слот с ранее подготовленный приложение теперь имеет предыдущего рабочего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="85552-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="85552-114">Если изменения hello в производственный слот hello не соответствуют ожидаемым вы, можно выполнить приветствия же замены немедленно tooget вашей «последнего проверенного узла» резервное.</span><span class="sxs-lookup"><span data-stu-id="85552-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="85552-115">Каждый режим плана службы приложений поддерживает разное количество слотов развертывания.</span><span class="sxs-lookup"><span data-stu-id="85552-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="85552-116">поддерживает режим приложения toofind out hello Число слотов см. в разделе [цены на службу приложения](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="85552-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="85552-117">Если приложение имеет несколько слотов, нельзя изменить режим hello.</span><span class="sxs-lookup"><span data-stu-id="85552-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="85552-118">Масштабирование для веб-сайтов, не находящихся в производственной области, недоступно.</span><span class="sxs-lookup"><span data-stu-id="85552-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="85552-119">Для непроизводственных областей управление связанными ресурсами недоступно.</span><span class="sxs-lookup"><span data-stu-id="85552-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="85552-120">В hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715) только это потенциальное воздействие на производственный слот можно избежать, временно перемещение hello не производственный слот tooa другого приложения службы плана режима.</span><span class="sxs-lookup"><span data-stu-id="85552-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="85552-121">Примечание, слот нерабочей hello снова должны совместно использовать hello же режим hello производственный слот, прежде чем можно переключить слоты hello двух.</span><span class="sxs-lookup"><span data-stu-id="85552-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="85552-122">Добавление слота развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-122">Add a deployment slot</span></span>
<span data-ttu-id="85552-123">приложение Hello должна быть запущена в hello **Стандартная** или **Premium** режим в порядок tooenable вас несколько слотов развертывания.</span><span class="sxs-lookup"><span data-stu-id="85552-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="85552-124">В hello [портала Azure](https://portal.azure.com/), откройте ваше приложение [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="85552-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="85552-125">Выберите hello **слоты развертывания** параметр, а затем нажмите кнопку **добавить слот**.</span><span class="sxs-lookup"><span data-stu-id="85552-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Добавить новый слот развернутого приложения][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="85552-127">Если приложение hello уже не hello **Стандартная** или **Premium** режиме, вы получите сообщение hello поддерживается режимов, позволяющих включить промежуточную публикацию.</span><span class="sxs-lookup"><span data-stu-id="85552-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="85552-128">На этом этапе, что у вас есть параметр tooselect hello **обновление** и перейдите toohello **шкалы** вкладку приложения перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="85552-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="85552-129">В hello **Добавление слота** , имя слота hello и, при необходимости выберите ли конфигурация tooclone приложения из другого существующего слота развертывания.</span><span class="sxs-lookup"><span data-stu-id="85552-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="85552-130">Щелкните флажок toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="85552-130">Click hello check mark toocontinue.</span></span>
   
    ![Источник конфигурации][ConfigurationSource1]
   
    <span data-ttu-id="85552-132">Hello Добавление слота, первый раз будет имеется только два варианта: конфигурации клона из области по умолчанию hello в рабочей среде или вообще.</span><span class="sxs-lookup"><span data-stu-id="85552-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="85552-133">После создания несколько слотов будут конфигурации может tooclone из слота, кроме одного hello в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="85552-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Источники конфигураций][MultipleConfigurationSources]
4. <span data-ttu-id="85552-135">В свое приложение с колонкой ресурсов, нажмите кнопку **слоты развертывания**, щелкните слот развертывания tooopen колонки ресурсов, область памяти, с набором метрик и конфигурации так же, как любое другое приложение.</span><span class="sxs-lookup"><span data-stu-id="85552-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="85552-136">Hello имя слота hello отображается вверху hello tooremind hello колонку, вы просматриваете hello слот развертывания.</span><span class="sxs-lookup"><span data-stu-id="85552-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Название области развертывания][StagingTitle]
5. <span data-ttu-id="85552-138">Щелкните URL-адрес приложения hello в колонке слот hello.</span><span class="sxs-lookup"><span data-stu-id="85552-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="85552-139">Обратите внимание hello слот развертывания имеет свое имя сервера, а также является динамическим приложением.</span><span class="sxs-lookup"><span data-stu-id="85552-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="85552-140">слот развертывания toohello toolimit общего доступа, в разделе [приложения службы веб-приложения — слоты развертывания рабочей toonon доступа web блока](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="85552-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="85552-141">В созданном слоте развертывания изначально нет содержимого.</span><span class="sxs-lookup"><span data-stu-id="85552-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="85552-142">Вы можете развернуть слот toohello из другого репозитория ветвь или другую системную репозитория.</span><span class="sxs-lookup"><span data-stu-id="85552-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="85552-143">Можно также изменить конфигурацию слота hello.</span><span class="sxs-lookup"><span data-stu-id="85552-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="85552-144">Используйте hello опубликовать профиль или развертывания учетные данные, связанные с hello слот развертывания для обновлений содержимого.</span><span class="sxs-lookup"><span data-stu-id="85552-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="85552-145">Например, вы можете [публикации toothis слот с git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="85552-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="85552-146">Конфигурация слотов развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-146">Configuration for deployment slots</span></span>
<span data-ttu-id="85552-147">При клонировании конфигурации из другой слот развертывания hello клонированных доступен для редактирования.</span><span class="sxs-lookup"><span data-stu-id="85552-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="85552-148">Кроме того некоторые элементы конфигурации, последует содержимое hello через swap (не слот конкретных) пока другие элементы конфигурации будут оставаться в hello же слот после переключения (слот конкретных).</span><span class="sxs-lookup"><span data-stu-id="85552-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="85552-149">Hello следующих списках приведены hello конфигурацию, которая будет изменяться при переключить слоты.</span><span class="sxs-lookup"><span data-stu-id="85552-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="85552-150">**Переносимые параметры**:</span><span class="sxs-lookup"><span data-stu-id="85552-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="85552-151">Общие параметры, например версия платформы, 32/64-разрядная версия, веб-сокеты</span><span class="sxs-lookup"><span data-stu-id="85552-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="85552-152">Параметры приложения (может быть настроенный toostick tooa слот)</span><span class="sxs-lookup"><span data-stu-id="85552-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="85552-153">Строки подключения (может быть настроенный toostick tooa слот)</span><span class="sxs-lookup"><span data-stu-id="85552-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="85552-154">Сопоставления обработчиков</span><span class="sxs-lookup"><span data-stu-id="85552-154">Handler mappings</span></span>
* <span data-ttu-id="85552-155">Настройки диагностики и мониторинга</span><span class="sxs-lookup"><span data-stu-id="85552-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="85552-156">Содержимое веб-заданий</span><span class="sxs-lookup"><span data-stu-id="85552-156">WebJobs content</span></span>

<span data-ttu-id="85552-157">**Непереносимые параметры**:</span><span class="sxs-lookup"><span data-stu-id="85552-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="85552-158">Конечные точки публикации</span><span class="sxs-lookup"><span data-stu-id="85552-158">Publishing endpoints</span></span>
* <span data-ttu-id="85552-159">Имена пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="85552-159">Custom Domain Names</span></span>
* <span data-ttu-id="85552-160">SSL-сертификаты и SSL-привязки</span><span class="sxs-lookup"><span data-stu-id="85552-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="85552-161">Параметры масштабирования</span><span class="sxs-lookup"><span data-stu-id="85552-161">Scale settings</span></span>
* <span data-ttu-id="85552-162">Планировщики веб-заданий</span><span class="sxs-lookup"><span data-stu-id="85552-162">WebJobs schedulers</span></span>

<span data-ttu-id="85552-163">tooconfigure приложения параметр или соединения строки toostick tooa разъем (не перемещаются) hello доступа **параметры приложения** колонку для определенной области памяти, а затем выберите hello **параметр слот** поле для hello элементы конфигурации, которые следует придерживаться слот hello.</span><span class="sxs-lookup"><span data-stu-id="85552-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="85552-164">Обратите внимание, что пометки элемента конфигурации как слот конкретных приводит hello настройке этого элемента в качестве не замены через все слоты развертывания hello, связанные с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="85552-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Параметры слота][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="85552-166">Переключение слотов развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-166">Swap deployment slots</span></span> 
<span data-ttu-id="85552-167">Можно менять слоты развертывания в hello **Обзор** или **слоты развертывания** представление части колонки ресурсов приложения.</span><span class="sxs-lookup"><span data-stu-id="85552-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85552-168">Перед подкачки приложение из слота развертывания в рабочей среде, убедитесь, что все определенные параметры не слот настроены так, как toohave его в целевой области подкачки hello.</span><span class="sxs-lookup"><span data-stu-id="85552-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="85552-169">Слоты развертывания tooswap, щелкните hello **замены** на панели команд hello слота развертывания или в командной строке hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="85552-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Кнопка "Переключить"][SwapButtonBar]

2. <span data-ttu-id="85552-171">Убедитесь в том, hello переключения источника и замены ориентированных указаны правильно.</span><span class="sxs-lookup"><span data-stu-id="85552-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="85552-172">Как правило, hello целевого слота переключения выступает производственный слот hello.</span><span class="sxs-lookup"><span data-stu-id="85552-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="85552-173">Нажмите кнопку **ОК** toocomplete hello операции.</span><span class="sxs-lookup"><span data-stu-id="85552-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="85552-174">По завершении операции hello слоты развертывания hello меняться местами.</span><span class="sxs-lookup"><span data-stu-id="85552-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Полное переключение](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="85552-176">Для hello **переключение с предварительным просмотром** замены типа см. в разделе [переключение с предварительным просмотром (многоэтапный подкачка)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="85552-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="85552-177">Переключение с предварительным просмотром (многофазное переключение)</span><span class="sxs-lookup"><span data-stu-id="85552-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="85552-178">Переключение с предварительным просмотром, называемое также многофазным переключением, упрощает проверку настроек, определяемых слотами, таких как строки подключения.</span><span class="sxs-lookup"><span data-stu-id="85552-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="85552-179">Для критически важных рабочих нагрузок, требуется toovalidate, приложение hello работает надлежащим образом при применении конфигурации hello производственный слот, и необходимо выполнить подобную проверку *перед* приложение hello сбрасывается в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="85552-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="85552-180">Для этого используется переключение с предварительным просмотром.</span><span class="sxs-lookup"><span data-stu-id="85552-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="85552-181">Переключения с предварительным просмотром не поддерживаются в веб-приложениях Linux.</span><span class="sxs-lookup"><span data-stu-id="85552-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="85552-182">При использовании hello **переключения с предварительным просмотром** параметр (см. [переключение слотов развертывания](#Swap)), службы приложения hello следующие:</span><span class="sxs-lookup"><span data-stu-id="85552-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="85552-183">Не влияет на сохраняет hello целевой слот без изменений поэтому существующие рабочей нагрузки на этом слоте (например, производство).</span><span class="sxs-lookup"><span data-stu-id="85552-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="85552-184">Применяет элементы конфигурации hello hello слот toohello источника слоте назначения, включая строки подключения для конкретного слот hello и параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="85552-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="85552-185">Перезапускает hello рабочих процессов на hello исходный слот с помощью этих элементов конфигурации, упомянутых выше.</span><span class="sxs-lookup"><span data-stu-id="85552-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="85552-186">После завершения замены hello: Перемещает hello warmed-up исходный слот в слоте назначения hello.</span><span class="sxs-lookup"><span data-stu-id="85552-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="85552-187">Hello целевого слота, перемещается в исходный слот hello как вручную замены.</span><span class="sxs-lookup"><span data-stu-id="85552-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="85552-188">При отмене hello swap: повторно применяет элементы конфигурации hello hello исходный слот toohello источника слот.</span><span class="sxs-lookup"><span data-stu-id="85552-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="85552-189">Можно просмотреть только приложение hello поведения с помощью конфигурации целевого слота hello.</span><span class="sxs-lookup"><span data-stu-id="85552-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="85552-190">После завершения проверки, выполнения замены hello отдельно.</span><span class="sxs-lookup"><span data-stu-id="85552-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="85552-191">Этот шаг имеет hello дополнительное преимущество hello исходный слот уже активированию с настройкой требуемого hello, что клиенты не будут сталкиваться простоев.</span><span class="sxs-lookup"><span data-stu-id="85552-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="85552-192">Образцы для hello командлетов Azure PowerShell для замены многоэтапный включаются в hello командлетов Azure PowerShell для раздела слотов развертывания.</span><span class="sxs-lookup"><span data-stu-id="85552-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="85552-193">Настройка автоматического переключения</span><span class="sxs-lookup"><span data-stu-id="85552-193">Configure Auto Swap</span></span>
<span data-ttu-id="85552-194">Ускоряет процесс замены автоматически DevOps сценарии, где требуется toocontinuously развернуть приложение с нуля холодный запуск и обеспечит нулевое время простоя для конечных пользователей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="85552-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="85552-195">Когда слот развертывания настроена для автоматического переключения в производственной среде, каждый раз при принудительной гнезда toothat обновление кода, приложение службы автоматически поменяет приложение hello в производственной среде после его уже подготовлен в слоте hello.</span><span class="sxs-lookup"><span data-stu-id="85552-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85552-196">При включении автоматическое переключение для слота убедитесь, что конфигурации слота hello является точно hello конфигурации, предназначенное для hello целевого слота (обычно hello производственный слот).</span><span class="sxs-lookup"><span data-stu-id="85552-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="85552-197">Автоматическое переключение не поддерживается в веб-приложениях Linux.</span><span class="sxs-lookup"><span data-stu-id="85552-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="85552-198">Настроить автоматический перенос для слота очень просто.</span><span class="sxs-lookup"><span data-stu-id="85552-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="85552-199">Выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="85552-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="85552-200">В списке **слотов развертывания** выберите слот, не являющийся рабочим, и выберите **Параметры приложения** в колонке ресурсов этого слота.</span><span class="sxs-lookup"><span data-stu-id="85552-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="85552-201">Выберите **на** для **автоматическое переключение**выберите нужного целевого слота hello в **замены слота автоматического**и нажмите кнопку **Сохранить** hello панели команд.</span><span class="sxs-lookup"><span data-stu-id="85552-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="85552-202">Убедитесь, что конфигурация для слота hello является точно hello предназначен для целевого слота hello.</span><span class="sxs-lookup"><span data-stu-id="85552-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="85552-203">Hello **уведомления** вкладка будет мигать зеленым **успех** после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="85552-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="85552-204">tootest автоматическое переключение для вашего приложения, можно сначала выбрать ячейку в непроизводственной целевой **замены слота автоматического** toobecome знакомы с функцией hello.</span><span class="sxs-lookup"><span data-stu-id="85552-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="85552-205">Выполнение слота развертывания toothat принудительной кода.</span><span class="sxs-lookup"><span data-stu-id="85552-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="85552-206">Через некоторое время происходит автоматического переключения и hello обновления будут отражены в URL-адрес целевого слота.</span><span class="sxs-lookup"><span data-stu-id="85552-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="85552-207">toorollback производственного приложения после переключения</span><span class="sxs-lookup"><span data-stu-id="85552-207">toorollback a production app after swap</span></span>
<span data-ttu-id="85552-208">В случае ошибки в производственной среде после переключения слотов, накат слоты hello задней tootheir до переключения состояния путем замены hello же двух слотов немедленно.</span><span class="sxs-lookup"><span data-stu-id="85552-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="85552-209">Пользовательский прогрев перед заменой</span><span class="sxs-lookup"><span data-stu-id="85552-209">Custom warm-up before swap</span></span>
<span data-ttu-id="85552-210">Некоторые приложения могут потребовать пользовательских действий прогрева перед заменой.</span><span class="sxs-lookup"><span data-stu-id="85552-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="85552-211">Hello `applicationInitialization` элемента конфигурации в файле web.config позволяет вам toospecify пользовательскую инициализацию действий toobe выполнять до поступает запрос.</span><span class="sxs-lookup"><span data-stu-id="85552-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="85552-212">Операция замены Hello будет ожидать toocomplete этот пользовательский прогрева.</span><span class="sxs-lookup"><span data-stu-id="85552-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="85552-213">Ниже приведен пример фрагмента файла web.config.</span><span class="sxs-lookup"><span data-stu-id="85552-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="85552-214">toodelete слота развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-214">toodelete a deployment slot</span></span>
<span data-ttu-id="85552-215">В колонке hello для слота развертывания, слот развертывания Привет открыть колонку, щелкните **Обзор** (страница по умолчанию hello) и нажмите кнопку **удалить** hello панели команд.</span><span class="sxs-lookup"><span data-stu-id="85552-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Удаление слота развертывания][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="85552-217">Командлеты Azure PowerShell для слотов развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="85552-218">Azure PowerShell — это модуль, который предоставляет toomanage командлеты Azure через Windows PowerShell, включая поддержку управления слоты развертывания в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="85552-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="85552-219">Сведения об установке и настройке Azure PowerShell, а также на проверке подлинности Azure PowerShell с подпиской Azure см. в разделе [как tooinstall и настройка Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85552-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="85552-220">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="85552-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="85552-221">Создание слота развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="85552-222">Инициировать переключение с просмотра (многоэтапный подкачка) и применить слоте toosource конфигурации слота назначения</span><span class="sxs-lookup"><span data-stu-id="85552-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="85552-223">Отмена промежуточного переключения (переключения с предварительным просмотром) и восстановление конфигурации исходного слота</span><span class="sxs-lookup"><span data-stu-id="85552-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="85552-224">Переключение слотов развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="85552-225">Удаление слота развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="85552-226">Команды интерфейса командной строки Azure (Azure CLI) для слотов развертывания</span><span class="sxs-lookup"><span data-stu-id="85552-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="85552-227">Hello Azure CLI предоставляет межплатформенных команд для работы с Azure, включая поддержку для управления слоты развертывания служб приложений.</span><span class="sxs-lookup"><span data-stu-id="85552-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="85552-228">Для указания по установке и настройке hello Azure CLI, включая сведения о том, как Azure CLI tooconnect tooyour подписки Azure в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="85552-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="85552-229">Вызовите toolist, hello, команд, доступных для службы приложений Azure в hello Azure CLI `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="85552-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="85552-230">Чтобы ознакомиться с командами [Azure CLI 2.0](https://github.com/Azure/azure-cli) для слотов развертывания, выполните команду [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="85552-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="85552-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="85552-231">azure site list</span></span>
<span data-ttu-id="85552-232">Сведения о приложениях hello в текущей подписке hello вызвать **список сайтов azure**, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="85552-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="85552-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="85552-233">azure site create</span></span>
<span data-ttu-id="85552-234">Вызовите toocreate слота развертывания, **узел azure создать** и укажите имя существующего приложения hello и имя hello toocreate слот hello, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="85552-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="85552-235">tooenable системы управления версиями для нового слота hello, используйте hello **--git** параметр как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="85552-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="85552-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="85552-236">azure site swap</span></span>
<span data-ttu-id="85552-237">toomake hello развертывания слот hello рабочее приложение, используйте hello **swap azure сайта** tooperform команда операции замены, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="85552-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="85552-238">приложение Hello производства будет в любое время простоя, а также будут подвергнуты холодный запуск.</span><span class="sxs-lookup"><span data-stu-id="85552-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="85552-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="85552-239">azure site delete</span></span>
<span data-ttu-id="85552-240">toodelete слот развертывания, которые больше не требуется, используйте hello **удаления сайта azure** команду, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="85552-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="85552-241">Веб-приложение можно увидеть в действии.</span><span class="sxs-lookup"><span data-stu-id="85552-241">See a web app in action.</span></span> <span data-ttu-id="85552-242">[Попробуйте службу приложений](https://azure.microsoft.com/try/app-service/) — в ней можно быстро создать кратковременное приложение начального уровня. Для этого не потребуется ни кредитная карта, ни какие-либо обязательства.</span><span class="sxs-lookup"><span data-stu-id="85552-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="85552-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85552-243">Next Steps</span></span>
<span data-ttu-id="85552-244">[Azure службы приложений веб-приложения — блокировать слоты развертывания web access toonon рабочей](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp введение службы в Linux](./app-service-linux-intro.md)
[бесплатной пробной версии Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="85552-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

