---
title: "aaaOn локальный шлюз данных | Документы Microsoft"
description: "Локальный шлюз необходим в том случае, если сервер служб Analysis Services в Azure будут подключаться tooon локальные источники данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="121de-103">Соединение tooon локальные источники данных с помощью Azure на локальный шлюз данных</span><span class="sxs-lookup"><span data-stu-id="121de-103">Connecting tooon-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="121de-104">Hello локального шлюза данных выступает в качестве моста, обеспечивая безопасную передачу данных между локальным источникам данных и серверов в облаке hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="121de-104">hello on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in hello cloud.</span></span> <span data-ttu-id="121de-105">В дополнение tooworking с несколькими серверами служб Azure Analysis Services в hello же регионе, hello последнюю версию шлюза hello также работает с логику приложения Azure, Power BI, приложения Power и Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="121de-105">In addition tooworking with multiple Azure Analysis Services servers in hello same region, hello latest version of hello gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="121de-106">Можно связать несколько служб в hello совпадают с одного шлюза.</span><span class="sxs-lookup"><span data-stu-id="121de-106">You can associate multiple services in hello same region with a single gateway.</span></span> 

 <span data-ttu-id="121de-107">Azure Analysis Services требуется ресурс шлюза в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="121de-107">Azure Analysis Services requires a gateway resource in hello same region.</span></span> <span data-ttu-id="121de-108">Например при наличии серверов служб Analysis Services Azure в регионе Восток США 2 hello необходимо ресурса шлюза в регионе Восток США 2 hello.</span><span class="sxs-lookup"><span data-stu-id="121de-108">For example, if you have Azure Analysis Services servers in hello East US 2 region, you need a gateway resource in hello East US 2 region.</span></span> <span data-ttu-id="121de-109">Несколько серверов в восточная часть США 2 можно использовать hello одного шлюза.</span><span class="sxs-lookup"><span data-stu-id="121de-109">Multiple servers in East US 2 can use hello same gateway.</span></span>

<span data-ttu-id="121de-110">Начало установки с hello шлюза hello первый раз процесс состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="121de-110">Getting setup with hello gateway hello first time is a four-part process:</span></span>

- <span data-ttu-id="121de-111">**Скачивание и запуск программы установки.** На этом шаге устанавливается служба шлюза на компьютер организации.</span><span class="sxs-lookup"><span data-stu-id="121de-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="121de-112">**Зарегистрируйте свой шлюз** — на этом шаге укажите имя и восстановления ключа для шлюза и выберите регион, регистрация шлюза в облачной службе шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="121de-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with hello Gateway Cloud Service.</span></span>

- <span data-ttu-id="121de-113">**Создание ресурса шлюза в Azure.** На этом шаге необходимо создать ресурс шлюза в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="121de-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="121de-114">**Подключение ресурса серверы шлюза tooyour** -после ресурсов шлюза в подписке, можно начать подключение к tooit серверов.</span><span class="sxs-lookup"><span data-stu-id="121de-114">**Connect your servers tooyour gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers tooit.</span></span>

<span data-ttu-id="121de-115">При наличии шлюза ресурс, настроенный для вашей подписки, можно подключить несколько серверов и других служб tooit.</span><span class="sxs-lookup"><span data-stu-id="121de-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services tooit.</span></span> <span data-ttu-id="121de-116">Только требуется tooinstall другой шлюз и создавать шлюза дополнительных ресурсов при наличии серверов или других служб в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="121de-116">You only need tooinstall a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="121de-117">tooget работу прямо сейчас. в разделе [установить и настроить локальный шлюз данных](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="121de-117">tooget started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="121de-118"><a name="how-it-works"> </a>Принцип работы</span><span class="sxs-lookup"><span data-stu-id="121de-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="121de-119">Hello шлюза, установить на компьютере в организации выполняется как служба Windows, **локального шлюза данных**.</span><span class="sxs-lookup"><span data-stu-id="121de-119">hello gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="121de-120">Это локальная служба зарегистрирована hello облачной службе шлюза через Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="121de-120">This local service is registered with hello Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="121de-121">Затем создается ресурс шлюза в службе Gateway Cloud для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="121de-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="121de-122">В Azure со службами Analysis Services серверов, затем подключен tooyour ресурса шлюза.</span><span class="sxs-lookup"><span data-stu-id="121de-122">Your Azure Analysis Services servers are then connected tooyour gateway resource.</span></span> <span data-ttu-id="121de-123">При модели на ваш сервер необходимость tooconnect tooyour локальных источников данных для запросов и обработки, запросов и данных потока перебирает hello шлюза ресурса, Azure Service Bus hello служба шлюза локальных данных и источников данных.</span><span class="sxs-lookup"><span data-stu-id="121de-123">When models on your server need tooconnect tooyour on-premises data sources for queries or processing, a query and data flow traverses hello gateway resource, Azure Service Bus, hello local on-premises data gateway service, and your data sources.</span></span> 

