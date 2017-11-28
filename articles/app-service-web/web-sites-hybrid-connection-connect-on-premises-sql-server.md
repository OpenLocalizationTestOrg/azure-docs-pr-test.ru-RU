---
title: "Подключение к локальному SQL Server из веб-приложения, размещенного в службе приложений Azure с помощью гибридных подключений"
description: "Создание веб-приложения в Microsoft Azure и его подключение к локальной базе данных SQL Server"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="97da5-103">Подключение к локальному SQL Server из веб-приложения, размещенного в службе приложений Azure с помощью гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="97da5-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="97da5-104">Гибридные подключения могут подключать [службу приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) к локальным ресурсам, которые используют статический TCP-порт.</span><span class="sxs-lookup"><span data-stu-id="97da5-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="97da5-105">Поддерживаются такие ресурсы: Microsoft SQL Server, MySQL, веб-API HTTP, служба приложений и большинство настраиваемых веб-служб.</span><span class="sxs-lookup"><span data-stu-id="97da5-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="97da5-106">В этом учебнике вы узнаете, как создать веб-приложение службы приложений [на портале Azure](http://go.microsoft.com/fwlink/?LinkId=529715), подключить веб-приложение к локальной базе данных SQL Server с помощью новой функции гибридного подключения, создать простое приложение ASP.NET, которое будет использовать гибридное подключение, и развернуть приложение в веб-приложение службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="97da5-107">В полном веб-приложении Azure учетные данные пользователя хранятся в локальной базе данных участников.</span><span class="sxs-lookup"><span data-stu-id="97da5-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="97da5-108">Этот учебник разработан для читателей, не имеющих опыта использования Azure или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97da5-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="97da5-109">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="97da5-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="97da5-110">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="97da5-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="97da5-111">Часть функции гибридных подключений, которая называется "Веб-приложения", доступна только на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97da5-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="97da5-112">Сведения о создании подключения в службах BizTalk см. в статье [Обзор гибридных подключений](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="97da5-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="97da5-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="97da5-113">Prerequisites</span></span>
<span data-ttu-id="97da5-114">Для работы с этим учебником вам потребуются следующие продукты.</span><span class="sxs-lookup"><span data-stu-id="97da5-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="97da5-115">У всех этих продуктов есть бесплатные версии, так что можно начать разработку для Azure полностью бесплатно.</span><span class="sxs-lookup"><span data-stu-id="97da5-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="97da5-116">**Подписка Azure**. Сведения о бесплатной подписке см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97da5-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="97da5-117">**Visual Studio 2013**. Сведения о загрузке бесплатной пробной версии см. на странице [Скачиваемые файлы для Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="97da5-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="97da5-118">Прежде чем продолжить, установите этот продукт.</span><span class="sxs-lookup"><span data-stu-id="97da5-118">Install this before continuing.</span></span>
* <span data-ttu-id="97da5-119">**Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1)**. Если вы используете операционную систему Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 или Windows Server 2008 R2, ее можно включить на панели управления, последовательно выбрав "Программы и компоненты", "Включение или отключение компонентов Windows".</span><span class="sxs-lookup"><span data-stu-id="97da5-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="97da5-120">В противном случае программу можно скачать в [Центре загрузки Майкрософт](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="97da5-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="97da5-121">**SQL Server 2014 Express с инструментами** — загрузите Microsoft SQL Server Express бесплатно на [странице базы данных веб-платформы Майкрософт](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="97da5-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="97da5-122">Выберите версию **Express** (не LocalDB).</span><span class="sxs-lookup"><span data-stu-id="97da5-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="97da5-123">Версия **Express с инструментами** включает SQL Server Management Studio, который будет использоваться в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="97da5-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="97da5-124">**SQL Server Management Studio Express**. Сюда включается SQL Server 2014, экспресс-выпуск с инструментами, указанный выше, но если требуется установить его отдельно, можно скачать и установить его на [странице загрузки SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="97da5-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="97da5-125">В учебнике предполагается, что у вас есть подписка Azure, установлена служба Visual Studio 2013 и установлена или включена .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="97da5-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="97da5-126">В учебнике показано, как установить SQL Server 2014 Express в конфигурации, которая хорошо работает с функцией гибридных подключений Azure (экземпляр по умолчанию со статическим TCP-портом).</span><span class="sxs-lookup"><span data-stu-id="97da5-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="97da5-127">Перед тем как начать учебник, если у вас не установлен SQL Server, скачайте SQL Server 2014, экспресс-выпуск с инструментами, из указанного выше расположения.</span><span class="sxs-lookup"><span data-stu-id="97da5-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="97da5-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="97da5-128">Notes</span></span>
<span data-ttu-id="97da5-129">Для использования локальной базы данных SQL Server или SQL Server Express с помощью гибридного подключения в статическом порте должен быть включен протокол TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="97da5-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="97da5-130">Экземпляры SQL Server по умолчанию используют статический порт 1433, а именованные экземпляры не используют этот порт.</span><span class="sxs-lookup"><span data-stu-id="97da5-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="97da5-131">Компьютер, на котором установлен локальный агент диспетчера гибридных подключений:</span><span class="sxs-lookup"><span data-stu-id="97da5-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="97da5-132">Необходимо иметь исходящее подключение к Azure через:</span><span class="sxs-lookup"><span data-stu-id="97da5-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="97da5-133">Порт</span><span class="sxs-lookup"><span data-stu-id="97da5-133">Port</span></span> | <span data-ttu-id="97da5-134">Назначение</span><span class="sxs-lookup"><span data-stu-id="97da5-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="97da5-135">80</span><span class="sxs-lookup"><span data-stu-id="97da5-135">80</span></span> |<span data-ttu-id="97da5-136">**Требуется** для порта HTTP при проверке сертификатов и (необязательно) для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="97da5-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="97da5-137">443</span><span class="sxs-lookup"><span data-stu-id="97da5-137">443</span></span> |<span data-ttu-id="97da5-138">**Необязательно** для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="97da5-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="97da5-139">Если исходящее подключение к порту 443 недоступно, то используется порт TCP 80.</span><span class="sxs-lookup"><span data-stu-id="97da5-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="97da5-140">5671 и 9352</span><span class="sxs-lookup"><span data-stu-id="97da5-140">5671 and 9352</span></span> |<span data-ttu-id="97da5-141">**Рекомендуется** , но необязательно для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="97da5-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="97da5-142">Обратите внимание, что в этом режиме обеспечивается более высокая пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="97da5-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="97da5-143">Если исходящее подключение к этим портам недоступно, то используется порт TCP 443.</span><span class="sxs-lookup"><span data-stu-id="97da5-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="97da5-144">должен подключаться к *hostname*:*portnumber* локального источника.</span><span class="sxs-lookup"><span data-stu-id="97da5-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="97da5-145">В шагах этой статьи предполагается, что вы используете браузер с компьютера, на котором размещается локальный агент гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="97da5-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="97da5-146">Если SQL Server уже установлен в конфигурации и среде, которые соответствуют приведенным выше условиям, можно пропустить этот этап и перейти к разделу [Создание локальной базы данных SQL Server](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="97da5-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="97da5-147">О.</span><span class="sxs-lookup"><span data-stu-id="97da5-147">A.</span></span> <span data-ttu-id="97da5-148">Установка экспресс-выпуска SQL Server, включение TCP/IP и создание локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="97da5-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="97da5-149">В этом разделе показывается, как установить SQL Server Express, включить TCP/IP и создать базу данных, чтобы веб-приложение работало с порталом Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="97da5-150">Установка SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="97da5-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="97da5-151">Чтобы установить SQL Server Express, запустите скачанный файл **SQLEXPRWT_x64_ENU.exe** или **SQLEXPR_x86_ENU.exe**.</span><span class="sxs-lookup"><span data-stu-id="97da5-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="97da5-152">Появится мастер центра установки SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97da5-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![Установка SQL Server][SQLServerInstall]
2. <span data-ttu-id="97da5-154">Нажмите кнопку **Создать изолированную установку SQL Server или добавить компоненты к существующему экземпляру**.</span><span class="sxs-lookup"><span data-stu-id="97da5-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="97da5-155">Следуйте инструкциям, принимая варианты и параметры по умолчанию, пока не откроется страница **Конфигурация экземпляров** .</span><span class="sxs-lookup"><span data-stu-id="97da5-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="97da5-156">На странице **Конфигурация экземпляра** выберите параметр **Экземпляр по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="97da5-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Выбор экземпляра по умолчанию][ChooseDefaultInstance]
   
    <span data-ttu-id="97da5-158">Экземпляр SQL Server по умолчанию прослушивает запросы от клиентов SQL Server в статическом порте 1433 в соответствии с требованиями функции гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="97da5-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="97da5-159">Именованные экземпляры используют динамические порты и UDP, которые не поддерживаются гибридными подключениями.</span><span class="sxs-lookup"><span data-stu-id="97da5-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="97da5-160">Примите значения по умолчанию на странице **Конфигурация сервера** .</span><span class="sxs-lookup"><span data-stu-id="97da5-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="97da5-161">На странице **Настройка ядра СУБД** в разделе **Режим проверки подлинности** выберите параметр **Смешанный режим (проверка подлинности SQL Server и Windows)** и укажите пароль.</span><span class="sxs-lookup"><span data-stu-id="97da5-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Выбор смешанного режима][ChooseMixedMode]
   
    <span data-ttu-id="97da5-163">В этом учебнике вы будете использовать проверку подлинности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97da5-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="97da5-164">Убедитесь, что запомнили указанный пароль, поскольку он понадобится вам позже.</span><span class="sxs-lookup"><span data-stu-id="97da5-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="97da5-165">Выполните все инструкции мастера, чтобы завершить установку.</span><span class="sxs-lookup"><span data-stu-id="97da5-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="97da5-166">Включение TCP/IP</span><span class="sxs-lookup"><span data-stu-id="97da5-166">Enable TCP/IP</span></span>
<span data-ttu-id="97da5-167">Чтобы включить TCP/IP, необходимо использовать диспетчер конфигурации SQL Server, который устанавливается при установке SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="97da5-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="97da5-168">Перед тем как продолжить, выполните шаги в разделе [Включение протокола сети TCP/IP для SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="97da5-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="97da5-169">Создание локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="97da5-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="97da5-170">Для веб-приложения Visual Studio требуется база данных участников, к которой может получить доступ Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="97da5-171">Для этого необходим SQL Server или база данных SQL Server Express (а не база данных LocalDB, которую шаблон MVC использует по умолчанию), поэтому далее следует создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="97da5-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="97da5-172">В SQL Server Management Studio подключитесь к установленному SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97da5-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="97da5-173">(Если диалоговое окно **Подключение к серверу** не откроется автоматически, перейдите к **обозревателю объектов** на левой панели, щелкните **Подключение**, а затем — **Ядро СУБД**.) ![Подключение к серверу][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="97da5-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="97da5-174">Для параметра **Тип сервера** выберите значение **Ядро СУБД**.</span><span class="sxs-lookup"><span data-stu-id="97da5-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="97da5-175">В качестве **имени сервера** можно использовать значение **localhost** или имя используемого компьютера.</span><span class="sxs-lookup"><span data-stu-id="97da5-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="97da5-176">Выберите **Проверка подлинности SQL Server**, а затем войдите с именем пользователя и паролем, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="97da5-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="97da5-177">Чтобы создать новую базу данных, используя SQL Server Management Studio, в обозревателе объектов щелкните правой кнопкой мыши элемент **Базы данных** и выберите команду **Создать базу данных**.</span><span class="sxs-lookup"><span data-stu-id="97da5-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Создание базы данных][SSMScreateNewDB]
3. <span data-ttu-id="97da5-179">В диалоговом окне **Создание базы данных** введите в качестве имени базы данных MembershipDB и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97da5-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Предоставление имени базы данных][SSMSprovideDBname]
   
    <span data-ttu-id="97da5-181">Обратите внимание, что в этот момент в базу данных не вносятся никакие изменения.</span><span class="sxs-lookup"><span data-stu-id="97da5-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="97da5-182">Сведения об участниках веб-приложение добавит позже, автоматически при запуске.</span><span class="sxs-lookup"><span data-stu-id="97da5-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="97da5-183">Если развернуть в обозревателе объектов **Базы данных**, вы увидите, что была создана база данных участников.</span><span class="sxs-lookup"><span data-stu-id="97da5-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![Создана MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="97da5-185">B.</span><span class="sxs-lookup"><span data-stu-id="97da5-185">B.</span></span> <span data-ttu-id="97da5-186">Создание веб-приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="97da5-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="97da5-187">Если вы уже создали веб-приложение на портале Azure, которое хотите использовать при прохождении этого учебника, можно пропустить этот шаг и продолжить с раздела [Создание гибридного подключения и службы BizTalk](#CreateHC) .</span><span class="sxs-lookup"><span data-stu-id="97da5-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="97da5-188">На [портале Azure](https://portal.azure.com) последовательно выберите **Создать** > **Интернет+мобильные устройства** > **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="97da5-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Кнопка «Создать»][New]
2. <span data-ttu-id="97da5-190">Настройте веб-приложение и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="97da5-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. <span data-ttu-id="97da5-192">Через несколько секунд будет создано веб-приложение и появится его колонка.</span><span class="sxs-lookup"><span data-stu-id="97da5-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="97da5-193">Колонка — это вертикальная панель мониторинга, которую можно прокручивать и которая позволяет управлять веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="97da5-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
   
    <span data-ttu-id="97da5-195">Чтобы проверить, что веб-приложение работает, можно щелкнуть значок **Обзор** для отображения страницы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="97da5-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="97da5-196">Далее вы создадите гибридное подключение и службу BizTalk для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="97da5-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="97da5-197">C.</span><span class="sxs-lookup"><span data-stu-id="97da5-197">C.</span></span> <span data-ttu-id="97da5-198">Создание гибридного подключения и службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="97da5-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="97da5-199">Вернитесь на портал, откройте настройки и выберите **Сети** > **Настройте конечные точки гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="97da5-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Гибридные подключения][CreateHCHCIcon]
2. <span data-ttu-id="97da5-201">В колонке "Гибридные подключения" щелкните **Добавить** > **Новое гибридное подключение**.</span><span class="sxs-lookup"><span data-stu-id="97da5-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="97da5-202">В колонке **Создание гибридного подключения** :</span><span class="sxs-lookup"><span data-stu-id="97da5-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="97da5-203">в поле **Имя**укажите имя подключения;</span><span class="sxs-lookup"><span data-stu-id="97da5-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="97da5-204">в поле **Имя узла**введите имя компьютера главного компьютера SQL Server;</span><span class="sxs-lookup"><span data-stu-id="97da5-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="97da5-205">в поле **Порт**введите 1433 (порт по умолчанию для SQL Server).</span><span class="sxs-lookup"><span data-stu-id="97da5-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="97da5-206">Выберите **Служба BizTalk** > **Новая служба BizTalk** и введите имя службы.</span><span class="sxs-lookup"><span data-stu-id="97da5-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Создание гибридного подключения][TwinCreateHCBlades]
4. <span data-ttu-id="97da5-208">Нажмите **ОК** дважды.</span><span class="sxs-lookup"><span data-stu-id="97da5-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="97da5-209">По завершении процесса в области **Уведомления** будет мигать зеленым надпись **УСПЕШНО**, а в колонке **Гибридное подключение** будет отображено новое гибридное подключение с состоянием **Не подключено**.</span><span class="sxs-lookup"><span data-stu-id="97da5-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

