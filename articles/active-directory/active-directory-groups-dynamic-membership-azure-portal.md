---
title: "на основе aaaAttribute динамическое членство в группе в Azure Active Directory | Документы Microsoft"
description: "Как toocreate Дополнительные правила для динамического членства в группе включая поддерживаемые логические операторы и параметры."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fb434cc2-9a91-4ebf-9753-dd81e289787e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cd06ed70433eff65401c67d7351d5dcc12a9dd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Создание правил на основе атрибутов для динамического членства в группах в Azure Active Directory
В Azure Active Directory (Azure AD) можно создать расширенных правил tooenable сложных основанное на атрибутах динамическое членство в группе. В этой статье указаны атрибуты hello и правила динамического членства toocreate синтаксис для пользователей или устройств.

Если какие-либо атрибуты изменение пользователя или устройства системы hello проверяет все правила динамическую группу в toosee каталог, если изменение hello приведет к запуску любую группу добавляет или удаляет. Если пользователь или устройство отвечает правилу, установленному для группы, они добавляются в эту группу. Если они больше не удовлетворяют правилу hello, они будут удалены.

> [!NOTE]
> - Вы можете настроить правило динамического членства для групп безопасности или групп Office 365.
>
> - Этот компонент требует наличия лицензии Azure AD Premium P1 для каждой член добавлен tooat по крайней мере одно динамические группы пользователей.
>
> - Вы можете создать динамическую группу как для устройств, так и для пользователей, но невозможно создать правило, которое включает объекты пользователей и устройств одновременно.

> - В момент hello не возможные toocreate основании атрибуты пользователя-Владелец группы устройств. Правила членства устройство можно только ссылочные немедленно атрибуты объектов устройств в каталоге hello.

