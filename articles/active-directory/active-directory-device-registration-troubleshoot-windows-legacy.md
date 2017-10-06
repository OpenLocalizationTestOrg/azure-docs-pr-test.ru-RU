---
title: "aaaTroubleshooting hello автоматической регистрации Azure AD домена компьютеров, присоединенных к для клиентов нижнего уровня Windows | Документы Microsoft"
description: "Устранение неполадок hello функции автоматической регистрации Azure AD домена компьютеров, присоединенных к для клиентов нижнего уровня Windows."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="2bc10-103">Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD для клиентов нижнего уровня Windows</span><span class="sxs-lookup"><span data-stu-id="2bc10-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="2bc10-104">Этот раздел является применимо только toohello следующих клиентов:</span><span class="sxs-lookup"><span data-stu-id="2bc10-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="2bc10-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="2bc10-105">Windows 7</span></span> 
- <span data-ttu-id="2bc10-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="2bc10-106">Windows 8.1</span></span> 
- <span data-ttu-id="2bc10-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="2bc10-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="2bc10-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2bc10-108">Windows Server 2012</span></span> 
- <span data-ttu-id="2bc10-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2bc10-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="2bc10-110">Windows 10 или Windows Server 2016 см. в разделе [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="2bc10-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="2bc10-111">В этом разделе предполагается, что функции автоматической регистрации устройств, присоединенных к домену, перечисленные в описано в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2bc10-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="2bc10-112">Этот раздел содержит рекомендации по каким образом tooresolve потенциальные проблемы устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2bc10-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="2bc10-113">Toonote некоторые действия для успешного результатов:</span><span class="sxs-lookup"><span data-stu-id="2bc10-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="2bc10-114">Регистрация клиентов в Azure AD выполняется для каждого пользователя или устройства.</span><span class="sxs-lookup"><span data-stu-id="2bc10-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="2bc10-115">Например: Если jdoe и jharnett входа в систему устройства toothis отдельной регистрации (DeviceID) создается для каждого пользователя на вкладке сведения пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="2bc10-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="2bc10-116">Регистрации из этих клиентов стандартной hello является настроенным tootry при входе или заблокировать или разблокировать и возможна задержка 5 минут, что это должно запускаться с помощью задачи планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="2bc10-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="2bc10-117">Повторно установите hello операционной системы или вручную отменить регистрацию и повторно зарегистрировать может создать новую регистрацию в Azure AD, появится несколько записей в разделе вкладка сведений пользователя hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2bc10-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="2bc10-118">Шаг 1: Получить состояние регистрации hello</span><span class="sxs-lookup"><span data-stu-id="2bc10-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="2bc10-119">**Состояние регистрации hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="2bc10-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="2bc10-120">Привет открыть командную строку с правами администратора</span><span class="sxs-lookup"><span data-stu-id="2bc10-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="2bc10-121">Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.</span><span class="sxs-lookup"><span data-stu-id="2bc10-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="2bc10-122">Эта команда отображает диалоговое окно, предоставляет дополнительные сведения о состоянии соединения hello.</span><span class="sxs-lookup"><span data-stu-id="2bc10-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="2bc10-124">Шаг 2: Оценка hello состояние регистрации</span><span class="sxs-lookup"><span data-stu-id="2bc10-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="2bc10-125">Если hello соединения не прошла успешно, диалоговое окно «hello» предоставляет сведения о возникшей проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="2bc10-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="2bc10-126">**приведены наиболее часто возникающих проблем Hello.**</span><span class="sxs-lookup"><span data-stu-id="2bc10-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="2bc10-127">Службы федерации Active Directory или служба Azure AD настроены неправильно</span><span class="sxs-lookup"><span data-stu-id="2bc10-127">A misconfigured AD FS or Azure AD</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="2bc10-129">Вы не вошли в качестве пользователя домена</span><span class="sxs-lookup"><span data-stu-id="2bc10-129">You are not signed on as a domain user</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="2bc10-131">Достигнут предел квоты</span><span class="sxs-lookup"><span data-stu-id="2bc10-131">A quota has been reached</span></span>

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="2bc10-133">Hello служба не отвечает</span><span class="sxs-lookup"><span data-stu-id="2bc10-133">hello service is not responding</span></span> 

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="2bc10-135">Сведения о состоянии hello также можно найти в журнале событий hello **приложений и служб Log\Microsoft — присоединение к**.</span><span class="sxs-lookup"><span data-stu-id="2bc10-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="2bc10-136">**наиболее распространенные причины сбоя регистрации Hello**</span><span class="sxs-lookup"><span data-stu-id="2bc10-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="2bc10-137">Отсутствует на компьютере hello внутренней сети организации или виртуальная частная сеть без подключения tooan локального контроллера домена AD.</span><span class="sxs-lookup"><span data-stu-id="2bc10-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="2bc10-138">Вы вошли на компьютер tooyour с учетной записью локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="2bc10-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="2bc10-139">Проблемы конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="2bc10-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="2bc10-140">Hello сервера федерации была настроенных toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="2bc10-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="2bc10-141">Отсутствует точка подключения службы объект, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello.</span><span class="sxs-lookup"><span data-stu-id="2bc10-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="2bc10-142">Пользователь достиг предела hello устройств.</span><span class="sxs-lookup"><span data-stu-id="2bc10-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="2bc10-143">Прочитайте статью "Знакомство с регистрацией устройств в Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="2bc10-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bc10-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bc10-144">Next steps</span></span>

<span data-ttu-id="2bc10-145">Дополнительные сведения см. в разделе hello [автоматической регистрации устройств вопросы и ответы](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="2bc10-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
