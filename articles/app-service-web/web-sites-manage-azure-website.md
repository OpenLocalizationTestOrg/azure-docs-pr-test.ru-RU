---
title: "aaaManage веб-приложения в службе приложений Azure"
description: "Tooresources ссылки для управления веб-приложения в службе приложений Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Управление веб-приложением в службе приложений Azure
В этом разделе содержатся ссылки tooresources для управления веб-приложения в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Управление включает в себя все задачи hello, сохранить бесперебойной работы веб-приложения. 

За время жизни hello веб-приложения будет выполнять задачи управления при перемещении от операции toonormal первоначального развертывания, обслуживания и обновления.

Многие веб-приложения управления задачи могут выполняться в hello портала Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Перед развертыванием вашей tooproduction web app
### <a name="choose-a-tier"></a>Выберите уровень.
Служба приложений Azure доступна для 5 уровней: Free, Shared, Basic, Standard и Premium. Сведения о функции hello и цен для каждого уровня см. в разделе [сведения о ценах](https://azure.microsoft.com/pricing/details/app-service/). 

* [Планы служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) позволяют группировать несколько веб-приложений в группе hello того же уровня.
* Всегда можно [сменить уровень](web-sites-scale.md) после создания веб-приложения.

### <a name="configuration"></a>Конфигурация
Используйте hello [портала Azure](https://portal.azure.com/) tooset различные параметры конфигурации. Подробные сведения см. в разделе [Настройка веб-приложений в службе приложений Azure](web-sites-configure.md). Вот краткий контрольный список:

* При необходимости выберите **версии сред выполнения** для .NET, PHP, Java или Python.
* Включить **WebSockets** Если веб-приложение использует протокол WebSocket hello. (Это относится к приложениям, которые используют [ASP.NET SignalR](http://www.asp.net/signalr) или [socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Вы используете непрерывные веб-задания? Если да, то выберите параметр **Always On**(Всегда включено).
* Набор hello **документ по умолчанию**, такие как index.html.

Добавление toothese базовые параметры конфигурации вы можете tooconfigure hello следующее:

* Шифрование **SSL**. toouse SSL с именем пользовательского домена, необходимо получить SSL сертификатов и настройка вашей toouse web app его. Ознакомьтесь со статьей [Включение протокола HTTPS для веб-приложения в службе приложений Azure](app-service-web-tutorial-custom-ssl.md).
* **Имя личного домена**. Вашему веб-приложению автоматически присваивается дочерний домен в azurewebsites.net. Вы можете связать сайт с пользовательским доменным именем, например contoso.com. Ознакомьтесь со статьей [Настройка личного доменного имени для службы приложений Azure](app-service-web-tutorial-custom-domain.md).

Настройка для определенных языков программирования:

* **PHP**: статья [Настройка PHP в веб-приложениях службы приложений Azure](web-sites-php-configure.md).
* **Python**: статья [Настройка Python в веб-приложениях службы приложений Azure](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>В ходе эксплуатации веб-приложения
Во время веб-приложения необходимо убедиться, что он доступен и является toomeet пользовательский трафик toomake. Может также потребоваться tootroubleshoot ошибок.

### <a name="monitoring"></a>Мониторинг
* Через hello портал Azure, вы можете [добавить метрики производительности](web-sites-monitor.md) как ЦП и число запросов клиентов.
* [Масштабирование веб-приложения](web-sites-scale.md) в tootraffic ответа. В зависимости от вашего уровня можно масштабировать число hello виртуальных машин и размер hello hello экземпляров виртуальных Машин. В hello Standard и Premium уровней вы можно также настроить автоматическое масштабирование, поэтому веб-приложения автоматически масштабируется по фиксированному расписанию или в ответ tooload.  

### <a name="backups"></a>Резервные копии
* Настройка [автоматизированной архивации](web-sites-backup.md) для веб-приложения. Дополнительные сведения об архивации см. в [этом видео](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Сведения о способах hello [восстановление базы данных](../sql-database/sql-database-business-continuity.md) в базе данных SQL Azure.

### <a name="troubleshooting"></a>Устранение неполадок
* Если что-то пойдет не так, вы можете [Устранение неполадок в Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), с помощью журналов диагностики и отладки в облаке hello. 
* За пределами Visual Studio существуют различные способы журналы диагностики toocollect. Ознакомьтесь со статьей [Включение ведения журнала диагностики для веб-приложений в службе приложений Azure](web-sites-enable-diagnostic-log.md).
* Для приложений Node.js. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Восстановление данных
* [восстанавливать](web-sites-restore.md) из ранее созданных резервных копий.

## <a name="when-you-update-your-web-app"></a>При обновлении веб-приложения
Если вы не включили автоматическое резервное копирование, то можете создавать резервные копии [вручную](web-sites-backup.md).

Возможно, вас также заинтересует [промежуточное развертывание](web-sites-staged-publishing.md). Этот параметр позволяет публиковать обновления tooa промежуточное развертывание запускаемую side-by-side с производственного развертывания. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


