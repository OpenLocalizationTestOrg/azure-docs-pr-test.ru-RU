---
title: "Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="5f4d0-103">Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="5f4d0-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="5f4d0-104">Приложение служб приложений Azure можно подключить к любому локальному ресурсу, который использует статический TCP-порт: например, SQL Server, MySQL, веб-интерфейсы API HTTP и большинство настраиваемых веб-служб.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="5f4d0-105">В этой статье показано, как создать гибридное подключение между приложением в службе приложений и локальной базой данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="5f4d0-106">Часть функции гибридных подключений, которая называется "Веб-приложения", доступна только на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="5f4d0-107">Сведения о создании подключения в службах BizTalk см. в статье [Обзор гибридных подключений](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="5f4d0-108">Это содержимое также применяется к мобильным приложениям в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5f4d0-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5f4d0-109">Prerequisites</span></span>
* <span data-ttu-id="5f4d0-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-110">An Azure subscription.</span></span> <span data-ttu-id="5f4d0-111">Бесплатную подписку можно найти на сайте [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="5f4d0-112">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5f4d0-113">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="5f4d0-114">Для использования локальной базы данных SQL Server или SQL Server Express с помощью гибридного подключения в статическом порте должен быть включен протокол TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="5f4d0-115">Мы рекомендуем использовать экземпляр SQL Server по умолчанию, так как он использует статический порт 1433.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="5f4d0-116">Информацию об установке и настройке SQL Server Express для использования с гибридными подключениями см. в разделе [Подключение к локальному SQL Server с веб-сайта Azure с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="5f4d0-117">Компьютер, на котором установлен локальный агент диспетчера гибридных подключений, описан далее в этой статье:</span><span class="sxs-lookup"><span data-stu-id="5f4d0-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="5f4d0-118">должен подключаться к Azure через порт 5671;</span><span class="sxs-lookup"><span data-stu-id="5f4d0-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="5f4d0-119">должен подключаться к *hostname*:*portnumber* локального источника.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="5f4d0-120">В шагах этой статьи предполагается, что вы используете браузер с компьютера, на котором размещается локальный агент гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="5f4d0-121">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5f4d0-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="5f4d0-122">Если вы уже создали веб-приложение или серверную часть мобильного приложения на портале Azure и хотите использовать его в этом учебнике, можно пропустить этот шаг и начать с раздела [Создание гибридного подключения и службы BizTalk](#CreateHC) .</span><span class="sxs-lookup"><span data-stu-id="5f4d0-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="5f4d0-123">В левом верхнем углу [портала Azure](https://portal.azure.com) щелкните **Создать** > **Интернет + мобильные устройства** > **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Создание веб-приложения][NewWebsite]
2. <span data-ttu-id="5f4d0-125">В колонке **Веб-приложение** укажите URL-адрес и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. <span data-ttu-id="5f4d0-127">Через несколько секунд будет создано веб-приложение и появится его колонка.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="5f4d0-128">Выноска — это вертикальная панель мониторинга, которую можно прокручивать и которая позволяет управлять сайтом.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
4. <span data-ttu-id="5f4d0-130">Чтобы проверить, что веб-сайт работает, можно щелкнуть значок **Обзор** для отображения страницы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Щелкните "Обзор", чтобы посмотреть веб-приложение][Browse]
   
    ![Страница веб-приложения по умолчанию][DefaultWebSitePage]

<span data-ttu-id="5f4d0-133">Далее вы создадите гибридное подключение и службу BizTalk для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="5f4d0-134">Создание гибридного подключения и службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="5f4d0-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="5f4d0-135">В своей колонке веб-приложения щелкните **Все настройки** > **Сеть** > **Настройка конечных точек гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Гибридные подключения][CreateHCHCIcon]
2. <span data-ttu-id="5f4d0-137">На выноске «Гибридные подключения» щелкните кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="5f4d0-138">Откроется выноска **Добавление гибридного подключения** .</span><span class="sxs-lookup"><span data-stu-id="5f4d0-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="5f4d0-139">Так как это ваше первое гибридное подключение, параметр **Новое гибридное подключение** будет выбран автоматически, и откроется колонка **Создание гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Создание гибридного подключения][TwinCreateHCBlades]
   
    <span data-ttu-id="5f4d0-141">На **выноске Создание гибридного подключения**:</span><span class="sxs-lookup"><span data-stu-id="5f4d0-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="5f4d0-142">в поле **Имя**укажите имя подключения;</span><span class="sxs-lookup"><span data-stu-id="5f4d0-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="5f4d0-143">в поле **Имя узла**введите имя локального компьютера, на котором размещается ваш ресурс;</span><span class="sxs-lookup"><span data-stu-id="5f4d0-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="5f4d0-144">в поле **Порт**введите номер порта, который использует ваш локальный ресурс (1433 для экземпляра SQL Server по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="5f4d0-145">Щелкните кнопку **Служба BizTalk**</span><span class="sxs-lookup"><span data-stu-id="5f4d0-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="5f4d0-146">Откроется колонка **Создание службы BizTalk** .</span><span class="sxs-lookup"><span data-stu-id="5f4d0-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="5f4d0-147">Введите имя службы BizTalk и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Создание службы BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="5f4d0-149">Колонка **Создание службы BizTalk** закроется, и вы вернетесь к колонке **Создание гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="5f4d0-150">На выноске «Создание гибридного подключения» щелкните кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Нажмите кнопку "ОК"][CreateBTScomplete]
6. <span data-ttu-id="5f4d0-152">После завершения процесса в области уведомлений на портале появится сообщение об успешном создании подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="5f4d0-153">Теперь в колонке веб-приложения значок **Гибридные подключения** показывает, что создано одно гибридное подключение.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

<span data-ttu-id="5f4d0-155">На этот момент вы завершили важную часть облачной инфраструктуры гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="5f4d0-156">Далее вы создадите соответствующую локальную часть.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="5f4d0-157">Установка локального диспетчера гибридных подключений для завершения подключения</span><span class="sxs-lookup"><span data-stu-id="5f4d0-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="5f4d0-158">В колонке веб-приложения щелкните **Все настройки** > **Сеть** > **Настройка конечных точек гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Значок «Гибридные подключения»][HCIcon]
2. <span data-ttu-id="5f4d0-160">В колонке **Гибридные подключения** в столбце **Состояние** для недавно добавленных конечных точек отображается состояние **Не подключено**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="5f4d0-161">Щелкните подключение, чтобы настроить его.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-161">Click the connection to configure it.</span></span>
   
    ![Не подключено][NotConnected]
   
    <span data-ttu-id="5f4d0-163">Откроется выноска гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="5f4d0-165">Щелкните на выноске **Установка прослушивателя**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Щелкните «Установка прослушивателя»][ClickListenerSetup]
4. <span data-ttu-id="5f4d0-167">Откроется выноска **Свойства гибридного подключения** .</span><span class="sxs-lookup"><span data-stu-id="5f4d0-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="5f4d0-168">В **локальном диспетчере гибридных подключений** выберите **Щелкните, чтобы установить**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Щелкните здесь, чтобы установить][ClickToInstallHCM]
5. <span data-ttu-id="5f4d0-170">В диалоговом окне предупреждения системы безопасности «Запуск приложения» нажмите кнопку **Запустить** , чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Нажмите кнопку «Запустить», чтобы продолжить][ApplicationRunWarning]
6. <span data-ttu-id="5f4d0-172">В диалоговом окне **Контроль учетных записей пользователей** щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Щелкните «Да»][UAC]
7. <span data-ttu-id="5f4d0-174">Диспетчер гибридных подключений скачан и установлен.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Установка][HCMInstalling]
8. <span data-ttu-id="5f4d0-176">После завершения установки щелкните кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-176">When the install completes, click **Close**.</span></span>
   
    ![Щелкните кнопку «Закрыть»][HCMInstallComplete]
   
    <span data-ttu-id="5f4d0-178">В колонке **Гибридные подключения** в столбце **Состояние** теперь отображается **Подключено**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Состояние «Подключено»][HCStatusConnected]

