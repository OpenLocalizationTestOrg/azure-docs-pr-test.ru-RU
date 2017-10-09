---
title: "Azure AD Connect: принципы проектирования | Документация Майкрософт"
description: "В этой статье описываются факторы, которые необходимо учитывать при проектировании реализации."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: принципы проектирования
Hello в этом разделе предназначена toodescribe областей, которые необходимо рассматривать во время разработки реализации hello из Azure AD Connect. Здесь подробно рассмотрены некоторые вопросы, но часть из них вкратце рассмотрена в других статьях.

## <a name="sourceanchor"></a>sourceAnchor
атрибут sourceAnchor Hello определен как *неизменяемый во время существования hello объекта атрибута*. Однозначно определяет объект как hello один объектов в локальной среде и в Azure AD. атрибут Hello также называется **immutableId** и hello двух имена используются взаимозаменяемыми.

Hello слово, неизменяемый, которое является «не может быть изменен», раздел важные toothis. Поскольку значение этого атрибута нельзя изменить после его задания, она будет toopick важно разработать проект, который поддерживает вашего сценария.

Hello атрибут используется для hello следующие сценарии:

* При создании нового сервера синхронизации или его пересоздании после аварийного восстановления: в таком случае этот атрибут связывает существующие объекты в Azure AD с локальными объектами.
* Если переместить из модели только для облака удостоверения tooa синхронизированные удостоверения, то этот атрибут позволяет объектам слишком существующие объекты в Azure AD с локальными объектами «жестких соответствия».
* Если вы используете федерации, то этот атрибут, а также hello **userPrincipalName** используется в hello утверждения toouniquely идентификации пользователя.

В этом разделе рассказывается о sourceAnchor, только по отношению toousers. Hello применяются те же правила tooall типы объектов, но он предназначен только для пользователей, что это проблема обычно возникает.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Выбор значений атрибута sourceAnchor.
значение атрибута Hello должно соответствовать правилам hello:

* Его длина должна быть меньше 60 символов.
  * Символы, отличные от a–z, A–Z или 0–9, кодируются, и каждый из них считается как три символа.
* Оно не должно содержать специальные символы: &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Оно должно быть глобально уникальным.
* Значение должно относиться к строковому, целочисленному или двоичному типу.
* Значение не должно быть основано на имени пользователя.
* Значение не должно быть с учетом регистра и содержать значения, которые изменяются в зависимости от регистра.
* Следует назначить при создании hello объекта

Если hello выбран sourceAnchor не типа String и tooensure значение атрибута hello Base64Encode подключения Azure AD не имеются специальные знаки. При использовании другого сервера федерации, чем служб федерации Active Directory, убедитесь, что сервер может также атрибут Base64Encode hello.

атрибут sourceAnchor Hello учитывается регистр. Значение «АБВГД» не является hello такой же, как «АБВГД». При этом не стоит создавать два объекта, имена которых отличаются только регистром.

При наличии одного леса является локальной, затем атрибута hello, следует использовать **objectGUID**. Это атрибут hello, используется, если используются стандартные параметры в Azure AD Connect и также hello атрибуте, используемом DirSync.

Если вы используете несколько лесов и не перемещайте пользователей между лесами и доменами, затем **objectGUID** toouse хорошо атрибута даже в этом случае является.

При перемещении пользователей между доменами и лесами, затем необходимо найти атрибут, который не изменяется, или можно переместить с пользователями hello во время перемещения hello. Рекомендуемый подход — toointroduce искусственных атрибута. Для этого подходит атрибут, который может содержать что-нибудь наподобие идентификатора GUID. При создании объекта новый идентификатор GUID создается и меткой hello пользователя. Правило пользовательских синхронизации может быть создано в hello синхронизации ядра сервера toocreate значение в зависимости от hello **objectGUID** и обновление hello выбранного атрибута в ADDS. При перемещении hello объекта, делает содержимое hello копирования tooalso убедиться, что это значение.

Другим решением является toopick существующий атрибут, вы знаете, не изменяется. Зачастую можно использовать атрибут **employeeID**. Если вы рассматриваете атрибут, который содержит буквы, убедитесь, что не вероятность hello регистр (верхний и нижний регистр) можно изменить для значения атрибута hello. Неверные атрибуты, которые не должны использоваться включить эти атрибуты с именем hello hello пользователя. В семье или divorce используется имя hello ожидаемый toochange, что не допускается для этого атрибута. Кроме того, это одна из причин почему атрибуты, такие как **userPrincipalName**, **mail**, и **targetAddress** не возможно также tooselect в установке hello Azure AD Connect мастер. Эти атрибуты также содержат hello «@» символ, что не допускается в hello sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Изменения атрибута sourceAnchor hello
значение атрибута sourceAnchor Hello не может изменяться после создания hello объекта в Azure AD и синхронизации удостоверений hello.

