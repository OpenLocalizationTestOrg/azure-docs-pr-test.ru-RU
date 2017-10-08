---
title: "Отчет об использовании aaaUnlicensed | Документы Microsoft"
description: "Здравствуйте Нелицензированное использование отчетов позволяет выявить Нелицензированные пользователи, использующие платные функции Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Отчет о нелицензированном использовании
Здравствуйте Нелицензированное использование отчетов позволяет выявить Нелицензированные пользователи, использующие платные функции Azure AD. Это позволяет лучше использовать toomake лицензий, приобретенных и tooidentify, вы знаете, когда может потребоваться дополнительные лицензии. 

Hello отчетов отображает активные использование hello платные функции hello последние 30 дней. 

## <a name="report-structure"></a>Структура отчета
| Имя столбца | Описание |
|:--- |:--- |
| Пользователь без лицензии |Имя пользователя hello |
| Функция |имя функции Hello. Например, условный доступ |
| Приложение к которому осуществлялся доступ |Имя приложения hello, к которому осуществляется с помощью функции hello Hello. Например, Office 365 SharePoint Online |

> [!NOTE]
> Если учетная запись пользователя была удалена Здравствуйте, «Нелицензированные пользователя» будет заполнен столбец с Идентификатором, например 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Функция условного доступа
При доступе к службе, для которой применяется политика условного доступа, пользователи без лицензии будут помечены, если у них нет лицензии Azure AD Premium. 

Это относится tooMFA / расположение политики, а также устройств политики, использовать Intune.

## <a name="see-also"></a>См. также
* [Защита доступа к Office 365 и другим приложениям, подключенным к Azure Active Directory](active-directory-conditional-access.md)
* [Начало работы с условным доступом tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

