---
title: "Включение сквозного режима связи SSL в шлюзе приложений Azure| Документация Майкрософт"
description: "На этой странице представлен обзор поддержки сквозного режима связи SSL в шлюзе приложений."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: 689ee54dc1db2ea371b08270718278fd98c65bb5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-end-to-end-ssl-with-application-gateway"></a><span data-ttu-id="72d26-103">Обзор сквозного режима связи SSL в шлюзе приложений</span><span class="sxs-lookup"><span data-stu-id="72d26-103">Overview of end to end SSL with Application Gateway</span></span>

<span data-ttu-id="72d26-104">Шлюз приложений поддерживает функции моста SSL, после применения которых трафик обычно передается в незашифрованном виде на внутренние серверы.</span><span class="sxs-lookup"><span data-stu-id="72d26-104">Application gateway supports SSL termination at the gateway, after which traffic typically flows unencrypted to the backend servers.</span></span> <span data-ttu-id="72d26-105">Это позволяет избавить веб-серверы от накладных расходов, связанных с ресурсоемкими операциями шифрования и расшифровки.</span><span class="sxs-lookup"><span data-stu-id="72d26-105">This feature allows web servers to be unburdened from costly encryption and decryption overhead.</span></span> <span data-ttu-id="72d26-106">Однако для некоторых клиентов незашифрованная связь с внутренними серверами — неприемлемый вариант.</span><span class="sxs-lookup"><span data-stu-id="72d26-106">However for some customers unencrypted communication to the backend servers is not an acceptable option.</span></span> <span data-ttu-id="72d26-107">Причина может быть связана с требованиями безопасности и соответствия или с тем, что приложение может принимать только безопасные подключения.</span><span class="sxs-lookup"><span data-stu-id="72d26-107">This unencrypted communication could be due to security requirements, compliance requirements, or the application may only accept a secure connection.</span></span> <span data-ttu-id="72d26-108">Теперь для таких приложений шлюз приложений поддерживает сквозное шифрование SSL.</span><span class="sxs-lookup"><span data-stu-id="72d26-108">For such applications, application gateway supports end to end SSL encryption.</span></span>

## <a name="overview"></a><span data-ttu-id="72d26-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="72d26-109">Overview</span></span>

<span data-ttu-id="72d26-110">Сквозное шифрование SSL позволяет безопасно передавать зашифрованные конфиденциальные данные в серверную часть, используя при этом обеспечиваемые шлюзом приложений преимущества балансировки нагрузки уровня 7.</span><span class="sxs-lookup"><span data-stu-id="72d26-110">End to end SSL allows you to securely transmit sensitive data to the backend encrypted while still taking advantage of the benefits of Layer 7 load balancing features which application gateway provides.</span></span> <span data-ttu-id="72d26-111">Сюда входит сходство сеансов на основе файлов cookie, маршрутизация на основе URL-адресов, поддержка маршрутизации на основе сайтов и возможность внедрения заголовков X-Forwarded-*.</span><span class="sxs-lookup"><span data-stu-id="72d26-111">Some of these features are cookie-based session affinity, URL-based routing, support for routing based on sites, or ability to inject X-Forwarded-* headers.</span></span>

