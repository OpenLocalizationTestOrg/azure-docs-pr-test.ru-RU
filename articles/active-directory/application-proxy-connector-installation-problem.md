---
title: "Проблема при установке соединителя агента прокси приложения | Документы Майкрософт"
description: "Устранение проблем при установке соединителя агента прокси приложения"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="963d7-103">Проблема при установке соединителя агента прокси приложения</span><span class="sxs-lookup"><span data-stu-id="963d7-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="963d7-104">Соединитель прокси приложения Microsoft AAD — это внутренний компонент домена, использующий исходящие соединения для установки подключения из конечной точки в облаке к внутреннему домену.</span><span class="sxs-lookup"><span data-stu-id="963d7-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="963d7-105">Общие проблемные области при установке соединителя</span><span class="sxs-lookup"><span data-stu-id="963d7-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="963d7-106">При сбое установки соединителя первопричина обычно относится к одной из следующих областей:</span><span class="sxs-lookup"><span data-stu-id="963d7-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="963d7-107">**Подключение** — для успешной установки новому соединителю нужно зарегистрироваться и установить свойства доверия.</span><span class="sxs-lookup"><span data-stu-id="963d7-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="963d7-108">Это осуществляется путем подключения к облачной службе прокси приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="963d7-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="963d7-109">**Установление отношений доверия** — новый соединитель создает самозаверяющий сертификат и регистрируется в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="963d7-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="963d7-110">**Проверка подлинности администратора** — для завершения установки соединителя пользователю нужно предоставить учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="963d7-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="963d7-111">Проверка подключения к прокси-службе облачного приложения и странице входа Майкрософт</span><span class="sxs-lookup"><span data-stu-id="963d7-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="963d7-112">**Цель:** убедитесь, что компьютер соединителя может подключиться к конечной точке регистрации прокси приложения AAD, а также к странице входа Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="963d7-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="963d7-113">Откройте браузер, перейдите к веб-странице <https://aadap-portcheck.connectorporttest.msappproxy.net> и проверьте наличие связи с центрами обработки данных в центральной и восточной частях США с портами 9090 и 9091.</span><span class="sxs-lookup"><span data-stu-id="963d7-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="963d7-114">Если подключение к любому из этих портов не установлено (не отображается зеленая галочка), убедитесь, что в брандмауэре или на внутреннем прокси-сервере правильно определен \*.msappproxy.net с портами 9090 и 9091.</span><span class="sxs-lookup"><span data-stu-id="963d7-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="963d7-115">Откройте браузер (отдельную вкладку), перейдите к веб-странице <https://login.microsoftonline.com> и убедитесь, что можете войти на эту страницу.</span><span class="sxs-lookup"><span data-stu-id="963d7-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="963d7-116">Проверка того, поддерживают ли внутренние компоненты и компьютер сертификат доверия прокси приложения</span><span class="sxs-lookup"><span data-stu-id="963d7-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="963d7-117">**Цель:** убедитесь, что компьютер соединителя, внутренний прокси-сервер и брандмауэр поддерживают сертификат, созданный соединителем для будущих отношений доверия.</span><span class="sxs-lookup"><span data-stu-id="963d7-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="963d7-118">Соединитель пытается создать сертификат SHA512, поддерживаемый TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="963d7-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="963d7-119">Если компьютер или внутренний серверный брандмауэр и прокси-сервер не поддерживают TLS1.2, происходит сбой установки.</span><span class="sxs-lookup"><span data-stu-id="963d7-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="963d7-120">**Устранение проблемы:**</span><span class="sxs-lookup"><span data-stu-id="963d7-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="963d7-121">Убедитесь, что компьютер поддерживает TLS1.2. Для этого требуется версия Windows после 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="963d7-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="963d7-122">Если компьютер соединителя относится к версии 2012 R2 или более ранней, убедитесь, что на нем установлены следующие пакеты обновления: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="963d7-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="963d7-123">Обратитесь к администратору сети и попросите убедиться, что внутренний прокси-сервер и брандмауэр не блокируют SHA512 для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="963d7-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="963d7-124">Проверка прав администратора у пользователя, устанавливающего соединитель</span><span class="sxs-lookup"><span data-stu-id="963d7-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="963d7-125">**Цель:** убедитесь, что пользователь, пытающийся установить соединитель, является администратором с подходящими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="963d7-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="963d7-126">Сейчас для успешной установки пользователь должен быть глобальным администратором.</span><span class="sxs-lookup"><span data-stu-id="963d7-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="963d7-127">**Проверка правильности учетных данных:**</span><span class="sxs-lookup"><span data-stu-id="963d7-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="963d7-128">Подключитесь к <https://login.microsoftonline.com> и используйте те же учетные данные.</span><span class="sxs-lookup"><span data-stu-id="963d7-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="963d7-129">Убедитесь, что вход прошел успешно.</span><span class="sxs-lookup"><span data-stu-id="963d7-129">Make sure the login is successful.</span></span> <span data-ttu-id="963d7-130">Вы можете проверить роль пользователя, перейдя в раздел **Azure Active Directory** -&gt; **Пользователи и группы** -&gt; **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="963d7-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="963d7-131">Выберите свою учетную запись пользователя и затем "Роль каталога" в появившемся меню.</span><span class="sxs-lookup"><span data-stu-id="963d7-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="963d7-132">Убедитесь, что выбрана роль "Глобальный администратор".</span><span class="sxs-lookup"><span data-stu-id="963d7-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="963d7-133">Если вам не удается открыть какие-либо страницы из описанных действий, вы не являетесь глобальным администратором.</span><span class="sxs-lookup"><span data-stu-id="963d7-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="963d7-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="963d7-134">Next steps</span></span>
[<span data-ttu-id="963d7-135">Сведения о соединителях прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="963d7-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
