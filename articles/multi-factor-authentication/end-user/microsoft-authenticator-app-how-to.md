---
title: "aaaMicrosoft приложение для проверки подлинности для мобильных телефонов | Документы Microsoft"
description: "Узнайте, как tooupgrade toohello последнюю версию Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Приступая к работе с приложением для проверки подлинности Microsoft hello
Hello приложение для проверки подлинности Microsoft обеспечивает дополнительный уровень безопасности в вашей рабочей или учебной учетной записи (например, bsimon@contoso.com) или учетной записи Майкрософт (например, bsimon@outlook.com).

приложение Hello работает в одном из двух способов:

* **Уведомление.** приложение Hello могут помочь предотвратить несанкционированный доступ tooaccounts и остановить мошеннические транзакции с помощью принудительной отправки уведомлений tooyour смартфоне или планшете. Просто просмотреть hello уведомлений и если оно легитимное, выберите **проверьте**. В противном случае нажмите кнопку **Отклонить**. 
* **Код проверки**. приложение Hello можно использовать как программный маркер toogenerate OAuth код проверки. Введите имя пользователя и пароль, можно ввести код hello, предоставляемые приложение hello в экране входа hello. код проверки Hello предоставляет второй формы проверки подлинности.

приложение для проверки подлинности Microsoft Hello заменяет приложение Azure Authenticator hello. приложение Azure Authenticator Hello по-прежнему работает, но если вы решите toomove toohello новый Microsoft приложение для проверки подлинности, в этой статье помогут вам.  

## <a name="opt-in-for-two-step-verification"></a>Выбор двухфакторной проверки подлинности

приложение для проверки подлинности Microsoft Hello не работает самостоятельно. Настройте каждый из вашего tooprompt учетные записи для второй способ проверки после при входе с использованием имени пользователя и пароля. 

Для рабочей или учебной учетной записи не получить обычно toochoose эту функцию для текущего пользователя. Вместо этого администратор безопасности будет означать согласие от имени пользователя и уведомляет tooregister методы проверки для вашей учетной записи. Если этот сценарий применим tooyou, Дополнительные сведения см. в разделе [что многофакторной проверки подлинности Azure означает для меня](multi-factor-authentication-end-user.md).

Личная учетная запись необходимо tooset копирование двухшаговую проверку для текущего пользователя. Если у вас есть учетная запись Майкрософт, это описание этих действий доступно на странице [Сведения о двухшаговой проверке](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Также можно использовать hello проверки подлинности Microsoft с учетными записями других производителей. Они вызывать функции hello нечто, отличное от двухшаговую проверку, но должен быть доступ toofind его в параметры безопасности или входа в систему. 

## <a name="install-hello-app"></a>Установите приложение hello
приложение для проверки подлинности Microsoft Hello доступен для [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), и [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Добавить приложение toohello учетных записей
Для каждой учетной записи, которую приложением проверки подлинности Microsoft toohello tooadd используйте один из следующих процедур hello.

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Добавить личные приложения toohello учетной записи Майкрософт

Для личную учетную запись Майкрософт (один используется toosign tooOutlook.com, Xbox, Скайп, т. д.), все имеют toodo — войти в учетную запись tooyour в приложение для проверки подлинности Microsoft hello.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Добавить рабочий или учебный приложение toohello учетной записи, с помощью сканера hello QR кода
1. Откройте экран настройки проверки безопасности toohello.  Сведения о том, как tooget toothis экрана, в разделе [изменение настроек безопасности](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Установите флажок "hello" рядом слишком**приложение для проверки подлинности** выберите **Настройка**.

    ![кнопку "настроить" Hello на экране параметров проверки безопасности hello](./media/authenticator-app-how-to/azureauthe.png)

    Откроется страница с QR-кодом.

    ![Экран, который предоставляет hello QR-код](./media/authenticator-app-how-to/barcode2.png)
3. Приложение для проверки подлинности Microsoft Open hello. На hello **учетные записи** выберите  **+** , а затем указать, что tooadd рабочей или учебной учетной записи.
4. Используйте камеры tooscan hello hello QR-код, а затем выберите **сделать** tooclose hello QR кода экрана.

    Если камера не работает должным образом, вы можете [вручную введите hello QR-код и URL-адрес](#add-an-account-to-the-app-manually).

5. Когда приложение hello показывает имя учетной записи с шестизначным кодом под ним, процедура завершена. 

    ![Окно с учетными записями](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Вручную добавить приложение toohello учетной записи
1. Откройте экран настройки проверки безопасности toohello.  Сведения о том, как tooget toothis экрана, в разделе [изменение настроек безопасности](multi-factor-authentication-end-user-manage-settings.md).
2. Нажмите кнопку **Настроить**.

    ![кнопку "настроить" Hello на экране параметров проверки безопасности hello](./media/authenticator-app-how-to/azureauthe.png)

    Откроется страница с QR-кодом.  Обратите внимание, кода hello и URL-адрес.

    ![Экран с hello QR-код и URL-адрес](./media/authenticator-app-how-to/barcode2.png)
3. Приложение для проверки подлинности Microsoft Open hello. На hello **учетные записи** выберите  **+** , а затем указать, что tooadd рабочей или учебной учетной записи.

4. В сканер hello, выберите **вручную ввести код**.

    ![Окно для сканирования QR-кода](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Введите в соответствующие поля hello в приложение hello кода hello и hello URL-адрес, а затем выберите **Готово**.

    ![Окно ввода кода и URL-адреса](./media/authenticator-app-how-to/manual.png)

6. Когда приложение hello показывает имя учетной записи с шестизначным кодом под ним, процедура завершена.

    ![Окно с учетными записями](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Добавление приложения toohello учетной записи, с помощью Touch ID
приложение проверки подлинности Microsoft Hello, IOS, поддерживает Touch ID.  Azure Multi-factor Authentication позволяет организациям toorequire ПИН-код для устройств. С Touch ID iOS пользователям нет необходимости tooenter ПИН-код. Вместо этого можно просканировать отпечатки пальцев и нажать кнопку **Утвердить**.

Настройка Touch ID в приложении Microsoft Authenticator выполняется очень просто. Обычная проверка заканчивается вводом ПИН-кода. Если устройство поддерживает Touch ID, Microsoft Authenticator автоматически настроит его для учетной записи.

![Проверка настройки Touch ID](./media/authenticator-app-how-to/touchid1.png)

От момента, когда вы будете необходимые tooverify вход в систему, выберите push-уведомление получено hello и проверять отпечаток пальца вместо ввода ПИН-кода.

![push-уведомление](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Используйте приложение hello при входе

После добавления учетной записи toohello приложения может быть запрос toodo toomake для проверки теста, убедиться, что все было настроено правильно. После этого все будет готово! Не нужно toodo других действий пока hello при очередном входе.

Если вы выбрали toouse кодов проверки в приложение hello, запуске toosee их на домашнюю страницу приветствия. Они изменяются каждые 30 секунд, поэтому при необходимости у вас всегда будет новый код. Но не требуется toodo ничего с ними до входа и являются запрашиваемые tooenter код проверки.  
