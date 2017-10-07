---
title: "Azure AD Connect: выражения декларативной подготовки | Документация Майкрософт"
description: "Описание выражения декларативной подготовки hello."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Служба синхронизации Azure AD Connect: общие сведения о выражениях декларативной подготовки
Служба синхронизации Azure AD Connect основана на принципах декларативной подготовки, впервые представленной в Forefront Identity Manager 2010. Позволяет tooimplement бизнес-логики интеграции удостоверений завершения без необходимости toowrite hello скомпилированный код.

Важной частью декларативной подготовки является язык выражений hello, используемый в потоке атрибутов. Hello язык, используемый — это подмножество Microsoft® Visual Basic® для приложений (VBA). Этот язык используется в Microsoft Office и знаком пользователи, имеющим опыт работы с VBScript. Hello декларативной подготовки язык выражений использует только функции и не является структурным языком. но не методы или инструкции. Вместо этого вложенные функции tooexpress программировании потока.

Дополнительные сведения см. в разделе [Добро пожаловать toohello Visual Basic для приложений Справочник по языку для Office 2013](https://msdn.microsoft.com/library/gg264383.aspx).

Hello атрибуты являются строго типизированными. Функция принимает только атрибуты правильного типа hello. Регистр символов также учитывается. Имена функций и атрибутов должны указываться с учетом регистра, иначе произойдет ошибка.

## <a name="language-definitions-and-identifiers"></a>Определения и идентификаторы языка
* У функции есть имя, за которым следует список аргументов в скобках: имя_функции(аргумент 1, аргумент N).
* Атрибуты заключаются в квадратные скобки: [имя_атрибута].
* Параметры задаются знаком процента: %имя_параметра%.
* Строковые константы заключаются в кавычки, например "Contoso" (обратите внимание, что необходимо использовать прямые (""), а не парные (“”) кавычки).
* Числовые значения выражаются без кавычек и ожидаемый toobe десятичное число. Шестнадцатеричные значения должны иметь префикс &H. Например, 98052, &HFF.
* Логические значения выражаются константами True и False.
* Встроенные константы и литералы выражаются только своим именем: NULL, CRLF, IgnoreThisFlow.

### <a name="functions"></a>Функции
Декларативной подготовки использует много значений атрибута tootransform вероятность функции tooenable hello. Эти функции могут быть вложенными, поэтому результат hello одной функции передается в функцию tooanother.

`Function1(Function2(Function3()))`

Полный список функций Hello можно найти в hello [функции ссылка](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>Параметры
Параметр задается соединителем или администратором с помощью PowerShell. Параметры обычно содержат значения, отличные от toosystem системы, например hello имя пользователя hello hello домена находится в папке. Эти параметры могут использоваться в потоках атрибутов.

Hello Соединитель Active Directory предоставленный hello следующие параметры для входящих правил синхронизации:

| Имя параметра | Комментарий |
| --- | --- |
| Domain.Netbios |Формат NetBIOS hello домена импортируемые в настоящее время, например FABRIKAMSALES |
| Domain.FQDN |Полное доменное имя формата hello домена импортируемые в настоящее время, например sales.fabrikam.com |
| Domain.LDAP |Формат LDAP hello домена импортируемые в настоящее время, например DC = sales, DC = fabrikam, DC = com |
| Forest.Netbios |NetBIOS формат hello леса имени импортируемого в настоящее время, например FABRIKAMCORP |
| Forest.FQDN |Полное доменное имя формата hello леса имени импортируемого в настоящее время, например fabrikam.com |
| Forest.LDAP |LDAP формата hello леса имени импортируемого в настоящее время, например DC = fabrikam, DC = com |

система Hello предоставляет hello следующий параметр, который используется tooget идентификатор hello hello соединителя выполняется в данный момент:  
`Connector.ID`

Ниже приведен пример, который заполняет hello домена атрибут метавселенной с hello NetBIOS-имя домена hello, где находится пользователь hello:  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Операторы
можно использовать следующие операторы Hello.

* **Сравнение**: <, <=, <>, =, >, >=
* **Математические**: +, -, \*, -
* **Строковые**: & (сцепление)
* **Логические**: && (и), || (или)
* **Порядок вычисления**: ( )

Операторы вычисленное левой tooright и hello имеют одинаковый приоритет вычисления. Здравствуйте, то есть \* (множитель) не вычисляется до - (вычитание). 2\*(5 + 3) не является Здравствуйте таким же, как 2\*5 + 3. Hello используются скобки () оценки hello toochange заказа при tooright порядок вычисления не.

## <a name="multi-valued-attributes"></a>Многозначные атрибуты
можно использовать функции Hello однозначных и многозначных атрибутов. Для многозначных атрибутов функции hello работает через каждые значение и применяет hello же функцию tooevery значение.

Например:  
`Trim([proxyAddresses])`Выполните усечение каждого значения атрибута proxyAddress hello.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Для каждого значения с @-sign, замените домен hello с @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Найдите адрес SIP hello и удалите его из значения hello.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о модели конфигурации hello в [декларативной подготовки основные сведения о](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* См. в разделе как декларативной подготовки является используемым out-of-box в [основные сведения о настройке по умолчанию hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Просмотреть, как toomake практическая изменяются с помощью декларативной подготовки в [как конфигурация по умолчанию toomake toohello изменение](active-directory-aadconnectsync-change-the-configuration.md).

**Обзорные статьи**

* [Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)

**Справочные материалы**

* [Синхронизация Azure AD Connect: справочник по функциям](active-directory-aadconnectsync-functions-reference.md)

