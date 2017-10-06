---
title: "задачи запуска aaaCommon для облачных служб | Документы Microsoft"
description: "Некоторые примеры типичных задач запуска можно tooperform в облако службы веб-роли или рабочей роли."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a>Стандартные задачи запуска в облачной службе
В этой статье приведены некоторые примеры типичных задач запуска вы можете tooperform в облачной службе. Можно использовать операции tooperform запуска задачи до запуска роли. Операции, вы можете tooperform включают установки компонента, регистрация компонентов COM, установка разделов реестра или запуск длительного процесса. 

В разделе [в этой статье](cloud-services-startup-tasks.md) toounderstand работа задач запуска, и в частности как toocreate hello записей, которые определяют задачу запуска.

> [!NOTE]
> При запуске задачи не машины tooVirtual применимо, только tooCloud Service Web и рабочих ролей.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Определение переменных среды до запуска роли
Переменные среды, заданные для конкретных задач, используйте hello [среды] элемент внутри hello [задачи] элемента.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Можно также использовать переменные [допустимое значение Azure XPath](cloud-services-role-config-xpath.md) tooreference что-нибудь о развертывании hello. Вместо использования hello `value` атрибута, следует определить [RoleInstanceValue] дочерний элемент.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Настройка запуска IIS с помощью AppCmd.exe
Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) средство командной строки может быть параметров IIS используется toomanage при запуске в Azure. *AppCmd.exe* предоставляет удобный доступ командной строки tooconfiguration параметры для использования в задачах запуска в Azure. С помощью *AppCmd.exe*можно добавить, изменить или удалить параметры веб-сайта для приложений и сайтов.

Однако существует несколько вещей toowatch out для использования hello в *AppCmd.exe* качестве задачи запуска:

* Задачи запуска могут несколько раз выполняться между перезагрузками. Например, при перезапуске роли.
* Если действие *AppCmd.exe* выполняется несколько раз, может произойти ошибка. Например, попытка tooadd раздел слишком*Web.config* дважды приведет к ошибке.
* Задачи запуска завершаются ошибкой, если они возвращают ненулевой код выхода или **errorlevel**. Например, если *AppCmd.exe* выдает ошибку.

Он является хорошей практикой toocheck hello **errorlevel** после вызова *AppCmd.exe*, это просто toodo, если вызов Привет упаковкой слишком*AppCmd.exe* с *.cmd*  файла. При обнаружении известного ответа **errorlevel** его можно пропустить или вернуть.

Здравствуйте, errorlevel, возвращенных *AppCmd.exe* перечислены в файле winerror.h hello, а также можно увидеть на [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Пример управления уровень ошибки hello
В этом примере добавляется раздел сжатия и запись сжатия для JSON toohello *Web.config* файл, а обработка ошибок и ведение журнала.

Здравствуйте, соответствующие разделы hello [ServiceDefinition.csdef] показаны ниже, включая задание hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) атрибут слишком`elevated` toogive *AppCmd.exe*  необходимых настроек разрешений toochange hello в hello *Web.config* файла:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

Hello *Startup.cmd* пакетного файла используется *AppCmd.exe* tooadd раздел сжатия и запись сжатия для JSON toohello *Web.config* файла. Ожидается Hello **errorlevel** 183 приравнивается toozero hello УБЕДИТЕСЬ с помощью. EXE-файла программы командной строки. Непредвиденные errorlevels являются tooStartupErrorLog.txt журнала.

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a>Добавление правил брандмауэра
Фактически в Azure есть два брандмауэра. Hello брандмауэр управляет соединениями между виртуальной машиной hello и hello за пределами системы. Этот брандмауэр управляется hello [конечные точки] элемент в hello [ServiceDefinition.csdef] файла.

Hello другой брандмауэр управляет соединениями между виртуальной машиной hello и процессы hello в этой виртуальной машине. Брандмауэр может управляться hello `netsh advfirewall firewall` средство командной строки.