<span data-ttu-id="97da5-211">На этот момент вы завершили важную часть облачной инфраструктуры гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="97da5-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="97da5-212">Далее вы создадите соответствующую локальную часть.</span><span class="sxs-lookup"><span data-stu-id="97da5-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="97da5-213">D.</span><span class="sxs-lookup"><span data-stu-id="97da5-213">D.</span></span> <span data-ttu-id="97da5-214">Установка локального диспетчера гибридных подключений для завершения подключения</span><span class="sxs-lookup"><span data-stu-id="97da5-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="97da5-215">Теперь по завершении инфраструктуры гибридных подключений создайте веб-приложение, которое использует ее.</span><span class="sxs-lookup"><span data-stu-id="97da5-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="97da5-216">E.</span><span class="sxs-lookup"><span data-stu-id="97da5-216">E.</span></span> <span data-ttu-id="97da5-217">Создание базового веб-проекта ASP.NET, изменение строки подключения к базе данных и локальный запуск проекта</span><span class="sxs-lookup"><span data-stu-id="97da5-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="97da5-218">Создание базового проекта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="97da5-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="97da5-219">В Visual Studio в меню **Файл** создайте новый проект:</span><span class="sxs-lookup"><span data-stu-id="97da5-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![Новый проект Visual Studio][HCVSNewProject]
2. <span data-ttu-id="97da5-221">В разделе **Шаблоны** диалогового окна **Новый проект** выберите элемент **Интернет** и щелкните **Веб-приложение ASP.NET**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97da5-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Выбор веб-приложения ASP.NET][HCVSChooseASPNET]
3. <span data-ttu-id="97da5-223">В диалоговом окне **Новый проект ASP.NET** выберите **MVC** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97da5-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Выбор MVC][HCVSChooseMVC]
4. <span data-ttu-id="97da5-225">При создании проекта появится страница файла сведений приложения.</span><span class="sxs-lookup"><span data-stu-id="97da5-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="97da5-226">Не запускайте пока что веб-проект.</span><span class="sxs-lookup"><span data-stu-id="97da5-226">Do not run the web project yet.</span></span>
   
    ![Страница файла сведений][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="97da5-228">Изменение строки подключения базы данных для приложения</span><span class="sxs-lookup"><span data-stu-id="97da5-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="97da5-229">В этом шаге необходимо настроить строку подключения, которая сообщает приложению, где найти локальную базу данных SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="97da5-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="97da5-230">Строка подключения находится в файле Web.config приложения, в котором содержатся сведения о конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="97da5-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="97da5-231">Чтобы убедиться, что приложение использует базу данных, созданную в экспресс-выпуске SQL Server, а не LocalDB Visual Studio по умолчанию, важно выполнить это действие до запуска проекта.</span><span class="sxs-lookup"><span data-stu-id="97da5-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="97da5-232">Дважды щелкните в обозревателе решений файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="97da5-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="97da5-234">Измените раздел **connectionStrings** , чтобы он указывал на базу данных SQL Server на локальном компьютере, используя синтаксис в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="97da5-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Строка подключения][HCVSConnectionString]
   
    <span data-ttu-id="97da5-236">При создании строки подключения помните о следующем.</span><span class="sxs-lookup"><span data-stu-id="97da5-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="97da5-237">Если вы подключаетесь к именованному экземпляру, а не к экземпляру по умолчанию (например, YourServer\SQLEXPRESS), необходимо настроить SQL Server для использования статических портов.</span><span class="sxs-lookup"><span data-stu-id="97da5-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="97da5-238">Сведения о настройке статических портов см. в статье [Как настроить SQL Server на прослушивание определенного порта](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="97da5-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="97da5-239">По умолчанию именованные экземпляры используют UDP и динамические порты, которые не поддерживаются гибридными подключениями.</span><span class="sxs-lookup"><span data-stu-id="97da5-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="97da5-240">Рекомендуется указать порт (1433 по умолчанию, как показано в примере) в строке подключения, чтобы убедиться, что в локальном SQL Server включен TCP, использующий правильный порт.</span><span class="sxs-lookup"><span data-stu-id="97da5-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="97da5-241">Следует использовать проверку подлинности SQL Server для подключения, указав идентификатор и пароль пользователя в строке подключений.</span><span class="sxs-lookup"><span data-stu-id="97da5-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="97da5-242">Щелкните кнопку **Сохранить** в Visual Studio, чтобы сохранить файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="97da5-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="97da5-243">Запуск проекта локально и регистрация нового пользователя</span><span class="sxs-lookup"><span data-stu-id="97da5-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="97da5-244">Теперь запустите новый веб-проект локально, щелкнув кнопку «Обзор» в разделе «Отладка».</span><span class="sxs-lookup"><span data-stu-id="97da5-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="97da5-245">В этом примере используется Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="97da5-245">This example uses Internet Explorer.</span></span>
   
    ![Запуск проекта][HCVSRunProject]
2. <span data-ttu-id="97da5-247">В правом верхнем углу веб-страницы по умолчанию нажмите кнопку **Зарегистрировать** , чтобы зарегистрировать новую учетную запись:</span><span class="sxs-lookup"><span data-stu-id="97da5-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Регистрация новой учетной записи][HCVSRegisterLocally]
3. <span data-ttu-id="97da5-249">Введите имя пользователя и пароль:</span><span class="sxs-lookup"><span data-stu-id="97da5-249">Enter a user name and password:</span></span>
   
    ![Ввод имени пользователя и пароля][HCVSCreateNewAccount]
   
    <span data-ttu-id="97da5-251">Это автоматически создаст базу данных в локальном SQL Server, в котором хранятся сведения об участниках для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="97da5-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="97da5-252">В одной из таблиц (**dbo.AspNetUsers**) сохранены учетные данные пользователя веб-приложения, аналогичные только что указанным.</span><span class="sxs-lookup"><span data-stu-id="97da5-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="97da5-253">Эта таблица появится позже в данном учебном курсе.</span><span class="sxs-lookup"><span data-stu-id="97da5-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="97da5-254">Закройте окно браузера веб-страницы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="97da5-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="97da5-255">Это остановит приложение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97da5-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="97da5-256">Теперь вы готовы к следующему шагу — публикации приложения в Azure и тестировании его.</span><span class="sxs-lookup"><span data-stu-id="97da5-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="97da5-257">F.</span><span class="sxs-lookup"><span data-stu-id="97da5-257">F.</span></span> <span data-ttu-id="97da5-258">Публикация веб-приложения в Azure и его тестирование</span><span class="sxs-lookup"><span data-stu-id="97da5-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="97da5-259">Далее вы опубликуете приложение в веб-приложение службы приложений и протестируете его, чтобы увидеть, как настроенное ранее гибридное подключение используется для подключения веб-приложения к базе данных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="97da5-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="97da5-260">Публикация веб-приложения</span><span class="sxs-lookup"><span data-stu-id="97da5-260">Publish the web application</span></span>
1. <span data-ttu-id="97da5-261">Можно загрузить свой профиль публикации для данного веб-приложения службы приложений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="97da5-262">В колонке веб-приложения нажмите **Загрузить профиль публикации**и сохраните файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="97da5-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Загрузить профиль публикации][PortalDownloadPublishProfile]
   
    <span data-ttu-id="97da5-264">Далее вы импортируете этот файл в веб-приложение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97da5-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="97da5-265">В Visual Studio щелкните правой кнопкой мыши имя проекта в обозревателе решений и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="97da5-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Выбор публикации][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="97da5-267">В диалоговом окне **Публикация веб-сайта** на вкладке **Профиль** выберите элемент **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="97da5-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Импорт][HCVSPublishWebDialogImport]
