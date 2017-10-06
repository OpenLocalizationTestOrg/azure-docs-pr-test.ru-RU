---
title: "Синхронизация Azure AD Connect: справочник по функциям | Документация Майкрософт"
description: "Общие сведения о выражениях декларативной подготовки в Azure AD Connect Sync"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Синхронизация Azure AD Connect: справочник по функциям
В Azure AD Connect функции, используемые toomanipulate значение атрибута во время синхронизации.  
Синтаксис функции hello Hello выражается с помощью hello следующий формат:  
`<output type> FunctionName(<input type> <position name>, ..)`

Если функция перегружена и принимает несколько вариантов синтаксиса, перечисляются все допустимые варианты синтаксиса.  
функции Hello строго типизированы и проверяют, тип hello переданный тип hello задокументированы совпадений.  
Если тип hello не совпадают, возникает ошибка.

типы Hello выражаются с hello, используя синтаксис:

* **bin** – двоичное значение
* **bool** — логическое значение
* **dt** — дата и время в формате UTC
* **enum** — перечисление известных констант
* **EXP** — выражение, являющееся ожидается tooevaluate tooa логическое значение
* **mvbin** — двоичное значение с несколькими значениями.
* **mvstr** — строка с несколькими значениями.
* **mvref** — ссылка с несколькими значениями.
* **num** — числовое значение
* **ref** — ссылка.
* **str** — строка.
* **var** — вариант (почти) любого другого типа
* **void** — не возвращает значение

Здравствуйте, функции, имеющие типы hello **mvbin**, **mvstr**, и **mvref** может работать только с несколькими значениями атрибутов. Функции типов **bin**, **str** и **ref** работают с однозначными и многозначными атрибутами.