Azure создает правила брандмауэра для hello процессов, запущенных с помощью ролей. Например при запуске службы или программы, Azure автоматически создает tooallow правила брандмауэра, необходимые hello toocommunicate этой службы с hello Интернета. Однако, если создать службу, которая запускается процессом вне роли (например, службы COM + или запланированную задачу), необходимо toomanually создать службу toothat доступа tooallow правила брандмауэра. Эти правила брандмауэра можно создавать с помощью задачи запуска.

У задачи запуска, которая создает правило брандмауэра, должен быть [executionContext][задачи] со значением **elevated**. Добавить hello после запуска задачи toohello [ServiceDefinition.csdef] файла.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

правило брандмауэра hello tooadd, необходимо использовать соответствующий hello `netsh advfirewall firewall` команды в пакетном файле запуска. В этом примере hello задачи запуска требуется безопасность и шифрование для TCP-порт 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Блокирование определенного IP-адреса
Вы можете ограничить доступ tooa Azure web роли набором указанных IP-адресов, изменяя служб IIS **web.config** файла. Необходимо также toouse командный файл, разблокирующий hello **ipSecurity** раздел hello **ApplicationHost.config** файла.

toodo разблокировать hello **ipSecurity** раздел hello **ApplicationHost.config** создайте командный файл, который выполняется при запуске роли. Создайте папку на корневом уровне hello вызывается веб-роли **запуска** и в этой папке создайте пакетный файл под названием **startup.cmd**. Добавьте проект Visual Studio tooyour этот файл и задайте свойства hello слишком**всегда Копировать** tooensure, что она включена в пакет.

Добавить hello после запуска задачи toohello [ServiceDefinition.csdef] файла.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

Добавление этой команды toohello **startup.cmd** файла:

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Эта задача заставляет hello **startup.cmd** пакетного файла toobe выполнять каждый раз при инициализации hello веб-роли, обеспечивая hello, что необходимые **ipSecurity** разблокирован раздел.

Наконец, измените hello [раздел System.WebServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) веб-роли **web.config** файл tooadd список IP-адресов, которым предоставлен доступ, как показано в следующий пример hello:

Этот образец настройки **позволяет** все IP-адреса tooaccess hello server за исключением двух определенных hello

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

Этот образец настройки **запрещает** все IP-адреса по доступу к серверу hello, за исключением двух определенных hello.

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a>Создание задачи запуска PowerShell
Скрипты Windows PowerShell нельзя вызывать непосредственно из hello [ServiceDefinition.csdef] файл, но они могут быть вызваны из пакетного файла запуска.

PowerShell по умолчанию не запускает неподписанные сценарии. Если вы подписываете сценарий, требуется tooconfigure PowerShell toorun неподписанные сценарии. toorun неподписанные сценарии, hello **ExecutionPolicy** необходимо задать слишком**Unrestricted**. Hello **ExecutionPolicy** параметр зависит от версии Windows PowerShell hello.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Если вы используете гостевой ОС, которая работает PowerShell 2.0 или 1.0 можно принудительно toorun версии 2, а если эта кнопка недоступна, используется версия 1.

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Создание файлов в локальном хранилище из задачи запуска
Можно использовать локальное хранилище ресурсов toostore файлов, созданных при последующем доступе к приложению задачи запуска.

toocreate Здравствуйте локального ресурса хранилища, добавьте [LocalResources] toohello раздел [ServiceDefinition.csdef] файл и затем добавить hello [LocalStorage] дочерний элемент. Предоставьте ресурс локального хранилища hello уникальное имя и соответствующий размер для задачи запуска.

toouse ресурс локального хранилища в задаче запуска необходимо toocreate среды переменной tooreference hello расположение локального ресурса хранилища. Затем hello задачи запуска и приложение hello может tooread и записи файлов toohello локального ресурса хранилища.

Здравствуйте, соответствующие разделы hello **ServiceDefinition.csdef** показаны ниже:

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

