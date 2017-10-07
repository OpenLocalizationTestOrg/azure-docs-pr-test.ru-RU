---
title: "Устойчивость aaaIdentity синхронизации и дубликат атрибута | Документы Microsoft"
description: "Новое поведение toohandle объектов с помощью имени участника-пользователя или ProxyAddress конфликтов во время синхронизации каталогов с помощью Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Синхронизация удостоверений и устойчивость повторяющихся атрибутов
Устойчивость повторяющихся атрибутов — это компонент Azure Active Directory, устраняющий проблемы из-за конфликтов атрибутов **UserPrincipalName** и **ProxyAddress** при запуске средств синхронизации Майкрософт.

Эти атрибуты являются обычно требуется toobe уникальным во всех **пользователя**, **группы**, или **контакт** объектов в заданной клиента Azure Active Directory.

> [!NOTE]
> Только пользователи могут иметь имена участников-пользователей (UPN).
> 
> 

в части конвейера синхронизации hello облака hello Hello новое поведение, эта функция позволяет, таким образом это клиент, независимые и соответствующие для любого продукта Microsoft синхронизации, включая Azure AD Connect, DirSync и MIM + соединителя. Hello универсальный термин «клиент синхронизации» используется в toorepresent этого документа, один из этих продуктов.

## <a name="current-behavior"></a>Текущее поведение
Если попытка tooprovision новый объект со значением имени участника-пользователя или ProxyAddress, которые нарушают это ограничение уникальности, Azure Active Directory блокирует этот объект создаются. Аналогично Если объект обновляется с неуникальное имя участника-пользователя или ProxyAddress, hello обновление завершилось ошибкой. Здравствуйте, подготовки обновления или попытка будет предпринята повторная попытка синхронизации клиентом hello после каждого цикла экспорта и toofail продолжается, пока hello конфликт разрешается. Сообщение электронной почты ошибки отчета создается при каждой попытке и регистрирует ошибку hello синхронизации клиента.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Поведение с устойчивостью повторяющихся атрибутов
Вместо полного сбоя tooprovision или обновления с повторяющимся атрибутом Azure Active Directory» в карантин» hello повторяющийся атрибут, который нарушает ограничение уникальности hello объекта. Если этот атрибут является обязательным для инициализации, такие как UserPrincipalName, hello служба присваивает значение заполнителя. Формат Hello эти временные значения:  
“***<OriginalPrefix>+<четырехзначное_число>@<InitialTenantDomain>.onmicrosoft.com***”.</четырехзначное_число>>  
Если атрибут hello не является обязательной, например **ProxyAddress**, Azure Active Directory просто карантин атрибут конфликт hello и выполняет создание hello объекта или обновления.

После отправки в карантин атрибут hello, сведения о конфликте hello отправляется в hello же ошибки отчета по электронной почте используется старое поведение hello. Тем не менее эти сведения отображается только в отчет об ошибке hello один раз, когда происходит карантина hello, его не продолжать toobe регистрации в журнале сообщений электронной почты. Кроме того с момента успешного экспорта hello для этого объекта hello синхронизации клиента не регистрирует ошибку и не повтора hello Создание или обновление операции при последующей синхронизации циклов.

toosupport такое поведение нового атрибута была добавлены классы объектов toohello пользователей, групп и контактов:  
**DirSyncProvisioningErrors**

Это многозначный атрибут, который используется toostore hello конфликтующие атрибуты приведет к нарушению ограничения уникальности hello следует их добавить обычно является. В фоновом режиме таймер включен в Azure Active Directory, который выполняется каждый час toolook конфликтов повторяющийся атрибут разрешения, которые автоматически удаляет hello атрибуты рассматриваемый из карантина.