![Принцип работы](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="121de-125">Запросы и поток данных</span><span class="sxs-lookup"><span data-stu-id="121de-125">Queries and data flow:</span></span>

1. <span data-ttu-id="121de-126">Запрос создается путем hello облачной службы с hello зашифрованные учетные данные для источника данных в локальной среде hello.</span><span class="sxs-lookup"><span data-stu-id="121de-126">A query is created by hello cloud service with hello encrypted credentials for hello on-premises data source.</span></span> <span data-ttu-id="121de-127">Затем он отправил tooa очереди шлюза tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="121de-127">It's then sent tooa queue for hello gateway tooprocess.</span></span>
2. <span data-ttu-id="121de-128">облачной службе шлюза Hello анализирует запрос hello и помещает hello запроса toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="121de-128">hello gateway cloud service analyzes hello query and pushes hello request toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="121de-129">Hello локальный шлюз данных опрашивает hello Azure Service Bus для ожидающих запросов.</span><span class="sxs-lookup"><span data-stu-id="121de-129">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="121de-130">Hello шлюз получает запрос hello, расшифровывает учетные данные hello и соединяет источники данных toohello с этими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="121de-130">hello gateway gets hello query, decrypts hello credentials, and connects toohello data sources with those credentials.</span></span>
5. <span data-ttu-id="121de-131">шлюз Hello отправляет источник данных toohello hello запросов для выполнения.</span><span class="sxs-lookup"><span data-stu-id="121de-131">hello gateway sends hello query toohello data source for execution.</span></span>
6. <span data-ttu-id="121de-132">Hello результаты отправляются из источника данных hello, шлюз toohello назад, а затем на облачную службу hello и сервера.</span><span class="sxs-lookup"><span data-stu-id="121de-132">hello results are sent from hello data source, back toohello gateway, and then onto hello cloud service and your server.</span></span>

## <span data-ttu-id="121de-133"><a name="windows-service-account"> </a>Учетная запись службы Windows</span><span class="sxs-lookup"><span data-stu-id="121de-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="121de-134">Hello локального шлюза данных является настроенным toouse *NT SERVICE\PBIEgwService* для учетных данных входа для службы Windows hello.</span><span class="sxs-lookup"><span data-stu-id="121de-134">hello on-premises data gateway is configured toouse *NT SERVICE\PBIEgwService* for hello Windows service logon credential.</span></span> <span data-ttu-id="121de-135">По умолчанию она содержит hello правого входа как службы; в контексте hello hello компьютера, на котором вы устанавливаете hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="121de-135">By default, it has hello right of Logon as a service; in hello context of hello machine that you are installing hello gateway on.</span></span> <span data-ttu-id="121de-136">Эти учетные данные не hello, же учетная запись, используемая tooconnect tooon локальные источники данных или учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="121de-136">This credential is not hello same account used tooconnect tooon-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="121de-137">При возникновении проблем с прокси-сервера из-за tooauthentication, вы можете toochange hello Windows или управляемые службы учетной записи пользователя домена tooa учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="121de-137">If you encounter issues with your proxy server due tooauthentication, you may want toochange hello Windows service account tooa domain user or managed service account.</span></span>

## <span data-ttu-id="121de-138"><a name="ports"> </a>Порты</span><span class="sxs-lookup"><span data-stu-id="121de-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="121de-139">Hello шлюз создает исходящее подключение tooAzure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="121de-139">hello gateway creates an outbound connection tooAzure Service Bus.</span></span> <span data-ttu-id="121de-140">Он обменивается данными через исходящие порты: TCP 443 (по умолчанию), а также 5671, 5672 и 9350–9354.</span><span class="sxs-lookup"><span data-stu-id="121de-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="121de-141">Hello шлюзу не требуются входящие порты.</span><span class="sxs-lookup"><span data-stu-id="121de-141">hello gateway does not require inbound ports.</span></span>

<span data-ttu-id="121de-142">Мы рекомендуем белого списка hello IP-адреса для своего региона данных через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="121de-142">We recommend you whitelist hello IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="121de-143">Вы можете загрузить hello [список IP-адресов центра обработки данных Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="121de-143">You can download hello [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="121de-144">Список обновляется раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="121de-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="121de-145">Hello IP-адресов в списке IP-центра обработки данных Azure hello находятся в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="121de-145">hello IP Addresses listed in hello Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="121de-146">Например, 10.0.0.0/24 не означает 10.0.0.0–10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="121de-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="121de-147">Дополнительные сведения о hello [в CIDR-нотации](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="121de-147">Learn more about hello [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="121de-148">Здесь представлены Hello hello полные доменные имена, используемый шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="121de-148">hello following are hello fully qualified domain names used by hello gateway.</span></span>

| <span data-ttu-id="121de-149">Имена доменов</span><span class="sxs-lookup"><span data-stu-id="121de-149">Domain names</span></span> | <span data-ttu-id="121de-150">Исходящие порты</span><span class="sxs-lookup"><span data-stu-id="121de-150">Outbound ports</span></span> | <span data-ttu-id="121de-151">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="121de-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="121de-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="121de-152">*.powerbi.com</span></span> |<span data-ttu-id="121de-153">80</span><span class="sxs-lookup"><span data-stu-id="121de-153">80</span></span> |<span data-ttu-id="121de-154">Установщик hello toodownload используется HTTP.</span><span class="sxs-lookup"><span data-stu-id="121de-154">HTTP used toodownload hello installer.</span></span> |
| <span data-ttu-id="121de-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="121de-155">*.powerbi.com</span></span> |<span data-ttu-id="121de-156">443</span><span class="sxs-lookup"><span data-stu-id="121de-156">443</span></span> |<span data-ttu-id="121de-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-157">HTTPS</span></span> |
| <span data-ttu-id="121de-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="121de-158">*.analysis.windows.net</span></span> |<span data-ttu-id="121de-159">443</span><span class="sxs-lookup"><span data-stu-id="121de-159">443</span></span> |<span data-ttu-id="121de-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-160">HTTPS</span></span> |
| <span data-ttu-id="121de-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="121de-161">*.login.windows.net</span></span> |<span data-ttu-id="121de-162">443</span><span class="sxs-lookup"><span data-stu-id="121de-162">443</span></span> |<span data-ttu-id="121de-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-163">HTTPS</span></span> |
| <span data-ttu-id="121de-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="121de-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="121de-165">5671–5672</span><span class="sxs-lookup"><span data-stu-id="121de-165">5671-5672</span></span> |<span data-ttu-id="121de-166">Протокол AMQP</span><span class="sxs-lookup"><span data-stu-id="121de-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="121de-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="121de-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="121de-168">443, 9350–9354</span><span class="sxs-lookup"><span data-stu-id="121de-168">443, 9350-9354</span></span> |<span data-ttu-id="121de-169">Прослушиватели ретрансляции служебной шины по протоколу TCP (порт 443 требуется для получения маркера контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="121de-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="121de-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="121de-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="121de-171">443</span><span class="sxs-lookup"><span data-stu-id="121de-171">443</span></span> |<span data-ttu-id="121de-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-172">HTTPS</span></span> |
| <span data-ttu-id="121de-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="121de-173">*.core.windows.net</span></span> |<span data-ttu-id="121de-174">443</span><span class="sxs-lookup"><span data-stu-id="121de-174">443</span></span> |<span data-ttu-id="121de-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-175">HTTPS</span></span> |
| <span data-ttu-id="121de-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="121de-176">login.microsoftonline.com</span></span> |<span data-ttu-id="121de-177">443</span><span class="sxs-lookup"><span data-stu-id="121de-177">443</span></span> |<span data-ttu-id="121de-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="121de-178">HTTPS</span></span> |
| <span data-ttu-id="121de-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="121de-179">*.msftncsi.com</span></span> |<span data-ttu-id="121de-180">443</span><span class="sxs-lookup"><span data-stu-id="121de-180">443</span></span> |<span data-ttu-id="121de-181">Подключение к Интернету tootest используется в том случае, если шлюз hello недоступен для hello службы Power BI.</span><span class="sxs-lookup"><span data-stu-id="121de-181">Used tootest internet connectivity if hello gateway is unreachable by hello Power BI service.</span></span> |
| <span data-ttu-id="121de-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="121de-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="121de-183">443</span><span class="sxs-lookup"><span data-stu-id="121de-183">443</span></span> |<span data-ttu-id="121de-184">Используется для проверки подлинности в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="121de-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="121de-185"><a name="force-https"></a>Принудительное взаимодействие протокола HTTPS со служебной шиной Azure</span><span class="sxs-lookup"><span data-stu-id="121de-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="121de-186">Можно принудительно toocommunicate hello шлюза с Azure Service Bus с помощью HTTPS вместо прямого TCP; Тем не менее это таким образом может значительно снизить производительность.</span><span class="sxs-lookup"><span data-stu-id="121de-186">You can force hello gateway toocommunicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="121de-187">Вы можете изменить hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* файла, изменив значение hello с `AutoDetect` слишком`Https`.</span><span class="sxs-lookup"><span data-stu-id="121de-187">You can modify hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing hello value from `AutoDetect` too`Https`.</span></span> <span data-ttu-id="121de-188">Обычно этот файл находится в расположении *C:\Program Files\On-premises data gateway*.</span><span class="sxs-lookup"><span data-stu-id="121de-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="121de-189"><a name="faq"></a>Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="121de-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="121de-190">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="121de-190">General</span></span>

<span data-ttu-id="121de-191">**Q**: требуется использовать шлюз для источников данных в облаке hello, таких как базы данных SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="121de-191">**Q**: Do I need a gateway for data sources in hello cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="121de-192">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="121de-192">
**A**: No.</span></span> <span data-ttu-id="121de-193">Шлюз соединяет локальные tooon только источники данных.</span><span class="sxs-lookup"><span data-stu-id="121de-193">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="121de-194">**Q**: hello шлюза имеет toobe установлен на компьютер же, как источник данных hello hello?</span><span class="sxs-lookup"><span data-stu-id="121de-194">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="121de-195">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="121de-195">
**A**: No.</span></span> <span data-ttu-id="121de-196">toohello источника данных, используя сведения о соединении hello, предоставленный подключение шлюза Hello.</span><span class="sxs-lookup"><span data-stu-id="121de-196">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="121de-197">Рассмотрим hello шлюза как клиентское приложение в этом смысле.</span><span class="sxs-lookup"><span data-stu-id="121de-197">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="121de-198">Hello шлюз требуется только hello возможность tooconnect toohello имя сервера, предоставленный, обычно на hello же сети.</span><span class="sxs-lookup"><span data-stu-id="121de-198">hello gateway just needs hello capability tooconnect toohello server name that was provided, typically on hello same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="121de-199">**Q**: Почему требуется toouse рабочей или учебной учетной записи toosign в?</span><span class="sxs-lookup"><span data-stu-id="121de-199">**Q**: Why do I need toouse a work or school account toosign in?</span></span> <br/><span data-ttu-id="121de-200">
**Объект**: только можно использовать Azure на работе или рабочую учетную запись при установке hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="121de-200">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="121de-201">Учетная запись для входа хранится в клиенте, которым управляет Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="121de-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="121de-202">Как правило учетной записи Azure AD имя участника-пользователя (UPN) соответствует адресу электронной почты hello.</span><span class="sxs-lookup"><span data-stu-id="121de-202">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="121de-203">**Вопрос**. Где хранятся мои учетные данные?</span><span class="sxs-lookup"><span data-stu-id="121de-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="121de-204">
**Объект**: зашифрованы и хранятся в облачной службе шлюза hello hello учетные данные, введенные для источника данных.</span><span class="sxs-lookup"><span data-stu-id="121de-204">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello Gateway Cloud Service.</span></span> <span data-ttu-id="121de-205">Hello они расшифровываются hello локальный шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="121de-205">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="121de-206">**Вопрос**. Есть ли какие-либо требования к пропускной способности сети?</span><span class="sxs-lookup"><span data-stu-id="121de-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="121de-207">
**Ответ.** Пропускная способность сети должна быть высокой.</span><span class="sxs-lookup"><span data-stu-id="121de-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="121de-208">Каждая среда имеет свои и hello объем отправляемых данных влияет на результаты hello.</span><span class="sxs-lookup"><span data-stu-id="121de-208">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="121de-209">С помощью ExpressRoute может помочь tooguarantee определенную пропускную способность между локальной и hello центрами обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="121de-209">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="121de-210">Можно использовать пропускную способность hello стороннего средства Azure скорость тестирования приложения toohelp датчика.</span><span class="sxs-lookup"><span data-stu-id="121de-210">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="121de-211">**Q**: что такое hello задержку для выполнения запросов источника данных tooa из шлюза hello?</span><span class="sxs-lookup"><span data-stu-id="121de-211">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="121de-212">Что такое hello оптимальная архитектура?</span><span class="sxs-lookup"><span data-stu-id="121de-212">What is hello best architecture?</span></span> <br/><span data-ttu-id="121de-213">
**Объект**: tooreduce задержку в сети и установить шлюз hello закрыть toohello источник данных как можно.</span><span class="sxs-lookup"><span data-stu-id="121de-213">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="121de-214">При установке шлюза hello hello фактические данные источника этого выражения с учетом сводит к минимуму задержки hello, введенной.</span><span class="sxs-lookup"><span data-stu-id="121de-214">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="121de-215">Рассмотрим слишком hello центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="121de-215">Consider hello datacenters too.</span></span> <span data-ttu-id="121de-216">Например если служба использует hello Запад США центра обработки данных и сервер SQL Server, размещенных на виртуальной Машине Azure, ВМ Azure должны находиться в hello Запад США слишком.</span><span class="sxs-lookup"><span data-stu-id="121de-216">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="121de-217">Это выражение с учетом сводит к минимуму задержки и позволяет избежать расходов на исходящие данные на виртуальной Машине Azure hello.</span><span class="sxs-lookup"><span data-stu-id="121de-217">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="121de-218">**Q**: как являются облачной серверной toohello набор результатов?</span><span class="sxs-lookup"><span data-stu-id="121de-218">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="121de-219">
**Объект**: результаты отправляются через hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="121de-219">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="121de-220">**Q**: существуют шлюза toohello все входящие подключения из облака hello?</span><span class="sxs-lookup"><span data-stu-id="121de-220">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="121de-221">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="121de-221">
**A**: No.</span></span> <span data-ttu-id="121de-222">шлюз Hello использует tooAzure исходящие подключения Service Bus.</span><span class="sxs-lookup"><span data-stu-id="121de-222">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="121de-223">**Вопрос**. Что делать, если мной заблокированы исходящие подключения?</span><span class="sxs-lookup"><span data-stu-id="121de-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="121de-224">Что делать мне tooopen?</span><span class="sxs-lookup"><span data-stu-id="121de-224">What do I need tooopen?</span></span> <br/><span data-ttu-id="121de-225">
**Объект**: hello порты и узлы, которые использует шлюз hello. в разделе.</span><span class="sxs-lookup"><span data-stu-id="121de-225">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="121de-226">**Q**: как называется соответствующая служба Windows hello?</span><span class="sxs-lookup"><span data-stu-id="121de-226">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="121de-227">
**Объект**: В службах, hello шлюз указан под именем локальной службы шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="121de-227">
**A**: In Services, hello gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="121de-228">**Q**: можно запускать с учетной записью Azure Active Directory служба Windows шлюза "hello"?</span><span class="sxs-lookup"><span data-stu-id="121de-228">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="121de-229">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="121de-229">
**A**: No.</span></span> <span data-ttu-id="121de-230">Служба Windows Hello должен иметь допустимую учетную запись Windows.</span><span class="sxs-lookup"><span data-stu-id="121de-230">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="121de-231">По умолчанию hello служба запускается с hello SID службы NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="121de-231">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="121de-232"><a name="high-availability"></a>Высокий уровень доступности и аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="121de-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="121de-233">**Вопрос**. Какие варианты доступны для аварийного восстановления?</span><span class="sxs-lookup"><span data-stu-id="121de-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="121de-234">
**Объект**: можно использовать toorestore ключа восстановления hello или переноса шлюза.</span><span class="sxs-lookup"><span data-stu-id="121de-234">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="121de-235">При установке шлюза hello, укажите ключ восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="121de-235">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="121de-236">**Q**: что такое преимущество hello hello ключ восстановления?</span><span class="sxs-lookup"><span data-stu-id="121de-236">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="121de-237">
**Объект**: hello ключ восстановления предоставляет toomigrate способом или восстановить параметры шлюза после сбоя.</span><span class="sxs-lookup"><span data-stu-id="121de-237">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="121de-238"><a name="troubleshooting"> </a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="121de-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="121de-239">**Q**: как я могу узнать, какие запросы отправляются toohello к локальному источнику данных?</span><span class="sxs-lookup"><span data-stu-id="121de-239">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="121de-240">
**Объект**: можно включить трассировку запроса, включая hello запросы, отправленные.</span><span class="sxs-lookup"><span data-stu-id="121de-240">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="121de-241">Не забывайте toochange запроса отслеживания в обратном toohello исходное значение после завершения устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="121de-241">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="121de-242">При включенной трассировке запросов создаются журналы большего размера.</span><span class="sxs-lookup"><span data-stu-id="121de-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="121de-243">Кроме того, можно рассмотреть инструменты трассировки запросов, доступные для вашего источника данных.</span><span class="sxs-lookup"><span data-stu-id="121de-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="121de-244">Например, можно использовать расширенные события или SQL Profiler для SQL Server и служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="121de-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="121de-245">**Q**: где находятся журналы шлюза hello?</span><span class="sxs-lookup"><span data-stu-id="121de-245">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="121de-246">
**Ответ**. См. раздел "Журналы" далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="121de-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="121de-247"><a name="update"></a>Последнюю версию обновления toohello</span><span class="sxs-lookup"><span data-stu-id="121de-247"><a name="update"></a>Update toohello latest version</span></span>

<span data-ttu-id="121de-248">Многие проблемы могут возникать при устаревшей версии шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="121de-248">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="121de-249">В качестве общих рекомендаций убедитесь, что используется последняя версия hello.</span><span class="sxs-lookup"><span data-stu-id="121de-249">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="121de-250">Hello шлюз не обновлялся в течение месяца или более, может рекомендуется установить последнюю версию шлюза hello hello и разделе, если можно воспроизвести проблему hello.</span><span class="sxs-lookup"><span data-stu-id="121de-250">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="121de-251">: Ошибка toogroup tooadd пользователя.</span><span class="sxs-lookup"><span data-stu-id="121de-251">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="121de-252">(-2147463168 PBIEgwService Performance Log Users ) (-2147463168 пользователей журналов производительности PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="121de-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="121de-253">Эту ошибку можно получить, если при попытке tooinstall hello шлюз на контроллере домена, который не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="121de-253">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="121de-254">Убедитесь, что развертывании hello шлюза на компьютере, который не контроллер домена.</span><span class="sxs-lookup"><span data-stu-id="121de-254">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="121de-255"><a name="logs"></a>Журналы</span><span class="sxs-lookup"><span data-stu-id="121de-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="121de-256">Файлы журналов являются важным ресурсом при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="121de-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="121de-257">Журналы службы корпоративного шлюза</span><span class="sxs-lookup"><span data-stu-id="121de-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="121de-258">Журналы конфигурации</span><span class="sxs-lookup"><span data-stu-id="121de-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="121de-259">Журналы событий</span><span class="sxs-lookup"><span data-stu-id="121de-259">Event logs</span></span>

<span data-ttu-id="121de-260">Найти hello журналы шлюза управления данными и PowerBIGateway **журналы приложений и служб**.</span><span class="sxs-lookup"><span data-stu-id="121de-260">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="121de-261"><a name="telemetry"></a>Телеметрия</span><span class="sxs-lookup"><span data-stu-id="121de-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="121de-262">Телеметрию можно использовать для мониторинга и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="121de-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="121de-263">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="121de-263">By default</span></span>

<span data-ttu-id="121de-264">**tooturn телеметрию**</span><span class="sxs-lookup"><span data-stu-id="121de-264">**tooturn on telemetry**</span></span>

1.  <span data-ttu-id="121de-265">Проверьте hello локальных данных шлюза клиентский каталог на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="121de-265">Check hello On-premises data gateway client directory on hello computer.</span></span> <span data-ttu-id="121de-266">Обычно это каталог **%системный_диск%\Program Files\On-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="121de-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="121de-267">Или откройте консоль служб и проверьте путь tooexecutable hello: свойство службы шлюза hello локальных данных.</span><span class="sxs-lookup"><span data-stu-id="121de-267">Or, you can open a Services console and check hello Path tooexecutable: A property of hello On-premises data gateway service.</span></span>
2.  <span data-ttu-id="121de-268">В файле Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config hello из каталога клиента.</span><span class="sxs-lookup"><span data-stu-id="121de-268">In hello Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="121de-269">Измените параметр tootrue hello SendTelemetry.</span><span class="sxs-lookup"><span data-stu-id="121de-269">Change hello SendTelemetry setting tootrue.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="121de-270">Сохраните изменения и перезапустите службу Windows hello: локальная служба шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="121de-270">Save your changes and restart hello Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="121de-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="121de-271">Next steps</span></span>
* [<span data-ttu-id="121de-272">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="121de-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="121de-273">Получение данных из служб Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="121de-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
