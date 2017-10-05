---
title: "Локальный шлюз данных | Документация Майкрософт"
description: "Локальный шлюз данных необходим тогда, когда сервер служб Analysis Services в Azure будет подключен к локальным источникам данных."
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
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="58912-103">Подключение к локальным источникам данных с помощью локального шлюза данных Azure</span><span class="sxs-lookup"><span data-stu-id="58912-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="58912-104">Локальный шлюз данных действует как мост, обеспечивая передачу данных между локальными источниками данных и серверами служб Azure Analysis Services в облаке.</span><span class="sxs-lookup"><span data-stu-id="58912-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="58912-105">Последняя версия шлюза работает с несколькими серверами служб Azure Analysis Services в том же регионе, а также с Azure Logic Apps, Power BI, Power Apps и Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="58912-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="58912-106">Несколько служб в одном регионе можно связать с одним шлюзом.</span><span class="sxs-lookup"><span data-stu-id="58912-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="58912-107">Для этого Azure Analysis Services необходимо, чтобы в том же регионе находился ресурс шлюза.</span><span class="sxs-lookup"><span data-stu-id="58912-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="58912-108">Например, при наличии серверов служб Azure Analysis Services в регионе "Восток США 2" необходим ресурс шлюза в регионе "Восток США 2".</span><span class="sxs-lookup"><span data-stu-id="58912-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="58912-109">Несколько серверов в регионе "Восток США 2" могут использовать один шлюз.</span><span class="sxs-lookup"><span data-stu-id="58912-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="58912-110">Впервые процесс установки с помощью шлюза проходит в четыре этапа:</span><span class="sxs-lookup"><span data-stu-id="58912-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="58912-111">**Скачивание и запуск программы установки.** На этом шаге устанавливается служба шлюза на компьютер организации.</span><span class="sxs-lookup"><span data-stu-id="58912-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="58912-112">**Регистрация шлюза.** На этом шаге следует указать имя и ключ восстановления для шлюза и выбрать регион. Таким образом шлюз регистрируется в облачной службе шлюза.</span><span class="sxs-lookup"><span data-stu-id="58912-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="58912-113">**Создание ресурса шлюза в Azure.** На этом шаге необходимо создать ресурс шлюза в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="58912-114">**Подключение серверов к ресурсу шлюза.** После получения ресурса шлюза в подписке можно начать подключение к нему серверов.</span><span class="sxs-lookup"><span data-stu-id="58912-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="58912-115">При наличии настроенного для вашей подписки ресурса шлюза можно подключить к нему несколько серверов и других служб.</span><span class="sxs-lookup"><span data-stu-id="58912-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="58912-116">Необходимо только установить другой шлюз и создать дополнительные ресурсы шлюза при наличии серверов или других служб в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="58912-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="58912-117">Чтобы начать работу прямо сейчас, см. статью [Установка и настройка локального шлюза данных](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="58912-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="58912-118"><a name="how-it-works"> </a>Принцип работы</span><span class="sxs-lookup"><span data-stu-id="58912-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="58912-119">Установленный на компьютере в вашей организации шлюз работает как служба Windows, **локальный шлюз данных**.</span><span class="sxs-lookup"><span data-stu-id="58912-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="58912-120">Эта локальная служба зарегистрирована в облачной службе шлюза с помощью служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="58912-121">Затем создается ресурс шлюза в службе Gateway Cloud для подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="58912-122">После этого серверы служб Azure Analysis Services уже подключены к ресурсу шлюза.</span><span class="sxs-lookup"><span data-stu-id="58912-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="58912-123">Если моделям вашего сервера необходимо подключиться к локальным источникам данных для запросов или обработки, запрос и поток данных проходит через ресурс шлюза, служебную шину Azure, локальную службу локального шлюза данных и источники данных.</span><span class="sxs-lookup"><span data-stu-id="58912-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![Принцип работы](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="58912-125">Запросы и поток данных</span><span class="sxs-lookup"><span data-stu-id="58912-125">Queries and data flow:</span></span>

1. <span data-ttu-id="58912-126">Облачная служба создает запрос с зашифрованными учетными данными для локального источника.</span><span class="sxs-lookup"><span data-stu-id="58912-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="58912-127">Затем запрос отправляется в очередь, чтобы его обработал шлюз.</span><span class="sxs-lookup"><span data-stu-id="58912-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="58912-128">Облачная служба шлюза анализирует запрос и отправляет его в [служебную шину Azure](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="58912-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="58912-129">Локальный шлюз данных опрашивает служебную шину Azure, чтобы проверить наличие ожидающих запросов.</span><span class="sxs-lookup"><span data-stu-id="58912-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="58912-130">Шлюз получает запрос, расшифровывает учетные данные и подключается к источникам данных, используя эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="58912-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="58912-131">Затем шлюз отправляет запрос к источнику данных для выполнения.</span><span class="sxs-lookup"><span data-stu-id="58912-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="58912-132">Результаты отправляются из источника данных обратно в шлюз, а затем в облачную службу и на сервер.</span><span class="sxs-lookup"><span data-stu-id="58912-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="58912-133"><a name="windows-service-account"> </a>Учетная запись службы Windows</span><span class="sxs-lookup"><span data-stu-id="58912-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="58912-134">Локальный шлюз данных настроен для использования *NT SERVICE\PBIEgwService* в качестве учетных данных для входа службы Windows.</span><span class="sxs-lookup"><span data-stu-id="58912-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="58912-135">По умолчанию у него есть право входа в систему в качестве службы в контексте компьютера, на котором устанавливается шлюз.</span><span class="sxs-lookup"><span data-stu-id="58912-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="58912-136">Эти учетные данные не принадлежат той же учетной записи, которая используется для подключения к локальным источникам данных или к учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="58912-137">При возникновении проблем с прокси-сервером из-за проверки подлинности можно изменить учетную запись службы Windows на учетную запись пользователя домена или управляемую запись службы.</span><span class="sxs-lookup"><span data-stu-id="58912-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="58912-138"><a name="ports"> </a>Порты</span><span class="sxs-lookup"><span data-stu-id="58912-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="58912-139">Шлюз создает исходящее подключение к служебной шине Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="58912-140">Он обменивается данными через исходящие порты: TCP 443 (по умолчанию), а также 5671, 5672 и 9350–9354.</span><span class="sxs-lookup"><span data-stu-id="58912-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="58912-141">Шлюзу не требуются входящие порты.</span><span class="sxs-lookup"><span data-stu-id="58912-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="58912-142">Мы рекомендуем добавить IP-адреса для области данных в список разрешений вашего брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="58912-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="58912-143">Вы можете скачать [список IP-адресов центра обработки данных Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="58912-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="58912-144">Список обновляется раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="58912-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="58912-145">IP-адреса, перечисленные в списке центра обработки данных Azure, находятся в нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="58912-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="58912-146">Например, 10.0.0.0/24 не означает 10.0.0.0–10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="58912-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="58912-147">Дополнительные сведения о нотации CIDR см. [здесь](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="58912-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="58912-148">Ниже приведены полные доменные имена, которые используются шлюзом.</span><span class="sxs-lookup"><span data-stu-id="58912-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="58912-149">Имена доменов</span><span class="sxs-lookup"><span data-stu-id="58912-149">Domain names</span></span> | <span data-ttu-id="58912-150">Исходящие порты</span><span class="sxs-lookup"><span data-stu-id="58912-150">Outbound ports</span></span> | <span data-ttu-id="58912-151">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="58912-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58912-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="58912-152">*.powerbi.com</span></span> |<span data-ttu-id="58912-153">80</span><span class="sxs-lookup"><span data-stu-id="58912-153">80</span></span> |<span data-ttu-id="58912-154">HTTP для скачивания установщика.</span><span class="sxs-lookup"><span data-stu-id="58912-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="58912-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="58912-155">*.powerbi.com</span></span> |<span data-ttu-id="58912-156">443</span><span class="sxs-lookup"><span data-stu-id="58912-156">443</span></span> |<span data-ttu-id="58912-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-157">HTTPS</span></span> |
| <span data-ttu-id="58912-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="58912-158">*.analysis.windows.net</span></span> |<span data-ttu-id="58912-159">443</span><span class="sxs-lookup"><span data-stu-id="58912-159">443</span></span> |<span data-ttu-id="58912-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-160">HTTPS</span></span> |
| <span data-ttu-id="58912-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="58912-161">*.login.windows.net</span></span> |<span data-ttu-id="58912-162">443</span><span class="sxs-lookup"><span data-stu-id="58912-162">443</span></span> |<span data-ttu-id="58912-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-163">HTTPS</span></span> |
| <span data-ttu-id="58912-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="58912-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="58912-165">5671–5672</span><span class="sxs-lookup"><span data-stu-id="58912-165">5671-5672</span></span> |<span data-ttu-id="58912-166">Протокол AMQP</span><span class="sxs-lookup"><span data-stu-id="58912-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="58912-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="58912-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="58912-168">443, 9350–9354</span><span class="sxs-lookup"><span data-stu-id="58912-168">443, 9350-9354</span></span> |<span data-ttu-id="58912-169">Прослушиватели ретрансляции служебной шины по протоколу TCP (порт 443 требуется для получения маркера контроля доступа).</span><span class="sxs-lookup"><span data-stu-id="58912-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="58912-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="58912-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="58912-171">443</span><span class="sxs-lookup"><span data-stu-id="58912-171">443</span></span> |<span data-ttu-id="58912-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-172">HTTPS</span></span> |
| <span data-ttu-id="58912-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="58912-173">*.core.windows.net</span></span> |<span data-ttu-id="58912-174">443</span><span class="sxs-lookup"><span data-stu-id="58912-174">443</span></span> |<span data-ttu-id="58912-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-175">HTTPS</span></span> |
| <span data-ttu-id="58912-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="58912-176">login.microsoftonline.com</span></span> |<span data-ttu-id="58912-177">443</span><span class="sxs-lookup"><span data-stu-id="58912-177">443</span></span> |<span data-ttu-id="58912-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="58912-178">HTTPS</span></span> |
| <span data-ttu-id="58912-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="58912-179">*.msftncsi.com</span></span> |<span data-ttu-id="58912-180">443</span><span class="sxs-lookup"><span data-stu-id="58912-180">443</span></span> |<span data-ttu-id="58912-181">Используется для проверки подключения к Интернету, если шлюз недоступен для службы Power BI.</span><span class="sxs-lookup"><span data-stu-id="58912-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="58912-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="58912-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="58912-183">443</span><span class="sxs-lookup"><span data-stu-id="58912-183">443</span></span> |<span data-ttu-id="58912-184">Используется для проверки подлинности в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="58912-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="58912-185"><a name="force-https"></a>Принудительное взаимодействие протокола HTTPS со служебной шиной Azure</span><span class="sxs-lookup"><span data-stu-id="58912-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="58912-186">Можно настроить шлюз для принудительного использования протокола HTTPS для связи со служебной шиной Azure вместо прямого подключения TCP. Однако это может значительно снизить производительность.</span><span class="sxs-lookup"><span data-stu-id="58912-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="58912-187">Для этого можно отредактировать файл *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config*, изменив значение `AutoDetect` на `Https`.</span><span class="sxs-lookup"><span data-stu-id="58912-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="58912-188">Обычно этот файл находится в расположении *C:\Program Files\On-premises data gateway*.</span><span class="sxs-lookup"><span data-stu-id="58912-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="58912-189"><a name="faq"></a>Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="58912-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="58912-190">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="58912-190">General</span></span>

<span data-ttu-id="58912-191">**Вопрос**. Нужно ли устанавливать шлюз для источников данных в облаке, например для базы данных SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="58912-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="58912-192">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="58912-192">
**A**: No.</span></span> <span data-ttu-id="58912-193">Шлюз подключается только к локальным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="58912-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="58912-194">**Вопрос**. Нужно ли устанавливать шлюз на том же компьютере, на котором находится источник данных?</span><span class="sxs-lookup"><span data-stu-id="58912-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="58912-195">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="58912-195">
**A**: No.</span></span> <span data-ttu-id="58912-196">Шлюз подключается к источнику данных, используя предоставленные сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="58912-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="58912-197">В этом смысле шлюз можно рассматривать как клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="58912-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="58912-198">Для шлюза требуется только возможность подключения к серверу, имя которого было указано (как правило, в пределах той же сети).</span><span class="sxs-lookup"><span data-stu-id="58912-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="58912-199">**Вопрос.** Почему для входа необходимо использовать рабочую или учебную учетную запись Azure?</span><span class="sxs-lookup"><span data-stu-id="58912-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="58912-200">
**Ответ**. При установке локального шлюза данных вы можете использовать только рабочую или учебную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="58912-201">Учетная запись для входа хранится в клиенте, которым управляет Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58912-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="58912-202">Как правило, имя участника-пользователя учетной записи Azure AD совпадает с адресом электронной почты.</span><span class="sxs-lookup"><span data-stu-id="58912-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="58912-203">**Вопрос**. Где хранятся мои учетные данные?</span><span class="sxs-lookup"><span data-stu-id="58912-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="58912-204">
**Ответ.** Учетные данные, введенные для источника данных, хранятся в облачной службе шлюза в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="58912-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="58912-205">Расшифровываются они в локальном шлюзе данных.</span><span class="sxs-lookup"><span data-stu-id="58912-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="58912-206">**Вопрос**. Есть ли какие-либо требования к пропускной способности сети?</span><span class="sxs-lookup"><span data-stu-id="58912-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="58912-207">
**Ответ.** Пропускная способность сети должна быть высокой.</span><span class="sxs-lookup"><span data-stu-id="58912-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="58912-208">Все среды разные и объем отправляемых данных влияет на результаты.</span><span class="sxs-lookup"><span data-stu-id="58912-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="58912-209">Гарантировать определенный уровень пропускной способности между локальной средой и центрами обработки данных Azure может помочь применение ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="58912-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="58912-210">Измерить текущую пропускную способность можно с помощью стороннего инструмента — приложения Azure Speed Test.</span><span class="sxs-lookup"><span data-stu-id="58912-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="58912-211">**Вопрос**. Что такое задержка при выполнении запросов к источнику данных из шлюза?</span><span class="sxs-lookup"><span data-stu-id="58912-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="58912-212">Какая архитектура подойдет лучше всего?</span><span class="sxs-lookup"><span data-stu-id="58912-212">What is the best architecture?</span></span> <br/><span data-ttu-id="58912-213">
**Ответ**. Чтобы уменьшить задержки в сети, необходимо установить шлюз как можно ближе к источнику данных.</span><span class="sxs-lookup"><span data-stu-id="58912-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="58912-214">Вы можете установить шлюз на фактический источник данных, что сведет к минимуму соответствующие задержки.</span><span class="sxs-lookup"><span data-stu-id="58912-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="58912-215">Для этого также стоит рассмотреть центры обработки данных.</span><span class="sxs-lookup"><span data-stu-id="58912-215">Consider the datacenters too.</span></span> <span data-ttu-id="58912-216">Например, если служба использует центр обработки данных в западной части США, а SQL Server размещен на виртуальной машине Azure, то эту виртуальную машину лучше также разместить в западной части США.</span><span class="sxs-lookup"><span data-stu-id="58912-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="58912-217">Это позволит свести к минимуму задержки и избежать затрат на исходящий трафик виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="58912-218">**Вопрос**. Как результаты отправляются обратно в облако?</span><span class="sxs-lookup"><span data-stu-id="58912-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="58912-219">
**Ответ**. Результаты отправляются с помощью служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="58912-220">**Вопрос**. Устанавливаются ли какие-либо входящие подключения к шлюзу из облака?</span><span class="sxs-lookup"><span data-stu-id="58912-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="58912-221">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="58912-221">
**A**: No.</span></span> <span data-ttu-id="58912-222">Шлюз использует исходящие подключения к служебной шине Azure.</span><span class="sxs-lookup"><span data-stu-id="58912-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="58912-223">**Вопрос**. Что делать, если мной заблокированы исходящие подключения?</span><span class="sxs-lookup"><span data-stu-id="58912-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="58912-224">Что нужно открыть?</span><span class="sxs-lookup"><span data-stu-id="58912-224">What do I need to open?</span></span> <br/><span data-ttu-id="58912-225">
**Ответ**. Проверьте порты и узлы, которые использует шлюз.</span><span class="sxs-lookup"><span data-stu-id="58912-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="58912-226">**Вопрос**. Как на самом деле называется служба Windows?</span><span class="sxs-lookup"><span data-stu-id="58912-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="58912-227">
**Ответ**. В списке служб шлюз называется службой локального шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="58912-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="58912-228">**Вопрос**. Может ли служба Windows шлюза работать с учетной записью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58912-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="58912-229">
**Ответ**. Нет.</span><span class="sxs-lookup"><span data-stu-id="58912-229">
**A**: No.</span></span> <span data-ttu-id="58912-230">Службе Windows требуется действительная учетная запись Windows.</span><span class="sxs-lookup"><span data-stu-id="58912-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="58912-231">По умолчанию служба будет выполняться с идентификатором безопасности службы NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="58912-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="58912-232"><a name="high-availability"></a>Высокий уровень доступности и аварийное восстановление</span><span class="sxs-lookup"><span data-stu-id="58912-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="58912-233">**Вопрос**. Какие варианты доступны для аварийного восстановления?</span><span class="sxs-lookup"><span data-stu-id="58912-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="58912-234">
**Ответ**. Вы можете использовать ключ восстановления для восстановления или переноса шлюза.</span><span class="sxs-lookup"><span data-stu-id="58912-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="58912-235">Ключ восстановления указывается при установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="58912-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="58912-236">**Вопрос**. В чем заключается преимущество ключа восстановления?</span><span class="sxs-lookup"><span data-stu-id="58912-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="58912-237">
**Ответ.** Он позволяет перенести шлюз или восстановить его параметры после аварии.</span><span class="sxs-lookup"><span data-stu-id="58912-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="58912-238"><a name="troubleshooting"> </a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="58912-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="58912-239">**Вопрос**. Как узнать, какие запросы отправляются к локальному источнику данных?</span><span class="sxs-lookup"><span data-stu-id="58912-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="58912-240">
**Ответ**. Вы можете включить трассировку запросов, в том числе и отправляемых.</span><span class="sxs-lookup"><span data-stu-id="58912-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="58912-241">Не забудьте вернуть исходное значение трассировки запросов после устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="58912-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="58912-242">При включенной трассировке запросов создаются журналы большего размера.</span><span class="sxs-lookup"><span data-stu-id="58912-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="58912-243">Кроме того, можно рассмотреть инструменты трассировки запросов, доступные для вашего источника данных.</span><span class="sxs-lookup"><span data-stu-id="58912-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="58912-244">Например, можно использовать расширенные события или SQL Profiler для SQL Server и служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="58912-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="58912-245">**Вопрос**. Где находятся журналы шлюза?</span><span class="sxs-lookup"><span data-stu-id="58912-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="58912-246">
**Ответ**. См. раздел "Журналы" далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="58912-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="58912-247"><a name="update"></a>Обновление до последней версии</span><span class="sxs-lookup"><span data-stu-id="58912-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="58912-248">При использовании устаревшей версии шлюза может возникать ряд проблем.</span><span class="sxs-lookup"><span data-stu-id="58912-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="58912-249">Рекомендуем убедиться, что используется последняя версия.</span><span class="sxs-lookup"><span data-stu-id="58912-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="58912-250">Если шлюз не обновлялся месяц или дольше, то можно установить его последнюю версию и проверить, получится ли воспроизвести проблему.</span><span class="sxs-lookup"><span data-stu-id="58912-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="58912-251">Error: Failed to add user to group. (Ошибка: не удалось добавить пользователя в группу.)</span><span class="sxs-lookup"><span data-stu-id="58912-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="58912-252">(-2147463168 PBIEgwService Performance Log Users ) (-2147463168 пользователей журналов производительности PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="58912-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="58912-253">Эта ошибка появляется, если вы пытаетесь установить шлюз на контроллер домена, который не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="58912-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="58912-254">Убедитесь, что развертывание шлюза происходит на компьютере, который не является контроллером домена.</span><span class="sxs-lookup"><span data-stu-id="58912-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="58912-255"><a name="logs"></a>Журналы</span><span class="sxs-lookup"><span data-stu-id="58912-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="58912-256">Файлы журналов являются важным ресурсом при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="58912-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="58912-257">Журналы службы корпоративного шлюза</span><span class="sxs-lookup"><span data-stu-id="58912-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="58912-258">Журналы конфигурации</span><span class="sxs-lookup"><span data-stu-id="58912-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="58912-259">Журналы событий</span><span class="sxs-lookup"><span data-stu-id="58912-259">Event logs</span></span>

<span data-ttu-id="58912-260">Журналы шлюза управления данными и PowerBIGateway находятся в разделе **Журналы приложения и служб**.</span><span class="sxs-lookup"><span data-stu-id="58912-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="58912-261"><a name="telemetry"></a>Телеметрия</span><span class="sxs-lookup"><span data-stu-id="58912-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="58912-262">Телеметрию можно использовать для мониторинга и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="58912-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="58912-263">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="58912-263">By default</span></span>

<span data-ttu-id="58912-264">**Включение телеметрии**</span><span class="sxs-lookup"><span data-stu-id="58912-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="58912-265">Проверьте клиентский каталог локального шлюза данных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="58912-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="58912-266">Обычно это каталог **%системный_диск%\Program Files\On-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="58912-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="58912-267">Кроме того, можно открыть консоль "Службы" и проверить свойство "Путь доступа к исполняемому файлу" для службы локального шлюза данных.</span><span class="sxs-lookup"><span data-stu-id="58912-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="58912-268">В файле Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config в каталоге клиента выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="58912-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="58912-269">Измените значение параметра SendTelemetry на true.</span><span class="sxs-lookup"><span data-stu-id="58912-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="58912-270">Сохраните изменения и перезапустите службу Windows "Локальный шлюз данных".</span><span class="sxs-lookup"><span data-stu-id="58912-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="58912-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58912-271">Next steps</span></span>
* [<span data-ttu-id="58912-272">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="58912-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="58912-273">Получение данных из служб Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="58912-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
