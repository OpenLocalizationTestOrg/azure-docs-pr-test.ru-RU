---
title: "Синхронизация Azure AD Connect: расширения каталогов | Документация Майкрософт"
description: "В этом разделе описывается функция расширения hello каталог в Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Синхронизация Azure AD Connect: расширения каталогов
Расширения каталогов позволяет tooextend hello схемы в Azure AD с помощью собственных атрибутов из локальной службы Active Directory. Эта функция позволяет toobuild бизнес-приложения, использование атрибутов продолжить toomanage в локальной среде. Эти атрибуты могут быть использованы через [расширения каталогов Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) или [Microsoft Graph](https://graph.microsoft.io/). Вы увидите hello атрибуты доступны с помощью [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) и [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) соответственно.

В настоящее время рабочие нагрузки Office 365 не используют эти атрибуты.

Настройка дополнительных атрибутов требуется toosynchronize пути hello пользовательские параметры в мастере установки hello.
![Мастер расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
Hello установки показаны следующие атрибуты, которые являются допустимыми кандидатами hello.

* Типы объектов пользователей и групп
* Однозначные атрибуты: строка, логическое значение, целое число, двоичное значение.
* Многозначные атрибуты: строка, двоичное значение.

Список атрибутов Hello считывается из кэша схем hello создается во время установки Azure AD Connect. Если расширения схемы Active Directory hello с дополнительные атрибуты, затем hello [схема должна быть обновлена](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) перед эти новые атрибуты являются видимыми.

Объект в Azure AD может иметь атрибутов расширений каталога too100. Максимальная длина Hello-250 знаков. Если значение атрибута длиннее, оно усекается обработчиком синхронизации hello.

Во время установки Azure AD Connect приложение регистрируется при условии наличия этих атрибутов. Можно видеть это приложение в hello портал Azure.  
![Приложение расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Теперь эти атрибуты доступны в Graph:   
![График](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Hello атрибуты имеют префикс с расширением\_{AppClientId}\_. Hello AppClientId имеет одинаковое значение для всех атрибутов в клиенте Azure AD hello.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
