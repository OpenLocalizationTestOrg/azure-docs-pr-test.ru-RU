---
title: "руководство по началу aaaNode.js работы | Документы Microsoft"
description: "Узнайте, как toocreate простой Node.js веб-приложение и развернуть ее tooan облачной службы Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="4e060-103">Построение и развертывание tooan приложений Node.js облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="4e060-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="4e060-104">В этом учебнике показано как toocreate простой Node.js приложение, работающее в облачной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="4e060-105">Облачные службы являются стандартными блоками hello масштабируемых облачных приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="4e060-106">Они позволяют независимых управление и разделение hello и масштабное развертывание служб переднего плана и внутренними компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="4e060-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="4e060-107">Облачные службы предоставляют надежную выделенную виртуальную машину для надежного размещения каждой роли.</span><span class="sxs-lookup"><span data-stu-id="4e060-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="4e060-108">Дополнительные сведения о облачных служб и их сравнение tooAzure веб-сайтов и виртуальных машин см. в разделе [веб-сайтов Azure, облачных служб и виртуальных машин сравнения].</span><span class="sxs-lookup"><span data-stu-id="4e060-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="4e060-109">Ищете простой веб-сайт toobuild?</span><span class="sxs-lookup"><span data-stu-id="4e060-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="4e060-110">Если в вашем сценарии задействован простой интерфейс веб-сайта, мы рекомендуем [использовать упрощенное веб-приложение].</span><span class="sxs-lookup"><span data-stu-id="4e060-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="4e060-111">Легко можно обновить tooa облачной службы как роста веб-приложения и изменения требований.</span><span class="sxs-lookup"><span data-stu-id="4e060-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="4e060-112">Руководствуясь этим учебником, вы соберете простое веб-приложение, размещенное в веб-роли.</span><span class="sxs-lookup"><span data-stu-id="4e060-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="4e060-113">Будет использовать ваше приложение tootest эмулятор вычислений hello локально, а затем развернуть его с помощью средства командной строки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e060-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="4e060-114">приложение Hello представляет простое приложение «hello world»:</span><span class="sxs-lookup"><span data-stu-id="4e060-114">hello application is a simple "hello world" application:</span></span>

