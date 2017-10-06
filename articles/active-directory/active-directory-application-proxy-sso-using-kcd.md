---
title: "aaaSingle входа с помощью прокси приложения | Документы Microsoft"
description: "Описывается, как tooprovide единый вход с помощью прокси приложения Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Ограниченное делегирование Kerberos для-tooyour приложений с помощью прокси приложения

Вы можете организовать поддержку единого входа для локальных приложений, опубликованных через прокси приложения и защищенных с использованием встроенной проверки подлинности Windows. Для доступа к таким приложениям нужен билет Kerberos. Прокси приложения использует ограниченное делегирование Kerberos (KCD) toosupport этих приложений. 

Вы можете включить-tooyour приложений с помощью встроенной проверки подлинности Windows (IWA), предоставляя разрешение соединителей прокси приложения в tooimpersonate пользователей Active Directory. соединители Hello использовать это разрешение toosend и получать от их имени маркеры.

## <a name="how-single-sign-on-with-kcd-works"></a>Принцип работы единого входа с применением KCD
Схема иллюстрирует поток hello, когда пользователь пытается tooaccess к локальному приложению, которое использует IWA.

![Схема проверки подлинности Microsoft Azure AD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. Hello пользователь вводит приложения hello URL-адрес tooaccess hello в локальной среде с помощью прокси приложения.
2. Прокси приложения перенаправляет hello запроса tooAzure AD проверки подлинности службы toopreauthenticate. На этом этапе Azure AD применяет все применимые политики проверки подлинности и авторизации, например многофакторную проверку подлинности. Если проверки hello пользователя Azure AD создает маркер и отправляет его toohello пользователя.
3. Hello пользователь передает маркер tooApplication hello прокси-сервера.
4. Прокси приложения проверяет токен hello и извлекает hello имя участника пользователя (UPN) из него, а затем отправляет hello запроса, hello имени участника-пользователя и имя участника службы (SPN) toohello соединитель через безопасный канал двойной проверкой hello.
5. Hello соединитель выполняет согласование ограниченное делегирование Kerberos (KCD) с hello в локальной среде AD, обезличивает пользователя hello tooget приложении toohello маркера Kerberos.
6. Active Directory отправляет маркер Kerberos hello для toohello приложения hello соединителя.
7. Hello соединитель отправляет hello исходного запроса toohello сервера приложений, с использованием маркера Kerberos hello, полученного из AD.
8. приложение Hello отправляет ответ hello toohello соединитель, который затем возвращается toohello прокси-сервера приложения службы и, наконец, toohello пользователя.

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы с единого входа для приложений IWA, убедитесь, что среде готов с hello следующие параметры и конфигурации:

* Приложения, такие как SharePoint веб-приложениям, задаются toouse встроенную проверку подлинности Windows. Дополнительные сведения см. в статье [Включение поддержки протокола проверки подлинности Kerberos](https://technet.microsoft.com/library/dd759186.aspx) или (для SharePoint) в статье [Планирование проверки подлинности Kerberos в SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Все приложения должны иметь [имена субъектов-служб](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* выполнение приветствие сервера Hello соединитель, а сервер hello приложение hello, присоединенных к домену и частью hello того же домена или доверяющих доменов. Дополнительные сведения о присоединении к домену см. в разделе [присоединить компьютер tooa домена](https://technet.microsoft.com/library/dd807102.aspx).
* сервер Hello hello соединителя имеет атрибут TokenGroupsGlobalAndUniversal hello tooread доступ для пользователей. Этот параметр по умолчанию может затронула среды hello усиления безопасности.

### <a name="configure-active-directory"></a>Настройка Active Directory
зависит от конфигурации Active Directory Hello, в зависимости от ли ваш соединитель прокси приложения и приложения hello находятся в hello того же домена, или нет.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Соединитель и сервера приложений в hello того же домена
1. В Active Directory перейдите слишком**средства** > **пользователи и компьютеры**.
2. Выберите сервер hello hello соединителя.
3. Щелкните его правой кнопкой мыши и выберите **Свойства** > **Делегирование**.
4. Выберите **доверять компьютеру делегирование только службы toospecified**. 
5. В разделе **toowhich службы этой учетной записи может представлять делегированные учетные данные** добавьте значение hello hello удостоверение имени участника-службы сервера приложения hello. Это позволяет пользователям tooimpersonate hello соединитель прокси приложения в AD для приложения hello, определенные в списке hello.

   ![Окно свойств соединителя SVR (снимок экрана)](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Соединитель и сервер приложения находятся в разных доменах
1. Список предварительных требований для работы с ограниченным делегированием Kerberos в разных доменах см. в статье [Ограниченное делегирование Kerberos в разных доменах](https://technet.microsoft.com/library/hh831477.aspx).
2. Используйте hello `principalsallowedtodelegateto` свойство hello соединитель сервера tooenable hello прокси приложения toodelegate для сервера соединителя hello. сервер приложений Hello `sharepointserviceaccount` и делегирование сервера hello `connectormachineaccount`. Следующий пример содержит код для Windows 2012 R2:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount может быть учетная запись компьютера сервера SPS hello или учетная запись службы, под которой hello SPS пула приложений.

## <a name="configure-single-sign-on"></a>Настройка единого входа 
1. Опубликуйте приложение в соответствии с toohello инструкциям, описанным в [публикации приложений с помощью прокси приложения](application-proxy-publish-azure-portal.md). Убедитесь, что tooselect **Azure Active Directory** как hello **метод предварительной проверки подлинности**.
2. После появления приложения в списке hello корпоративных приложений, выберите его и нажмите кнопку **единого входа**.
3. Режим hello единого входа слишком**встроенная проверка подлинности Windows**.  
4. Введите hello **SPN внутреннего приложения** hello сервера приложений. В этом примере hello имени участника-службы для нашего опубликованного приложения является http/www.contoso.com. Toobe потребностей этого имени участника-службы в списке hello соединителя hello toowhich службы может представлять делегированные учетные данные. 
5. Выберите hello **делегированы идентификатора имени входа** для hello toouse соединитель от имени пользователей. См. дополнительные сведения о [реализации единого входа в приложения с помощью прокси приложения](#Working-with-different-on-premises-and-cloud-identities).

   ![Дополнительная настройка приложения](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Единый вход для приложений не на базе Windows
Hello поток делегирование Kerberos в прокси приложения Azure AD начинается, когда Azure AD проверяет подлинность пользователя hello в облаке hello. После hello запрос прибывает в локальной среде, hello прокси приложения Azure AD, соединитель выдает билет Kerberos от имени пользователя hello, взаимодействуя с hello локальной службы Active Directory. Этот процесс является ссылка tooas ограниченное делегирование Kerberos (KCD). В hello следующей фазе отправляется запрос toohello внутреннее приложение с Этот билет Kerberos. Существует несколько протоколов, которые определяют, каким образом toosend например запросы. Большинство серверов не на базе Windows ожидают механизм Negotiate/SPNego, который теперь поддерживается в прокси приложения Azure AD.

Дополнительные сведения о протоколе Kerberos см. в разделе [все требуется tooknow о ограниченное делегирование Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Приложения других ОС, кроме Windows, вместо доменных адресов электронной почты обычно используют имена пользователей или имена учетных записей SAM. Такой ситуации применяется tooyour приложений, необходимо tooconfigure hello делегированы входа идентификатора поля tooconnect удостоверениями облака tooyour удостоверения приложения. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Реализация единого входа в приложения с помощью прокси приложения
Прокси приложения предполагает, что пользователи точно hello удостоверением в hello облачных и локальных. Если это не так hello, можно можно по-прежнему использовать ограниченное делегирование Kerberos для единого входа. Настройка **делегированы идентификатора имени входа** для каждого приложения, toospecify личных данных, следует использовать при выполнении единого входа.  

Эта возможность позволяет во многих организациях, которые используют различные локальные и облачные удостоверения toohave единого входа из hello облачных tooon локальных приложений без необходимости пользователей hello tooenter разные имена пользователей и пароли. Сюда относятся следующие виды организаций:

* Внутренне имеют несколько доменов (joe@us.contoso.com, joe@eu.contoso.com) и отдельный домен в облаке hello (joe@contoso.com).
* Внутренне у немаршрутизируемый доменного имени (joe@contoso.usa) и юридические один в облаке hello.
* организации, которые не используют внутренние доменные имена (joe);
* Использование различных псевдонимов в локальной среде и в облаке hello. Например, joe-johns@contoso.com и joej@contoso.com.  

С помощью прокси приложения можно выбрать какие удостоверения toouse tooobtain hello билета Kerberos. Этот параметр устанавливается в каждом отдельном приложении. Некоторые из этих параметров подходят для систем, не поддерживающих значения в формате адреса электронной почты, другие предназначены для альтернативного входа в систему.

![Снимок экрана параметра "Делегированное удостоверение для входа"](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Если используется удостоверение делегированного входа, hello значение может не быть уникальным для всех hello доменов или леса в организации. Этой проблемы можно избежать, опубликовав приложения дважды с использованием двух разных групп соединителей. Поскольку каждое приложение имеет аудитории другого пользователя, можно соединить его соединители tooa другого домена.

### <a name="configure-sso-for-different-identities"></a>Настройка единого входа для использования разных удостоверений
1. Настройте параметры Azure AD Connect, поэтому основное удостоверение hello hello адрес электронной почты (почта). Это можно сделать с частью hello настройки процесса, изменив hello **имя участника-пользователя** в параметры синхронизации hello. Эти параметры определяют, каким образом пользователи вход tooOffice365 устройств Windows 10 и других приложений, использующих Azure AD в качестве хранилища своих удостоверений.  
   ![Снимок экрана "Идентификация пользователей": раскрывающееся меню "Имя участника-пользователя"](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. В параметры конфигурации приложения hello приложения hello хотелось бы toomodify выберите hello **делегированы идентификатора имени входа** toobe используется:

   * имя участника-пользователя (например, joe@contoso.com);
   * дополнительное имя участника-пользователя (например, joed@contoso.local);
   * имя пользователя, входящее в имя участника-пользователя (например, joe);
   * имя пользователя, входящее в дополнительное имя участника-пользователя (например, joed);
   * (Зависит от конфигурации контроллера домена hello) имя учетной записи SAM в локальной среде

### <a name="troubleshooting-sso-for-different-identities"></a>Устранение неполадок единого входа для различных удостоверений
Если имеется ошибка в hello процесс единого входа, он отображается в журнал событий на компьютере соединителя hello как объясняется в [Устранение неполадок](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Однако в некоторых случаях запрос hello успешной отправки toohello внутреннее приложение во время ответа приложения в различных HTTP-ответов. Устранение неполадок в этих случаях необходимо начать с изучения номер события 24029 на компьютере соединителя hello в журнале событий сеанса прокси приложения hello. в поле «user» hello в сведения о событии hello появится Hello удостоверение пользователя, который был использован для делегирования. Выберите tooturn журнала сеанса на **Отобразить аналитический и отладочный журналы** в меню "Вид" средство просмотра событий hello.

## <a name="next-steps"></a>Дальнейшие действия

* [Как tooconfigure toouse приложения прокси приложения ограниченное делегирование Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Устранение неполадок с прокси приложения](active-directory-application-proxy-troubleshoot.md)


Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)

