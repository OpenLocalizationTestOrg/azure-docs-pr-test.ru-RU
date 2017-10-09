---
title: "Синхронизация Azure AD Connect: изменение учетной записи службы синхронизации подключения hello Azure AD | Документы Microsoft"
description: "В этом разделе документе описываются hello ключ шифрования, а как tooabandon его после hello пароль изменен."
services: active-directory
keywords: "учетная запись службы синхронизации Azure AD, пароль"
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Изменение пароля учетной записи службы синхронизации Azure AD Connect hello
При изменении пароля учетной записи службы синхронизации Azure AD Connect hello hello службы синхронизации будут начала может неверно до прервана hello ключ шифрования и пароль учетной записи службы синхронизации Azure AD Connect hello повторной инициализации. 

Azure AD Connect, как часть hello служб синхронизации использует шифрование ключа toostore hello пароли hello AD DS и учетные записи служб Azure AD.  Эти учетные записи, шифруются перед сохранением в базе данных hello. 

Hello ключ шифрования, используемый защищается с помощью [защиты данных Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI защищает ключ шифрования hello, с помощью hello **пароль учетной записи службы hello Azure AD Connect sync**. 

Если вам требуется пароль учетной записи службы hello toochange можно использовать процедуры hello в [ключ шифрования Abandoning hello Azure AD Sync подключения](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish это.  Эти процедуры также следует использовать, если требуется ключ шифрования hello tooabandon по любой причине.

##<a name="issues-that-arise-from-changing-hello-password"></a>Проблемы, которые возникают вследствие изменения пароля hello
Есть две вещи, которые должны производиться при изменении пароля учетной записи службы hello toobe.

Во-первых необходимо в диспетчер управления службами Windows hello пароль toochange hello.  Пока вы не устраните эту проблему, будут появляться следующие ошибки.


- При попытке hello toostart службы синхронизации в диспетчере управления службами Windows, возникает ошибка hello»**Windows не удалось запустить службу Microsoft Azure AD Sync hello на локальном компьютере**». **Ошибка 1069: hello не запустилась из-за ошибки tooa входа в систему.** "
- В области просмотра событий Windows журнал системных событий hello содержит ошибку с **7038 идентификатор события** и сообщение «**hello службы ADSync было невозможно toolog на как и в настоящее время настроен hello пароль из-за следующих toohello ошибка: Hello имя пользователя или пароль неправильный.** "

Во-вторых при определенных условиях, при обновлении пароля hello hello служба синхронизации больше не можем извлечь ключ шифрования hello посредством DPAPI. Без ключа шифрования hello приветствия служба синхронизации не удается расшифровать hello toosynchronize необходимые пароли из локальной AD и Azure AD.
Вы этом случае вы увидите такие ошибки.

- В разделе диспетчера управления службами, если при toostart hello службы синхронизации, не удалось получить ключ шифрования hello, он завершается с ошибкой «** hello Microsoft Azure AD Sync не удается запустить Windows на локальном компьютере. Дополнительные сведения просмотрите журнал событий системы hello. Если это служба не корпорации Майкрософт, обратитесь к поставщику службы hello и см. код ошибки tooservice **-21451857952 ***.»
- В средстве просмотра событий Windows, журнал событий приложения hello содержит ошибку с **6028 идентификатор события** и сообщение об ошибке *»**ключа шифрования сервера hello невозможен.* *»*

tooensure, не получают эти ошибки, выполните процедуры hello в [ключ шифрования Abandoning hello Azure AD Sync подключения](#abandoning-the-azure-ad-connect-sync-encryption-key) при изменении пароля hello.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Ключ шифрования подключения службу синхронизации Azure AD прерывающее hello
>[!IMPORTANT]
>Hello следующие процедуры применяются только tooAzure AD Connect сборки 1.1.443.0 или более ранних версий.

Используйте следующий ключ шифрования hello tooabandon процедуры hello.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Какие toodo, если требуется ключ шифрования tooabandon hello

Если требуется ключ шифрования hello tooabandon используйте следующие процедуры tooaccomplish hello.

1. [Прервать hello существующий ключ шифрования](#abandon-the-existing-encryption-key)

2. [Указывать пароль учетной записи hello hello учетной записи службы AD DS](#provide-the-password-of-the-ad-ds-account)

3. [Повторная инициализация hello пароль учетной записи Azure AD sync hello](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Запуск службы синхронизации hello](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Прервать hello существующий ключ шифрования
Отказаться от hello существующий ключ шифрования, поэтому могут создаваться этого нового ключа шифрования:

1. Войдите в систему tooyour подключения сервера Azure AD как администратор.

2. Запустите сеанс PowerShell.

3. Найдите toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Выполните команду hello.`./miiskmu.exe /a`

![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Указывать пароль учетной записи hello hello учетной записи службы AD DS
Как больше не могут быть расшифрованы hello существующие пароли, хранящийся в базе данных hello, необходимо tooprovide hello служба синхронизации с hello пароль учетной записи hello AD DS. Служба синхронизации Hello шифрует hello пароли, с помощью нового ключа шифрования hello:

1. Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).
</br>![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Go toohello **соединители** вкладки.
3. Выберите hello **соединителя AD** , соответствующий tooyour локальной AD. При наличии более одного соединителя AD, повторите указанные действия для каждого из них hello.
4. В разделе **Действия** выберите **Свойства**.
5. В всплывающем диалоговом окне приветствия выберите **подключения леса tooActive**:
6. Введите пароль hello учетной записи hello AD DS в hello **пароль** текстового поля. Если вы не знаете пароль, необходимо задать tooa известно значение перед выполнением этого шага.
7. Нажмите кнопку **ОК** toosave hello новый пароль и закрыть hello всплывающем диалоговом окне.
![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Повторная инициализация hello пароль учетной записи Azure AD sync hello
Нельзя напрямую предоставить hello пароль учетной записи службы toohello службы синхронизации для hello Azure AD. Вместо этого необходим командлет hello toouse **ADSyncAADServiceAccount добавить** tooreinitialize hello учетной записи службы Azure AD. Hello командлет сбрасывает пароль учетной записи hello и делает доступными toohello служба синхронизации:

1. Запустите новый сеанс PowerShell на сервере hello Azure AD Connect.
2. Выполните командлет `Add-ADSyncAADServiceAccount`.
3. В диалоговом окне всплывающих hello учетные данные hello Azure AD глобального администратора для вашего клиента Azure AD.
![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Если успешна, вы увидите командную строку PowerShell hello.

#### <a name="start-hello-synchronization-service"></a>Запуск службы синхронизации hello
Теперь, когда hello служба синхронизации имеет ключ шифрования toohello доступа и все hello пароли ему, можно перезапустить службу hello в диспетчер управления службами Windows hello:


1. Go tooWindows диспетчера управления службами (Пуск → службы).
2. Выберите **службу синхронизации Microsoft Azure AD** и нажмите кнопку "Перезапустить".

## <a name="next-steps"></a>Дальнейшие действия
**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)

* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
