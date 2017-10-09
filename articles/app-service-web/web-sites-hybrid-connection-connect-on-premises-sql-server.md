---
title: "aaaConnect tooon локальный SQL Server из веб-приложения в службе приложений Azure с помощью гибридных подключений"
description: "Создание веб-приложения в Microsoft Azure и подключите его tooan базы данных SQL Server в локальной среде"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="a8297-103">Подключение локальной tooon SQL Server из веб-приложения в службе приложений Azure с помощью гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="a8297-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="a8297-104">Гибридные подключения могут подключаться [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) ресурсов tooon локальный веб-приложения, используется ли статический порт TCP.</span><span class="sxs-lookup"><span data-stu-id="a8297-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="a8297-105">Поддерживаются такие ресурсы: Microsoft SQL Server, MySQL, веб-API HTTP, служба приложений и большинство настраиваемых веб-служб.</span><span class="sxs-lookup"><span data-stu-id="a8297-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="a8297-106">В этом учебнике вы узнаете, как приложение в hello веб-службы приложения toocreate [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715), подключение hello web приложения tooyour локальной базы данных SQL Server с помощью новой функции гибридного подключения hello, создания простого ASP.NET приложение, которое будет использовать hello гибридного подключения и развертывать приложения hello toohello веб-приложения служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a8297-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="a8297-107">Hello завершения веб-приложения в Azure хранит учетные данные пользователя в базе данных членства, расположенном на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8297-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="a8297-108">Hello учебником нет опыта работы с Azure или ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8297-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="a8297-109">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="a8297-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a8297-110">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="a8297-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="a8297-111">часть функции hello гибридные подключения веб-приложения Hello доступен только в hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8297-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="a8297-112">toocreate соединений в службах BizTalk. в разделе [гибридные подключения](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="a8297-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a8297-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8297-113">Prerequisites</span></span>
<span data-ttu-id="a8297-114">toocomplete этого учебника вам потребуется hello следующие продукты.</span><span class="sxs-lookup"><span data-stu-id="a8297-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="a8297-115">У всех этих продуктов есть бесплатные версии, так что можно начать разработку для Azure полностью бесплатно.</span><span class="sxs-lookup"><span data-stu-id="a8297-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="a8297-116">**Подписка Azure**. Сведения о бесплатной подписке см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8297-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="a8297-117">**Visual Studio 2013** -разделе бесплатную ознакомительную версию Visual Studio 2013 toodownload [загрузки Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="a8297-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="a8297-118">Прежде чем продолжить, установите этот продукт.</span><span class="sxs-lookup"><span data-stu-id="a8297-118">Install this before continuing.</span></span>
* <span data-ttu-id="a8297-119">**Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1)**. Если вы используете операционную систему Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 или Windows Server 2008 R2, ее можно включить на панели управления, последовательно выбрав "Программы и компоненты", "Включение или отключение компонентов Windows".</span><span class="sxs-lookup"><span data-stu-id="a8297-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="a8297-120">В противном случае ее можно загрузить с hello [центра загрузки Майкрософт](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="a8297-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="a8297-121">**SQL Server 2014 Express с инструментами** -Microsoft SQL Server Express для бесплатной загрузки в hello [страницу Microsoft веб-платформы, база данных](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8297-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="a8297-122">Выберите hello **Express** (не LocalDB) версии.</span><span class="sxs-lookup"><span data-stu-id="a8297-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="a8297-123">Hello **Express с инструментами** версия включает SQL Server Management Studio, который будет использоваться в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a8297-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="a8297-124">**SQL Server Management Studio Express** — это входят в состав SQL Server 2014 Express hello загрузки средства было сказано выше, но при необходимости tooinstall его отдельно, можно загрузить и установить его с hello [SQL Server Express Страница загрузки](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8297-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="a8297-125">Hello учебнике предполагается, что у вас есть подписка Azure, что вы установили Visual Studio 2013, и что вы установили или включить .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="a8297-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="a8297-126">Hello учебнике рассказывается о том, как tooinstall SQL Server 2014 Express в конфигурации, которая хорошо подходит для гибридных подключений hello Azure компонентов (экземпляр по умолчанию с помощью статического порта TCP).</span><span class="sxs-lookup"><span data-stu-id="a8297-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="a8297-127">Перед началом работы с учебником hello Загрузите SQL Server 2014 Express с инструментами из папки hello, упомянутых выше, если у вас установлен SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="a8297-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="a8297-128">Notes</span></span>
<span data-ttu-id="a8297-129">toouse в локальной среде SQL Server или SQL Server, экспресс-выпуск базы данных с помощью гибридного подключения, TCP/IP должен toobe, включена ли статический порт.</span><span class="sxs-lookup"><span data-stu-id="a8297-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="a8297-130">Экземпляры SQL Server по умолчанию используют статический порт 1433, а именованные экземпляры не используют этот порт.</span><span class="sxs-lookup"><span data-stu-id="a8297-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="a8297-131">Hello компьютера, на котором устанавливается hello локальный диспетчер гибридного подключения агента:</span><span class="sxs-lookup"><span data-stu-id="a8297-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="a8297-132">Необходимо иметь tooAzure исходящие подключения через:</span><span class="sxs-lookup"><span data-stu-id="a8297-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="a8297-133">Порт</span><span class="sxs-lookup"><span data-stu-id="a8297-133">Port</span></span> | <span data-ttu-id="a8297-134">Назначение</span><span class="sxs-lookup"><span data-stu-id="a8297-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="a8297-135">80</span><span class="sxs-lookup"><span data-stu-id="a8297-135">80</span></span> |<span data-ttu-id="a8297-136">**Требуется** для порта HTTP при проверке сертификатов и (необязательно) для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="a8297-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="a8297-137">443</span><span class="sxs-lookup"><span data-stu-id="a8297-137">443</span></span> |<span data-ttu-id="a8297-138">**Необязательно** для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="a8297-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="a8297-139">В случае недоступности too443 исходящие подключения используется TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="a8297-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="a8297-140">5671 и 9352</span><span class="sxs-lookup"><span data-stu-id="a8297-140">5671 and 9352</span></span> |<span data-ttu-id="a8297-141">**Рекомендуется** , но необязательно для подключения к данным.</span><span class="sxs-lookup"><span data-stu-id="a8297-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="a8297-142">Обратите внимание, что в этом режиме обеспечивается более высокая пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="a8297-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="a8297-143">В случае недоступности toothese портов исходящей связи используется TCP-порт 443.</span><span class="sxs-lookup"><span data-stu-id="a8297-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="a8297-144">Должен быть hello может tooreach *hostname*:*Номер_порта* локального ресурса.</span><span class="sxs-lookup"><span data-stu-id="a8297-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="a8297-145">Hello в этой статье предполагается, что вы используете браузер hello hello компьютере, где будет размещаться агент hello локальной гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="a8297-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="a8297-146">Если уже имеется SQL Server, установленный в конфигурации и в среде, которая соответствует условиям hello, описанных выше, можно пропустить и начинаться с [создать базу данных SQL Server в локальной](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="a8297-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="a8297-147">О.</span><span class="sxs-lookup"><span data-stu-id="a8297-147">A.</span></span> <span data-ttu-id="a8297-148">Установка экспресс-выпуска SQL Server, включение TCP/IP и создание локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="a8297-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="a8297-149">В этом разделе показано, как включить протокол TCP/IP и создать базу данных, веб-приложение будет работать с портала Azure hello tooinstall SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="a8297-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="a8297-150">Установка SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="a8297-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="a8297-151">SQL Server Express, tooinstall запуска hello **SQLEXPRWT_x64_ENU.exe** или **SQLEXPR_x86_ENU.exe** загруженный файл.</span><span class="sxs-lookup"><span data-stu-id="a8297-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="a8297-152">Откроется мастер Hello центр установки SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![Установка SQL Server][SQLServerInstall]
2. <span data-ttu-id="a8297-154">Выберите **автономная установка нового SQL Server или добавление компонентов tooan существующей установки**.</span><span class="sxs-lookup"><span data-stu-id="a8297-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="a8297-155">Следуйте инструкциям hello, принимающий параметры по умолчанию hello и параметры, пока не будет получен toohello **конфигурации экземпляра** страницы.</span><span class="sxs-lookup"><span data-stu-id="a8297-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="a8297-156">На hello **конфигурации экземпляра** выберите **экземпляр по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="a8297-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Выбор экземпляра по умолчанию][ChooseDefaultInstance]
   
    <span data-ttu-id="a8297-158">По умолчанию hello по умолчанию экземпляра SQL Server прослушивает запросы от клиентов SQL Server статический порт 1433, являющееся какие hello гибридные подключения компонента необходимо.</span><span class="sxs-lookup"><span data-stu-id="a8297-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="a8297-159">Именованные экземпляры используют динамические порты и UDP, которые не поддерживаются гибридными подключениями.</span><span class="sxs-lookup"><span data-stu-id="a8297-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="a8297-160">Примите значения по умолчанию hello в hello **конфигурации сервера** страницы.</span><span class="sxs-lookup"><span data-stu-id="a8297-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="a8297-161">На hello **Настройка компонента Database Engine** в разделе **режим проверки подлинности**, выберите **смешанный режим (проверка подлинности SQL Server и Windows)**и укажите пароль.</span><span class="sxs-lookup"><span data-stu-id="a8297-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Выбор смешанного режима][ChooseMixedMode]
   
    <span data-ttu-id="a8297-163">В этом учебнике вы будете использовать проверку подлинности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="a8297-164">Быть убедиться, что tooremember hello пароля, так как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="a8297-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="a8297-165">Пошагово rest hello toocomplete hello приветствия мастера установки.</span><span class="sxs-lookup"><span data-stu-id="a8297-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="a8297-166">Включение TCP/IP</span><span class="sxs-lookup"><span data-stu-id="a8297-166">Enable TCP/IP</span></span>
<span data-ttu-id="a8297-167">tooenable TCP/IP, используется диспетчер конфигурации SQL Server, который был установлен при установке SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="a8297-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="a8297-168">Следуйте указаниям hello [включить сетевой протокол TCP/IP для SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="a8297-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="a8297-169">Создание локальной базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="a8297-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="a8297-170">Для веб-приложения Visual Studio требуется база данных участников, к которой может получить доступ Azure.</span><span class="sxs-lookup"><span data-stu-id="a8297-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="a8297-171">Это требуется SQL Server или SQL Server, экспресс-выпуск базы данных (не hello LocalDB базы данных, hello использование шаблона MVC по умолчанию), поэтому вы создадите базы данных членства hello рядом.</span><span class="sxs-lookup"><span data-stu-id="a8297-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="a8297-172">В SQL Server Management Studio подключитесь toohello был только что установлен SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="a8297-173">(Если hello **подключения tooServer** окно не открывается автоматически, перейдите в слишком**обозревателя объектов** hello левой панели щелкните **Connect**и нажмите кнопку **Компонент database Engine**.) ![Подключение tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="a8297-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="a8297-174">Для параметра **Тип сервера** выберите значение **Ядро СУБД**.</span><span class="sxs-lookup"><span data-stu-id="a8297-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="a8297-175">Для **имя сервера**, можно использовать **localhost** или имя hello hello компьютера, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="a8297-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="a8297-176">Выберите **проверки подлинности SQL Server**и войдите в систему с учетной записи SA hello и hello пароль, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="a8297-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="a8297-177">Щелкните правой кнопкой мыши toocreate новую базу данных с помощью SQL Server Management Studio **баз данных** в обозревателе объектов и выберите **новой базы данных**.</span><span class="sxs-lookup"><span data-stu-id="a8297-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Создание базы данных][SSMScreateNewDB]
3. <span data-ttu-id="a8297-179">В hello **новую базу данных** диалоговое окно, введите MembershipDB hello имени базы данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8297-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Предоставление имени базы данных][SSMSprovideDBname]
   
    <span data-ttu-id="a8297-181">Обратите внимание, что вы не выполните любую базу данных toohello изменения на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="a8297-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="a8297-182">сведения о членстве Hello будут добавлены автоматически позже веб-приложением при его запуске.</span><span class="sxs-lookup"><span data-stu-id="a8297-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="a8297-183">В обозревателе объектов, если развернуть **баз данных**, вы увидите, будет создана база данных членства, hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![Создана MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="a8297-185">B.</span><span class="sxs-lookup"><span data-stu-id="a8297-185">B.</span></span> <span data-ttu-id="a8297-186">Создание веб-приложения в hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="a8297-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="a8297-187">Если вы уже создали веб-приложения в портале Azure, что в этом учебнике требуется toouse hello, можно сразу перейти слишком[создать гибридное подключение и служба BizTalk](#CreateHC) и продолжить оттуда.</span><span class="sxs-lookup"><span data-stu-id="a8297-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="a8297-188">В hello [портала Azure](https://portal.azure.com), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8297-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Кнопка «Создать»][New]
2. <span data-ttu-id="a8297-190">Настройте веб-приложение и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8297-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. <span data-ttu-id="a8297-192">Через несколько секунд hello веб-приложения создается и отображается колонке web app.</span><span class="sxs-lookup"><span data-stu-id="a8297-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="a8297-193">Hello колонка предназначена поддерживающим вертикальную прокрутку, позволяющий управлять веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a8297-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
   
    <span data-ttu-id="a8297-195">веб-приложения hello tooverify динамической, можно нажать hello **Обзор** страница по умолчанию hello toodisplay значок.</span><span class="sxs-lookup"><span data-stu-id="a8297-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="a8297-196">Затем вы создадите гибридного подключения и служба BizTalk для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="a8297-197">C.</span><span class="sxs-lookup"><span data-stu-id="a8297-197">C.</span></span> <span data-ttu-id="a8297-198">Создание гибридного подключения и службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="a8297-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="a8297-199">Назад в hello портала, go toosettings и нажмите кнопку **сети** > **настроить конечные точки гибридного подключения**.</span><span class="sxs-lookup"><span data-stu-id="a8297-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Гибридные подключения][CreateHCHCIcon]
2. <span data-ttu-id="a8297-201">В колонке подключений гибридного hello, нажмите кнопку **добавить** > **гибридное подключение**.</span><span class="sxs-lookup"><span data-stu-id="a8297-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="a8297-202">На hello **создать гибридное подключение** колонки:</span><span class="sxs-lookup"><span data-stu-id="a8297-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="a8297-203">Для **имя**, введите имя для соединения hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="a8297-204">Для **Hostname**, введите имя компьютера hello главный компьютер SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="a8297-205">Для **порт**, введите 1433 (порт по умолчанию hello для SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a8297-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="a8297-206">Нажмите кнопку **службы BizTalk** > **новую службу BizTalk** и введите имя для hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a8297-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Создание гибридного подключения][TwinCreateHCBlades]
4. <span data-ttu-id="a8297-208">Нажмите **ОК** дважды.</span><span class="sxs-lookup"><span data-stu-id="a8297-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="a8297-209">Когда hello завершения процесса hello **уведомления** области будет мигать зеленым **успех** и hello **гибридное подключение** колонке покажет hello гибридное подключение с Здравствуйте, состояние как **не подключен**.</span><span class="sxs-lookup"><span data-stu-id="a8297-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

<span data-ttu-id="a8297-211">На этом этапе вы прошли важной частью гибридного подключения hello облачной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a8297-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="a8297-212">Далее вы создадите соответствующую локальную часть.</span><span class="sxs-lookup"><span data-stu-id="a8297-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="a8297-213">D.</span><span class="sxs-lookup"><span data-stu-id="a8297-213">D.</span></span> <span data-ttu-id="a8297-214">Установка подключения к hello toocomplete hello локальный диспетчер гибридного подключения</span><span class="sxs-lookup"><span data-stu-id="a8297-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="a8297-215">Стало ИТ-инфраструктуры hello гибридное подключение будет создать веб-приложения, которые его используют.</span><span class="sxs-lookup"><span data-stu-id="a8297-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="a8297-216">E.</span><span class="sxs-lookup"><span data-stu-id="a8297-216">E.</span></span> <span data-ttu-id="a8297-217">Создание базовых веб-проекта ASP.NET и изменить строку подключения базы данных hello локально запустить проект hello</span><span class="sxs-lookup"><span data-stu-id="a8297-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="a8297-218">Создание базового проекта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8297-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="a8297-219">В Visual Studio в hello **файл** меню, создайте новый проект:</span><span class="sxs-lookup"><span data-stu-id="a8297-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![Новый проект Visual Studio][HCVSNewProject]
2. <span data-ttu-id="a8297-221">В hello **шаблоны** раздел hello **новый проект** диалогового окна выберите **Web** и выберите **веб-приложение ASP.NET**и нажмите кнопку  **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8297-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Выбор веб-приложения ASP.NET][HCVSChooseASPNET]
3. <span data-ttu-id="a8297-223">В hello **новый проект ASP.NET** диалоговое окно, выберите **MVC**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8297-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Выбор MVC][HCVSChooseMVC]
4. <span data-ttu-id="a8297-225">При создании проекта hello открывается страница сведений приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="a8297-226">Еще не запущены hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="a8297-226">Do not run hello web project yet.</span></span>
   
    ![Страница файла сведений][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="a8297-228">Изменить строку соединения hello базы данных для приложения hello</span><span class="sxs-lookup"><span data-stu-id="a8297-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="a8297-229">На данном этапе изменить hello строку подключения, которая указывает приложения где toofind локального SQL Server Express базы данных.</span><span class="sxs-lookup"><span data-stu-id="a8297-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="a8297-230">Строка подключения Hello — в файле Web.config приложения hello, который содержит сведения о конфигурации для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="a8297-231">tooensure, который использует приложение hello базы данных, созданную в SQL Server Express, а не hello один в Visual Studio по умолчанию, LocalDB, очень важно выполнить этот шаг перед запуском проекта.</span><span class="sxs-lookup"><span data-stu-id="a8297-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="a8297-232">В обозревателе решений дважды щелкните файл Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="a8297-234">Изменить hello **connectionStrings** раздел базы данных SQL Server toopoint toohello на локальном компьютере, используя синтаксис hello в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="a8297-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Строка подключения][HCVSConnectionString]
   
    <span data-ttu-id="a8297-236">При создании строки подключения hello, имейте в виду следующие hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="a8297-237">Если вы подключаетесь tooa именованного экземпляра, а не как экземпляр по умолчанию (например, YourServer\SQLEXPRESS), необходимо настроить статические порты toouse SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="a8297-238">Сведения о настройке статических портов см. в разделе [как tooconfigure toolisten SQL Server через определенный порт](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="a8297-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="a8297-239">По умолчанию именованные экземпляры используют UDP и динамические порты, которые не поддерживаются гибридными подключениями.</span><span class="sxs-lookup"><span data-stu-id="a8297-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="a8297-240">Рекомендуется указывать hello порт (1433 по умолчанию, как показано в примере hello) в строке подключения hello, так что можно быть уверенным, что локальный SQL Server имеется включенный протокол TCP и использует правильный порт hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="a8297-241">Не забывайте tooconnect toouse проверки подлинности SQL Server, указав hello идентификатор пользователя и пароль в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="a8297-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="a8297-242">Нажмите кнопку **Сохранить** в файле Web.config hello toosave Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8297-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="a8297-243">Запустите проект hello локально и регистрации нового пользователя</span><span class="sxs-lookup"><span data-stu-id="a8297-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="a8297-244">Теперь запустите новый веб-проект локально, нажав кнопку обзора hello в области отладки.</span><span class="sxs-lookup"><span data-stu-id="a8297-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="a8297-245">В этом примере используется Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a8297-245">This example uses Internet Explorer.</span></span>
   
    ![Запуск проекта][HCVSRunProject]
2. <span data-ttu-id="a8297-247">В правом верхнем углу hello веб-страницы по умолчанию hello и выберите **зарегистрировать** tooregister новой учетной записи:</span><span class="sxs-lookup"><span data-stu-id="a8297-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Регистрация новой учетной записи][HCVSRegisterLocally]
3. <span data-ttu-id="a8297-249">Введите имя пользователя и пароль:</span><span class="sxs-lookup"><span data-stu-id="a8297-249">Enter a user name and password:</span></span>
   
    ![Ввод имени пользователя и пароля][HCVSCreateNewAccount]
   
    <span data-ttu-id="a8297-251">Это автоматически создает базу данных на локальном сервере SQL, содержащий сведения о членстве hello для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a8297-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="a8297-252">Одной из таблиц hello (**dbo. AspNetUsers**) содержит веб-приложения, как те, которые вы ввели hello учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8297-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="a8297-253">Вы увидите далее в учебнике hello в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="a8297-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="a8297-254">Закройте окно браузера hello веб-страницы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="a8297-255">При этом прекращается выполнение приложения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8297-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="a8297-256">Все готово для hello следующий шаг — tooAzure приложения hello toopublish и проверить его.</span><span class="sxs-lookup"><span data-stu-id="a8297-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="a8297-257">F.</span><span class="sxs-lookup"><span data-stu-id="a8297-257">F.</span></span> <span data-ttu-id="a8297-258">Публикация tooAzure приложения hello web и проверить его</span><span class="sxs-lookup"><span data-stu-id="a8297-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="a8297-259">Теперь будет опубликовать tooyour вашего приложения службы приложений веб-приложение и проверить его toosee как hello гибридного подключения, ранее — идет используется tooconnect вашего приложения для веб-toohello база данных на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8297-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="a8297-260">Публикация веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="a8297-260">Publish hello web application</span></span>
1. <span data-ttu-id="a8297-261">Вы можете загрузить профиль публикации для hello веб-приложения служб приложений в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a8297-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="a8297-262">В колонке hello веб-приложения, нажмите кнопку **получение профиля публикации**и сохраните hello файл tooyour компьютера.</span><span class="sxs-lookup"><span data-stu-id="a8297-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Загрузить профиль публикации][PortalDownloadPublishProfile]
   
    <span data-ttu-id="a8297-264">Далее вы импортируете этот файл в веб-приложение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8297-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="a8297-265">В Visual Studio, щелкните правой кнопкой мыши имя проекта hello в обозревателе решений и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="a8297-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Выбор публикации][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="a8297-267">В hello **веб-публикация** диалоговое окно на hello **профиль** выберите **импорта**.</span><span class="sxs-lookup"><span data-stu-id="a8297-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Импорт][HCVSPublishWebDialogImport]
