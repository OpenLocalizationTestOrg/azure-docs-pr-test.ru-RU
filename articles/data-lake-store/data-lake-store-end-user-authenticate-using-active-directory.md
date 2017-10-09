---
title: "Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как проверка подлинности для конечных пользователей tooachieve с хранилища Озера данных с помощью Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory
> [!div class="op_single_selector"]
> * [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md)
> * [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store использует Azure Active Directory для аутентификации. До создания приложения, которое работает с хранилища Озера данных Azure и аналитики Озера данных Azure, сначала необходимо решить, как tooauthenticate приложения с Azure Active Directory (Azure AD). Hello основные возможные варианты:

* Аутентификация пользователей (в этой статье)
* Взаимодействие между службами

Оба этих параметра привести приложение, предоставляемой с токеном OAuth 2.0, который получает tooeach вложенного запроса, выполняемого tooAzure хранилища Озера данных или аналитики Озера данных Azure.

Из этой статьи вы узнаете, как создать **собственное приложение Azure AD для аутентификации пользователей**. Инструкции по настройке приложения Azure AD для аутентификации между службами см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* Идентификатор подписки. Его можно получить из hello портала Azure. Например он доступен из колонки учетной записи хранилища Озера данных hello.
  
    ![Получение идентификатора подписки](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Доменное имя Azure AD. Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портала Azure. Из hello снимке hello доменное имя — **contoso.onmicrosoft.com**, и hello GUID внутри скобок является идентификатором hello клиента. 
  
    ![Получение домена AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Аутентификация пользователей
Это рекомендованный подход, если требуется, чтобы toolog конечным пользователем в приложении tooyour через Azure AD hello. Приложение будет подвергаться может tooaccess ресурсы Azure с hello таким же уровнем доступа как hello конечного пользователя, который вход. Конечному пользователю потребуется tooprovide свои учетные данные периодически toomaintain приложению доступ.

Hello с конечным пользователем hello вход образом, приложение получает токен доступа и токена обновления. маркер доступа Hello получает запрос tooeach вложенное хранилище Озера tooData или аналитики Озера данных и действителен в течение одного часа, по умолчанию. токен обновления Hello может быть используется tooobtain новый маркер доступа, который действителен для копии недель tootwo по умолчанию, если используется регулярно. Для входа пользователей можно использовать два разных подхода.

### <a name="using-hello-oauth-20-pop-up"></a>С помощью всплывающего окна hello OAuth 2.0
Приложение может вызывать всплывающих авторизации OAuth 2.0, в которых hello для конечных пользователей можно вводить свои учетные данные. Это всплывающее окно также работает с процессом hello Azure AD, двухфакторной проверки подлинности (2FA), при необходимости. 

> [!NOTE]
> Этот метод не еще поддерживается в hello библиотеки проверки подлинности Azure AD (ADAL) для Python или Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Непосредственная передача учетных данных пользователя
Приложение может предоставлять непосредственно tooAzure учетные данные пользователя AD. Этот метод работает только для учетных записей на основе идентификаторов организации. Он не подходит для личных учетных записей пользователей или учетных записей на основе Live ID, включая те, которые заканчиваются на @outlook.com или @live.com. Кроме того, данный метод несовместим с учетными записями пользователей, для которых требуется двухфакторная проверка подлинности (2FA) Azure AD.

### <a name="what-do-i-need-toouse-this-approach"></a>Что делать мне toouse этот подход?
* Доменное имя Azure AD Уже есть в необходимом компоненте hello данной статьи.
* **Собственное приложение** Azure AD.
* Идентификатор приложения для собственного приложения hello Azure AD
* URI перенаправления для hello собственное приложение Azure AD
* Настроенные делегированные разрешения.


## <a name="step-1-create-an-active-directory-native-application"></a>Шаг 1. Создание собственного приложения Active Directory

Создайте и настройте собственное приложение Azure AD для аутентификации пользователей в Azure Data Lake Store с помощью Azure Active Directory. Инструкции см. в разделе [Создание приложения Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Придерживаясь инструкциям hello в hello выше ссылку, обязательно выберите **собственного** для типа приложения, как показано на следующем снимке экрана приветствия.

![Создание веб-приложения](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Создание собственного приложения")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Шаг 2. Получение идентификатора приложения и URI перенаправления

В разделе [получить идентификатор приложения hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello идентификатор приложения (также называется hello идентификатор клиента в hello классический портал Azure) собственного приложения hello Azure AD.

tooretrieve hello URI перенаправления, выполните следующие шаги hello.

1. Hello портал Azure, выберите **Azure Active Directory**, нажмите кнопку **регистрации приложения**, затем найдите и выберите только что созданный собственное приложение hello Azure AD.

2. Из hello **параметры** щелкните колонку для приложения hello **URI перенаправления**.

    ![Получение URI перенаправления](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Скопируйте отображаемое значение hello.


## <a name="step-3-set-permissions"></a>Шаг 3. Установка разрешений

1. Hello портал Azure, выберите **Azure Active Directory**, нажмите кнопку **регистрации приложения**, затем найдите и выберите только что созданный собственное приложение hello Azure AD.

2. Из hello **параметры** щелкните колонку для приложения hello **разрешения, необходимые**и нажмите кнопку **добавить**.

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. В hello **Добавление доступа к API** колонке нажмите кнопку **выберите API**, нажмите кнопку **Озера данных Azure**, а затем нажмите кнопку **выберите**.

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  В hello **Добавление доступа к API** колонке нажмите кнопку **разрешений Select**, выберите hello флажок toogive **полного доступа к хранилищу Озера tooData**и нажмите кнопку **выберите** .

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Нажмите кнопку **Done**(Готово).

5. Повторите hello последние два шага toogrant разрешения для **API управления службами Windows Azure** также.
   
## <a name="next-steps"></a>Дальнейшие действия
В этой статье создания собственного приложения Azure AD и собрать информацию о hello в клиентские приложения, создаваемые с помощью пакета SDK для .NET, Java SDK, REST API, и т. д. Теперь можно перейти toohello следующие статьи, в которых расскажем, как проверка подлинности приложения web toofirst для toouse hello Azure AD с хранилища Озера данных и затем выполнить другие операции в хранилище hello.

* [Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET](data-lake-store-get-started-net-sdk.md)
* [Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET](data-lake-store-get-started-java-sdk.md)
* [Начало работы с Azure Data Lake Store с помощью REST API](data-lake-store-get-started-rest-api.md)

