---
title: "Проверка подлинности Windows и сервер Многофакторной идентификации Azure | Документация Майкрософт"
description: "Это страница Azure Multi-Factor Authentication, которая будет полезна при развертывании проверки подлинности Windows и сервера Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="69554-103">Проверка подлинности Windows и сервер Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="69554-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="69554-104">Раздел проверки подлинности Windows сервера Многофакторной идентификации Azure позволяет включить и настроить проверку подлинности Windows для приложений.</span><span class="sxs-lookup"><span data-stu-id="69554-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="69554-105">Перед тем как настроить проверку подлинности Windows, обратите внимание на следующий список.</span><span class="sxs-lookup"><span data-stu-id="69554-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="69554-106">После завершения установки перезапустите Многофакторную идентификацию для служб терминалов, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="69554-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="69554-107">Если установлен флажок «Требуется сопоставление пользователей Multi-Factor Authentication» и вас нет в списке пользователей, после перезагрузки вы не сможете войти в систему.</span><span class="sxs-lookup"><span data-stu-id="69554-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="69554-108">Надежные IP-адреса зависят от того, может ли приложение предоставлять IP-адрес клиента с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="69554-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="69554-109">В настоящее время поддерживаются только службы терминалов.</span><span class="sxs-lookup"><span data-stu-id="69554-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="69554-110">Для обеспечения безопасности служб терминалов в Windows Server 2012 R2 эта функция не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="69554-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="69554-111">Для защиты приложения с помощью проверки подлинности Windows используйте следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="69554-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="69554-112">На сервере Многофакторной идентификации Azure щелкните значок проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="69554-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="69554-113">![Проверка подлинности Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="69554-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="69554-114">Установите флажок **Включить проверку подлинности Windows**.</span><span class="sxs-lookup"><span data-stu-id="69554-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="69554-115">По умолчанию этот флажок не установлен.</span><span class="sxs-lookup"><span data-stu-id="69554-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="69554-116">На вкладке «Приложения» администратор может настроить одно или несколько приложений для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="69554-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="69554-117">Выберите сервер или приложение — укажите, включен ли сервер или приложение.</span><span class="sxs-lookup"><span data-stu-id="69554-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="69554-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="69554-118">Click **OK**.</span></span>
5. <span data-ttu-id="69554-119">Щелкните **Добавить…**</span><span class="sxs-lookup"><span data-stu-id="69554-119">Click **Add…**</span></span>
6. <span data-ttu-id="69554-120">На вкладке «Надежные IP-адреса» можно пропустить Azure Multi-Factor Authentication для сеансов Windows с конкретных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="69554-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="69554-121">Например, если сотрудники используют приложение как в офисе, так и дома, то можно сделать так, чтобы их телефоны не звонили для службы Azure Multi-Factor Authentication, пока они находятся в офисе.</span><span class="sxs-lookup"><span data-stu-id="69554-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="69554-122">Для этого для офисной подсети установите значение «Надежные IP-адреса».</span><span class="sxs-lookup"><span data-stu-id="69554-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="69554-123">Щелкните **Добавить…**</span><span class="sxs-lookup"><span data-stu-id="69554-123">Click **Add…**</span></span>
8. <span data-ttu-id="69554-124">Выберите **один IP-адрес**, если необходимо пропустить один IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="69554-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="69554-125">Выберите **диапазон IP-адресов**, если необходимо пропустить целый диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="69554-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="69554-126">Пример: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="69554-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="69554-127">Выберите **подсеть**, если необходимо указать диапазон IP-адресов с помощью подсети.</span><span class="sxs-lookup"><span data-stu-id="69554-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="69554-128">Введите начальный IP-адрес подсети и выберите соответствующую маску сети в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="69554-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="69554-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="69554-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69554-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69554-130">Next steps</span></span>

- [<span data-ttu-id="69554-131">Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков</span><span class="sxs-lookup"><span data-stu-id="69554-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="69554-132">Включение расширения NPS для Многофакторной идентификации Azure (общедоступная предварительная версия) в существующую инфраструктуру аутентификации</span><span class="sxs-lookup"><span data-stu-id="69554-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
