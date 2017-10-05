---
title: "Windows 10 для предприятия: использование устройств для работы | Документация Майкрософт"
description: "Общие сведения о развертывании устройств с Windows 10 для предприятий, а также об интеграции облачной среды Windows с Azure Active Directory. Описываются разные способы подготовки и использования устройства с помощью портала Azure."
keywords: "облако Windows, Windows в Azure Active Directory устройства Windows 10 в Azure, устройства Azure Windows"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="c2253-105">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="c2253-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="c2253-106">В Windows 10 реализована возможность интеграции с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2253-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c2253-107">Вы можете подключать к Azure AD устройства с Windows 10, чтобы пользователи могли входить в Windows, используя учетные записи Azure AD или добавляя идентификаторы Azure для получения доступа к ресурсам и бизнес-приложениям.</span><span class="sxs-lookup"><span data-stu-id="c2253-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory с облаком Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="c2253-109">Интеграция устройств Windows 10 с Azure Active Directory: карта содержимого</span><span class="sxs-lookup"><span data-stu-id="c2253-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="c2253-110">В следующих статьях описываются способы использования устройств с Windows 10 в организации.</span><span class="sxs-lookup"><span data-stu-id="c2253-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="c2253-111">Разделы</span><span class="sxs-lookup"><span data-stu-id="c2253-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="c2253-112">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c2253-112">Getting started</span></span> |[<span data-ttu-id="c2253-113">Устройства под управлением Windows 10 в вашей рабочей области</span><span class="sxs-lookup"><span data-stu-id="c2253-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="c2253-114">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2253-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="c2253-115">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="c2253-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="c2253-116">Развертывание</span><span class="sxs-lookup"><span data-stu-id="c2253-116">Deployment</span></span> |[<span data-ttu-id="c2253-117">Сценарии использования и рекомендации по развертыванию для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2253-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="c2253-118">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="c2253-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="c2253-119">Включение Microsoft Passport for Work в организации</span><span class="sxs-lookup"><span data-stu-id="c2253-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="c2253-120">Включение Enterprise State Roaming для Windows 10</span><span class="sxs-lookup"><span data-stu-id="c2253-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="c2253-121">Задачи пользователя</span><span class="sxs-lookup"><span data-stu-id="c2253-121">User tasks</span></span> |[<span data-ttu-id="c2253-122">Настройка нового устройства под управлением Windows 10 на работу с Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2253-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="c2253-123">Настройка устройства Windows 10 для работы с Azure AD через меню "Настройка"</span><span class="sxs-lookup"><span data-stu-id="c2253-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="c2253-124">Присоединение личного устройства к своей организации</span><span class="sxs-lookup"><span data-stu-id="c2253-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

