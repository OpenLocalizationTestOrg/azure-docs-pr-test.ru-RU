---
title: "aaaSign модули после нескольких неудачных попыток"
description: "Отчет, содержащий пользователей, которые успешно выполнили вход после нескольких последовательных неудачных попыток входа."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="aab30-103">"Операции входа после нескольких неудачных попыток";</span><span class="sxs-lookup"><span data-stu-id="aab30-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="aab30-104">В этом отчете указываются пользователи, которые успешно выполнили вход после нескольких последовательных неудачных попыток входа.</span><span class="sxs-lookup"><span data-stu-id="aab30-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="aab30-105">Возможные причины:</span><span class="sxs-lookup"><span data-stu-id="aab30-105">Possible causes include:</span></span>

* <span data-ttu-id="aab30-106">пользователь забыл свой пароль;</span><span class="sxs-lookup"><span data-stu-id="aab30-106">User had forgotten their password</span></span></li><li><span data-ttu-id="aab30-107">Пользователь является hello жертвой успешной пароля подбора</span><span class="sxs-lookup"><span data-stu-id="aab30-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="aab30-108">В результатах этого отчета будут отображены hello число последовательных неудачных вход попыток предыдущих toohello успешного входа в систему и метки времени hello первого успешного входа в.</span><span class="sxs-lookup"><span data-stu-id="aab30-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="aab30-109">**Параметры отчета**: можно настроить минимальное количество последовательных неудачных попыток входа hello попыток, прежде чем может быть отображен в отчете hello.</span><span class="sxs-lookup"><span data-stu-id="aab30-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="aab30-110">При внесении изменений, которые его установке toothis toonote важно, эти изменения не будет применен tooany существующие неудачных входов, которые отображаются в существующем отчете.</span><span class="sxs-lookup"><span data-stu-id="aab30-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="aab30-111">Тем не менее они будут применяться tooall будущих входов. Отчет об изменениях toothis могут производиться только Лицензированные Администраторы.</span><span class="sxs-lookup"><span data-stu-id="aab30-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Операции входа после нескольких сбоев](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

