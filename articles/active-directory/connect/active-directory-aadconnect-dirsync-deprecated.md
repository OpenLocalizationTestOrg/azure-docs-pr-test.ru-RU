---
title: "aaaUpgrade из DirSync и Azure AD Sync | Документы Microsoft"
description: "Описывает способ tooupgrade из DirSync и Azure AD Sync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Обновление Windows Azure Active Directory Sync и Azure Active Directory Sync
Azure AD Connect hello лучшим способом tooconnect вашего локального каталога с Azure AD и Office 365. Это помешает tooupgrade tooAzure подключение AD из синхронизации Windows Azure Active Directory (DirSync) или Azure AD Sync как эти средства являются теперь рекомендуется к использованию и конец поддержки на 13 апреле 2017 г.

для одного леса клиентов (DirSync), а также для нескольких лесов и других опытных пользователей (Azure AD Sync) предоставляются Hello два идентификатора синхронизации средства, которые являются устаревшими. На смену этим средствам пришло единое решение, подходящее для любой ситуации: Azure AD Connect. Оно включает новые возможности, усовершенствования функций и поддержку новых сценариев. возможности toocontinue toosynchronize toobe tooAzure данных удостоверений в локальной среде AD и Office 365, настоятельно рекомендуется обновить tooAzure AD Connect.

последним выпуском Hello DirSync была выпущена в июле 2014 и hello последним выпуском Azure AD Sync, выпущенной в май 2015 г.

## <a name="what-is-azure-ad-connect"></a>Что такое Azure AD Connect?
Azure AD Connect — tooDirSync последователь hello и Azure AD Sync. В нем объединены все сценарии, которые поддерживались этими средствами. Дополнительные сведения см. в статье [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>График устаревания
| Дата | Комментарий |
| --- | --- |
| 13 апреля 2016 г. |Windows Azure Active Directory Sync (DirSync) и Microsoft Azure Active Directory Sync (Azure AD Sync) объявлены устаревшими. |
| 13 апреля 2017 г. |Прекращение поддержки. Клиенты больше не будет возможности tooopen обращение в службу поддержки без обновления tooAzure AD подключиться в первую очередь. |
|31 декабря 2017 г.|Azure AD больше не будет принимать подключения от Windows Azure Active Directory Sync (DirSync) и Microsoft Azure Active Directory Sync (Azure AD Sync).

## <a name="how-tootransition-tooazure-ad-connect"></a>Как tootransition tooAzure AD Connect
Если вы используете DirSync, то переход можно выполнить одним из двух способов: это может быть обновление на месте и параллельное развертывание. Обновление на месте рекомендуется для большинства клиентов при наличии последней версии операционной системы и менее чем 50 000 объектов. В других случаях рекомендуется toodo параллельного развертывания, где конфигурации DirSync перемещен tooa новый сервер Azure AD Connect.

Если используется Azure AD Sync, то рекомендуется обновление на месте. Если вы хотите, возможные tooinstall нового сервера Azure AD Connect параллельно и ходу миграции из вашего tooAzure сервера синхронизации AD Azure AD Connect.

| Решение | Сценарий |
| --- | --- |
| [Обновление из DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Если есть уже работающий сервер DirSync.</li> |
| [Обновление из Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>При переходе с Azure AD Sync.</li> |

Если вы хотите toosee как toodo месте обновление от DirSync tooAzure AD Connect, а затем см. в этом видео Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Часто задаваемые вопросы
**Вопрос было получено уведомление по электронной почте от группы разработчиков Azure hello и/или сообщение от центра сообщений hello Office 365, но я использую подключение.**  
Hello уведомление отправляется toocustomers с Azure AD Connect 1.0 номер сборки. \*.0 (с использованием версии pre 1.1). Корпорация Майкрософт рекомендует заказчикам освобождает toostay текущего с Azure AD Connect. Hello [автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md) впервые появилось в версии 1.1 позволяет легко tooalways имеют последнюю версию Azure AD Connect установлена.

**Вопрос. Перестанет ли DirSync или Azure AD Sync работать 13 апреля 2017 года?**  
DirSync и Azure AD Sync продолжится toowork на 13-й апреле 2017 г.  Но служба Azure AD больше не будет принимать подключения из DirSync (Azure AD Sync), начиная с 31 декабря 2017 г.

**Вопрос. Какие версии DirSync можно обновить?**  
Это поддерживается tooupgrade из любого из выпусков DirSync в настоящее время используется.

**Вопрос hello соединителя Azure AD для FIM или MIM?**  
имеет Hello соединителя Azure AD для FIM или MIM **не** было объявлено как устаревшие. Проект **заморожен**, т. е. новые функции не добавляются, а ошибки не исправляются. Корпорация Майкрософт рекомендует клиентов с помощью toomove tooplan от него tooAzure AD Connect. Настоятельно рекомендуется начала toonot любые новые развертывания, используя его. Этот соединитель будут объявлены устаревшими в будущем hello.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
