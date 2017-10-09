---
title: "возникает tooAzure aaaConnect устройств, присоединенных к домену AD для Windows 10 | Документы Microsoft"
description: "Объясняет, как администраторы могут настроить групповую политику tooenable устройств toobe домену toohello корпоративной сети."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="1c982-103">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="1c982-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="1c982-104">Присоединение к домену — организаций hello традиционным способом подключения устройств для работы по hello последние 15 лет и многое другое.</span><span class="sxs-lookup"><span data-stu-id="1c982-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="1c982-105">Включил toosign пользователей в tootheir устройств с помощью своей работы Windows Server Active Directory (Active Directory) или учебных учетных записей и разрешенных toofully ИТ управлять этими устройствами.</span><span class="sxs-lookup"><span data-stu-id="1c982-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="1c982-106">Организациям обычно полагаются на toousers устройств tooprovision методы создания образа и обычно используют System Center Configuration Manager (SCCM) или групповой политики toomanage их.</span><span class="sxs-lookup"><span data-stu-id="1c982-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="1c982-107">Присоединение к домену, в Windows 10 предоставляет следующие преимущества, после подключения устройства tooAzure Active Directory (Azure AD) hello:</span><span class="sxs-lookup"><span data-stu-id="1c982-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="1c982-108">Единого входа (SSO) tooAzure AD ресурсам из любого места</span><span class="sxs-lookup"><span data-stu-id="1c982-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="1c982-109">Доступ к toohello корпоративного магазина Windows с помощью рабочих или школьные учетные записи (не требуется учетная запись Майкрософт)</span><span class="sxs-lookup"><span data-stu-id="1c982-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="1c982-110">перенос пользовательских параметров между устройствами, которые используют рабочую учетную запись (с соблюдением корпоративных требований; не требуется учетная запись Майкрософт);</span><span class="sxs-lookup"><span data-stu-id="1c982-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="1c982-111">строгая аутентификация и удобный вход с использованием рабочих или учебных учетных записей с помощью Windows Hello для бизнеса и Windows Hello;</span><span class="sxs-lookup"><span data-stu-id="1c982-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="1c982-112">Возможность toorestrict доступ только toodevices, совместимых с параметрами групповой политики организации устройства</span><span class="sxs-lookup"><span data-stu-id="1c982-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c982-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1c982-113">Prerequisites</span></span>
<span data-ttu-id="1c982-114">Присоединение к домену продолжается toobe полезно.</span><span class="sxs-lookup"><span data-stu-id="1c982-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="1c982-115">Однако tooget hello Azure AD преимущества единого входа, перемещаемых параметров с работать или школьные учетные записи и получить доступ к хранилищу tooWindows с рабочие или школьные учетные записи, вы должны будете hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1c982-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="1c982-116">Подписка Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c982-116">Azure AD subscription</span></span>
* <span data-ttu-id="1c982-117">Azure AD Connect tooextend hello локального каталога tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="1c982-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="1c982-118">Политики, которое задано tooAzure tooconnect устройств, присоединенных к домену AD</span><span class="sxs-lookup"><span data-stu-id="1c982-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="1c982-119">сборка Windows 10 (сборка 10551 или более поздней версии) для устройств.</span><span class="sxs-lookup"><span data-stu-id="1c982-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="1c982-120">tooenable Windows Hello для бизнеса и Windows Hello, необходимо также hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1c982-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="1c982-121">**инфраструктура открытых ключей (PKI)** для выдачи сертификатов пользователей;</span><span class="sxs-lookup"><span data-stu-id="1c982-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="1c982-122">**Текущей ветви System Center Configuration Manager** -требуется tooinstall версии 1606 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="1c982-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="1c982-123">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="1c982-123">For more information, see:</span></span> 
    - [<span data-ttu-id="1c982-124">Документация по System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1c982-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="1c982-125">Блог команды разработчиков Microsoft System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1c982-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="1c982-126">Параметры Windows Hello для бизнеса с помощью System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1c982-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="1c982-127">Как альтернативный toohello требование развертывания PKI, можно сделать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1c982-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="1c982-128">Несколько контроллеров домена с доменными службами Active Directory Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1c982-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="1c982-129">tooenable условного доступа, можно создать параметры групповой политики, позволяющие доступа к устройствам, присоединенным toodomain с нет дополнительные развертывания.</span><span class="sxs-lookup"><span data-stu-id="1c982-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="1c982-130">toomanage управление доступом на основе соответствия устройства hello, вам потребуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1c982-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="1c982-131">Текущая версия System Center Configuration Manager (1606 и выше) для сценариев Windows Hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="1c982-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="1c982-132">Инструкции по развертыванию</span><span class="sxs-lookup"><span data-stu-id="1c982-132">Deployment instructions</span></span>

<span data-ttu-id="1c982-133">toodeploy, повторите шаги hello, перечисленных в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="1c982-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="1c982-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c982-134">Next step</span></span>
* [<span data-ttu-id="1c982-135">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="1c982-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="1c982-136">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c982-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="1c982-137">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c982-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="1c982-138">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="1c982-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="1c982-139">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c982-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

