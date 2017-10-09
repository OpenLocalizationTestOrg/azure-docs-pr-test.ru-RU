---
title: "aaaContinuous доставка для облачных служб с Team Foundation Server в Azure | Документы Microsoft"
description: "Дополнительные сведения об tooset копирование непрерывная доставка для Azure облачных приложений. Примеры программного кода для инструкций командной строки MSBuild и сценариев PowerShell."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Непрерывная доставка для облачных служб в Azure
Hello процесс, описанный в этой статье показано, как tooset копирование непрерывная доставка для Azure облачных приложений. Этот процесс позволяет автоматически создавать пакеты и развертывание пакета tooAzure hello после каждого возврата кода. Hello процесс построения пакета, описанных в этой статье — эквивалент toohello **пакета** команд в Visual Studio и публикации действия, эквивалентные toohello **публикации** в Visual Studio.
Hello статье рассматриваются hello методов используется toocreate сервер сборки с помощью инструкций командной строки MSBuild и сценарии Windows PowerShell, а также показано, как toooptionally настроить Visual Studio Team Foundation Server - Team Build определения toouse hello MSBuild команд и сценариев PowerShell. процесс Hello можно настраивать для построения среды и Azure целевых средах.

Можно также использовать Visual Studio Team Services, к версии TFS, размещенной в Azure, toodo это проще. 

Прежде чем начать, следует опубликовать приложение из Visual Studio.
Это обеспечит, все hello ресурсы, доступные и инициализируется при попытке установить процесс публикации tooautomate hello.

## <a name="1-configure-hello-build-server"></a>1: Настройка hello сервера построения
Перед созданием пакета служб Azure с помощью MSBuild hello требуется программное обеспечение и средства необходимо установить на сервере сборки hello.

Visual Studio не требуется toobe установлен на сервере сборки hello. Toomanage toouse службу сборок Team Foundation ваш сервер сборки, выполните инструкции hello в hello [службу сборок Team Foundation] [ Team Foundation Build Service] документации.

