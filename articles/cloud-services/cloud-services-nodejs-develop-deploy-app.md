---
title: "руководство по началу aaaNode.js работы | Документы Microsoft"
description: "Узнайте, как toocreate простой Node.js веб-приложение и развернуть ее tooan облачной службы Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Построение и развертывание tooan приложений Node.js облачной службы Azure

В этом учебнике показано как toocreate простой Node.js приложение, работающее в облачной службе Azure. Облачные службы являются стандартными блоками hello масштабируемых облачных приложений в Azure. Они позволяют независимых управление и разделение hello и масштабное развертывание служб переднего плана и внутренними компонентами приложения.  Облачные службы предоставляют надежную выделенную виртуальную машину для надежного размещения каждой роли.

Дополнительные сведения о облачных служб и их сравнение tooAzure веб-сайтов и виртуальных машин см. в разделе [веб-сайтов Azure, облачных служб и виртуальных машин сравнения].

> [!TIP]
> Ищете простой веб-сайт toobuild? Если в вашем сценарии задействован простой интерфейс веб-сайта, мы рекомендуем [использовать упрощенное веб-приложение]. Легко можно обновить tooa облачной службы как роста веб-приложения и изменения требований.

Руководствуясь этим учебником, вы соберете простое веб-приложение, размещенное в веб-роли. Будет использовать ваше приложение tootest эмулятор вычислений hello локально, а затем развернуть его с помощью средства командной строки PowerShell.

приложение Hello представляет простое приложение «hello world»:

