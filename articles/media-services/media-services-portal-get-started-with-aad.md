---
title: "aaaGet к выполнению проверки подлинности Azure AD с помощью hello портал Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure портала tooaccess tooconsume проверки подлинности Azure Active Directory (Azure AD) hello API служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Начало работы с проверкой подлинности Azure AD с помощью портала Azure hello

Узнайте, как toouse hello Azure tooaccess портала Azure Active Directory (Azure AD) для проверки подлинности tooaccess hello API служб мультимедиа Azure.

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/). 
- Учетная запись служб мультимедиа. Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).
- Обязательно изучите hello [доступ к Azure API служб мультимедиа с обзор проверки подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

При использовании аутентификации Azure AD со службами мультимедиа Azure доступны два метода аутентификации.

- **Аутентификация пользователя**. Проверка подлинности пользователя, работающего с toointeract приложения hello с ресурсами службы мультимедиа. интерактивные приложения Hello должен сначала запросить учетные данные пользователя hello. Пример — приложение консоли управления, используемые заданий кодирования toomonitor авторизованных пользователей или динамической потоковой передачи. 
- **Аутентификация субъекта-службы**. Аутентификация службы. Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания: веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.

> [!IMPORTANT]
> В настоящее время службы мультимедиа поддерживают модель проверки подлинности службы контроля доступа Azure hello. Тем не менее авторизация посредством службы контроля доступа будет объявлена устаревшей 1 июня 2018 года. Рекомендуется как можно быстрее перейти модель проверки подлинности toohello Azure AD.

## <a name="select-hello-authentication-method"></a>Выберите метод проверки подлинности hello

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа.
2. Выбор метода tooconnect toohello API служб мультимедиа.

    ![Страница выбора способа подключения](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Аутентификация пользователей

toohello tooconnect API служб мультимедиа с помощью hello вариант проверки подлинности пользователя, клиентское приложение hello должен toorequest маркера Azure AD, который имеет hello следующие параметры:  

* Конечная точка клиента Azure AD.
* Универсальный код ресурса (URI) для ресурса служб мультимедиа.
* Идентификатор клиента (собственного) приложения служб мультимедиа. 
* Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа. 
* Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.

Вы можете получить hello значения для этих параметров на hello **API служб мультимедиа с проверкой подлинности пользователя** страницы. 

![Страница подключения с помощью аутентификации пользователя](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

При подключении toohello API служб мультимедиа с помощью Media Services Microsoft .NET SDK hello hello необходимых значений tooyou доступны как часть пакета SDK для hello. Дополнительные сведения см. в разделе [tooaccess проверки подлинности используют Azure AD hello API служб мультимедиа Azure в .NET Framework](media-services-dotnet-get-started-with-aad.md).

Если вы не используете пакет SDK для клиента .NET служб мультимедиа hello, необходимо вручную создать запрос токена Azure AD с помощью параметров hello уже было сказано ранее. Дополнительные сведения см. в разделе [как tooget библиотеки проверки подлинности Azure AD hello toouse hello Azure AD токен](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Проверка подлинности субъекта-службы

toohello tooconnect API служб мультимедиа с помощью hello параметр участника службы, приложения среднего уровня (веб-API или веб-приложение) должен toorequest маркера Azure AD, который имеет hello следующие параметры:  

* Конечная точка клиента Azure AD.
* Универсальный код ресурса (URI) для ресурса служб мультимедиа. 
* Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.
* Значения приложения Azure AD: hello **идентификатор клиента** и **секрет клиента**

Вы можете получить hello значения для этих параметров на hello **подключения tooMedia API служб с субъектом-службой** страницы. Использование этой страницы toocreate новый Azure AD приложения или tooselect уже существующий. После выбора приложения hello Azure AD можно получить идентификатор клиента hello (идентификатор приложения) и создать секрет (ключ) значениями hello клиента. 

![Страница подключения с помощью субъекта-службы](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Здравствуйте, когда **участника-службы** открывает колонку, выбран первый Azure AD приложения hello, отвечающего hello следующие условия:

- оно зарегистрировано в Azure AD;
- Он имеет разрешения участника или Owner Role-Based управления доступом для hello учетной записи.

После создания или выбора приложения Azure AD, можно создать и скопируйте секрет клиента (ключ) и hello идентификатор клиента (идентификатор приложения). Идентификатор секрета и клиент клиента Hello, маркер доступа требуется tooget hello в этом сценарии.

При отсутствии приложения Azure AD toocreate разрешений в вашем домене, не отображаются элементы управления приложения Azure AD hello колонка hello и выводится предупреждающее сообщение.

При подключении toohello API служб мультимедиа с помощью Media Services .NET SDK hello. в разделе [tooaccess проверки подлинности используют Azure AD hello API служб мультимедиа Azure в .NET Framework](media-services-dotnet-get-started-with-aad.md).

Если не используется пакет SDK для клиента .NET служб мультимедиа hello, необходимо вручную создать запрос токена Azure AD с помощью параметров hello уже было сказано ранее. Дополнительные сведения см. в разделе [как tooget библиотеки проверки подлинности Azure AD hello toouse hello Azure AD токен](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Получить идентификатор и секрет клиента приветствия клиента

После выбора существующего приложения Azure AD или выберите hello параметр toocreate новый, отображаются hello следующие кнопки:

![Кнопки "Управление разрешениями" и "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

hello tooopen колонке приложения Azure AD щелкните **управления приложением**. На hello **управления приложением** колонки, можно получить идентификатор клиента приложения hello (идентификатор приложения). секрет клиента (ключ), выберите toogenerate **ключей**.

![Параметр "Ключи" в колонке "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Управление разрешениями и приложения hello

После выбора приложения hello Azure AD, вы можете управлять приложения hello и разрешения. tooset копирование вашего tooaccess приложения Azure AD щелкните другие приложения **Управление разрешениями**. Для задач управления, таких как изменение ключей и URL-адреса ответа и манифест приложения hello tooedit, нажмите кнопку **управления приложением**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Изменить параметры приложения hello или манифеста

параметры или манифест, приложение hello tooedit щелкните **управления приложением**.

![Страница "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Дальнейшие действия

Приступая к работе с [передача файлов учетная запись tooyour](media-services-portal-upload-files.md).
