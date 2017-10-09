---
title: "Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory | Документация Майкрософт"
description: "Предоставляет список сообщений об ошибках из hello Azure Active Directory действия содержимого пакета и шаги toofix их."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="c2ec7-103">Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2ec7-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="c2ec7-104">При работе с hello пакет содержимого Power BI для предварительной версии Azure Active Directory, возможно, возникли следующие ошибки hello:</span><span class="sxs-lookup"><span data-stu-id="c2ec7-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="c2ec7-105">Сбой обновления</span><span class="sxs-lookup"><span data-stu-id="c2ec7-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="c2ec7-106">Не удалось tooupdate учетные данные источника данных</span><span class="sxs-lookup"><span data-stu-id="c2ec7-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- <span data-ttu-id="c2ec7-107">[Importing of data is taking too long](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) (Импорт данных занимает слишком много времени)</span><span class="sxs-lookup"><span data-stu-id="c2ec7-107">[Importing of data is taking too long](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long)</span></span> 
 
<span data-ttu-id="c2ec7-108">Этот раздел содержит сведения о возможных причинах hello и как toofix эти ошибки.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="c2ec7-109">"Сбой обновления"</span><span class="sxs-lookup"><span data-stu-id="c2ec7-109">Refresh failed</span></span> 
 
<span data-ttu-id="c2ec7-110">**Как эта ошибка будет отображена**: электронной почты из Power BI или состояние ошибки в журнал обновления hello.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="c2ec7-111">Причина:</span><span class="sxs-lookup"><span data-stu-id="c2ec7-111">Cause</span></span> | <span data-ttu-id="c2ec7-112">Как toofix</span><span class="sxs-lookup"><span data-stu-id="c2ec7-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="c2ec7-113">Обновите сбоя, которые могут возникать ошибки при hello учетные данные пользователей hello подключении пакет содержимого toohello были сброса, но не обновляются в параметры подключения, hello hello hello содержимого пакета.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="c2ec7-114">В Power BI найдите соответствующий toohello hello набора данных мониторинга журналы действие Azure Active Directory (Azure Active Directory действия журналы), выберите расписание обновления и затем введите учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="c2ec7-115">Обновление может завершиться ошибкой из-за проблемы toodata в базовый пакет содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="c2ec7-116">Отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-116">File a support ticket.</span></span> <span data-ttu-id="c2ec7-117">Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="c2ec7-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="c2ec7-118">Не удалось tooupdate учетные данные источника данных</span><span class="sxs-lookup"><span data-stu-id="c2ec7-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="c2ec7-119">**Как эта ошибка будет отображена**: В Power BI, можно использовать при подключении пакет содержимого журналов (Предварительная версия) Azure Active Directory действия toohello.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="c2ec7-120">Причина:</span><span class="sxs-lookup"><span data-stu-id="c2ec7-120">Cause</span></span> | <span data-ttu-id="c2ec7-121">Как toofix</span><span class="sxs-lookup"><span data-stu-id="c2ec7-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="c2ec7-122">Hello подключающегося пользователя является глобальным администратором, ни чтения безопасности или является администратором безопасности.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="c2ec7-123">Эта учетная запись глобального администратора или чтения безопасности или безопасность admin tooaccess hello пакеты содержимого.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="c2ec7-124">Клиент не имеет лицензии Premium или по крайней мере одного пользователя с файлом лицензии Premium.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="c2ec7-125">Отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-125">File a support ticket.</span></span> <span data-ttu-id="c2ec7-126">Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="c2ec7-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="c2ec7-127">"Importing of data is taking too long" (Импорт данных занимает слишком много времени)</span><span class="sxs-lookup"><span data-stu-id="c2ec7-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="c2ec7-128">**Как эта ошибка будет отображена**: В Power BI, после подключения ваш пакет содержимого hello данных процесс импорта начинается tooprepare панели мониторинга для Azure Active Directory журналом.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="c2ec7-129">Вы видите приветственное сообщение: «*Импорт данных...* »</span><span class="sxs-lookup"><span data-stu-id="c2ec7-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="c2ec7-130">Причина:</span><span class="sxs-lookup"><span data-stu-id="c2ec7-130">Cause</span></span> | <span data-ttu-id="c2ec7-131">Как toofix</span><span class="sxs-lookup"><span data-stu-id="c2ec7-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="c2ec7-132">В зависимости от размера вашего клиента hello этот шаг может занять от нескольких минут too30 мин..</span><span class="sxs-lookup"><span data-stu-id="c2ec7-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="c2ec7-133">Просто подождите.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-133">Just be patient.</span></span> <span data-ttu-id="c2ec7-134">Если сообщение hello не изменяет tooshowing панели мониторинга в течение часа, отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="c2ec7-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="c2ec7-135">Дополнительные сведения см. в разделе [как tooget поддерживают для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="c2ec7-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="c2ec7-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2ec7-136">Next steps</span></span>

<span data-ttu-id="c2ec7-137">Щелкните tooinstall hello пакет содержимого Power BI в Azure Active Directory предварительной версии [здесь](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="c2ec7-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


