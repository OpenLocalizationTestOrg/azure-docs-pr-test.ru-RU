---
title: "Присоединение личного устройства к своей организации | Документация Майкрософт"
description: "Поясняет, как пользователи могут регистрировать свои персональные устройства Windows 10 в корпоративной сети, а также шаги по развертыванию для сценария BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="1cb40-103">Присоединение личного устройства к своей организации</span><span class="sxs-lookup"><span data-stu-id="1cb40-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="1cb40-104">Присоединение личного устройства с Windows 10 к своей организации</span><span class="sxs-lookup"><span data-stu-id="1cb40-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="1cb40-105">В меню **Пуск** выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="1cb40-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="1cb40-106">Выберите пункт **Учетные записи**, а затем нажмите кнопку **Ваша учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="1cb40-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="1cb40-107">Выберите команду **Добавить рабочую или учебную учетную запись**и введите свою корпоративную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="1cb40-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="1cb40-108">На странице входа своей организации введите имя пользователя и пароль, затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1cb40-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="1cb40-109">Появится окно многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="1cb40-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="1cb40-110">(Этот запрос может настроить ИТ-администратор).</span><span class="sxs-lookup"><span data-stu-id="1cb40-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="1cb40-111">Azure Active Directory (Azure AD) проверяет, требует ли устройство регистрации в службе управления мобильными устройствами.</span><span class="sxs-lookup"><span data-stu-id="1cb40-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="1cb40-112">Windows регистрирует устройство в каталоге организации в Azure AD и в службе управления мобильными устройствами, если это уместно.</span><span class="sxs-lookup"><span data-stu-id="1cb40-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="1cb40-113">Если вы являетесь управляемым пользователем, Windows осуществляет переход на рабочий стол с помощью автоматического входа.</span><span class="sxs-lookup"><span data-stu-id="1cb40-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="1cb40-114">Если вы являетесь федеративным пользователем, то появится экран входа в Windows, где нужно будет ввести учетные данные.</span><span class="sxs-lookup"><span data-stu-id="1cb40-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="1cb40-115">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="1cb40-115">Additional information</span></span>
* [<span data-ttu-id="1cb40-116">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="1cb40-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="1cb40-117">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1cb40-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="1cb40-118">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="1cb40-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="1cb40-119">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="1cb40-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="1cb40-120">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="1cb40-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="1cb40-121">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="1cb40-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