<span data-ttu-id="5f4d0-180">Теперь по завершении инфраструктуры гибридных подключений вы можете создать гибридное приложение, которое использует ее.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="5f4d0-181">В следующих разделах показано, как использовать гибридное подключение в проекте серверной части мобильных приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="5f4d0-182">Настройка проекта серверной части мобильного приложения .NET для подключения к базе данных сервера SQL Server</span><span class="sxs-lookup"><span data-stu-id="5f4d0-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="5f4d0-183">В службе приложений проект серверной части мобильного приложения .NET — это просто веб-приложение ASP.NET с установленным и инициализированным дополнительным пакетом SDK для мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="5f4d0-184">Чтобы использовать веб-приложение в качестве серверной части мобильного приложения, необходимо [скачать и инициализировать пакет SDK серверной части .NET для мобильных приложений](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="5f4d0-185">Для мобильных приложений также необходимо определить строку подключения для локальной базы данных и изменить серверную часть для использования этого подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="5f4d0-186">В обозревателе решений Visual Studio откройте файл Web.config для своей серверной части .NET мобильного приложения, найдите раздел **connectionStrings** и добавьте новую запись SqlClient (см. пример ниже), которая указывает на локальную базу данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="5f4d0-187">Не забудьте заменить `<**secure_password**>` в этой строке паролем, созданным для объекта *HbyridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="5f4d0-188">Щелкните кнопку **Сохранить** в Visual Studio, чтобы сохранить файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5f4d0-189">Эти параметры подключения используются при запуске на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="5f4d0-190">При запуске в среде Azure они заменяются строкой подключения, определенной на портале.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="5f4d0-191">Разверните папку **Модели** и откройте файл модели данных, заканчивающийся на *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="5f4d0-192">Измените конструктор экземпляра **DbContext** таким образом, чтобы он передавал значение `OnPremisesDBConnection` в базовый конструктор **DbContext**, с помощью кода наподобие приведенного ниже фрагмента.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="5f4d0-193">Теперь служба будет использовать новую строку подключения для базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="5f4d0-194">Обновление серверной части мобильного приложения для использования локальной строки подключения</span><span class="sxs-lookup"><span data-stu-id="5f4d0-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="5f4d0-195">Далее, чтобы использовать новую строку подключения среды Azure, вам нужно добавить в нее параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="5f4d0-196">На [портале Azure](https://portal.azure.com) в коде серверной части веб-приложения для своего мобильного приложения щелкните **Все параметры** и выберите **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="5f4d0-197">В колонке **Параметры веб-приложения** прокрутите содержимое до раздела **Строки подключения** и добавьте новую строку подключения **SQL Server** с именем `OnPremisesDBConnection` и значением наподобие `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="5f4d0-198">Замените `<**secure_password**>` надежным паролем для локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Строка подключения для локальной базы данных](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="5f4d0-200">Нажмите кнопку **Сохранить** , чтобы сохранить созданное гибридное подключение и строку подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="5f4d0-201">На этом этапе можно повторно опубликовать серверный проект и проверить новое подключение для существующих клиентов мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="5f4d0-202">Данные будут считываться и записываться в локальную базу данных с помощью гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="5f4d0-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f4d0-203">Next Steps</span></span>
* <span data-ttu-id="5f4d0-204">Сведения о создании веб-приложения ASP.NET, которое использует гибридное подключение, см. в разделе [Подключение к локальному SQL Server из веб-приложения, размещенного в службе приложений Azure с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="5f4d0-205">дополнительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5f4d0-205">Additional Resources</span></span>
[<span data-ttu-id="5f4d0-206">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="5f4d0-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="5f4d0-207">Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5f4d0-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="5f4d0-208">Веб-сайт гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="5f4d0-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="5f4d0-209">Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"</span><span class="sxs-lookup"><span data-stu-id="5f4d0-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="5f4d0-210">Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5f4d0-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="5f4d0-211">Подключение к локальному SQL Server с мобильных служб Azure с помощью гибридных подключений (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5f4d0-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="5f4d0-212">Изменения</span><span class="sxs-lookup"><span data-stu-id="5f4d0-212">What's changed</span></span>
* <span data-ttu-id="5f4d0-213">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5f4d0-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
