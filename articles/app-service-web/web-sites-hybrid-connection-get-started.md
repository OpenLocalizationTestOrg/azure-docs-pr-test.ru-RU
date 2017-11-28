---
title: "aaaAccess локальных ресурсов с помощью гибридных подключений в службе приложений Azure"
description: "Создание подключения между веб-приложением в службе приложений Azure и локальным ресурсом, который использует статический TCP-порт."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="ecfd9-103">Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ecfd9-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="ecfd9-104">Вы можете подключиться к службе приложений Azure приложение tooany локальных ресурсов, использующих статического TCP-порта, например SQL Server, MySQL, HTTP веб-API и большинство пользовательских веб-служб.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="ecfd9-105">В этой статье показано, как toocreate гибридного подключения между службой приложения и локальная база данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="ecfd9-106">часть функции hello гибридные подключения веб-приложения Hello доступен только в hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="ecfd9-107">toocreate соединений в службах BizTalk. в разделе [гибридные подключения](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="ecfd9-108">Это содержимое также применяется tooMobile приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ecfd9-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ecfd9-109">Prerequisites</span></span>
* <span data-ttu-id="ecfd9-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-110">An Azure subscription.</span></span> <span data-ttu-id="ecfd9-111">Бесплатную подписку можно найти на сайте [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="ecfd9-112">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ecfd9-113">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="ecfd9-114">toouse в локальной среде SQL Server или SQL Server, экспресс-выпуск базы данных с помощью гибридного подключения, TCP/IP должен toobe, включена ли статический порт.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="ecfd9-115">Мы рекомендуем использовать экземпляр SQL Server по умолчанию, так как он использует статический порт 1433.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="ecfd9-116">Сведения об установке и настройке SQL Server Express для использования с гибридных подключений см. в разделе [tooan подключение локального SQL Server с веб-сайта Azure, с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="ecfd9-117">Hello компьютер, на котором устанавливается hello локальный диспетчер гибридного подключения агента описано далее в этой статье:</span><span class="sxs-lookup"><span data-stu-id="ecfd9-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="ecfd9-118">Должна быть tooAzure tooconnect доступ через порт 5671</span><span class="sxs-lookup"><span data-stu-id="ecfd9-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="ecfd9-119">Должен быть hello может tooreach *hostname*:*Номер_порта* локального ресурса.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="ecfd9-120">Hello в этой статье предполагается, что вы используете браузер hello hello компьютере, где будет размещаться агент hello локальной гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="ecfd9-121">Создание веб-приложения в hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="ecfd9-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="ecfd9-122">Если вы уже создали веб-приложения или внутреннего сервера мобильного приложения в портале Azure, что в этом учебнике требуется toouse hello, можно сразу перейти слишком[создать гибридное подключение и служба BizTalk](#CreateHC) и начать с него.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="ecfd9-123">В верхнем левом углу hello hello [портала Azure](https://portal.azure.com), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Создание веб-приложения][NewWebsite]
2. <span data-ttu-id="ecfd9-125">На hello **веб-приложения** колонки, укажите URL-адрес и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. <span data-ttu-id="ecfd9-127">Через несколько секунд hello веб-приложения создается и отображается колонке web app.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="ecfd9-128">Hello колонка предназначена поддерживающим вертикальную прокрутку, позволяющий управлять веб-узла.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
4. <span data-ttu-id="ecfd9-130">tooverify hello сайт будет динамически, можно нажать hello **Обзор** страница по умолчанию hello toodisplay значок.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Нажмите кнопку обзора toosee веб-приложения][Browse]
   
    ![Страница веб-приложения по умолчанию][DefaultWebSitePage]

<span data-ttu-id="ecfd9-133">Затем вы создадите гибридного подключения и служба BizTalk для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="ecfd9-134">Создание гибридного подключения и службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="ecfd9-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="ecfd9-135">В своей колонке веб-приложения щелкните **Все настройки** > **Сеть** > **Настройка конечных точек гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Гибридные подключения][CreateHCHCIcon]
2. <span data-ttu-id="ecfd9-137">В колонке подключений гибридного hello, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="ecfd9-138">Hello **добавить гибридное подключение** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="ecfd9-139">Здравствуйте, так как это ваш первый гибридного подключения **гибридное подключение** параметр выбран, а hello **создать гибридное подключение** колонке открывает для вас.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Создание гибридного подключения][TwinCreateHCBlades]
   
    <span data-ttu-id="ecfd9-141">На hello **создать гибридное подключение колонке**:</span><span class="sxs-lookup"><span data-stu-id="ecfd9-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="ecfd9-142">Для **имя**, введите имя для соединения hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="ecfd9-143">Для **Hostname**, введите имя hello hello на локальном компьютере, на котором находится ресурс.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="ecfd9-144">Для **порт**, введите номер порта hello, что локальный ресурс использует (1433 для экземпляра SQL Server по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="ecfd9-145">Щелкните кнопку **Служба BizTalk**</span><span class="sxs-lookup"><span data-stu-id="ecfd9-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="ecfd9-146">Hello **Создание службы BizTalk** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="ecfd9-147">Введите имя для службы BizTalk hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Создание службы BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="ecfd9-149">Hello **Создание службы BizTalk** закрывает колонки и возвращаются toohello **создать гибридное подключение** колонку.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="ecfd9-150">В колонке hello создать гибридные подключения выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Нажмите кнопку "ОК"][CreateBTScomplete]