## <a name="toocreate-an-advanced-rule"></a>toocreate расширенного правила
1. Войдите в toohello [Центр администрирования Azure AD](https://aad.portal.azure.com) под учетной записью, глобальный администратор или администратор учетной записи пользователя.
2. Выберите **Пользователи и группы**.
3. Выберите **Все группы**.

   ![Открытие hello групп колонку](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. В разделе **Все группы** выберите **Новая группа**.

   ![Добавление новой группы](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. На hello **группы** колонки, введите имя и описание для новой группы hello. Выберите **тип регистрации членства** любого **динамический пользовательский** или **динамического устройства**, в зависимости от того, является ли должны toocreate правило для пользователей или устройств, а затем выберите **Добавить динамический запрос**. Hello атрибутов, используемых для правила устройств, в разделе [с помощью правил toocreate атрибуты для объектов-устройств](#using-attributes-to-create-rules-for-device-objects).

   ![Добавление правила динамического членства](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. На hello **правила динамического членства** колонке введите правило в hello **динамического членства для добавления дополнительного правила** поле, нажмите клавишу ВВОД, а затем выберите **создать** внизу hello Hello колонку.
7. Выберите **создать** на hello **группы** колонке toocreate hello группы.

## <a name="constructing-hello-body-of-an-advanced-rule"></a>Создав hello текста расширенного правила
Hello расширенное правило, которое можно создать для hello динамическое членство в группе является по сути логическое выражение, которое состоит из трех частей и приводит к истинному или ложному результату. Ниже перечислены три части Hello

* параметр в левой части;
* бинарный оператор;
* константа в правой части.

Готовое расширенное правило выглядит примерно toothis: (leftParameter binaryOperator «RightConstant»), где hello открывающие и закрывающие скобки необязательны для всего двоичного выражения hello, двойные кавычки являются необязательными, требуется только для hello вправо Константа, если он является строкой, и hello синтаксис для левого параметра hello пользователь.свойство. Расширенное правило может состоять из нескольких двоичных выражений, разделенных hello- и, - или и - не логические операторы.

Hello ниже приведены примеры правильно построенных расширенных правил:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Hello полный список поддерживаемых параметров и операторов выражений правил см. в разделах ниже. Hello атрибутов, используемых для правила устройств, в разделе [с помощью правил toocreate атрибуты для объектов-устройств](#using-attributes-to-create-rules-for-device-objects).

Общая длина Hello hello текста расширенного правила не может превышать 2048 символов.

> [!NOTE]
> В операциях со строками и регулярными выражениями не учитывается регистр знаков. Можно также выполнить проверку наличия значений Null, используя $null как константу, например: user.department - eq $null.
> Строки, содержащие кавычки ("), следует экранировать с помощью знака '. Например: user.department -eq \`"Sales".

## <a name="supported-expression-rule-operators"></a>Поддерживаемые операторы выражений правил
Hello следующей таблице перечислены все логические операторы поддерживаются hello и toobe их синтаксис, используемый в тексте hello hello дополнительного правила.

| operator | Синтаксис |
| --- | --- |
| Не равно |-ne |
| Равно |-eq |
| Не начинается с |-notStartsWith |
| Начинается с |-startsWith |
| Не содержит |-notContains |
| Содержит |-contains |
| Не соответствует |-notMatch |
| Соответствует |-match |
| В | -in |
| Не входит | -notIn |

## <a name="operator-precedence"></a>Приоритет операторов

Ниже перечислены все операторы каждого приоритета от нижней toohigher. Операторы в одной строке имеют одинаковый приоритет.
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Все операторы можно использовать с или без префикса дефис hello. Скобки требуются только в том случае, если приоритет не соответствует вашим требованиям.
Например:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
эквивалентно правилу
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-hello--in-and--notin-operators"></a>С помощью hello - в и - notIn операторы

Если необходимо toocompare hello значение пользовательского атрибута к число различных значений можно использовать hello - в - notIn операторы и операторы. Ниже приведен пример с использованием hello - в оператор:
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Обратите внимание на использование hello hello «[» и «]» в hello начало и конец hello список значений. Это условие принимает tooTrue значения hello user.department равно одному hello значений в списке hello.


## <a name="query-error-remediation"></a>Исправление ошибки запроса
Hello следующей таблице перечислены потенциальные ошибки и как toocorrect их, если они происходят

| Ошибка анализа запроса | Неправильное использование | Правильное использование |
| --- | --- | --- |
| Ошибка: атрибут не поддерживается. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>Свойства должны соответствовать одному из hello [свойства список поддерживаемых](#supported-properties). |
| Ошибка: не поддерживается оператор для атрибута. |(user.accountEnabled -contains true) |(user.accountEnabled - eq true)<br/>Свойство имеет логический тип. Используйте операторы hello поддерживается (-eq или - ne) для логического типа из hello над списком. |
| Ошибка: ошибка компиляции запроса. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Логический оператор должен соответствовать одному из списка свойства hello поддерживается выше. (user.userPrincipalName-соответствует». *@domain.ext») или (user.userPrincipalName-соответствует «@domain.ext$») Ошибка в регулярном выражении. |
| Ошибка: неправильный формат двоичного выражения. |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>Запрос содержит несколько ошибок. Скобки не в нужном месте. |
| Ошибка: неизвестная ошибка при настройке динамического членства. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>Запрос содержит несколько ошибок. Скобки не в нужном месте. |

## <a name="supported-properties"></a>Поддерживаемые свойства
Здесь представлены Hello все hello пользовательские свойства, которые можно использовать в расширенных правилах:

### <a name="properties-of-type-boolean"></a>Свойства логического типа
Допустимые операторы

* -eq
* -ne

| Свойства | Допустимые значения | Использование |
| --- | --- | --- |
| AccountEnabled |true, false |user.accountEnabled -eq true |
| dirSyncEnabled |true, false |user.dirSyncEnabled -eq true |

### <a name="properties-of-type-string"></a>Свойства строкового типа
Допустимые операторы

* -eq
* -ne
* -notStartsWith
* -StartsWith
* -contains
* -notContains
* -match
* -notMatch
* -in
* -notIn

| Свойства | Допустимые значения | Использование |
| --- | --- | --- |
| city |Любое строковое значение или $null |(user.city -eq "value") |
| country |Любое строковое значение или $null |(user.country -eq "value") |
| companyName | Любое строковое значение или $null | (user.companyName -eq "value") |
| department |Любое строковое значение или $null |(user.department -eq "value") |
| displayName |Любое строковое значение. |(user.displayName -eq "value") |
| facsimileTelephoneNumber |Любое строковое значение или $null |(user.facsimileTelephoneNumber -eq "value") |
| givenName |Любое строковое значение или $null |(user.givenName -eq "value") |
| jobTitle |Любое строковое значение или $null |(user.jobTitle -eq "value") |
| mail |Любое строковое значение или $null (SMTP-адрес пользователя hello) |(user.mail -eq "value") |
| mailNickName |Любое строковое значение (псевдоним электронной почты пользователя hello) |(user.mailNickName -eq "value") |
| mobile |Любое строковое значение или $null |(user.mobile -eq "value") |
| objectId |Идентификатор GUID объекта пользователя hello |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier; | Локальный идентификатор безопасности (SID) для пользователей, которые были синхронизированы из локальной toohello облака. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
| passwordPolicies |None, DisableStrongPassword, DisablePasswordExpiration, DisablePasswordExpiration, DisableStrongPassword |(user.passwordPolicies -eq "DisableStrongPassword") |
| physicalDeliveryOfficeName |Любое строковое значение или $null |(user.physicalDeliveryOfficeName -eq "value") |
| postalCode |Любое строковое значение или $null |(user.postalCode -eq "value") |
| preferredLanguage |Код ISO 639-1. |(user.preferredLanguage -eq "en-US") |
| sipProxyAddress |Любое строковое значение или $null |(user.sipProxyAddress -eq "value") |
| state |Любое строковое значение или $null |(user.state -eq "value") |
| streetAddress |Любое строковое значение или $null |(user.streetAddress -eq "value") |
| surname |Любое строковое значение или $null |(user.surname -eq "value") |
| TelephoneNumber |Любое строковое значение или $null |(user.telephoneNumber -eq "value") |
| usageLocation |Двухбуквенный код страны. |(user.usageLocation -eq "US") |
| userPrincipalName |Любое строковое значение. |(user.userPrincipalName -eq "alias@domain") |
| userType |member, guest, $null |(user.userType -eq "Member") |

### <a name="properties-of-type-string-collection"></a>Свойства типа коллекции строк
Допустимые операторы

* -contains
* -notContains

| Свойства | Допустимые значения | Использование |
| --- | --- | --- |
| otherMails |Любое строковое значение. |(user.otherMails -contains "alias@domain") |
| proxyAddresses |SMTP: alias@domain, smtp: alias@domain |(user.proxyAddresses -contains "SMTP: alias@domain") |

## <a name="multi-value-properties"></a>Многозначные свойства
Допустимые операторы

* -любое (удовлетворены, если хотя бы один элемент в коллекции hello соответствует условию hello)
* -все (выполнены, когда все элементы коллекции hello условию hello)

| Свойства | Значения | Использование |
| --- | --- | --- |
| assignedPlans |Каждый объект в коллекции hello предоставляет следующие свойства строка hello: capabilityStatus, служба, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

Многозначные свойства представляют собой коллекции объектов hello того же типа. Можно использовать - любые и - все операторы tooapply tooone условие или все hello элементы в коллекции hello, соответственно. Например:

assignedPlans — это свойство Многозначный, в которой перечислены все сервисные планы, назначенный пользователь toohello. Пользователи, имеющие hello Exchange Online (план 2) службе план, который также находится в состоянии Enabled выбирает Hello ниже выражение:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(идентификатор Guid hello определяет план обслуживания Exchange Online (план 2) hello).

> [!NOTE]
> Это полезно, если вы хотите tooidentify все пользователи которого Office 365 (или другую службу Microsoft Online) возможность включена, для примера tootarget их с помощью набора политик.

Hello следующее выражение выбирает все пользователи, имеющие любого плана службы, связанный с hello службы Intune (определяется имя службы «SCO»):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Использование значений Null

toospecify значение null, в правиле, можно использовать «null» или $null. Пример:
```
   user.mail –ne null
```
эквивалентно правилу
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Атрибуты расширения и настраиваемые атрибуты
Атрибуты расширения и настраиваемые атрибуты поддерживаются в правилах динамического членства.

Атрибуты расширения, синхронизируемые из окна на локальном сервере AD и выполните hello формат «ExtensionAttributeX», где X равно 1-15.
Пример правила, которое использует атрибут расширения:
```
(user.extensionAttribute15 -eq "Marketing")
```
Настраиваемые атрибуты, синхронизируемые из Windows Server в локальной среде AD или из подключенных SaaS hello и приложения hello формат «user.extension_[GUID]\__ [Attribute]», где [GUID] — уникальный идентификатор hello в Azure Active Directory для приложения hello, атрибут созданный hello в AAD и [Attribute] является именем hello hello атрибута, как он был создан.
Пример правила, которое использует настраиваемый атрибут:
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Hello имени настраиваемого атрибута можно найти в каталоге hello, запрашивая пользователя атрибут с помощью Graph Explorer и поиск имени атрибута hello.

## <a name="direct-reports-rule"></a>Правило "Непосредственные подчиненные"
Вы можете создать группу, в которую войдут все непосредственные подчиненные определенного руководителя. При изменении подчиненных руководителя hello в будущем hello членство в группе hello будет настроено автоматически.

> [!NOTE]
> 1. Toowork правило hello, убедитесь в том, hello **идентификатор менеджера** правильно задано свойство на пользователей в клиенте. Можно проверить текущее значение hello для пользователя на их **вкладке профиля**.
> 2. Это правило учитывает только **непосредственных** подчиненных. Оно не возможные toocreate группы для вложенной иерархии, например группу, содержащую прямые отчеты и связанные отчеты.

**Группа tooconfigure hello**

1. Выполните шаги 1 – 5 из раздела [toocreate hello дополнительного правила](#to-create-the-advanced-rule)и выберите **тип регистрации членства** из **динамический пользовательский**.
2. На hello **правила динамического членства** колонке введите правило hello hello, используя синтаксис:

    *Direct Reports for "{идентификатор_объекта_руководителя}"*

    Пример допустимого правила:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is hello objectID of hello manager. hello object ID can be found on manager's **Profile tab**.
3. После сохранения правила hello, все пользователи, имеющие hello указанный идентификатор менеджера будут добавлены toohello группы.

## <a name="using-attributes-toocreate-rules-for-device-objects"></a>С помощью правил toocreate атрибуты для объектов-устройств
Можно также создать правило, которое выбирает объекты устройств для членства в группе. можно использовать следующие атрибуты устройства Hello.

 Атрибут устройства  | Значения | Пример
 ----- | ----- | ----------------
 AccountEnabled | true, false | (device.accountEnabled -eq true)
 displayName | Любое строковое значение |(device.displayName -eq "Rob Iphone”)
 deviceOSType | Любое строковое значение | (device.deviceOSType -eq "IOS")
 deviceOSVersion | Любое строковое значение | (device.OSVersion -eq "9.1")
 deviceCategory | Допустимое имя категории устройств. | (device.deviceCategory -eq "BYOD")
 deviceManufacturer | Любое строковое значение. | (device.deviceManufacturer -eq "Samsung")
 deviceModel | Любое строковое значение. | (device.deviceModel -eq "iPad Air")
 deviceOwnership | Personal или Company. | (device.deviceOwnership -eq "Company")
 domainName | Любое строковое значение. | (device.domainName -eq "contoso.com")
 enrollmentProfileName | Имя профиля регистрации устройства Apple. | (device.enrollmentProfileName -eq "DEP iPhones")
 isRooted | true, false | (device.isRooted -eq true)
 managementType | MDM (для мобильных устройств).<br>ПК (для компьютеров, управляемых агентом hello ПК Intune) | (device.managementType -eq "MDM")
 organizationalUnit | любое строковое значение, которое совпадает с именем hello hello организационного подразделения, заданные в локальной среде Active Directory | (device.organizationalUnit -eq "US PCs")
 deviceId | Допустимый идентификатор устройства Azure AD. | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 objectId | Допустимый идентификатор объекта Azure AD. |  (device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")




## <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения о группах в Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Создание группы и добавление участников](active-directory-groups-create-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
