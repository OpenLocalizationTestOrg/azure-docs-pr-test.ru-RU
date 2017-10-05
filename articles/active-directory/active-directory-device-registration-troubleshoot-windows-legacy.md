---
title: "Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для клиентов Windows нижнего уровня | Документация Майкрософт"
description: "Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для клиентов Windows нижнего уровня."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="18768-103">Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для клиентов Windows нижнего уровня</span><span class="sxs-lookup"><span data-stu-id="18768-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="18768-104">Это руководство касается только следующих клиентов:</span><span class="sxs-lookup"><span data-stu-id="18768-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="18768-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="18768-105">Windows 7</span></span> 
- <span data-ttu-id="18768-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="18768-106">Windows 8.1</span></span> 
- <span data-ttu-id="18768-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="18768-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="18768-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="18768-108">Windows Server 2012</span></span> 
- <span data-ttu-id="18768-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="18768-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="18768-110">Сведения о Windows 10 или Windows Server 2016 см. в статье [Устранение неполадок автоматической регистрации присоединенных к домену Azure AD компьютеров для Windows 10 и Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="18768-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="18768-111">В этом руководстве предполагается, что вы настроили автоматическую регистрацию присоединенных к домену устройств в соответствии со сведениями, указанными в статье [Настройка автоматической регистрации присоединенных к домену устройств Windows в Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18768-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="18768-112">В этом руководстве содержатся рекомендации по устранению неполадок для решения потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="18768-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="18768-113">Чтобы получить успешный результат, обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="18768-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="18768-114">Регистрация клиентов в Azure AD выполняется для каждого пользователя или устройства.</span><span class="sxs-lookup"><span data-stu-id="18768-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="18768-115">Например, если jdoe и jharnett войдут в устройство, в таблице сведений о пользователе для каждого из них будет создана отдельная регистрация (DeviceID).</span><span class="sxs-lookup"><span data-stu-id="18768-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="18768-116">Регистрация клиентов по умолчанию выполняется при входе или блокировке либо разблокировке. Эта операция может активироваться с помощью задачи планировщика задач с 5-минутной задержкой.</span><span class="sxs-lookup"><span data-stu-id="18768-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="18768-117">При переустановке операционной системы или отмене регистрации либо повторной регистрации вручную в Azure AD может быть создана новая регистрация. Из-за этого в таблице сведений о пользователе на портале Azure появится несколько записей.</span><span class="sxs-lookup"><span data-stu-id="18768-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="18768-118">Шаг 1. Получение сведений о состоянии регистрации</span><span class="sxs-lookup"><span data-stu-id="18768-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="18768-119">**Чтобы проверить сведения о состоянии регистрации, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="18768-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="18768-120">Запустите командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="18768-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="18768-121">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="18768-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="18768-122">Эта команда отображает диалоговое окно, содержащее дополнительные сведения о состоянии присоединения.</span><span class="sxs-lookup"><span data-stu-id="18768-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="18768-124">Шаг 2. Анализ сведений о состоянии регистрации</span><span class="sxs-lookup"><span data-stu-id="18768-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="18768-125">Если не удалось выполнить присоединение, в диалоговом окне появятся подробные сведения о возникшей проблеме.</span><span class="sxs-lookup"><span data-stu-id="18768-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="18768-126">**Ниже перечислены наиболее распространенные проблемы.**</span><span class="sxs-lookup"><span data-stu-id="18768-126">**The most common issues are:**</span></span>

- <span data-ttu-id="18768-127">Службы федерации Active Directory или служба Azure AD настроены неправильно</span><span class="sxs-lookup"><span data-stu-id="18768-127">A misconfigured AD FS or Azure AD</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="18768-129">Вы не вошли в качестве пользователя домена</span><span class="sxs-lookup"><span data-stu-id="18768-129">You are not signed on as a domain user</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="18768-131">Достигнут предел квоты</span><span class="sxs-lookup"><span data-stu-id="18768-131">A quota has been reached</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="18768-133">Служба не отвечает</span><span class="sxs-lookup"><span data-stu-id="18768-133">The service is not responding</span></span> 

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="18768-135">Сведения о состоянии можно также найти в журнале событий в разделе **Applications and Services Log\Microsoft-Workplace Join** (Журнал приложений и служб > Microsoft — присоединение к рабочей области).</span><span class="sxs-lookup"><span data-stu-id="18768-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="18768-136">**Ниже перечислены основные причины сбоя регистрации.**</span><span class="sxs-lookup"><span data-stu-id="18768-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="18768-137">Компьютер может быть не подключен к внутренней сети организации или к VPN без подключения к локальному контроллеру домена AD.</span><span class="sxs-lookup"><span data-stu-id="18768-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="18768-138">Вы вошли в систему с помощью учетной записи локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="18768-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="18768-139">Проблемы конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="18768-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="18768-140">сервер федерации настроен для поддержки **WIAORMULTIAUTHN**;</span><span class="sxs-lookup"><span data-stu-id="18768-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="18768-141">нет объекта точки подключения службы, указывающего на имя проверенного домена в Azure AD в лесу AD, к которому относится компьютер;</span><span class="sxs-lookup"><span data-stu-id="18768-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="18768-142">пользователь достиг предела подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="18768-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="18768-143">Прочитайте статью "Знакомство с регистрацией устройств в Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="18768-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18768-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18768-144">Next steps</span></span>

<span data-ttu-id="18768-145">Дополнительные сведения см. в статье [Automatic device registration FAQ](active-directory-device-registration-faq.md) (Часто задаваемые вопросы об автоматической регистрации устройств)</span><span class="sxs-lookup"><span data-stu-id="18768-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
