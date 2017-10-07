---
title: "Облачные ресурсы aaaSecure с Azure MFA и AD FS | Документы Microsoft"
description: "Это страница hello Azure многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA и AD FS в облаке hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Защита облачных ресурсов с помощью Azure Multi-Factor Authentication и AD FS
Если в организации настроена федерация с Azure Active Directory, используйте Azure Multi-factor Authentication или служб федерации Active Directory (AD FS) toosecure ресурсы, к которым обращаются Azure AD. Используйте следующие процедуры ресурсов Azure Active Directory toosecure с Azure Multi-factor Authentication или служб федерации Active Directory hello.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Защита ресурсов Azure AD с помощью AD FS
toosecure ресурса облака, настроить правило для утверждений, чтобы службы федерации Active Directory выдает утверждение multipleauthn hello, когда пользователь успешно выполняет двухшаговую проверку. Это утверждение будет передано в tooAzure AD. Выполните это процедура toowalk шаги hello.


1. Откройте оснастку управления AD FS.
2. В левой части экрана приветствия выберите **доверия с проверяющей стороной**.
3. Щелкните правой кнопкой мыши **Платформа удостоверений Microsoft Office 365** и выберите **Изменить правила утверждений**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. На Здравствуйте преобразования мастера добавления правила утверждения, выберите **пропуск или Фильтрация входящего утверждения** из hello раскрывающегося списка и нажмите кнопку **Далее**.

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Укажите имя правила. 
7. Выберите **ссылки на методы проверки подлинности** тип hello входящего утверждения.
8. Щелкните **Пройти по всем значениям утверждений**.
    ![Мастер добавления правила преобразования утверждений](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Нажмите кнопку **Готово** Закройте консоль управления FS hello AD.

## <a name="trusted-ips-for-federated-users"></a>Доверенные IP-адреса для федеративных пользователей
Надежные IP-адреса Администраторы на этапе tooby двухшаговую проверку для конкретных IP-адресов или для федеративных пользователей, имеющих запросов, исходящих из собственной интрасети. Hello ниже описано, как tooconfigure Azure многофакторной проверки подлинности надежных IP-адресов с помощью федеративных пользователей и обойти двухшаговую проверку, когда запрос исходит от в интрасети федеративных пользователей. Это достигается путем настройки AD FS toouse транзитного или фильтрации входящего шаблона утверждения с hello типа утверждения внутри корпоративной сети.

В этом примере для доверенных отношений с проверяющей стороной используется Office 365.

### <a name="configure-hello-ad-fs-claims-rules"></a>Настройка правил утверждений AD FS hello
Первое Hello нам нужно toodo — утверждений tooconfigure hello AD FS. Создание двух правил для утверждений, один для hello внутри корпоративной сети утверждений типа и дополнительное для сохранения пользователей в системе.

1. Откройте оснастку управления AD FS.
2. В левой части экрана приветствия выберите **доверия с проверяющей стороной**.
3. Щелкните правой кнопкой мыши **Microsoft Office 365 Identity Platform** (Платформа идентификации Microsoft Office 365) и выберите **Изменить правила утверждений...**
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. На Здравствуйте преобразования мастера добавления правила утверждения, выберите **пропуск или Фильтрация входящего утверждения** из hello раскрывающегося списка и нажмите кнопку **Далее**.
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. В hello поле Далее tooClaim имя правила присвойте правилу имя. Пример: InsideCorpNet.
7. Из hello раскрывающегося списка, далее tooIncoming тип утверждения, выберите **внутри корпоративной сети**.
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Нажмите кнопку **Готово**
9. На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.
10. На Здравствуйте преобразования мастера добавления правила утверждения, выберите **Отправка утверждений с помощью настраиваемого правила** из hello раскрывающегося списка и нажмите кнопку **Далее**.
11. В окне приветствия под именем правила утверждений: введите *сохранить пользователей подписаны в*.
12. В hello пользовательские правила введите:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Нажмите кнопку **Готово**
14. Нажмите кнопку **Применить**.
15. Нажмите кнопку **ОК**.
16. Откройте оснастку управления AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Настройка Multi-Factor Authentication с доверенными IP-адресами в Azure для федеративных пользователей
Теперь, когда hello утверждения будут на месте, можно настроить надежные IP-адреса.

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. В левой части экрана приветствия щелкните **Active Directory**.
3. В каталоге выберите каталог hello, где требуется tooset копирование надежные IP-адреса.
4. На hello выбранном вами каталоге нажмите **Настройка**.
5. В разделе hello многофакторной проверки подлинности щелкните **Управление параметрами службы**.
6. На странице настройки службы hello в списке надежных IP-адресов, выберите **пропустить / Multi-factor-authentication для запросов от федеративных пользователей из моей интрасети**.  

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Щелкните **Сохранить**.
8. После применения обновления hello щелкните **закрыть**.

Это все! На этом этапе федеративные пользователи Office 365 должна иметь только toouse многофакторной проверки Подлинности когда утверждения приходят из вне корпоративной интрасети hello.
