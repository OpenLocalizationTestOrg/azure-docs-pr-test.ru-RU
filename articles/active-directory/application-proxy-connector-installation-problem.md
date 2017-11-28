---
title: "Установка aaaProblem hello соединитель агента прокси приложения | Документы Microsoft"
description: "Как tootroubleshoot проблемы вы может hello лицевой стороны, при установке соединителя агента прокси-сервера приложений"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="b93d3-103">Проблемы с установкой hello соединитель агента прокси приложения</span><span class="sxs-lookup"><span data-stu-id="b93d3-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="b93d3-104">Microsoft AAD Application Proxy Connector — это компонент внутреннего домена, который использует подключение hello tooestablish исходящие подключения из внутреннего домена доступную конечную точку облака toohello hello.</span><span class="sxs-lookup"><span data-stu-id="b93d3-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="b93d3-105">Общие проблемные области при установке соединителя</span><span class="sxs-lookup"><span data-stu-id="b93d3-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="b93d3-106">При сбое установки hello соединителя, hello корневой причиной обычно является одним из следующих областей hello:</span><span class="sxs-lookup"><span data-stu-id="b93d3-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="b93d3-107">**Подключение** — toocomplete успешной установке hello tooregister потребностей нового соединителя и устанавливать свойства будущих отношений доверия.</span><span class="sxs-lookup"><span data-stu-id="b93d3-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="b93d3-108">Это делается путем подключения toohello облачной службы прокси приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="b93d3-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="b93d3-109">**Установление доверия** — новый соединитель hello создает самозаверяющий сертификат и регистрирует toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b93d3-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="b93d3-110">**Проверка подлинности Здравствуйте, администратор** — во время установки hello пользователь должен предоставить учетные данные администратора установки соединителя toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="b93d3-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="b93d3-111">Проверка подключения toohello прокси приложения облачной службы и страницы входа Microsoft</span><span class="sxs-lookup"><span data-stu-id="b93d3-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="b93d3-112">**Цель:** проверки возможности подключения этого компьютера соединителя hello toohello конечной точке регистрации прокси-сервер приложения AAD, а также страницы входа Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b93d3-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="b93d3-113">Откройте браузер и перейдите toohello, следующие веб-страницы: <https://aadap-portcheck.connectorporttest.msappproxy.net> и убедитесь, что tooCentral подключения hello США и работа Восток США центрах обработки данных с портами 9090 и 9091.</span><span class="sxs-lookup"><span data-stu-id="b93d3-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="b93d3-114">Если любой из этих портов не обнаруживаются (нет зеленым флажком), убедитесь, что hello брандмауэра или прокси-сервера базы данных имеет \*. msappproxy.net с портами 9090 и 9091 правильно определен.</span><span class="sxs-lookup"><span data-stu-id="b93d3-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="b93d3-115">Откройте браузер (вкладка «отдельный») и перейдите toohello следующие веб-страницы: <https://login.microsoftonline.com>, убедитесь в том, что можно выполнить вход toothat страницы.</span><span class="sxs-lookup"><span data-stu-id="b93d3-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="b93d3-116">Проверка того, поддерживают ли внутренние компоненты и компьютер сертификат доверия прокси приложения</span><span class="sxs-lookup"><span data-stu-id="b93d3-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="b93d3-117">**Цель:** убедитесь, что соединитель машины hello, внутреннего прокси-сервера и брандмауэра поддерживает hello сертификат, созданный соединитель hello для будущих отношений доверия.</span><span class="sxs-lookup"><span data-stu-id="b93d3-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="b93d3-118">Соединитель Hello предпринимает toocreate cert SHA512, который поддерживается модулем TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="b93d3-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="b93d3-119">Если машины hello или hello серверный брандмауэр и прокси-сервера не поддерживает TLS1.2, сбой установки hello.</span><span class="sxs-lookup"><span data-stu-id="b93d3-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="b93d3-120">**проблема tooresolve hello.**</span><span class="sxs-lookup"><span data-stu-id="b93d3-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="b93d3-121">Проверьте TLS1.2 поддерживает hello компьютер — все версии Windows после 2012 R2 следует поддерживают TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="b93d3-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="b93d3-122">Ли соединитель компьютере версии 2012 R2 или prior, убедитесь в том, что hello статьи базы знаний установлена на машине hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="b93d3-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="b93d3-123">Обратитесь к администратору сети и попросите tooverify что hello внутреннего прокси-сервера и брандмауэра не блокируют SHA512 для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b93d3-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="b93d3-124">Убедитесь, что администратор соединителя используется tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="b93d3-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="b93d3-125">**Цель:** убедитесь hello пользователя, который пытается tooinstall hello соединитель является администратором с правильными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="b93d3-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="b93d3-126">В настоящее время hello пользователь должен быть глобальным администратором для установки toosucceed hello.</span><span class="sxs-lookup"><span data-stu-id="b93d3-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="b93d3-127">**используются правильные учетные данные tooverify hello:**</span><span class="sxs-lookup"><span data-stu-id="b93d3-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="b93d3-128">Подключение слишком<https://login.microsoftonline.com> и использование hello одинаковые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b93d3-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="b93d3-129">Убедитесь, что hello вход выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="b93d3-129">Make sure hello login is successful.</span></span> <span data-ttu-id="b93d3-130">Роль пользователя hello можно проверить, происходит слишком**Azure Active Directory**  - &gt; **пользователей и групп**  - &gt; **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b93d3-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="b93d3-131">Выберите учетную запись пользователя, а затем «роли каталога» в итоговом меню hello.</span><span class="sxs-lookup"><span data-stu-id="b93d3-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="b93d3-132">Убедитесь что hello выбранную роль «Глобальный администратор».</span><span class="sxs-lookup"><span data-stu-id="b93d3-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="b93d3-133">Если не удается tooaccess любой hello страницы вместе эти действия, вы не глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="b93d3-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b93d3-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b93d3-134">Next steps</span></span>
[<span data-ttu-id="b93d3-135">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="b93d3-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