1. Установите на сервере сборки hello hello [.NET Framework 4.5.2][.NET Framework 4.5.2], которая включает MSBuild.
2. Установить последние hello [средствам разработки Azure для .NET](https://azure.microsoft.com/develop/net/).
3. Установка hello [библиотек Azure для .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Копировать hello файл Microsoft.WebApplication.targets из установки Visual Studio toohello сборки сервера.

   На компьютере с установленной среды Visual Studio, этот файл расположен в каталоге hello C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications. Его необходимо скопировать toohello один каталог на сервере сборки hello.
5. Установка hello [средства Azure для Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2. Создание пакета с помощью команд MSBuild
В этом разделе описываются как tooconstruct MSBuild команды построения пакета служб Azure. Выполните этот шаг на tooverify сервер сборки hello, все настроено правильно и что команда MSBuild hello делает, необходимую toodo. Можно либо добавить этой командной строки tooexisting создавать сценарии на сервере сборки hello, или можно использовать командную строку hello в определение построения TFS, как описано в следующем разделе hello. Дополнительные сведения о параметрах командной строки и MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Если установлена среда Visual Studio на сервере сборки hello, найдите и выберите **командной строки Visual Studio** в hello **набора средств Visual Studio** папки в Windows.

   Если Visual Studio не установлена на сервере сборки hello, откройте командную строку и убедитесь, что MSBuild.exe доступен по пути. MSBuild устанавливается вместе с hello .NET Framework в hello пути % WINDIR %\\Microsoft.NET\\Framework\\*версии*. Например для добавления переменной среды PATH toohello MSBuild.exe, если у вас установлена платформа .NET Framework 4, введите следующую команду в командной строке hello hello:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. В командной строке hello перейдите toohello папки, содержащей файл проекта Azure, что требуется toobuild.
3. Запустите MSBuild с hello/target: параметр как следующий пример hello публикации:

       MSBuild /target:Publish

   Этот параметр можно сократить до /t:Publish. параметр /t:Publish Hello в MSBuild не следует путать с команды hello публикации, доступные в Visual Studio, при наличии приветствия установлен пакет SDK Azure. Здравствуйте, / t: публикация параметр только для сборок hello Azure пакетов. Он не осуществляет развертывание пакетов hello, как команды hello публикации в Visual Studio.

   При необходимости можно указать имя проекта hello как параметр MSBuild. Если не указан, используется текущий каталог hello. Дополнительные сведения о параметрах командной строки MSBuild см. в [справочнике по командной строке MSBuild](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Найдите выходные данные hello. По умолчанию эта команда создает каталог отношения toohello корневой папки для проекта hello, таких как *ProjectDir*\\bin\\*конфигурации* \\ App.Publish\\. При построении проекта Azure создаются два файла, собственно файл пакета hello и hello, сопровождающие файла конфигурации:

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   По умолчанию каждый проект Azure включает в себя один файл конфигурации службы (с расширением .cscfg) для локальных сборок (отладка) и еще один файл для облачных сборок (промежуточная или рабочая среда), но вы можете добавлять или удалять файлы конфигурации службы при необходимости. При построении пакета в среде Visual Studio будет запрашиваться tooinclude файла конфигурации какие службы, наряду с hello пакета.
5. Укажите файл конфигурации службы hello. При создании пакета с помощью MSBuild, файл конфигурации локальной службы hello включается по умолчанию. tooinclude файл конфигурации другую службу, задайте свойство TargetProfile команды MSBuild hello, как следующий пример hello:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Укажите место hello hello выходных данных. Задает путь к hello с помощью /p:PublishDir =*каталога* \\ параметр, включая конечный разделитель обратной косой черты, как следующий пример hello hello:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   После создания и тестирования соответствующие MSBuild командной строки toobuild проектов и объединять их в пакете служб Azure, можно добавить сценарии построения tooyour этой командной строки. Если сервер сборки использует пользовательские сценарии, этот процесс будет зависеть от особенностей пользовательского процесса сборки. При использовании TFS в качестве среды разработки необходимо выполнить инструкции hello hello следующий шаг tooadd hello Azure пакет сборки tooyour процесса построения.

## <a name="3-build-a-package-using-tfs-team-build"></a>3. Создание пакета с помощью TFS Team Build
Если у вас есть настроить Team Foundation Server (TFS) настроить контроллер построений и hello серверы сборки, в качестве компьютера сборки TFS, а затем при необходимости можно настроить автоматизированной сборки для пакета Azure. Сведения о статье tooset копирование и использование сервера Team Foundation server в качестве системы сборки, [масштабирование системы построения][Scale out your build system]. В частности, в следующей процедуре предполагается, что настроили ваш сервер сборки, как описано в [развертывание и настройка сервера сборки][Deploy and configure a build server], и что вы создали командный проект, создать облако проект службы в командном проекте hello.

tooconfigure TFS toobuild Azure пакеты, выполните следующие шаги hello:

1. В Visual Studio на компьютере разработчика, в меню "Вид" hello, выберите **Team Explorer**, или нажмите сочетание клавиш Ctrl +\\, Ctrl + M. В командном обозревателе разверните hello **строит** узла или выберите hello **строит** странице и выберите **создать определение построения**.

   ![Параметр "Создать определение сборки"][0]
2. Выберите hello **триггер** и укажите hello требуемого условия для при необходимости hello построен toobe пакета. Например, указать **непрерывной интеграции** происходит toobuild hello пакета всякий раз, когда возврата системы управления версиями.
3. Выберите hello **параметры источника** вкладку и убедитесь, что папку проекта, перечисленные в hello **папка системы управления версиями** столбца, и находится в состоянии hello **Active**.
4. Выберите hello **сборки по умолчанию** и в списке контроллер построений убедитесь hello имя сервера построения hello.  Кроме того, выберите параметр hello **следующие toohello выходные данные построения копирования транзитный каталог** и укажите расположение сброса требуемого hello.
5. Выберите hello **процесс** вкладки. На вкладке "процесс" hello, выберите шаблон по умолчанию hello в разделе **построения**, выберите проект hello в том случае, если он еще не выбран и разверните hello **Дополнительно** раздела hello **построения**части сетки hello.
6. Выберите **Аргументы MSBuild**и задать аргументы командной строки MSBuild соответствующие hello, как описано в шаге 2 выше. Например, введите **/t: публикация /p:PublishDir =\\\\myserver\\удаляет\\**  toobuild пакет hello пакета и скопируйте файлы toohello расположение \\ \\myserver\\удаляет\\:

   ![Аргументы MSBuild][2]

   > [!NOTE]
   > Копирование файлов tooa hello общей папке упрощает toomanually упрощает развертывание пакетов hello с компьютера разработчика.
7. Протестировать успех hello этапа построения путем возврата изменений tooyour проекта или очередь новую сборку. tooqueue копирование новую сборку в Team Explorer, щелкните правой кнопкой мыши **определений сборок,** и выберите **новую сборку в очередь**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4. Публикация пакета с помощью сценария PowerShell
В этом разделе описывается, как сценарий Windows PowerShell, который будет публиковать пакет приложения hello облака tooconstruct вывода tooAzure использование необязательных параметров. Этот сценарий может быть вызвана после шага построения hello в автоматизации настраиваемой сборки. Также он может быть вызван из действий рабочего процесса шаблона процесса в Visual Studio TFS Team Build.

1. Установка hello [командлетов Azure PowerShell] [ Azure PowerShell cmdlets] (v0.6.1 или более поздней версии).
   Во время фазы установки командлета hello выберите tooinstall в качестве оснастки. Обратите внимание, что официально поддерживаемой заменяет старую версию hello, предоставляемые через CodePlex, несмотря на то, что hello предыдущих версий были номерами 2.x.x.
2. Запустите PowerShell Azure с помощью меню "Пуск" hello "или" Начальная страница. При запуске таким образом, будут загружены hello командлетов Azure PowerShell.
3. В командной строке PowerShell hello, проверьте загрузку hello командлеты PowerShell, введя команду частичного hello `Get-Azure` и нажав клавишу Tab для завершения операторов "hello".

   При нажатии клавиши Tab hello многократно, вы увидите различные команды Azure PowerShell.
4. Убедитесь, что можно подключиться tooyour подписке Azure путем импорта из файла .publishsettings hello сведений о подписке.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Затем введите команду hello

   `Get-AzureSubscription`

   Отобразится информация о подписке. Убедитесь, что все работает правильно.
5. Сохранить шаблон скрипта hello, указанный в конце hello в этой статье в папку скриптов в c:\\сценариев\\WindowsAzure\\**PublishCloudService.ps1**.
6. Прочтите раздел параметров hello hello скрипта. Добавьте или измените любые значения по умолчанию. Эти значения можно всегда переопределить с помощью передачи явных параметров.
7. Убедитесь, существует допустимое облачной службы и учетные записи хранения в подписке, может быть целевым объектом hello скрипта публикации. Учетной записи хранения (хранилище blob) будет использоваться tooupload и временного хранения hello развертывания пакета и файле конфигурации во время развертывания.

   * toocreate новой облачной службы, может вызывать этот сценарий или используйте hello [портал Azure](https://portal.azure.com). Hello имя облачной службы будет использоваться в качестве префикса в полное доменное имя, и поэтому должен быть уникальным.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate новой учетной записи хранения, можно вызвать этот сценарий или используйте hello [портал Azure](https://portal.azure.com). Имя учетной записи хранения Hello будет использован в качестве префикса в полное доменное имя, и поэтому должен быть уникальным. Попробуйте использовать одинаковые имена, hello как облачную службу.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Вызов скрипта hello прямо из Azure PowerShell или подключить этот скрипт построения узла tooyour автоматизации toooccur после сборки пакета hello.

   > [!IMPORTANT]
   > сценарий Hello всегда удалит или замене существующих развертываний по умолчанию, если они обнаружены. Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя.
   >
   >

   **Пример сценария 1:** toohello непрерывного развертывания промежуточной среде службы:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Это обычно сопровождается тестовым запуском проверки и замены виртуального IP-адреса. swap Hello виртуальных IP-адресов можно сделать с помощью hello [портал Azure](https://portal.azure.com) или с помощью командлета Move развертывания hello.

   **Пример сценария 2:** непрерывного развертывания toohello рабочей среде служба выделенной тестирования

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Удаленный рабочий стол**

   Если удаленный рабочий стол включен в проекте Azure необходимо будет tooperform дополнительные одноразовый действия tooensure приветствия правильный сертификат службы облачной отправлен tooall облачные службы мишенью для этого сценария.

   Найдите значения отпечатка сертификата hello, ожидаемый вашей роли. Отпечаток значения видны hello сертификаты из раздела файла конфигурации облака (т. е. ServiceConfiguration.Cloud.cscfg). Это также отображается в диалоговом окне Конфигурация удаленного рабочего стола hello в Visual Studio, когда Показать параметры и представление hello выбран сертификат.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Передавать сертификаты удаленного рабочего стола, как на этапе одноразовой настройки, с помощью hello, выполнив командлет сценария:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Например:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Кроме того, можно экспортировать файл hello сертификата PFX с закрытым ключом и передачи сертификатов tooeach целевой облачной службы с помощью [портал Azure](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Обновление развертывания по сравнению с удалением развертывания и \>созданием развертывания**

   Hello по умолчанию выполняет скрипт развертывания обновления ($enableDeploymentUpgrade = 1) Если не передаются никакие параметры в или явным образом передается значение 1. Для одного экземпляра это имеет преимущество, поскольку тратится меньше времени, чем на полное развертывание. Для экземпляров, которые требуют высокой доступности, это также имеет преимущество hello, остаются некоторые под управлением, тогда как другие экземпляры обновляются (проходу домена обновления), а также VIP-адрес не будет удален.

   Развертывания обновления можно отключить в скрипте hello ($enableDeploymentUpgrade = 0) или путем передачи *- enableDeploymentUpgrade 0* как параметр, который изменяет поведение toofirst сценарий удаления любого существующего развертывания, а затем создать новое развертывание.

   > [!IMPORTANT]
   > сценарий Hello всегда удалит или замене существующих развертываний по умолчанию, если они обнаружены. Это необходимо для включения непрерывной доставки из автоматизации, где невозможно вмешательство пользователя или оператора.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5. Публикация пакета с помощью TFS Team Build
Этот необязательный шаг подключается TFS Team Build toohello сценарий, созданный на шаге 4, обрабатывающего публикации tooAzure построения пакета hello. Влечет за собой изменение hello шаблон процесса используется в определении построения, чтобы он выполняет действие публикации, в конце hello hello рабочего процесса. Hello действия публикации будет запустите команду PowerShell передача в параметры из сборки hello. Должен быть выведен hello MSBuild предназначен и публикации скриптов выходные данные в выходные данные построения Стандартная hello.

1. Изменить определение построения, отвечающий за hello непрерывного развертывания.
2. Выберите hello **процесс** вкладки.
3. Выполните [эти инструкции](http://msdn.microsoft.com/library/dd647551.aspx) tooadd проекта действия для hello шаблон процесса сборки, загрузить шаблон по умолчанию hello, добавьте его в проект hello и вернуть его на сервер. Предоставьте новое имя, например AzureBuildProcessTemplate hello шаблон процесса сборки.
4. Вернуть toohello **процесс** вкладку и использовать **Показать подробности** tooshow список шаблонов процесса сборки. Выберите hello **создать...**  кнопку и перейдите toohello проекта только что добавленный и возврата. Найдите только что созданный шаблон hello и выберите **ОК**.
5. Откройте hello выбранного шаблона процесса для редактирования. Можно открыть непосредственно в конструкторе рабочих процессов hello или hello toowork редактор XML с hello XAML.
6. Добавьте следующие список новые аргументы в виде отдельных элементов строки на вкладке hello аргументы конструктора рабочих процессов hello hello. Все аргументы должны иметь параметры direction=In и type=String. Они будут используется tooflow параметров из определения построения hello в рабочем процессе hello, которой затем используется toocall hello get скрипта публикации.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Список аргументов][3]

   Привет, соответствующий XAML выглядит следующим образом:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Добавьте новую последовательность в конце hello выполнение в агенте:

   1. Начните с добавления toocheck действия оператора If для является допустимым файлом сценария. Задайте значение toothis hello условия:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Затем в hello регистр hello оператора If, добавьте новое действие последовательности. Отображаемое имя набора hello too'Start публикации "
   3. С начала публикации последовательности по-прежнему выбран hello добавьте приведенный ниже перечень новые переменные как отдельные элементы строки на вкладке "переменные" hello конструктора рабочих процессов. Все переменные должны иметь тип String и Scope=Start publish. Они будут используется tooflow параметров из определения построения hello в рабочий процесс, которой затем используется toocall hello get скрипта публикации.

      * SubscriptionDataFilePath типа String.
      * PublishScriptFilePath типа String.

        ![Новые переменные][4]
   4. Если вы используете TFS 2012 или более ранней версии, добавить действие ConvertWorkspaceItem в начале hello hello новой последовательности. Если вы используете TFS 2013 или более поздней версии, добавить действие GetLocalPath в начале hello hello новой последовательности. Для ConvertWorkspaceItem свойства hello следующим образом: направление = ServerToLocal DisplayName = «Convert опубликовать имя файла сценария,» входные данные = «PublishScriptLocation», результат = рабочей области «PublishScriptFilePath» = «Рабочую область». Для операции GetLocalPath задать too'PublishScriptLocation IncomingPath свойство hello ", и результат too'PublishScriptFilePath hello". Это действие преобразует hello путь toohello публикации скрипта из расположения сервера TFS (если применимо) путь tooa стандартного локального диска.
   5. Если вы используете TFS 2012 или более ранней версии, добавьте еще одно действие ConvertWorkspaceItem конце hello hello новой последовательности. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. Если вы используете TFS 2013 или более позднюю версию, добавьте еще одно действие GetLocalPath. IncomingPath='SubscriptionDataFileLocation' и Result='SubscriptionDataFilePath.'
   6. Добавить действие InvokeProcess конце hello hello новой последовательности.
      Это действие вызовы PowerShell.exe, с аргументами hello переданный hello определения сборки.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Выполнение сценария публикации
      + FileName = «PowerShell» (используйте кавычки hello)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. В hello **обработать стандартный вывод** статьи текстового поля из InvokeProcess, задайте значение too'data hello текстовое поле ". Это стандартный вывод данных переменной toostore hello.
   8. Добавить действие WriteBuildMessage под hello **обработать стандартный вывод** раздела. Задать важность hello = «Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High» и сообщение hello = «данные». Это гарантирует, что hello стандартные выходные данные сценария будут записанных toohello выходные данные построения.
   9. В hello **обработать вывод ошибки** статьи текстового поля из InvokeProcess, задайте значение too'data hello текстовое поле ". Это стандартная ошибка данных переменной toostore hello.
   10. Добавить действие WriteBuildError под hello **обработать вывод ошибки** раздела. Задать сообщение hello = «данные». Это гарантирует, что hello стандартной погрешности hello скрипта будет получить запись toohello вывод ошибок построения.
   11. Исправьте все ошибки, отмеченные синими восклицательными знаками. Наведите указатель мыши tooget восклицательных знаков подсказку об ошибке hello. Сохраните hello рабочего процесса, чтобы очистить ошибки.

   конечным результатом Hello hello публикации действий будет выглядеть следующим образом в конструкторе hello рабочего процесса:

   ![Действия рабочего процесса][5]

   конечный результат Hello hello опубликовать рабочий процесс, который действий в XAML будет выглядеть следующим образом:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Сохранение шаблона процесса построения hello и проверять в этом файле.
9. Измените определение сборки hello (Закрыть его, если он открыт) и выберите hello **New** кнопку, если вы еще не видите hello новый шаблон в списке hello шаблонов процессов.
10. Задайте значения свойств параметров hello в разделе Прочее hello следующим образом:

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *Это значение является производным от: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *Это значение является производным от: ($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = «mycloudservicename» *используйте hello соответствующее имя облачной службы здесь*
    5. Environment = 'Staging'
    6. StorageAccountName = «mystorageaccountname» *имя учетной записи хранилища, соответствующий hello используйте здесь*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![Значения свойств параметров][6]
11. Сохраните изменения hello toohello определения сборки.
12. Очередь tooexecute сборки, оба hello номер сборки пакета и публикации. Если задать tooContinuous интеграции триггер, это поведение будет выполняться на каждом возврате.

### <a name="publishcloudserviceps1-script-template"></a>Шаблон сценария PublishCloudService.ps1
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Дальнейшие действия
tooenable удаленную отладку при использовании непрерывной поставки разделе [включить удаленную отладку при использовании непрерывной поставки toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
