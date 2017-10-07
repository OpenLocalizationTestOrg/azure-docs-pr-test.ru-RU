---
title: "Синхронизация Azure AD Connect: изменение пароля учетной записи доменных служб Active Directory hello AD | Документы Microsoft"
description: "Этот раздел документа описывает, как изменена tooupdate Azure AD Connect после hello пароль учетной записи hello AD DS."
services: active-directory
keywords: "учетная запись AD DS, учетная запись Active Directory, пароль"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Изменение пароля учетной записи hello AD DS
Учетная запись Hello AD DS ссылается toohello учетная запись пользователя Azure AD Connect toocommunicate с локальной Active Directory. При изменении пароля hello hello учетной записи службы AD DS необходимо обновить службы подключения синхронизации Azure AD с hello нового пароля. В противном случае приветствия синхронизации больше не могут правильно синхронизировать с hello локальной Active Directory и могут возникнуть следующие ошибки hello:

* В hello диспетчер службы синхронизации любой импорта или экспорта операцию с локальным AD завершится неудачно, **без запуска учетных данных** ошибки.

* В средстве просмотра событий Windows, журнал событий приложения hello содержит ошибку с **событий Идентификатором 6000** и сообщение **«hello агент управления «contoso.com» сбой toorun недопустимые учетные данные hello»** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Как tooupdate hello служба синхронизации с нового пароля для учетной записи службы AD DS
hello tooupdate службы синхронизации с hello нового пароля:

1. Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Go toohello **соединители** вкладки.

3. Выберите hello **соединителя AD** , соответствующий учетной записи toohello AD доменных служб Active Directory, для которого было изменено его пароль.

4. В разделе **Действия** выберите **Свойства**.

5. В всплывающем диалоговом окне приветствия выберите **подключения леса tooActive**:

6. Введите новый пароль учетной записи, hello AD DS hello в hello **пароль** текстового поля.

7. Нажмите кнопку **ОК** toosave hello новый пароль и закрыть hello всплывающем диалоговом окне.

8. Перезапуск hello Azure AD подключения службы синхронизации в диспетчере служб Windows. Это tooensure, старый пароль toohello любые ссылки, удаляется из кэша памяти hello.

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)

* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
