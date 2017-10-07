---
title: "Лицензирование: Azure AD SSPR | Документация Майкрософт"
description: "Требования к лицензированию самостоятельного сброса пароля в Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Требования к лицензированию самостоятельного сброса пароля в Azure AD

Чтобы toofunction сброса пароля Azure AD вы **необходимо наличие по крайней мере один лицензии в вашей организации**. Не выполняют лицензирования на hello интерфейса для сброса пароля пользователя. соответствие toomaintain лицензионном соглашении корпорации Майкрософт, необходимо tooassign лицензий tooany пользователей, которые используют функции premium.

* **Полностью облачные пользователи.** Любой платный номер SKU Office 365 (O365) или Azure AD Basic.
* **Облачные пользователи** или **локальные пользователи.** Azure AD Premium P1 или P2, Enterprise Mobility + Security (EMS) или Secure Productive Enterprise (SPE).

## <a name="licenses-required-for-password-writeback"></a>Лицензии, необходимые для компонента обратной записи паролей

toouse обратной записи паролей, необходимо иметь одно из следующих лицензии, назначенные в вашем клиенте hello.

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Office 365 автономный планов лицензирования **не поддерживают обратную запись паролей** и требует выполнения одного из предыдущих планы для этой функции toowork hello.

Дополнительно лицензирования, включая затраты на можно найти на следующих страницах hello

* [Сайт с ценами на Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security).
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx).

## <a name="enable-group-or-user-based-licensing"></a>Включение группового и пользовательского лицензирования

Azure AD теперь поддерживает групповые лицензирования допускающему лицензии tooassign администраторов в массовой tooa группы пользователей, а не их назначения по одному. [Назначение лицензий группе пользователей в Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Некоторые службы Майкрософт недоступны во всех расположениях. Перед tooa пользователя можно назначить лицензию, Здравствуйте, администратор должен указать свойство «Место использования» hello hello пользователя. Назначение лицензий можно сделать записью > профиль > раздел параметров hello портал Azure. **При использовании Назначение группы лицензирования, все пользователи, не указано место использования наследуют hello расположение каталога hello.**

## <a name="next-steps"></a>Дальнейшие действия

Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD

* [**Быстрое начало работы с самостоятельным сбросом пароля в Azure AD**](active-directory-passwords-getting-started.md). Запуск и выполнение службы самостоятельного управления паролями Azure AD. 
* [**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями
* [**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу
* [**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.
* [**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.
* [**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы
* [**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как? Почему? Что? Где? Кто? Когда? -Ответы tooquestions требуется, чтобы tooask
* [**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR

