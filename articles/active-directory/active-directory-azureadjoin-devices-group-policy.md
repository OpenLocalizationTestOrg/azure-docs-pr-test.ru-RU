---
title: "Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10 | Документация Майкрософт"
description: "Описание настройки групповой политики, которая позволяет присоединять устройства к домену в корпоративной сети."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="25a62-103">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="25a62-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="25a62-104">Организации уже более 15 лет используют присоединение к домену для подключения устройств.</span><span class="sxs-lookup"><span data-stu-id="25a62-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="25a62-105">Оно позволяет пользователям входить на устройства с помощью рабочих учетных записей Windows Server Active Directory (Active Directory), а ИТ-специалистам — полностью управлять этими устройствами.</span><span class="sxs-lookup"><span data-stu-id="25a62-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="25a62-106">Организации обычно полагаются на создание образов для подготовки устройств для пользователей и используют для управления ими System Center Configuration Manager (SCCM) или групповые политики.</span><span class="sxs-lookup"><span data-stu-id="25a62-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="25a62-107">Присоединение к домену в Windows 10 обеспечивает следующие преимущества после подключения устройств к Azure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="25a62-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="25a62-108">единый вход для доступа к ресурсам Azure AD из любого расположения;</span><span class="sxs-lookup"><span data-stu-id="25a62-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="25a62-109">доступ к корпоративному хранилищу Windows с помощью рабочих учетных записей (не требуется учетная запись Майкрософт);</span><span class="sxs-lookup"><span data-stu-id="25a62-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="25a62-110">перенос пользовательских параметров между устройствами, которые используют рабочую учетную запись (с соблюдением корпоративных требований; не требуется учетная запись Майкрософт);</span><span class="sxs-lookup"><span data-stu-id="25a62-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="25a62-111">строгая аутентификация и удобный вход с использованием рабочих или учебных учетных записей с помощью Windows Hello для бизнеса и Windows Hello;</span><span class="sxs-lookup"><span data-stu-id="25a62-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="25a62-112">возможность ограничить доступ только для устройств, соответствующих параметрам групповой политики устройств организации.</span><span class="sxs-lookup"><span data-stu-id="25a62-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25a62-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="25a62-113">Prerequisites</span></span>
<span data-ttu-id="25a62-114">Присоединение к домену доступно, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="25a62-114">Domain join continues to be useful.</span></span> <span data-ttu-id="25a62-115">Однако чтобы получить преимущества Azure AD в отношении единого входа, перемещения параметров с помощью рабочей учетной записи и доступа к Магазину Windows с рабочей учетной записью, потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="25a62-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="25a62-116">Подписка Azure AD</span><span class="sxs-lookup"><span data-stu-id="25a62-116">Azure AD subscription</span></span>
* <span data-ttu-id="25a62-117">Azure AD Connect для расширения локального каталога до Azure AD;</span><span class="sxs-lookup"><span data-stu-id="25a62-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="25a62-118">политика, настроенная для подключения к Azure AD устройств, присоединенных к домену;</span><span class="sxs-lookup"><span data-stu-id="25a62-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="25a62-119">сборка Windows 10 (сборка 10551 или более поздней версии) для устройств.</span><span class="sxs-lookup"><span data-stu-id="25a62-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="25a62-120">Для включения Windows Hello для бизнеса и Windows Hello вам также потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="25a62-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="25a62-121">**инфраструктура открытых ключей (PKI)** для выдачи сертификатов пользователей;</span><span class="sxs-lookup"><span data-stu-id="25a62-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="25a62-122">**System Center Configuration Manager (текущая версия)**. Необходимо установить версию 1606 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="25a62-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="25a62-123">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="25a62-123">For more information, see:</span></span> 
    - [<span data-ttu-id="25a62-124">Документация по System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="25a62-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="25a62-125">Блог команды разработчиков Microsoft System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="25a62-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="25a62-126">Параметры Windows Hello для бизнеса с помощью System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="25a62-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="25a62-127">В качестве альтернативы для требования развертывания PKI можно реализовать следующую конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="25a62-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="25a62-128">Несколько контроллеров домена с доменными службами Active Directory Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="25a62-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="25a62-129">Для включения условного доступа можно создать параметры групповой политики, разрешающие доступ к присоединенным к домену устройствам без дополнительных развертываний.</span><span class="sxs-lookup"><span data-stu-id="25a62-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="25a62-130">Для управления доступом в зависимости от соответствия устройства требованиям необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="25a62-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="25a62-131">Текущая версия System Center Configuration Manager (1606 и выше) для сценариев Windows Hello для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="25a62-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="25a62-132">Инструкции по развертыванию</span><span class="sxs-lookup"><span data-stu-id="25a62-132">Deployment instructions</span></span>

<span data-ttu-id="25a62-133">Инструкции по развертыванию см. в статье [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="25a62-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="25a62-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25a62-134">Next step</span></span>
* [<span data-ttu-id="25a62-135">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="25a62-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="25a62-136">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25a62-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="25a62-137">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="25a62-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="25a62-138">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="25a62-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="25a62-139">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="25a62-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

