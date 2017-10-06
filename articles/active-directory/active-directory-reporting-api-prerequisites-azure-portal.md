---
title: "API отчетов Azure AD hello tooaccess aaaPrerequisites | Документы Microsoft"
description: "Дополнительные сведения об отчетности API hello Azure AD tooaccess hello предварительные требования"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API отчетов hello Azure AD tooaccess предварительные требования

Hello [reporting API-интерфейсов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставить программный доступ к данным toohello через набор API на основе REST. Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.

модуль отчетов API Hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize доступа toohello веб-API. 

tooget доступ toohello данных отчетов с помощью hello API, необходимо toohave одно из следующих ролях, назначенных hello:

- Чтение данных безопасности
- администратор безопасности;
- глобальный администратор.


tooprepare вашей reporting API toohello доступ, необходимо:

1. Регистрация приложения 
2. предоставьте разрешения; 
3. Сбор параметров конфигурации 

Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, [отправьте запрос в службу поддержки](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Регистрация приложения Azure Active Directory

Необходимо tooregister приложения, даже если вы пользуетесь hello reporting API, с помощью скрипта. Этот метод позволяет **идентификатор приложения**, которая используется для вызова авторизации и позволяет маркеры tooreceive кода.

tooconfigure directory API отчетов tooaccess hello Azure AD, необходимо войти в toohello портал Azure с учетной записью администратора Azure, который также является членом hello **глобального администратора** роли каталога в клиенте Azure AD .

> [!IMPORTANT]
> Приложениям, выполняемым учетные данные с правами «admin», как это может быть очень мощные, поэтому имейте безопасного убедиться, что tookeep hello идентификатор и секрет учетные данные приложения.
> 


**tooregister приложение Azure Active Directory:**

1. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. На hello **Azure Active Directory** колонка, щелкните **регистрации приложения**.

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. На hello **регистрации приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **Регистрация нового приложения**.

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. На hello **создать** колонки, выполните следующие шаги hello:

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    а. В hello **имя** введите `Reporting API application`.

    b. В качестве **типа приложения** выберите **Веб-приложение или API**.

    c. В hello **URL-адрес входа** введите `https://localhost`.

    d. Щелкните **Создать**. 


## <a name="grant-permissions"></a>Предоставление разрешений 

Цель этого шага Hello является toogrant приложения **читать данные каталога** toohello разрешения **Windows Azure Active Directory** API.

![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant вашего приложения hello toouse разрешение API:**

1. На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.

2. На hello **Reporting API приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **параметры**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. На hello **параметры** колонка, щелкните **требуемые разрешения**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. На hello **разрешения, необходимые** колонки в hello **API** выберите **Windows Azure Active Directory**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. На hello **включить доступ** колонке выберите **читать данные каталога**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Щелкните hello панели инструментов в верхней части hello **Сохранить**.

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Сбор параметров конфигурации 
В этом разделе показано, как hello tooget следующие параметры из каталога:

* Доменное имя
* Идентификатор клиента
* Секрет клиента

Эти значения необходимо при настройке отчетов API toohello вызовов. 

### <a name="get-your-domain-name"></a>Получение имени домена

**tooget доменного имени:**

1. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. На hello **Azure Active Directory** колонка, щелкните **доменных имен**.

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Скопируйте имя домена из списка доменов hello.


### <a name="get-your-applications-client-id"></a>Получение идентификатора клиента приложения

**tooget идентификатор клиента приложения:**

1. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.

3. На hello **Reporting API приложения** колонки в hello **идентификатор приложения**, нажмите кнопку **щелкните toocopy**.

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Получение секрета клиента приложения
tooget клиентского приложения в тайне, нужно toocreate новый ключ и сохранить его значение при сохранении hello новый ключ, так как он не возможные tooretrieve позже больше это значение.

**tooget секрет клиента приложения:**

1. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.


3. На hello **Reporting API приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **параметры**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. На hello **параметры** колонки в hello **доступа APIR** щелкните **ключей**. 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. На hello **ключей** колонки, выполните следующие шаги hello:

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    а. В hello **описание** введите `Reporting API`.

    b. Для параметра **Срок действия истекает** выберите значение **Через 2 года**.

    c. Щелкните **Сохранить**.

    d. Скопируйте значение ключа hello.


## <a name="next-steps"></a>Дальнейшие действия
* Бы вы, как данные из Azure AD hello hello tooaccess reporting API программным способом Извлечение [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).
* Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).  

