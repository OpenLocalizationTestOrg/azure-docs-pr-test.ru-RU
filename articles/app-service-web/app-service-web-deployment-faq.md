---
title: "aaaDeployment вопросы и ответы для веб-приложениях Azure | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о развертывании для веб-приложений функции hello службе приложений Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Часто задаваемые вопросы о развертывании в веб-приложениях Azure

Данная статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о проблем развертывания для hello [веб-приложений функции службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Я только начинаю работу с веб-приложениями службы приложений. Как опубликовать код?

Опубликовать код можно несколькими способами:

*   Развертывание с помощью Visual Studio. Если у вас есть решение Visual Studio hello, щелкните правой кнопкой мыши проект веб-приложения hello и выберите **публикации**.
*   Развертывание с помощью FTP-клиента. В hello портал Azure, профиль для веб-приложения hello публикации hello загрузки должен toodeploy код. Затем добавьте hello too\site\wwwroot файлы с помощью hello же опубликовать профиль FTP учетные данные.

Дополнительные сведения см. в разделе [развертывание вашего приложения tooApp службы](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Я вижу сообщение об ошибке при попытке toodeploy из Visual Studio. Как решить эту проблему?

При появлении следующего сообщением hello, возможно, вы используете старую версию пакета SDK для hello: «ошибка при развертывании для ресурса «YourResourceName» в группе ресурсов «YourResourceGroup»: MissingRegistrationForLocation: hello подписка не зарегистрирована для Hello тип ресурса «components» в расположении hello «Центральной части США». Повторите регистрацию для этого поставщика в порядке toohave доступа toothis расположении.» 

tooresolve это ошибка, обновления toohello [новейшую версию пакета SDK](https://azure.microsoft.com/downloads/). Если вы видите это сообщение и иметь hello новейшую версию пакета SDK, отправьте запрос на техническую поддержку.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Развертывание приложений ASP.NET из Visual Studio tooApp службы
<a id="deployasp"></a>

Учебник Hello [создание первого веб-приложения ASP.NET в Azure в течение пяти минут](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) показано, как toodeploy ASP.NET веб-приложения tooa веб-приложения в службе приложений с помощью Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Что такое hello различные типы учетных данных развертывания

Служба приложений поддерживает два типа учетных данных для развертывания локальной системы Git и развертывания FTP(S). Дополнительные сведения о том, как tooconfigure учетные данные развертывания, в разделе [настроить учетные данные развертывания для приложения службы](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Что такое hello файл или каталог структуру веб-приложение службы приложений?

Сведения о структуре его файла hello приложение службы приложений см. в разделе [файла структуры в Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Как решить «Ошибка FTP 550 - там не достаточно места на диске hello» при попытке tooFTP Мои файлы?

Если вы видите это сообщение, вполне вероятно, что выполняется в дисковой квоты в плане обслуживания hello веб-приложения. Может потребоваться tooscale копирование tooa зависимости от потребностей места на диске более высоком уровне службы. Дополнительные сведения о ценах на планы и ограничениях ресурсов см. на [этой странице](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Как настроить непрерывное развертывание веб-приложения служб приложений?

Непрерывное развертывание можно настроить из нескольких ресурсов, в том числе Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox и других репозиториев Git. Эти параметры доступны на портале hello. [Непрерывное развертывание tooApp службы](app-service-continuous-deployment.md) является полезным учебник, в котором объясняется, как tooset непрерывное развертывание.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Как устранить проблемы с непрерывным развертыванием из GitHub и Bitbucket?

Сведения о проблемах с непрерывным развертыванием из GitHub или Bitbucket см. в статье [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment) (Изучение непрерывного развертывания).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Нельзя FTP-сайта toomy и опубликовать мой код. Как решить эту проблему?

проблемы tooresolve FTP:

1. Проверка ввода hello правильным именем узла и учетные данные. Подробные сведения о различных типах учетных данных и как toouse, см. статью [учетные данные развертывания](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Убедитесь, что hello FTP-порты не заблокирован брандмауэром. Hello порты должны иметь следующие параметры:
    * Порт подключения для управления FTP: 21
    * Порт подключения к данным FTP: 989, 10001–10300.

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Как опубликовать мой код tooApp службы?

Hello быстрый запуск Azure — спроектированный toohelp развертывания приложения с помощью развертывания стека hello и метод по своему усмотрению. hello toouse краткое руководство, в hello портал Azure перейдите слишком**параметры** > **развертывания приложения**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Почему мое приложение иногда перезапускает после развертывания tooApp службы?

toolearn об условиях возникновения hello, при которых развертывания приложения может привести к перезагрузка, в разделе [развертывания и проблемам](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Как описано в статье hello, службы приложений развертывает папки wwwroot toohello файлов. Она никогда напрямую не перезапускает приложение.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Как интегрировать код Visual Studio Team Services с помощью службы приложений?

Реализовать непрерывное развертывание с помощью Visual Studio Team Services можно двумя способами:

*   Используйте проект Git. Подключение через службы приложений с помощью hello параметры развертывания для этого репозитория.
*   Используйте проект системы управления версиями Team Foundation (TFVC). Развертывание с помощью hello агент сборки для приложения службы.

В обоих случаях непрерывное развертывание кода зависит от имеющихся рабочих процессов разработчика и процедур проверки. Дополнительные сведения вы найдете в следующих статьях: 

*   [Реализовать непрерывного развертывания вашего приложения tooan веб-сайте Azure](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Настройка учетной записи Visual Studio Team Services, чтобы можно было развернуть tooa веб-приложения](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Как использовать FTP или FTPS toodeploy tooApp Мои приложения службы

Дополнительные сведения об использовании FTP или FTPS toodeploy вашей tooApp app web Service, в разделе [развертывание вашего приложения tooApp службы с помощью FTP/S](app-service-deploy-ftp.md).
