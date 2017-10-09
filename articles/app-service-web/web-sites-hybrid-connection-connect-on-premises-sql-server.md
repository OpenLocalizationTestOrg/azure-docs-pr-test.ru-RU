---
title: "aaaConnect tooon локальный SQL Server из веб-приложения в службе приложений Azure с помощью гибридных подключений"
description: "Создание веб-приложения в Microsoft Azure и подключите его tooan базы данных SQL Server в локальной среде"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Подключение локальной tooon SQL Server из веб-приложения в службе приложений Azure с помощью гибридных подключений
Гибридные подключения могут подключаться [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) ресурсов tooon локальный веб-приложения, используется ли статический порт TCP. Поддерживаются такие ресурсы: Microsoft SQL Server, MySQL, веб-API HTTP, служба приложений и большинство настраиваемых веб-служб.

В этом учебнике вы узнаете, как приложение в hello веб-службы приложения toocreate [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715), подключение hello web приложения tooyour локальной базы данных SQL Server с помощью новой функции гибридного подключения hello, создания простого ASP.NET приложение, которое будет использовать hello гибридного подключения и развертывать приложения hello toohello веб-приложения служб приложений. Hello завершения веб-приложения в Azure хранит учетные данные пользователя в базе данных членства, расположенном на локальном компьютере. Hello учебником нет опыта работы с Azure или ASP.NET.

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> часть функции hello гибридные подключения веб-приложения Hello доступен только в hello [портала Azure](https://portal.azure.com). toocreate соединений в службах BizTalk. в разделе [гибридные подключения](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника вам потребуется hello следующие продукты. У всех этих продуктов есть бесплатные версии, так что можно начать разработку для Azure полностью бесплатно.

* **Подписка Azure**. Сведения о бесплатной подписке см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](/pricing/free-trial/).
* **Visual Studio 2013** -разделе бесплатную ознакомительную версию Visual Studio 2013 toodownload [загрузки Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs). Прежде чем продолжить, установите этот продукт.
* **Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1)**. Если вы используете операционную систему Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 или Windows Server 2008 R2, ее можно включить на панели управления, последовательно выбрав "Программы и компоненты", "Включение или отключение компонентов Windows". В противном случае ее можно загрузить с hello [центра загрузки Майкрософт](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express с инструментами** -Microsoft SQL Server Express для бесплатной загрузки в hello [страницу Microsoft веб-платформы, база данных](http://www.microsoft.com/web/platform/database.aspx). Выберите hello **Express** (не LocalDB) версии. Hello **Express с инструментами** версия включает SQL Server Management Studio, который будет использоваться в этом учебнике.
* **SQL Server Management Studio Express** — это входят в состав SQL Server 2014 Express hello загрузки средства было сказано выше, но при необходимости tooinstall его отдельно, можно загрузить и установить его с hello [SQL Server Express Страница загрузки](http://www.microsoft.com/web/platform/database.aspx).

Hello учебнике предполагается, что у вас есть подписка Azure, что вы установили Visual Studio 2013, и что вы установили или включить .NET Framework 3.5. Hello учебнике рассказывается о том, как tooinstall SQL Server 2014 Express в конфигурации, которая хорошо подходит для гибридных подключений hello Azure компонентов (экземпляр по умолчанию с помощью статического порта TCP). Перед началом работы с учебником hello Загрузите SQL Server 2014 Express с инструментами из папки hello, упомянутых выше, если у вас установлен SQL Server.

### <a name="notes"></a>Примечания
toouse в локальной среде SQL Server или SQL Server, экспресс-выпуск базы данных с помощью гибридного подключения, TCP/IP должен toobe, включена ли статический порт. Экземпляры SQL Server по умолчанию используют статический порт 1433, а именованные экземпляры не используют этот порт.

Hello компьютера, на котором устанавливается hello локальный диспетчер гибридного подключения агента:

* Необходимо иметь tooAzure исходящие подключения через:

| Порт | Назначение |
| --- | --- |
| 80 |**Требуется** для порта HTTP при проверке сертификатов и (необязательно) для подключения к данным. |
| 443 |**Необязательно** для подключения к данным. В случае недоступности too443 исходящие подключения используется TCP-порт 80. |
| 5671 и 9352 |**Рекомендуется** , но необязательно для подключения к данным. Обратите внимание, что в этом режиме обеспечивается более высокая пропускная способность. В случае недоступности toothese портов исходящей связи используется TCP-порт 443. |

* Должен быть hello может tooreach *hostname*:*Номер_порта* локального ресурса.

Hello в этой статье предполагается, что вы используете браузер hello hello компьютере, где будет размещаться агент hello локальной гибридных подключений.

Если уже имеется SQL Server, установленный в конфигурации и в среде, которая соответствует условиям hello, описанных выше, можно пропустить и начинаться с [создать базу данных SQL Server в локальной](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>О. Установка экспресс-выпуска SQL Server, включение TCP/IP и создание локальной базы данных SQL Server
В этом разделе показано, как включить протокол TCP/IP и создать базу данных, веб-приложение будет работать с портала Azure hello tooinstall SQL Server Express.

### <a name="install-sql-server-express"></a>Установка SQL Server Express
1. SQL Server Express, tooinstall запуска hello **SQLEXPRWT_x64_ENU.exe** или **SQLEXPR_x86_ENU.exe** загруженный файл. Откроется мастер Hello центр установки SQL Server.
   
    ![Установка SQL Server][SQLServerInstall]
2. Выберите **автономная установка нового SQL Server или добавление компонентов tooan существующей установки**. Следуйте инструкциям hello, принимающий параметры по умолчанию hello и параметры, пока не будет получен toohello **конфигурации экземпляра** страницы.
3. На hello **конфигурации экземпляра** выберите **экземпляр по умолчанию**.
   
    ![Выбор экземпляра по умолчанию][ChooseDefaultInstance]
   
    По умолчанию hello по умолчанию экземпляра SQL Server прослушивает запросы от клиентов SQL Server статический порт 1433, являющееся какие hello гибридные подключения компонента необходимо. Именованные экземпляры используют динамические порты и UDP, которые не поддерживаются гибридными подключениями.
4. Примите значения по умолчанию hello в hello **конфигурации сервера** страницы.
5. На hello **Настройка компонента Database Engine** в разделе **режим проверки подлинности**, выберите **смешанный режим (проверка подлинности SQL Server и Windows)**и укажите пароль.
   
    ![Выбор смешанного режима][ChooseMixedMode]
   
    В этом учебнике вы будете использовать проверку подлинности SQL Server. Быть убедиться, что tooremember hello пароля, так как он понадобится позже.
6. Пошагово rest hello toocomplete hello приветствия мастера установки.

### <a name="enable-tcpip"></a>Включение TCP/IP
tooenable TCP/IP, используется диспетчер конфигурации SQL Server, который был установлен при установке SQL Server Express. Следуйте указаниям hello [включить сетевой протокол TCP/IP для SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) перед продолжением.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Создание локальной базы данных SQL Server
Для веб-приложения Visual Studio требуется база данных участников, к которой может получить доступ Azure. Это требуется SQL Server или SQL Server, экспресс-выпуск базы данных (не hello LocalDB базы данных, hello использование шаблона MVC по умолчанию), поэтому вы создадите базы данных членства hello рядом.

1. В SQL Server Management Studio подключитесь toohello был только что установлен SQL Server. (Если hello **подключения tooServer** окно не открывается автоматически, перейдите в слишком**обозревателя объектов** hello левой панели щелкните **Connect**и нажмите кнопку **Компонент database Engine**.) ![Подключение tooServer][SSMSConnectToServer]
   
    Для параметра **Тип сервера** выберите значение **Ядро СУБД**. Для **имя сервера**, можно использовать **localhost** или имя hello hello компьютера, который вы используете. Выберите **проверки подлинности SQL Server**и войдите в систему с учетной записи SA hello и hello пароль, созданный ранее.
2. Щелкните правой кнопкой мыши toocreate новую базу данных с помощью SQL Server Management Studio **баз данных** в обозревателе объектов и выберите **новой базы данных**.
   
    ![Создание базы данных][SSMScreateNewDB]
3. В hello **новую базу данных** диалоговое окно, введите MembershipDB hello имени базы данных и нажмите кнопку **ОК**.
   
    ![Предоставление имени базы данных][SSMSprovideDBname]
   
    Обратите внимание, что вы не выполните любую базу данных toohello изменения на этом этапе. сведения о членстве Hello будут добавлены автоматически позже веб-приложением при его запуске.
4. В обозревателе объектов, если развернуть **баз данных**, вы увидите, будет создана база данных членства, hello.
   
    ![Создана MembershipDB][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Создание веб-приложения в hello портала Azure
> [!NOTE]
> Если вы уже создали веб-приложения в портале Azure, что в этом учебнике требуется toouse hello, можно сразу перейти слишком[создать гибридное подключение и служба BizTalk](#CreateHC) и продолжить оттуда.
> 
> 

1. В hello [портала Azure](https://portal.azure.com), нажмите кнопку **New** > **Интернет + мобильные устройства** > **веб-приложения**.
   
    ![Кнопка «Создать»][New]
2. Настройте веб-приложение и нажмите кнопку **Создать**.
   
    ![Имя веб-сайта][WebsiteCreationBlade]
3. Через несколько секунд hello веб-приложения создается и отображается колонке web app. Hello колонка предназначена поддерживающим вертикальную прокрутку, позволяющий управлять веб-приложения.
   
    ![Запущенный веб-сайт][WebSiteRunningBlade]
   
    веб-приложения hello tooverify динамической, можно нажать hello **Обзор** страница по умолчанию hello toodisplay значок.

Затем вы создадите гибридного подключения и служба BizTalk для веб-приложения hello.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Создание гибридного подключения и службы BizTalk
1. Назад в hello портала, go toosettings и нажмите кнопку **сети** > **настроить конечные точки гибридного подключения**.
   
    ![Гибридные подключения][CreateHCHCIcon]
2. В колонке подключений гибридного hello, нажмите кнопку **добавить** > **гибридное подключение**.
3. На hello **создать гибридное подключение** колонки:
   
   * Для **имя**, введите имя для соединения hello.
   * Для **Hostname**, введите имя компьютера hello главный компьютер SQL Server.
   * Для **порт**, введите 1433 (порт по умолчанию hello для SQL Server).
   * Нажмите кнопку **службы BizTalk** > **новую службу BizTalk** и введите имя для hello службы BizTalk.
     
     ![Создание гибридного подключения][TwinCreateHCBlades]
4. Нажмите **ОК** дважды.
   
    Когда hello завершения процесса hello **уведомления** области будет мигать зеленым **успех** и hello **гибридное подключение** колонке покажет hello гибридное подключение с Здравствуйте, состояние как **не подключен**.
   
    ![Создано одно гибридное подключение][CreateHCOneConnectionCreated]

На этом этапе вы прошли важной частью гибридного подключения hello облачной инфраструктуры. Далее вы создадите соответствующую локальную часть.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Установка подключения к hello toocomplete hello локальный диспетчер гибридного подключения
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Стало ИТ-инфраструктуры hello гибридное подключение будет создать веб-приложения, которые его используют.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Создание базовых веб-проекта ASP.NET и изменить строку подключения базы данных hello локально запустить проект hello
### <a name="create-a-basic-aspnet-project"></a>Создание базового проекта ASP.NET
1. В Visual Studio в hello **файл** меню, создайте новый проект:
   
    ![Новый проект Visual Studio][HCVSNewProject]
2. В hello **шаблоны** раздел hello **новый проект** диалогового окна выберите **Web** и выберите **веб-приложение ASP.NET**и нажмите кнопку  **ОК**.
   
    ![Выбор веб-приложения ASP.NET][HCVSChooseASPNET]
3. В hello **новый проект ASP.NET** диалоговое окно, выберите **MVC**, а затем нажмите кнопку **ОК**.
   
    ![Выбор MVC][HCVSChooseMVC]
4. При создании проекта hello открывается страница сведений приложения hello. Еще не запущены hello веб-проекта.
   
    ![Страница файла сведений][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Изменить строку соединения hello базы данных для приложения hello
На данном этапе изменить hello строку подключения, которая указывает приложения где toofind локального SQL Server Express базы данных. Строка подключения Hello — в файле Web.config приложения hello, который содержит сведения о конфигурации для приложения hello.

> [!NOTE]
> tooensure, который использует приложение hello базы данных, созданную в SQL Server Express, а не hello один в Visual Studio по умолчанию, LocalDB, очень важно выполнить этот шаг перед запуском проекта.
> 
> 

1. В обозревателе решений дважды щелкните файл Web.config hello.
   
    ![Web.config][HCVSChooseWebConfig]
2. Изменить hello **connectionStrings** раздел базы данных SQL Server toopoint toohello на локальном компьютере, используя синтаксис hello в следующий пример hello:
   
    ![Строка подключения][HCVSConnectionString]
   
    При создании строки подключения hello, имейте в виду следующие hello.
   
   * Если вы подключаетесь tooa именованного экземпляра, а не как экземпляр по умолчанию (например, YourServer\SQLEXPRESS), необходимо настроить статические порты toouse SQL Server. Сведения о настройке статических портов см. в разделе [как tooconfigure toolisten SQL Server через определенный порт](http://support.microsoft.com/kb/823938). По умолчанию именованные экземпляры используют UDP и динамические порты, которые не поддерживаются гибридными подключениями.
   * Рекомендуется указывать hello порт (1433 по умолчанию, как показано в примере hello) в строке подключения hello, так что можно быть уверенным, что локальный SQL Server имеется включенный протокол TCP и использует правильный порт hello.
   * Не забывайте tooconnect toouse проверки подлинности SQL Server, указав hello идентификатор пользователя и пароль в строке подключения.
3. Нажмите кнопку **Сохранить** в файле Web.config hello toosave Visual Studio.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Запустите проект hello локально и регистрации нового пользователя
1. Теперь запустите новый веб-проект локально, нажав кнопку обзора hello в области отладки. В этом примере используется Internet Explorer.
   
    ![Запуск проекта][HCVSRunProject]
2. В правом верхнем углу hello веб-страницы по умолчанию hello и выберите **зарегистрировать** tooregister новой учетной записи:
   
    ![Регистрация новой учетной записи][HCVSRegisterLocally]
3. Введите имя пользователя и пароль:
   
    ![Ввод имени пользователя и пароля][HCVSCreateNewAccount]
   
    Это автоматически создает базу данных на локальном сервере SQL, содержащий сведения о членстве hello для вашего приложения. Одной из таблиц hello (**dbo. AspNetUsers**) содержит веб-приложения, как те, которые вы ввели hello учетные данные пользователя. Вы увидите далее в учебнике hello в этой таблице.
4. Закройте окно браузера hello веб-страницы по умолчанию hello. При этом прекращается выполнение приложения hello в Visual Studio.

Все готово для hello следующий шаг — tooAzure приложения hello toopublish и проверить его.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Публикация tooAzure приложения hello web и проверить его
Теперь будет опубликовать tooyour вашего приложения службы приложений веб-приложение и проверить его toosee как hello гибридного подключения, ранее — идет используется tooconnect вашего приложения для веб-toohello база данных на локальном компьютере.

### <a name="publish-hello-web-application"></a>Публикация веб-приложения hello
1. Вы можете загрузить профиль публикации для hello веб-приложения служб приложений в hello портала Azure. В колонке hello веб-приложения, нажмите кнопку **получение профиля публикации**и сохраните hello файл tooyour компьютера.
   
    ![Загрузить профиль публикации][PortalDownloadPublishProfile]
   
    Далее вы импортируете этот файл в веб-приложение Visual Studio.
2. В Visual Studio, щелкните правой кнопкой мыши имя проекта hello в обозревателе решений и выберите **публикации**.
   
    ![Выбор публикации][HCVSRightClickProjectSelectPublish]
3. В hello **веб-публикация** диалоговое окно на hello **профиль** выберите **импорта**.
   
    ![Импорт][HCVSPublishWebDialogImport]
4. Обзор tooyour загрузить профиль публикации, выберите его и нажмите кнопку **ОК**.
   
    ![Обзор tooprofile][HCVSBrowseToImportPubProfile]
5. Данные публикации импортируется и отображает на hello **подключения** вкладка диалогового окна "hello".
   
    ![Нажмите кнопку "Опубликовать"][HCVSClickPublish]
   
    Щелкните **Опубликовать**.
   
    По завершении публикации браузере запустится и Показать теперь знакомые приложения ASP.NET--, за исключением того, что он в активном состоянии в облаке Azure hello!

Далее используется вашей toosee приложения динамической web его гибридное подключение в действии.

### <a name="test-hello-completed-web-application-on-azure"></a>Hello тест завершения веб-приложения в Azure
1. В верхней части hello справа от веб-страницы в Azure, выберите **входа**.
   
    ![Тестирование входа][HCTestLogIn]
2. Приложение службы, веб-приложения сейчас подключение базы данных членства tooyour веб-приложения на локальном компьютере. tooverify этого, войдите в систему под hello учетные данные, введенные в hello локальной базы данных более ранней версии.
   
    ![Приветствие][HCTestHelloContoso]
3. toofurther тестирование нового гибридного подключения, выйти из системы веб-приложения Azure и зарегистрировать в качестве другого пользователя. Укажите новое имя пользователя и пароль, а затем щелкните кнопку **Зарегистрировать**.
   
    ![Тестирование регистрации другого пользователя][HCTestRegisterRelecloud]
4. что hello новые учетные данные пользователя хранятся в локальной базы данных через подключение к гибридного tooverify откройте SQL Management Studio на локальном компьютере. В обозревателе объектов разверните hello **MembershipDB** базы данных, а затем разверните **таблиц**. Щелкните правой кнопкой мыши hello **dbo. AspNetUsers** членства таблицы и выберите **выделить 1000 верхних строк** tooview hello результаты.
   
    ![Просмотр результатов hello][HCTestSSMSTree]
5. Членство в локальной таблице теперь отображаются обе учетные записи - hello создан локально и hello подпись, которая создается в облаке Azure hello. подпись, которая создается в облаке hello Hello была сохранена tooyour локальной базы данных посредством функции гибридного подключения в Azure.
   
    ![Зарегистрированные пользователи в локальной базе данных][HCTestShowMemberDb]

Создания и развертывания веб-приложения ASP.NET, использующего гибридное подключение между веб-приложения в облако Azure hello и локальная база данных SQL Server. Поздравляем!

## <a name="see-also"></a>См. также
[Обзор гибридных подключений](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Джош Твист (Josh Twist) представляет гибридные подключения (видео Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Обзор гибридных подключений](/services/biztalk-services/)

[Службы BizTalk: вкладки "Панель мониторинга", "Монитор", "Масштаб", "Настройка" и "Гибридные подключения"](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Создание реального облака с гибридным подключением с помощью простой переносимости приложений (видео Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Доступ к локальным ресурсам с помощью гибридных подключений в службе приложений Azure](web-sites-hybrid-connection-get-started.md)

[Общие сведения об удостоверениях ASP.NET](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
