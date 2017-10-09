---
title: "aaaCreate служб Azure BizTalk в hello портал Azure | Документы Microsoft"
description: "Узнайте, как tooprovision или создание служб Azure BizTalk в hello портал Azure; MABS СЛУЖБЫ BIZTALK WINDOWS AZURE"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="d9bb2-103">Создание службы BizTalk с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="d9bb2-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="d9bb2-104">toosign в toohello портал Azure, требуется учетная запись Azure и подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="d9bb2-105">Если учетной записи нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="d9bb2-106">См. страницу [Бесплатная пробная версия Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="d9bb2-107"><a name="CreateService"></a>Создание службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="d9bb2-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="d9bb2-108">В зависимости от hello выбранного выпуска могут быть доступны не все параметры службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="d9bb2-109">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d9bb2-110">Hello нижней панели навигации, выберите **NEW**:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="d9bb2-111">![Выберите новую кнопку hello][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="d9bb2-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="d9bb2-112">Выберите **Службы приложений** > **Служба BizTalk** > **Настраиваемое создание**:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="d9bb2-113">![Выбор элементов "Служба BizTalk" и "Настраиваемое создание"][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="d9bb2-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="d9bb2-114">Введите параметры hello службы BizTalk:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="d9bb2-115"><strong>Имя службы BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-116">Можно ввести любое имя, но рекомендуется использовать конкретные имена.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-116">You can enter any name but be specific.</span></span> <span data-ttu-id="d9bb2-117">Некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-117">Some examples include:</span></span><br/><br/><span data-ttu-id="d9bb2-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d9bb2-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d9bb2-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d9bb2-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d9bb2-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d9bb2-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="d9bb2-121">«. biztalk.windows.net» — имя автоматически добавлены toohello ввода.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="d9bb2-122">При этом создается URL-адреса, используемые tooaccess вашей BizTalk службы как <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-123"><strong>Выпуск</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-124">Если на этапе тестирования или разработки hello выберите <strong>разработчика</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="d9bb2-125">На этапе производства hello, использовать hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">службы BizTalk: схема с выпусками</a> toodetermine Если <strong>Premium</strong>, <strong>Стандартная</strong>, или <strong>Basic</strong>является правильным выбором hello для бизнес-сценария.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-126"><strong>Регион</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-127">Выделите службу BizTalk toohost hello географического региона.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-128"><strong>URL-адрес домена</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-129"><strong>Необязательно</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="d9bb2-130">По умолчанию используется URL-адрес домена hello <em>адрес YourBizTalkServiceName</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="d9bb2-131">Можно также указать пользовательский домен.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-131">A custom domain can also be entered.</span></span> <span data-ttu-id="d9bb2-132">Например, если вы используете домен <em>contoso</em>, можно ввести следующее:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="d9bb2-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d9bb2-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="d9bb2-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d9bb2-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d9bb2-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d9bb2-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d9bb2-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d9bb2-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="d9bb2-137">Выберите стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="d9bb2-138">5.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-138">5.</span></span> <span data-ttu-id="d9bb2-139">Введите hello хранения и настройки базы данных:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d9bb2-140"><strong>Учетная запись хранения для мониторинга и архивации</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-141">Выберите существующую учетную запись хранения или параметр «Создать новую учетную запись хранения».</span><span class="sxs-lookup"><span data-stu-id="d9bb2-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="d9bb2-142">При создании новой учетной записи хранения, введите hello <strong>имя учетной записи хранения</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-143"><strong>База данных отслеживания</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-144">Если используется существующая база данных SQL Azure, ее нельзя использовать в другой службе BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="d9bb2-145">Необходимо hello имя входа и пароль, введенный в процессе создания этот сервер базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="d9bb2-146"><strong>Совет</strong> создать базу данных отслеживания hello и учетной записи мониторинга и архивации на hello же регионе, как hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="d9bb2-147">Выберите стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="d9bb2-148">6.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-148">6.</span></span> <span data-ttu-id="d9bb2-149">Введите параметры hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d9bb2-150"><strong>Имя</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-151">Доступна при <strong>создать новый экземпляр базы данных SQL</strong> выбранных в предыдущем экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d9bb2-152">Введите toobe имя базы данных SQL, используемой службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-153"><strong>Сервер</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-154">Доступна при <strong>создать новый экземпляр базы данных SQL</strong> выбранных в предыдущем экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d9bb2-155">Выберите существующий сервер базы данных SQL или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-156"><strong>Имя входа на сервер</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-157">Введите имя пользователя для входа в систему hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-158"><strong>Пароль для входа на сервер</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-159">Введите пароль для входа hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d9bb2-160"><strong>Регион</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d9bb2-161">Параметр доступен, если выбран параметр <strong>Создать экземпляр базы данных SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="d9bb2-162">Выберите географический регион toohost hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="d9bb2-163">Выберите hello флажок toocomplete приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="d9bb2-164">появится значок хода выполнения Hello:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-164">hello progress icon appears:</span></span>  
![Значок хода выполнения, отображаемый при завершении процесса][ProgressComplete]

<span data-ttu-id="d9bb2-166">По завершении hello службы Azure BizTalk, созданы и готовы для ваших приложений.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="d9bb2-167">значения по умолчанию Hello подходят.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-167">hello default settings are sufficient.</span></span> <span data-ttu-id="d9bb2-168">Параметры по умолчанию hello toochange установите **службы BIZTALK** в hello левой панели навигации, а затем выберите службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="d9bb2-169">Дополнительные параметры отображаются на hello [вкладки панели мониторинга, монитора и масштабирования](biztalk-dashboard-monitor-scale-tabs.md) вверху hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="d9bb2-170">В зависимости от состояния hello hello службы BizTalk существуют некоторые операции, которые не может быть завершена.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="d9bb2-171">Список этих операций, go слишком[диаграммы состояния служб BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="d9bb2-172">Действия после подготовки</span><span class="sxs-lookup"><span data-stu-id="d9bb2-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="d9bb2-173">Установите сертификат hello на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="d9bb2-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="d9bb2-174">Добавление готового сертификата для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="d9bb2-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="d9bb2-175">Получение имен Access Control hello</span><span class="sxs-lookup"><span data-stu-id="d9bb2-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="d9bb2-176"><a name="InstallCert"></a>Установите сертификат hello на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="d9bb2-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="d9bb2-177">На этапе подготовки службы BizTalk создается самозаверяющий сертификат, который связывается с вашей подпиской службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="d9bb2-178">Необходимо загрузить этот сертификат и установить его на компьютерах, в котором развертывания приложений службы BizTalk или отправки сообщений tooa конечной точки службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="d9bb2-179">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d9bb2-180">Выберите **службы BIZTALK** в hello левой панели навигации, а затем выберите подписке на службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="d9bb2-181">Выберите hello **мониторинга** вкладки.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="d9bb2-182">Выберите **Загрузить SSL-сертификат**:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="d9bb2-183">![Изменение SSL-сертификата][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="d9bb2-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="d9bb2-184">Дважды щелкните сертификат hello и выполните приветствия мастера tooinstall hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="d9bb2-185">Убедитесь, что установить сертификат hello hello **доверенные корневые центры сертификации** хранения.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="d9bb2-186"><a name="AddCert"></a>Добавление готового сертификата для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="d9bb2-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="d9bb2-187">Hello самозаверяющий сертификат, который создается автоматически при создании службы BizTalk предназначен для использования в средах разработки только.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="d9bb2-188">Для выполнения рабочих сценариев замените его готовым сертификатом для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="d9bb2-189">На hello **мониторинга** выберите **обновления SSL-сертификат**.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="d9bb2-190">Обзор tooyour закрытый сертификат SSL (*CertificateName*PFX-файл), включает имя службы BizTalk, введите пароль hello и нажмите кнопку флажок hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="d9bb2-191"><a name="ACS"></a>Получение имен Access Control hello</span><span class="sxs-lookup"><span data-stu-id="d9bb2-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="d9bb2-192">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d9bb2-193">Выберите **службы BIZTALK** в hello левой панели навигации, а затем выберите службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="d9bb2-194">На панели задач hello, выберите **сведения о соединении**:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="d9bb2-195">![Выбор элемента "Сведения о подключении"][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="d9bb2-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="d9bb2-196">Скопируйте значения hello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="d9bb2-197">Это пространство имен Access Control вводится при развертывании проекта службы BizTalk из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d9bb2-198">пространство имен Access Control Hello автоматически создается для службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="d9bb2-199">значения Hello контроля доступа могут использоваться с любым приложением.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="d9bb2-200">При создании службы BizTalk Azure это пространство имен контроля доступа управляет hello проверку подлинности с помощью развертывания службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="d9bb2-201">Если требуется toochange hello подписки или управление приветствия имен, выберите **ACTIVE DIRECTORY** в hello левой панели навигации, а затем выберите пространство имен.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="d9bb2-202">панель задач Hello список параметров.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-202">hello task bar lists your options.</span></span>

<span data-ttu-id="d9bb2-203">Щелкнув **управление** Здравствуйте, откроется портал управления Access Control.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="d9bb2-204">В hello портал управления Access Control, hello служба BizTalk использует **удостоверения службы**:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="d9bb2-205">![Удостоверения службы ACS в hello портал управления Access Control][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="d9bb2-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="d9bb2-206">Hello удостоверение службы управления доступом — это набор учетных данных, которые позволяют приложениям или tooauthenticate клиентов напрямую с помощью контроля доступа и получать токен.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9bb2-207">Hello служба BizTalk использует **владельца** для удостоверения службы по умолчанию hello и hello **пароль** значение.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="d9bb2-208">Если вы используете значение симметричного ключа hello вместо hello значение пароля, hello может возникнуть следующая ошибка.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="d9bb2-209">*Не удалось подключиться учетной записи службы управления для управления доступом toohello hello указан учетные данные*</span><span class="sxs-lookup"><span data-stu-id="d9bb2-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="d9bb2-210">[Управление пространством имен ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) приведены некоторые правила и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="d9bb2-211">Пояснение требований</span><span class="sxs-lookup"><span data-stu-id="d9bb2-211">Requirements explained</span></span>
<span data-ttu-id="d9bb2-212">Эти требования не применяются toohello бесплатный выпуск.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="d9bb2-213"><strong>Необходимые элементы</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="d9bb2-214"><strong>Их назначение</strong></span><span class="sxs-lookup"><span data-stu-id="d9bb2-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d9bb2-215">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-215">Azure subscription</span></span></td>
<td><span data-ttu-id="d9bb2-216">Hello подписка определяет, кто может входить в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="d9bb2-217">Владелец учетной записи Hello создается подписка hello в <a HREF="https://account.windowsazure.com/Subscriptions"> подписок Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-218">Hello Azure учетная запись может иметь несколько подписок и можно управлять всеми пользователями, которым разрешено.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="d9bb2-219">Например, лица вашей учетной записи Azure создает подписку с именем <em>BizTalkServiceSubscription</em> и дает hello Администраторы BizTalk в вашей организации (например, ContosoBTSAdmins@live.com) получить доступ к подписке toothis.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="d9bb2-220">В этом сценарии Администраторы BizTalk hello вход toohello портал Azure и имеют полный администратор права tooall hello размещенных служб в подписке hello, включая службы Azure BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="d9bb2-221">Администраторы BizTalk Hello не будут носителями hello учетная запись Azure и нет сведений о выставлении счетов tooany доступа.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="d9bb2-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Управление подписками и учетными записями хранения в hello портал Azure</a> предоставляет дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="d9bb2-223">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d9bb2-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="d9bb2-224">Хранит hello таблицы, представления и хранимые процедуры, используемые hello службы BizTalk, включая данные отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-225">При создании службы BizTalk можно использовать существующий сервер SQL Server Azure, базу данных SQL Azure или автоматически создать новый сервер или базу данных.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-226">автоматически настраивается Hello масштабирование базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="d9bb2-227">Как правило масштаб по умолчанию hello достаточно для службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="d9bb2-228">Изменение масштаба hello влияет на цены.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="d9bb2-229">См. статью о <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">стоимости услуг Azure</a>
.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="d9bb2-230">
<strong>Примечания</strong>
</span><span class="sxs-lookup"><span data-stu-id="d9bb2-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="d9bb2-231">При создании нового сервера SQL Server и базы данных Azure автоматически включаются службы Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="d9bb2-232">Служба BizTalk Hello требуются службы Azure включить.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="d9bb2-233">При создании новой базы данных SQL Azure на существующем сервере SQL Azure, hello правила брандмауэра сервера не изменяются hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="d9bb2-234">В результате возможна других служб Azure не допускаются доступа toohello сервера баз данных.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="d9bb2-235">Пространство имен Azure Access Control</span><span class="sxs-lookup"><span data-stu-id="d9bb2-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="d9bb2-236">Выполняет проверку подлинности с помощью служб BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="d9bb2-237">Это пространство имен Access Control вводится при развертывании проекта службы BizTalk из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d9bb2-238">При создании службы BizTalk, автоматически создается пространство имен Access Control hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="d9bb2-239">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d9bb2-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="d9bb2-240">Предоставляет доступ tootables, больших двоичных объектов и очередей, используемых службой вашей службы BizTalk toosave hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="d9bb2-241">Файлы журналов, монитор hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="d9bb2-242">Привет, отслеживающую выходные данные также отображаются в hello **мониторинг** hello портал Azure на вкладке.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="d9bb2-243">При создании X12 или соглашения AS2 между партнерами, можно включить свойства сообщения toostore функция архивации hello.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="d9bb2-244">Эти данные сохраняются в hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d9bb2-245">При создании службы BizTalk можно использовать существующую или автоматически созданную новую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-246">настройки хранилища по умолчанию Hello достаточны для службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-247">При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="d9bb2-248">Эти ключи управляют tooyour доступа к учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="d9bb2-249">Hello службы BizTalk автоматически использует hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="d9bb2-250">Дополнительные сведения см. в статье <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Хранилище</a>.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="d9bb2-251">Закрытый сертификат SSL</span><span class="sxs-lookup"><span data-stu-id="d9bb2-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="d9bb2-252">При создании службы BizTalk Azure также создается URL-адрес HTTPS-узла, включающий имя службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="d9bb2-253">Этот URL-адрес будет автоматически настроенного toouse самозаверяющий сертификат только для разработки.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="d9bb2-254">На рабочем этапе вам потребуется личный SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="d9bb2-255">
<strong>Важные сведения об SSL-сертификате</strong>

</span><span class="sxs-lookup"><span data-stu-id="d9bb2-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="d9bb2-256">Срок действия сертификата Hello должно быть меньше 5 лет.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="d9bb2-257">Все личные сертификаты требуют наличия пароля.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-257">All private certificates require a password.</span></span> <span data-ttu-id="d9bb2-258">Запомните этот пароль, а также сообщите его вашим администраторам.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="d9bb2-259">Самозаверяющие сертификаты используются в средах разработки/тестирования.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="d9bb2-260">При использовании самозаверяющих сертификатов, импортируйте хранилище личных сертификатов tooyour сертификатов hello и hello хранилище сертификатов доверенных корневых центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="d9bb2-261">При отправке центра сертификации tooyour запрос сертификата hello производства, предоставьте hello следующие свойства сертификата:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="d9bb2-262"><strong>Расширенное использование ключа.</strong> Службы BizTalk Azure требуют как минимум проверки подлинности сервера.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="d9bb2-263"><strong>Общее имя</strong>: Введите hello полное доменное имя (FQDN) URL-адрес службы BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="d9bb2-264">См. раздел <a HREF="#CreateService">Создание службы BizTalk</a> в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d9bb2-265">После создания службы BizTalk hello можно добавить новые или другой сертификат.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="d9bb2-266">через гибридные подключения</span><span class="sxs-lookup"><span data-stu-id="d9bb2-266">Hybrid Connections</span></span>
<span data-ttu-id="d9bb2-267">При создании службы BizTalk Azure hello **гибридных подключений** вкладка доступна:</span><span class="sxs-lookup"><span data-stu-id="d9bb2-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![вкладка "Гибридные подключения"][HybridConnectionTab]

<span data-ttu-id="d9bb2-269">Гибридные подключения, используемые tooconnect Azure веб-сайта или tooany мобильной службы Azure локального ресурса, который использует статический порт TCP, таких как SQL Server, MySQL, веб-API HTTP, мобильных служб и большинство пользовательских веб-служб.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="d9bb2-270">Гибридные подключения и hello службы адаптера BizTalk отличаются.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="d9bb2-271">Hello службы адаптера BizTalk — используется tooconnect служб Azure BizTalk tooan в локальной строке из БИЗНЕС-системе.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="d9bb2-272">В разделе [гибридных подключений](integration-hybrid-connection-overview.md) toolearn, включая создание и управление гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9bb2-273">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9bb2-273">Next steps</span></span>
<span data-ttu-id="d9bb2-274">После создания службы BizTalk ознакомиться с разных hello [службы BizTalk: вкладки панели мониторинга, монитора и масштабирования](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="d9bb2-275">Служба BizTalk готова для использования в приложениях.</span><span class="sxs-lookup"><span data-stu-id="d9bb2-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="d9bb2-276">Создание приложений, перейдите в слишком toostart[служб Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="d9bb2-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="d9bb2-277">См. также</span><span class="sxs-lookup"><span data-stu-id="d9bb2-277">See also</span></span>
* [<span data-ttu-id="d9bb2-278">Службы BizTalk: диаграмма выпусков</span><span class="sxs-lookup"><span data-stu-id="d9bb2-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="d9bb2-279">Службы BizTalk: диаграмма состояния</span><span class="sxs-lookup"><span data-stu-id="d9bb2-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="d9bb2-280">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="d9bb2-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="d9bb2-281">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="d9bb2-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="d9bb2-282">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="d9bb2-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="d9bb2-283">Как я запустить с помощью hello пакета SDK служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="d9bb2-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="d9bb2-284">гибридных подключений</span><span class="sxs-lookup"><span data-stu-id="d9bb2-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