6. <span data-ttu-id="ecfd9-152">После завершения процесса hello область уведомлений hello в hello портала о том, успешно созданы подключение hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="ecfd9-153">В колонке hello веб-приложения hello **гибридных подключений** значок теперь отображает создания 1 гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

<span data-ttu-id="ecfd9-155">На этом этапе вы прошли важной частью гибридного подключения hello облачной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="ecfd9-156">Далее вы создадите соответствующую локальную часть.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="ecfd9-157">Установка подключения к hello toocomplete hello локальный диспетчер гибридного подключения</span><span class="sxs-lookup"><span data-stu-id="ecfd9-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="ecfd9-158">В колонке hello веб-приложение, нажмите кнопку **все параметры** > **сети** > **настроить конечные точки гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Значок «Гибридные подключения»][HCIcon]
2. <span data-ttu-id="ecfd9-160">На hello **гибридных подключений** колонки, hello **состояние** столбца для hello недавно был добавлен конечной точки показывает **не подключен**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="ecfd9-161">Нажмите кнопку подключения tooconfigure hello его.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-161">Click hello connection tooconfigure it.</span></span>
   
    ![Не подключено][NotConnected]
   
    <span data-ttu-id="ecfd9-163">Открывает колонку подключения гибридного Hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="ecfd9-165">В колонке hello щелкните **установки прослушивателя**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Щелкните «Установка прослушивателя»][ClickListenerSetup]
4. <span data-ttu-id="ecfd9-167">Hello **свойства гибридного подключения** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="ecfd9-168">В разделе **на локальный диспетчер гибридного подключения**, выберите **щелкните здесь tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Щелкните здесь tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="ecfd9-170">В hello запуска приложения безопасности диалоговое окно предупреждения, выберите **запуска** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Выберите toocontinue выполнения][ApplicationRunWarning]
6. <span data-ttu-id="ecfd9-172">В hello **контроль учетных записей пользователей** диалоговое окно, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Щелкните «Да»][UAC]
7. <span data-ttu-id="ecfd9-174">Hello диспетчер гибридного подключения загружается и устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Установка][HCMInstalling]
8. <span data-ttu-id="ecfd9-176">После завершения установки hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-176">When hello install completes, click **Close**.</span></span>
   
    ![Щелкните кнопку «Закрыть»][HCMInstallComplete]
   
    <span data-ttu-id="ecfd9-178">На hello **гибридных подключений** колонки, hello **состояние** столбец теперь показывает **подключен**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Состояние «Подключено»][HCStatusConnected]

