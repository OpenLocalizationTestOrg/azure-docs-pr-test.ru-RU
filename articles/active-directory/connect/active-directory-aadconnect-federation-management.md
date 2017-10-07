---
title: "Службы федерации Directory aaaActive управления и настройки с Azure AD Connect | Документы Microsoft"
description: "Управление службами AD FS с помощью Azure AD Connect и настройка пользовательского входа в AD FS с помощью Azure AD Connect и PowerShell."
keywords: "AD FS, ADFS, управление AD FS, AAD Connect, Connect, вход, настройка AD FS, восстановление доверия, Office 365, федерация, проверяющая сторона"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect
В этой статье описывается как toomanage и настройте службы федерации Active Directory (AD FS), используя подключение Azure Active Directory (Azure AD). Он также включает другие стандартные задачи AD FS, которые могут потребоваться toodo для завершения настройки фермы AD FS.

| Раздел | Что описывает |
|:--- |:--- |
| **Управление AD FS** | |
| [Восстановите доверие hello](#repairthetrust) |Как федерации hello toorepair доверие с Office 365. |
| [Федерация с Azure AD с помощью альтернативного имени пользователя](#alternateid) | Настройка федерации с использованием альтернативного имени пользователя.  |
| [Добавление сервера AD FS](#addadfsserver) |Каким образом AD FS tooexpand фермы с дополнительного сервера AD FS. |
| [Добавление прокси-сервера веб-приложения AD FS](#addwapserver) |Каким образом AD FS tooexpand фермы с дополнительного сервера прокси-сервера веб-приложения (WAP). |
| [Добавление федеративного домена](#addfeddomain) |Как tooadd федеративный домен. |
| [Обновить сертификат SSL hello](active-directory-aadconnectfed-ssl-update.md)| Как tooupdate hello SSL сертификат для фермы AD FS. |
| **Настройка AD FS** | |
| [Добавление настраиваемого логотипа компании или иллюстрации](#customlogo) |Как войти toocustomize AD FS страницы с эмблемой компании и иллюстрации. |
| [Добавление описания входа в систему](#addsignindescription) |Как tooadd входа в странице описания. |
| [Изменение правил утверждений служб федерации Active Directory](#modclaims) |Как toomodify AD FS утверждений для различных сценариев федерации. |

## <a name="manage-ad-fs"></a>Управление AD FS
В Azure AD Connect с минимальным участием пользователя выполнять различные задачи AD FS связанные с помощью мастера hello Azure AD Connect. После завершения установки Azure AD Connect выполнения мастером hello hello мастер можно запустить снова tooperform дополнительные задачи.

## Восстановите доверие hello<a name=repairthetrust></a>
Можно использовать Azure AD Connect toocheck hello текущее состояние работоспособности hello AD FS и отношение доверия Azure AD и выполнить соответствующие действия toorepair hello доверия. Выполните эти шаги toorepair Azure AD и AD FS доверия.

1. Выберите **AAD восстановления и доверия ADFS** списке hello дополнительные задачи.
   ![Восстановление доверия AAD и ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. На hello **подключения tooAzure AD** , введите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.
   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. На hello **учетные данные для удаленного доступа** введите hello учетные данные администратора домена hello.

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Когда вы нажмете кнопку **Далее**, Azure AD Connect проверит работоспособность сертификата и отобразит возможные проблемы.

    ![Состояние сертификатов](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Hello **готовности tooconfigure** страница hello показан список действий, которые будут выполнены toorepair hello доверия.

    ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Нажмите кнопку **установить** toorepair hello доверия.

> [!NOTE]
> Azure AD Connect может выполнить восстановление или другие действия только для самозаверяющих сертификатов. С помощью Azure AD Connect нельзя восстановить сертификаты третьих сторон.

## Федерация с Azure AD с помощью альтернативного имени пользователя <a name=alternateid></a>
Рекомендуется, hello локальной Name(UPN) участника-пользователя и облака hello, имя участника-пользователя хранятся hello таким же. Если hello локального имени участника-пользователя используется немаршрутизируемый домена (например,). Contoso.local) или не может быть изменен из-за зависимостей приложения toolocal, рекомендуется настроить альтернативное имя пользователя. Альтернативного идентификатора входа позволяет tooconfigure входа пользователей где пользователи могут войти под атрибут, отличный от их имени участника-пользователя, например, почту. Hello Выбор для имени участника-пользователя в Azure AD Connect атрибут userPrincipalName toohello значения по умолчанию в Active Directory. Если выбрать для имени участника-пользователя любой другой атрибут и выполнить федерацию с помощью AD FS, то Azure AD Connect настроит AD FS на использование альтернативного имени пользователя. В приведенном ниже примере показано, как выбрать другой атрибут для имени участника-пользователя.

![Выбор альтернативного атрибута имени пользователя](media/active-directory-aadconnect-federation-management/attributeselection.png)

Настройка альтернативного имени пользователя для AD FS состоит из двух основных этапов:
1. **Настройка hello правильный набор утверждений для выдачи**: hello правил утверждений выдачи в проверяющей стороне hello Azure AD доверии toouse измененный атрибут UserPrincipalName hello выбран как hello альтернативного идентификатора пользователя hello.
2. **Включение альтернативного идентификатора входа в конфигурации AD FS hello**: hello AD FS конфигурации обновляется, чтобы службы федерации Active Directory можно найти пользователей в соответствующие лесах hello, используя hello альтернативный идентификатор. Эта конфигурация поддерживается для службы AD FS, работающей под управлением Windows Server 2012 R2 (с обновлением KB2919355) и более поздних версий. Если серверы hello AD FS 2012 R2, Azure AD Connect проверяет наличие hello hello требуется КБ. Если hello КБ не обнаруживается, предупреждение будет отображаться после завершения настройки, как показано ниже:

    ![Предупреждение об отсутствии обновления в версии 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    Конфигурация hello toorectify в случае отсутствующих КБ, установите необходимые hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) и затем восстановить с помощью доверия hello [восстановить AAD и отношение доверия AD FS](#repairthetrust).

> [!NOTE]
> Дополнительные сведения о toomanually alternateID и шаги настройки, чтение [настройка альтернативного идентификатора входа](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Добавление сервера AD FS <a name=addadfsserver></a>

> [!NOTE]
> сервер AD FS tooadd Azure AD Connect требуется hello PFX-сертификат. Таким образом можно выполнить эту операцию только в том случае, если вы настроили фермы hello AD FS с помощью Azure AD Connect.

1. Выберите пункт **Развернуть дополнительный сервер федерации** и нажмите кнопку **Далее**.

   ![Дополнительный сервер федерации](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. На hello **подключения tooAzure AD** введите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Укажите учетные данные администратора домена hello.

   ![Учетные данные администратора домена](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect запрашивает пароль hello hello PFX-файл, указанный при настройке новой ферме AD FS с Azure AD Connect. Нажмите кнопку **ввод пароля** tooprovide hello пароль для PFX-файла hello.

   ![Пароль сертификата](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. На hello **серверов AD FS** введите hello имя сервера или IP адрес toobe добавлены фермы toohello AD FS.

   ![Серверы AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Нажмите кнопку **Далее**и ознакомиться со статьей hello окончательного **Настройка** страницы. После завершения добавления toohello AD FS hello серверы фермы Azure AD Connect будет предоставлена tooverify hello hello параметр подключения.

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Установка завершена](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Добавление WAP-сервера AD FS <a name=addwapserver></a>

> [!NOTE]
> tooadd WAP-сервера Azure AD Connect требуется hello PFX-сертификат. Таким образом можно выполнять только операции при настройке фермы hello AD FS с помощью Azure AD Connect.

1. Выберите **развернуть прокси веб-приложения** hello списке доступных задач.

   ![Развертывание прокси-службы веб-приложения](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Укажите учетные данные глобальный администратор Azure hello.

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. На hello **укажите SSL-сертификат** укажите hello пароль для PFX-файла hello, указанный при настройке фермы hello AD FS с Azure AD Connect.
   ![Пароль сертификата](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Добавьте сервер toobe hello, добавления в качестве сервера WAP. Hello WAP-сервера могут быть присоединены к домену toohello домена, hello мастер запрашивает добавляемом сервере toohello учетные данные администратора.

   ![Учетные данные администратора сервера](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. На hello **учетные данные прокси-сервера доверия** укажите учетные данные администратора tooconfigure hello прокси доверия и доступа hello основной сервер в ферме AD FS hello.

   ![Учетные данные доверия прокси-сервера](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. На hello **готовности tooconfigure** странице приветствия мастера отображаются hello список действий, которые будут выполнены.

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Нажмите кнопку **установить** toofinish hello конфигурации. После завершения настройки hello, предоставляет мастер hello hello tooverify параметр hello серверов toohello подключения. Нажмите кнопку **проверьте** toocheck подключения.

   ![Установка завершена](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Добавление федеративного домена <a name=addfeddomain></a>

Это легко tooadd toobe домена в федерацию с Azure AD с помощью Azure AD Connect. Azure AD Connect добавляет hello домен для федерации и изменяет hello утверждений, правила toocorrectly отражают hello издателя при наличии нескольких доменов в федерацию с Azure AD.

1. tooadd федеративный домен, выберите hello задач **добавить дополнительный домен Azure AD**.

   ![Дополнительный домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. На следующей странице приветствия мастера hello укажите учетные данные глобального администратора hello в Azure AD.

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. На hello **учетные данные для удаленного доступа** укажите учетные данные администратора домена hello.

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. На следующей странице приветствия hello мастер предоставляет список доменов Azure AD, которые можно создать федерацию с вашего локального каталога. Выберите домен hello из списка hello.

   ![Домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    После выбора домена hello hello мастером вам соответствующую информацию о дальнейших действиях, которые мастер hello примет и влияние настроек hello hello. В некоторых случаях при выборе домена, не еще выполняется в Azure AD hello мастер предоставляет сведения о toohelp проверьте hello домена. В разделе [добавить ваш tooAzure имя пользовательского домена Active Directory](../active-directory-add-domain.md) для получения дополнительных сведений.

5. Щелкните **Далее**. Hello **готовности tooconfigure** странице отображаются hello список действий, которые выполняют Azure AD Connect. Нажмите кнопку **установить** toofinish hello конфигурации.

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Добавить пользователей из hello федеративного домена должна быть синхронизирована, прежде чем их можно будет toologin tooAzure AD.

## <a name="ad-fs-customization"></a>Пользовательская настройка AD FS
Hello следующие разделы содержат сведения о распространенных задач hello, возможно, tooperform во время настройки страницы входа AD FS.

## Добавление настраиваемого логотипа компании или иллюстрации <a name=customlogo></a>
Эмблема hello toochange hello компании, которая отображается на hello **входа** , используйте следующий командлет Windows PowerShell и синтаксисом hello.

> [!NOTE]
> Здравствуйте, рекомендуется измерения для hello логотипа — 260 x 35 @ 96 точек на дюйм. размер файла не должен превышать 10 КБ.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Hello *TargetName* является обязательным. имя по умолчанию — тема по умолчанию Hello, предоставляемая в AD FS.

## Добавление описания входа в систему <a name=addsignindescription></a>
tooadd toohello описание страницы входа **страницы входа**, используйте следующий командлет Windows PowerShell и синтаксисом hello.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Изменение правил утверждений служб федерации Active Directory <a name=modclaims></a>
Службы федерации Active Directory поддерживает языка форматированного утверждений, который можно использовать toocreate пользовательские правила утверждений. Дополнительные сведения см. в разделе [hello роль языка правил утверждений hello](https://technet.microsoft.com/library/dd807118.aspx).

Hello следующих разделах описаны как можно создавать настраиваемые правила для некоторых сценариев, связывающие tooAzure AD и федерации AD FS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Неизменяемый идентификатор условного по значению их присутствия в атрибуте hello
Azure AD Connect позволяет указать атрибут toobe использовать привязку к источнику, если объекты — синхронизироваться tooAzure AD. Если hello значения настраиваемого атрибута hello не пуст, вы можете tooissue утверждение неизменяемый идентификатор.

Например, можно выбрать **ms-ds-consistencyguid** как атрибут hello для привязки источника hello и проблема **ImmutableID** как **ms-ds-consistencyguid** в вариантов hello атрибут имеет значение для нее. Если нет значения для атрибута hello, отправить **objectGuid** как hello неизменяемый идентификатор. Вы можете создать hello набор настраиваемых правил утверждений, как описано в следующем разделе hello.

**Правило 1. Атрибуты запросов**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

В этом правиле выполняется запрос значения hello **ms-ds-consistencyguid** и **objectGuid** для hello пользователя из Active Directory. Измените имя hello хранилища имя tooan соответствующее хранилище в развертывание AD FS. Также изменить тип утверждения, соответствующие tooa типа утверждений hello для федерации, согласно его определению **objectGuid** и **ms-ds-consistencyguid**.

Кроме того, с помощью **добавить** и не **проблему**, следует избегать добавления исходящего проблемы для сущности hello и hello значения можно использовать как промежуточные значения. Будет выдавать hello утверждения в правиле более поздней версии, после установления какие toouse значение как hello неизменяемый идентификатор.

**Правило 2: Проверьте, существует ли ms-ds-consistencyguid для пользователя hello**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Это правило определяет временной пометку **idflag** , задано слишком**useguid** при наличии не **ms-ds-consistencyguid** заполняется для пользователя hello. Hello смысл этого заключается в hello тем, что службы федерации Active Directory не разрешают пустой утверждений. Поэтому при добавлении утверждений http://contoso.com/ws/2016/02/identity/claims/objectguid и http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid правила 1, вы получаете **msdsconsistencyguid** только если утверждения значение Hello заполняется для пользователя hello. Если оно не заполнено, службы AD FS определяют, что значение окажется пустым, и немедленно его опускают. **objectGuid**имеют все объекты, поэтому такое утверждение всегда будет присутствовать после выполнения правила 1.

**Правило 3. Выдача ms-ds-consistencyguid в качестве неизменяемого идентификатора, если он присутствует**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Это неявная проверка **Exist** . Если существует значение hello для утверждения hello, затем выполните, как hello неизменяемый идентификатор. Hello в предыдущем примере hello **nameidentifier** утверждения. Вы получите toochange типа toohello соответствующие утверждения для hello неизменяемый идентификатор в вашей среде.

**Правило 4. Выдача objectGuid в качестве неизменяемого идентификатора при отсутствии ms-ds-consistencyGuid**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

В этом правиле, просто выполняется проверка hello временные флаг **idflag**. Принято, основаны ли tooissue hello утверждения на его значение.

> [!NOTE]
> Важно соблюдать последовательность Hello этих правил.

### <a name="sso-with-a-subdomain-upn"></a>Единый вход с помощью UPN поддомена
Можно добавить несколько toobe домена федерации с помощью Azure AD Connect, как описано в [добавьте новый федеративный домен](active-directory-aadconnect-federation-management.md#addfeddomain). Утверждение имени участника (UPN) пользователя hello необходимо изменить, чтобы hello ИД издателя соответствует toohello корневого домена, а не hello дочерний домен, поскольку hello федеративной корневого домена также охватывает дочерний hello.

По умолчанию hello правил утверждений для издателя, как будет задан ИД:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Утверждение идентификатора издателя по умолчанию](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

правило по умолчанию Hello принимает суффикс UPN hello и использует его в утверждение идентификатора издателя hello. Предположим, Григорий является пользователем в домене sub.contoso.com, а contoso.com включен в федерацию с Azure AD. Вводит Джон john@sub.contoso.com как hello имя пользователя при входе в tooAzure AD. правило утверждения идентификатор издателя по умолчанию Hello в AD FS обработает его в hello, следуя способом:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Значение утверждения:** http://sub.contoso.com/adfs/services/trust/.

toohave только hello корневого домена hello поставщиком значение утверждения, измените hello утверждения правило toomatch hello следующее.

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Дальнейшие действия
См. [дополнительные сведения о параметрах входа пользователя](active-directory-aadconnect-user-signin.md).