![Веб-браузер, отображение веб-страницы Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Предварительные требования
> [!NOTE]
> В этом учебнике используется Azure PowerShell, для которого требуется операционная система Windows.

* Установите и настройте [Azure PowerShell].
* Загрузите и установите hello [пакет Azure SDK для .NET 2.7]. Выберите, в hello запустите программу установки.
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Создание проекта облачной службы Azure
Выполните следующие задачи toocreate новый проект облачной службы Azure, наряду с basic Node.js формирование шаблонов hello.

1. Запустите **Windows PowerShell** от имени администратора, от hello **меню "Пуск"** или **рабочий стол**, поиск **Windows PowerShell**.
2. [Подключение PowerShell] tooyour подписки.
3. Введите hello после проекта hello toocreate toocreate командлета PowerShell:

        New-AzureServiceProject helloworld

    ![результат команды New-AzureService hello helloworld Hello][hello result of hello New-AzureService helloworld command]

    Hello **New AzureServiceProject** командлет создает базовую структуру для публикации tooa приложений Node.js облачной службы. Он содержит файлы конфигурации, необходимые для публикации tooAzure. Hello также изменяет каталог toohello рабочий каталог для службы hello.

    Hello создает hello следующие файлы:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** и **ServiceDefinition.csdef** — специальные файлы Azure, необходимые для публикации приложения. См. [общие сведения о создании размещенной службы для Azure].
   * **deploymentSettings.json**: сохраняет локальные параметры, используемые hello Azure PowerShell командлеты развертывания.
4. Введите hello, следующая команда tooadd новый веб-роли:

       Add-AzureNodeWebRole

   ![выходные данные команды Add-AzureNodeWebRole hello Hello][hello output of hello Add-AzureNodeWebRole command]

   Hello **Add-AzureNodeWebRole** командлет создает простое приложение Node.js. Он также изменяет hello **.csfg** и **.csdef** файлы tooadd записи конфигурации для новой роли hello.

   > [!NOTE]
   > Если имя роли не указано, используется имя по умолчанию. Можно ввести имя в качестве первого параметра командлета hello:`Add-AzureNodeWebRole MyRole`

приложение Hello Node.js определяется в файле hello **server.js**, расположенного в каталоге hello hello веб-роли (**WebRole1** по умолчанию). Ниже приведен код hello.

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Данный пример кода является по сути hello образец так же, как Здравствуйте, «Hello World» на hello [nodejs.org] веб-сайта, за исключением того, он использует hello номер порта, присвоенный hello облачной среде.

## <a name="deploy-hello-application-tooazure"></a>Развертывание tooAzure приложения hello

> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Вы можете [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) или [зарегистрироваться для получения бесплатной версии](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Загрузите hello Azure параметры публикации
toodeploy tooAzure вашего приложения, необходимо сначала загрузить hello публикации параметров для подписки Azure.

1. Выполните следующий командлет Azure PowerShell hello.

       Get-AzurePublishSettingsFile

   Это будет использоваться браузер toonavigate toohello страница загрузки параметров публикации. Возможно, запрошенные toolog учетную запись Майкрософт. В этом случае используйте hello учетную запись, связанную с подпиской Azure.

   Сохраните расположение файла tooa профиля загружаются hello может легко получить доступ.
2. Выполните следующий командлет tooimport hello профиль, который вы загрузили публикации:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > После импорта hello параметры публикации, рассмотрите возможность удаления hello загрузки файла PUBLISHSETTINGS, так как он содержит сведения, которые может разрешить другому tooaccess вашей учетной записи.

### <a name="publish-hello-application"></a>Публикация приложения hello
toopublish запуска hello, следующие команды:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** указывает имя hello для развертывания hello. Это должно быть уникальное имя, в противном случае hello публикации процесс завершится ошибкой. Hello **Get-Date** вещам командной строки даты и времени, следует сделать hello имя уникальным.
* **-Location** указывает hello центра обработки данных, который будет размещаться приложение hello в. Список доступных центров обработки данных, используйте hello toosee **Get AzureLocation** командлета.
* **-Запуск** открывает окно браузера и переходит по ним toohello размещенной службы после завершения развертывания.

После успешной публикации появится ответ аналогичные toohello следующее:

![выходные данные Hello hello команда Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Он может toodeploy приложения hello через несколько минут и становятся доступными при первой публикации.

После завершения развертывания hello окно браузера откройте и перехода toohello облачной службы.

![Окно браузера, отображение hello hello world страницы; URL-адрес Hello указывает, что страница hello размещается в Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Теперь приложение работает в Azure.

Hello **AzureServiceProject публикации** командлет выполняет следующие шаги hello:

1. Создает toodeploy пакета. Hello пакет содержит все файлы hello в папке приложения.
2. Создайте новую **учетную запись хранения** , если она не существует. Hello учетной записи хранилища Azure — пакет приложения hello toostore используется во время развертывания. После завершения развертывания можно безопасно удалить учетную запись хранения hello.
3. При необходимости создайте **облачную службу**. Объект **облачная служба** hello контейнер, в котором размещается приложение при развернутой tooAzure. См. [общие сведения о создании размещенной службы для Azure].
4. Публикует tooAzure пакета развертывания hello.

## <a name="stopping-and-deleting-your-application"></a>Остановка и удаление приложения
После развертывания приложения, вы можете toodisable его, чтобы избежать дополнительных расходов. Для экземпляров веб-роли Azure выставляет счета за почасовое использование серверного времени. После развертывания приложения даже в том случае, если экземпляры hello не запущены и находятся в состоянии остановки hello потребляются времени сервера.

1. В окне приветствия Windows PowerShell Остановите развертывание службы hello, созданным в предыдущем разделе hello, hello, выполнив командлет:

       Stop-AzureService

   Остановка службы hello может занять несколько минут. При остановке службы hello, появляется сообщение о том, что он был остановлен.

   ![состояние Hello команды Stop-AzureService hello][hello status of hello Stop-AzureService command]
2. Служба toodelete hello, вызов hello, выполнив командлет:

       Remove-AzureService

   При появлении запроса введите **Y** toodelete hello службы.

   Удаление службы hello может занять несколько минут. После удаления службы hello появится сообщение, указывающее на то, что служба hello была удалена.

   ![состояние Hello команды Remove-AzureService hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Удаление службы hello не удаляет hello учетной записи хранилища, который был создан при первоначальной публикации службы hello и будет выставлен счет за хранилище, используемое toobe. Если ничего не используют хранилище hello, вы можете toodelete его.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика Node.js].

<!-- URL List -->

[веб-сайтов Azure, облачных служб и виртуальных машин сравнения]: ../app-service-web/choose-web-site-cloud-service-vm.md
[использовать упрощенное веб-приложение]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[пакет Azure SDK для .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Подключение PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[общие сведения о создании размещенной службы для Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Центр разработчика Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
