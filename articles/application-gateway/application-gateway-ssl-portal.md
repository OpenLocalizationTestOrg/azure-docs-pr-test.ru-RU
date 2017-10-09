---
title: "aaaConfigure SSL разгрузки - шлюз Azure приложения - портал Azure | Документы Microsoft"
description: "На этой странице представлены инструкции toocreate разгрузки шлюза приложения с помощью протокола SSL с помощью портала hello"
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="33c68-103">Настройка шлюза приложения для разгрузки SSL с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="33c68-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="33c68-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="33c68-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="33c68-105">PowerShell и диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="33c68-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="33c68-106">Классическая модель — Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33c68-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="33c68-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="33c68-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="33c68-108">Шлюз приложения Azure может быть настроенный tooterminate hello Secure Sockets Layer (SSL) сеанс при hello шлюза tooavoid дорогостоящих SSL расшифровки задачи toohappen на hello веб-фермы.</span><span class="sxs-lookup"><span data-stu-id="33c68-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="33c68-109">Разгрузка SSL также упрощает hello интерфейсном сервере настройку и управление ими hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="33c68-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="33c68-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="33c68-110">Scenario</span></span>

<span data-ttu-id="33c68-111">следующие сценарии Hello проходит через Настройка разгрузки SSL для существующего шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="33c68-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="33c68-112">Hello сценарии предполагается, что уже выполнены действия hello слишком[создания шлюза приложения](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33c68-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="33c68-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="33c68-113">Before you begin</span></span>

<span data-ttu-id="33c68-114">tooconfigure разгрузки SSL со шлюзом приложений, требуется сертификат.</span><span class="sxs-lookup"><span data-stu-id="33c68-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="33c68-115">Этот сертификат загружается на шлюзе приложения hello и использовать tooencrypt и расшифровки hello трафика, передаваемого через SSL.</span><span class="sxs-lookup"><span data-stu-id="33c68-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="33c68-116">Hello сертификат должен toobe в формате обмена личной информацией (pfx).</span><span class="sxs-lookup"><span data-stu-id="33c68-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="33c68-117">Этот формат позволяет для hello закрытого ключа toobe экспортированы, необходимые для hello приложения шлюза tooperform hello шифрованием/дешифрованием трафика.</span><span class="sxs-lookup"><span data-stu-id="33c68-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="33c68-118">Добавление прослушивателя HTTPS</span><span class="sxs-lookup"><span data-stu-id="33c68-118">Add an HTTPS listener</span></span>

<span data-ttu-id="33c68-119">HTTPS-прослушиватель Hello ищет трафика в зависимости от конфигурации и помогает маршрута hello трафика toohello внутренние пулы.</span><span class="sxs-lookup"><span data-stu-id="33c68-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="33c68-120">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="33c68-120">Step 1</span></span>

<span data-ttu-id="33c68-121">Найдите toohello портал Azure и выберите существующего шлюза приложения</span><span class="sxs-lookup"><span data-stu-id="33c68-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="33c68-122">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="33c68-122">Step 2</span></span>

<span data-ttu-id="33c68-123">Нажмите кнопку прослушивателей затем tooadd кнопку hello добавить прослушиватель.</span><span class="sxs-lookup"><span data-stu-id="33c68-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![Колонка обзора шлюза приложений][1]

### <a name="step-3"></a><span data-ttu-id="33c68-125">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="33c68-125">Step 3</span></span>

<span data-ttu-id="33c68-126">Заполните необходимые сведения для прослушивателя hello hello и передачи hello PFX-файл сертификата, по завершении нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="33c68-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="33c68-127">**Имя** -это значение — это понятное имя прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="33c68-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="33c68-128">**Конфигурация интерфейсных IP-адресов** -это значение равно hello IP-конфигурацию, используемый для прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="33c68-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="33c68-129">**Интерфейсный порт (имя и порт)** -понятное имя для hello порт, используемый для внешнего интерфейса hello шлюза приложения hello и hello фактическое порт, используемый.</span><span class="sxs-lookup"><span data-stu-id="33c68-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="33c68-130">**Протокол** -toodetermine коммутатор, если для hello переднего плана используется протокол https или http.</span><span class="sxs-lookup"><span data-stu-id="33c68-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="33c68-131">**Сертификат (имя и пароль)** — если используется разгрузка SSL, то для этого параметра требуется указать PFX-файл сертификата, понятное имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="33c68-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![Колонка добавления прослушивателя][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="33c68-133">Создание правила и связать его toohello прослушивателя</span><span class="sxs-lookup"><span data-stu-id="33c68-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="33c68-134">создан прослушиватель Hello.</span><span class="sxs-lookup"><span data-stu-id="33c68-134">hello listener has now been created.</span></span> <span data-ttu-id="33c68-135">Это время toocreate трафика hello toohandle правило из hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="33c68-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="33c68-136">Правила определяют, как трафика перенаправленное toohello внутренние пулы на основе нескольких параметры конфигурации, включая использование сходство сеансов на основе файлов cookie, протокол, порт и проверках работоспособности.</span><span class="sxs-lookup"><span data-stu-id="33c68-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="33c68-137">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="33c68-137">Step 1</span></span>

<span data-ttu-id="33c68-138">Нажмите кнопку hello **правила** шлюза приложения hello и нажмите кнопку Добавить.</span><span class="sxs-lookup"><span data-stu-id="33c68-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![Колонка правил шлюза приложений][3]

### <a name="step-2"></a><span data-ttu-id="33c68-140">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="33c68-140">Step 2</span></span>

<span data-ttu-id="33c68-141">На hello **добавить базовое правило** колонки, введите в hello понятное имя для правила hello и нажмите на предыдущем шаге hello прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="33c68-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="33c68-142">Выберите соответствующий внутренний пул hello и настройка http и нажмите кнопку **ОК**</span><span class="sxs-lookup"><span data-stu-id="33c68-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![Окно параметров HTTPS][4]

<span data-ttu-id="33c68-144">Hello параметры будут сохранены toohello шлюз приложений.</span><span class="sxs-lookup"><span data-stu-id="33c68-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="33c68-145">Hello сохранения этих параметров может занять некоторое время, прежде чем они станут доступны tooview через портал hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33c68-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="33c68-146">Шлюз приложений после сохранения hello обрабатывает hello шифрования и расшифровки трафика.</span><span class="sxs-lookup"><span data-stu-id="33c68-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="33c68-147">Весь трафик между шлюзом приложения hello и hello серверной части веб-серверов будет осуществляться по протоколу http.</span><span class="sxs-lookup"><span data-stu-id="33c68-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="33c68-148">Любой клиент задней toohello связи, если инициировано по протоколу https будет возвращаться клиента toohello зашифрован.</span><span class="sxs-lookup"><span data-stu-id="33c68-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33c68-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33c68-149">Next steps</span></span>

<span data-ttu-id="33c68-150">toolearn tooconfigure пользовательские работоспособности проверки с помощью шлюза приложения Azure, в статье [создать пробу пользовательских работоспособности](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33c68-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
