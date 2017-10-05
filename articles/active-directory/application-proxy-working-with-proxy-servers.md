---
title: "Работа с имеющимися локальными прокси-серверами в Azure AD | Документация Майкрософт"
description: "В этой статье описывается, как работать с существующими локальными прокси-серверами."
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="0dfd2-103">Работа с имеющимися локальными прокси-серверами</span><span class="sxs-lookup"><span data-stu-id="0dfd2-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="0dfd2-104">В этой статье описывается, как настроить соединители прокси приложения Azure Active Directory для работы с исходящими прокси-серверами.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="0dfd2-105">Она предназначена для клиентов, использующих сетевые среды с имеющимися прокси.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="0dfd2-106">Рассмотрим основные сценарии развертывания:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="0dfd2-107">Настройка соединителей для обхода локальных исходящих прокси-серверов.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="0dfd2-108">Настройка соединителей для доступа к прокси приложения Azure AD через исходящий прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="0dfd2-109">Дополнительные сведения о соединителях см. в статье [Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="0dfd2-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="0dfd2-110">Настройка исходящего прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="0dfd2-110">Configure the outbound proxy</span></span>

<span data-ttu-id="0dfd2-111">Если в вашей среде имеется исходящий прокси-сервер, используйте учетную запись с соответствующими разрешениями для настройки исходящих прокси.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="0dfd2-112">Поскольку программа установки выполняется в контексте пользователя, который выполняет установку, настройки можно проверить с помощью Microsoft Edge или любого другого браузера.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="0dfd2-113">Настройка параметров прокси с помощью Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="0dfd2-114">Последовательно выберите пункты **Параметры** > **Дополнительные параметры** > **Открыть параметры прокси-сервера** > **Настройка прокси вручную**.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="0dfd2-115">**Включите** параметр **Использовать прокси-сервер**, установите флажок **Не использовать прокси-сервер для локальных (внутрисетевых) адресов**, а затем укажите адрес и порт локального прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="0dfd2-116">Заполните необходимые параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-116">Fill in the necessary proxy settings.</span></span>

   ![Диалоговое окно для настройки прокси-сервера](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="0dfd2-118">Обход исходящих прокси-серверов</span><span class="sxs-lookup"><span data-stu-id="0dfd2-118">Bypass outbound proxies</span></span>

<span data-ttu-id="0dfd2-119">Соединители имеют базовые компоненты ОС, выполняющие исходящие запросы.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="0dfd2-120">Эти компоненты автоматически пытаются найти прокси-сервер в сети.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="0dfd2-121">Для этого применяется протокол автоматической настройки прокси, если он поддерживается в сети.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="0dfd2-122">Компоненты ОС для поиска прокси-сервера выполняют поиск в DNS для доменного имени wpad.[доменный_суффикс].</span><span class="sxs-lookup"><span data-stu-id="0dfd2-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="0dfd2-123">Если DNS возвращает IP-адрес для этого имени, выполняется HTTP-запрос на этот адрес для получения файла wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="0dfd2-124">Этот запрос возвращает скрипт конфигурации прокси-сервера для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="0dfd2-125">Соединитель использует этот скрипт, чтобы выбрать исходящий прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="0dfd2-126">Однако прокси-сервер может не принимать трафик соединителя, поскольку для этого требуется настройка дополнительных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="0dfd2-127">Можно настроить соединитель, чтобы он игнорировал локальный прокси-сервер и подключался к службам Azure напрямую.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="0dfd2-128">Мы рекомендуем использовать именно этот подход (если допускает политика сети), так как он позволяет сократить количество конфигураций.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="0dfd2-129">Чтобы отключить в соединителе использование исходящего прокси-сервера, измените файл C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config. Добавьте в него раздел *system.net* с приведенным далее текстом:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="0dfd2-130">Чтобы служба обновления соединителя также обходила прокси-сервер, измените аналогичным образом и файл ApplicationProxyConnectorUpdaterService.exe.config, расположенный в каталоге C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="0dfd2-131">Обязательно сделайте копии исходных файлов на случай, если потребуется восстановить конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="0dfd2-132">Использование исходящего прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="0dfd2-132">Use the outbound proxy server</span></span>

<span data-ttu-id="0dfd2-133">В некоторых средах весь исходящий трафик без исключений должен проходить через исходящий прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="0dfd2-134">В результате этого невозможно будет выполнить обход прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="0dfd2-135">Вы можете настроить передачу трафика соединителя через исходящий прокси-сервер, как показано на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Использование исходящего прокси-сервера для передачи трафика от соединителя к прокси приложения Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="0dfd2-137">Поскольку соединитель использует только исходящий трафик, нет необходимости пропускать входящий трафик через брандмауэры.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="0dfd2-138">Шаг 1. Настройка использования исходящего прокси-сервера для соединителя и службы средства обновления</span><span class="sxs-lookup"><span data-stu-id="0dfd2-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="0dfd2-139">Как мы уже объясняли выше, соединитель автоматически обнаружит исходящий прокси-сервер и попытается его использовать, если в среде поддерживается протокол автоматической настройки прокси.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="0dfd2-140">Тем не менее можно явным образом настроить использование исходящего прокси-сервера для соединителя.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="0dfd2-141">Для этого измените файл C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config и добавьте раздел *system.net*, поместив в него следующий образец кода.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="0dfd2-142">Вместо *proxyserver:8080* укажите имя или IP-адрес локального прокси-сервера и номер порта для доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="0dfd2-143">Затем настройте службу обновления соединителя, чтобы она использовала тот же прокси-сервер, изменив аналогичным образом файл, расположенный по пути C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="0dfd2-144">Шаг 2. Настройка прокси-сервера для передачи трафика соединителя и связанных с ним служб</span><span class="sxs-lookup"><span data-stu-id="0dfd2-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="0dfd2-145">В настройках прокси-сервера нужно учесть 4 аспекта:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="0dfd2-146">правила для исходящих подключений прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-146">Proxy outbound rules</span></span>
* <span data-ttu-id="0dfd2-147">проверка подлинности прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-147">Proxy authentication</span></span>
* <span data-ttu-id="0dfd2-148">порты прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-148">Proxy ports</span></span>
* <span data-ttu-id="0dfd2-149">проверка SSL.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="0dfd2-150">правила для исходящих подключений прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-150">Proxy outbound rules</span></span>
<span data-ttu-id="0dfd2-151">Разрешите доступ к следующих конечным точкам, чтобы получить доступ к службе соединителя:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="0dfd2-152">*.msappproxy.net;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-152">*.msappproxy.net</span></span>
* <span data-ttu-id="0dfd2-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="0dfd2-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="0dfd2-154">Для первоначальной регистрации нужно разрешить доступ к следующим конечным точкам:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="0dfd2-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="0dfd2-155">login.windows.net</span></span>
* <span data-ttu-id="0dfd2-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="0dfd2-156">login.microsoftonline.com</span></span>

<span data-ttu-id="0dfd2-157">Невозможно разрешить подключения по полному доменному имени. Вместо этого укажите диапазоны IP-адресов. Используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="0dfd2-158">разрешите соединителю исходящий доступ к любым адресам назначения;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="0dfd2-159">разрешите соединителю исходящий доступ к [IP-адресам центров обработки данных Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="0dfd2-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="0dfd2-160">Если вы предпочитаете использовать диапазоны IP-адресов центров обработки данных Azure, вас ждет одна сложность — эти списки обновляются еженедельно.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="0dfd2-161">Необходимо организовать процесс соответствующего обновления правил доступа.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="0dfd2-162">проверка подлинности прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-162">Proxy authentication</span></span>

<span data-ttu-id="0dfd2-163">Проверка подлинности прокси в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="0dfd2-164">Сейчас мы рекомендуем разрешить соединителю получать анонимный доступ к определенному сайту Интернета.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="0dfd2-165">порты прокси-сервера;</span><span class="sxs-lookup"><span data-stu-id="0dfd2-165">Proxy ports</span></span>

<span data-ttu-id="0dfd2-166">Соединитель устанавливает исходящие SSL-подключения, используя метод CONNECT.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="0dfd2-167">По сути он создает туннель через исходящий прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="0dfd2-168">В настройках прокси-сервера разрешите туннелирование к портам 443 и 80.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="0dfd2-169">При запуске служебной шины по протоколу HTTPS используется порт 443.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="0dfd2-170">По умолчанию служебная шина пытается использовать прямые TCP-подключения, а протокол HTTPS применяет только при невозможности прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="0dfd2-171">Чтобы проверить, отправляется ли трафик служебной шины через исходящий прокси-сервер, убедитесь, что соединитель не может напрямую подключиться к службам Azure по портам 9350, 9352 и 5671.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="0dfd2-172">проверка SSL.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-172">SSL inspection</span></span>
<span data-ttu-id="0dfd2-173">Для трафика соединителя не стоит использовать проверку SSL, так как это вызывает проблемы.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="0dfd2-174">Устранение неполадок в работе соединителя через прокси-сервера и с подключением к службе</span><span class="sxs-lookup"><span data-stu-id="0dfd2-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="0dfd2-175">Теперь весь трафик должен проходить через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="0dfd2-176">Если вы столкнетесь с проблемами, попробуйте применить следующие сведения об устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="0dfd2-177">Для определения и устранения проблем с подключением соединителя мы рекомендуем выполнить запись сетевых данных для службы соединителя во время ее запуска.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="0dfd2-178">Это может оказаться непростой задачей, так что давайте рассмотрим советы по сбору и фильтрации данных трассировки сети.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="0dfd2-179">Вы можете использовать выбранное средство мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="0dfd2-180">Для целей этой статьи мы использовали Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="0dfd2-181">Эту версию можно загрузить [здесь](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="0dfd2-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="0dfd2-182">Примеры и фильтры, которые мы используем ниже, относятся именно к сетевому монитору, но те же принципы можно применить к любому средству анализа.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="0dfd2-183">Выполнение записи с помощью сетевого монитора</span><span class="sxs-lookup"><span data-stu-id="0dfd2-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="0dfd2-184">Для начала записи:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-184">To start a capture:</span></span>

1. <span data-ttu-id="0dfd2-185">Откройте сетевой монитор и щелкните **New Capture** (Новая запись).</span><span class="sxs-lookup"><span data-stu-id="0dfd2-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="0dfd2-186">Нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-186">Click the **Start** button.</span></span>

   ![Окно сетевого монитора](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="0dfd2-188">Когда вы закончите запись данных, нажмите кнопку **Стоп**, чтобы завершить процесс.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="0dfd2-189">Сбор трафика соединителя</span><span class="sxs-lookup"><span data-stu-id="0dfd2-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="0dfd2-190">Для первоначального устранения неполадок сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="0dfd2-191">Из оснастки services.msc остановите службу соединителя прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="0dfd2-192">Запустите запись сетевых данных.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-192">Start the network capture.</span></span>
3. <span data-ttu-id="0dfd2-193">Запустите службу соединителя прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="0dfd2-194">Остановите запись сетевых данных.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-194">Stop the network capture.</span></span>

   ![Служба соединителя прокси приложения Azure AD в services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="0dfd2-196">Просмотр запросов от соединителя к прокси-серверу</span><span class="sxs-lookup"><span data-stu-id="0dfd2-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="0dfd2-197">Итак, вы собрали сетевые данные и теперь можете отфильтровать их.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="0dfd2-198">Основным моментом в трассировке является умение фильтровать собранные данные.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="0dfd2-199">Например, можно использовать такой фильтр (где 8080 — это порт службы прокси-сервера):</span><span class="sxs-lookup"><span data-stu-id="0dfd2-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="0dfd2-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="0dfd2-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="0dfd2-201">Если вы введете этот фильтр в окно **Фильтр отображения** и щелкнете **Применить**, собранный трафик отфильтруется по этому фильтру.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="0dfd2-202">Указанный выше фильтр отбирает только HTTP-запросы на порт прокси-сервера и его ответы.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="0dfd2-203">Для запуска соединителя, настроенного для использования прокси-сервера, этот фильтр отобразит примерно такие результаты:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Пример списка отфильтрованных запросов и ответов HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="0dfd2-205">Теперь нужно найти запросы CONNECT, которые демонстрируют взаимодействие с прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="0dfd2-206">В случае успеха вы получите ответ OK с HTTP-кодом 200.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="0dfd2-207">Если отобразятся другие коды ответов, например 407 или 502, это означает, что прокси-сервер требует проверки подлинности или не разрешает передачу трафика по другой причине.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="0dfd2-208">На этом этапе следует обратиться в службу поддержки прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="0dfd2-209">Выявление неудачных попыток подключения TCP</span><span class="sxs-lookup"><span data-stu-id="0dfd2-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="0dfd2-210">Вас может заинтересовать еще один распространенный сценарий: соединитель пытается подключиться напрямую, но не может.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="0dfd2-211">Ниже представлен пример фильтра сетевого монитора, который позволяет легко выявить такую проблему.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="0dfd2-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="0dfd2-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="0dfd2-213">Пакет SYN — это первый пакет, отправленный для установления подключения TCP.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="0dfd2-214">Если ответ на этот пакет не возвращается, пакет SYN отправляется еще раз.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="0dfd2-215">Для поиска повторных пакетов SYN можно использовать предыдущий фильтр.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="0dfd2-216">После этого можно проверить, соответствуют ли эти пакеты SYN трафику соединителя.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="0dfd2-217">В следующем примере показана ошибка подключения к порту 9352 служебной шины:</span><span class="sxs-lookup"><span data-stu-id="0dfd2-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Пример ответа для ошибки подключения](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="0dfd2-219">Если вы видите ответ, аналогичный указанному выше, значит соединитель пытается напрямую взаимодействовать со службой служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="0dfd2-220">Если соединитель действительно должен подключаться к службам Azure напрямую, логично предположить проблему в сети или в брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="0dfd2-221">Если же вы используете подключение через прокси-сервер, такой ответ может означать, что служебная шина пытается применить прямое подключение TCP, прежде чем использовать подключение по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="0dfd2-222">Анализ трассировки сети — не идеальное решение.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="0dfd2-223">Но он может быть ценным средством для быстрого получения сведений о проблемах с сетью.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="0dfd2-224">Если проблемы с подключением соединителя не удалось устранить, отправьте запрос в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="0dfd2-225">Мы поможем вам с устранением неполадок.</span><span class="sxs-lookup"><span data-stu-id="0dfd2-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="0dfd2-226">Сведения об устранении ошибок соединителя прокси приложения см. в [этой статье](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="0dfd2-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dfd2-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0dfd2-227">Next steps</span></span>

[<span data-ttu-id="0dfd2-228">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dfd2-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="0dfd2-229">
[Автоматическая установка соединителя прокси приложения Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="0dfd2-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