Например это **Startup.cmd** пакетный файл использует hello **PathToStartupStorage** файла hello toocreate переменной среды **MyTest.txt** в локальном хранилище hello расположение.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Локальное хранилище папки доступен с hello Azure SDK с помощью hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) метод.

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Запустить в эмуляторе hello или облака
Возможно выполнение различных действий при работе в toowhen облаке, в отличие hello в эмуляторе вычислений hello, задача запуска. Например может потребоваться toouse новую копию данных SQL, только при выполнении в эмуляторе hello. Или вы можете toodo некоторые оптимизации производительности для облака hello, что нет необходимости toodo при выполнении в эмуляторе hello.

Это возможность tooperform различные действия на hello эмулятор вычислений и hello облаке реализуется путем создания переменной среды в hello [ServiceDefinition.csdef] файла. Затем переменная проверяется в задаче запуска.

переменная среды toocreate hello, добавить hello [переменной]/[RoleInstanceValue] элемент и создать значение XPath `/RoleEnvironment/Deployment/@emulated`. Здравствуйте, значение hello **% ComputeEmulatorRunning %** переменная среды `true` при выполнении в эмуляторе вычислений hello, и `false` при выполнении в облаке hello.

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

Задача Hello, теперь можно проверить hello **% ComputeEmulatorRunning %** различных действий среды переменной tooperform зависимости от того, работает ли роли hello в hello облачной или hello эмулятора. Вот CMD-файл сценария оболочки для проверки этой переменной среды.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Обнаружение запуска задачи
Hello роли может перезапустить без перезагрузки снова вызывает вашей toorun задачи запуска. Нет не tooindicate флаг, который задача уже был запущен на размещение виртуальных Машин hello. Возможно, для некоторых задач не важно, сколько раз они выполняются. Тем не менее можно запустить в ситуации, когда необходимо tooprevent задачи запуска несколько раз.

Простейший способ toodetect Hello, задача уже выполнена является toocreate файл в hello **% TEMP %** папки при успешной задачу hello и просмотрите hello для его запуска задачи «hello». Ниже приведен пример CMD-файла сценария оболочки, который это делает.

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a>Рекомендации по задачам
Ниже приведены некоторые рекомендации, которые необходимо выполнять при настройке задачи для рабочей роли или веб-роли.

### <a name="always-log-startup-activities"></a>Всегда ведите журнал операций запуска
Visual Studio не предоставляет toostep отладчик выполнения пакетных файлов, поэтому очень хорошо tooget объема данных hello операции пакетных файлов, как можно. Ведение журнала выходных данных пакетных файлов, hello и **stdout** и **stderr**, можно предоставить вам важную информацию, при попытке toodebug и исправления пакетных файлов. toolog оба **stdout** и **stderr** toohello файл StartupLog.txt hello указывает tooby directory hello **% TEMP %** переменной среды, добавьте текст hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello конец конкретной строки, вы хотите toolog. Например, tooexecute setup.exe в hello **% PathToApp1Install %** каталога:

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify xml, можно создать оболочку *cmd* файла, который вызывает все загрузочного задачи, а также ведение журнала и гарантирует общих папок каждая дочерняя задача hello же переменных среды.

Может оказаться менее раздражающих toouse `>> "%TEMP%\StartupLog.txt" 2>&1` на конце hello каждой задачи запуска. Чтобы настроить принудительную регистрацию задач, можно создать оболочку, которая выполняет ведение журнала автоматически. Эта оболочка вызывает hello реальные пакетный файл, требуется toorun. Любые выходные данные hello целевой пакетный файл будет перенаправленный toohello *Startuplog.txt* файла.

Привет, в следующем примере показано, как tooredirect все выходные данные из пакетного файла запуска. В этом примере hello файл ServerDefinition.csdef создает задачу запуска, который вызывает *logwrap.cmd*. *logwrap.cmd* вызовы *Startup2.cmd*, перенаправляя весь вывод слишком**% TEMP %\\StartupLog.txt**.

