---
title: "aaaHost несколько сайтов со шлюзом приложения Azure | Документы Microsoft"
description: "Эта страница предоставляет инструкции tooconfigure существующего шлюза приложения Azure для размещения нескольких веб-приложений на hello одного шлюза с портала Azure hello."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="32f49-103">Настройка шлюза приложений для размещения нескольких веб-приложений</span><span class="sxs-lookup"><span data-stu-id="32f49-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="32f49-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="32f49-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="32f49-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="32f49-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="32f49-106">Размещение нескольких сайтов позволяет toodeploy более одного веб-приложения на hello же шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="32f49-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="32f49-107">Он основывается на присутствие заголовка узла в hello входящего запроса HTTP, toodetermine прослушивателя, который будет получать трафик.</span><span class="sxs-lookup"><span data-stu-id="32f49-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="32f49-108">затем Hello прослушиватель направляет трафик tooappropriate внутреннего пула, настроенным в определение правил hello hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="32f49-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="32f49-109">В веб-приложениях включен протокол SSL шлюз приложений зависит от hello Указание имени сервера (SNI) расширения toochoose hello правильный прослушивателя для hello веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="32f49-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="32f49-110">Обычно используются для размещения нескольких сайтов — tooload балансировать нагрузку по запросам для другом доменах toodifferent серверных пулов.</span><span class="sxs-lookup"><span data-stu-id="32f49-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="32f49-111">Аналогичным образом несколько поддомены одного корневого домена также может быть размещена на приветствия hello же шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="32f49-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="32f49-112">Сценарий</span><span class="sxs-lookup"><span data-stu-id="32f49-112">Scenario</span></span>