<span data-ttu-id="ecfd9-180">Стало ИТ-инфраструктуры hello гибридного подключения можно создать гибридное приложение, которое использует его.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="ecfd9-181">Hello следующих разделах показано, как toouse гибридные подключения с серверного проекта .NET мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="ecfd9-182">Настройка hello мобильного приложения .NET серверной части проекта tooconnect toohello базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="ecfd9-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="ecfd9-183">В службе приложений проект серверной части мобильного приложения .NET — это просто веб-приложение ASP.NET с установленным и инициализированным дополнительным пакетом SDK для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="ecfd9-184">toouse веб-приложения в качестве серверной части мобильных приложений, необходимо [загрузки и инициализации серверной части мобильных приложений .NET hello SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="ecfd9-185">Для мобильных приложений также необходимые toodefine строку подключения для базы данных в локальной среде hello и изменения toouse hello серверной части этого соединения.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="ecfd9-186">В обозревателе решений в Visual Studio, откройте hello файл Web.config для серверной части мобильных приложений .NET, найдите hello **connectionStrings** добавьте новую запись SqlClient следующего вида hello, какие точки toohello локального SQL База данных сервера:</span><span class="sxs-lookup"><span data-stu-id="ecfd9-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="ecfd9-187">Помните, tooreplace `<**secure_password**>` в данной строке с hello пароль, созданный для *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="ecfd9-188">Нажмите кнопку **Сохранить** в файле Web.config hello toosave Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ecfd9-189">Этот параметр для подключения используется при выполнении на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="ecfd9-190">При работе в Azure, этот параметр является переопределен аргументом параметр подключения hello, определенный в портал hello.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="ecfd9-191">Разверните hello **моделей** папку и файл модели данных откройте hello, который заканчивается на *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="ecfd9-192">Изменение hello **DbContext** toopass конструктор экземпляра hello значение `OnPremisesDBConnection` toohello базового **DbContext** конструктор, аналогичные toohello следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="ecfd9-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="ecfd9-193">Hello теперь использует hello нового подключения toohello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="ecfd9-194">Обновление локальной строки подключения внутреннего toouse hello мобильное приложение hello</span><span class="sxs-lookup"><span data-stu-id="ecfd9-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="ecfd9-195">Далее необходимо tooadd Настройка приложения для этого новую строку подключения, чтобы его можно использовать из Azure.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="ecfd9-196">Вернитесь в hello [портал Azure](https://portal.azure.com) hello кода веб-приложения серверной части для мобильного приложения, щелкните **все параметры**, затем **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="ecfd9-197">В hello **веб-параметров приложения** колонки, прокрутите вниз слишком**строки подключения** и добавьте новый **SQL Server** строку подключения с именем `OnPremisesDBConnection` значение типа `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="ecfd9-198">Замените `<**secure_password**>` с hello надежный пароль для локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Строка подключения для локальной базы данных](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="ecfd9-200">Нажмите клавишу **Сохранить** toosave hello гибридного подключения и строкой подключения только что создали.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="ecfd9-201">На этом этапе можно повторно опубликовать проект сервера hello и протестировать hello новое соединение с существующие клиенты мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="ecfd9-202">Данные будут считываются и записываются toohello локальной базы данных с помощью hello гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="ecfd9-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ecfd9-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ecfd9-203">Next Steps</span></span>
* <span data-ttu-id="ecfd9-204">Сведения о создании веб-приложение ASP.NET, который использует гибридного подключения см. в разделе [tooan подключение локального SQL Server с веб-сайта Azure, с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="ecfd9-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="ecfd9-205">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ecfd9-205">Additional Resources</span></span>
[<span data-ttu-id="ecfd9-206">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="ecfd9-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="ecfd9-207">Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ecfd9-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="ecfd9-208">Веб-сайт гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="ecfd9-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="ecfd9-209">Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"</span><span class="sxs-lookup"><span data-stu-id="ecfd9-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="ecfd9-210">Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ecfd9-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="ecfd9-211">Подключение tooan локального SQL Server из мобильных служб Azure с помощью гибридных подключений (видео на канале 9)</span><span class="sxs-lookup"><span data-stu-id="ecfd9-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="ecfd9-212">Изменения</span><span class="sxs-lookup"><span data-stu-id="ecfd9-212">What's changed</span></span>
* <span data-ttu-id="ecfd9-213">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ecfd9-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