## <a name="functions-reference"></a>Справочник по функциям
| Список функций |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificate** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[ CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Преобразование** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Date / Time** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Каталог** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Оценка** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Math** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Функции с несколькими значениями:** | | | | |
| [Содержит](#contains) |[Count](#count) |[Элемент](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[разделение;](#split) | | |
| **Program Flow** | | | | |
| [Ошибка](#error) |[IIF](#iif) |[Выбор](#select) |[Switch](#switch) | |
| [Where](#where) |[With](#with) | | | |
| **текст** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Замените](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Описание.**  
Hello функция BitAnd устанавливает указанные биты значения.

**Синтаксис**  
`num BitAnd(num value1, num value2)`

* value1, value2: числовые значения, которые должны быть соединены оператором AND.

**Примечания:**  
Эта функция преобразует оба параметры toohello двоичное представление и устанавливает для бита:

* 0 — Если один или оба соответствующих бита в Здравствуйте, *маска* и *флаг* : 0
* 1 — Если оба соответствующих бита hello равны 1.

Другими словами она возвращает 0 во всех случаях, за исключением случаев, когда hello соответствующие биты в обоих параметрах равны 1.

**Пример**  
`BitAnd(&HF, &HF7)`  
Возвращает 7, так как шестнадцатеричное "F" и «F7» вычислить значение toothis.

- - -
### <a name="bitor"></a>BitOr
**Описание.**  
Hello функция BitOr устанавливает указанные биты значения.

**Синтаксис**  
`num BitOr(num value1, num value2)`

* value1, value2: числовые значения, которые должны быть соединены оператором OR.

**Примечания:**  
Эта функция преобразует оба параметры toohello двоичное представление и задает too1 бит, если один или оба соответствующих бита hello в маске и флаге 1 и too0, если оба соответствующих бита hello равны 0. Другими словами он возвращает 1 во всех случаях, за исключением того, где hello соответствующие биты в обоих параметрах равны 0.

- - -
### <a name="cbool"></a>CBool
**Описание.**  
Hello функция CBool возвращает логическое выражение вычисляется hello

**Синтаксис**  
`bool CBool(exp Expression)`

**Примечания:**  
Если hello выражения вычисляется tooa ненулевое значение, CBool возвращает True, в противном случае он возвращает значение False.

**Пример**  
`CBool([attrib1] = [attrib2])`  

Здравствуйте, возвращает True, если атрибуты имеют одинаковое значение.

- - -
### <a name="cdate"></a>CDate
**Описание.**  
Hello Функция CDate возвращает UTC DateTime из строки. DateTime не является собственным типом атрибута синхронизации, но используется некоторыми функциями.

**Синтаксис**  
`dt CDate(str value)`

* Value: строка с датой, временем и (необязательно) часовым поясом.

**Примечания:**  
Hello возвращается строка всегда находится в формате UTC.

**Пример**  
`CDate([employeeStartTime])`  
Возвращает значение DateTime, на основе времени начала hello сотрудника

`CDate("2013-01-10 4:00 PM -8")`  
Возвращает объект DateTime, представляющий значение 2013-01-11 12:00 AM.








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Описание.**  
Возвращает hello значения Oid все критические расширения hello объекта сертификата.

**Синтаксис**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certformat"></a>CertFormat
**Описание.**  
Возвращает hello имя hello формата сертификата X.509v3.

**Синтаксис**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Описание.**  
Возвращает hello связанный псевдоним для сертификата.

**Синтаксис**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certhashstring"></a>CertHashString
**Описание.**  
Возвращает хэш-значение SHA1 для сертификата X.509v3 hello hello виде шестнадцатеричной строки.

**Синтаксис**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certissuer"></a>CertIssuer
**Описание.**  
Возвращает hello имя hello сертификации, выдавшего сертификат X.509v3 hello.

**Синтаксис**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Описание.**  
Возвращает hello различающееся имя издателя сертификата hello.

**Синтаксис**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Описание.**  
Возвращает hello Oid hello издателя сертификата.

**Синтаксис**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Описание.**  
Возвращает hello сведения об алгоритме ключа для сертификата X.509v3 в виде строки.

**Синтаксис**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Описание.**  
Возвращает hello параметры алгоритма ключа для сертификата X.509v3 hello в виде шестнадцатеричной строки.

**Синтаксис**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Описание.**  
Возвращает hello субъекта и издателя имена из сертификата.

**Синтаксис**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.
*   X509NameType: hello X509NameType значение для темы hello.
*   includesIssuerName: имя издателя hello tooinclude значение true; в противном случае — значение false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Описание.**  
Возвращает hello дату в формате местного времени, после чего сертификат является допустимым.

**Синтаксис**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Описание.**  
Возвращает hello дату в формате местного времени, в которой сертификат становится действительным.

**Синтаксис**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Описание.**  
Возвращает hello Oid hello открытого ключа для сертификата X.509v3 hello.

**Синтаксис**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Описание.**  
Возвращает hello Oid hello параметров открытого ключа для сертификата X.509v3 hello.

**Синтаксис**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Описание.**  
Возвращает серийный номер сертификата X.509v3 hello hello.

**Синтаксис**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Описание.**  
Возвращает hello Oid hello алгоритма используется toocreate hello подписи сертификата.

**Синтаксис**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certsubject"></a>CertSubject
**Описание.**  
Возвращает hello различающееся имя субъекта из сертификата.

**Синтаксис**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Описание.**  
Возвращает hello различающееся имя субъекта из сертификата.

**Синтаксис**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Описание.**  
Возвращает hello Oid hello имени субъекта из сертификата.

**Синтаксис**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**Описание.**  
Возвращает hello отпечаток сертификата.

**Синтаксис**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="certversion"></a>CertVersion
**Описание.**  
Возвращает hello версию формата сертификата X.509.

**Синтаксис**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.

- - -
### <a name="cguid"></a>CGuid
**Описание.**  
Hello функция CGuid Преобразует строковое представление hello tooits двоичное представление идентификатора GUID.

**Синтаксис**  
`bin CGuid(str GUID)`

* Строка отформатирована по следующему шаблону: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx или {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Содержит
**Описание.**  
функции Hello Contains находит строку внутри многозначного атрибута

**Синтаксис**  
`num Contains (mvstring attribute, str search)` — с учетом регистра  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` — с учетом регистра

* атрибут: hello toosearch многозначного атрибута.
* Поиск: строка toofind в атрибуте hello.
* Casetype: без учета регистра или с учетом регистра.

Возвращает индекс в многозначном атрибуте hello, где найдена строка hello. Если строка hello не найдена, возвращается 0.

**Примечания:**  
Для многозначных строковых атрибутов hello искомое подстроки в значениях hello.  
Для ссылочных атрибутов hello искомая строка должна точно соответствовать рассматриваются как совпадающие toobe значение hello.

**Пример**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Если атрибут proxyAddresses hello содержит основной адрес электронной почты (обозначается в верхний регистр «SMTP:»), возвращается атрибут proxyAddress hello, в противном случае возвращает сообщение об ошибке.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Описание.**  
Hello ConvertFromBase64 функция преобразует hello указан строка регулярного tooa значение в кодировке base64.

**Синтаксис**  
`str ConvertFromBase64(str source)` — здесь предполагается кодирование Юникод.  
`str ConvertFromBase64(str source, enum Encoding)`

* source: строка в кодировке Base64  
* Кодировка: Юникод, ASCII, UTF8

**Пример**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Оба примера возвращают сообщение "*Hello world!*".

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Описание.**  
Hello ConvertFromUTF8Hex функция преобразует hello указанную строку tooa значение шестнадцатеричной кодировке UTF8.

**Синтаксис**  
`str ConvertFromUTF8Hex(str source)`

* source: строка в двухбайтовой кодировке UTF8.

**Примечания:**  
Hello различие между этой функции и ConvertFromBase64([],UTF8) в результате этого hello понятное для атрибута DN hello.  
Azure Active Directory использует этот формат в качестве различающегося имени.

**Пример**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Возвращает сообщение*Hello world!*.

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Описание.**  
Hello функция ConvertToBase64 преобразует строку tooa Юникода в кодировке Base64.  
Преобразует значение hello массив целых чисел tooits эквивалентное строковое представление, представлен в кодировке base-64 знаков.

**Синтаксис**  
`str ConvertToBase64(str source)`

**Пример**  
`ConvertToBase64("Hello world!")`  
Возвращает SABlAGwAbABvACAAdwBvAHIAbABkACEA.

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Описание.**  
Hello функция ConvertToUTF8Hex преобразует строку tooa значение шестнадцатеричной кодировке UTF8.

**Синтаксис**  
`str ConvertToUTF8Hex(str source)`

**Примечания:**  
Hello формат вывода этой функции используется службой Azure Active Directory в качестве формата атрибута DN.

**Пример**  
`ConvertToUTF8Hex("Hello world!")`  
Возвращает 48656C6C6F20776F726C6421.

- - -
### <a name="count"></a>Count
**Описание.**  
Hello функция Count возвращает количество элементов в hello в многозначном атрибуте

**Синтаксис**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Описание.**  
Hello функция CNum принимает строку и возвращает числовой тип данных.

**Синтаксис**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Описание.**  
Преобразует строку tooa ссылочный атрибут

**Синтаксис**  
`ref CRef(str value)`

**Пример**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Описание.**  
Hello функция CStr преобразует tooa строкового типа данных.

**Синтаксис**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* value: может быть числовым значением, ссылочным атрибутом или логическим значением.

**Пример**  
`CStr([dn])`  
Может вернуть cn=Joe,dc=contoso,dc=com.

- - -
### <a name="dateadd"></a>DateAdd
**Описание.**  
Возвращает дату, содержащий toowhich даты, который был добавлен указанный интервал времени.

**Синтаксис**  
`dt DateAdd(str interval, num value, dt date)`

* интервал: строковое выражение, интервал времени, tooadd hello. Строка Hello должен иметь одно из hello следующие значения:
  * yyyy год
  * q квартал
  * m месяц
  * y день года
  * d день
  * w день недели
  * ww неделя
  * h час
  * n минута
  * s секунда
* значение: hello число единиц, требуется tooadd. Оно может быть положительным (tooget даты в будущем hello) или отрицательное (tooget даты в прошлом hello).
* Дата: DateTime, представляющих дату toowhich hello интервал добавляется.

**Пример**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
Добавляет три месяца и возвращает значение DateTime 2001-04-01.

- - -
### <a name="datefromnum"></a>DateFromNum
**Описание.**  
Hello функция DateFromNum преобразует значение в tooa формат даты AD типа DateTime.

**Синтаксис**  
`dt DateFromNum(num value)`

**Пример**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
Возвращает значение DateTime, равное 2012-01-01 23:00:00.

- - -
### <a name="dncomponent"></a>DNComponent
**Описание.**  
Hello функция DNComponent возвращает значение hello указанного компонента различающегося Имени, отсчитываемого слева.

**Синтаксис**  
`str DNComponent(ref dn, num ComponentNumber)`

* различающееся имя: hello ссылку атрибут toointerpret
* ComponentNumber: компонент hello в tooreturn hello DN

**Пример**  
`DNComponent([dn],1)`  
Если значение различающегося имени равно cn=Joe,ou=…, функция возвращает Joe.

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Описание.**  
Hello функция DNComponentRev возвращает значение hello указанного компонента различающегося Имени, отсчитываемого справа (hello end).

**Синтаксис**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* различающееся имя: hello ссылку атрибут toointerpret
* ComponentNumber - компонент hello в tooreturn hello DN
* Options: DC — игнорировать все компоненты с "dc=".

**Пример**  
Если различающееся имя — cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com, то  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
оба вернут US.

- - -
### <a name="error"></a>Ошибка
**Описание.**  
функции ошибок Hello — используется tooreturn настраиваемой ошибки.

**Синтаксис**  
`void Error(str ErrorMessage)`

**Пример**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Если отсутствует атрибут accountName hello, вызывают ошибку для hello объекта.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Описание.**  
функция EscapeDNComponent Hello один компонент различающегося имени и переключает его, поэтому он может быть представлен в LDAP.

**Синтаксис**  
`str EscapeDNComponent(str value)`

**Пример**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Гарантирует, что hello объекта может быть создан в каталоге LDAP, даже если hello атрибут displayName содержит символы, которые необходимо экранировать в LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Описание.**  
функция FormatDateTime Hello — используется tooformat строка tooa DateTime в указанном формате

**Синтаксис**  
`str FormatDateTime(dt value, str format)`

* значение: значение в формате DateTime hello
* формат: строка, представляющая hello tooconvert формат для.

**Примечания:**  
Здравствуйте возможные значения для hello формата можно найти здесь: [определяемые пользователем форматы даты и времени (функция Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Пример**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
выдает результат 2007-12-25.

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
может вернуть результат 20140905081453.0Z.

- - -
### <a name="guid"></a>GUID
**Описание.**  
Hello функция GUID создает случайный идентификатор GUID

**Синтаксис**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Описание.**  
Hello функции IIF возвращает один из набора возможных значений на основе заданного условия.

**Синтаксис**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* условие: любое значение или выражение, которое может быть вычислено tootrue или false.
* valueIfTrue: hello условие tootrue, hello возвращенное значение.
* valueIfFalse: hello условие toofalse, hello возвращенное значение.

**Пример**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Если пользователь hello интернирования, возвращает hello псевдоним пользователя, имеющего «t-» добавлены toohello начале, else возвращает псевдоним пользователя hello без изменений.

- - -
### <a name="instr"></a>InStr
**Описание.**  
Hello функция InStr находит hello первого вхождения подстроки в строке.

**Синтаксис**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* проверяемая_строка: строка toobe поиск
* искомая_строка: строка найдена toobe
* Начать: начиная с позиции toofind hello подстроки
* compare: vbTextCompare или vbBinaryCompare.

**Примечания:**  
Позиция возвращает hello, где было найдено подстроки hello или 0, если не найден.

**Пример**  
`InStr("hello quick brown fox","quick")`  
/ / Возвращает too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Результатом является too7

- - -
### <a name="instrrev"></a>InStrRev
**Описание.**  
Hello функция InStrRev находит hello последнее вхождение подстроки в строке.

**Синтаксис**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* проверяемая_строка: строка toobe поиск
* искомая_строка: строка найдена toobe
* Начать: начиная с позиции toofind hello подстроки
* compare: vbTextCompare или vbBinaryCompare.

**Примечания:**  
Позиция возвращает hello, где было найдено подстроки hello или 0, если не найден.

**Пример**  
`InStrRev("abbcdbbbef","bb")`  
Возвращает значение 7.

- - -
### <a name="isbitset"></a>IsBitSet
**Описание.**  
Hello функция IsBitSet проверяет, если битовое или нет

**Синтаксис**  
`bool IsBitSet(num value, num flag)`

* значение: числовое значение, представляющее evaluated.flag: числовое значение, которое имеет hello бит toobe оценка

**Пример**  
`IsBitSet(&HF,4)`  
Возвращает значение True, так как «4» бита в шестнадцатеричное значение hello «F»

- - -
### <a name="isdate"></a>IsDate
**Описание.**  
Если hello выражение может быть hello Функция IsDate принимает tooTrue вычисляет типа DateTime.

**Синтаксис**  
`bool IsDate(var Expression)`

**Примечания:**  
Toodetermine используется в том случае, если функция CDate() может быть успешно.

- - -
### <a name="iscert"></a>IsCert
**Описание.**  
Возвращает значение true, если hello необработанные данные могут быть сериализованы в объект .NET X509Certificate2 сертификата.

**Синтаксис**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData: представление сертификата X.509 в виде массива байтов. Массив байтов Hello может быть бинарные (DER) или данных X.509 в кодировке Base64.
- - -
### <a name="isempty"></a>IsEmpty
**Описание.**  
Если атрибут hello в hello CS или MV, но результатом является пустая строка tooan, функция IsEmpty hello оценивает tooTrue.

**Синтаксис**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Описание.**  
Если строка hello удалось преобразованный tooa GUID, функция isguid возвращает hello вычисляется tootrue.

**Синтаксис**  
`bool IsGuid(str GUID)`

**Примечания:**  
GUID представляет собой строку, созданную по одному из этих шаблонов: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx или {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.

Toodetermine используется в том случае, если функция CGuid() может быть успешно.

**Пример**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Если hello атрибут StrAttribute имеет формат GUID, возвращает двоичное представление, в противном случае возвращает значение Null.

- - -
### <a name="isnull"></a>IsNull
**Описание.**  
Если hello выражение tooNull, hello IsNull, функция возвращает значение true.

**Синтаксис**  
`bool IsNull(var Expression)`

**Примечания:**  
Значение Null для атрибута, выражается hello отсутствие атрибута hello.

**Пример**  
`IsNull([displayName])`  
Возвращает значение True, если отсутствует атрибут hello в hello CS и MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Описание.**  
Если hello выражение имеет значение null или пустую строку, hello функция IsNullOrEmpty возвращает true.

**Синтаксис**  
`bool IsNullOrEmpty(var Expression)`

**Примечания:**  
Для атрибута эта функция tooTrue Если атрибут hello отсутствует или присутствует, но является пустой строкой.  
Hello обратная функция называется IsPresent.

**Пример**  
`IsNullOrEmpty([displayName])`  
Возвращает значение True, если атрибут hello не существует или является пустой строкой в hello CS и MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Описание.**  
Hello функция IsNumeric возвращает логическое значение, указывающее, является ли выражение может быть распознано как числовой тип.

**Синтаксис**  
`bool IsNumeric(var Expression)`

**Примечания:**  
Использовать toodetermine ли CNum() успешно tooparse hello выражения.

- - -
### <a name="isstring"></a>IsString
**Описание.**  
Если выражение hello может быть вычисленное tooa строковый тип, то hello функция IsString возвращает tooTrue.

**Синтаксис**  
`bool IsString(var expression)`

**Примечания:**  
Использовать toodetermine ли CStr() успешно tooparse hello выражения.

- - -
### <a name="ispresent"></a>IsPresent
**Описание.**  
Если hello выражение tooa строку, которая не имеет значение Null и не является пустым, затем hello IsPresent, функция возвращает значение true.

**Синтаксис**  
`bool IsPresent(var expression)`

**Примечания:**  
Hello обратная функция называется IsNullOrEmpty.

**Пример**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Элемент
**Описание.**  
Hello функция Item возвращает один элемент из многозначной строки или атрибута.

**Синтаксис**  
`var Item(mvstr attribute, num index)`

* attribute: атрибут с несколькими значениями
* Индекс: элемент tooan индекса в многозначную строку hello.

**Примечания:**  
Hello функция Item полезна в сочетании hello функция Contains так как последний функции hello возвращает элемент tooan индекса hello в многозначном атрибуте hello.

Вызывает ошибку, если индекс выходит за допустимые пределы.

**Пример**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Возвращает hello основной адрес электронной почты.

- - -
### <a name="itemornull"></a>ItemOrNull
**Описание.**  
Hello функция ItemOrNull возвращает один элемент из многозначной строки или атрибута.

**Синтаксис**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute: атрибут с несколькими значениями
* Индекс: элемент tooan индекса в многозначную строку hello.

**Примечания:**  
Hello функция ItemOrNull полезна в сочетании hello функция Contains так как последний функции hello возвращает элемент tooan индекса hello в многозначном атрибуте hello.

Возвращает значение Null, если индекс выходит за допустимые пределы.

- - -
### <a name="join"></a>Join
**Описание.**  
функции Hello Join принимает многозначную строку и возвращает однозначную строку с указанным разделителем между элементами.

**Синтаксис**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* атрибут: многозначный атрибут, содержащий строки toobe присоединен.
* разделитель: любая строка, используемые tooseparate подстроки hello вернул строку hello. Если не указано, hello символ пробела (» «) используется. Если разделитель является строкой нулевой длины ("») или Nothing, все элементы в списке hello сцепляются без разделителей.

**Примечания**  
Имеется соответствие между hello соединения и функции разбиения. Hello функция Join принимает массив строк и объединяет их с помощью строки-разделителя, tooreturn одну строку. Hello функция Split принимает строку и разбивает ее по разделителям hello, tooreturn массив строк. Эти функции различаются тем, что Join может объединять строки с любой строкой-разделителем, а Split может разделять строки с помощью одного символа-разделителя.

**Пример**  
`Join([proxyAddresses],",")`  
Может вернуть: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"

- - -
### <a name="lcase"></a>LCase
**Описание.**  
Hello функция LCase преобразует все символы в случае toolower строки.

**Синтаксис**  
`str LCase(str value)`

**Пример**  
`LCase("TeSt")`  
Возвращает значение Test.

- - -
### <a name="left"></a>Left
**Описание.**  
Hello функция Left возвращает указанное количество символов слева hello строки.

**Синтаксис**  
`str Left(str string, num NumChars)`

* строки: hello tooreturn символов строки из
* NumChars: число, задающее количество hello tooreturn символов с начала hello (слева), строки

**Примечания:**  
Строка, содержащая первые numChars символов hello в строке:

* если numChars = 0, возвращается пустая строка;
* если numChars < 0, возвращается введенная строка;
* если строка имеет значение Null, возвращается пустая строка.

Если строка содержит меньше символов, чем hello числу, заданному параметром numChars, возвращается строка идентичные toostring, (, содержащего все символы в параметр 1).

**Пример**  
`Left("John Doe", 3)`  
Возвращает значение Joh.

- - -
### <a name="len"></a>Len
**Описание.**  
Hello функция Len возвращает число символов в строке.

**Синтаксис**  
`num Len(str value)`

**Пример**  
`Len("John Doe")`  
Возвращает значение 8.

- - -
### <a name="ltrim"></a>LTrim
**Описание.**  
Hello функция LTrim удаляет начальные пробелы из строки.

**Синтаксис**  
`str LTrim(str value)`

**Пример**  
`LTrim(" Test ")`  
Возвращает значение Test.

- - -
### <a name="mid"></a>Mid
**Описание.**  
Здравствуйте, Mid функция возвращает указанное количество символов, начиная с указанной позиции в строке.

**Синтаксис**  
`str Mid(str string, num start, num NumChars)`

* строки: hello tooreturn символов строки из
* Начать: число, задающее hello, начальная позиция в строку символов tooreturn из
* NumChars: число, задающее количество hello tooreturn символов из положения в строке

**Примечания:**  
Возвращает символы numChars, начиная с позиции start в строке.  
Строка, содержащая numChars символов начиная с позиции start в строке:

* если numChars = 0, возвращается пустая строка;
* если numChars < 0, возвращается введенная строка;
* Если запустить > Здравствуйте, длина строки, возвращается исходная строка.
* если start < = 0, возвращается введенная строка;
* если строка имеет значение Null, возвращается пустая строка.

Если в строке не осталось numChar символов начиная с позиции start, возвращается столько символов, сколько может быть возвращено.

**Пример**  
`Mid("John Doe", 3, 5)`  
Возвращает значение hn Do.

`Mid("John Doe", 6, 999)`  
Возвращает значение Doe.

- - -
### <a name="now"></a>Now
**Описание.**  
Hello Теперь функция возвращает значение типа DateTime hello текущую дату и время, в соответствии с tooyour компьютера системной даты и времени.

**Синтаксис**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Описание.**  
Hello функция NumFromDate возвращает дату в формате.

**Синтаксис**  
`num NumFromDate(dt value)`

**Пример**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
Возвращает значение 129699324000000000.

- - -
### <a name="padleft"></a>PadLeft
**Описание.**  
Hello PadLeft функции left дополняет tooa строку, в указанный длины, используя заданный заполняющий символ.

**Синтаксис**  
`str PadLeft(str string, num length, str padCharacter)`

* строки: hello toopad строки.
* Длина: integer, представляющее hello требуемого длину строки.
* символ padCharacter: строка, состоящая из одного символа toouse как знак-заполнитель hello

**Примечания:**

* Если hello длина строки меньше length, символ padCharacter — многократно присоединенных toohello начало (слева) строки до его длина равна toolength.
* Значение padCharacter может быть символом пробела, но оно не может иметь значение Null.
* Если длина hello строки больше, чем длина равна tooor, строка возвращается без изменений.
* Если строка имеет длину больше или равно toolength, возвращается toostring одинаковые строки.
* Если hello длина строки меньше length, новая строка hello требуемого возвращается длина, содержащий строку, дополненную символом padCharacter.
* Если строка имеет значение null, функция hello возвращает пустую строку.

**Пример**  
`PadLeft("User", 10, "0")`  
Возвращает значение 000000User.

- - -
### <a name="padright"></a>PadRight
**Описание.**  
Hello PadRight функция дополняет справа tooa строку, в указанный длины, используя заданный заполняющий символ.

**Синтаксис**  
`str PadRight(str string, num length, str padCharacter)`

* строки: hello toopad строки.
* Длина: integer, представляющее hello требуемого длину строки.
* символ padCharacter: строка, состоящая из одного символа toouse как знак-заполнитель hello

**Примечания:**

* Если hello длина строки меньше length, символ padCharacter — многократно присоединенных toohello конец (справа) строки до его длина равна toolength.
* Значение padCharacter может быть символом пробела, но оно не может иметь значение Null.
* Если длина hello строки больше, чем длина равна tooor, строка возвращается без изменений.
* Если строка имеет длину больше или равно toolength, возвращается toostring одинаковые строки.
* Если hello длина строки меньше length, новая строка hello требуемого возвращается длина, содержащий строку, дополненную символом padCharacter.
* Если строка имеет значение null, функция hello возвращает пустую строку.

**Пример**  
`PadRight("User", 10, "0")`  
Возвращает значение User000000.

- - -
### <a name="pcase"></a>PCase
**Описание.**  
Hello функция PCase преобразует первый символ каждого слова с разделителями-пробелами, в случае tooupper строку hello, а все остальные символы преобразуются toolower регистр.

**Синтаксис**  
`String PCase(string)`

**Примечания:**

* Эта функция не обеспечивает в настоящее время tooconvert с учетом регистра слово, которое является полностью верхнем регистре, например акронима.

**Пример**  
`PCase("TEsT")`  
Возвращает значение Test.

`PCase(LCase("TEST"))`  
Возвращает значение Test.

- - -
### <a name="randomnum"></a>RandomNum
**Описание.**  
Hello функция RandomNum возвращает случайное число из указанного интервала.

**Синтаксис**  
`num RandomNum(num start, num end)`

* Начать: номер идентификации hello нижний предел toogenerate случайное значение hello
* конец: номер идентификации hello верхний предел toogenerate случайное значение hello

**Пример**  
`Random(100,999)`  
Может вернуть значение 734.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Описание.**  
Hello функция RemoveDuplicates принимает многозначную строку и убедитесь, что каждое значение является уникальным.

**Синтаксис**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Пример**  
`RemoveDuplicates([proxyAddresses])`  
Возвращает очищенный атрибут proxyAddress, в котором удалены все повторяющиеся значения.

- - -
### <a name="replace"></a>Замените
**Описание.**  
Hello функция Replace заменяет все вхождения строки tooanother строки.

**Синтаксис**  
`str Replace(str string, str OldValue, str NewValue)`

* Строка: tooreplace строка значений.
* OldValue: hello toosearch строку для и tooreplace.
* Новое значение: hello tooreplace строка для.

**Примечания:**  
функции Hello распознает следующие специальные моникеры hello.

* \n — новая строка;
* \r — возврат каретки;
* \t – символ табуляции.

**Пример**  
`Replace([address],"\r\n",", ")`  
Заменяет CRLF запятую и пробел и может вызвать слишком «Один Microsoft способом, Редмонд, штат Вашингтон, США»

- - -
### <a name="replacechars"></a>ReplaceChars
**Описание.**  
Hello функция ReplaceChars заменяет все вхождения символов в строке ReplacePattern hello.

**Синтаксис**  
`str ReplaceChars(str string, str ReplacePattern)`

* Строка: tooreplace строка символов.
* ReplacePattern: строка, содержащая словарь с tooreplace символов.

Hello формат: {source1}: {target1}, {source2}: {target2}, {sourceN}: {targetN} где hello символ toofind и целевой hello строка tooreplace с исходной.

**Примечания:**

* функция Hello принимает каждое вхождение каждого исходного и заменяет их символом hello целевых объектов.
* Hello источник должен иметь ровно один символ (Юникод).
* Hello источником не может быть пустым или содержать больше одного символа (Ошибка синтаксического анализа).
* Hello целевая служба может иметь несколько символов, например ö, β: ss.
* Hello цель может быть пустым, указывающее на то, что символ hello должны быть удалены.
* Источник Hello с учетом регистра и должны точно совпадать.
* Привет, (запятая) и: (двоеточие) зарезервированы и не может быть заменен с использованием этой функции.
* Пробелы и другие пробельные символы в hello строки ReplacePattern игнорируются.

**Пример**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Возвращает значение Raksmorgas.

`ReplaceChars("O’Neil",%ReplaceString%)`  
Возвращает «oneil "; hello такт имеет определенный toobe удалены.

- - -
### <a name="right"></a>Right
**Описание.**  
Hello функция Right возвращает указанное количество символов из hello вправо (конец) строки.

**Синтаксис**  
`str Right(str string, num NumChars)`

* строки: hello tooreturn символов строки из
* NumChars: число, задающее количество hello tooreturn символов из hello конец (справа) строки

**Примечания:**  
Возвращает NumChars символов начиная с последней позиции hello строки.

Строка, содержащая последние numChars символов hello в строке:

* если numChars = 0, возвращается пустая строка;
* если numChars < 0, возвращается введенная строка;
* если строка имеет значение Null, возвращается пустая строка.

Если строка содержит меньше символов, чем число NumChars hello, возвращается toostring одинаковые строки.

**Пример**  
`Right("John Doe", 3)`  
Возвращает значение Doe.

- - -
### <a name="rtrim"></a>RTrim
**Описание.**  
Hello функция RTrim удаляет конечные пробелы из строки.

**Синтаксис**  
`str RTrim(str value)`

**Пример**  
`RTrim(" Test ")`  
Возвращает значение Test.

- - -
### <a name="select"></a>Выберите пункт
**Описание.**  
Обработка всех значений атрибута с несколькими значениями (или выходного значения выражения) в соответствии с указанной функцией.

**Синтаксис**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* элемент: представляет элемент в многозначном атрибуте hello
* атрибут: hello многозначный атрибут
* expression: выражение, возвращающее коллекцию значений
* условие: любая функция, которая может обрабатывать элемента в атрибуте hello

**Примеры**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Возврат всех значений hello в многозначном атрибуте телефон hello, после удаления дефисы (-).

- - -
### <a name="split"></a>разделение;
**Описание.**  
Hello функция Split принимает строку с разделителями и делает его многозначную строку.

**Синтаксис**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* значение: hello строку с tooseparate символ разделителя.
* разделитель: один символ toobe используется как разделитель hello.
* limit: максимальное количество значений, которые могут быть возвращены.

**Пример**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Возвращает многозначную строку с двумя элементами, полезные для атрибута proxyAddress hello.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Описание.**  
Hello функция StringFromGuid принимает двоичный идентификатор GUID и преобразует его в строку tooa

**Синтаксис**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Описание.**  
Hello функция StringFromSid преобразует массив байтов, содержащий строку tooa идентификатора безопасности.

**Синтаксис**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Описание.**  
функция Switch Hello — tooreturn используется одно значение в соответствии с результатом проверки условий.

**Синтаксис**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr: выражение типа Variant, которое должно tooevaluate.
* значение: toobe значение возвращаемое, если hello соответствующее выражение имеет значение True.

**Примечания:**  
Здравствуйте, аргумент функции Switch состоит из пар выражений и значений. Hello выражения вычисляются из левой tooright и возвращается значение hello, связанное с hello первого выражения tooevaluate tooTrue. Если hello составлены неправильно, возникает ошибка времени выполнения.

Например, если expr1 имеет значение True, функция Switch возвращает value1. Если expr-1 имеет значение False, а expr-2 — True функция Switch возвращает значение value-2 и т. д.

Функция Switch возвращает Nothing при таких условиях:

* Ни одно из выражений hello имеют значение True.
* Hello первое значение True, выражение имеет соответствующее значение, равное Null.

Функция Switch вычисляет все выражения, хотя возвращает только одно из них. Поэтому необходимо следить за нежелательными побочными эффектами. Например если вычисление hello любого выражения происходит деление на ноль, возвращается ошибка.

Значение может быть также hello ошибки функции, которая возвращает настраиваемую строку.

**Пример**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Возвращает язык hello в некоторых основных городов, в противном случае возвращает ошибку.

- - -
### <a name="trim"></a>Trim
**Описание.**  
функция Trim Hello удаляет начальные и конечные пробелы из строки.

**Синтаксис**  
`str Trim(str value)`  

**Пример**  
`Trim(" Test ")`  
Возвращает значение Test.

`Trim([proxyAddresses])`  
Удаляет начальные и конечные пробелы для каждого значения атрибута proxyAddress hello.

- - -
### <a name="ucase"></a>UCase
**Описание.**  
Hello функция UCase преобразует все символы в случае tooupper строки.

**Синтаксис**  
`str UCase(str string)`

**Пример**  
`UCase("TeSt")`  
Возвращает значение Test.

- - -
### <a name="where"></a>Where

**Описание.**  
Возвращает подмножество значений атрибута с несколькими значениями (или выходного значения выражения) в соответствии с указанным условием.

**Синтаксис**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* элемент: представляет элемент в многозначном атрибуте hello
* атрибут: hello многозначный атрибут
* условие: любое выражение, которое может быть вычислено tootrue или false
* expression: выражение, возвращающее коллекцию значений

**Пример**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Возвращаемые значения сертификата hello в многозначном атрибуте userCertificate hello, которой не истек срок действия.

- - -
### <a name="with"></a>With
**Описание.**  
Hello с функцией предоставляет toosimplify способом сложное выражение с помощью переменной toorepresent часть выражения, которая отображается один или более раз в hello сложного выражения.

**Синтаксис:**
`With(var variable, exp subExpression, exp complexExpression)`  
* переменная: представляет hello части выражения.
* subExpression: часть выражения, представленная переменной.
* complexExpression: сложное выражение.

**Пример**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Функционально эквивалентно следующему:  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
В атрибуте userCertificate hello, которая возвращает только значения с неистекшим сроком действия сертификата.


- - -
### <a name="word"></a>Word
**Описание.**  
Hello функция Word возвращает слово, содержащееся в строки, с учетом параметров, описывающих toouse разделители hello и номеров tooreturn слово hello.

**Синтаксис**  
`str Word(str string, num WordNumber, str delimiters)`

* строки: hello слова из строки tooreturn.
* WordNumber: число, определяющее количество слов, которые должны быть возвращены.
* разделители: строка, представляющая delimiter(s) hello, следует использовать tooidentify слова

**Примечания:**  
Каждая строка символов строки, разделенные одним из символов hello в разделители hello идентифицируются как слов:

* если number < 1, возвращается пустая строка;
* если string имеет значение Null, возвращается пустая строка.

Если строка содержит меньше слов, чем number, или строка не содержит слов, идентифицируемых с помощью разделителей, возвращается пустая строка.

**Пример**  
`Word("hello quick brown fox",3," ")`  
Возвращает значение "brown".

`Word("This,string!has&many separators",3,",!&#")`  
Вернет значение "has".

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Знакомство с выражениями декларативной подготовки.](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect Sync: настройка параметров синхронизации](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