4. <span data-ttu-id="97da5-269">Откройте скачанный профиль публикации, выберите его и щелкните кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="97da5-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Открытие профиля][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="97da5-271">Сведения о публикации импортируются и отображаются на вкладке **Подключение** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="97da5-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Нажмите кнопку "Опубликовать"][HCVSClickPublish]
   
    <span data-ttu-id="97da5-273">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="97da5-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="97da5-274">По завершении публикации браузер запустит и покажет знакомое приложение ASP.NET, которое теперь еще и работает в облаке Azure!</span><span class="sxs-lookup"><span data-stu-id="97da5-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="97da5-275">Далее вы используете веб-приложение, чтобы увидеть гибридные подключения в действии.</span><span class="sxs-lookup"><span data-stu-id="97da5-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="97da5-276">Тестирование полного веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="97da5-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="97da5-277">В правом верхнем углу веб-страницы Azure нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="97da5-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Тестирование входа][HCTestLogIn]
2. <span data-ttu-id="97da5-279">Веб-приложение службы приложений теперь подключено к базе данных участников веб-приложения на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="97da5-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="97da5-280">Чтобы проверить это, войдите с помощью тех же учетных данных, которые указали в локальной базе данных раньше.</span><span class="sxs-lookup"><span data-stu-id="97da5-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Приветствие][HCTestHelloContoso]
3. <span data-ttu-id="97da5-282">Для дальнейшего тестирования гибридного подключения выйдите из веб-приложения Azure и зарегистрируйте другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="97da5-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="97da5-283">Укажите новое имя пользователя и пароль, а затем щелкните кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="97da5-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Тестирование регистрации другого пользователя][HCTestRegisterRelecloud]
4. <span data-ttu-id="97da5-285">Чтобы убедиться, что учетные данные нового пользователя сохранены в локальной базе данных с помощью гибридного подключения, откройте SQL Management Studio на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="97da5-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="97da5-286">Разверните в обозревателе объектов базу данных **MembershipDB**, а затем разверните узел **Таблицы**.</span><span class="sxs-lookup"><span data-stu-id="97da5-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="97da5-287">Щелкните правой кнопкой мыши таблицу участников **dbo.AspNetUsers** и выберите пункт **Select Top 1000 Rows** (Выбрать первые 1000 строк), чтобы просмотреть результаты.</span><span class="sxs-lookup"><span data-stu-id="97da5-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![Просмотр результатов][HCTestSSMSTree]
5. <span data-ttu-id="97da5-289">В локальной таблице участников теперь отображаются обе учетные записи: созданная локально и созданная в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="97da5-290">Учетная запись, созданная в облаке, сохранена в локальной базе данных с помощью функции гибридного подключения Azure.</span><span class="sxs-lookup"><span data-stu-id="97da5-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Зарегистрированные пользователи в локальной базе данных][HCTestShowMemberDb]

<span data-ttu-id="97da5-292">Теперь вы создали и развернули веб-приложение ASP.NET, которое использует гибридное подключение между веб-приложением в облаке Azure и локальной базой данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97da5-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="97da5-293">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="97da5-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="97da5-294">См. также</span><span class="sxs-lookup"><span data-stu-id="97da5-294">See Also</span></span>
[<span data-ttu-id="97da5-295">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="97da5-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="97da5-296">Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="97da5-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="97da5-297">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="97da5-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="97da5-298">Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"</span><span class="sxs-lookup"><span data-stu-id="97da5-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="97da5-299">Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="97da5-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="97da5-300">Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="97da5-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="97da5-301">Общие сведения об удостоверениях ASP.NET</span><span class="sxs-lookup"><span data-stu-id="97da5-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