### <a name="enabling-duplicate-attribute-resiliency"></a>Включение устойчивости повторяющихся атрибутов
Повторяющийся атрибут устойчивости будет новое поведение по умолчанию hello распределяются по всем клиентам Azure Active Directory. Он будет иметь по умолчанию для всех клиентов, которые включены в синхронизацию для hello первый раз 22 августа 2016 г. или более поздней версии. Клиенты, которые включены даты предыдущего toothis синхронизации будет включена в пакетах функция hello. Развертывания начнется в сентябре 2016 года, а уведомление по электронной почте будет отправлено контакт Техническое Уведомление клиента tooeach hello определенную дату, когда hello будет включена.

> [!NOTE]
> После включения режим устойчивости повторяющихся атрибутов невозможно отключить.

toocheck, если включена функция hello для вашего клиента, это можно сделать, скачав последнюю версию модуля Azure Active Directory PowerShell hello hello и запустив:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Больше не функция MsolDirSyncFeature набор командлет tooproactively enable hello повторяющийся атрибут устойчивости, прежде чем он включен для вашего клиента. функция hello может tootest toobe, необходимо будет toocreate новый клиент Azure Active Directory.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Идентификация объектов с DirSyncProvisioningErrors
В настоящее время двумя способами tooidentify объекты с ошибками из-за конфликтов tooduplicate свойств, Azure Active Directory PowerShell и hello портал администрирования Office 365. Нет планов tooextend tooadditional портал на основе отчетов в будущем hello.

### <a name="azure-active-directory-powershell"></a>PowerShell Azure Active Directory
Для hello командлеты PowerShell в этом разделе справедливо следующее hello:

* Все следующие командлеты hello чувствительны к регистру.
* Hello **— ErrorCategory PropertyConflict** всегда должен быть включен. В настоящее время нет других типов из **ErrorCategory**, но это может быть расширен в будущем hello.

Для начала выполните командлет **Connect-MsolService** и введите учетные данные администратора клиента.

Выполните следующие командлеты и операторы tooview ошибки по-разному hello.

