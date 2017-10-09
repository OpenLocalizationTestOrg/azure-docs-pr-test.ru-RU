---
title: "Параметры приложения Azure функция aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooconfigure Azure функция параметров приложения."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Как toomanage приложении функции в hello портал Azure 

В функциях Azure приложения функция предоставляет контекст выполнения hello для отдельных функций. Функции приложения поведения применяются функции tooall, размещаемую в приложении заданной функции. В этом разделе описывается способ tooconfigure и управляйте своими приложениями функции hello портал Azure.

toobegin перейдите toohello [портал Azure](http://portal.azure.com) и выполните вход tooyour учетная запись Azure. В строке поиска hello hello верхней части портала hello введите имя функции приложения hello и выберите его из списка hello. После выбора функции приложения, появится следующая страница приветствия:

![Обзор функции приложения в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Вкладка параметров приложения-функции

![Обзор функции приложения в hello портал Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Hello **параметры** вкладка —, где вы можете обновить версию среды выполнения функции hello, используемые приложением функции. Также он служит для управления hello узла ключи, используемые toorestrict HTTP tooall функции для доступа к размещенным функция приложение hello.

Компонент функции поддерживает планы размещения как для потребления, так и для службы приложений. Дополнительные сведения см. в разделе [Выбор плана правильную службу hello для функций Azure](functions-scale.md). Позволяет лучше прогнозировать в плане использования hello функций позволяет ограничить использование платформы, установив ежедневной квоты на использование в секундах гигабайт. После достижения hello ежедневной квоты на использование функции приложение hello остановлена. Функции приложения, остановлена в результате достижения hello тратит квоты можно будет снова включить из hello же контексте, что установление hello ежедневно тратит квоты. В разделе hello [функции Azure странице цен](http://azure.microsoft.com/pricing/details/functions/) подробные сведения о счете.   

## <a name="platform-features-tab"></a>Вкладка функций платформы

![Вкладка функций платформы для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Функции приложения выполняются и поддерживаются платформой hello службе приложений Azure. Таким образом ваши функции приложения имеют доступ toomost функции hello Azure core платформу веб-хостинга. Hello **возможности платформы** вкладка — где доступ hello многие функции платформы службы приложений, можно использовать в приложениях функции hello. 

> [!NOTE]
> Не все функции службы приложений доступны при запуске приложения функции для плана размещения потребления hello.

Hello остальной части этого раздела основное внимание уделяется hello следующие функции службы приложений в hello портал Azure, которые удобно использовать для функции:

+ [Редактор службы приложений](#editor)
+ [Параметры приложения](#settings) 
+ [Console](#console)
+ [Дополнительные инструменты (Kudu)](#kudu)
+ [Варианты развертывания](#deployment)
+ [CORS](#cors)
+ [Аутентификация](#auth)
+ [Определение интерфейса API](#swagger)

Дополнительные сведения о том, как toowork с параметрами приложения службы в разделе [настройки параметров службы приложения Azure](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Редактор службы приложений

| | |
|-|-|
| ![Редактор службы приложений для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Редактор служб приложения Hello является расширенный редактор через портал можно использовать toomodify JSON-файлов конфигурации и файлы кода одинаково. При выборе этого параметра откроется отдельная вкладка браузера с базовым редактором. Это позволяет toointegrate с Git hello репозитория, выполнения и отладки кода, а также изменить параметры функции приложения. Этот редактор предоставляет расширенные возможности разработки среду для функций по сравнению с колонкой приложения функции по умолчанию hello.    |

![Редактор служб приложения Hello](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Параметры приложения

| | |
|-|-|
| ![Параметры приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Службы приложений Hello **параметры приложения** колонка находится где требуется настроить и управлять версии framework, удаленная отладка, параметры приложения и строки подключения. При интеграции приложения-функции с Azure и сторонними службами соответствующие параметры можно изменить здесь. |

![Настройка параметров приложения](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Консоль

| | |
|-|-|
| ![Функция консоли приложения hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | консоль Hello в портал является средством идеальный разработчика при желании toointeract вместе с приложением функцию из командной строки hello. Стандартные команды включают создание каталогов и файлов и навигацию по ним, а также выполнение пакетных файлов и сценариев. |

![Консоль приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Дополнительные инструменты (Kudu)

| | |
|-|-|
| ![Функции приложения Kudu в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Hello мощные средства для службы приложений (также известный как Kudu) предоставляют доступ tooadvanced административные функции, функции приложения. С помощью Kudu можно управлять системными сведениями, параметрами приложения, переменными среды, заголовками HTTP и переменными сервера. Можно также запустить **Kudu** путем просмотра toohello конечную точку SCM для функции приложения, например`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Настройка Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Варианты развертывания

| | |
|-|-|
| ![Функция варианты развертывания приложений в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Компонент функции позволяет разрабатывать код функций на локальном компьютере. Затем вы можете передать tooAzure проекта приложения вашей локальной функции. В дополнение к этому tootraditional передачи FTP, функции позволяет развертывать с помощью решений популярных непрерывная интеграция, как GitHub, VSTS, Dropbox, Bitbucket и другие функции приложения. Дополнительные сведения см. в статье [Непрерывное развертывание для функций Azure](functions-continuous-deployment.md). tooupload вручную с помощью FTP или local Git, вы также должны [настроить учетные данные развертывания](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Функции приложения CORS в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | tooprevent выполнения вредоносного кода в службах, блоки службы приложений вызывает tooyour приложений-функций из внешних источников. Функции поддерживает ресурсов независимо от источника (CORS) toolet определяют «список» допускается источников, из которых функций может принимать удаленные запросы для управления доступом.  |

![Настройка CORS приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Проверка подлинности

| | |
|-|-|
| ![Проверка подлинности приложения функции в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Если функции используют триггер HTTP, можно потребовать, чтобы вызовы toofirst пройти проверку подлинности. Служба приложений поддерживает проверку подлинности Azure Active Directory и вход в систему с помощью поставщиков социальных сетей, таких как Facebook, Майкрософт и Twitter. Дополнительные сведения о настройке определенных поставщиков аутентификации см. в разделе [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md). |

![Настройка проверки подлинности для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Определение интерфейса API

| | |
|-|-|
| ![Функция API приложения swagger определения в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Функции поддерживает Swagger toomore tooallow клиентам возможность использования функции активации HTTP. Дополнительные сведения о создании определений API с помощью Swagger см. в статье [Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure](../app-service-api/app-service-api-dotnet-get-started.md). Также можно использовать функции прокси-серверы toodefine одну область API для нескольких функций. Дополнительные сведения см. в статье [Работа с прокси-серверами для функций Azure](functions-proxies.md). |

![Настройка API приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Дальнейшие действия

+ [Настройка параметров службы приложений Azure](../app-service-web/web-sites-configure.md)
+ [Непрерывное развертывание для функций Azure](functions-continuous-deployment.md)



