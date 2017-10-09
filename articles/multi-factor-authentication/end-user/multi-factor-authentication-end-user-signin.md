---
title: "вход aaaAzure многофакторной проверки Подлинности с помощью двухэтапной проверки | Документы Microsoft"
description: "Эта страница предоставит рекомендации на где toogo toosee hello вход методов, доступных с помощью Azure MFA."
keywords: "проверка подлинности пользователя, вход в систему, вход с помощью мобильного телефона, вход с помощью рабочего телефона"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Hello входа в систему с многофакторной проверкой подлинности Azure
> [!NOTE]
> Hello в этой статье предназначен toowalk через стандартные входа в систему. Справку по вход в систему или tootroubleshoot проблем см. в разделе [возникли трудности с многофакторной проверкой подлинности Azure](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Каким будет ваш вариант входа
Процедура входа отличается в зависимости от того, какое значение выбрано toouse как ваш второго фактора: телефонный звонок, тексты или приложения проверки подлинности. Выберите параметр hello, наиболее точно описывающий действиях:

| Как вы входите в учетную запись? | 
| --- |
| [С помощью телефонного звонка toomy мобильный или рабочий телефон](#signing-in-with-a-phone-call) |
| [С помощью SMS на мобильный телефон toomy](#signing-in-with-a-text-message)
| [С помощью уведомления в приложение для проверки подлинности Microsoft hello](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [С помощью кодов подтверждения из приложения hello проверки подлинности Майкрософт](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [С помощью другого метода, так как я не могу использовать прямо сейчас основной вариант](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Вход с помощью телефонного звонка
Hello следующую информацию описывает hello двухэтапный проверки и опыт работы с мобильными tooyour вызова или рабочий телефон.

1. Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.  
2. Вам поступит звонок от корпорации Майкрософт.  
3. Ответить на телефонный hello и нажмите клавишу # hello.  

## <a name="signing-in-with-a-text-message"></a>Вход с помощью текстового сообщения
Hello следующую информацию описывается hello двухэтапный проверки взаимодействие с мобильным телефоном tooyour текст сообщения:

1. Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль. 
2. Корпорация Майкрософт отправляет текстовое сообщение, содержащее числовой код. 
3. Введите в поле на странице входа hello hello hello код. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Вход в приложение для проверки подлинности Microsoft hello 
Hello следующие данные описывают hello работы с приложением для проверки подлинности Microsoft hello для двухшаговой проверки. Существует приложение hello toouse двумя различными способами. Вы можете получать push-уведомлений на устройства или tooget приложения hello код проверки можно открыть.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign вход с помощью уведомления от приложения hello проверки подлинности Майкрософт
1. Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.
2. Майкрософт отправляет приложением проверки подлинности Microsoft toohello уведомления на вашем устройстве.

  ![Майкрософт отправляет уведомление](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Откройте hello уведомления на телефон и выберите hello **проверьте** ключа. Если компания требует ввода ПИН-кода, укажите его.
4. После этого вы войдете в систему.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign использовать код проверки с приложением для проверки подлинности Microsoft hello

При использовании кодов проверки tooget приложение проверки подлинности Microsoft hello, затем при открытии приложение hello появляются в списке имя учетной записи. Этот номер изменяется каждые 30 секунд, чтобы не использовать одно и тоже число дважды hello. В ответ на запрос проверки кода, откройте приложение "hello" и использовать независимо от значения в текущий момент отображается. 

1. Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.
2. Вам будет предложено ввести код проверки.

  ![Введите код проверки](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Откройте приложение проверки подлинности Microsoft hello на телефоне и введите код hello в поле hello, где вы входите.

## <a name="signing-in-with-an-alternate-method"></a>Вход с помощью альтернативного метода
Иногда у вас нет hello phone или устройства, настроенные как проверки предпочтительный метод. Именно поэтому мы рекомендуем настроить резервный метод проверки подлинности для учетной записи. Hello следующем разделе показано, как toosign с альтернативным способом при основного способа могут быть недоступны.

1. Войдите в tooan приложения или службы, такие как Office 365, используя имя пользователя и пароль.
2. Выберите **Использовать другой вариант проверки**. Вы увидите другие варианты проверки, число которых зависит от ваших настроек.
3. Выберите альтернативный метод и войдите.

  ![Использовать другой метод](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Дальнейшие действия

Если у вас возникли проблемы при входе в систему с помощью двухфакторной проверки подлинности, см. статью [Проблемы с двухфакторной проверкой подлинности](multi-factor-authentication-end-user-troubleshoot.md).

Узнайте, каким образом слишком[управление параметры двухшаговой проверки](multi-factor-authentication-end-user-manage-settings.md).

Узнайте, как слишком[Приступая к работе с приложением для проверки подлинности Microsoft hello](microsoft-authenticator-app-how-to.md) , чтобы можно было использовать toosign уведомления, вместо текстов и телефонные звонки. 
