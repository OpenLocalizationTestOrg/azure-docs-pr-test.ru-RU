---
title: "aaaAccess локальных ресурсов с помощью гибридных подключений в службе приложений Azure"
description: "Создание подключения между веб-приложением в службе приложений Azure и локальным ресурсом, который использует статический TCP-порт."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure
Вы можете подключиться к службе приложений Azure приложение tooany локальных ресурсов, использующих статического TCP-порта, например SQL Server, MySQL, HTTP веб-API и большинство пользовательских веб-служб. В этой статье показано, как toocreate гибридного подключения между службой приложения и локальная база данных SQL Server.

> [!NOTE]
> часть функции hello гибридные подключения веб-приложения Hello доступен только в hello [портала Azure](https://portal.azure.com). toocreate соединений в службах BizTalk. в разделе [гибридные подключения](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Это содержимое также применяется tooMobile приложений в службе приложений Azure. 
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Бесплатную подписку можно найти на сайте [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
* toouse в локальной среде SQL Server или SQL Server, экспресс-выпуск базы данных с помощью гибридного подключения, TCP/IP должен toobe, включена ли статический порт. Мы рекомендуем использовать экземпляр SQL Server по умолчанию, так как он использует статический порт 1433. Сведения об установке и настройке SQL Server Express для использования с гибридных подключений см. в разделе [tooan подключение локального SQL Server с веб-сайта Azure, с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979).
* Hello компьютер, на котором устанавливается hello локальный диспетчер гибридного подключения агента описано далее в этой статье:
  
  * Должна быть tooAzure tooconnect доступ через порт 5671
  * Должен быть hello может tooreach *hostname*:*Номер_порта* локального ресурса. 

> [!NOTE]
> Hello в этой статье предполагается, что вы используете браузер hello hello компьютере, где будет размещаться агент hello локальной гибридных подключений.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Создание веб-приложения в hello портала Azure
> [!NOTE]
> Если вы уже создали веб-приложения или внутреннего сервера мобильного приложения в портале Azure, что в этом учебнике требуется toouse hello, можно сразу перейти слишком[создать гибридное подключение и служба BizTalk](#CreateHC) и начать с него.
> 
> 

1. В верхнем левом углу hello hello [портала Azure](https://portal.azure.com), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.
   
    ![Создание веб-приложения][NewWebsite]
2. На hello **веб-приложения** колонки, укажите URL-адрес и нажмите кнопку **создать**. 
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. Через несколько секунд hello веб-приложения создается и отображается колонке web app. Hello колонка предназначена поддерживающим вертикальную прокрутку, позволяющий управлять веб-узла.
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
4. tooverify hello сайт будет динамически, можно нажать hello **Обзор** страница по умолчанию hello toodisplay значок.
   
    ![Нажмите кнопку обзора toosee веб-приложения][Browse]
   
    ![Страница веб-приложения по умолчанию][DefaultWebSitePage]

Затем вы создадите гибридного подключения и служба BizTalk для веб-приложения hello.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Создание гибридного подключения и службы BizTalk
1. В своей колонке веб-приложения щелкните **Все настройки** > **Сеть** > **Настройка конечных точек гибридного подключения**.
   
    ![Гибридные подключения][CreateHCHCIcon]
2. В колонке подключений гибридного hello, нажмите кнопку **добавить**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Hello **добавить гибридное подключение** открывает колонку.  Здравствуйте, так как это ваш первый гибридного подключения **гибридное подключение** параметр выбран, а hello **создать гибридное подключение** колонке открывает для вас.
   
    ![Создание гибридного подключения][TwinCreateHCBlades]
   
    На hello **создать гибридное подключение колонке**:
   
   * Для **имя**, введите имя для соединения hello.
   * Для **Hostname**, введите имя hello hello на локальном компьютере, на котором находится ресурс.
   * Для **порт**, введите номер порта hello, что локальный ресурс использует (1433 для экземпляра SQL Server по умолчанию).
   * Щелкните кнопку **Служба BizTalk**
4. Hello **Создание службы BizTalk** открывает колонку. Введите имя для службы BizTalk hello и нажмите кнопку **ОК**.
   
    ![Создание службы BizTalk][CreateHCCreateBTS]
   
    Hello **Создание службы BizTalk** закрывает колонки и возвращаются toohello **создать гибридное подключение** колонку.
5. В колонке hello создать гибридные подключения выберите **ОК**. 
   
    ![Нажмите кнопку "ОК"][CreateBTScomplete]
6. После завершения процесса hello область уведомлений hello в hello портала о том, успешно созданы подключение hello.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. В колонке hello веб-приложения hello **гибридных подключений** значок теперь отображает создания 1 гибридного подключения.
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

На этом этапе вы прошли важной частью гибридного подключения hello облачной инфраструктуры. Далее вы создадите соответствующую локальную часть.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Установка подключения к hello toocomplete hello локальный диспетчер гибридного подключения
1. В колонке hello веб-приложение, нажмите кнопку **все параметры** > **сети** > **настроить конечные точки гибридного подключения**. 
   
    ![Значок «Гибридные подключения»][HCIcon]
2. На hello **гибридных подключений** колонки, hello **состояние** столбца для hello недавно был добавлен конечной точки показывает **не подключен**. Нажмите кнопку подключения tooconfigure hello его.
   
    ![Не подключено][NotConnected]
   
    Открывает колонку подключения гибридного Hello.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. В колонке hello щелкните **установки прослушивателя**.
   
    ![Щелкните «Установка прослушивателя»][ClickListenerSetup]
4. Hello **свойства гибридного подключения** открывает колонку. В разделе **на локальный диспетчер гибридного подключения**, выберите **щелкните здесь tooinstall**.
   
    ![Щелкните здесь tooinstall][ClickToInstallHCM]
5. В hello запуска приложения безопасности диалоговое окно предупреждения, выберите **запуска** toocontinue.
   
    ![Выберите toocontinue выполнения][ApplicationRunWarning]
6. В hello **контроль учетных записей пользователей** диалоговое окно, выберите **Да**.
   
   ![Щелкните «Да»][UAC]
7. Hello диспетчер гибридного подключения загружается и устанавливается автоматически. 
   
    ![Установка][HCMInstalling]
8. После завершения установки hello, нажмите кнопку **закрыть**.
   
    ![Щелкните кнопку «Закрыть»][HCMInstallComplete]
   
    На hello **гибридных подключений** колонки, hello **состояние** столбец теперь показывает **подключен**. 
   
    ![Состояние «Подключено»][HCStatusConnected]

Стало ИТ-инфраструктуры hello гибридного подключения можно создать гибридное приложение, которое использует его. 

> [!NOTE]
> Hello следующих разделах показано, как toouse гибридные подключения с серверного проекта .NET мобильных приложений.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Настройка hello мобильного приложения .NET серверной части проекта tooconnect toohello базы данных SQL Server
В службе приложений проект серверной части мобильного приложения .NET — это просто веб-приложение ASP.NET с установленным и инициализированным дополнительным пакетом SDK для мобильных приложений. toouse веб-приложения в качестве серверной части мобильных приложений, необходимо [загрузки и инициализации серверной части мобильных приложений .NET hello SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Для мобильных приложений также необходимые toodefine строку подключения для базы данных в локальной среде hello и изменения toouse hello серверной части этого соединения. 

1. В обозревателе решений в Visual Studio, откройте hello файл Web.config для серверной части мобильных приложений .NET, найдите hello **connectionStrings** добавьте новую запись SqlClient следующего вида hello, какие точки toohello локального SQL База данных сервера:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Помните, tooreplace `<**secure_password**>` в данной строке с hello пароль, созданный для *HybridConnectionLogin*.
2. Нажмите кнопку **Сохранить** в файле Web.config hello toosave Visual Studio.
   
   > [!NOTE]
   > Этот параметр для подключения используется при выполнении на локальном компьютере hello. При работе в Azure, этот параметр является переопределен аргументом параметр подключения hello, определенный в портал hello.
   > 
   > 
3. Разверните hello **моделей** папку и файл модели данных откройте hello, который заканчивается на *Context.cs*.
4. Изменение hello **DbContext** toopass конструктор экземпляра hello значение `OnPremisesDBConnection` toohello базового **DbContext** конструктор, аналогичные toohello следующий фрагмент кода:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    Hello теперь использует hello нового подключения toohello базы данных SQL Server.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Обновление локальной строки подключения внутреннего toouse hello мобильное приложение hello
Далее необходимо tooadd Настройка приложения для этого новую строку подключения, чтобы его можно использовать из Azure.  

1. Вернитесь в hello [портал Azure](https://portal.azure.com) hello кода веб-приложения серверной части для мобильного приложения, щелкните **все параметры**, затем **параметры приложения**.
2. В hello **веб-параметров приложения** колонки, прокрутите вниз слишком**строки подключения** и добавьте новый **SQL Server** строку подключения с именем `OnPremisesDBConnection` значение типа `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Замените `<**secure_password**>` с hello надежный пароль для локальной базы данных.
   
    ![Строка подключения для локальной базы данных](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Нажмите клавишу **Сохранить** toosave hello гибридного подключения и строкой подключения только что создали.

На этом этапе можно повторно опубликовать проект сервера hello и протестировать hello новое соединение с существующие клиенты мобильные приложения. Данные будут считываются и записываются toohello локальной базы данных с помощью hello гибридного подключения.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о создании веб-приложение ASP.NET, который использует гибридного подключения см. в разделе [tooan подключение локального SQL Server с веб-сайта Azure, с помощью гибридных подключений](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Дополнительные ресурсы
[Обзор гибридных подключений](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Веб-сайт гибридных подключений](https://azure.microsoft.com/services/biztalk-services/)

[Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Подключение tooan локального SQL Server из мобильных служб Azure с помощью гибридных подключений (видео на канале 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
