---
title: "политики проверки подлинности API Management aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello политики проверки подлинности, доступные для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>Политики аутентификации в службе управления API
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AuthenticationPolicies"></a> Политики аутентификации  
  
-   [Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.  
  
-   [Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.  
  
##  <a name="Basic"></a> Обычная проверка подлинности  
 Используйте hello `authentication-basic` tooauthenticate политики с помощью серверной службы с использованием обычной проверки подлинности. Эта политика фактически устанавливает toohello заголовок авторизации HTTP hello значение соответствующего toohello учетные данные, указанные в политике hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|authentication-basic|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|Имя пользователя|Указывает имя пользователя hello hello основных учетных данных.|Да|Недоступно|  
|пароль|Указывает пароль hello hello основных учетных данных.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** API.  
  
##  <a name="ClientCertificate"></a> Аутентификация с помощью сертификата клиента  
 Используйте hello `authentication-certificate` tooauthenticate политики с помощью серверной службы с использованием клиентского сертификата. Hello сертификат должен toobe [установлен в API Management](http://go.microsoft.com/fwlink/?LinkID=511599) первый и определяется его отпечатком.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|authentication-certificate|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|thumbprint|отпечаток сертификата клиента hello Hello.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** API.  
  

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  