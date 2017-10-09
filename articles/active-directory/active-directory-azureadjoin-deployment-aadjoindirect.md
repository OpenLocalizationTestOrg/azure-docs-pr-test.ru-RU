---
title: "aaaUsage сценарии и рекомендации по развертыванию для присоединения Azure AD | Документы Microsoft"
description: "Поясняет, как администраторы могут настроить подключение конечных пользователей (сотрудников компаний, учащихся и других пользователей) к Azure AD. Он также рассматриваются различные реальные сценарии hello использования присоединения Azure AD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Сценарии использования и рекомендации по развертыванию для присоединения к Azure AD
## <a name="usage-scenarios-for-azure-ad-join"></a>Сценарии использования для присоединения к Azure AD
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Сценарий 1: Предприятий главным образом в облаке hello
Azure Active Directory соединения (Azure AD Join) могут помочь вам Если в настоящее время работы и управление удостоверениями для вашей организации в облаке hello или скоро перемещается toohello облака. Можно использовать учетную запись, созданную в Azure AD toosign в tooWindows 10. Через [hello, сначала запустите процесс качества (FRX)](active-directory-azureadjoin-user-frx.md), или с помощью присоединения Azure AD из [меню "настройки" hello](active-directory-azureadjoin-user-upgrade.md), пользователям можно соединить их tooAzure машины AD.  Пользователи также могут пользоваться единого входа (SSO) доступ слишком облачные ресурсы, такие как Office 365, в браузере или в приложениях Office.

### <a name="scenario-2-educational-institutions"></a>Сценарий 2. Образовательные учреждения
В образовательных учреждениях обычно существуют два типа пользователей: преподаватели и учащиеся. Члены преподавателей, считаются долговременного члены организации hello. Рекомендуется создать для них локальные учетные записи. Но учащихся shorter-term входят hello организации и своих учетных записей можно управлять в Azure AD. Это означает, что каталог шкалы можно принудительно отправить toohello облака, а не хранятся локально. Это также означает, что студенты будут может toosign в tooWindows с их учетными записями Azure AD и получить доступ tooOffice 365 ресурсы в приложениях Office.

### <a name="scenario-3-retail-businesses"></a>Сценарий 3. Предприятия розничной торговли
На предприятиях розничной торговли имеются как сезонные работники, так и долгосрочные сотрудники. Как правило, для долгосрочных сотрудников, занятых полный рабочий день, создаются локальные учетные записи и используются компьютеры, присоединенные к домену. Но сезонных работников shorter-term входят организации hello и это нежелательно toomanage своих учетных записей, где пользовательских лицензий можно легко перемещать. При создании учетных записей пользователей в облаке hello с Office 365 лицензий эти пользователи будут получать преимущества hello вход tooWindows и приложений Office с помощью учетной записи Azure AD, пока поддерживать большую гибкость и их лицензий после окончания.

### <a name="scenario-4-additional-scenarios"></a>Сценарий 4. Дополнительные сценарии
Вместе с hello преимуществ уже было сказано ранее вы при наличии более эффективно присоединиться их устройства tooAzure AD из-за упрощенные присоединяемый, управление устройствами для эффективного, регистрации управления автоматическое мобильных устройств и tooAzure пользователей AD и локальным ресурсам.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Рекомендации по развертыванию для присоединения к Azure AD
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Включить вашей toojoin пользователям устройства, принадлежащие компании непосредственно tooAzure AD
Предприятия может предоставить учетным записям только для облака toopartner компании и организации. Партнеры затем смогут легко получать доступ к приложениям и ресурсам организации, используя функцию единого входа. Этот сценарий является применимо toousers, доступ к ресурсам в основном в hello облака, такие как Office 365 или SaaS приложений, которые зависят от Azure AD для проверки подлинности.

### <a name="prerequisites"></a>Предварительные требования
**На уровне предприятия hello (администратор)**

* Подписка Azure и доступ к Azure Active Directory  

**На уровне пользователя hello**

* Windows 10 (выпуски "Профессиональная" и "Корпоративная")

### <a name="administrator-tasks"></a>Задачи администратора
* [Настройка регистрации устройств](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Задачи пользователя
* [Настройка нового устройства Windows 10 для работы с Azure AD во время установки](active-directory-azureadjoin-user-frx.md)
* [Настройка устройства Windows 10 с помощью Azure AD из меню параметров hello](active-directory-azureadjoin-user-upgrade.md)
* [Присоединение личных организации tooyour устройства Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Реализация концепции BYOD в организации для устройств Windows 10
Можно настроить на пользователей и сотрудникам toouse свои личные устройства (BYOD) tooaccess компании приложений Windows и ресурсы. Пользователи могут добавлять их Azure AD учетных записей (рабочие или учебные учетные записи) tooa личных устройств tooaccess ресурсов Windows в режиме безопасность и соответствие.

### <a name="prerequisites"></a>Предварительные требования
**На уровне предприятия hello (администратор)**

* Подписка Azure AD

**На уровне пользователя hello**

* Windows 10 (выпуски "Профессиональная" и "Корпоративная")

### <a name="administrator-tasks"></a>Задачи администратора
* [Настройка регистрации устройств](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Задачи пользователя
* [Присоединение личных организации tooyour устройства Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Дополнительная информация
* [Windows 10 для предприятия hello: способов toouse устройств для работы](active-directory-azureadjoin-windows10-devices-overview.md)
* [Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Сценарии использования для присоединения к Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Подключитесь к домену устройства tooAzure AD для Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Настройка присоединения к Azure AD](active-directory-azureadjoin-setup.md)

