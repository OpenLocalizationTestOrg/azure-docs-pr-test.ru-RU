---
title: "Настройка разгрузки SSL для шлюза приложений Azure с помощью портала Azure | Документация Майкрософт"
description: "На этой странице приводятся инструкции по созданию шлюза приложений с разгрузкой SSL с помощью портала."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="6f9b8-103">Настройка шлюза приложений для разгрузки SSL с помощью портала</span><span class="sxs-lookup"><span data-stu-id="6f9b8-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f9b8-104">портал Azure</span><span class="sxs-lookup"><span data-stu-id="6f9b8-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="6f9b8-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="6f9b8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="6f9b8-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f9b8-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="6f9b8-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f9b8-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="6f9b8-108">Шлюз приложений Azure можно настроить на завершение сеанса SSL в шлюзе, что позволит избежать выполнения дорогостоящей задачи SSL-шифрования на веб-ферме.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="6f9b8-109">Кроме того, разгрузка SSL упрощает процесс установки внешнего сервера и управления веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="6f9b8-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="6f9b8-110">Scenario</span></span>

<span data-ttu-id="6f9b8-111">В следующем сценарии рассматривается настройка разгрузки SSL в существующем шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="6f9b8-112">Предполагается, что действия по [созданию шлюза приложений](application-gateway-create-gateway-portal.md)уже выполнены.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f9b8-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6f9b8-113">Before you begin</span></span>

<span data-ttu-id="6f9b8-114">Чтобы настроить разгрузку SSL с помощью шлюза приложений, требуется сертификат.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="6f9b8-115">Этот сертификат загружается в шлюз приложений и используется для шифрования и расшифровки трафика, передаваемого через подключение SSL.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="6f9b8-116">Сертификат должен быть в формате PFX (файл обмена личной информацией).</span><span class="sxs-lookup"><span data-stu-id="6f9b8-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="6f9b8-117">Этот формат файла позволяет экспортировать закрытый ключ, необходимый шлюзу приложений для шифрования и расшифровки трафика.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="6f9b8-118">Добавление прослушивателя HTTPS</span><span class="sxs-lookup"><span data-stu-id="6f9b8-118">Add an HTTPS listener</span></span>

<span data-ttu-id="6f9b8-119">Прослушиватель HTTPS ищет трафик согласно заданной конфигурации и помогает направлять трафик во внутренние пулы.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="6f9b8-120">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6f9b8-120">Step 1</span></span>

<span data-ttu-id="6f9b8-121">Перейдите на портал Azure и выберите существующий шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="6f9b8-122">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6f9b8-122">Step 2</span></span>

<span data-ttu-id="6f9b8-123">Щелкните "Прослушиватели" и нажмите кнопку "Добавить", чтобы добавить прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-123">Click Listeners and click the Add button to add a listener.</span></span>

![Колонка обзора шлюза приложений][1]

### <a name="step-3"></a><span data-ttu-id="6f9b8-125">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-125">Step 3</span></span>

<span data-ttu-id="6f9b8-126">Введите необходимые сведения о прослушивателе и передайте PFX-файл сертификата. По завершении нажмите кнопку "ОК".</span><span class="sxs-lookup"><span data-stu-id="6f9b8-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="6f9b8-127">**Имя** — понятное имя прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="6f9b8-128">**Интерфейсная IP-конфигурация** — конфигурация интерфейсных IP-адресов, используемая для прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="6f9b8-129">**Интерфейсный порт (имя и порт)** — понятное имя порта, используемого во внешнем интерфейсе шлюза приложений, и фактически используемый порт.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="6f9b8-130">**Протокол** — параметр, позволяющий определить протокол, используемый для внешнего интерфейса: https или http.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="6f9b8-131">**Сертификат (имя и пароль)** — если используется разгрузка SSL, то для этого параметра требуется указать PFX-файл сертификата, понятное имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Колонка добавления прослушивателя][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="6f9b8-133">Создание правила и его привязка к прослушивателю</span><span class="sxs-lookup"><span data-stu-id="6f9b8-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="6f9b8-134">Теперь прослушиватель создан.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-134">The listener has now been created.</span></span> <span data-ttu-id="6f9b8-135">Пора создать правило для обработки трафика, поступающего от этого прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="6f9b8-136">Правила определяют, как трафик направляется во внутренние пулы, согласно параметрам нескольких конфигураций, включая использование сходства сеансов на основе файлов cookie, а также протокол, порт и пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="6f9b8-137">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="6f9b8-137">Step 1</span></span>

<span data-ttu-id="6f9b8-138">Щелкните **Правила** для шлюза приложений, затем щелкните "Добавить".</span><span class="sxs-lookup"><span data-stu-id="6f9b8-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![Колонка правил шлюза приложений][3]

### <a name="step-2"></a><span data-ttu-id="6f9b8-140">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="6f9b8-140">Step 2</span></span>

<span data-ttu-id="6f9b8-141">В колонке **Добавление базового правила** введите понятное имя правила и выберите прослушиватель, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="6f9b8-142">Выберите соответствующий внутренний пул и параметр http, затем нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="6f9b8-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![Окно параметров HTTPS][4]

<span data-ttu-id="6f9b8-144">Теперь параметры сохранены в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="6f9b8-145">Процесс сохранения этих параметров может занять некоторое время, которое пройдет, прежде чем они станут доступны для просмотра посредством портала или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="6f9b8-146">После сохранения параметров шлюз приложений выполняет шифрование и расшифровку трафика.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="6f9b8-147">Весь трафик между шлюзом приложений и внутренними веб-серверами будет передаваться с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="6f9b8-148">Если передача была инициирована по протоколу HTTPS, то любые данные, передаваемые обратно клиенту, будут шифроваться.</span><span class="sxs-lookup"><span data-stu-id="6f9b8-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f9b8-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f9b8-149">Next steps</span></span>

<span data-ttu-id="6f9b8-150">Чтобы узнать, как настроить пользовательскую пробу работоспособности с использованием шлюза приложений Azure, ознакомьтесь с разделом [Create a custom probe for Application Gateway by using the portal](application-gateway-create-gateway-portal.md)(Создание пользовательской пробы для шлюза приложений с помощью портала).</span><span class="sxs-lookup"><span data-stu-id="6f9b8-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
