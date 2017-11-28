---
title: "aaaWork с существующими локальными прокси-серверами и Azure AD | Документы Microsoft"
description: "Рассматриваются как toowork с существующими локальными прокси-серверов."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="c595d-103">Работа с имеющимися локальными прокси-серверами</span><span class="sxs-lookup"><span data-stu-id="c595d-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="c595d-104">В этой статье объясняется, как tooconfigure toowork соединителей прокси приложения Azure Active Directory (Azure AD) с исходящий прокси-серверами.</span><span class="sxs-lookup"><span data-stu-id="c595d-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="c595d-105">Она предназначена для клиентов, использующих сетевые среды с имеющимися прокси.</span><span class="sxs-lookup"><span data-stu-id="c595d-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="c595d-106">Рассмотрим основные сценарии развертывания:</span><span class="sxs-lookup"><span data-stu-id="c595d-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="c595d-107">Настройте соединители toobypass вашей локальной исходящих прокси-серверов.</span><span class="sxs-lookup"><span data-stu-id="c595d-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="c595d-108">Настройте соединители toouse исходящего прокси-сервера tooaccess прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c595d-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="c595d-109">Дополнительные сведения о соединителях см. в статье [Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="c595d-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="c595d-110">Настройка прокси-сервера на исходящие hello</span><span class="sxs-lookup"><span data-stu-id="c595d-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="c595d-111">Если имеется исходящий прокси-сервер в вашей среде, необходимо используйте учетную запись с соответствующими разрешениями tooconfigure hello исходящего прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="c595d-112">Поскольку hello установщик запускается в контексте hello hello пользователя, который выполняет установку hello, проверьте конфигурацию hello с помощью Microsoft Edge или другой браузер Интернета.</span><span class="sxs-lookup"><span data-stu-id="c595d-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="c595d-113">параметры прокси-сервера tooconfigure hello в Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="c595d-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="c595d-114">Go слишком**параметры** > **Дополнительные параметры представления** > **откройте параметры прокси-сервера** > **ручной настройки прокси-сервера** .</span><span class="sxs-lookup"><span data-stu-id="c595d-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="c595d-115">Задать **использовать прокси-сервер** слишком**на**выберите hello **не используйте hello прокси-сервер для локальных адресов (интрасеть)** флажок, а затем tooreflect изменение hello адрес и порт ваш локальный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="c595d-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="c595d-116">Заполните параметры hello необходимые прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-116">Fill in hello necessary proxy settings.</span></span>

   ![Диалоговое окно для настройки прокси-сервера](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="c595d-118">Обход исходящих прокси-серверов</span><span class="sxs-lookup"><span data-stu-id="c595d-118">Bypass outbound proxies</span></span>

<span data-ttu-id="c595d-119">Соединители имеют базовые компоненты ОС, выполняющие исходящие запросы.</span><span class="sxs-lookup"><span data-stu-id="c595d-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="c595d-120">Эти компоненты автоматически предпринимает toolocate прокси-сервера в сети hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="c595d-121">Они используют автоматическое обнаружение прокси-сервера веб-(WPAD), если он включен в среде hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="c595d-122">компоненты операционной системы Hello попытку toolocate прокси-сервер, выполняющий поиск в DNS для wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="c595d-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="c595d-123">Если это разрешается в DNS, HTTP-запроса затем выполняется toohello IP-адрес для wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="c595d-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="c595d-124">Этот запрос становится hello сценарий настройки прокси-сервера в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="c595d-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="c595d-125">Соединитель Hello использует этот сценарий tooselect исходящий прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="c595d-126">Тем не менее, соединитель трафик может по-прежнему не проходит через, из-за дополнительных параметров настройки для hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="c595d-127">Можно настроить toobypass соединитель hello вашей tooensure прокси-сервера в локальной среде, она использует прямое подключение toohello Azure службы.</span><span class="sxs-lookup"><span data-stu-id="c595d-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="c595d-128">Это рекомендуемый подход (если сетевой политики разрешает для него), так как он означает, что один меньше toomaintain конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c595d-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="c595d-129">Использование toodisable исходящего прокси-сервера для соединителя hello, измените файл C:\Program Files\Microsoft AAD приложения прокси Connector\ApplicationProxyConnectorService.exe.config hello и добавьте hello *system.net* раздела показано в этом примере кода :</span><span class="sxs-lookup"><span data-stu-id="c595d-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="c595d-130">tooensure, средство обновления соединителя службы hello в обход прокси-сервера hello, внести аналогичные изменения toohello ApplicationProxyConnectorUpdaterService.exe.config файл, расположенный в средство обновления соединителя прокси приложения в AAD Files\Microsoft C:\Program.</span><span class="sxs-lookup"><span data-stu-id="c595d-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="c595d-131">Следует убедиться, что toomake копии hello исходные файлы, необходимые файлы .config toorevert toohello по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c595d-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="c595d-132">Использовать hello исходящий прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="c595d-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="c595d-133">Некоторые среды требуют все toogo исходящего трафика через исходящий прокси-сервер без исключений.</span><span class="sxs-lookup"><span data-stu-id="c595d-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="c595d-134">В результате обход прокси-сервера hello являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="c595d-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="c595d-135">Hello соединителя трафика toogo через прокси-сервер hello Исходящие, можно настроить, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="c595d-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Настройка соединителя toogo трафика через tooAzure исходящего прокси-сервера AD прокси приложения](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="c595d-137">В результате возникают только исходящий трафик, выделяется tooconfigure не требуется входящий доступ через межсетевой экран.</span><span class="sxs-lookup"><span data-stu-id="c595d-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="c595d-138">Шаг 1: Настройте соединитель hello и связанных служб toogo через hello исходящего прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="c595d-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="c595d-139">Как описано ранее, если включен в среде hello и надлежащим образом настраивается WPAD, соединитель hello автоматически обнаруживать hello toouse исходящего прокси-сервера сервера и попытка ее.</span><span class="sxs-lookup"><span data-stu-id="c595d-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="c595d-140">Тем не менее можно настроить явно toogo соединитель hello через исходящего прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="c595d-141">toodo таким образом, измените файл C:\Program Files\Microsoft AAD приложения прокси Connector\ApplicationProxyConnectorService.exe.config hello и добавьте hello *system.net* раздела показано в этом примере кода.</span><span class="sxs-lookup"><span data-stu-id="c595d-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="c595d-142">Изменение *proxyserver:8080* tooreflect ваш локальный прокси-сервер имя сервера или IP-адрес и hello порта, что он прослушивает.</span><span class="sxs-lookup"><span data-stu-id="c595d-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="c595d-143">Настройте прокси-сервер hello средство обновления соединителя службы toouse hello, делая аналогичные изменения toohello, находящемся в C:\Program Files\Microsoft AAD приложения прокси-сервера соединителя Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="c595d-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="c595d-144">Шаг 2: Настройка hello прокси tooallow трафик от соединителя hello и связанных служб tooflow через</span><span class="sxs-lookup"><span data-stu-id="c595d-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="c595d-145">Существует четыре tooconsider аспекты в hello исходящего прокси-сервера:</span><span class="sxs-lookup"><span data-stu-id="c595d-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="c595d-146">правила для исходящих подключений прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-146">Proxy outbound rules</span></span>
* <span data-ttu-id="c595d-147">проверка подлинности прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-147">Proxy authentication</span></span>
* <span data-ttu-id="c595d-148">порты прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-148">Proxy ports</span></span>
* <span data-ttu-id="c595d-149">проверка SSL.</span><span class="sxs-lookup"><span data-stu-id="c595d-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="c595d-150">правила для исходящих подключений прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-150">Proxy outbound rules</span></span>
<span data-ttu-id="c595d-151">Разрешить доступ toohello следующие конечные точки для доступа к службе соединителя:</span><span class="sxs-lookup"><span data-stu-id="c595d-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="c595d-152">*.msappproxy.net;</span><span class="sxs-lookup"><span data-stu-id="c595d-152">*.msappproxy.net</span></span>
* <span data-ttu-id="c595d-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="c595d-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="c595d-154">Для первоначальной регистрации разрешите доступ toohello следующие конечные точки:</span><span class="sxs-lookup"><span data-stu-id="c595d-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="c595d-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="c595d-155">login.windows.net</span></span>
* <span data-ttu-id="c595d-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="c595d-156">login.microsoftonline.com</span></span>

<span data-ttu-id="c595d-157">Если вы не сможете разрешить подключения по полному доменному ИМЕНИ и необходимые диапазоны IP-адресов toospecify используйте эти параметры:</span><span class="sxs-lookup"><span data-stu-id="c595d-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="c595d-158">Разрешите исходящий доступ соединитель hello tooall назначения.</span><span class="sxs-lookup"><span data-stu-id="c595d-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="c595d-159">Разрешить исходящий доступ соединитель hello слишком[диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="c595d-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="c595d-160">проблема Hello использования hello список диапазонов IP-адресов центра обработки данных Azure — еженедельно обновляется.</span><span class="sxs-lookup"><span data-stu-id="c595d-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="c595d-161">Необходимо tooput процесса в месте tooensure соответствующим образом обновлены правила доступа.</span><span class="sxs-lookup"><span data-stu-id="c595d-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="c595d-162">проверка подлинности прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-162">Proxy authentication</span></span>

<span data-ttu-id="c595d-163">Проверка подлинности прокси в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c595d-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="c595d-164">Мы рекомендуем — tooallow hello соединителя анонимный доступ toohello пунктам назначения в Интернете.</span><span class="sxs-lookup"><span data-stu-id="c595d-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="c595d-165">порты прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="c595d-165">Proxy ports</span></span>

<span data-ttu-id="c595d-166">Соединитель Hello делает исходящих соединений на основе протокола SSL с помощью метода CONNECT hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="c595d-167">Этот метод фактически устанавливает туннель через hello исходящего прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="c595d-168">Настройте hello прокси сервера tooallow туннелирование tooports 443 и 80.</span><span class="sxs-lookup"><span data-stu-id="c595d-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="c595d-169">При запуске служебной шины по протоколу HTTPS используется порт 443.</span><span class="sxs-lookup"><span data-stu-id="c595d-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="c595d-170">Тем не менее по умолчанию Service Bus пытается прямые подключения TCP и возвращается tooHTTPS только в том случае, если прямое подключение завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c595d-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="c595d-171">tooensure, Здравствуйте Service Bus, он также отправляется hello исходящий прокси-сервер, убедитесь, что для этого соединителя hello не может напрямую подключиться toohello службы Azure для порты 9350, 9352 и 5671.</span><span class="sxs-lookup"><span data-stu-id="c595d-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="c595d-172">проверка SSL.</span><span class="sxs-lookup"><span data-stu-id="c595d-172">SSL inspection</span></span>
<span data-ttu-id="c595d-173">Не используйте проверку SSL для трафика соединителя hello, так как это вызывает проблемы, для трафика соединителя hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="c595d-174">Устранение неполадок в работе соединителя через прокси-сервера и с подключением к службе</span><span class="sxs-lookup"><span data-stu-id="c595d-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="c595d-175">Теперь вы увидите все трафик через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="c595d-176">Если возникают проблемы, поможет hello следующие сведения об устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="c595d-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="c595d-177">Здравствуйте, лучшим способом tooidentify и устранения неполадок подключения соединитель проблемы является tootake сети записываться hello соединитель службы во время запуска службы соединителя hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="c595d-178">Это может оказаться непростой задачей, так что давайте рассмотрим советы по сбору и фильтрации данных трассировки сети.</span><span class="sxs-lookup"><span data-stu-id="c595d-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="c595d-179">Можно использовать средство по вашему выбору наблюдения за hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="c595d-180">В целях hello данной статьи мы использовали Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="c595d-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="c595d-181">Эту версию можно загрузить [здесь](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="c595d-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="c595d-182">Примеры Hello и фильтры, используемые в следующих разделах hello конкретных tooNetwork монитора, но принципы hello могут быть применен tooany средство анализа.</span><span class="sxs-lookup"><span data-stu-id="c595d-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="c595d-183">Выполнение записи с помощью сетевого монитора</span><span class="sxs-lookup"><span data-stu-id="c595d-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="c595d-184">toostart записи:</span><span class="sxs-lookup"><span data-stu-id="c595d-184">toostart a capture:</span></span>

1. <span data-ttu-id="c595d-185">Откройте сетевой монитор и щелкните **New Capture** (Новая запись).</span><span class="sxs-lookup"><span data-stu-id="c595d-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="c595d-186">Нажмите кнопку hello **запустить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c595d-186">Click hello **Start** button.</span></span>

   ![Окно сетевого монитора](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="c595d-188">После завершения записи нажмите кнопку hello **остановить** кнопку tooend его.</span><span class="sxs-lookup"><span data-stu-id="c595d-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="c595d-189">Сбор трафика соединителя</span><span class="sxs-lookup"><span data-stu-id="c595d-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="c595d-190">Изначальная Диагностика выполните hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c595d-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="c595d-191">Из services.msc остановите службу hello соединитель прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c595d-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="c595d-192">Начать запись сети hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-192">Start hello network capture.</span></span>
3. <span data-ttu-id="c595d-193">Запустите службу hello соединитель прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c595d-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="c595d-194">Остановка записи hello сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="c595d-194">Stop hello network capture.</span></span>

   ![Служба соединителя прокси приложения Azure AD в services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="c595d-196">Рассмотрим hello запросы от hello соединитель toohello прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="c595d-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="c595d-197">Теперь, когда у вас есть записи сетевого трафика, вы будете готовы toofilter его.</span><span class="sxs-lookup"><span data-stu-id="c595d-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="c595d-198">Hello ключа toolooking в трассировке hello понимания того, как записать toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="c595d-199">Один фильтр составляет (где 8080 — порт службы hello прокси-сервера):</span><span class="sxs-lookup"><span data-stu-id="c595d-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="c595d-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="c595d-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="c595d-201">Если указать этот фильтр в hello **фильтр отображения** и выберите **применить**, фильтрует hello захвачен трафика на основе фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="c595d-202">Hello выше отображаются лишь hello запросов и ответов HTTP из hello порт прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="c595d-203">Для запуска соединителя, где hello соединителя — toouse настроенный прокси-сервер hello фильтра будут показаны примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c595d-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Пример списка отфильтрованных запросов и ответов HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="c595d-205">Теперь специально Запрашиваемая hello ПОДКЛЮЧЕНИЕ запросов, показывающие связь с прокси-сервера hello.</span><span class="sxs-lookup"><span data-stu-id="c595d-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="c595d-206">В случае успеха вы получите ответ OK с HTTP-кодом 200.</span><span class="sxs-lookup"><span data-stu-id="c595d-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="c595d-207">Если другие коды ответа, например 407 или 502, hello прокси требование проверки подлинности или не позволяет hello трафика по другой причине.</span><span class="sxs-lookup"><span data-stu-id="c595d-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="c595d-208">На этом этапе следует обратиться в службу поддержки прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c595d-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="c595d-209">Выявление неудачных попыток подключения TCP</span><span class="sxs-lookup"><span data-stu-id="c595d-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="c595d-210">Hello другим распространенным сценарием, могут быть интересны является hello соединителя пытается tooconnect напрямую, когда происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="c595d-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="c595d-211">— Другой фильтр сетевой монитор, который помогает tooeasily идентификации проблемы:</span><span class="sxs-lookup"><span data-stu-id="c595d-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="c595d-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="c595d-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="c595d-213">Пакет SYN — первый пакет приветствия отправки tooestablish TCP-подключение.</span><span class="sxs-lookup"><span data-stu-id="c595d-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="c595d-214">Если этот пакет не возвращает ответ, hello SYN повторяется.</span><span class="sxs-lookup"><span data-stu-id="c595d-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="c595d-215">Можно использовать любой повторно SYN hello предшествующий toosee фильтра.</span><span class="sxs-lookup"><span data-stu-id="c595d-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="c595d-216">Затем можно проверить, соответствуют ли эти SYN tooany трафика соединителя.</span><span class="sxs-lookup"><span data-stu-id="c595d-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="c595d-217">Hello ниже приведен пример попытки неудачного подключения порт шины tooService 9352.</span><span class="sxs-lookup"><span data-stu-id="c595d-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Пример ответа для ошибки подключения](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="c595d-219">При появлении примерно hello предшествующий ответа соединителя hello пытается toocommunicate непосредственно с hello службы Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c595d-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="c595d-220">Если предполагается, что прямые подключения toomake toohello Azure для hello соединителя служб, этот ответ является четкое представление о том, что имеются проблемы с сетью или брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="c595d-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="c595d-221">Если toouse настроенный прокси-сервер, этот ответ может означать, что Service Bus пытается прямое подключение TCP перед переключением tooattempting соединение по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c595d-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="c595d-222">Анализ трассировки сети — не идеальное решение.</span><span class="sxs-lookup"><span data-stu-id="c595d-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="c595d-223">Но это может быть полезным средством tooget краткие сведения о том, что сети.</span><span class="sxs-lookup"><span data-stu-id="c595d-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="c595d-224">В случае продолжения toostruggle с проблемами подключения соединитель создайте билет с нашей группой поддержки.</span><span class="sxs-lookup"><span data-stu-id="c595d-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="c595d-225">Команда Hello может помочь устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="c595d-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="c595d-226">Сведения об устранении ошибок соединителя прокси приложения см. в [этой статье](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="c595d-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c595d-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c595d-227">Next steps</span></span>

[<span data-ttu-id="c595d-228">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="c595d-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="c595d-229">
[Как toosilently установку hello соединитель прокси приложения Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="c595d-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
