---
title: "aaaSet специальную домашнюю страницу для опубликованных приложений с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Описываются основы hello о соединителей прокси приложения Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Настройка пользовательской домашней страницы для опубликованных приложений с помощью прокси приложения Azure AD

В этой статье рассматриваются как tooconfigure приложений toodirect пользователей tooa специальную домашнюю страницу. При публикации приложения с помощью прокси приложения задать внутренний URL-адрес, но иногда, не видят пользователи должны сначала страницы приветствия. Задайте специальную домашнюю страницу, чтобы пользователи переход на страницу правой toohello при доступе приложения hello из панели доступа Active Directory Azure hello или средство запуска приложений Office 365 hello.

Когда пользователь запустит приложение hello, они все руководством по умолчанию toohello корневой домен URL-адрес для опубликованного приложения hello. Целевая страница Hello обычно устанавливается в виде URL-адрес домашней страницы приветствия. Используйте URL-адреса hello Azure AD PowerShell модуль toodefine специальную домашнюю страницу, при необходимости tooland пользователей приложения на конкретной странице в приложение hello. 

Например:
- В корпоративной сети, будут переходить пользователи слишком*https://ExpenseApp/login/login.aspx* toosign в и доступ к вашему приложению.
- Так как у вас есть другие активы, подобно изображениям, прокси-сервер приложений должен tooaccess на верхнем уровне структуры папок hello hello, публикации приложения hello с *https://ExpenseApp* как hello внутренний URL-адрес.
- Здравствуйте, внешний URL-адрес по умолчанию *https://ExpenseApp-contoso.msappproxy.net*, который не принимает toohello входа пользователей на странице.  
- Задать *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* как hello toogive URL-адрес домашней страницы пользователей эффективной работы. 

>[!NOTE]
>Когда приложения toopublished предоставить доступ пользователям приложения hello, отображаются в hello [панели доступа Azure AD](active-directory-saas-access-panel-introduction.md) и hello [средство запуска приложений Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Перед началом работы

Перед установкой URL-адрес домашней страницы приветствия Имейте в виду hello следующие требования:

* Убедитесь, что этот путь hello представляет собой путь к поддомен hello корневой домен URL-адрес.

  Если URL-адрес корневого домена hello, например, https://apps.contoso.com/app1/, hello Домашняя страница URL-адреса должно начинаться с https://apps.contoso.com/app1/.

* При внесении изменений toohello публикации приложения, изменение hello может сбросить значение hello URL-адрес домашней страницы приветствия. При обновлении приложения hello в будущем hello, необходимо повторно проверить и, при необходимости измените URL-адрес домашней страницы приветствия.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Изменить домашнюю страницу приветствия в hello портал Azure

1. Войдите в toohello [портал Azure](https://portal.azure.com) с правами администратора.
2. Перейдите в слишком**Azure Active Directory** > **регистрации приложения** и выберите приложение из списка hello. 
3. Выберите **свойства** из настроек hello.
4. Обновление hello **URL-адрес домашней страницы** поле ваш новый путь. 

   ![Указание нового URL-адреса домашней страницы](./media/application-proxy-office365-app-launcher/homepage.png)

5. Нажмите кнопку **Сохранить**.

## <a name="change-hello-home-page-with-powershell"></a>Изменить домашнюю страницу приветствия с помощью PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Установка модуля Azure AD PowerShell hello

Прежде чем определить URL-адрес домашней страницы с помощью PowerShell, установите модуль Azure AD PowerShell hello. Можно загрузить пакет hello hello [коллекции PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), который использует hello конечная точка Graph API. 

tooinstall hello пакет, выполните следующие действия:

1. Откройте стандартное окно PowerShell и выполните следующую команду hello:

    ```
     Install-Module -Name AzureAD
    ```
    Если вы используете команду hello как без прав администратора, используйте hello `-scope currentuser` параметр.
2. Во время установки hello выберите **Y** tooinstall двух пакетов из Nuget.org. Требуются оба пакета. 

### <a name="find-hello-objectid-of-hello-app"></a>Найти hello ObjectID приложение hello

Получите hello ObjectID приложение hello и выполните поиск приложения hello, домашняя страница.

1. Откройте PowerShell и импорт модуля hello Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Войдите в toohello модуля Azure AD как администратор клиента hello.

    ```
    Connect-AzureAD
    ```
3. Найти приложение hello в зависимости от его URL-адрес домашней страницы. Hello URL-адрес можно найти в портале hello, перейдя слишком**Azure Active Directory** > **корпоративных приложений** > **все приложения**. В этом примере используется *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Вы должны получить результат, аналогичный toohello показанной здесь. Скопируйте hello toouse ObjectID GUID в следующем разделе hello.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Обновить URL-адрес домашней страницы приветствия

В hello же модуль PowerShell, который использовался в шаге 1, выполните следующие шаги hello.

1. Убедитесь, что hello исправьте приложения и замените *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* с hello ObjectID, скопированным на предшествующий шаг hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Теперь, когда вы убедились, приложение hello, вы готовы tooupdate hello домашней страницы, следующим образом.

2. Создайте пустое приложение объекта toohold hello изменения, которые должны toomake. Эта переменная содержит hello значения, которые должны tooupdate. На этом шаге ничто не создается.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Набор hello Домашняя страница URL-адрес toohello нужное значение. Hello значение должно быть контура поддомен опубликованное приложение hello. Например, если изменить hello URL-адрес домашней страницы из *https://sharepoint-iddemo.msappproxy.net/* слишком*https://sharepoint-iddemo.msappproxy.net/hybrid/*, пользователи приложения перейдите непосредственно настраиваемый toohello Домашняя страница.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Сделать hello обновления с помощью hello GUID (ObjectID), который был скопирован в «шаг 1: hello поиска ObjectID приложение hello.»

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm, hello изменений успешно выполнена, перезапустите приложение hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>URL-адрес домашней страницы приветствия, могут быть сброшены изменения, выполняемые toohello приложения. Если URL-адрес домашней страницы сбрасывается, то повторите шаг 2.

## <a name="next-steps"></a>Дальнейшие действия

- [Включить tooSharePoint удаленного доступа с помощью прокси приложения Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Включите прокси приложения в hello портал Azure](active-directory-application-proxy-enable.md)
