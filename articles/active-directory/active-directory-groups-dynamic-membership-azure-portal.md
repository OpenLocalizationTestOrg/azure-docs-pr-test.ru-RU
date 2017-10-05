---
title: "Управление участниками группы на основе атрибутов в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как создать расширенные правила для динамического членства в группе, используя поддерживаемые операторы и параметры выражений правила."
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
ms.openlocfilehash: f4d9a08551d616ff98bc8734cbeec01d6e0d04ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-attribute-based-rules-for-dynamic-group-membership-in-azure-active-directory"></a>Создание правил на основе атрибутов для динамического членства в группах в Azure Active Directory
В Azure Active Directory (Azure AD) можно создать дополнительные правила для включения сложного, основанного на атрибутах динамического членства в группах. В этой статье подробно описываются атрибуты и синтаксис для создания правил динамического членства пользователей или устройств.

Когда изменяются любые атрибуты пользователя, система оценивает все правила динамических групп в каталоге, чтобы определить, приведет ли это изменение к добавлению или удалению в группах. Если пользователь или устройство отвечает правилу, установленному для группы, они добавляются в эту группу. Они удаляются из группы, когда перестают отвечать этому правилу.

> [!NOTE]
> - Вы можете настроить правило динамического членства для групп безопасности или групп Office 365.
>
> - Этот компонент требует наличия лицензии Azure AD Premium P1 для каждого члена, добавленного хотя бы в одну из динамических групп.
>
> - Вы можете создать динамическую группу как для устройств, так и для пользователей, но невозможно создать правило, которое включает объекты пользователей и устройств одновременно.

> - Сейчас невозможно создать группу устройств на основе атрибутов пользователей, которым принадлежат эти устройства. Правила членства для устройств могут ссылаться только на непосредственные атрибуты объектов устройств в каталоге.

