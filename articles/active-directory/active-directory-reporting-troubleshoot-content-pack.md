---
title: "Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory | Документация Майкрософт"
description: "Содержит список сообщений об ошибках пакета содержимого действий Azure Active Directory и инструкции по их исправлению."
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
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="311f7-103">Устранение ошибок пакетов содержимого, зарегистрированных в журналах действий Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="311f7-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="311f7-104">При работе с пакетом содержимого Power BI для предварительной версии Azure Active Directory могут произойти приведенные ниже ошибки.</span><span class="sxs-lookup"><span data-stu-id="311f7-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="311f7-105">Сбой обновления</span><span class="sxs-lookup"><span data-stu-id="311f7-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="311f7-106">Не удалось обновить учетные данные источников данных</span><span class="sxs-lookup"><span data-stu-id="311f7-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- <span data-ttu-id="311f7-107">[Importing of data is taking too long](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) (Импорт данных занимает слишком много времени)</span><span class="sxs-lookup"><span data-stu-id="311f7-107">[Importing of data is taking too long](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long)</span></span> 
 
<span data-ttu-id="311f7-108">Данный раздел содержит сведения о возможных причинах и способах устранения этих ошибок.</span><span class="sxs-lookup"><span data-stu-id="311f7-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="311f7-109">"Сбой обновления"</span><span class="sxs-lookup"><span data-stu-id="311f7-109">Refresh failed</span></span> 
 
<span data-ttu-id="311f7-110">**Как отображается эта ошибка**: электронное сообщение от Power BI или состояние ошибки в журнале обновлений.</span><span class="sxs-lookup"><span data-stu-id="311f7-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="311f7-111">Причина:</span><span class="sxs-lookup"><span data-stu-id="311f7-111">Cause</span></span> | <span data-ttu-id="311f7-112">Как устранить</span><span class="sxs-lookup"><span data-stu-id="311f7-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="311f7-113">Сбои обновления могут возникнуть, если учетные данные пользователей, подключающихся к пакету содержимого, были сброшены, но не были обновлены в параметры подключения пакета содержимого.</span><span class="sxs-lookup"><span data-stu-id="311f7-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="311f7-114">В Power BI найдите набор данных, соответствующий панели мониторинга журналов действий Azure Active Directory (журналы действий Azure Active Directory), выберите "Запланировать обновление" и введите учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="311f7-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="311f7-115">Обновление может завершиться сбоем из-за проблем с данными в базовом пакете содержимого.</span><span class="sxs-lookup"><span data-stu-id="311f7-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="311f7-116">Отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="311f7-116">File a support ticket.</span></span> <span data-ttu-id="311f7-117">Дополнительные сведения см. в разделе [Как получить поддержку для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="311f7-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="311f7-118">"Не удалось обновить учетные данные источников данных"</span><span class="sxs-lookup"><span data-stu-id="311f7-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="311f7-119">**Как отображается эта ошибка**: в Power BI, при подключении к пакету содержимого журналов действий Azure Active Directory (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="311f7-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="311f7-120">Причина:</span><span class="sxs-lookup"><span data-stu-id="311f7-120">Cause</span></span> | <span data-ttu-id="311f7-121">Как устранить</span><span class="sxs-lookup"><span data-stu-id="311f7-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="311f7-122">Подключающийся пользователь не является глобальным администратором, читателем безопасности или администратором безопасности.</span><span class="sxs-lookup"><span data-stu-id="311f7-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="311f7-123">Используйте учетную запись глобального администратора, читателя безопасности или администратора безопасности для доступа к пакетам содержимого.</span><span class="sxs-lookup"><span data-stu-id="311f7-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="311f7-124">Клиент не имеет лицензии Premium или по крайней мере одного пользователя с файлом лицензии Premium.</span><span class="sxs-lookup"><span data-stu-id="311f7-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="311f7-125">Отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="311f7-125">File a support ticket.</span></span> <span data-ttu-id="311f7-126">Дополнительные сведения см. в разделе [Как получить поддержку для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="311f7-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="311f7-127">"Importing of data is taking too long" (Импорт данных занимает слишком много времени)</span><span class="sxs-lookup"><span data-stu-id="311f7-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="311f7-128">**Как отображается эта ошибка**: в Power BI после подключения к пакету содержимого процесс импорта данных приступает к подготовке панели мониторинга для журнала действий Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="311f7-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="311f7-129">Отображается сообщение: *Importing of data…* (Импорт данных…)</span><span class="sxs-lookup"><span data-stu-id="311f7-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="311f7-130">Причина:</span><span class="sxs-lookup"><span data-stu-id="311f7-130">Cause</span></span> | <span data-ttu-id="311f7-131">Как устранить</span><span class="sxs-lookup"><span data-stu-id="311f7-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="311f7-132">В зависимости от размера клиента шаг может длиться от нескольких минут до получаса.</span><span class="sxs-lookup"><span data-stu-id="311f7-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="311f7-133">Просто подождите.</span><span class="sxs-lookup"><span data-stu-id="311f7-133">Just be patient.</span></span> <span data-ttu-id="311f7-134">Если в течение часа сообщение не исчезнет и не отобразится панель мониторинга, отправьте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="311f7-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="311f7-135">Дополнительные сведения см. в разделе [Как получить поддержку для Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="311f7-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="311f7-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="311f7-136">Next steps</span></span>

<span data-ttu-id="311f7-137">Чтобы установить пакет содержимого Power BI для предварительной версии Azure Active Directory, щелкните [здесь](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="311f7-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


