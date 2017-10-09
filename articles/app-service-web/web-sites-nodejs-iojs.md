---
title: "io.js toouse aaaHow с веб-приложениях службы приложений Azure"
description: "Узнайте, как веб-приложения в службе приложений Azure с io.js toouse."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Как io.js toouse с веб-приложениях службы приложений Azure
Популярные узел ветвления Hello [io.js] функции проекта Node.js различные tooJoyent различия, включая более откройте модель управления, быстрее цикл выпуска и быстрее внедрения новых и экспериментальный функций JavaScript.

Несмотря на то, что для веб-приложений [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) имеется достаточно много предустановленных версий Node.js, существует возможность использовать двоичный файл Node.js, предоставляемый пользователями. В этой статье описываются два способа, применение hello io.js в веб-приложениях службы приложений: hello использования расширенного развертывания сценария, который автоматически настраивает последнюю версию доступных io.js Azure toouse hello, а также отправки вручную hello io.js двоичного файла. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Использование скрипта развертывания.
При развертывании приложения Node.js приложение службы веб-приложения выполняется ряд небольших команды tooensure, hello среде правильно настроена. С помощью скрипта развертывания, этот процесс может быть настроенный tooinclude hello загрузки и конфигурации io.js.

Hello [io.js скрипт развертывания](https://github.com/felixrieseberg/iojs-azure) можно найти в GitHub. io.js tooenable на веб-приложения, просто скопируйте **.deployment**, **deploy.cmd** и **IISNode.yml** toohello корневой папке приложения и развертывать приложения tooWeb.  

Первый файл Hello, **.deployment**, указывает, что веб-приложений toorun **deploy.cmd** после развертывания. Этот скрипт выполняется все обычные действия приветствия для Node.js приложения, но также загружает последнюю версию io.js hello. Наконец **IISNode.yml** настраивает веб-приложений toouse просто hello загружены io.js двоичных вместо предустановленных двоичный файл Node.js.

> [!NOTE]
> tooupdate hello используется двоичный файл io.js, просто повторите развертывание приложения — hello скрипт загрузит новую версию io.js развертывания каждое приложение hello один раз.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Использование ручной установки
Ручная установка версии пользовательских io.js Hello включает только два этапа. Сначала загрузите hello **win x64** двоичных непосредственно из hello [io.js распространения]. Требуются два файла, **iojs.exe** и **iojs.lib**. Сохранить обе папки с файлами tooa внутри веб-приложения, например в **bin/iojs**.

toouse веб-приложений tooconfigure **iojs.exe** вместо предварительно установленную версию узла, создайте **IISNode.yml** в корневом каталоге приложения hello и добавьте следующей строкой hello.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как указано io.js toouse для приложения службы веб-приложений, с помощью скриптов развертывания, а также установка вручную. 

> [!NOTE]
> Платформа io.js продолжает усиленно разрабатываться и обновляется чаще чем Node.js. Ряд модулей Node.js может не работать с платформой io.js. Для устранения неполадок обратитесь к материалам по платформе [io.js на сайте GitHub].
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

[io.js]: https://iojs.org
[io.js распространения]: https://iojs.org/dist/
[io.js на сайте GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
