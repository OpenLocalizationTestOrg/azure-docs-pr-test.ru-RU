---
title: "Синхронизация Azure AD Connect: как учетная запись службы toomanage hello Azure AD | Документы Microsoft"
description: "В этом разделе описываются, как учетная запись службы toorestore hello Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, как tooreset hello пароль для hello Azure AD Connect sync учетная запись службы соединителя"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Синхронизация Azure AD Connect: как учетная запись службы toomanage hello Azure AD
бесплатные службы toobe должен Hello учетной записи службы hello соединителя Azure AD. Если вам требуется tooreset свои учетные данные, этот раздел предназначен для вас. Например, если по ошибке сброс пароля hello hello учетной записи службы с помощью PowerShell имеет глобального администратора.

## <a name="reset-hello-credentials"></a>Сброс учетных данных hello
Если учетная запись службы hello, определенные для hello соединителя Azure AD не удается связаться с Azure AD из-за проблем tooauthentication, можно сбросить пароль hello.

1. Войдите в сервер синхронизации Azure AD Connect toohello и запустите PowerShell.
2. Запустите `Add-ADSyncAADServiceAccount`.  
   ![Командлет PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Введите учетные данные глобального администратора Azure AD.

Этот командлет сбрасывает hello пароль для учетной записи службы hello и обновить его в Azure AD и в модуле синхронизации hello.

## <a name="known-issues-these-steps-can-solve"></a>Известные проблемы, которые можно решить с помощью описанных действий
В этом разделе приведен список ошибок, обнаруженных командой клиентов, которые были исправлены при помощи учетных данных, сброс hello учетной записи службы Azure AD.

- - -
Событие 6900  
Hello сервер обнаружил непредвиденную ошибку при обработке уведомления об изменении пароля:  
AADSTS70002: ошибка при проверке учетных данных. AADSTS50054: старый пароль используется для проверки подлинности.

- - -
Событие 659  
Произошла ошибка при получении конфигурации синхронизации политики паролей. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException.  
AADSTS70002: ошибка при проверке учетных данных. AADSTS50054: старый пароль используется для проверки подлинности.

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)

