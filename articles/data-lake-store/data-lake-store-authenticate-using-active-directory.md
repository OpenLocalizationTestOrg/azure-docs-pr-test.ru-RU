---
title: "Аутентификация между службами в Data Lake Store с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как проверка подлинности service to service tooachieve с Azure Active Directory с помощью хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Аутентификация между службами в Data Lake Store с помощью Azure Active Directory
> [!div class="op_single_selector"]
> * [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md)
> * [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store использует Azure Active Directory для аутентификации. До создания приложения, которое работает с хранилища Озера данных Azure и аналитики Озера данных Azure, сначала необходимо решить, как tooauthenticate приложения с Azure Active Directory (Azure AD). Hello основные возможные варианты:

* Аутентификация пользователей 
* Аутентификация между службами (в этой статье) 

Оба этих параметра привести приложение, предоставляемой с токеном OAuth 2.0, который получает tooeach вложенного запроса, выполняемого tooAzure хранилища Озера данных или аналитики Озера данных Azure.

Из этой статьи вы узнаете, как создать **веб-приложение Azure AD для аутентификации между службами**. Инструкции по настройке приложения Azure AD для аутентификации пользователей см. в статье [Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Шаг 1. Создание веб-приложения Active Directory

Создайте и настройте веб-приложение Azure AD для аутентификации между службами в Azure Data Lake Store с помощью Azure Active Directory. Инструкции см. в разделе [Создание приложения Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Придерживаясь инструкциям hello в hello выше ссылку, обязательно выберите **веб-приложения и API** для типа приложения, как показано на следующем снимке экрана приветствия.

![Создание веб-приложения](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Создание веб-приложения")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Шаг 2. Получение идентификатора приложения, ключа проверки подлинности и идентификатора клиента
Программным способом входа в систему необходимо hello идентификатор для вашего приложения. Если приложение hello работает под свои собственные учетные данные, необходимо также ключ проверки подлинности.

* Инструкции как идентификатор приложения hello tooretrieve и проверка подлинности ключа (также секрет клиента вызываемой hello) для вашего приложения см. в разделе [ключ идентификатора и проверки подлинности приложения Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Инструкции как tooretrieve hello ИД клиента см. в разделе [получить идентификатор клиента](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Шаг 3: Назначение файла учетной записи хранилища Озера данных Azure toohello приложения hello Azure AD или папки (только для проверки подлинности для служб)
1. Войдите на новый toohello [портал Azure](https://portal.azure.com) и откройте hello хранилища Озера данных Azure учетной записью, которая tooassociate с hello приложения Azure Active Directory, созданной ранее.
2. В колонке учетной записи «Хранилище озера данных» щелкните **Обозреватель данных**.
   
    ![Создание каталогов в учетной записи Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Создание каталогов в учетной записи Data Lake")
3. В hello **обозреватель данных** колонке выберите hello файл или папку, для которой хотите tooprovide доступа Azure AD toohello приложения и нажмите кнопку **доступа**. файл tooa tooconfigure доступ, необходимо нажать кнопку **доступа** из hello **Просмотр файлов** колонку.
   
    ![Настройка списков управления доступом в файловой системе Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Настройка списков управления доступом в файловой системе Data Lake")
4. Hello **доступа** колонке перечислены стандартным доступом hello и настраиваемого доступа уже назначены toohello корневой. Нажмите кнопку hello **добавить** значок tooadd другой списки управления доступом.
   
    ![Перечисление стандартных и пользовательских сценариев доступа](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "Перечисление стандартных и пользовательских сценариев доступа")
5. Нажмите кнопку hello **добавить** hello значок tooopen **добавить доступ к пользовательским** колонку. В этой колонке нажмите кнопку **Выбор пользователя или группы**, а затем в **Выбор пользователя или группы** колонки, найдите приложение hello Azure Active Directory, созданной ранее. Если имеется много toosearch групп из используйте hello текстовое поле в верхнем toofilter hello на имя группы hello. Щелкните группу hello tooadd и нажмите кнопку **выберите**.
   
    ![Добавление группы](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Добавление группы")
6. Нажмите кнопку **выберите разрешения**, выберите разрешения hello и следует tooassign hello разрешения по умолчанию ACL ли получить доступ к ACL или оба. Нажмите кнопку **ОК**.
   
    ![Назначьте разрешения toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "назначить разрешения toogroup")
   
    Дополнительные сведения о разрешениях в Data Lake Store и списках ACL (по умолчанию и для доступа) см. в статье [Контроль доступа в Data Lake Store](data-lake-store-access-control.md).
7. В hello **добавить доступ к пользовательским** колонка, щелкните **ОК**. Hello добавленным группы с разрешениями hello связанные будут перечислены в hello **доступа** колонку.
   
    ![Назначьте разрешения toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "назначить разрешения toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Шаг 4: Получение hello конечная точка маркера OAuth 2.0 (только для приложений на основе Java)

1. Войдите на новый toohello [портал Azure](https://portal.azure.com) и выберите Active Directory hello левой панели.

2. На левой панели hello, нажмите кнопку **регистрации приложения**.

3. Hello верхней части колонки регистрации приложения hello, щелкните **конечные точки**.

    ![Конечная точка маркера OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")

4. Из списка hello конечных точек скопируйте конечная точка маркера OAuth 2.0 hello.

    ![Конечная точка маркера OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")   

## <a name="next-steps"></a>Дальнейшие действия
В этой статье необходимо создать веб-приложение Azure AD и собрать hello сведения, необходимые в клиентских приложениях можно создавать с помощью пакета SDK для .NET, Java SDK, и т. д. Теперь можно перейти toohello следующие статьи, в которых расскажем, как проверка подлинности приложения web toofirst для toouse hello Azure AD с хранилища Озера данных и затем выполнить другие операции в хранилище hello.

* [Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET](data-lake-store-get-started-net-sdk.md)
* [Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET](data-lake-store-get-started-java-sdk.md)

В этой статье подробно описан hello основные шаги, необходимые tooget пользователь основной копии и запущена для вашего приложения. Можно взглянуть на hello следующие статьи tooget дополнительную информацию.
* [Использовать субъекта-службы toocreate PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Создание субъекта-службы с использованием сертификата](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Другие методы tooauthenticate tooAzure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


