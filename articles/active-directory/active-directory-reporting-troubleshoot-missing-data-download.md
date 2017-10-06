---
title: "Устранение неполадок: Отсутствующие данные в hello загрузить журналы действий Azure Active Directory | Документы Microsoft"
description: "Предоставляет данные toomissing разрешения в загруженный журналы действий Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Данные не найдены в журналы действий hello Azure Active Directory, я загрузил


## <a name="symptoms"></a>Симптомы

Я загрузил журналы действий hello (аудита или входа в систему), и я не вижу все записи hello для hello раз, когда я выбрал. Почему? 

 ![Отчеты](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Причина:

При загрузке журналы действий в hello портал Azure ограничена hello шкалы too120K записей, отсортированных по дате последней. 

## <a name="resolution"></a>Способы устранения:

Можно использовать [Azure AD API-интерфейсы отчетов](active-directory-reporting-api-getting-started.md) toofetch tooa миллионов записей в любой момент. Наш рекомендуется toorun сценария в соответствии с расписанием, вызывающий hello отчетов API-интерфейсы toofetch записывает в реальному за период времени (например, ежедневно или еженедельно).

## <a name="next-steps"></a>Дальнейшие действия
В разделе hello [отчетов часто задаваемые вопросы об Azure Active Directory](active-directory-reporting-faq.md).

