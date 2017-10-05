---
title: "Синхронизация Azure AD Connect: расширения каталогов | Документация Майкрософт"
description: "В этой статье описывается функция расширений каталогов в Azure AD Connect."
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a>Синхронизация Azure AD Connect: расширения каталогов
Расширения каталогов позволяет расширять схему в Azure AD с помощью собственных атрибутов из локального каталога Active Directory. Эта функция позволяет создавать бизнес-приложения, использующие атрибуты, которыми вы по-прежнему можете управлять локально. Эти атрибуты могут быть использованы через [расширения каталогов Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) или [Microsoft Graph](https://graph.microsoft.io/). Просмотреть доступные атрибуты можно с помощью [проводника Azure AD Graph](https://graphexplorer.cloudapp.net) и [проводника Microsoft Graph](https://graphexplorer2.azurewebsites.net/) соответственно.

В настоящее время рабочие нагрузки Office 365 не используют эти атрибуты.

Дополнительные атрибуты для синхронизации выбираются в разделе пользовательских параметров мастера установки.
![Мастер расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)  
При установке отображаются следующие допустимые атрибуты:

* Типы объектов пользователей и групп
* Однозначные атрибуты: строка, логическое значение, целое число, двоичное значение.
* Многозначные атрибуты: строка, двоичное значение.

Список атрибутов считывается из кэша схемы, созданного во время установки Azure AD Connect. Если в схему Active Directory добавлены дополнительные атрибуты, они будут отображаться только после [обновления схемы](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema).

Объект в Azure AD может иметь до 100 атрибутов расширений каталога. Максимальная длина составляет 250 символов. Если значение атрибута больше, он будет усечен модулем синхронизации.

Во время установки Azure AD Connect приложение регистрируется при условии наличия этих атрибутов. Это приложение отображается на портале Azure.  
![Приложение расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

Теперь эти атрибуты доступны в Graph:   
![График](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

Атрибуты имеют префикс extension\_{AppClientId}\_. AppClientId имеет одно значение для всех атрибутов в вашем клиенте Azure AD.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
