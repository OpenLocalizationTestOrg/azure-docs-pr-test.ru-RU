---
title: "элементов управления на странице управления API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello страницы элементов управления, доступных для использования в шаблонах портала разработчиков в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Элементы управления страницей в службе управления API Azure
Управления API Azure предоставляет следующие элементы управления для использования в шаблонах портала разработчиков hello hello.  
  
 toouse элемент управления поместить его в расположение требуемого hello в шаблоне портала разработчиков hello. Некоторые элементы управления, такие как hello [действия приложения](#app-actions) управления, имеют параметры, как показано в следующий пример hello.  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 Hello значения для параметров hello передаются в составе hello модели данных для шаблона hello. В большинстве случаев можно просто вставить в hello заданного пример для каждого элемента управления для него toowork правильно. Дополнительные сведения о значениях параметра hello видно hello раздел модели данных для каждого шаблона, в котором можно будет использовать элемент управления.  
  
 Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
## <a name="developer-portal-template-page-controls"></a>Элементы управления страницей в шаблонах портала разработчика  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [providers](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a> app-actions  
 Hello `app-actions` управления предоставляет пользовательский интерфейс для взаимодействия с приложениями на странице профиля пользователя hello на портале разработчиков hello.  
  
 ![элемент управления действиями](./media/api-management-page-controls/APIM-app-actions-control.png "элемент управления действиями для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>Параметры  
  
|Параметр|Описание|  
|---------------|-----------------|  
|appId|Идентификатор приложения hello Hello.|  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `app-actions` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Приложения](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a> basic-signin  
 Hello `basic-signin` управления предоставляет элемент управления для сбора данных вход пользователя сведения в hello войти в портале разработчика hello.  
  
 ![базовый элемент управления входом](./media/api-management-page-controls/APIM-basic-signin-control.png "базовый элемент управления входом для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `basic-signin` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Вход](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a> paging-control  
 Hello `paging-control` предоставляет функциональные возможности для разбиения на страницы разработчика страницы портала, отображать список элементов.  
  
 ![элемент управления разбиением по страницам ](./media/api-management-page-controls/APIM-paging-control.png "элемент управления разбиением по страницам для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `paging-control` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Список API](api-management-api-templates.md#APIList)  
  
-   [Список проблем](api-management-issue-templates.md#IssueList)  
  
-   [Список продуктов](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a> providers  
 Hello `providers` управления предоставляет элемент управления для выбора поставщиков проверки подлинности в hello входа в портал разработчиков hello.  
  
 ![Элемент управления поставщиками](./media/api-management-page-controls/APIM-providers-control.png "Элемент управления поставщиками для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `providers` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Вход](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a> search-control  
 Hello `search-control` предоставляет функциональные возможности поиска разработчика страницы портала, отображать список элементов.  
  
 ![Элемент управления поиском](./media/api-management-page-controls/APIM-search-control.png "Элемент управления поиском для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `search-control` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Список API](api-management-api-templates.md#APIList)  
  
-   [Список продуктов](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a> sign-up  
 Hello `sign-up` управления предоставляет элемент управления для сбора данных профиля пользователя в страницу на портале разработчиков hello регистрации hello.  
  
 ![Элемент управления регистрацией](./media/api-management-page-controls/APIM-sign-up-control.png "Элемент управления регистрацией для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `sign-up` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Регистрация](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a> subscribe-button  
 Hello `subscribe-button` предоставляет элемент управления для подписки пользователя tooa продукта.  
  
 ![Элемент управления подпиской](./media/api-management-page-controls/APIM-subscribe-button-control.png "Элемент управления подпиской для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>Параметры  
 Отсутствует.  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `subscribe-button` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Продукт](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a> subscription-cancel  
 Hello `subscription-cancel` управления предоставляет элемент управления для отмены подписки tooa продукт в hello страницу профиля пользователя на портале разработчиков hello.  
  
 ![Элемент управления отменой подписки](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Элемент управления отменой подписки для APIM")  
  
### <a name="usage"></a>Использование  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>Параметры  
  
|Параметр|Описание|  
|---------------|-----------------|  
|subscriptionId|идентификатор подписки toocancel hello Hello.|  
|cancelUrl|Подписка Hello отменить URL-адрес.|  
  
### <a name="developer-portal-templates"></a>Шаблоны портала разработчика  
 Hello `subscription-cancel` управления может быть использована для hello следующие шаблоны портала разработчиков.  
  
-   [Продукт](api-management-product-templates.md#Product)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).
