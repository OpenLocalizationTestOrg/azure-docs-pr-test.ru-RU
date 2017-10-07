---
title: "aaaDeploy tooAzure вашего приложения службы приложений с помощью FTP/S | Документы Microsoft"
description: "Узнайте, как toodeploy tooAzure вашего приложения, приложение службы с помощью FTP или FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Развертывание вашего приложения tooAzure службы приложений с помощью FTP/S

В этой статье показано, как toouse FTP или FTPS toodeploy вашего веб-приложения, внутреннего сервера мобильного приложения или приложения API слишком[службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

конечную точку FTP/S Hello для приложения уже активен. Конфигурация не является развертывание FTP/S необходимые tooenable.

> [!IMPORTANT]
> Мы выполняем постоянно tooimprove действия безопасности на платформе Microsoft Azure. В ходе этой работы планируется обновление веб-приложений в регионе "Центральная Германия" и "Северо-восточная Германия". Во время этого веб-приложения отключение hello использование протокола обычный текст FTP для развертывания. Рекомендации клиентов tooour — tooFTPS tooswitch для развертываний. Не ожидается tooyour любой перебоев в работе службы во время этого обновления, который планируется для 9/5. Благодарим за вашу помощь!

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Шаг 1. Настройка учетных данных развертывания

сервер tooaccess hello FTP для приложения, необходимо сначала учетные данные развертывания. 

tooset или Сброс учетных данных развертывания, см. раздел [учетные данные развертывания службы приложения Azure](app-service-deployment-credentials.md). В этом учебнике показано hello использовать учетные данные уровня пользователя.

## <a name="step-2-get-ftp-connection-information"></a>Шаг 2. Получение информации о подключении по FTP

1. В hello [портал Azure](https://portal.azure.com), откройте ваше приложение [колонки ресурсов](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Выберите **Обзор** в левом меню hello, затем запишите значения hello для **пользователя FTP или развертывание**, **имя узла FTP**, и **FTPS имя узла**. 

    ![Информация о подключении по FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Hello **пользователя FTP или развертывание** значение пользователя, отображаться по hello портал Azure, включая имя приложения hello в порядке tooprovide правильный контекст для hello FTP-сервера.
    > Можно найти hello же данные при выборе **свойства** в левом меню hello. 
    >
    > Кроме того пароль развертывания hello никогда не отображается. Если вы забудете пароль развертывания, вернитесь слишком[шаг 1](#step1) и сбросить пароль развертывания.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Шаг 3: Развертывание файлов tooAzure

1. Из клиента FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)и т. д), используйте сведения о подключении hello собранные tooconnect tooyour приложения.
3. Скопировать файлы и их соответствующих структуры toohello [ **/сайт/wwwroot** каталога](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) в Azure (или hello **/сайта и wwwroot/App_Data и задания или** каталогом Веб-заданий).
4. Приложение hello tooverify URL-адрес приложения tooyour обзора выполняется правильно. 

> [!NOTE] 
> В отличие от [развертывания на основе Git](app-service-deploy-local-git.md), развертывание FTP не поддерживает следующие автоматизации развертывания hello: 
>
> - восстановление зависимостей (например, в инструментах автоматизации NuGet, NPM, PIP и Composer);
> - компиляция двоичных файлов .NET;
> - создание файла Web.config (вот [пример для Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps)).
> 
> Необходимо вручную выполнить восстановление, сборку и создание этих необходимых файлов на локальном компьютере, а затем развернуть их вместе с приложением.
>
>

## <a name="next-steps"></a>Дальнейшие действия

Для более сложных сценариев развертывания, попробуйте [развертывание tooAzure с Git](app-service-deploy-local-git.md). Развертывание на основе Git tooAzure позволяет системе управления версиями, восстановление пакета, MSBuild и многое другое.

## <a name="more-resources"></a>Дополнительные ресурсы

* [Создание веб-приложения PHP-MySQL и его развертывание с помощью FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Учетные данные развертывания службы приложений Azure](app-service-deploy-ftp.md)