По этой причине hello следующие ограничения применяются tooAzure AD Connect:

* атрибут sourceAnchor Hello можно задать только во время первоначальной установки. При повторном запуске мастера установки hello, этот параметр доступен, только для чтения. Если вам требуется toochange этот параметр, необходимо удалить и переустановить.
* При установке другого сервера Azure AD Connect, то необходимо выбрать hello предыдущих же атрибут sourceAnchor. Если вы ранее использовали DirSync и переместите tooAzure AD подключиться, необходимо использовать **objectGUID** это hello атрибуте, используемом DirSync.
* При изменении значения hello для sourceAnchor после hello объекта экспортированного tooAzure AD, затем Azure AD Connect sync вызывает ошибку и не позволяет использовать новые изменения для этого объекта перед hello проблема была исправлена и обратно в hello изменяется hello sourceAnchor исходный каталог.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Использование msDS-ConsistencyGuid в качестве sourceAnchor
По умолчанию, Azure AD Connect (версия 1.1.486.0 и более ранних версий) использует objectGUID в качестве атрибута sourceAnchor hello. ObjectGUID создается системой. Его значение не указывается при создании локальных объектов AD. Как описано в разделе [sourceAnchor](#sourceanchor), существуют сценарии, где необходимо получить значение sourceAnchor toospecify hello. Если применимо tooyou сценарии hello, необходимо использовать настраиваемый атрибут AD (например, атрибут msDS-ConsistencyGuid) как атрибут sourceAnchor hello.

Azure AD Connect (версия 1.1.524.0 и после) теперь облегчает использование hello msDS-ConsistencyGuid в качестве атрибута sourceAnchor. При использовании этой функции, Azure AD Connect автоматически настраивает hello правилах синхронизации:

1. Используйте атрибут msDS-ConsistencyGuid как атрибут sourceAnchor hello для пользовательских объектов. Для других типов объектов используется ObjectGUID.

2. Для любой заданной локального пользователя AD, атрибут msDS-ConsistencyGuid не заполнено, Azure AD Connect записывает его атрибут msDS-ConsistencyGuid задней toohello значение objectGUID в локальной Active Directory объект. После заполнения атрибута msDS-ConsistencyGuid hello Azure AD Connect затем экспортирует tooAzure hello объекта AD.

>[!NOTE]
> Один раз в локальной среде AD импортируется в Azure AD Connect (который импортируется в пространство соединителя AD hello и проецируются в метавселенной hello), больше нельзя изменить его значение sourceAnchor. значения sourceAnchor hello toospecify для заданного локального AD объекта, настройте его атрибут msDS-ConsistencyGuid перед его импортом в Azure AD Connect.

### <a name="permission-required"></a>Требования к разрешениям
Для этого toowork функция toosynchronize учетная запись, используемая hello AD DS с локальной Active Directory должны быть предоставлены атрибут msDS-ConsistencyGuid toohello разрешения записи в локальной Active Directory.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Как tooenable hello функция ConsistencyGuid - новой установки
Во время новой установки, можно включить использование hello ConsistencyGuid в качестве sourceAnchor. В этом разделе подробно описывается экспресс- и пользовательская установка.

  >[!NOTE]
  > Только более новые версии Azure AD Connect (1.1.524.0 и после) поддерживает использование в качестве sourceAnchor ConsistencyGuid hello во время новой установки.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Как tooenable hello ConsistencyGuid-функция
В настоящее время hello функцию можно включить только во время новой установки Azure AD Connect только.

#### <a name="express-installation"></a>Экспресс-установка
При установке Azure AD Connect с режимом экспресс-выпуск, hello Azure AD Connect мастер автоматически определяет toouse hello наиболее Подходящие атрибут как атрибут sourceAnchor hello, с помощью hello следующая логика:

* Во-первых hello Azure AD Connect мастера запросов в атрибуте hello AD tooretrieve клиента Azure AD используются в качестве hello атрибут sourceAnchor в установке hello предыдущих Azure AD Connect (если таковые имеются). Если эта информация доступна, Azure AD Connect использует атрибут hello же AD.

  >[!NOTE]
  > Только более новые версии Azure AD Connect (1.1.524.0 и после) в клиенте Azure AD хранит сведения о hello sourceAnchor атрибут, используемый во время установки. Более ранние версии Azure AD Connect этого не делают.

* Если сведения о hello sourceAnchor атрибут, используемый недоступно, мастер hello проверяет состояние hello атрибут msDS-ConsistencyGuid hello в локальной службе Active Directory. Если атрибут hello не настроен для любого объекта в каталоге hello, hello мастер использует hello msDS-ConsistencyGuid как атрибут sourceAnchor hello. Атрибут hello, настроенных на один или несколько объектов в каталоге hello, мастер hello завершается hello атрибут используется другими приложениями и не может использоваться как атрибут sourceAnchor...

* В этом случае мастер hello возвращается toousing objectGUID как атрибут sourceAnchor hello.

* После решено атрибут sourceAnchor hello hello мастер сохраняет hello сведения в клиенте Azure AD. Hello информация будет использоваться будущих установки Azure AD Connect.

После завершения установки экспресс-выпуск hello мастер сообщает, выбравший какой атрибут как атрибут источника привязки hello.

![Мастер сообщает атрибут AD, выбранный для sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Выборочная установка
При установке Azure AD Connect с пользовательский режим, мастер Azure AD Connect hello обеспечивает два варианта при настройке атрибут sourceAnchor.

![Выборочная установка: настройка sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Настройка | Описание |
| --- | --- |
| Платформа Azure управление hello источник привязки | Выберите этот параметр, если требуется атрибут hello toopick Azure AD для вас. Если этот параметр выбран, мастер применяет Azure AD Connect hello же [логику выбора атрибута sourceAnchor, используемых во время установки Express](#express-installation). Аналогичные tooExpress установки, приветствия мастера о том, какой атрибут был выбравший как hello атрибут привязки источника после завершения выборочной установки. |
| Определенный атрибут | Выберите этот параметр, при желании toospecify существующие AD атрибут как атрибут sourceAnchor hello. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Как tooenable hello функция ConsistencyGuid - существующего развертывания
При наличии существующего развертывания Azure AD Connect, который использует objectGUID в качестве источника привязки атрибута hello, можно переключить его toousing ConsistencyGuid вместо него.

>[!NOTE]
> Только более новые версии Azure AD Connect (1.1.552.0 и после) поддерживает переключение с tooConsistencyGuid ObjectGuid как атрибут источника привязки hello.

tooswitch из tooConsistencyGuid objectGUID как атрибут источника привязки hello:

1. Запустите мастер hello Azure AD Connect и нажмите кнопку **Настройка** toogo toohello задачи экрана.

2. Выберите hello **Настройка привязки источника** задач параметр и нажмите кнопку **Далее**.

   ![Включение ConsistencyGuid для существующего развертывания — шаг 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Введите учетные данные администратора Azure AD и нажмите кнопку **Далее**.

4. Мастер Azure AD Connect анализирует hello состояние атрибута msDS-ConsistencyGuid hello в локальной службе Active Directory. Если атрибут hello не настроен на любой объект в каталоге, Azure AD Connect завершается, что никакое другое приложение использует в настоящее время атрибут hello и является безопасным toouse приветствия его как атрибут источника привязки hello. Нажмите кнопку **Далее** toocontinue.

   ![Включение ConsistencyGuid для существующего развертывания — шаг 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. В hello **готовности tooConfigure** щелкните **Настройка** изменение конфигурации toomake hello.

   ![Включение ConsistencyGuid для существующего развертывания — шаг 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. После завершения настройки hello, мастер hello указывает, что этот атрибут msDS-ConsistencyGuid теперь используется как атрибут источника привязки hello.

   ![Включение ConsistencyGuid для существующего развертывания — шаг 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Во время анализа hello (этап 4) атрибут hello, настроенных на один или несколько объектов в каталоге hello приветствия мастера завершается hello атрибута используется другим приложением и возвращает сообщение об ошибке, как показано на следующей схеме hello. Если вы уверены, что этот атрибут hello не используется средством существующих приложений, сведения о как toosuppress hello ошибки необходимо toocontact поддержки.

![Включение ConsistencyGuid для существующего развертывания — ошибка](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Влияние на конфигурацию AD FS или федерацию сторонних поставщиков
Если вы используете Azure AD Connect toomanage локального развертывания AD FS, hello Azure AD Connect автоматически обновляет атрибут hello же AD toouse правила утверждения hello как sourceAnchor. Это обеспечивает утверждения ImmutableID hello созданные ADFS согласованность с hello sourceAnchor значения экспортированного tooAzure AD.

Если вы управляете AD FS за пределами Azure AD Connect или использовании серверов федерации сторонних разработчиков для проверки подлинности, необходимо вручную обновить hello правил утверждений для утверждения toobe соответствуют значения sourceAnchor hello экспортировать tooAzure AD в качестве ImmutableID описано в разделе статьи [изменить AD FS правил для утверждений](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Мастер Hello возвращает hello следующие предупреждения после завершения установки:

![Настройка сторонней федерации](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Добавление нового развертывания tooexisting каталоги
Предположим, что вы развернули Azure AD Connect с включенной функцией ConsistencyGuid hello, а теперь хотите tooadd развертывания toohello другой каталог. При попытке tooadd hello directory мастер Azure AD Connect проверяет состояние hello атрибута mSDS-ConsistencyGuid hello в каталоге hello. Атрибут hello, настроенных на один или несколько объектов в каталоге hello, мастер hello заканчивается hello атрибута используется другими приложениями и возвращает сообщение об ошибке, как показано на следующей схеме hello. Если вы уверены, что этот атрибут hello не используется средством существующих приложений, сведения о как toosuppress hello ошибки необходимо toocontact поддержки.

![Добавление нового развертывания tooexisting каталоги](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Вход в Azure AD
При интеграции локальной службы каталогов с Azure AD, является важным toounderstand влияние параметров синхронизации hello hello способом пользователь проходит проверку подлинности. Azure AD использует пользователь hello tooauthenticate userPrincipalName (UPN). Однако при синхронизации пользователей, необходимо выбрать аккуратном значений userPrincipalName toobe атрибут hello.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Выбрав атрибут userPrincipalName hello
При выборе атрибута hello для предоставления hello значение toobe имя участника-пользователя, используемый в Azure из них следует

* значения атрибутов Hello соответствуют синтаксиса имени участника-пользователя toohello (RFC 822), то есть оно должно иметь формат hellousername@domain
* суффикс Hello в tooone совпадения значений hello объекта hello проверки пользовательских доменов в Azure AD

В параметрах express hello предполагалось, что выбрана для hello атрибут userPrincipalName. Если атрибут userPrincipalName hello не содержит значение hello требуется вашей toosign пользователей в tooAzure, то необходимо выбрать **выборочной установки**.

### <a name="custom-domain-state-and-upn"></a>Состояние и имя участника-пользователя пользовательского домена
Это важные tooensure это проверенного домена для hello суффикса имени участника-пользователя.

Джон (John) является пользователем в contoso.com. Вы хотите Джон toouse hello локального имени участника-пользователя john@contoso.com toosign в tooAzure окончании синхронизированы каталог contoso.onmicrosoft.com. toodo tooyour Azure AD для пользователей таким образом, требуется tooadd и проверка contoso.com как пользовательский домен в Azure AD, прежде чем начать Синхронизация пользователей hello. Если суффикс UPN hello Джон, например contoso.com, не соответствует проверенному домену в Azure AD, Azure AD заменяет суффикс UPN hello с contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Не поддерживающие маршрутизацию локальные домены и имена участников-пользователей для Azure AD
В некоторых организациях используются домены, не поддерживающие маршрутизацию, например contoso.local, или простые одноуровневые домены наподобие contoso. Вы не можете tooverify немаршрутизируемый домена в Azure AD. Azure AD Connect можно синхронизировать tooonly проверенного домена в Azure AD. При создании каталога Azure AD служба создает маршрутизируемый домен (например, contoso.onmicrosoft.com), который становится для Azure AD доменом по умолчанию. Таким образом он становится необходимые tooverify других маршрутизируемый домен в этом случае в случае, если вы не хотите домена onmicrosoft.com по умолчанию toohello toosync.

Чтение [добавить ваш tooAzure имя пользовательского домена Active Directory](../active-directory-add-domain.md) Дополнительные сведения о добавлении и проверка доменов.

Azure AD Connect определяет, когда используется не поддерживающая маршрутизацию доменная среда и соответствующим образом предупреждает, чтобы вы не продолжали, не изменив стандартные параметры. При работе в домене, не поддерживающий маршрутизацию, то он, скорее всего, что имена участников-пользователей hello hello имеют слишком немаршрутизируемый суффиксы. Например, если приложение выполняется под contoso.local, Azure AD Connect предложит вы toouse настраиваемые параметры, вместо того чтобы использовать стандартные параметры. С помощью настраиваемых параметров, все возможности toospecify hello атрибут, который следует использовать в качестве имени участника-пользователя toosign в tooAzure после hello пользователей, синхронизированных tooAzure AD.

## <a name="next-steps"></a>Дальнейшие действия
Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
