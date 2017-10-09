---
title: "атрибуты aaaAzure AD Connect sync службы теневого | Документы Microsoft"
description: "Описание работы теневых атрибутов в службе синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Теневые атрибуты службы синхронизации Azure AD Connect
Большинство атрибутов представляются Здравствуйте таким же, как в Azure AD как в вашей локальной Active Directory. Некоторые атрибуты имеют некоторые специальной обработки, но значение атрибута hello в Azure AD может отличаться от синхронизации Azure AD Connect.

## <a name="introducing-shadow-attributes"></a>Общие сведения о теневых атрибутах
Для некоторых атрибутов в Azure AD используются два представления. Значение в локальной среде hello и вычисляемого значения сохраняются. Эти дополнительные атрибуты называются теневыми. Hello два наиболее распространенных атрибуты, где вы видите это поведение **userPrincipalName** и **proxyAddress**. Изменение Hello в значениях атрибутов происходит, когда отсутствуют значения этих атрибутов, представляющих не проверенные домены. Однако подсистема синхронизации hello в соединение hello значение считывается в атрибуте тени hello, с ее точки зрения, атрибут hello подтверждено с помощью Azure AD.

Не могут видеть атрибутов тени hello, с помощью hello портал Azure или с помощью PowerShell. Но основные сведения о концепции hello помогает вы tootroubleshoot определенных сценариях где hello атрибут имеет различные значения в локальной среде и в облаке hello.

toobetter понять поведение hello, рассмотрим следующий пример от компании Fabrikam:  
![Домены](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Они используют несколько суффиксов имени участника-пользователя в своей локальной службе Active Directory, но проверен только один из них.

### <a name="userprincipalname"></a>userPrincipalName
Пользователь имеет следующие значения атрибутов в домене не проверен hello:

| Атрибут | Значение |
| --- | --- |
| userPrincipalName для локальной среды | lee.sperry@fabrikam.com |
| shadowUserPrincipalName для Azure AD | lee.sperry@fabrikam.com |
| userPrincipalName для Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

атрибут userPrincipalName Hello значение hello, отображаемые при использовании PowerShell.

Так как значение атрибута реальные локальной hello хранится в Azure AD, когда проверки домена fabrikam.com hello, Azure AD обновляет атрибут userPrincipalName hello hello значение из hello shadowUserPrincipalName. У вас toosynchronize все изменения из Azure AD Connect для этих toobe значения обновлены.

### <a name="proxyaddresses"></a>proxyAddresses
Здравствуйте, один процесс для только в том числе проверенных доменов, также происходит proxyAddresses, только имеет дополнительную логику. Привет, ищите проверенных доменов происходит только для почтовых ящиков пользователей. Поддержкой электронной почты пользователя или контакт представляют пользователя в другой организации Exchange и можно добавить все значения в объектах toothese proxyAddresses.

Для пользователя почтового ящика, размещенного в локальной среде или Exchange Online, отображаются только значения для проверенных доменов. Это выглядит следующим образом.

| Атрибут | Значение |
| --- | --- |
| proxyAddresses для локальной среды | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| proxyAddresses для Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

В этом случае **smtp:abbie.spencer@fabrikam.com** был удален, так как этот домен не проверен. Но служба Exchange также добавила **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam не использовал Lync или Skype локально, но Azure AD и Exchange Online готовы к этому.

Эта логика для proxyAddresses является ссылка tooas **ProxyCalc**. ProxyCalc вызывается при каждом изменении пользователя, когда:

- пользователь Hello назначила план обслуживания, включающую Exchange Online, даже если пользователь hello не был лицензию на Exchange. Например если hello пользователю назначается hello Office E3 SKU, но только был назначен SharePoint Online. Это верно, даже если ваш почтовый ящик является локальным.
- Hello msExchRecipientTypeDetails атрибут имеет значение.
- Внесенные изменения tooproxyAddresses или userPrincipalName.

ProxyCalc может занять некоторое время tooprocess изменения для пользователя и не синхронном процесс экспорта hello Azure AD Connect.

> [!NOTE]
> Hello логику ProxyCalc имеет некоторые дополнительные возможности для более сложных сценариев, которые не описаны в этом разделе. В этом разделе предоставляется для вас toounderstand hello поведение и описываются все внутренней логики.

### <a name="quarantined-attribute-values"></a>Значения атрибутов, помещенных в карантин
Теневые атрибуты также используются при наличии повторяющихся значений атрибутов. Дополнительные сведения см. в разделе [Синхронизация удостоверений и устойчивость повторяющихся атрибутов](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Дополнительные материалы
* [Службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
