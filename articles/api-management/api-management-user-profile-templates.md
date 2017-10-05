---
title: "Шаблоны профилей пользователей в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как настроить содержимое страниц профилей пользователей на портале разработчика в службе управления API Azure."
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
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="d5707-103">Шаблоны профилей пользователей в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="d5707-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="d5707-104">Служба управления API Azure позволяет настраивать содержимое страниц портала разработчика с помощью набора шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d5707-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="d5707-105">С помощью этих шаблонов вы можете гибко настраивать содержимое страниц, используя синтаксис [DotLiquid](http://dotliquidmarkup.org/), любой удобный текстовый редактор, например [DotLiquid для разработчиков](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), и предоставленный набор локализованных [строковых ресурсов](api-management-template-resources.md#strings), [ресурсов глифов](api-management-template-resources.md#glyphs), а также [элементов управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="d5707-106">С помощью шаблонов в этом разделе вы сможете настроить содержимое страниц профилей пользователей на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5707-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="d5707-107">Профиль</span><span class="sxs-lookup"><span data-stu-id="d5707-107">Profile</span></span>](#Profile)  
  
-   <span data-ttu-id="d5707-108">[Подписки](#Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="d5707-108">[Subscriptions](#Subscriptions)</span></span>  
  
-   <span data-ttu-id="d5707-109">[Приложения](#Applications).</span><span class="sxs-lookup"><span data-stu-id="d5707-109">[Applications](#Applications)</span></span>  
  
-   <span data-ttu-id="d5707-110">[Обновление сведений об учетной записи](#UpdateAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="d5707-110">[Update account info](#UpdateAccountInfo)</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5707-111">Примеры стандартных шаблонов включены в следующую документацию, но могут в любой момент измениться, так как ведется постоянная работа по их улучшению.</span><span class="sxs-lookup"><span data-stu-id="d5707-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="d5707-112">Актуальные шаблоны по умолчанию можно просмотреть на портале разработчика, перейдя к требуемому отдельному шаблону.</span><span class="sxs-lookup"><span data-stu-id="d5707-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="d5707-113">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="d5707-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="d5707-114"><a name="Profile"></a> Профиль</span><span class="sxs-lookup"><span data-stu-id="d5707-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="d5707-115">Шаблон **профиля** позволяет настроить раздел профиля пользователя на странице профиля пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5707-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d5707-116">![Страница профиля пользователя](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Страница профиля пользователя APIM")</span><span class="sxs-lookup"><span data-stu-id="d5707-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d5707-117">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5707-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d5707-118">Управление</span><span class="sxs-lookup"><span data-stu-id="d5707-118">Controls</span></span>  
 <span data-ttu-id="d5707-119">В этом шаблоне нельзя использовать [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d5707-120">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d5707-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5707-121">Шаблоны [профиля](#Profile), [приложений](#Applications) и [подписок](#Subscriptions) используют одинаковую модель данных и получают одни и те же данные шаблона.</span><span class="sxs-lookup"><span data-stu-id="d5707-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d5707-122">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5707-122">Property</span></span>|<span data-ttu-id="d5707-123">Тип</span><span class="sxs-lookup"><span data-stu-id="d5707-123">Type</span></span>|<span data-ttu-id="d5707-124">Описание</span><span class="sxs-lookup"><span data-stu-id="d5707-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d5707-125">firstName</span><span class="sxs-lookup"><span data-stu-id="d5707-125">firstName</span></span>|<span data-ttu-id="d5707-126">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-126">string</span></span>|<span data-ttu-id="d5707-127">Имя текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-127">First name of the current user.</span></span>|  
|<span data-ttu-id="d5707-128">lastName</span><span class="sxs-lookup"><span data-stu-id="d5707-128">lastName</span></span>|<span data-ttu-id="d5707-129">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-129">string</span></span>|<span data-ttu-id="d5707-130">Фамилия текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="d5707-131">companyName</span><span class="sxs-lookup"><span data-stu-id="d5707-131">companyName</span></span>|<span data-ttu-id="d5707-132">string</span><span class="sxs-lookup"><span data-stu-id="d5707-132">string</span></span>|<span data-ttu-id="d5707-133">Название компании текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="d5707-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d5707-134">addresserEmail</span></span>|<span data-ttu-id="d5707-135">string</span><span class="sxs-lookup"><span data-stu-id="d5707-135">string</span></span>|<span data-ttu-id="d5707-136">Адрес электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="d5707-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d5707-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d5707-138">string</span><span class="sxs-lookup"><span data-stu-id="d5707-138">string</span></span>|<span data-ttu-id="d5707-139">Относительный URL-адрес для просмотра аналитики по текущему пользователю.</span><span class="sxs-lookup"><span data-stu-id="d5707-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d5707-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="d5707-140">subscriptions</span></span>|<span data-ttu-id="d5707-141">Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).</span><span class="sxs-lookup"><span data-stu-id="d5707-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d5707-142">Подписки текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d5707-143">веб-масштабированием;</span><span class="sxs-lookup"><span data-stu-id="d5707-143">applications</span></span>|<span data-ttu-id="d5707-144">Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).</span><span class="sxs-lookup"><span data-stu-id="d5707-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d5707-145">Приложения текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="d5707-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-146">changePasswordUrl</span></span>|<span data-ttu-id="d5707-147">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-147">string</span></span>|<span data-ttu-id="d5707-148">Относительный URL-адрес для изменения пароля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d5707-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d5707-150">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-150">string</span></span>|<span data-ttu-id="d5707-151">Относительный URL-адрес для изменения имени и адреса электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d5707-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d5707-152">canChangePassword</span></span>|<span data-ttu-id="d5707-153">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-153">boolean</span></span>|<span data-ttu-id="d5707-154">Определяет, может ли текущий пользователь изменять свой пароль.</span><span class="sxs-lookup"><span data-stu-id="d5707-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d5707-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d5707-155">isSystemUser</span></span>|<span data-ttu-id="d5707-156">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-156">boolean</span></span>|<span data-ttu-id="d5707-157">Определяет, входит ли текущий пользователь в одну из встроенных [групп](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="d5707-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d5707-158">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d5707-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="d5707-159"><a name="Subscriptions"></a>Подписки</span><span class="sxs-lookup"><span data-stu-id="d5707-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="d5707-160">Шаблон **подписок** позволяет настроить раздел подписок на странице профиля пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5707-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d5707-161">![Страница подписки пользователя](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Страница подписки пользователя APIM ")</span><span class="sxs-lookup"><span data-stu-id="d5707-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d5707-162">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5707-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d5707-163">Управление</span><span class="sxs-lookup"><span data-stu-id="d5707-163">Controls</span></span>  
 <span data-ttu-id="d5707-164">В этом шаблоне могут использоваться следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d5707-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="d5707-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="d5707-166">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d5707-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5707-167">Шаблоны [профиля](#Profile), [приложений](#Applications) и [подписок](#Subscriptions) используют одинаковую модель данных и получают одни и те же данные шаблона.</span><span class="sxs-lookup"><span data-stu-id="d5707-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d5707-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5707-168">Property</span></span>|<span data-ttu-id="d5707-169">Тип</span><span class="sxs-lookup"><span data-stu-id="d5707-169">Type</span></span>|<span data-ttu-id="d5707-170">Описание</span><span class="sxs-lookup"><span data-stu-id="d5707-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d5707-171">firstName</span><span class="sxs-lookup"><span data-stu-id="d5707-171">firstName</span></span>|<span data-ttu-id="d5707-172">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-172">string</span></span>|<span data-ttu-id="d5707-173">Имя текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-173">First name of the current user.</span></span>|  
|<span data-ttu-id="d5707-174">lastName</span><span class="sxs-lookup"><span data-stu-id="d5707-174">lastName</span></span>|<span data-ttu-id="d5707-175">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-175">string</span></span>|<span data-ttu-id="d5707-176">Фамилия текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="d5707-177">companyName</span><span class="sxs-lookup"><span data-stu-id="d5707-177">companyName</span></span>|<span data-ttu-id="d5707-178">string</span><span class="sxs-lookup"><span data-stu-id="d5707-178">string</span></span>|<span data-ttu-id="d5707-179">Название компании текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="d5707-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d5707-180">addresserEmail</span></span>|<span data-ttu-id="d5707-181">string</span><span class="sxs-lookup"><span data-stu-id="d5707-181">string</span></span>|<span data-ttu-id="d5707-182">Адрес электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="d5707-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d5707-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d5707-184">string</span><span class="sxs-lookup"><span data-stu-id="d5707-184">string</span></span>|<span data-ttu-id="d5707-185">Относительный URL-адрес для просмотра аналитики по текущему пользователю.</span><span class="sxs-lookup"><span data-stu-id="d5707-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d5707-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="d5707-186">subscriptions</span></span>|<span data-ttu-id="d5707-187">Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).</span><span class="sxs-lookup"><span data-stu-id="d5707-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d5707-188">Подписки текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d5707-189">веб-масштабированием;</span><span class="sxs-lookup"><span data-stu-id="d5707-189">applications</span></span>|<span data-ttu-id="d5707-190">Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).</span><span class="sxs-lookup"><span data-stu-id="d5707-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d5707-191">Приложения текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="d5707-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-192">changePasswordUrl</span></span>|<span data-ttu-id="d5707-193">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-193">string</span></span>|<span data-ttu-id="d5707-194">Относительный URL-адрес для изменения пароля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d5707-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d5707-196">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-196">string</span></span>|<span data-ttu-id="d5707-197">Относительный URL-адрес для изменения имени и адреса электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d5707-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d5707-198">canChangePassword</span></span>|<span data-ttu-id="d5707-199">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-199">boolean</span></span>|<span data-ttu-id="d5707-200">Определяет, может ли текущий пользователь изменять свой пароль.</span><span class="sxs-lookup"><span data-stu-id="d5707-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d5707-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d5707-201">isSystemUser</span></span>|<span data-ttu-id="d5707-202">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-202">boolean</span></span>|<span data-ttu-id="d5707-203">Определяет, входит ли текущий пользователь в одну из встроенных [групп](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="d5707-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d5707-204">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d5707-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="d5707-205"><a name="Applications"></a> Приложения</span><span class="sxs-lookup"><span data-stu-id="d5707-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="d5707-206">Шаблон **приложений** позволяет настроить раздел приложений на странице профиля пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5707-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d5707-207">![Страница приложений учетной записи пользователя](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "Страница приложений учетной записи пользователя APIM")</span><span class="sxs-lookup"><span data-stu-id="d5707-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d5707-208">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5707-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d5707-209">Управление</span><span class="sxs-lookup"><span data-stu-id="d5707-209">Controls</span></span>  
 <span data-ttu-id="d5707-210">В этом шаблоне могут использоваться следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d5707-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="d5707-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="d5707-212">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d5707-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5707-213">Шаблоны [профиля](#Profile), [приложений](#Applications) и [подписок](#Subscriptions) используют одинаковую модель данных и получают одни и те же данные шаблона.</span><span class="sxs-lookup"><span data-stu-id="d5707-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d5707-214">Свойство</span><span class="sxs-lookup"><span data-stu-id="d5707-214">Property</span></span>|<span data-ttu-id="d5707-215">Тип</span><span class="sxs-lookup"><span data-stu-id="d5707-215">Type</span></span>|<span data-ttu-id="d5707-216">Описание</span><span class="sxs-lookup"><span data-stu-id="d5707-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d5707-217">firstName</span><span class="sxs-lookup"><span data-stu-id="d5707-217">firstName</span></span>|<span data-ttu-id="d5707-218">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-218">string</span></span>|<span data-ttu-id="d5707-219">Имя текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-219">First name of the current user.</span></span>|  
|<span data-ttu-id="d5707-220">lastName</span><span class="sxs-lookup"><span data-stu-id="d5707-220">lastName</span></span>|<span data-ttu-id="d5707-221">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-221">string</span></span>|<span data-ttu-id="d5707-222">Фамилия текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="d5707-223">companyName</span><span class="sxs-lookup"><span data-stu-id="d5707-223">companyName</span></span>|<span data-ttu-id="d5707-224">string</span><span class="sxs-lookup"><span data-stu-id="d5707-224">string</span></span>|<span data-ttu-id="d5707-225">Название компании текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="d5707-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d5707-226">addresserEmail</span></span>|<span data-ttu-id="d5707-227">string</span><span class="sxs-lookup"><span data-stu-id="d5707-227">string</span></span>|<span data-ttu-id="d5707-228">Адрес электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="d5707-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d5707-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d5707-230">string</span><span class="sxs-lookup"><span data-stu-id="d5707-230">string</span></span>|<span data-ttu-id="d5707-231">Относительный URL-адрес для просмотра аналитики по текущему пользователю.</span><span class="sxs-lookup"><span data-stu-id="d5707-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d5707-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="d5707-232">subscriptions</span></span>|<span data-ttu-id="d5707-233">Коллекция сущностей [Subscription](api-management-template-data-model-reference.md#Subscription) (Подписка).</span><span class="sxs-lookup"><span data-stu-id="d5707-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d5707-234">Подписки текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d5707-235">веб-масштабированием;</span><span class="sxs-lookup"><span data-stu-id="d5707-235">applications</span></span>|<span data-ttu-id="d5707-236">Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).</span><span class="sxs-lookup"><span data-stu-id="d5707-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d5707-237">Приложения текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="d5707-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-238">changePasswordUrl</span></span>|<span data-ttu-id="d5707-239">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-239">string</span></span>|<span data-ttu-id="d5707-240">Относительный URL-адрес для изменения пароля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d5707-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d5707-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d5707-242">строка</span><span class="sxs-lookup"><span data-stu-id="d5707-242">string</span></span>|<span data-ttu-id="d5707-243">Относительный URL-адрес для изменения имени и адреса электронной почты текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5707-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d5707-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d5707-244">canChangePassword</span></span>|<span data-ttu-id="d5707-245">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-245">boolean</span></span>|<span data-ttu-id="d5707-246">Определяет, может ли текущий пользователь изменять свой пароль.</span><span class="sxs-lookup"><span data-stu-id="d5707-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d5707-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d5707-247">isSystemUser</span></span>|<span data-ttu-id="d5707-248">Логическое</span><span class="sxs-lookup"><span data-stu-id="d5707-248">boolean</span></span>|<span data-ttu-id="d5707-249">Определяет, входит ли текущий пользователь в одну из встроенных [групп](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="d5707-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d5707-250">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d5707-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="d5707-251"><a name="UpdateAccountInfo"></a> Обновление сведений об учетной записи</span><span class="sxs-lookup"><span data-stu-id="d5707-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="d5707-252">Шаблон **обновления сведений об учетной записи** позволяет настраивать страницу **обновления сведений об учетной записи** на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5707-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="d5707-253">![Шаблоны информации об учетной записи на портале разработчика](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Шаблоны информации об учетной записи на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="d5707-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d5707-254">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5707-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="d5707-255">Управление</span><span class="sxs-lookup"><span data-stu-id="d5707-255">Controls</span></span>  
 <span data-ttu-id="d5707-256">В этом шаблоне нельзя использовать [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d5707-257">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d5707-257">Data model</span></span>  
 <span data-ttu-id="d5707-258">Сущность [сведений об учетной записи пользователя](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="d5707-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d5707-259">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d5707-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="d5707-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5707-260">Next steps</span></span>
<span data-ttu-id="d5707-261">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d5707-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>