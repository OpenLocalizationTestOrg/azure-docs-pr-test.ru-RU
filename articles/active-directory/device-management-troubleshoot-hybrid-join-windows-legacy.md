---
title: "старых устройств, присоединенных к aaaTroubleshooting гибридной Azure Active Directory | Документы Microsoft"
description: "Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="74a27-103">Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74a27-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="74a27-104">Этот раздел является применимо только toohello следующих устройств:</span><span class="sxs-lookup"><span data-stu-id="74a27-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="74a27-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="74a27-105">Windows 7</span></span> 
- <span data-ttu-id="74a27-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="74a27-106">Windows 8.1</span></span> 
- <span data-ttu-id="74a27-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="74a27-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="74a27-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="74a27-108">Windows Server 2012</span></span> 
- <span data-ttu-id="74a27-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="74a27-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="74a27-110">Сведения об устройствах под управлением Windows 10 и Windows Server 2016 см. в статье [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md) (Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="74a27-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="74a27-111">В этом разделе предполагается, что [устройств, присоединенных к настроенным гибридной Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="74a27-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="74a27-112">Условный доступ на основе устройств</span><span class="sxs-lookup"><span data-stu-id="74a27-112">Device-based conditional access</span></span>

- [<span data-ttu-id="74a27-113">Корпоративное перемещение параметров</span><span class="sxs-lookup"><span data-stu-id="74a27-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="74a27-114">Настройка Windows Hello для бизнеса</span><span class="sxs-lookup"><span data-stu-id="74a27-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="74a27-115">Этот раздел содержит рекомендации по каким образом tooresolve потенциальные проблемы устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="74a27-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="74a27-116">**Важная информация**</span><span class="sxs-lookup"><span data-stu-id="74a27-116">**What you should know:**</span></span> 

- <span data-ttu-id="74a27-117">Hello максимальное число устройств на пользователя будет состоять из устройства.</span><span class="sxs-lookup"><span data-stu-id="74a27-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="74a27-118">Например если *jdoe* и *jharnett* tooa входа в устройство, отдельные регистрации (DeviceID) создается для каждого из них в hello **пользователя** вкладка «сведения».</span><span class="sxs-lookup"><span data-stu-id="74a27-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="74a27-119">Здравствуйте, начальная регистрация / join устройств настроенных tooperform попытка входа в систему или блокировки или разблокировки.</span><span class="sxs-lookup"><span data-stu-id="74a27-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="74a27-120">Возможна 5-минутная задержка, связанная с выполнением задачи планировщика задач.</span><span class="sxs-lookup"><span data-stu-id="74a27-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="74a27-121">Переустановка hello операционную систему или вручную отменить регистрацию и повторно зарегистрируйте может создать новую регистрацию в Azure AD и результаты в несколько записей в списке Вкладка сведений пользователя hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="74a27-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="74a27-122">Шаг 1: Получить состояние регистрации hello</span><span class="sxs-lookup"><span data-stu-id="74a27-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="74a27-123">**Состояние регистрации hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="74a27-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="74a27-124">Привет открыть командную строку с правами администратора</span><span class="sxs-lookup"><span data-stu-id="74a27-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="74a27-125">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="74a27-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="74a27-126">Эта команда отображает диалоговое окно, предоставляет дополнительные сведения о состоянии соединения hello.</span><span class="sxs-lookup"><span data-stu-id="74a27-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="74a27-128">Шаг 2: Оценка состояние соединения Azure AD гибридного hello</span><span class="sxs-lookup"><span data-stu-id="74a27-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="74a27-129">Если hello гибридной Azure AD соединения не прошла успешно, диалоговое окно «hello» предоставляет сведения о возникшей проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="74a27-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="74a27-130">**приведены наиболее часто возникающих проблем Hello.**</span><span class="sxs-lookup"><span data-stu-id="74a27-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="74a27-131">Службы федерации Active Directory или служба Azure AD настроены неправильно</span><span class="sxs-lookup"><span data-stu-id="74a27-131">A misconfigured AD FS or Azure AD</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="74a27-133">Вы не вошли в качестве пользователя домена</span><span class="sxs-lookup"><span data-stu-id="74a27-133">You are not signed on as a domain user</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="74a27-135">Достигнут предел квоты</span><span class="sxs-lookup"><span data-stu-id="74a27-135">A quota has been reached</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="74a27-137">Hello служба не отвечает</span><span class="sxs-lookup"><span data-stu-id="74a27-137">hello service is not responding</span></span> 

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="74a27-139">Сведения о состоянии hello также можно найти в журнале событий hello **приложений и служб Log\Microsoft — присоединение к**.</span><span class="sxs-lookup"><span data-stu-id="74a27-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="74a27-140">**наиболее распространенными причинами сбоя гибридное соединение Azure AD для Hello являются:**</span><span class="sxs-lookup"><span data-stu-id="74a27-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="74a27-141">Отсутствует на компьютере hello внутренней сети организации или виртуальная частная сеть без подключения tooan локального контроллера домена AD.</span><span class="sxs-lookup"><span data-stu-id="74a27-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="74a27-142">Вы вошли на компьютер tooyour с учетной записью локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="74a27-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="74a27-143">Проблемы конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="74a27-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="74a27-144">Hello сервера федерации была настроенных toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="74a27-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="74a27-145">Отсутствует точка подключения службы объект, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello.</span><span class="sxs-lookup"><span data-stu-id="74a27-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="74a27-146">Пользователь достиг предела hello устройств.</span><span class="sxs-lookup"><span data-stu-id="74a27-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="74a27-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74a27-147">Next steps</span></span>

<span data-ttu-id="74a27-148">Ответы на вопросы см hello [управление устройствами вопросы и ответы](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="74a27-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