<span data-ttu-id="72d26-112">Если на шлюзе приложений настроен сквозной режим связи SSL, он завершает сеансы SSL пользователей на шлюзе и расшифровывает пользовательский трафик.</span><span class="sxs-lookup"><span data-stu-id="72d26-112">When configured with end to end SSL communication mode, application gateway terminates the SSL sessions at the gateway and decrypts user traffic.</span></span> <span data-ttu-id="72d26-113">Затем он применяет настроенные правила и выбирает подходящий экземпляр внутреннего пула для передачи трафика в него.</span><span class="sxs-lookup"><span data-stu-id="72d26-113">It then applies the configured rules to select an appropriate backend pool instance to route traffic to.</span></span> <span data-ttu-id="72d26-114">Затем шлюз приложений инициирует новое SSL-подключение ко внутреннему серверу и повторно шифрует данные с помощью сертификата открытого ключа внутреннего сервера, прежде чем передать запрос в серверную часть.</span><span class="sxs-lookup"><span data-stu-id="72d26-114">Application gateway then initiates a new SSL connection to the backend server and re-encrypts data using the backend server's public key certificate before transmitting the request to the backend.</span></span> <span data-ttu-id="72d26-115">Чтобы включить сквозной режим связи SSL, следует задать значение HTTPS для параметра протокола в BackendHTTPSetting, который применяется к внутреннему пулу.</span><span class="sxs-lookup"><span data-stu-id="72d26-115">End to end SSL is enabled by setting protocol setting in BackendHTTPSetting to HTTPS, which is then applied to a backend pool.</span></span> <span data-ttu-id="72d26-116">Для каждого внутреннего сервера во внутреннем пуле, для которого включен сквозной режим связи SSL, должен быть настроен сертификат, обеспечивающий безопасный обмен данными.</span><span class="sxs-lookup"><span data-stu-id="72d26-116">Each backend server in the backend pool with end to end SSL enabled must be configured with a certificate to allow secure communication.</span></span>

![Сценарий сквозного шифрования SSL][1]

<span data-ttu-id="72d26-118">В этом примере запросы, в которых используется TLS1.2, направляются на внутренние серверы в пул 1 с помощью сквозного шифрования SSL.</span><span class="sxs-lookup"><span data-stu-id="72d26-118">In this example, requests using TLS1.2 are routed to backend servers in Pool1 using end to end SSL.</span></span>

## <a name="end-to-end-ssl-and-whitelisting-of-certificates"></a><span data-ttu-id="72d26-119">Сквозное шифрование SSL и список разрешенных сертификатов</span><span class="sxs-lookup"><span data-stu-id="72d26-119">End to end SSL and whitelisting of certificates</span></span>

<span data-ttu-id="72d26-120">Шлюз приложений взаимодействует только с известными экземплярами серверной части, которые имеют сертификат из списка разрешений, определенного на шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="72d26-120">Application gateway only communicates with known backend instances that have whitelisted their certificate with the application gateway.</span></span> <span data-ttu-id="72d26-121">Чтобы включить список разрешенных сертификатов, необходимо передать открытый ключ сертификатов внутреннего сервера (а не корневой сертификат) в шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="72d26-121">To enable whitelisting of certificates, you must upload the public key of backend server certificates to the application gateway (not the root certificate).</span></span> <span data-ttu-id="72d26-122">После этого будут разрешены подключения только к известным и включенным в разрешенный список серверам.</span><span class="sxs-lookup"><span data-stu-id="72d26-122">Only connections to known and whitelisted backends are then allowed.</span></span> <span data-ttu-id="72d26-123">Оставшиеся серверы будут выдавать ошибку шлюза.</span><span class="sxs-lookup"><span data-stu-id="72d26-123">The remaining backends results in a gateway error.</span></span> <span data-ttu-id="72d26-124">Самозаверяющие сертификаты предназначены только для тестирования и не рекомендуются для рабочих нагрузок в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="72d26-124">Self-signed certificates are for test purposes only and not recommended for production workloads.</span></span> <span data-ttu-id="72d26-125">Такие сертификаты также должны быть добавлены в список разрешений с помощью шлюза приложений, как было описано ранее, прежде чем их можно будет использовать.</span><span class="sxs-lookup"><span data-stu-id="72d26-125">Such certificates have to be whitelisted with the application gateway as described in the preceding steps before they can be used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72d26-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72d26-126">Next steps</span></span>

<span data-ttu-id="72d26-127">Ознакомившись со сквозным режимом связи SSL и политиками SSL, перейдите к [включению сквозного режима связи SSL в шлюзе приложений](application-gateway-end-to-end-ssl-powershell.md), чтобы создать шлюз приложений с помощью сквозного шифрования SSL.</span><span class="sxs-lookup"><span data-stu-id="72d26-127">After learning about end to end SSL, go to [enable end to end SSL on application gateway](application-gateway-end-to-end-ssl-powershell.md) to create an application gateway using end to end SSL.</span></span>

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
