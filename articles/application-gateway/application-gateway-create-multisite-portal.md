---
title: "Размещение нескольких сайтов с помощью шлюза приложений Azure | Документация Майкрософт"
description: "Эта страница содержит инструкции по настройке с помощью портала Azure существующего шлюза приложений Azure для размещения нескольких веб-приложений в одном шлюзе."
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
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="756dc-103">Настройка шлюза приложений для размещения нескольких веб-приложений</span><span class="sxs-lookup"><span data-stu-id="756dc-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="756dc-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="756dc-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="756dc-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="756dc-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="756dc-106">Размещение нескольких сайтов позволяет развернуть в одном шлюзе приложений не одно, а несколько веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="756dc-107">Чтобы определить, какой прослушиватель должен принимать трафик, шлюз приложений проверяет наличие заголовка узла во входящем HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="756dc-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="756dc-108">Затем прослушиватель направляет трафик в соответствующий внутренний пул согласно определениям правил шлюза.</span><span class="sxs-lookup"><span data-stu-id="756dc-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="756dc-109">В веб-приложениях с поддержкой протокола SSL шлюз приложений использует расширение SNI (указание имени сервера) для выбора соответствующего прослушивателя веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="756dc-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="756dc-110">Как правило, размещение нескольких сайтов используется для балансировки нагрузки запросов к разным веб-доменам между различными внутренними пулами серверов.</span><span class="sxs-lookup"><span data-stu-id="756dc-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="756dc-111">Подобным образом в одном шлюзе приложений можно разместить несколько поддоменов одного корневого домена.</span><span class="sxs-lookup"><span data-stu-id="756dc-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="756dc-112">Сценарий</span><span class="sxs-lookup"><span data-stu-id="756dc-112">Scenario</span></span>

