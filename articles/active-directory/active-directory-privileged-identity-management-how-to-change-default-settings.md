---
title: "параметры активации роли toomanage aaaHow | Документы Microsoft"
description: "Узнайте, как toochange hello параметры по умолчанию для привилегированных удостоверений с Azure Active Directory Privileged Identity Management расширения hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Как toomanage параметры активации роли в Azure AD Privileged Identity Management
Привилегированные роли Администратор может настроить Azure AD Privileged Identity Management (PIM) в своей организации, включая изменение hello взаимодействие для пользователя, который выполняется активация назначение ролей на право.

## <a name="manage-hello-role-activation-settings"></a>Управление параметрами активации роли hello
1. Go toohello [портал Azure](https://portal.azure.com) и выберите hello **Azure AD Privileged Identity Management** приложения hello панели мониторинга.
2. Выберите **Управление привилегированными ролями** > **Параметры**  > **Привилегированные роли**.
3. Выберите роль hello, параметры которого требуется toomanage.

На странице приветствия параметров для каждой роли существует несколько параметров, которые можно настроить. Эти параметры распространяются только на пользователей, которые являются временными администраторами, а не постоянными.

**Активаций**: hello время в часах, которые роль остается активной до истечения срока его действия. Возможное значение: от 1 до 72 часов.

**Уведомления о**: можно ли hello система отправляет tooadmins сообщений электронной почты, подтверждающее, что они активации роли. Этот параметр полезен, если требуется обнаружить несанкционированные или недопустимые активации.

**Билет инцидента или запроса**: можно выбрать номер ли tooinclude соответствующих администраторов toorequire билет при активации их роли. Этот параметр полезен при выполнении аудита доступа к ролям.

**Многофакторная проверка подлинности**: можно ли tooverify пользователей toorequire свою личность с помощью многофакторной проверки Подлинности, чтобы активировать их роли. Они достаточно tooverify один раз за сеанс не каждый раз при активации роли. Существует два tookeep советы помнить при включении многофакторной проверки Подлинности.

* Пользователи, имеющие учетные записи Майкрософт для адреса электронной почты (обычно @outlook.com, но не всегда) не может зарегистрироваться для многофакторной проверки Подлинности Azure. Если требуется tooassign toousers ролей с учетными записями Microsoft следует сделать их постоянных администраторов или отключить многофакторную проверку Подлинности для этой роли.
* Нельзя отключить MFA для ролей с высоким уровнем привилегий в Azure AD и Office 365. С помощью этой функции безопасности должны быть надежно защищены следующие роли:  
  
  * администратор приложений;
  * администратор прокси-сервера приложений;
  * Администратор выставления счетов  
  * администратор соответствия требованиям.  
  * администратор службы CRM;
  * лицо, утверждающее доступ клиентов к LockBox;
  * редактор каталогов;  
  * администратор Exchange;  
  * Глобальный администратор
  * администратор службы Intune;
  * администратор почтовых ящиков;  
  * партнер с поддержкой 1 уровня;  
  * партнер с поддержкой 2 уровня;  
  * администратор привилегированных ролей;   
  * администратор безопасности;  
  * администратор SharePoint;  
  * администратор Skype для бизнеса;  
  * администратор учетных записей;  

Дополнительные сведения об использовании многофакторной проверки Подлинности с PIM. в разделе [как tooRequire многофакторной проверки Подлинности](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