## <a name="to-create-an-advanced-rule"></a>Создание расширенного правила
1. Войдите в [центр администрирования Azure AD](https://aad.portal.azure.com) с помощью учетной записи глобального администратора или администратора учетных записей пользователей.
2. Выберите **Пользователи и группы**.
3. Выберите **Все группы**.

   ![Открытие колонки группы](./media/active-directory-groups-dynamic-membership-azure-portal/view-groups-blade.png)
4. В разделе **Все группы** выберите **Новая группа**.

   ![Добавление новой группы](./media/active-directory-groups-dynamic-membership-azure-portal/add-group-type.png)
5. В колонке **Группа** введите имя и описание новой группы. Для параметра **Тип членства** выберите значение **Динамический пользователь** или **Динамическое устройство** в зависимости от того, требуется создать правило для пользователей либо устройств, а затем щелкните **Добавить динамический запрос**. Атрибуты, используемые для правил устройств, описаны в разделе [Создание правил для объектов устройств с помощью атрибутов](#using-attributes-to-create-rules-for-device-objects).

   ![Добавление правила динамического членства](./media/active-directory-groups-dynamic-membership-azure-portal/add-dynamic-group-rule.png)
6. В колонке **Правила динамического членства** введите правило в поле **Добавить расширенное правило динамического членства** и нажмите клавишу ВВОД. Затем щелкните **Создать** в нижней части колонки.
7. Щелкните **Создать** в колонке **Группа**, чтобы создать группу.

## <a name="constructing-the-body-of-an-advanced-rule"></a>Создание текста расширенного правила
Расширенное правило, которое можно создать для динамического членства в группах, является по сути бинарным выражением из трех частей, результат которого — значение true или false. Вот эти три части:

* параметр в левой части;
* бинарный оператор;
* константа в правой части.

Полное расширенное правило выглядит примерно так: (левый_параметр бинарный_оператор "правая_константа"), где: двоичное выражение может (необязательно) окружаться скобками. Двойные кавычки обязательны, только если правая константа является строкой. Левый параметр записывается в формате "пользователь.свойство". Расширенное правило может состоять из нескольких двоичных выражений, разделенных логическими операторами -and, -or, и -not.

Ниже приведены примеры правильно составленных расширенных правил:
```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```
Полный список поддерживаемых параметров и операторов выражений правил см. в приведенных ниже разделах. Атрибуты, используемые для правил устройств, описаны в разделе [Создание правил для объектов устройств с помощью атрибутов](#using-attributes-to-create-rules-for-device-objects).

Общая длина текста расширенного правила не должна превышать 2048 символов.

> [!NOTE]
> В операциях со строками и регулярными выражениями не учитывается регистр знаков. Можно также выполнить проверку наличия значений Null, используя $null как константу, например: user.department - eq $null.
> Строки, содержащие кавычки ("), следует экранировать с помощью знака '. Например: user.department -eq \`"Sales".

## <a name="supported-expression-rule-operators"></a>Поддерживаемые операторы выражений правил
В следующей таблице перечислены все поддерживаемые операторы выражений правил и их синтаксис, используемый в тексте расширенного правила:

| Оператор | Синтаксис |
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

Ниже перечислены все операторы в порядке возрастания приоритета. Операторы в одной строке имеют одинаковый приоритет.
````
-any -all
-or
-and
-not
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
````
Все операторы можно использовать с дефисом в качестве префикса и без него. Скобки требуются только в том случае, если приоритет не соответствует вашим требованиям.
Например:
```
   user.department –eq "Marketing" –and user.country –eq "US"
```
эквивалентно правилу
```
   (user.department –eq "Marketing") –and (user.country –eq "US")
```
## <a name="using-the--in-and--notin-operators"></a>Использование операторов -In и -notIn

Чтобы сравнить значение атрибута пользователя с рядом различных значений, можно использовать оператор -In или -notIn. Ниже приведен пример использования оператора -In.
```
    user.department -In [ "50001", "50002", "50003", “50005”, “50006”, “50007”, “50008”, “50016”, “50020”, “50024”, “50038”, “50039”, “51100” ]
```
Обратите внимание на символы "[" и "]" в начале и конце списка значений. Это условие принимает значение True, если значение user.department равно одному из значений в списке.


## <a name="query-error-remediation"></a>Исправление ошибки запроса
В следующей таблице перечислены потенциальные ошибки и способы их исправления, если они встречаются

| Ошибка анализа запроса | Неправильное использование | Правильное использование |
| --- | --- | --- |
| Ошибка: атрибут не поддерживается. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/>Свойство должно соответствовать одному из свойств [в списке поддерживаемых свойств](#supported-properties). |
| Ошибка: не поддерживается оператор для атрибута. |(user.accountEnabled -contains true) |(user.accountEnabled - eq true)<br/>Свойство имеет логический тип. Используйте поддерживаемые операторы (-eq и - ne) для логического типа из списка выше. |
| Ошибка: ошибка компиляции запроса. |(user.department -eq "Sales") -and (user.department -eq "Marketing")(user.userPrincipalName -match "*@domain.ext") |(user.department -eq "Sales") -and (user.department -eq "Marketing")<br/>Логический оператор должен соответствовать одному из свойств в приведенном выше списке поддерживаемых свойств. (user.userPrincipalName -match ".*@domain.ext")or(user.userPrincipalName -match "@domain.ext$") — ошибка в регулярном выражении. |
| Ошибка: неправильный формат двоичного выражения. |(user.department –eq “Sales”) (user.department -eq "Sales")(user.department-eq"Sales") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>Запрос содержит несколько ошибок. Скобки не в нужном месте. |
| Ошибка: неизвестная ошибка при настройке динамического членства. |(user.accountEnabled -eq "True" AND user.userPrincipalName -contains "alias@domain") |(user.accountEnabled -eq true) -and (user.userPrincipalName -contains "alias@domain")<br/>Запрос содержит несколько ошибок. Скобки не в нужном месте. |

## <a name="supported-properties"></a>Поддерживаемые свойства
Ниже приведены все свойства пользователя, которые можно использовать в расширенном правиле.

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
| mail |Любое строковое значение или $null (SMTP-адрес пользователя) |(user.mail -eq "value") |
| mailNickName |Любое строковое значение (псевдоним электронной почты пользователя) |(user.mailNickName -eq "value") |
| mobile |Любое строковое значение или $null |(user.mobile -eq "value") |
| objectId |GUID объекта пользователя. |(user.objectId -eq "1111111-1111-1111-1111-111111111111") |
| onPremisesSecurityIdentifier; | Локальный идентификатор безопасности (SID) для пользователей, которые были синхронизированы из локальной среды в облако. |(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111") |
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

* -any (выполняется, когда условию соответствует хотя бы один элемент в коллекции)
* -all (выполняется, когда условию соответствуют все элементы в коллекции)

| Свойства | Значения | Использование |
| --- | --- | --- |
| assignedPlans |Каждый объект в коллекции предоставляет следующие строковые параметры: capabilityStatus, service, servicePlanId |user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled") |

Многозначные свойства являются коллекциями объектов того же типа. Вы можете использовать операторы -any и -all для применения условия к одному или ко всем элементам в коллекции соответственно. Например:

assignedPlans — это многозначное свойство, которое перечисляет все сервисные планы, назначенные пользователю. Представленное ниже выражение выбирает пользователей, которым назначен план обслуживания Exchange Online (План 2) и для которых этот план находится в состоянии Enabled:

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

(Идентификатор Guid обозначает план обслуживания Exchange Online (План 2)).

> [!NOTE]
> Это полезно, если вы хотите найти всех пользователей, которым разрешено использовать Office 365 (или другую службу Microsoft Online), например, чтобы применить к ним некоторый набор политик.

Следующее выражение выбирает всех пользователей, которым назначен любой план обслуживания, связанный со службой Intune (это определяется по имени службы "SCO"):
```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

## <a name="use-of-null-values"></a>Использование значений Null

Чтобы указать значение Null в правиле, можно использовать null или $null. Пример:
```
   user.mail –ne null
```
эквивалентно правилу
```
   user.mail –ne $null
   ```

## <a name="extension-attributes-and-custom-attributes"></a>Атрибуты расширения и настраиваемые атрибуты
Атрибуты расширения и настраиваемые атрибуты поддерживаются в правилах динамического членства.

Атрибуты расширения синхронизируются из локального каталога Windows Server AD и принимают формат ExtensionAttributeX, где X равно 1–15.
Пример правила, которое использует атрибут расширения:
```
(user.extensionAttribute15 -eq "Marketing")
```
Настраиваемые атрибуты синхронизируются из локального каталога Windows Server AD или из подключенного приложения SaaS в формате user.extension_[GUID]\__[Attribute], где [GUID] — уникальный идентификатор в AAD для приложения, создавшего атрибут в AAD, а [Attribute] — имя атрибута, присвоенное при создании.
Пример правила, которое использует настраиваемый атрибут:
```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber  
```
Имя настраиваемого атрибута можно найти в каталоге, отправив запрос на атрибут пользователя с помощью обозревателя графов и выполнив поиск по имени атрибута.

## <a name="direct-reports-rule"></a>Правило "Непосредственные подчиненные"
Вы можете создать группу, в которую войдут все непосредственные подчиненные определенного руководителя. Если в будущем состав подчиненных этого руководителя изменится, членство в группе будет скорректировано автоматически.

> [!NOTE]
> 1. Чтобы такое правило работало, следите за правильностью заполнения свойства **Manager ID** (Идентификатор руководителя) для всех пользователей в арендаторе. Текущее значение свойства можно проверить на **вкладке профиля** для каждого пользователя.
> 2. Это правило учитывает только **непосредственных** подчиненных. Сейчас невозможно создать группу с учетом вложенной иерархии, в которую будут входить не только непосредственные подчиненные, но и их подчиненные.

**Настройка группы**

1. Выполните шаги 1–5 из раздела [Создание расширенного правила](#to-create-the-advanced-rule) и для параметра **Тип членства** выберите значение **Динамический пользователь**.
2. В колонке **Dynamic membership rules** (Правила динамического членства) введите правило, используя приведенный ниже синтаксис.

    *Direct Reports for "{идентификатор_объекта_руководителя}"*

    Пример допустимого правила:
```
                    Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```
    where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager. The object ID can be found on manager's **Profile tab**.
3. Когда вы сохраните это правило, в группу будут добавлены все пользователи с выбранным значением идентификатора руководителя.

## <a name="using-attributes-to-create-rules-for-device-objects"></a>Создание правил для объектов устройств с помощью атрибутов
Можно также создать правило, которое выбирает объекты устройств для членства в группе. Можно использовать следующие атрибуты устройства.

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
 managementType | MDM (для мобильных устройств).<br>PC (для компьютеров, управляемых агентом Intune PC). | (device.managementType -eq "MDM")
 organizationalUnit | Любое строковое значение, соответствующее имени подразделения, заданному в локальном каталоге Active Directory. | (device.organizationalUnit -eq "US PCs")
 deviceId | Допустимый идентификатор устройства Azure AD. | (device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")
 objectId | Допустимый идентификатор объекта Azure AD. |  (device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")




## <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения о группах в Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Создание группы и добавление участников](active-directory-groups-create-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