<span data-ttu-id="32f49-113">В следующем примере hello, шлюз приложений обслуживает трафик для contoso.com и fabrikam.com с помощью двух серверных пулов: contoso пул серверов и fabrikam пул серверов.</span><span class="sxs-lookup"><span data-stu-id="32f49-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="32f49-114">Аналогичную программу установки может быть поддомены toohost используется как app.contoso.com и blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="32f49-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![сценарий с несколькими сайтами][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="32f49-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="32f49-116">Before you begin</span></span>

<span data-ttu-id="32f49-117">Этот сценарий добавляет поддержку нескольких сайтов tooan существующего приложения шлюза.</span><span class="sxs-lookup"><span data-stu-id="32f49-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="32f49-118">toocomplete этот сценарий существующего шлюза приложения должен доступных tooconfigure toobe.</span><span class="sxs-lookup"><span data-stu-id="32f49-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="32f49-119">Посетите [создать шлюз приложений с помощью портала hello](application-gateway-create-gateway-portal.md) toolearn как toocreate шлюз простого приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="32f49-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="32f49-120">представлены шаги hello нужен шлюз приложения hello tooupdate Hello:</span><span class="sxs-lookup"><span data-stu-id="32f49-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="32f49-121">Создание пулов серверной части toouse для каждого сайта.</span><span class="sxs-lookup"><span data-stu-id="32f49-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="32f49-122">Создание прослушивателя для каждого сайта, который поддерживает шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="32f49-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="32f49-123">Создайте правила toomap каждый прослушиватель с hello соответствующие серверной части.</span><span class="sxs-lookup"><span data-stu-id="32f49-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="32f49-124">Требования</span><span class="sxs-lookup"><span data-stu-id="32f49-124">Requirements</span></span>

* <span data-ttu-id="32f49-125">**Пул серверных:** hello список IP-адресов серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="32f49-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="32f49-126">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP.</span><span class="sxs-lookup"><span data-stu-id="32f49-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="32f49-127">Можно также использовать полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="32f49-127">FQDN can also be used.</span></span>
* <span data-ttu-id="32f49-128">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="32f49-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="32f49-129">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="32f49-130">**Интерфейсный порт:** этой цели используется порт hello открытый порт, который открыт в шлюзе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="32f49-131">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone серверов hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="32f49-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="32f49-132">**Прослушиватель:** hello прослушиватель имеет интерфейсный порт, протокол (Http или Https, эти значения зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки).</span><span class="sxs-lookup"><span data-stu-id="32f49-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="32f49-133">Для шлюзов приложений с поддержкой нескольких сайтов также добавляются имя узла и индикаторы SNI.</span><span class="sxs-lookup"><span data-stu-id="32f49-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="32f49-134">**Правило:** правило hello привязывает hello прослушивателя, пул серверных hello и определяет, какие серверных пула hello трафику следует применять направленной toowhen попадании конкретного прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="32f49-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="32f49-135">Правила обрабатываются в порядке hello, в котором они перечислены, а трафик будет направляться через hello первое подходящее правило вне зависимости от точности.</span><span class="sxs-lookup"><span data-stu-id="32f49-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="32f49-136">Например при наличии правила с помощью базовых прослушивателя и правила с помощью прослушивателя несколькими сайтами обоих на hello же порт, правило hello с прослушивателя hello нескольких сайтов, необходимо указать перед hello правило с прослушивателем basic hello в порядке для hello toofunction правило нескольких сайтов, как ожидается.</span><span class="sxs-lookup"><span data-stu-id="32f49-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="32f49-137">**Сертификаты:** каждый прослушиватель должен иметь уникальный сертификат. В этом примере мы создаем 2 прослушивателя для поддержки нескольких сайтов.</span><span class="sxs-lookup"><span data-stu-id="32f49-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="32f49-138">Два сертификаты PFX-файл и hello пароли для них должны toobe создан.</span><span class="sxs-lookup"><span data-stu-id="32f49-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="32f49-139">Создание пулов серверной части для каждого узла</span><span class="sxs-lookup"><span data-stu-id="32f49-139">Create back-end pools for each site</span></span>

<span data-ttu-id="32f49-140">Требуется отдельный внутренний пул для каждого сайта, который поддерживает шлюз приложений. В данном случае создаются 2 пула: один для contoso11.com и второй для fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="32f49-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="32f49-141">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="32f49-141">Step 1</span></span>

<span data-ttu-id="32f49-142">Перейдите tooan существующего шлюза приложения в hello портал Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32f49-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="32f49-143">Выберите **Пулы серверной части** и нажмите кнопку **Добавить**</span><span class="sxs-lookup"><span data-stu-id="32f49-143">Select **Backend pools** and click **Add**</span></span>

![Добавление пулов серверной части][7]

### <a name="step-2"></a><span data-ttu-id="32f49-145">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="32f49-145">Step 2</span></span>

<span data-ttu-id="32f49-146">Заполните сведения hello hello серверной части пула **pool1**, добавление hello IP-адресов или полных доменных имен для hello внутренних серверах и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="32f49-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![Параметры пула серверной части pool1][8]

### <a name="step-3"></a><span data-ttu-id="32f49-148">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="32f49-148">Step 3</span></span>

<span data-ttu-id="32f49-149">В колонке внутренние пулы hello щелкните **добавить** tooadd пул дополнительных серверной части **pool2**, добавление hello IP-адресов или полных доменных ИМЕН для hello внутренних серверах и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="32f49-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![Параметры пула серверной части pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="32f49-151">Создание прослушивателей для каждой серверной части</span><span class="sxs-lookup"><span data-stu-id="32f49-151">Create listeners for each back-end</span></span>

<span data-ttu-id="32f49-152">Шлюз приложений использует протокол HTTP 1.1 toohost заголовки узлов более одного веб-сайта на hello же общедоступный IP-адрес и порт.</span><span class="sxs-lookup"><span data-stu-id="32f49-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="32f49-153">создан в портале hello базовый прослушиватель Hello не содержит это свойство.</span><span class="sxs-lookup"><span data-stu-id="32f49-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="32f49-154">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="32f49-154">Step 1</span></span>

<span data-ttu-id="32f49-155">Нажмите кнопку **прослушиватели** hello существующего шлюза приложения и нажмите кнопку **многосайтовой** tooadd hello первого прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="32f49-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![Колонка обзора прослушивателей][1]

### <a name="step-2"></a><span data-ttu-id="32f49-157">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="32f49-157">Step 2</span></span>

<span data-ttu-id="32f49-158">Заполните сведения hello hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="32f49-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="32f49-159">В этом примере мы настраиваем оконечную точку SSL, поэтому создайте внешний порт.</span><span class="sxs-lookup"><span data-stu-id="32f49-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="32f49-160">Отправьте сертификат toobe hello PFX-файл, используемый для завершения запросов SSL.</span><span class="sxs-lookup"><span data-stu-id="32f49-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="32f49-161">Hello в этой колонке стандартный базовый прослушиватель toohello колонке сравнивается отличается только имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![Колонка свойств прослушивателя][2]

### <a name="step-3"></a><span data-ttu-id="32f49-163">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="32f49-163">Step 3</span></span>

<span data-ttu-id="32f49-164">Нажмите кнопку **многосайтовой** и создать другой прослушиватель, как описано в hello предыдущий шаг для hello второй узел.</span><span class="sxs-lookup"><span data-stu-id="32f49-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="32f49-165">Убедитесь в том toouse разные сертификаты для второй прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="32f49-166">Hello в этой колонке стандартный базовый прослушиватель toohello колонке сравнивается отличается только имя узла hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="32f49-167">Введите сведения о hello для прослушивателя hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="32f49-167">Fill out hello information for hello listener and click **OK**.</span></span>

![Колонка свойств прослушивателя][3]

> [!NOTE]
> <span data-ttu-id="32f49-169">Создание прослушивателей в Azure портал для шлюза приложения hello — длительные задачи, займет некоторое время toocreate hello двух прослушивателей в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="32f49-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="32f49-170">При прослушиватели завершения hello отображаться портале hello в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="32f49-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![Обзор прослушивателей][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="32f49-172">Создание правила toomap прослушиватели toobackend пулов</span><span class="sxs-lookup"><span data-stu-id="32f49-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="32f49-173">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="32f49-173">Step 1</span></span>

<span data-ttu-id="32f49-174">Перейдите tooan существующего шлюза приложения в hello портал Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32f49-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="32f49-175">Выберите **правила** и выберите существующее правило по умолчанию hello **правило 1** и нажмите кнопку **изменить**.</span><span class="sxs-lookup"><span data-stu-id="32f49-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="32f49-176">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="32f49-176">Step 2</span></span>

<span data-ttu-id="32f49-177">Заполните колонке правила hello в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="32f49-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="32f49-178">Выбор первого прослушивателя hello и первого пула и нажав кнопку **Сохранить** завершении выполнения.</span><span class="sxs-lookup"><span data-stu-id="32f49-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![Изменение существующего правила][6]

### <a name="step-3"></a><span data-ttu-id="32f49-180">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="32f49-180">Step 3</span></span>

<span data-ttu-id="32f49-181">Нажмите кнопку **основное правило** toocreate hello второе правило.</span><span class="sxs-lookup"><span data-stu-id="32f49-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="32f49-182">Заполните форму hello с hello второй прослушивателя и второй внутренний пул и нажмите кнопку **ОК** toosave.</span><span class="sxs-lookup"><span data-stu-id="32f49-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![Колонка добавления базового правила][10]

<span data-ttu-id="32f49-184">Этот сценарий завершения настройки шлюза существующие приложения с поддержкой нескольких сайтов через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="32f49-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32f49-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32f49-185">Next steps</span></span>

<span data-ttu-id="32f49-186">Узнайте, как tooprotect веб-сайты с [шлюз приложений - брандмауэр веб-приложения](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="32f49-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