ServiceDefinition.cmd:

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd:**

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

**Startup2.cmd:**

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

Пример выходных данных в hello **StartupLog.txt** файла:

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Hello **StartupLog.txt** файл находится в hello *C:\Resources\temp\\\RoleTemp {идентификатор роли}* папки.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Правильная настройка executionContext для задач запуска
Задать привилегии, необходимые для запуска задачи hello. Иногда задачи запуска должны работать с повышенными привилегиями, даже если роль hello выполняется с обычным уровнем привилегий.

Hello [executionContext][задачи] атрибут задает уровень прав доступа задачи запуска hello hello. С помощью `executionContext="limited"` означает имеет задачу запуска hello hello одинаковом уровне привилегий, как роль hello. С помощью `executionContext="elevated"` означает задачи запуска hello имеет права администратора, что позволяет hello запуска задач администратора tooperform задачи без предоставления прав tooyour роли администратора.

Пример задачи запуска, которая требует повышенных прав доступа — задача запуска, который использует **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** требуется `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Используйте подходящий taskType hello
Hello [taskType][задачи] атрибут определяет, выполняется задача запуска hello hello способом. Он имеет три значения: **simple**, **background** и **foreground**. Hello задачи фона и переднего плана запускаются асинхронно, а затем hello простые задачи выполняются синхронно по одному.

С **простой** задачи запуска можно задать порядок hello в которой запускаются задачи hello hello порядок, в которой hello задачи перечислены в файле ServiceDefinition.csdef hello. Если **простой** задача завершается с ненулевым код выхода, а затем hello останавливается процедуры запуска и hello роль не запускается.

Здравствуйте разницу между **фона** задачи запуска и **переднего плана** том, что **переднего плана** задачи сохранить hello роли выполняется до hello  **передний план** завершения задачи. Это также означает, что если hello **переднего плана** задач зависает или дает сбой, hello роль не обновляется до hello **переднего плана** задача принудительно закрыто. По этой причине **фона** рекомендуется использовать для асинхронных задач запуска, если не требуется эта функция hello **переднего плана** задачи.

### <a name="end-batch-files-with-exit-b-0"></a>Завершайте пакетные файлы командой EXIT /B 0
Hello роль будет запускать, только если hello **errorlevel** от каждого вашего простого запуска задач равно нулю. Не все программы устанавливают hello **errorlevel** (код завершения) правильно, поэтому hello пакетного файла должно заканчиваться `EXIT /B 0` Если все, что выполнена правильно.

Недостающий `EXIT /B 0` hello конец пакетного файла запуска является распространенной причиной роли, которые не запускаются.

> [!NOTE]
> Замечено, вложенные пакетные файлы иногда зависания при использовании hello `/B` параметра. Вы можете убедиться, что проблема зависания не произойдет при другой пакетный файл вызывает текущий пакетный файл, например при использовании hello toomake [оболочки журнала](#always-log-startup-activities). Можно опустить hello `/B` параметра в данном случае.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Ожидается, что при запуске задачи toorun более одного раза
Не все перезапуски роли включают в себя перезагрузку, но все они вызывают выполнение всех задач запуска. Это означает, что задачи запуска должны быть toorun может несколько раз между перезагрузками без проблем. Это описано в hello [предшествующий раздел](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Использовать локальное хранилище toostore файлы, которые должны быть доступны в роли hello
Если toocopy или создайте файл во время задачи запуска, затем доступны tooyour роли, то этот файл должен быть размещен в локальном хранилище. В разделе hello [предшествующий раздел](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите hello облака [модели и пакета службы](cloud-services-model-and-package.md)

Узнайте, как работают [задачи](cloud-services-startup-tasks.md) .

[Создайте и разверните](cloud-services-how-to-create-deploy-portal.md) свой пакет облачной службы.

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[задачи]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[среды]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[переменной]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[EndPoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