![Веб-браузер, отображение веб-страницы Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="4e060-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4e060-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="4e060-117">В этом учебнике используется Azure PowerShell, для которого требуется операционная система Windows.</span><span class="sxs-lookup"><span data-stu-id="4e060-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="4e060-118">Установите и настройте [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="4e060-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="4e060-119">Загрузите и установите hello [пакет Azure SDK для .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="4e060-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="4e060-120">Выберите, в hello запустите программу установки.</span><span class="sxs-lookup"><span data-stu-id="4e060-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="4e060-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="4e060-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="4e060-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="4e060-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="4e060-123">Создание проекта облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="4e060-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="4e060-124">Выполните следующие задачи toocreate новый проект облачной службы Azure, наряду с basic Node.js формирование шаблонов hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="4e060-125">Запустите **Windows PowerShell** от имени администратора, от hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4e060-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="4e060-126">[Подключение PowerShell] tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="4e060-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="4e060-127">Введите hello после проекта hello toocreate toocreate командлета PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4e060-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![результат команды New-AzureService hello helloworld Hello][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="4e060-129">Hello **New AzureServiceProject** командлет создает базовую структуру для публикации tooa приложений Node.js облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4e060-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="4e060-130">Он содержит файлы конфигурации, необходимые для публикации tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4e060-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="4e060-131">Hello также изменяет каталог toohello рабочий каталог для службы hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="4e060-132">Hello создает hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="4e060-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="4e060-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** и **ServiceDefinition.csdef** — специальные файлы Azure, необходимые для публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="4e060-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="4e060-134">См. [общие сведения о создании размещенной службы для Azure].</span><span class="sxs-lookup"><span data-stu-id="4e060-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="4e060-135">**deploymentSettings.json**: сохраняет локальные параметры, используемые hello Azure PowerShell командлеты развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e060-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="4e060-136">Введите hello, следующая команда tooadd новый веб-роли:</span><span class="sxs-lookup"><span data-stu-id="4e060-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![выходные данные команды Add-AzureNodeWebRole hello Hello][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="4e060-138">Hello **Add-AzureNodeWebRole** командлет создает простое приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="4e060-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="4e060-139">Он также изменяет hello **.csfg** и **.csdef** файлы tooadd записи конфигурации для новой роли hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4e060-140">Если имя роли не указано, используется имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e060-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="4e060-141">Можно ввести имя в качестве первого параметра командлета hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="4e060-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="4e060-142">приложение Hello Node.js определяется в файле hello **server.js**, расположенного в каталоге hello hello веб-роли (**WebRole1** по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="4e060-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="4e060-143">Ниже приведен код hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="4e060-144">Данный пример кода является по сути hello образец так же, как Здравствуйте, «Hello World» на hello [nodejs.org] веб-сайта, за исключением того, он использует hello номер порта, присвоенный hello облачной среде.</span><span class="sxs-lookup"><span data-stu-id="4e060-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="4e060-145">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="4e060-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="4e060-146">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="4e060-147">Вы можете [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) или [зарегистрироваться для получения бесплатной версии](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="4e060-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="4e060-148">Загрузите hello Azure параметры публикации</span><span class="sxs-lookup"><span data-stu-id="4e060-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="4e060-149">toodeploy tooAzure вашего приложения, необходимо сначала загрузить hello публикации параметров для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="4e060-150">Выполните следующий командлет Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="4e060-151">Это будет использоваться браузер toonavigate toohello страница загрузки параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="4e060-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="4e060-152">Возможно, запрошенные toolog учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4e060-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="4e060-153">В этом случае используйте hello учетную запись, связанную с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="4e060-154">Сохраните расположение файла tooa профиля загружаются hello может легко получить доступ.</span><span class="sxs-lookup"><span data-stu-id="4e060-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="4e060-155">Выполните следующий командлет tooimport hello профиль, который вы загрузили публикации:</span><span class="sxs-lookup"><span data-stu-id="4e060-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="4e060-156">После импорта hello параметры публикации, рассмотрите возможность удаления hello загрузки файла PUBLISHSETTINGS, так как он содержит сведения, которые может разрешить другому tooaccess вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4e060-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="4e060-157">Публикация приложения hello</span><span class="sxs-lookup"><span data-stu-id="4e060-157">Publish hello application</span></span>
<span data-ttu-id="4e060-158">toopublish запуска hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="4e060-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="4e060-159">**-ServiceName** указывает имя hello для развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="4e060-160">Это должно быть уникальное имя, в противном случае hello публикации процесс завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="4e060-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="4e060-161">Hello **Get-Date** вещам командной строки даты и времени, следует сделать hello имя уникальным.</span><span class="sxs-lookup"><span data-stu-id="4e060-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="4e060-162">**-Location** указывает hello центра обработки данных, который будет размещаться приложение hello в.</span><span class="sxs-lookup"><span data-stu-id="4e060-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="4e060-163">Список доступных центров обработки данных, используйте hello toosee **Get AzureLocation** командлета.</span><span class="sxs-lookup"><span data-stu-id="4e060-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="4e060-164">**-Запуск** открывает окно браузера и переходит по ним toohello размещенной службы после завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e060-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="4e060-165">После успешной публикации появится ответ аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="4e060-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![выходные данные Hello hello команда Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="4e060-167">Он может toodeploy приложения hello через несколько минут и становятся доступными при первой публикации.</span><span class="sxs-lookup"><span data-stu-id="4e060-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="4e060-168">После завершения развертывания hello окно браузера откройте и перехода toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4e060-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Окно браузера, отображение hello hello world страницы; URL-адрес Hello указывает, что страница hello размещается в Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="4e060-170">Теперь приложение работает в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e060-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="4e060-171">Hello **AzureServiceProject публикации** командлет выполняет следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4e060-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="4e060-172">Создает toodeploy пакета.</span><span class="sxs-lookup"><span data-stu-id="4e060-172">Creates a package toodeploy.</span></span> <span data-ttu-id="4e060-173">Hello пакет содержит все файлы hello в папке приложения.</span><span class="sxs-lookup"><span data-stu-id="4e060-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="4e060-174">Создайте новую **учетную запись хранения** , если она не существует.</span><span class="sxs-lookup"><span data-stu-id="4e060-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="4e060-175">Hello учетной записи хранилища Azure — пакет приложения hello toostore используется во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="4e060-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="4e060-176">После завершения развертывания можно безопасно удалить учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="4e060-177">При необходимости создайте **облачную службу**.</span><span class="sxs-lookup"><span data-stu-id="4e060-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="4e060-178">Объект **облачная служба** hello контейнер, в котором размещается приложение при развернутой tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4e060-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="4e060-179">См. [общие сведения о создании размещенной службы для Azure].</span><span class="sxs-lookup"><span data-stu-id="4e060-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="4e060-180">Публикует tooAzure пакета развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="4e060-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="4e060-181">Остановка и удаление приложения</span><span class="sxs-lookup"><span data-stu-id="4e060-181">Stopping and deleting your application</span></span>
<span data-ttu-id="4e060-182">После развертывания приложения, вы можете toodisable его, чтобы избежать дополнительных расходов.</span><span class="sxs-lookup"><span data-stu-id="4e060-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="4e060-183">Для экземпляров веб-роли Azure выставляет счета за почасовое использование серверного времени.</span><span class="sxs-lookup"><span data-stu-id="4e060-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="4e060-184">После развертывания приложения даже в том случае, если экземпляры hello не запущены и находятся в состоянии остановки hello потребляются времени сервера.</span><span class="sxs-lookup"><span data-stu-id="4e060-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="4e060-185">В окне приветствия Windows PowerShell Остановите развертывание службы hello, созданным в предыдущем разделе hello, hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="4e060-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="4e060-186">Остановка службы hello может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4e060-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="4e060-187">При остановке службы hello, появляется сообщение о том, что он был остановлен.</span><span class="sxs-lookup"><span data-stu-id="4e060-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![состояние Hello команды Stop-AzureService hello][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="4e060-189">Служба toodelete hello, вызов hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="4e060-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="4e060-190">При появлении запроса введите **Y** toodelete hello службы.</span><span class="sxs-lookup"><span data-stu-id="4e060-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="4e060-191">Удаление службы hello может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4e060-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="4e060-192">После удаления службы hello появится сообщение, указывающее на то, что служба hello была удалена.</span><span class="sxs-lookup"><span data-stu-id="4e060-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![состояние Hello команды Remove-AzureService hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="4e060-194">Удаление службы hello не удаляет hello учетной записи хранилища, который был создан при первоначальной публикации службы hello и будет выставлен счет за хранилище, используемое toobe.</span><span class="sxs-lookup"><span data-stu-id="4e060-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="4e060-195">Если ничего не используют хранилище hello, вы можете toodelete его.</span><span class="sxs-lookup"><span data-stu-id="4e060-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e060-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e060-196">Next steps</span></span>
<span data-ttu-id="4e060-197">Дополнительные сведения см. в разделе hello [Центр разработчика Node.js].</span><span class="sxs-lookup"><span data-stu-id="4e060-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[веб-сайтов Azure, облачных служб и виртуальных машин сравнения]: ../app-service-web/choose-web-site-cloud-service-vm.md
[использовать упрощенное веб-приложение]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[пакет Azure SDK для .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Подключение PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[общие сведения о создании размещенной службы для Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Центр разработчика Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
