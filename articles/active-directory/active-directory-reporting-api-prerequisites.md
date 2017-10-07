---
title: "aaaPrerequisites tooaccess hello Azure AD отчетов API. | Документация Майкрософт"
description: "Дополнительные сведения об отчетности API hello Azure AD tooaccess hello предварительные требования"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API отчетов hello Azure AD tooaccess предварительные требования
Hello [reporting API-интерфейсов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставить программный доступ к данным toohello через набор API на основе REST. Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.

модуль отчетов API Hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize доступа toohello веб-API. 

tooprepare вашей reporting API toohello доступ, необходимо:

1. Создайте приложение в клиенте Azure AD. 
2. Приложения соответствующие разрешения GRANT hello tooaccess hello данных Azure AD
3. Получите параметры конфигурации из каталога.

Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Создание приложения Azure AD
tooconfigure directory API отчетов tooaccess hello Azure AD, необходимо войти в toohello классический портал Azure с учетной записью администратора подписки Azure, который также является членом роли каталога hello глобального администратора в клиенте Azure AD.

> [!IMPORTANT]
> Приложениям, выполняемым учетные данные с правами «admin», как это может быть очень мощные, поэтому имейте безопасного убедиться, что tookeep hello идентификатор и секрет учетные данные приложения.
> 
> 

1. В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Из hello **active directory** список, выберите свой каталог.
3. В меню в верхней части hello hello выберите **приложений**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. На нижней панели hello щелкните **добавить**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/03.png) 
5. На hello **что вам требуется toodo?** диалоговое окно, нажмите кнопку **добавить приложение, разрабатываемое моей организацией**. 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/04.png) 
6. На hello **Расскажите о своем приложении** диалоговое окно, выполните следующие шаги hello: 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    а. В hello **имя** текстовом поле введите имя (например: приложения API для отчетов).
   
    b. Выберите **Веб-приложение и/или веб-API**.
   
    c. Щелкните **Далее**.
7. На hello **свойства приложения** диалоговое окно, выполните следующие шаги hello: 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    а. В hello **URL-адрес входа** введите `https://localhost`.
   
    b. В hello **URI идентификатора приложения** введите ```https://localhost/ReportingApiApp```.
   
    c. Нажмите **Завершено**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Предоставьте разрешение hello toouse API вашего приложения
1. В hello [классический портал Azure](https://manage.windowsazure.com/), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Из hello **active directory** список, выберите свой каталог.
3. В меню в верхней части hello hello выберите **приложений**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png)
4. В списке приложений hello выберите только что созданный приложения.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. В меню в верхней части hello hello выберите **Настройка**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. В hello **tooother разрешения приложений** раздел для hello **Azure Active Directory** ресурсов, щелкните hello **разрешения приложения** раскрывающегося списка, а затем Выберите **читать данные каталога**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/09.png)
7. На нижней панели hello щелкните **Сохранить**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Получите параметры конфигурации из каталога.
В этом разделе показано, как hello tooget следующие параметры из каталога:

* Доменное имя
* Идентификатор клиента
* Секрет клиента

Эти значения необходимо при настройке отчетов API toohello вызовов. 

### <a name="get-your-domain-name"></a>Получение имени домена
1. В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Из hello **active directory** список, выберите свой каталог.
3. В меню в верхней части hello hello выберите **домены**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/11.png) 
4. В hello **доменное имя** столбца, скопируйте имя домена.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Получить идентификатор клиента приложения hello
1. В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Из hello **active directory** список, выберите свой каталог.
3. В меню в верхней части hello hello выберите **приложений**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. В списке приложений hello выберите только что созданный приложения.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. В меню в верхней части hello hello выберите **Настройка**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. Скопируйте значение **идентификатор клиента**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Получить секрет клиента приложения hello
tooget клиентского приложения в тайне, нужно toocreate новый ключ и сохранить его значение при сохранении hello новый ключ, так как он не возможные tooretrieve позже больше это значение.

1. В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Из hello **active directory** список, выберите свой каталог.
3. В меню в верхней части hello hello выберите **приложений**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. В списке приложений hello выберите только что созданный приложения.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. В меню в верхней части hello hello выберите **Настройка**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. В hello **ключей** выполните следующие шаги hello: 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/14.png)
   
    а. Выберите из списка длительность hello длительность
   
    b. На нижней панели hello щелкните **Сохранить**.
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Скопируйте значение ключа hello.

## <a name="next-steps"></a>Дальнейшие действия
* Бы вы, как данные из Azure AD hello hello tooaccess reporting API программным способом Извлечение [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).
* Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).  