4. <span data-ttu-id="a8297-269">Обзор tooyour загрузить профиль публикации, выберите его и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8297-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Обзор tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="a8297-271">Данные публикации импортируется и отображает на hello **подключения** вкладка диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a8297-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Нажмите кнопку "Опубликовать"][HCVSClickPublish]
   
    <span data-ttu-id="a8297-273">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="a8297-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="a8297-274">По завершении публикации браузере запустится и Показать теперь знакомые приложения ASP.NET--, за исключением того, что он в активном состоянии в облаке Azure hello!</span><span class="sxs-lookup"><span data-stu-id="a8297-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="a8297-275">Далее используется вашей toosee приложения динамической web его гибридное подключение в действии.</span><span class="sxs-lookup"><span data-stu-id="a8297-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="a8297-276">Hello тест завершения веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="a8297-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="a8297-277">В верхней части hello справа от веб-страницы в Azure, выберите **входа**.</span><span class="sxs-lookup"><span data-stu-id="a8297-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Тестирование входа][HCTestLogIn]
2. <span data-ttu-id="a8297-279">Приложение службы, веб-приложения сейчас подключение базы данных членства tooyour веб-приложения на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8297-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="a8297-280">tooverify этого, войдите в систему под hello учетные данные, введенные в hello локальной базы данных более ранней версии.</span><span class="sxs-lookup"><span data-stu-id="a8297-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Приветствие][HCTestHelloContoso]
3. <span data-ttu-id="a8297-282">toofurther тестирование нового гибридного подключения, выйти из системы веб-приложения Azure и зарегистрировать в качестве другого пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8297-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="a8297-283">Укажите новое имя пользователя и пароль, а затем щелкните кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="a8297-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Тестирование регистрации другого пользователя][HCTestRegisterRelecloud]
4. <span data-ttu-id="a8297-285">что hello новые учетные данные пользователя хранятся в локальной базы данных через подключение к гибридного tooverify откройте SQL Management Studio на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8297-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="a8297-286">В обозревателе объектов разверните hello **MembershipDB** базы данных, а затем разверните **таблиц**.</span><span class="sxs-lookup"><span data-stu-id="a8297-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="a8297-287">Щелкните правой кнопкой мыши hello **dbo. AspNetUsers** членства таблицы и выберите **выделить 1000 верхних строк** tooview hello результаты.</span><span class="sxs-lookup"><span data-stu-id="a8297-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Просмотр результатов hello][HCTestSSMSTree]
5. <span data-ttu-id="a8297-289">Членство в локальной таблице теперь отображаются обе учетные записи - hello создан локально и hello подпись, которая создается в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a8297-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="a8297-290">подпись, которая создается в облаке hello Hello была сохранена tooyour локальной базы данных посредством функции гибридного подключения в Azure.</span><span class="sxs-lookup"><span data-stu-id="a8297-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Зарегистрированные пользователи в локальной базе данных][HCTestShowMemberDb]

<span data-ttu-id="a8297-292">Создания и развертывания веб-приложения ASP.NET, использующего гибридное подключение между веб-приложения в облако Azure hello и локальная база данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a8297-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="a8297-293">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a8297-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="a8297-294">См. также</span><span class="sxs-lookup"><span data-stu-id="a8297-294">See Also</span></span>
[<span data-ttu-id="a8297-295">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="a8297-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="a8297-296">Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a8297-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="a8297-297">Обзор гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="a8297-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="a8297-298">Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"</span><span class="sxs-lookup"><span data-stu-id="a8297-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="a8297-299">Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)</span><span class="sxs-lookup"><span data-stu-id="a8297-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="a8297-300">Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a8297-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="a8297-301">Общие сведения об удостоверениях ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a8297-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