<span data-ttu-id="756dc-113">В следующем примере шлюз приложений обслуживает трафик сайтов contoso.com и fabrikam.com с помощью двух внутренних пулов серверов: contoso и fabrikam.</span><span class="sxs-lookup"><span data-stu-id="756dc-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="756dc-114">Аналогичную конфигурацию можно использовать для размещения таких поддоменов, как app.contoso.com и blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="756dc-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![сценарий с несколькими сайтами][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="756dc-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="756dc-116">Before you begin</span></span>

<span data-ttu-id="756dc-117">Этот сценарий добавляет поддержку нескольких сайтов для существующего шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="756dc-118">Для выполнения этого сценария потребуется шлюз приложений, который можно настроить.</span><span class="sxs-lookup"><span data-stu-id="756dc-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="756dc-119">Изучите статью [Создание шлюза приложений с помощью портала](application-gateway-create-gateway-portal.md), чтобы узнать о создании базового шлюза приложений на портале.</span><span class="sxs-lookup"><span data-stu-id="756dc-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="756dc-120">Выполните следующие действия, чтобы обновить конфигурацию шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="756dc-121">Создание пулов серверной части для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="756dc-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="756dc-122">Создание прослушивателя для каждого сайта, который поддерживает шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="756dc-123">Создание правил для сопоставления каждого прослушивателя с соответствующей серверной частью.</span><span class="sxs-lookup"><span data-stu-id="756dc-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="756dc-124">Требования</span><span class="sxs-lookup"><span data-stu-id="756dc-124">Requirements</span></span>

* <span data-ttu-id="756dc-125">**Внутренний пул серверов**. Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="756dc-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="756dc-126">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные или виртуальные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="756dc-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="756dc-127">Можно также использовать полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="756dc-127">FQDN can also be used.</span></span>
* <span data-ttu-id="756dc-128">**Параметры внутреннего пула серверов**. Каждый пул имеет такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="756dc-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="756dc-129">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="756dc-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="756dc-130">**Интерфейсный порт**. Общедоступный порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="756dc-131">Трафик поступает на этот порт, а затем перенаправляется на один из тыловых серверов.</span><span class="sxs-lookup"><span data-stu-id="756dc-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="756dc-132">**Прослушиватель**. У прослушивателя есть интерфейсный порт, протокол (Http или Https — с учетом регистра) и имя SSL-сертификата (в случае настройки разгрузки SSL).</span><span class="sxs-lookup"><span data-stu-id="756dc-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="756dc-133">Для шлюзов приложений с поддержкой нескольких сайтов также добавляются имя узла и индикаторы SNI.</span><span class="sxs-lookup"><span data-stu-id="756dc-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="756dc-134">**Правило**. Правило связывает прослушиватель и внутренний пул серверов, а также определяет, в какой внутренний пул серверов следует направлять трафик, поступающий на определенный прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="756dc-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="756dc-135">Правила обрабатываются в том порядке, в котором они указаны, а трафик направляется через первое подходящее правило независимо от точности.</span><span class="sxs-lookup"><span data-stu-id="756dc-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="756dc-136">Например, если для одного порта имеется правило с базовым прослушивателем и правило с многосайтовым прослушивателем, для обеспечения правильной работы правило с многосайтовым прослушивателем должно быть указано перед правилом с базовым прослушивателем.</span><span class="sxs-lookup"><span data-stu-id="756dc-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="756dc-137">**Сертификаты:** каждый прослушиватель должен иметь уникальный сертификат. В этом примере мы создаем 2 прослушивателя для поддержки нескольких сайтов.</span><span class="sxs-lookup"><span data-stu-id="756dc-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="756dc-138">Для них нужно создать два сертификата PFX и пароли для них.</span><span class="sxs-lookup"><span data-stu-id="756dc-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="756dc-139">Создание пулов серверной части для каждого узла</span><span class="sxs-lookup"><span data-stu-id="756dc-139">Create back-end pools for each site</span></span>

<span data-ttu-id="756dc-140">Требуется отдельный внутренний пул для каждого сайта, который поддерживает шлюз приложений. В данном случае создаются 2 пула: один для contoso11.com и второй для fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="756dc-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="756dc-141">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="756dc-141">Step 1</span></span>

<span data-ttu-id="756dc-142">На портале Azure (https://portal.azure.com) перейдите к существующему шлюзу приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="756dc-143">Выберите **Пулы серверной части** и нажмите кнопку **Добавить**</span><span class="sxs-lookup"><span data-stu-id="756dc-143">Select **Backend pools** and click **Add**</span></span>

![Добавление пулов серверной части][7]

### <a name="step-2"></a><span data-ttu-id="756dc-145">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="756dc-145">Step 2</span></span>

<span data-ttu-id="756dc-146">Заполните сведения для пула серверной части **pool1**, добавив IP-адреса или полные доменные имена серверов, и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="756dc-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![Параметры пула серверной части pool1][8]

### <a name="step-3"></a><span data-ttu-id="756dc-148">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="756dc-148">Step 3</span></span>

<span data-ttu-id="756dc-149">В колонке пулов серверной части нажмите кнопку **Добавить**, чтобы создать дополнительный пул серверной части **pool2**. Внесите для него IP-адреса или полные доменные имена серверов и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="756dc-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![Параметры пула серверной части pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="756dc-151">Создание прослушивателей для каждой серверной части</span><span class="sxs-lookup"><span data-stu-id="756dc-151">Create listeners for each back-end</span></span>

<span data-ttu-id="756dc-152">Шлюз приложений использует заголовки узлов HTTP 1.1 для размещения нескольких веб-сайтов на одном общедоступном IP-адресе и порте.</span><span class="sxs-lookup"><span data-stu-id="756dc-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="756dc-153">Базовые прослушиватели, создаваемые на портале, не содержат этого свойства.</span><span class="sxs-lookup"><span data-stu-id="756dc-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="756dc-154">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="756dc-154">Step 1</span></span>

<span data-ttu-id="756dc-155">Щелкните **Прослушиватели** для существующего шлюза приложений, затем выберите **Многосайтовый**, чтобы добавить первый прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="756dc-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![Колонка обзора прослушивателей][1]

### <a name="step-2"></a><span data-ttu-id="756dc-157">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="756dc-157">Step 2</span></span>

<span data-ttu-id="756dc-158">Заполните сведения о прослушивателе.</span><span class="sxs-lookup"><span data-stu-id="756dc-158">Fill out the information for the listener.</span></span> <span data-ttu-id="756dc-159">В этом примере мы настраиваем оконечную точку SSL, поэтому создайте внешний порт.</span><span class="sxs-lookup"><span data-stu-id="756dc-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="756dc-160">Отправьте PFX-файл сертификата, который будет использоваться для оконечной точки SSL.</span><span class="sxs-lookup"><span data-stu-id="756dc-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="756dc-161">Эта колонка отличается от колонки стандартного базового прослушивателя только наличием имени узла.</span><span class="sxs-lookup"><span data-stu-id="756dc-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![Колонка свойств прослушивателя][2]

### <a name="step-3"></a><span data-ttu-id="756dc-163">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="756dc-163">Step 3</span></span>

<span data-ttu-id="756dc-164">Щелкните **Многосайтовый** и создайте второй прослушиватель для второго сайта, как описано в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="756dc-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="756dc-165">Для второго прослушивателя необходимо использовать другой сертификат.</span><span class="sxs-lookup"><span data-stu-id="756dc-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="756dc-166">Эта колонка отличается от колонки стандартного базового прослушивателя только наличием имени узла.</span><span class="sxs-lookup"><span data-stu-id="756dc-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="756dc-167">Введите сведения о прослушивателе и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="756dc-167">Fill out the information for the listener and click **OK**.</span></span>

![Колонка свойств прослушивателя][3]

> [!NOTE]
> <span data-ttu-id="756dc-169">Создание на портале Azure прослушивателей для шлюза приложений — довольно длительный процесс, и создание двух прослушивателей в нашем примере может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="756dc-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="756dc-170">По завершении процесса прослушиватели будут отображены на портале, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="756dc-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![Обзор прослушивателей][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="756dc-172">Создание правил для сопоставления прослушивателей с пулами серверной части</span><span class="sxs-lookup"><span data-stu-id="756dc-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="756dc-173">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="756dc-173">Step 1</span></span>

<span data-ttu-id="756dc-174">На портале Azure (https://portal.azure.com) перейдите к существующему шлюзу приложений.</span><span class="sxs-lookup"><span data-stu-id="756dc-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="756dc-175">Выберите **Правила**, затем выберите существующее правило по умолчанию **rule1** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="756dc-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="756dc-176">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="756dc-176">Step 2</span></span>

<span data-ttu-id="756dc-177">Заполните колонку правил, как показано на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="756dc-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="756dc-178">Для этого выберите первый прослушиватель и первый пул, затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="756dc-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![Изменение существующего правила][6]

### <a name="step-3"></a><span data-ttu-id="756dc-180">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="756dc-180">Step 3</span></span>

<span data-ttu-id="756dc-181">Щелкните **Basic rule** (Базовое правило), чтобы создать второе правило.</span><span class="sxs-lookup"><span data-stu-id="756dc-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="756dc-182">Заполните форму для второго прослушивателя и второго пула серверной части, затем щелкните **ОК** для сохранения.</span><span class="sxs-lookup"><span data-stu-id="756dc-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![Колонка добавления базового правила][10]

<span data-ttu-id="756dc-184">На этом завершается настройка существующего шлюза приложений с поддержкой нескольких сайтов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="756dc-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="756dc-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="756dc-185">Next steps</span></span>

<span data-ttu-id="756dc-186">Узнайте, как защитить веб-сайты с помощью [брандмауэра веб-приложения шлюза приложений](application-gateway-webapplicationfirewall-overview.md).</span><span class="sxs-lookup"><span data-stu-id="756dc-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
