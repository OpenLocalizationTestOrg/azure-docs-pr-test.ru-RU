---
title: "Azure AD Connect: устранение ошибок синхронизации | Документация Майкрософт"
description: "Объясняет, как tootroubleshoot ошибки, возникающие во время синхронизации с Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Устранение ошибок синхронизации
При синхронизации данных удостоверений из Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD), возможно возникновение ошибок. Это статье представлен обзор различных типов ошибок синхронизации, некоторые из возможных сценариев hello, вызывающие эти ошибки и возможные способы toofix hello. Данная статья включает hello распространенных типов ошибок и не могут охватывать все возможные ошибки hello.

 В этой статье предполагается hello читатель хорошо знаком с базовым hello [разработки концепции Azure AD и Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Последнюю версию Azure AD Connect hello \(августа 2016 или более поздней версии\), вывод отчета об ошибках синхронизации доступна в hello [портала Azure](https://aka.ms/aadconnecthealth) как часть Azure AD Connect Health для синхронизации.

Начиная с 1 сентября 2016 [Azure Active Directory повторяющийся атрибут устойчивости](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) , функция будет включена по умолчанию для всех hello *новый* клиентов Active Directory Azure. Эта функция будет автоматически включается для существующих клиентов в ближайшее hello.

Azure AD Connect выполняет три типа операций из здесь хранятся синхронизацию каталогов hello: экспорта и импорта, синхронизации. Ошибки могут иметь место во всех операциях hello. Данная статья в основном посвящена ошибки во время экспорта tooAzure AD.

## <a name="errors-during-export-tooazure-ad"></a>Ошибки во время экспорта tooAzure AD
Следующий раздел описывает различные типы ошибок, возникающих во время hello экспорта операции tooAzure AD с помощью синхронизации Здравствуйте, соединитель Azure AD. Этот соединитель может определяться формат имени hello, «contoso. *onmicrosoft.com*».
Ошибки во время экспорта tooAzure AD указывают hello операции \(Добавление, обновление, удаление и т.д.\) предпринимается попытка Azure AD Connect \(модуль синхронизации\) на Azure Active Directory не удалось.

![Обзор ошибок экспорта](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Ошибки несовпадения данных
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Описание
* Когда Azure AD Connect \(модуль синхронизации\) указывает, что Azure Active Directory tooadd или обновления объектов, Azure AD соответствует hello входящего объекта с помощью hello **sourceAnchor** атрибута toohello  **immutableId** атрибутов объектов в Azure AD. Это сопоставление называется **жестким**.
* Когда Azure AD **не удается найти** любой объект, который соответствует hello **immutableId** атрибута с hello **sourceAnchor** атрибут входящего объекта hello перед подготовкой новый объект возвращается toouse hello ProxyAddresses и UserPrincipalName атрибутов toofind совпадения. Такое сопоставление называется **мягким**. Hello мягкий совпадение — спроектированный toomatch объектов, уже присутствует в Azure AD (, определяемые в Azure AD) с помощью новых объектов hello, добавить или обновить во время синхронизации, представляющие hello одной сущности (пользователей, групп) на локальном компьютере.
* **InvalidSoftMatch** ошибка возникает, когда hello жестких совпадение не удается найти любой подходящий объект **AND** мягкий соответствия находит подходящий объект, но этот объект имеет значение, отличное от *immutableId* чем hello входящего объекта *SourceAnchor*, предложение, hello объекта сопоставления был синхронизирован с другим объектом из локальной Active Directory.

Другими словами, чтобы toowork мягкий соответствия hello, hello объекта toobe soft соответствует не следует любое значение для hello *immutableId*. Если любой объект с *immutableId* набор со значением сбой hello жестких соответствия, но соблюдение hello soft удовлетворяющем условиям, hello операция приведет к InvalidSoftMatch ошибка синхронизации.

Атрибуты Azure Active Directory схем не разрешает двух или более объектов toohave hello hello следуя тем же значением. \(Это неполный список.\)

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier;
* ObjectId

> [!NOTE]
> [Azure AD атрибут повторяющийся атрибут устойчивости](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) функция также разворачивается как поведение по умолчанию hello Azure Active Directory.  Это позволит снизить hello количество ошибок синхронизации Azure AD Connect (а также другие клиенты синхронизации) путем создания более устойчивым Azure AD в hello способ обработки повторяющихся ProxyAddresses и UserPrincipalName атрибуты, присутствующие в в локальной среде AD сред. Эта функция не исправляет ошибки дублирования hello. Поэтому hello данные по-прежнему должны toobe фиксированной. Однако он допускает подготовку новых объектов, которые в противном случае заблокирован из-за значения tooduplicated идет подготовка в Azure AD. Это также приводит к сокращению hello число ошибок синхронизации, возвращаемых toohello синхронизации клиента.
> Эта функция включена для вашего клиента, не увидят ошибок синхронизации InvalidSoftMatch hello, встреченных во время инициализации новых объектов.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Примеры сценариев для InvalidSoftMatch
1. Два или несколько объектов с hello же значение атрибута ProxyAddresses имеется в локальную службу Active Directory. Azure AD подготовит только один объект.
2. Два или несколько объектов с hello userPrincipalName тем же значением, имеется в локальную службу Active Directory. Azure AD подготовит только один объект.
3. Объект был добавлен в hello в локальной среде Active Directory с hello же значение атрибута ProxyAddresses, что и существующий объект в Azure Active Directory. Hello объект, добавленный на локальном компьютере не выполняется получение Подготовка в Azure Active Directory.
4. Объект был добавлен в локальной Active Directory с hello же значение атрибута userPrincipalName, что и учетная запись в Azure Active Directory. Hello объекта не выполняется получение Подготовка в Azure Active Directory.
5. Учетной записи синхронизированных был перемещен из леса A tooForest B. Azure AD Connect (модуль синхронизации) используется hello toocompute ObjectGUID атрибут SourceAnchor. После перемещения hello леса значение hello hello SourceAnchor отличается. новый объект Hello (в лесу Б) происходит сбой toosync с hello существующий объект в Azure AD.
6. Синхронизированных объектов были случайно удалены из в локальной среде Active Directory и новый объект был создан в Active Directory для hello же сущности (например, пользователь) без удаления учетной записи hello в Azure Active Directory. Учетная запись нового Hello не toosync с hello существующего объекта Azure AD.
7. Azure AD Connect удалили и переустановили. Во время повторной установки hello другой атрибут был выбран как hello SourceAnchor. Все объекты hello, которые ранее синхронизированы остановлена, синхронизация с InvalidSoftMatch ошибки.

#### <a name="example-case"></a>Пример
1. Пользователь **Григорий Авдеев** синхронизирован в Azure AD из локального каталога AD в домене *contoso.com*.
2. Для атрибута **userPrincipalName** Григория задано значение **bobs@contoso.com**.
3. **«abcdefghijklmnopqrstuv ==»** — hello **SourceAnchor** вычислены Azure AD Connect с помощью Bob Smith **objectGUID** из локальной Active Directory, который является hello **immutableId** Смит Боб в Azure Active Directory.
4. Боб также имеет следующие значения для hello **proxyAddresses** атрибута:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Новый пользователь **Taylor Боб**, добавляется toohello в локальной среде Active Directory.
6. Для атрибута **userPrincipalName** Артема задано значение **bobt@contoso.com**.
7. **«abcdefghijkl0123456789 == "«** — hello **sourceAnchor** вычислены Azure AD Connect с помощью Taylor Боб **objectGUID** из в локальной среде Active Directory. Боб Taylor объект имеет пока не синхронизировано tooAzure Active Directory.
8. Боб Taylor имеет следующие значения для атрибута proxyAddresses hello hello
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Во время синхронизации Azure AD Connect будет распознавать hello Добавление Taylor Боб в локальной Active Directory и запрос Azure AD toomake hello такие же изменения.
10. Сначала Azure AD выполнит жесткое сопоставление. То есть, он выполняет поиск Если любой объект с hello immutableId равно слишком "abcdefghijkl0123456789 ==». Так как в Azure AD отсутствуют объекты с таким атрибутом immutableId, жесткое сопоставление завершится ошибкой.
11. Azure AD предпримет toosoft-match Taylor Боб. То есть он выполняет поиск при наличии любого объекта равны toohello proxyAddresses три значения, включаяsmtp:bob@contoso.com
12. Azure AD будет объект Bob Smith toomatch hello soft-match критерии поиска. Но этот объект имеет значение immutableId hello = «abcdefghijklmnopqrstuv ==». Это значит, что этот объект синхронизирован из другого объекта локального каталога AD. Поэтому Azure AD не может выполнить нестрогое сопоставление, что приведет к ошибке синхронизации **InvalidSoftMatch**.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Как toofix InvalidSoftMatch ошибки
Hello самая распространенная причина ошибки InvalidSoftMatch hello имеет два объекта с разных SourceAnchor \(immutableId\) имеют одинаковое значение для атрибутов hello ProxyAddresses и/или UserPrincipalName, которые используются во время hello hello процесс soft-match в Azure AD. В порядке toofix hello недопустимый мягкий соответствия

1. Определите proxyAddresses hello дублирован, userPrincipalName или другие значения атрибута, вызвавших ошибки hello. Также определять два \(или более\) объекты вовлеченные в конфликт hello. Здравствуйте, отчет, сформированный [Azure AD Connect Health для синхронизации](https://aka.ms/aadchsyncerrors) может помочь выявить hello двух объектов.
2. Определите, какой объект следует продолжить toohave hello повторяющиеся значения и какой объект не должен.
3. Удалите повторяющийся hello значение из hello объекта, который не следует это значение. Обратите внимание, что необходимо внести изменения в каталоге hello, который является источником hello объекта из hello. В некоторых случаях может потребоваться toodelete один из объектов hello в конфликте.
4. Если вы внесли изменения в hello в локальной среде AD hello, позволяют изменить hello синхронизации Azure AD Connect.

Обратите внимание, что отчет об ошибках синхронизации в Azure AD Connect Health для синхронизации обновляется каждые 30 минут входят ошибки hello hello последней попытки синхронизации.

> [!NOTE]
> ImmutableId, по определению не должны изменяться в течение срока службы hello hello объекта. Если Azure AD Connect не был настроен в некоторых сценариях hello помните из hello над списком, иначе может оказаться в ситуации, где Azure AD Connect вычисляет другое значение hello SourceAnchor для объекта hello AD, что представляет hello одной сущности (того же пользователя или Группа или контакт и т. д), содержащее обратиться с помощью toocontinue существующего объекта AD Azure.
>
>

#### <a name="related-articles"></a>Связанные статьи
* [Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/en-us/kb/2647098) (Запрет синхронизации службы каталогов в Office 365 из-за повторяющихся или недопустимых атрибутов)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Описание
Когда Azure AD выполняет попытку toosoft совпадения двух объектов, это возможно, что двух разных объектов «тип объекта» (например, пользователя, группы, обратитесь в службу и т.д.) имеют hello же значения для атрибутов hello использовать мягкое соответствия tooperform hello. Как дублирования этих атрибутов не разрешено в Azure AD, hello операция может привести к «ObjectTypeMismatch» ошибки синхронизации.

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Примеры сценариев ошибки ObjectTypeMismatch
* Администратор создал в Office 365 группу безопасности, поддерживающую почту. Администратор добавляет нового пользователя или контакт в в локальной среде AD (которые tooAzure AD еще не синхронизирована) с hello одинаковое значение для атрибута ProxyAddresses hello, что и Office 365 hello группы.

#### <a name="example-case"></a>Примеры
1. Администратор создает новую группу безопасности включена поддержка почты в Office 365 для отдела налога hello и предоставляет адрес электронной почты как tax@contoso.com. Это назначает атрибут ProxyAddresses hello для этой группы со значением hello**smtp:tax@contoso.com**
2. Новый пользователь не присоединит Contoso.com и создания учетной записи для hello пользователя на локальном компьютере с proxyAddress hello как**smtp:tax@contoso.com**
3. Когда Azure AD Connect будет синхронизировать hello новой учетной записи пользователя, появится ошибка «ObjectTypeMismatch» hello.

#### <a name="how-toofix-objecttypemismatch-error"></a>Как toofix ObjectTypeMismatch ошибки
Наиболее распространенной причиной ошибки ObjectTypeMismatch hello Hello — два объекта другого типа (пользователя, группы, обратитесь в службу и т.д.) имеют одинаковое значение для атрибута ProxyAddresses hello hello. В порядке hello toofix ObjectTypeMismatch:

1. Определить повторяющийся hello proxyAddresses (или другой атрибут) значение, что может вызвать ошибки hello. Также определять два \(или более\) объекты вовлеченные в конфликт hello. Здравствуйте, отчет, сформированный [Azure AD Connect Health для синхронизации](https://aka.ms/aadchsyncerrors) может помочь выявить hello двух объектов.
2. Определите, какой объект следует продолжить toohave hello повторяющиеся значения и какой объект не должен.
3. Удалите повторяющийся hello значение из hello объекта, который не следует это значение. Обратите внимание, что необходимо внести изменения в каталоге hello, который является источником hello объекта из hello. В некоторых случаях может потребоваться toodelete один из объектов hello в конфликте.
4. Если вы внесли изменения в hello в локальной среде AD hello, позволяют изменить hello синхронизации Azure AD Connect. Отчет об ошибках синхронизации в Azure AD Connect Health для синхронизации обновляется каждые 30 минут и включает hello ошибки последней попытки синхронизации hello.

## <a name="duplicate-attributes"></a>Повторяющиеся атрибуты
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Описание
Атрибуты Azure Active Directory схем не разрешает двух или более объектов toohave hello hello следуя тем же значением. Является каждого объекта в Azure AD принудительного toohave уникальное значение этих атрибутов для данного экземпляра.

* ProxyAddresses
* UserPrincipalName

Если Azure AD Connect пытается tooadd объекта или обновить существующий объект со значением для hello выше атрибутов, уже назначенный объект tooanother в Azure Active Directory, операция hello приводит ошибки синхронизации «AttributeValueMustBeUnique» hello.

#### <a name="possible-scenarios"></a>Возможные сценарии
1. Повторяющееся значение: назначенного tooan уже синхронизирован объекта, который конфликтует с другим объектом синхронизирован.

#### <a name="example-case"></a>Пример
1. Пользователь **Григорий Авдеев** синхронизирован в Azure AD из локального каталога AD в домене contoso.com.
2. Для атрибута **userPrincipalName** Григория в локальном каталоге задано значение **bobs@contoso.com**.
3. Боб также имеет следующие значения для hello **proxyAddresses** атрибута:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Новый пользователь **Taylor Боб**, добавляется toohello в локальной среде Active Directory.
5. Для атрибута **userPrincipalName** Артема задано значение **bobt@contoso.com**.
6. **Боб Taylor** имеет следующие значения для hello hello **ProxyAddresses** атрибут i. smtp:bobt@contoso.com. smtp:bob.taylor@contoso.com
7. Синхронизация объекта Артема Кузнецова выполнена успешно.
8. Администратор решил Taylor Боб tooupdate **ProxyAddresses** атрибута с hello следующие значения: i. **smtp:bob@contoso.com**
9. Azure AD будет tooupdate Боб Taylor объекта в Azure AD с hello выше значения, но, операция завершится ошибкой в том, что значение ProxyAddresses уже назначен tooBob Smith, приведет к ошибке «AttributeValueMustBeUnique».

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Как toofix AttributeValueMustBeUnique ошибки
Hello самая распространенная причина ошибки AttributeValueMustBeUnique hello имеет два объекта с разных SourceAnchor \(immutableId\) имеют одинаковое значение для hello ProxyAddresses и (или) атрибуты UserPrincipalName hello. В порядке toofix AttributeValueMustBeUnique ошибки

1. Определите proxyAddresses hello дублирован, userPrincipalName или другие значения атрибута, вызвавших ошибки hello. Также определять два \(или более\) объекты вовлеченные в конфликт hello. Здравствуйте, отчет, сформированный [Azure AD Connect Health для синхронизации](https://aka.ms/aadchsyncerrors) может помочь выявить hello двух объектов.
2. Определите, какой объект следует продолжить toohave hello повторяющиеся значения и какой объект не должен.
3. Удалите повторяющийся hello значение из hello объекта, который не следует это значение. Обратите внимание, что необходимо внести изменения в каталоге hello, который является источником hello объекта из hello. В некоторых случаях может потребоваться toodelete один из объектов hello в конфликте.
4. При внесении изменения в hello в локальной среде AD hello позволяют изменить для фиксированной tooget ошибка hello hello синхронизации Azure AD Connect.

#### <a name="related-articles"></a>Связанные статьи
-[Duplicate or invalid attributes prevent directory synchronization in Office 365](https://support.microsoft.com/en-us/kb/2647098) (Запрет синхронизации службы каталогов в Office 365 из-за повторяющихся или недопустимых атрибутов)

## <a name="data-validation-failures"></a>Сбой проверки данных
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Описание
Azure Active Directory обеспечивает различные ограничения на hello сами данные перед разрешением, toobe данные записываются в каталог hello. Это tooensure, конечные пользователи могут получить возможных возможности hello при использовании приложения hello, зависящих от этих данных.

#### <a name="scenarios"></a>Сценарии
а. Hello UserPrincipalName значения атрибута имеет недопустимые или неподдерживаемые символы.
b. атрибут UserPrincipalName Hello не соответствует требуемому формату hello.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Как toofix IdentityDataValidationFailed ошибки
а. Убедитесь, что этот атрибут userPrincipalName hello поддерживала символов и требуемый формат.

#### <a name="related-articles"></a>Связанные статьи
* [Подготовка пользователей tooprovision через tooOffice синхронизации каталогов 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>Ошибка FederatedDomainChangeError
#### <a name="description"></a>Описание
Это определенный регистр, в результате **«FederatedDomainChangeError»** ошибка синхронизации при изменении hello суффикс UserPrincipalName пользователя из одного домена tooanother федеративной федеративный домен.

#### <a name="scenarios"></a>Сценарии
Для синхронизированного пользователя hello UserPrincipalName суффикс был изменен с одной федеративный домен федеративный домен tooanother на локальном компьютере. Например *UserPrincipalName = bob@contoso.com*  было изменено слишком*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Пример
1. Алексей иванов учетной записи для Contoso.com, добавляется как новых пользователей в Active Directory с hello UserPrincipalNamebob@contoso.com
2. Боб перемещает изменены другой деления tooa домена contoso.com, Fabrikam.com и его UserPrincipalNametoobob@fabrikam.com
3. Домены contoso.com и fabrikam.com — это федеративные домены Azure AD.
4. Атрибут userPrincipalName Григория не обновляется, поэтому возникла ошибка синхронизации FederatedDomainChangeError.

#### <a name="how-toofix"></a>Как toofix
Если суффикс UserPrincipalName пользователя был обновлен от Виктора @**contoso.com** toobob @**fabrikam.com**, где оба **contoso.com** и **fabrikam.com** , **федеративных доменов**, затем выполните эти шаги ошибку синхронизации hello toofix

1. Обновить пользователя hello UserPrincipalName в Azure AD из bob@contoso.com toobob@contoso.onmicrosoft.com. Можно использовать следующую команду PowerShell с помощью модуля Azure AD PowerShell hello hello.`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Разрешить hello следующей синхронизации цикла tooattempt синхронизации. Время синхронизации будет выполнено успешно, и будет выполнено обновление hello UserPrincipalName Боб toobob@fabrikam.com должным образом.

#### <a name="related-articles"></a>Связанные статьи
* [Изменения не синхронизированы hello средство синхронизации Azure Active Directory после изменения hello UPN toouse учетной записи пользователя другой федеративный домен](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Описание
Когда атрибут превышает hello допускается максимального размера, ограничение на длину или предельное число задается схема Azure Active Directory, операция синхронизации hello приводит hello **LargeObject** или **ExceededAllowedLength** ошибка синхронизации. Эта ошибка обычно возникает для hello следующие атрибуты

* userCertificate
* userSMIMECertificate
* thumbnailPhoto;
* proxyAddresses

### <a name="possible-scenarios"></a>Возможные сценарии
1. Атрибут userCertificate Боба хранящей слишком много tooBob сертификаты. К ним также относятся недействительные и старые сертификаты. жесткий предел Hello — 15 сертификаты. Дополнительные сведения о как атрибут toohandle LargeObject ошибок с userCertificate, пожалуйста ссылаться tooarticle [LargeObject обработки ошибок, вызванных userCertificate атрибут](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Атрибут userSMIMECertificate Боба хранящей слишком много tooBob сертификаты. К ним также относятся недействительные и старые сертификаты. жесткий предел Hello — 15 сертификаты.
3. ThumbnailPhoto Боба, заданных в Active Directory является слишком большой toobe синхронизированы в Azure AD.
4. Во время автоматического заполнения атрибута ProxyAddresses hello в Active Directory имеет слишком много ProxyAddresses назначенный объект.

### <a name="how-toofix"></a>Как toofix
1. Убедитесь, что этот атрибут hello, которая привела к ошибке hello находится в пределах hello допустимое ограничение.

## <a name="related-links"></a>Связанные ссылки
* [Locate Active Directory Objects in Active Directory Administrative Center](https://technet.microsoft.com/library/dd560661.aspx) (Поиск объектов Active Directory в центре администрирования Active Directory)
* [Как tooquery Azure Active Directory для объекта с помощью Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
