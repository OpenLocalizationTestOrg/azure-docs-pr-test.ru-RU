---
title: "Пример решения Интернета вещей Azure MyDriving: сборка | Документация Майкрософт"
description: "Создавать приложения, — это комплексный Демонстрация как tooarchitect IoT систему с помощью Microsoft Azure, включая Stream Analytics, машинное обучение и концентраторов событий."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Построение и развертывание решений tooyour hello MyDriving среды
MyDriving — это решение "Интернета вещей" (IoT), которое собирает данные о работе автомобиля, обрабатывает их с помощью методов машинного обучения и выводит полученную информацию на экран мобильного телефона. Hello серверной части состоит из различных служб, предоставляемых Microsoft Azure. Hello клиенты могут быть телефоны Android, iOS или Windows 10.

Мы создали hello MyDriving решения toogive вы введение в создание собственной системы IoT. Из hello [MyDriving репозитория в GitHub](https://github.com/Azure-Samples/MyDriving), сценарии диспетчера ресурсов Azure можно получить toodeploy hello внутренней архитектуры в вашу учетную запись Azure. Из этой точки можно перенастроить hello разных служб, изменить данные toosuit запросы hello и так далее. Можно найти эти сценарии--вместе с кодом для мобильного приложения hello, проект hello API службы приложений Azure и многое другое — в репозитории MyDriving hello.

Если вы еще не пробовали приложение hello, посмотрите hello [руководство для начинающих Get](iot-solution-get-started.md).

Подробные учетной записи архитектуры hello hello [MyDriving справочник](http://aka.ms/mydrivingdocs). Таким образом, имеется несколько компонентов, мы настраиваем toocreate аналогичного проекта:

* **Клиентское приложение** работает на телефонах Android, iOS и Windows 10. Мы используем tooshare платформа Xamarin hello большую часть кода hello, которое хранится на GitHub в `src/MobileApp`. приложение Hello фактически выполняет две функции distinct.
  * Он передает данные телеметрии из устройства hello встроенного диагностики (OBD) и свой собственный расположение службы toohello системы облачной серверной части.
  * Это пользовательский интерфейс, который позволяет пользователям запрашивать сведения о записанных поездках.
* Объект **облачная служба** принимает hello пути обработки данных в режиме реального времени и обрабатывает его. Hello основных действий по созданию эта служба является toochoose, параметризации и подключить различные службы Azure. Некоторые части hello требуют сценарии toofilter и процесс hello входящих данных. Мы используем tooconfigure шаблона диспетчера ресурсов Azure все части hello.
* Объект **мобильной службы приложения** — веб-служба hello за части интерфейса пользователя hello hello приложения для устройств. Его основной задания — база данных hello tooquery хранимые, обработанных данных. Код для этой службы размещен на сайте GitHub в разделе `src/MobileAppService`.
* **Visual Studio с Xamarin** . Xamarin, который существует как компонент Visual Studio и как изолированный интегрированной среды разработки (IDE), используется код устройства кросс платформенных toobuild hello. код для iOS toobuild hello, это необходимые toohave экземпляр Xamarin, запущенный на машине OS X. При необходимости он может выполняться как агент, управляемый из Visual Studio.
* **Модульное тестирование** hello устройства выполняется приложений в Xamarin Test Cloud.
* **GitHub** hello репозитория, где хранятся все кода hello, сценарии и шаблоны.
* **Visual Studio Team Services** — это облачная служба, который использовал toomanage hello непрерывном режиме построения и тестирования hello веб-службы и устройства приложений.
* **HockeyApp** — выпуски используется toodistribute кода hello устройства. Она также собирает отчеты о сбоях и использовании и отзывы пользователей.
* **Visual Studio Application Insights** мониторы hello мобильных веб-службы.

Теперь нам нужно все это настроить. 

> [!NOTE] 
> Многие hello, выполнив действия являются необязательными.
>
>

## <a name="sign-up-for-accounts"></a>Регистрация учетных записей
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Это бесплатная программа предоставляет простой доступ toomany разработчиков средств и служб, включая Visual Studio, Visual Studio Team Services и Azure. Кроме того, вы получаете кредит на использование Azure в размере 25 долл. США в месяц на протяжении года. Он также включает подписки tooPluralsight обучения и Xamarin университета. Можно также отдельно подписаться на службы [Azure](https://azure.com) и [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx) уровня "Бесплатный", но эти подписки не предоставляют деньги на счете в Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (необязательно). С помощью этой службы можно управлять тестовым распространением мобильных приложений и осуществлять сбор данных телеметрии.
* [Xamarin](https://xamarin.com/) (обязательно) для создания мобильного приложения hello запускается запусков отладки и тесты на [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (необязательно), toocreate свободного открытых репозиториев для кода (частных репозиториев оплачиваются). Кроме того можно использовать базовый план hello в Visual Studio Team Services для частных репозиториев.
* [Power BI](https://powerbi.microsoft.com/) (необязательно), toocreate широкими возможностями визуализации данных по всей системе hello.

> [!NOTE]
> Не требуется учетная запись tooaccess hello MyDriving код в GitHub [hello репозитория GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Установка средств разработки
Hello следующие настройки — для разработки полнофункционального решения hello: iOS, Android и Windows 10 Mobile кроссплатформенного приложения с использованием Azure серверной части.

В качестве альтернативы можно использовать Xamarin Studio на Mac и Windows toodevelop hello мобильных приложений, если вы не работаете hello завершить обратно в Azure.

Подробное описание указаний по настройке см. [здесь](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Компьютер разработки Windows
Средство центра Hello в Windows является Visual Studio для работы с MyDriving приложение hello для Android и Windows, проект API службы приложения hello и микрослужбу расширения.

Xamarin, Git, эмуляторы и другие полезные компоненты интегрированы в Visual Studio.

Установка:

* [Visual Studio с Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (любой выпуск; выпуск Community — бесплатный).
* [SQLite для универсальной платформы Windows](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Требуется код Windows 10 Mobile toobuild hello.
* [Пакет SDK Azure для Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Предоставляет hello пакета SDK для выполнения приложения в Azure, а также средства командной строки для управления Azure.
* [Пакет SDK для Azure Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Hello необходимые toobuild [микрослужбу](../service-fabric/service-fabric-get-started.md) расширения.

Убедитесь, что у вас есть hello правой расширения Visual Studio. Проверить это можно в разделе **Сервис**. Там вы увидите **Android, iOS, Xamarin и т. д.** В противном случае откройте Visual Studio, поиск Xamarin и tooinstall приглашения hello, выполните его. Также убедитесь, что клиент **Git для Windows** установлен. Если нет, в Visual Studio, выполните его поиск и следуйте tooinstall приглашения hello его. 

### <a name="mac-development-machine"></a>Компьютер разработки Mac
Hello Mac (Yosemite или более поздней версии) является обязательным, если вы хотите toodevelop для операций ввода-вывода. Несмотря на то, что мы использование Visual Studio с Xamarin на Windows toodevelop и управлять ими весь код hello, Xamarin использует агент, установленный на компьютере Mac в порядке toobuild и знак hello кода iOS.

![Разработка в среде Windows и выполнение сборки в среде Mac](./media/iot-solution-build-system/image1.png)

(В качестве альтернативы можно использовать Xamarin Studio непосредственно на hello Mac toodevelop кросс платформенные приложения).

Hello Mac не требуется, если вы не хотите tooinclude iOS в качестве целевой платформы.

Установка:

* [Xamarin Studio для iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Можно также установить Visual Studio и Xamarin на компьютере Mac с виртуальной машиной Windows. Дополнительные сведения см. в статье [Программа установки, установка и проверки для пользователей Mac](https://msdn.microsoft.com/library/mt488770.aspx) на портале MSDN.
* [Средства разработки Azure](https://azure.microsoft.com/downloads/) (необязательно).

Включить удаленное имя входа на hello Mac. Откройте **Системные настройки** > **Общий доступ** и установите флажок **Удаленный вход**.

При открытии проекта iOS в Visual Studio в Windows hello Xamarin подключаемый модуль предложит ввести идентификатор hello hello Mac.

## <a name="fetch-hello-github-repository"></a>Получить репозитории GitHub hello
Получить локальную копию [hello репозитория GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) с помощью hello **загрузить ZIP** кнопку в GitHub, Visual Studio или другой клиент Git.

Распакуйте hello tooa папке с краткий путь, например, C:\\кода.

Кроме того Если требуется tookeep копирование toodate с или добавлять код tooour, клонирование репозитория hello следующим образом:

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Получение ключа API для Карт Bing
[Зарегистрируйтесь для получения ключа API для Карт Bing](https://msdn.microsoft.com/library/ff428642.aspx).

Необходимо, чтобы в этой строки 22 дюйма tooreplace `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Построение образца приложения hello
Откройте следующие решения в Visual Studio:

* src\MobileApps\MyDriving.sln;
* src\MobileAppService\MyDrivingService.sln;
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln.

При этом вам понадобится сделать следующее:

* Подтвердить доверие некоторым потенциально ненадежным проектам. Выберите tooopen их, если вы хотите toogo вперед.
* Задать режим разработчика, если вы работаете на новом компьютере Windows 10.
* Ввести учетные данные Xamarin.
* Подключение toohello Xamarin Mac. Если у вас нет Mac, iOS hello щелкните правой кнопкой мыши проект в Visual Studio, а затем выберите **выгрузить проект**.

Перестройте решение hello.

При наличии проблем построения, попробуйте tooquirks решений hello, мы обнаружили.

* *Не загружает проект VINLookupApplication*: Убедитесь, что установлен hello [пакет Azure SDK для Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Сборка проекта Service Fabric не*: сначала построить проекты интерфейс hello и убедитесь, что установлен hello Service Fabric SDK.
* *Не удается выполнить сборку приложения Android*.
  
  * Щелкните **Сервис** > **Android** > **Диспетчер пакетов SDK для Android** и убедитесь, что Android 6 (API 23) и платформа SDK установлены.
  * Удалите следующий каталог, а затем повторите сборку:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Получение кода hello tooknow
В решении hello вы найдете:

* расширения Azure: Service Fabric;
* Azure HDInsight: сценарии для обработки данных поездок в Azure;
* Мобильные приложения: hello приложений для устройств.
* MobileAppsService/MyDrivingService: конец hello web обратно.
* Power BI: определение отчета hello.
* Scripts:
  
  * Диспетчер ресурсов: шаблоны toobuild hello ресурсов Azure.
  * PowerShell: Шаблоны диспетчера ресурсов hello toorun сценариев.
  * База данных SQL: базы данных отладки;
* База данных SQL: CreateTables — определения схем;
* Azure Stream Analytics: Запросы, преобразования hello входной поток данных.

## <a name="run-hello-apps-in-development-mode"></a>Запускайте приложения hello в режиме разработки
Выполните действие toorun приложения hello, в зависимости от устройства hello, которую вы используете.

* Внутренний: MyDrivingService набор как запускаемый проект hello и нажмите клавишу F5 toorun hello серверной части веб-службы. Откроется представление браузера листинг hello API.
* Мобильные клиенты: hello [разработки мобильных приложений в Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: чтобы узнать больше, ознакомьтесь с [отладкой приложений Android в Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: чтобы узнать больше, ознакомьтесь с [отладкой в iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: чтобы узнать больше, ознакомьтесь с разделом [Xamarin + Universal Windows Platform](https://developer.xamarin.com/guides/cross-platform/windows/phone/)(Xamarin и универсальная платформа Windows).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Отправка tooHockeyApp мобильное приложение hello
HockeyApp управляет hello распространения Windows, iOS или Android, приложение tootest пользователей, связанные с уведомлением пользователей новых выпусков. Кроме того, эта служба собирает отчеты о сбоях, отзывы пользователей со снимками экрана, а также метрики использования.

[Сначала передайте](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) приложение сборки. Затем войдите в слишком[HockeyApp](https://rink.hockeyapp.net) с компьютера разработки. На панели мониторинга разработчика hello, нажмите кнопку **новое приложение**и перетащите в окно приветствия файлов построенных hello. (Более поздней версии, можно автоматизировать вашей toodo службы построения это.)

Вы перейдете на панель мониторинга приложения.

![Вкладка обзора на панели мониторинга приложения hello](./media/iot-solution-build-system/image2.png)

Повторите процесс hello для каждой платформы, ваше приложение запускается. После этого можно сделать hello следующее:

* Используйте hello [идентификатор приложения](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) hello мониторинга toosend аварийного завершения данных и обратной связи от приложения. В MyDriving обновите их идентификаторы hello в src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Пригласите тестовых пользователей](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Вы получаете toorecruit URL-адрес пользователей тест-инженеры. Они будет может toosign для команды, загрузите приложение hello, а отправить отзыв.
* Если вы предпочитаете более открыта бета-версии, установите распространения toopublic hello. Щелкните **Manage App**(Управление приложением) > **Distribution**(Распространение) > **Download = Public** (Общедоступное скачивание). Теперь все пользователи могут скачать приложение и отправить отзыв о нем. Если вы опубликуете новую версию, они увидят соответствующее уведомление. Кроме того, они также могут отправить вам отчеты о сбоях.
  
   ![Команды на панели мониторинга hello](./media/iot-solution-build-system/image3.png)
* [Сбой связи сообщает tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Щелкните **Manage App**(Управление приложением) > **Visual Studio Team Services**. Служба HockeyApp может автоматически создавать рабочие элементы в Team Services при получении отчетов о сбоях или отзывов.

Чтение ознакомьтесь с hello [HockeyApp сайта](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Тестирование hello мобильных приложений в Xamarin Test Cloud
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) автоматизирует тестирование пользовательского интерфейса на реальном устройстве в облаке hello. С помощью платформы NUnit hello, нужно создать тесты, запустите приложение через пользовательский интерфейс hello.

toouse Xamarin внедрить hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK в веб-приложения, который поставляется в виде пакета NuGet. Вы найдете в hello нашего примера приложения, и он включен при создании новых проектов тестов с помощью hello шаблоны Xamarin.

![Где toofind hello кросс платформенных SDK на интерфейсе hello](./media/iot-solution-build-system/image4.png)

Пример тестовый проект входит в состав приложения hello в репозитории hello. Ищите его в каталоге [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/ в [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService).

Если вы используете построения Visual Studio Team Services, это легко toowrite пользовательского интерфейса Xamarin модульные тесты и их как часть построения.

## <a name="deploy-azure-services"></a>Развертывание служб Azure
toohello tooperform автоматическое развертывание служб Azure и службы построения Team Services, см. Подробные инструкции в **scripts/README.md**.

Microsoft Azure предоставляет множество различных служб, которые можно использовать toobuild облачных приложений. Несмотря на то, что многие могут использоваться отдельно (например, приложение службы и веб-приложения), они в их наиболее эффективно, если они взаимосвязанных tooform интегрированные системы так, мы используем в MyDriving.

Он будет возможно toocreate вручную соединений служб Azure, а это гораздо проще и надежнее шаблоны Azure Resource Manager toouse. [Диспетчер ресурсов](../azure-resource-manager/resource-group-overview.md) автоматизирует hello развертывание решения ресурсов, который hello соединения между ними.

Вы найдете hello шаблона для hello MyDriving системы в репозитории GitHub hello под [скриптов или платформы ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Он предоставляет полную и краткое представление как hello различными службами в нашей архитектуре связаны между собой. Все эти в hello подробно объясняются [MyDriving справочник](http://aka.ms/mydrivingdocs), но можно узнать много достаточно прочтя самого шаблона hello.

> [!NOTE]
> Большинство служб Azure имеют стоимость в зависимости от ценового уровня hello. Если вы новый tooAzure, вы можете [бесплатно опробовать](https://azure.microsoft.com/free/). Тем не менее, если вы не собираетесь toouse некоторые компоненты из hello MyDriving системы, быть tooremove убедиться, что их tooavoid дополнительных затрат. раздел «Оценка эксплуатационные расходы» Hello позже в этой статье представлена сводка обычной службы расходов.
> 
> 

### <a name="edit-hello-template"></a>Изменение шаблона hello
toocustomize развертывания, возможно tooremove ненужные компоненты или tooadd другим пользователям, сначала создайте копии сценарий\_complete.params.json и сценарии\_complete.json передачи toomake изменений.

Можно использовать сценарий hello\_toooverride файл complete.params.json различные значения по умолчанию, например hello SKU или hello хранилища репликации тип службы, как описано в следующей таблице hello. значения по умолчанию Hello выберите параметры наименьшую стоимость hello.

| **Параметр** | **Описание** | **Значение по умолчанию** |
| --- | --- | --- |
| SKU Центра Интернета вещей |Уровень службы Центра Интернета вещей Azure |F1 |
| Storage Account Type |Тип репликации хранилища |Standard LRS |
| SQL Service Objective |Использование слотов выдачи |DW100 |
| Hosting Plan SKU |План обслуживания службы приложений |F1 |

В файле scenario\_complete.json сделайте следующее:

* Поиск базовое «имя» и измените его имя tooa предпочтительным.
* Найдите значения Create. Каждый такой раздел создает ресурс.
* Значения sqlServerAdminLogin и sqlServerAdminPassword toosuitable.
* Прежде чем удалить раздел, в котором создан ресурс, проверьте, имеет ли он зависимых компонентов, выполняя поиск имени в другом месте в файле hello. Обратите внимание, что каждый раздел, который создает службу, содержит раздел *dependsOn*, где перечислены ее зависимости.

Вот настраивает какой шаблон hello. Дополнительные сведения приведены в hello [справочник](http://aka.ms/mydrivingdocs).

| **Служба** | **Описание и объяснение** |
| --- | --- |
| учетные записи хранения; |шаблон Hello создает три учетные записи: |
| -Базы данных SQL, получает статистические данные телеметрии от Stream Analytics и служит в качестве hello резервного хранилища для предоставления этих данных через конечные точки API службы приложений Azure таблиц. | |
| -Blob хранилище, накапливает исторические данные из другого задания Stream Analytics, обрабатываемых HDInsight toobe. | |
| — базы данных SQL, которая получает обработанные HDInsight данные для использования с Power BI. | |
| Центр Интернета вещей Azure |Устанавливает двустороннее подключение tooeach подключенное устройство. Мобильное приложение hello hello MyDriving решения, действует как поле шлюза toosend данных tooAzure центр IoT. Центр IoT Azure затем служит в качестве входного tooStream Analytics. |
| Концентраторы событий Azure |Выход для задания Stream Analytics, что очереди hello tooextensions выходных данных, созданных в Azure Service Fabric. |
| Хранилище данных SQL Azure | |
| Задания Stream Analytics |Запрос, который будет использоваться tooaggregate соединены входы и выходы в режиме реального времени и исторические данные для API-интерфейсы службы приложения hello, машинного обучения Azure, расширения и Power BI. |
| Рабочая область машинного обучения |Включает в себя эксперименты, код R и службу API. |
| Фабрика данных Azure |Эта служба используется для планового повторного обучения механизма машинного обучения. |
| План размещения Service Fabric |Это план для расширений. |
| Служба приложений (мобильное приложение) |Узлы проект API мобильной приложения hello, предоставляет конечные точки для мобильного приложения hello. Hello API код должен быть tooApp развернутой службы из Visual Studio. |
| Правила оповещения |Отправляет по электронной почте, если ответы приложения hello сведения о сбоях. |
| Application Insights |Для наблюдения за производительностью hello API-интерфейсы в службе приложений. В Visual Studio имеется tooconfigure hello соединения. |
| Хранилище ключей Azure |Для сохранения кластера сертификат hello веб-службы. |

### <a name="run-hello-template"></a>Запустить шаблон hello
В **scripts/README.md**, подробные инструкции для выполнения шаблона hello.

tooprovision все эти службы в вашу учетную запись Azure с помощью скрипта hello выполните hello следующие действия.

* Используйте PowerShell.
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *расположение* — hello [расположение Azure](https://azure.microsoft.com/regions/), такие как `North Europe` или `West US`. Используйте `Get-AzureLocation` toofind список доступных расположений.
  * *resourceGroupName* hello имя, которое требуется toogive toohello группу, которому принадлежат все ресурсы hello. По завершении работы с ресурсами hello их можно удалить вместе с удалением данной группы.
* Запустите DeploymentScripts/Bash/deploy.sh с помощью Bash.
* Откройте и решения Visual Studio hello DeploymentScripts/VS/DeployARM.sln.

Обратите внимание, что каждый шаблон hello времени выполнения, создается новый набор ресурсов с новыми именами. ресурсы hello toodelete, go toohello портала и удаления группы ресурсов hello.

Если скрипт hello какой-либо причине произошел сбой, можно повторно запустить его.

предоставляет сценарий Hello hello возможность настроить непрерывной интеграции в Visual Studio Team Services. Если вы установили проект Team Services, у вас будет URL-адрес https://yourAccountName.visualstudio.com. Введите полный URL-адрес hello в ответ на запрос. Проекту Team Services можно присвоить как новое, так и существующее имя.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Настройка определений сборки и тестирования в Visual Studio Team Services
В рамках это проекта Team Services главным образом используется из-за своих функций создания и тестирования. Но эта среда также предоставляет такие возможности для совместной работы, как управление задачами с помощью канбан-досок, функция проверки кода, интегрированная с задачами и системой управления версиями, а также условные сборки. Кроме того, службы Team Services поддерживают интеграцию с другими инструментами, например GitHub, Xamarin, HockeyApp и, конечно же, Visual Studio. Его можно открыть hello веб-интерфейсе или с помощью Visual Studio, какое значение является более удобным в любой момент.

шаги построения hello Hello и определения выпуска использовать различные подключаемого модуля служб, доступных в hello Team Services [Marketplace](https://marketplace.visualstudio.com/VSTS). В добавление toobasic программы toorun командной строки или копирования файлов существуют службы, вызывать сборки с Xamarin, Android и других поставщиков и tooHockeyApp, которые подключаются.

![Параметры сборки в Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Определения сборки
У нас есть определения построения для каждого hello основными целевыми объектами. У нас также есть отклонения для тестирования компонентов и регрессионного тестирования. Таким образом, мы имеем:

* MyDriving.Services (hello серверной части веб-приложение для мобильного приложения hello)
* MyDriving.Xamarin.Android:
  
  * MyDriving.Xamarin.Android-Feature;
  * MyDriving.Xamarin.Android-Regression.
* MyDriving.Xamarin.iOS:
  
  * MyDriving.Xamarin.iOS-Feature;
  * MyDriving.Xamarin.iOS-Regression.
* MyDriving.Xamarin.UWP:
  
  * MyDriving.Xamarin.UWP-Feature;
  * MyDriving.Xamarin.UWP-Regression.

Следует hello полностью toosee нашей конфигурации в разделе 4.7 hello [MyDriving справочник](http://aka.ms/mydrivingdocs), «Сборка и конфигурации выпуска.» Они следуют hello же общий шаблон. скрипт Hello:

1. Восстановление пакета NuGet hello. Мы не хранить скомпилированного кода в репозитории hello, таким образом, первые шаги hello каждой сборки будут toorestore hello необходимые пакеты NuGet.
2. Активирует hello лицензии. Hello сборка выполняется в облаке hello таким образом там, где нам нужна лицензия — в частности, служба--сборок Xamarin hello у нас есть tooactivate нашей лицензии на текущем компьютере построения hello. Затем мы деактивируйте его незамедлительно после tooallow его toobe используется на другом компьютере.
3. Создает с помощью соответствующую службу hello. Мы используем сборок Xamarin для мобильных приложений hello и Visual Studio создает для hello серверной части веб-службы.
4. Выполняет сборку тестов.
5. Выполняет тесты Мы тесты hello мобильных приложений в Xamarin Test Cloud.
6. Публикует расположение сброса toohello результат сборки hello.

Hello для основных сборок hello установлен toocontinuous интеграции. То есть hello выполняется каждый раз при возврате кода toohello главную ветвь.

![Интерфейс, где триггер hello — набор toocontinuous интеграции](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Определения выпуска
Определения выпуска, настраиваются в много hello таким же способом.

Для веб-службы hello мы настраиваем развертывания в виде веб-приложение Azure.

![Интерфейс для настройки развертывания в виде веб-приложения Azure](./media/iot-solution-build-system/image7.png)

И мы устанавливаем hello выпуска триггер toocontinuous развертывания. То есть, каждого возврата следуют результатов успешного построения в веб-приложение toohello обновления.

![Интерфейс для настройки развертывания toocontinuous триггера выпуска hello](./media/iot-solution-build-system/image8.png)

Для мобильных приложений мы развертывание tooHockeyApp:

![Интерфейс для развертывания tooHockeyApp мобильного приложения](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Просмотр данных телеметрии с помощью Application Insights
[Application Insights](../application-insights/app-insights-overview.md) собирает данные телеметрии об hello производительности и использовании веб-служб. Hello пакет SDK Application Insights отправляет данные телеметрии из службы hello toohello ресурс Application Insights в Azure.

Обзор настройки шаблона hello toohello ресурс Application Insights. Нет, вы можете просматривать диаграммы производительности hello вашей [служба мобильного приложения проекта](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). На них отображено число запросов к серверу и время ответа сервера, а также число сбоев и исключений. Также существуют диаграммы времени ответа зависимостей — то есть база данных вызовы toohello и tooREST API, например машинного обучения. Если имеются проблемы с производительностью, вы будете может toosee, какая часть системы вызывает их.

![Пример диаграммы производительности](./media/iot-solution-build-system/image11.png)

При наличии веб-службы, которую вы настроили вручную легко tooget hello же диаграммы. В колонке службы web hello, нажмите кнопку **средства** > **расширения** > **добавить**. Выберите **Application Insights**.

![Интерфейс для выбора диаграммы hello tooget Application Insights](./media/iot-solution-build-system/image12.png)

функция Hello работает по настройке приложения с помощью пакета SDK Application Insights hello.

Можно добавить пользовательские телеметрии (или инструментировать приложения, на котором работает где-либо за пределами Azure), [Добавление hello пакет SDK Application Insights](../application-insights/app-insights-asp-net.md) во время разработки. Это полезно toolog метрики, которые зависят от приложения hello, такие как длина среднее trip пользователей или общее расстояние. В Visual Studio, щелкните правой кнопкой мыши проект hello и выберите **добавить Application Insights**.

![Интерфейс для выбора пользовательского телеметрии tooadd добавить Application Insights](./media/iot-solution-build-system/image10.png)

Application Insights будет отправлять оповещения по электронной почте при обнаружении необычного числа ответов о сбое. Можно также настроить собственные оповещения о различных метриках, например, о времени отклика.

Том, что веб-службы всегда вверх и запущена, можно настроить только toobe [тестов доступности](../application-insights/app-insights-monitor-web-app-availability.md). Эти тесты проверки связи сайта из различных расположений вокруг Здравствуй, мир! каждые 15 минут. Снова вы получите сообщение электронной почты, если похоже, что toobe проблема.

## <a name="estimate-operational-costs"></a>Оценка эксплуатационных расходов
Это весьма недорогих toorun приложения такого рода при небольшом масштабе. Многие из служб hello быть свободного начального уровня, очень слабо стоимость разработки и небольших операции. И Конечно, собственных приложений отсутствует демонстрируются все функции hello в MyDriving toouse.

Вот приблизительной оценки наших затрат в настройке конфигурации hello разработки для MyDriving. Мы также отметим некоторые альтернативные варианты, которые мы *не* использовали. Эти сведения могут быть полезны при оценке своих собственных затрат.

Предполагается следующий сценарий:

* группа максимум из пяти человек (а также наблюдающие заинтересованные лица);
* приложение будет работать примерно месяц;
* 100 пользователей с четырьмя поездками в день.

> [!NOTE]
> Если вы новый tooAzure имеется [освободить учетной записи](https://azure.microsoft.com/free/).
> 
> 

| **Служба или компонент** | **Примечания** | **Стоимость в месяц** |
| --- | --- | --- |
| [Выпуск Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) с [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Кроссплатформенная среда разработки. |Visual Studio Community. (Требуется [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) для [Xamarin.Forms](https://xamarin.com/forms), toodesign кросс платформенных с единой базой кода.) |0 долл. США |
| [Центр Интернета вещей](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Данные двустороннее соединение toodevices |8000 сообщений плюс 0,5 КБ данных на сообщение — бесплатно. |0 долл. США |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Обработка большого объема потоковых данных. |Если включена, взимается 0,031 долл. США за единицу потоковой передачи в час. Выберите hello число единиц потоковой передачи, которые нужно; Дополнительные tooscale вверх. |23 долл. США |
| [Машинное обучение](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Адаптивные ответы. |10 долл. США за рабочее место в месяц. <br/>                                                                                                                                                                                 +3 часа эксперимента \* 1 долл. США за час эксперимента. <br/>                                                                                                                                                           +3,5 часа процессорного времени API \* 2 долл. США за час рабочего ЦП. <br/>                                                                                                                                                          Во времени ЦП API учитываются затраты 5 минут в день на повторное обучение, однако это значение будет увеличиваться по мере роста объема входных данных.                   <br/>                                                                                                                                                                     + 2 минут в день оценки tooprocess 400 приема-передачи данных в день. |20 долл. США |
| [Служба приложений](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Размещение серверной части мобильной службы. |Уровень B1 — рабочие веб-приложения. |56 долл. США |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Сборка, модульное тестирование и управление выпусками, управление задачами. |Частные агенты, пять пользователей. |0 долл. США |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Мониторинг производительности и использования веб-служб и сайтов. |Уровень "Бесплатный". |0 долл. США |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Распространение бета-версий приложений, а также сбор отзывов и данных об использовании и сбоях. |Два бесплатных приложения для новых пользователей.<br/> Затем 30 долл. США в месяц. |0 долл. США |
| [Xamarin](https://store.xamarin.com/)<br/> Программирование для универсальной платформы, подходящей для нескольких устройств. |Бесплатная пробная версия. <br/>Затем 25 долл. США в месяц. |0 долл. США |
| [База данных SQL](https://azure.microsoft.com/pricing/details/sql-database/) для службы приложений Azure. |Уровень "Базовый"; модель отдельных баз данных. |5 долл. США |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (необязательно) |Запуск локального кластера. |0 долл. США |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Универсальное средство отображения и исследования потоковых и статических данных. |Уровень "Бесплатный": 1 ГБ, 10 000 строк в час, ежедневное обновление. <br/> 10 долл. США за пользователя в месяц: [более высокие лимиты](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), дополнительные варианты подключения, совместная работа. |0 долл. США |
| [Хранилище](https://azure.microsoft.com/pricing/details/storage/) |Локально избыточное хранилище &lt; 100 ГБ по 0,024 долл. США за 1 ГБ. |3 долл. США |
| [Фабрика данных](https://azure.microsoft.com/pricing/details/data-factory/) |0,60 долл. США за действие\* (8–5 FOC). |2 долл. США |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Кластер по требованию для ежедневного повторного обучения. |Три узла A3 за 0,32 долл. США в час ежедневно * 31 день. |30 долл. США |
| [Концентраторы событий](https://azure.microsoft.com/pricing/details/event-hubs/) |Уровень "Базовый", 11 долл. США в месяц за единицу пропускной способности плюс 0,028 долл. США за входящие данные. |11 долл. США |
| Аппаратный ключ OBD | |12 долл. США |
| **Всего** | |**157 долл. США** |

Дополнительные сведения можно найти в разделе 

* Сводка по [квотам и ограничениям службы Azure](../azure-subscription-service-limits.md#iot-hub-limits)
* [Калькулятор стоимости](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Отправка отзывов
Поскольку мы создали введение toohelp MyDriving IoT системах, мы хотим наверняка toohear от вас о того, насколько хорошо он работает. Сообщите нам, если во время использования приложения вы столкнулись с такими ситуациями.

* Возникли неполадки или проблемы.
* Является точкой расширения, делает более подходящими tooyour сценария.
* Найти более эффективным способом tooaccomplish определенных требований.
* У вас есть предложения по улучшению MyDriving или этой документации.

отзыв toogive файла [проблемы на GitHub] или оставьте комментарий ниже (en-us edition).

Мы будем toohearing вашим отзывам.

## <a name="next-steps"></a>Дальнейшие действия
Рекомендуется hello [MyDriving справочник](http://aka.ms/mydrivingdocs), который является подробное описание структуры hello hello системы и ее компонентов.

