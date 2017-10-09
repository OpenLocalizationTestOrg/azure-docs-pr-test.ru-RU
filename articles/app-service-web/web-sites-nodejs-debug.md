---
title: "aaaHow toodebug Node.js веб-приложения в службе приложений Azure"
description: "Узнайте, как toodebug Node.js веб-приложения в службе приложений Azure."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Как toodebug Node.js веб-приложения в службе приложений Azure
Azure предоставляет tooassist встроенных средств диагностики с отладкой приложений Node.js, размещенных в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) веб-приложений. В этой статье вы узнаете, как ведение журнала tooenable stdout и stderr, сведения об ошибках отображения в браузере hello и как toodownload и просмотр файлов журнала.

Диагностика приложений Node.js, размещенных в Azure, обеспечивается [IISNode]. Хотя в этой статье рассматриваются наиболее распространенные параметры hello для сбора данных диагностики, он не предоставляет полный Справочник по работе с IISNode. Дополнительные сведения о работе с IISNode см. в разделе hello [IISNode Readme] на GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Включение ведения журналов
По умолчанию веб-приложения службы приложений записывают только диагностические сведения о развертывании, например при развертывании веб-приложения с использованием Git. Эта информация полезна при возникновении проблем во время развертывания, таких как сбой при установке модуля, на который ссылается файл **package.json**, или при использовании пользовательских сценариев развертывания.

tooenable hello при ведении журнала потоки stdout и stderr, необходимо создать **IISNode.yml** hello корневого каталога приложения Node.js и добавьте следующее hello:

    loggingEnabled: true

Это позволяет ведения журнала hello stderr и stdout из приложения Node.js.

Hello **IISNode.yml** файл также можно использовать toocontrol ли понятные ошибки или ошибки разработчика возвращаются toohello браузера при возникновении сбоя. ошибки tooenable разработчика, добавьте следующие строки toohello hello **IISNode.yml** файла:

    devErrorsEnabled: true

Этот параметр включен, IISNode будет выполнен возврат hello последние 64 КБ данных, отправляемых toostderr вместо сообщением об ошибке, такие как «произошла внутренняя ошибка сервера».

> [!NOTE]
> DevErrorsEnabled полезен при диагностике проблем во время разработки, включение его в рабочей среде может привести к ошибкам разработки, отправляемых пользователям tooend.
> 
> 

Если hello **IISNode.yml** файл не существовал в приложении, необходимо перезапустить веб-приложения после публикации приложения hello обновлены. При простом изменении настроек в существующем файле **IISNode.yml** , который ранее был опубликован, перезагрузка не требуется.

> [!NOTE]
> Если веб-приложения был создан с помощью средства командной строки hello Azure или командлеты PowerShell для Azure, значение по умолчанию **IISNode.yml** файл создается автоматически.
> 
> 

toorestart hello веб-приложения, веб-приложения выберите hello в hello [портала Azure](https://portal.azure.com), а затем нажмите кнопку **ПЕРЕЗАПУСТИТЕ** кнопки:

![кнопка перезагрузки][restart-button]

Если средства командной строки Azure hello установлены в среде разработки, можно использовать следующие команды toorestart hello веб-приложения hello:

    azure site restart [sitename]

> [!NOTE]
> Хотя loggingEnabled и devErrorsEnabled, параметры конфигурации IISNode.yml hello чаще всего используется для сбора диагностических сведений, IISNode.yml может быть tooconfigure используется ряд параметров для выбранной среды размещения. Полный список параметров конфигурации hello см. в разделе hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) файла.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Доступ к журналам
Журналы диагностики может осуществляться тремя способами; С помощью hello передачи файлов Protocol (FTP), загрузка ZIP-архив, или как активный обновляются потока журнала hello (также известного как заключительный фрагмент). Загрузка ZIP-архив hello hello файлов журнала или просмотр потоковой трансляции hello требуют hello Azure программы командной строки. Их можно устанавливать с помощью hello следующую команду:

    npm install azure-cli -g

После установки средств hello может осуществляться с помощью команды «azure» hello. Здравствуйте, средства командной строки, сначала должны быть настроенный toouse подписки Azure. Сведения о том, как tooaccomplish это задача см. в разделе hello **как toodownload и импорт параметров публикации** раздел hello [как tooUse hello средства командной строки Azure](../xplat-cli-connect.md) статьи.

### <a name="ftp"></a>FTP
tooaccess hello диагностических сведений по протоколу FTP, посетите hello [портала Azure](https://portal.azure.com), выберите веб-приложения, а затем выберите hello **МОНИТОРИНГА**. В hello **быстрые ссылки** статьи, hello **ЖУРНАЛЫ диагностики FTP** и **ЖУРНАЛЫ диагностики FTPS** ссылкам toohello журналы событий с помощью протокола hello FTP.

> [!NOTE]
> Если вы не настроили ранее имя пользователя и пароль для FTP или развертывание, это можно сделать из hello **краткое руководство** управления страницы, выбрав **настроить учетные данные развертывания**.
> 
> 

Hello URL-адрес FTP, возвращаются в панели мониторинга hello предназначен для hello **LogFiles** каталог, который будет содержать следующие вложенные каталоги hello:

* [Метод развертывания](web-sites-deploy.md) -при использовании метода развертывания, например Git каталог hello таким же именем будет создана и содержит сведения, связанные с toodeployments.
* nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.

### <a name="zip-archive"></a>ZIP-архив
toodownload ZIP-архив hello диагностических журналов, hello используйте следующую команду из командной строки средства hello Azure:

    azure site log download [sitename]

Будет загружен **diagnostics.zip** в текущем каталоге hello. Этот архив содержит hello следующая структура каталогов:

* deployments — журнал сведений о развертываниях вашего приложения.
* LogFiles
  
  * [Метод развертывания](web-sites-deploy.md) -при использовании метода развертывания, например Git каталог hello таким же именем будет создана и содержит сведения, связанные с toodeployments.
  * nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.

### <a name="live-stream-tail"></a>Поток в реальном времени (заключительный фрагмент)
tooview обновляющегося потока данных журнала диагностики, hello используйте следующую команду из командной строки средства hello Azure:

    azure site log tail [sitename]

Возвращает поток событий журнала, которые обновляются по мере их появления на сервере hello. Этот поток будет возвращать сведения о развертывании, а также сведения stdout и stderr (если параметр loggingEnabled имеет значение true).

<a id="nextsteps"></a>

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как tooenable и доступа диагностическую информацию по Azure. Хотя эта информация полезна в основные сведения о возникающих проблем с приложением, он может ссылаться неполадки tooa модуль, который вы используете или этой версии hello Node.js, используемые веб-приложений служб приложений отличается от hello календарем, используемым в развертывании Среда.

Сведения по работе с модулями Azure см. в разделе [Использование модулей Node.js с приложениями Azure](../nodejs-use-node-modules-azure-apps.md).

Сведения об определении версии Node.js для своего приложения см. в разделе [Установка версии Node.js в приложении Azure].

Дополнительные сведения см. также: hello [Центр разработчика Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Установка версии Node.js в приложении Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

