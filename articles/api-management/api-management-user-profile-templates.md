---
title: "aaa \"Шаблоны профиля в службе управления API Azure | Документы Microsoft»"
description: "Узнайте, как содержимое hello toocustomize hello профиль пользователя страниц hello портал разработчиков в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a>Шаблоны профилей пользователей в службе управления API Azure
Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого. С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.  
  
 шаблоны Hello в этом разделе разрешить доступ к содержимому hello toocustomize hello страниц профиля пользователя на портале разработчиков hello.  
  
-   [Профиль](#Profile)  
  
-   [Подписки](#Subscriptions).  
  
-   [Приложения](#Applications).  
  
-   [Обновление сведений об учетной записи](#UpdateAccountInfo).  
  
> [!NOTE]
>  Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения. Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов. Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="Profile"></a> Профиль  
 Hello **профиль** шаблон позволяет раздела профиля пользователя toocustomize hello hello страницы профиля пользователя на портале разработчиков hello.  
  
 ![Страница профиля пользователя](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Страница профиля пользователя APIM")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a>Управление  
 В этом шаблоне нельзя использовать [элементы управления страницы](api-management-page-controls.md).  
  
### <a name="data-model"></a>Модель данных  
  
> [!NOTE]
>  Hello [профиль](#Profile), [приложений](#Applications), и [подписки](#Subscriptions) шаблоны совместно использовать hello и те же данные модели и получения hello и тех же данных шаблона.  
  
|Свойство|Тип|Описание|  
|--------------|----------|-----------------|  
|firstName|string|Имя текущего пользователя hello.|  
|lastName|string|Фамилия hello текущего пользователя.|  
|companyName|string|имя компании Hello hello текущего пользователя.|  
|addresserEmail|string|Адрес электронной почты текущего пользователя hello.|  
|developersUsageStatisticsLinkk|string|Аналитика tooview относительный URL-адрес для текущего пользователя hello.|  
|subscriptions|Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).|Hello подписки для текущего пользователя hello.|  
|веб-масштабированием;|Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).|приложения Hello hello текущего пользователя.|  
|changePasswordUrl|string|Hello относительный URL-адрес toochange hello текущий пароль пользователя.|  
|changeNameOrEmailUrl|string|Здравствуйте, относительное имя hello toochange URL-адрес и адрес электронной почты для текущего пользователя hello.|  
|canChangePassword|Логическое|Является ли текущий пользователь hello может изменить свой пароль.|  
|isSystemUser|Логическое|Является ли hello текущий пользователь является членом одной из встроенных hello [группы](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Subscriptions"></a>Подписки  
 Hello **подписки** шаблон позволяет toocustomize hello подписок раздела hello страницу профиля пользователя на портале разработчиков hello.  
  
 ![Страница подписки пользователя](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Страница подписки пользователя APIM ")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a>Управление  
 Этот шаблон может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).  
  
-   [subscription-cancel](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a>Модель данных  
  
> [!NOTE]
>  Hello [профиль](#Profile), [приложений](#Applications), и [подписки](#Subscriptions) шаблоны совместно использовать hello и те же данные модели и получения hello и тех же данных шаблона.  
  
|Свойство|Тип|Описание|  
|--------------|----------|-----------------|  
|firstName|string|Имя текущего пользователя hello.|  
|lastName|string|Фамилия hello текущего пользователя.|  
|companyName|string|имя компании Hello hello текущего пользователя.|  
|addresserEmail|string|Адрес электронной почты текущего пользователя hello.|  
|developersUsageStatisticsLinkk|string|Аналитика tooview относительный URL-адрес для текущего пользователя hello.|  
|subscriptions|Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).|Hello подписки для текущего пользователя hello.|  
|веб-масштабированием;|Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).|приложения Hello hello текущего пользователя.|  
|changePasswordUrl|string|Hello относительный URL-адрес toochange hello текущий пароль пользователя.|  
|changeNameOrEmailUrl|string|Здравствуйте, относительное имя hello toochange URL-адрес и адрес электронной почты для текущего пользователя hello.|  
|canChangePassword|Логическое|Является ли текущий пользователь hello может изменить свой пароль.|  
|isSystemUser|Логическое|Является ли hello текущий пользователь является членом одной из встроенных hello [группы](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="Applications"></a> Приложения  
 Hello **приложений** шаблон позволяет toocustomize hello подписок раздела hello страницу профиля пользователя на портале разработчиков hello.  
  
 ![Страница приложений учетной записи пользователя](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Страница приложений учетной записи пользователя APIM")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a>Управление  
 Этот шаблон может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).  
  
-   [app-actions](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a>Модель данных  
  
> [!NOTE]
>  Hello [профиль](#Profile), [приложений](#Applications), и [подписки](#Subscriptions) шаблоны совместно использовать hello и те же данные модели и получения hello и тех же данных шаблона.  
  
|Свойство|Тип|Описание|  
|--------------|----------|-----------------|  
|firstName|string|Имя текущего пользователя hello.|  
|lastName|string|Фамилия hello текущего пользователя.|  
|companyName|string|имя компании Hello hello текущего пользователя.|  
|addresserEmail|string|Адрес электронной почты текущего пользователя hello.|  
|developersUsageStatisticsLinkk|string|Аналитика tooview относительный URL-адрес для текущего пользователя hello.|  
|subscriptions|Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).|Hello подписки для текущего пользователя hello.|  
|веб-масштабированием;|Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).|приложения Hello hello текущего пользователя.|  
|changePasswordUrl|string|Hello относительный URL-адрес toochange hello текущий пароль пользователя.|  
|changeNameOrEmailUrl|string|Здравствуйте, относительное имя hello toochange URL-адрес и адрес электронной почты для текущего пользователя hello.|  
|canChangePassword|Логическое|Является ли текущий пользователь hello может изменить свой пароль.|  
|isSystemUser|Логическое|Является ли hello текущий пользователь является членом одной из встроенных hello [группы](api-management-key-concepts.md#groups).|  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <a name="UpdateAccountInfo"></a> Обновление сведений об учетной записи  
 Hello **сведения учетной записи Uodate** шаблон позволяет toocustomize hello **Обновите информацию учетной записи** страницы на портале разработчиков hello.  
  
 ![Шаблоны информации об учетной записи на портале разработчика](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Шаблоны информации об учетной записи на портале разработчика APIM")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a>Управление  
 В этом шаблоне нельзя использовать [элементы управления страницы](api-management-page-controls.md).  
  
### <a name="data-model"></a>Модель данных  
 Сущность [сведений об учетной записи пользователя](api-management-template-data-model-reference.md#UserAccountInfo).  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).
