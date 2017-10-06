---
title: "aaaAzure AD подключения работоспособности История изменений"
description: "В этом документе перечислены hello выпусках для Azure AD Connect Health и содержимое в этих версиях."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: a583263e412f5da9af75947f3431de2494042388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a>Azure AD Connect Health: история выпусков версий
Команда Hello Azure Active Directory регулярно обновляет Azure AD Connect Health с новыми функциями и возможностями. В этой статье перечислены версии hello и функции, которые были выпущены.

## <a name="october-2016"></a>Октябрь 2016 г.
**Обновление агента:**

* Агент Azure AD Connect Health для AD FS \(версия 2.6.408.0\).
  1. Усовершенствования в сеансах определения IP-адресов клиентов в запросах проверки подлинности.
  2. Исправления ошибок, связанных с tooAlerts
* Агент Azure AD Connect Health для AD DS (версия 2.6.408.0).
  1. Исправления ошибок, связанных с tooAlerts.
* Агент Azure AD Connect Health для синхронизации (версия 2.6.353.0) выпущен вместе с Azure AD Connect версии 1.1.281.0.
  1. Предоставлять hello необходимые данные для hello отчеты об ошибках синхронизации
  2. Исправления ошибок, связанных с tooAlerts

**Новые функции предварительной версии:**

* Отчеты об ошибках синхронизации для Azure AD Connect.

**Новые функции:**

* Azure AD Connect Health для AD FS - поля IP-адреса доступен в отчете hello top 50 пользователей, неверное имя пользователя и пароль.

## <a name="july-2016"></a>Июль 2016 г.
**Новые функции предварительной версии:**

* [Azure AD Connect Health для AD DS](active-directory-aadconnect-health-adds.md).

## <a name="january-2016"></a>Январь 2016 г.
**Обновление агента:**

* Агент Azure AD Connect Health для AD FS (версия 2.6.91.1512).

**Новые функции:**

* [Средство проверки подключения для агентов Azure AD Connect Health.](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a>Ноябрь 2015 г.
**Новые функции:**

* Поддержка [управления доступом на основе ролей](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)

**Новые функции предварительной версии:**

* [Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md).

**Исправленные проблемы:**

* Исправления ошибок, возникающих во время регистрации агента.

## <a name="september-2015"></a>Сентябрь 2015 г.
**Новые функции:**

* Отчет о неправильном имени пользователя или пароле для AD FS.
* Поддержка tooconfigure Unauthenticated HTTP прокси-сервера
* Поддержка tooconfigure агента на Server core
* Усовершенствования tooAlerts для AD FS
* Улучшения в агенте Azure AD Connect Health для AD FS, связанные с отправкой данных и подключением.

**Исправленные проблемы:**

* Исправления ошибок в сведениях об использовании, связанные с типами ошибок AD FS.

## <a name="june-2015"></a>Июнь 2015 г.
**Первоначальный выпуск Azure AD Connect Health для AD FS и прокси-сервера AD FS.**

**Новые функции:**

* Предупреждения, касающиеся наблюдения за AD FS и прокси-серверами AD FS, с помощью уведомлений по электронной почте.
* Простой доступ tooAD FS топологии и шаблоны в счетчиках производительности AD FS.
* Тенденции успешных запросов маркеров на серверах AD FS, сгруппированные по приложениям, методам проверки подлинности, запросам сетевого расположения и т. д.
* Тенденции неудачных запросов на серверах AD FS, сгруппированные по приложениям, типам ошибок и т. д.
* Упрощенное развертывание агентов с помощью учетных данных глобального администратора Azure AD.  

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о [мониторинга вашей локальной инфраструктуры и синхронизации службы удостоверений в облаке hello](active-directory-aadconnect-health.md).