1. [Смотреть все](#see-all)
2. [По типу свойства.](#by-property-type)
3. [По конфликтующему значению.](#by-conflicting-value)
4. [С помощью поиска по строкам.](#using-a-string-search)
5. [Сортированные.](#sorted)
6. [В ограниченном количестве или все.](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Смотреть все
После подключения toosee общий список атрибутов, ошибки в клиенте hello подготовки выполните:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Результат hello следующим образом:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>По типу свойства.
ошибки toosee типом свойства, добавьте hello **- PropertyName** флаг с hello **UserPrincipalName** или **ProxyAddresses** аргумент:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Или

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>По конфликтующему значению.
добавить toosee проблем в определенное свойство tooa hello **- PropertyValue** флаг (**- PropertyName** необходимо также использовать при добавлении этого флага):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>С помощью поиска по строкам.
Поиск широкие строки toodo использовать hello **- SearchString** флаг. Это может использоваться независимо от всех hello выше флаги исключением hello **- ErrorCategory PropertyConflict**, которой требуется всегда:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>В ограниченном количестве или все.
1. **MaxResults <Int>**  можно использовать toolimit hello запроса tooa определенное число значений.
2. **Все** может быть используется tooensure, извлекаются все результаты в случае hello, существует большое количество ошибок.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Портал администрирования Office 365
Ошибки при синхронизации службы каталогов можно просмотреть в центре администрирования Office 365 hello. Здравствуйте, отчет отображается только портала Office 365 hello **пользователя** объекты, имеющие эти ошибки. Этот отчет не содержит сведений о конфликтах между такими объектами, как **Группы** и **Контакты**.

![Активные пользователи](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Активные пользователи")

Инструкции по как tooview ошибки синхронизации каталогов в Office 365 Здравствуйте, администратор центра см [выявить ошибки синхронизации каталогов Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Отчет об ошибках синхронизации удостоверений
При обработке объекта с конфликтом повторяющийся атрибут с помощью этого нового поведения уведомление, включенный в hello стандартный отчет об ошибках синхронизации удостоверений электронной почты, который отправляется toohello Техническое уведомление контакта для клиента hello. Но в этом поведении есть важные изменения. В прошлом hello сведений о конфликте повторяющийся атрибут будет включено во всех отчетов после ошибки до hello конфликт был разрешен. С помощью этого нового поведения hello уведомление об ошибке для данного конфликта использоваться только один раз — момент hello конфликтующим атрибутом hello в карантин.

Ниже приведен пример того, как выглядит какие hello уведомление по электронной почте о конфликте ProxyAddress:  
    ![Активные пользователи](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Активные пользователи")  

## <a name="resolving-conflicts"></a>Разрешение конфликтов
Устранение неполадок тактика стратегии и разрешения этих ошибок не должны отличаться от hello обработки ошибок повторяющийся атрибут были в прошлом hello. Hello единственное различие заключается в переходов задачи таймера hello через hello клиента на стороне службы tooautomatically hello добавлять атрибут hello в надлежащий объект toohello вопроса после конфликта hello.

Hello следующей статье описаны различные стратегии устранения неполадок и разрешения: [дубликаты или недопустимые атрибуты предотвратить синхронизацию каталогов на Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Известные проблемы
Ни одна из известных проблем не приводит к потере данных или снижению производительности службы. Некоторые из них являются внешнего вида, другие привести standard»*предварительной устойчивости*"повторяющийся атрибут ошибки toobe исключение вместо карантин hello конфликт атрибута, а другой вызывает определенные ошибки toorequire лишние вручную исправить доступ.

**Основное поведение**

1. Объекты с конфигурациями определенный атрибут по-прежнему ошибки экспорта tooreceive как противоположность toohello повторяющиеся атрибуты в карантине.  
   Например:
   
    а. В Active Directory создается новый пользователь со следующими свойствами: имя участника-пользователя (UPN) — **Joe@contoso.com**, ProxyAddress — **smtp:Joe@contoso.com**.
   
    b. Hello свойства этого объекта конфликтуют с существующей группой, где ProxyAddress  **SMTP:Joe@contoso.com** .
   
    c. При экспорте **конфликт ProxyAddress** вместо атрибутов конфликт hello в карантин, возникает ошибка. Hello операция повторяется после каждого цикла последующие синхронизации, как это было бы до включения функции hello исправления.
2. Если две группы создаются локально hello же SMTP-адрес, tooprovision один завершается с ошибкой при первой попытке hello с помощью стандартного повторяющиеся **ProxyAddress** ошибки. Тем не менее повторяющееся значение hello должным образом в карантин при hello следующего цикла синхронизации.

**Отчет на портале Office**

1. Hello подробное сообщение об ошибке для двух объектов в наборе конфликт имени участника-пользователя является таким же hello. Это означает, что свойство UPN обоих объектов изменено или помещено на карантин, но на самом деле данные изменились только в одном объекте.
2. Hello подробное сообщение об ошибке для конфликта UPN показывает hello неправильный displayName для пользователя, который был их имя участника-пользователя изменен карантин. Например:
   
    а. Сначала синхронизируется **пользователь A** с именем участника-пользователя **User@contoso.com**.
   
    b. **Пользователь Б** попытки toobe синхронизирован предыдущий с **UPN = User@contoso.com** .
   
    c. **Пользователь Б** UPN изменяется слишком **User1234@contoso.onmicrosoft.com**  и  **User@contoso.com**  добавляется слишком**DirSyncProvisioningErrors**.
   
    d. сообщение об ошибке Hello **пользователь Б** следует указать, что **пользователь A** уже  **User@contoso.com**  как имя участника-пользователя, но он показывает **пользователь Б** собственные отображаемое имя.

**Отчет об ошибках синхронизации удостоверений**.

Hello ссылку для *о том, как tooresolve этой проблемы* неверно:  
    ![Активные пользователи](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Активные пользователи")  

Он должен указывать слишком[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>См. также
* [Службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
* [Определение ошибок синхронизации службы каталогов в Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

