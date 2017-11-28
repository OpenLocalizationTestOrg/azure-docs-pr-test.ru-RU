---
title: "aaaWindows проверки подлинности и сервера Azure MFA | Документы Microsoft"
description: "Это является hello Azure многофакторной проверки подлинности, будет полезен при развертывании проверки подлинности Windows и сервера Azure Multi-factor Authentication."
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
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="18900-103">Проверка подлинности Windows и сервер Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="18900-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="18900-104">Использовать проверку подлинности Windows hello раздел tooenable сервера Azure Multi-factor Authentication hello и настроить проверку подлинности Windows для приложений.</span><span class="sxs-lookup"><span data-stu-id="18900-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="18900-105">Перед тем как настроить проверку подлинности Windows, оставьте hello после списка в виду:</span><span class="sxs-lookup"><span data-stu-id="18900-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="18900-106">После завершения установки перезагрузите hello многофакторной проверки подлинности Azure для служб терминалов tootake эффекта.</span><span class="sxs-lookup"><span data-stu-id="18900-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="18900-107">Если установлен флажок «Требовать многофакторную проверку подлинности Azure сопоставление пользователей» и вы не hello список пользователей, нельзя будет toolog в машину hello после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="18900-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="18900-108">Надежные IP-адреса зависят от того, может ли приложение hello предоставлять hello IP-адрес клиента с проверкой подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="18900-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="18900-109">В настоящее время поддерживаются только службы терминалов.</span><span class="sxs-lookup"><span data-stu-id="18900-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="18900-110">Эта функция не поддерживается toosecure служб терминалов в Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18900-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="18900-111">toosecure приложения с проверкой подлинности Windows, hello используйте следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="18900-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="18900-112">В hello сервера Azure Multi-factor Authentication щелкните значок проверки подлинности Windows hello.</span><span class="sxs-lookup"><span data-stu-id="18900-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="18900-113">![Проверка подлинности Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="18900-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="18900-114">Проверьте hello **включить проверку подлинности Windows** флажок.</span><span class="sxs-lookup"><span data-stu-id="18900-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="18900-115">По умолчанию этот флажок не установлен.</span><span class="sxs-lookup"><span data-stu-id="18900-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="18900-116">Вкладка "приложения" Hello позволяет администратору tooconfigure hello одно или несколько приложений для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="18900-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="18900-117">Выберите сервер или приложение — укажите, включен ли hello сервер или приложение.</span><span class="sxs-lookup"><span data-stu-id="18900-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="18900-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="18900-118">Click **OK**.</span></span>
5. <span data-ttu-id="18900-119">Щелкните **Добавить…**</span><span class="sxs-lookup"><span data-stu-id="18900-119">Click **Add…**</span></span>
6. <span data-ttu-id="18900-120">Вкладка Hello надежных IP-адресов позволяет tooskip Azure многофакторной проверки подлинности для сеансов Windows с определенных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="18900-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="18900-121">Например если сотрудники используют приложение hello из офиса hello и из дома, можно, не требуется их отвечать на звонки многофакторной проверки подлинности в Azure во время hello office.</span><span class="sxs-lookup"><span data-stu-id="18900-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="18900-122">Для этого следует указать подсети hello office как операция надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="18900-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="18900-123">Щелкните **Добавить…**</span><span class="sxs-lookup"><span data-stu-id="18900-123">Click **Add…**</span></span>
8. <span data-ttu-id="18900-124">Выберите **один IP-адрес** при желании tooskip один IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="18900-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="18900-125">Выберите **диапазон IP-адресов** при желании tooskip весь диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="18900-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="18900-126">Пример: 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="18900-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="18900-127">Выберите **подсети** при желании toospecify диапазон IP-адресов в нотации подсети.</span><span class="sxs-lookup"><span data-stu-id="18900-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="18900-128">Введите начальный IP-адрес подсети hello и выберите соответствующую маску сети из раскрывающегося списка hello hello.</span><span class="sxs-lookup"><span data-stu-id="18900-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="18900-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="18900-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18900-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18900-130">Next steps</span></span>

- [<span data-ttu-id="18900-131">Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков</span><span class="sxs-lookup"><span data-stu-id="18900-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="18900-132">Расширить существующую инфраструктуру проверки подлинности с hello NPS расширения для многофакторной проверки Подлинности Azure</span><span class="sxs-lookup"><span data-stu-id="18900-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
