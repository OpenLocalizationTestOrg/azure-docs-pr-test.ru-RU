---
title: "aaaGet работы с Python и облачных служб Azure | Документы Microsoft"
description: "Общие сведения об использовании средства Python для Visual Studio toocreate Azure облачных служб, включая веб-ролей и рабочих ролей."
services: cloud-services
documentationcenter: python
author: thraka
manager: timlt
editor: 
ms.assetid: 5489405d-6fa9-4b11-a161-609103cbdc18
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: f5fd85e754839f146abe912351c59dc4a148c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="python-web-and-worker-roles-with-python-tools-for-visual-studio"></a>Использование веб-ролей и рабочих ролей Python с помощью средств Python для Visual Studio

В этой статье представлен обзор способов использования веб-ролей и рабочих ролей Python с помощью [инструментов Python для Visual Studio][Python Tools for Visual Studio]. Узнайте, как toocreate toouse Visual Studio и развертывать основные облачные службы, использующей Python.

## <a name="prerequisites"></a>Предварительные требования
* [Visual Studio 2013, 2015 или 2017](https://www.visualstudio.com/)
* [Инструменты Python для Visual Studio][Python Tools for Visual Studio] (PTVS)
* [Инструменты пакета SDK для Azure для VS 2013][Azure SDK Tools for VS 2013] или  
[Инструменты пакета SDK для Azure для VS 2015][Azure SDK Tools for VS 2015] или  
[Инструменты пакета SDK для Azure для VS 2017][Azure SDK Tools for VS 2017]
* [Python 2.7 (32-разрядная версия)][Python 2.7 32-bit] или [Python 3.5 (32-разрядная версия)][Python 3.5 32-bit]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-are-python-web-and-worker-roles"></a>Что такое веб-роли и рабочие роли Python?
Azure предоставляет три вычислительные модели запуска приложений: [веб-приложения в службе приложений Azure][execution model-web sites], [виртуальные машины Azure][execution model-vms] и [облачные службы Azure][execution model-cloud services]. Все три модели поддерживают Python. Облачные службы, которые включают в себя веб-роли и рабочие роли, предоставляют *платформу как службу (PaaS)*. В облачной службе веб-роли предоставляет выделенный Internet Information Services (IIS) web server toohost внешнего интерфейса веб-приложений, во время рабочей роли могут выполнять асинхронные, длительные или постоянные задачи зависят от взаимодействия с пользователем или входные данные.

Дополнительные сведения см. в разделе [Информация об облачных службах].

> [!NOTE]
> *Ищете простой веб-сайт toobuild?*
> Если ваш сценарий включает в себя только клиентскую часть простого веб-сайта, рассмотрите возможность использования hello простую функцию веб-приложений в службе приложений Azure. При расширении веб-сайта, что изменение требований, могут выполнять обновление tooa облачной службы. В разделе hello <a href="/develop/python/">центре разработчиков Python</a> для статей, посвященных разработки функции hello веб-приложений в службе приложений Azure.
> <br />
> 
> 

## <a name="project-creation"></a>Создание проекта
В Visual Studio можно выбрать **облачной службы Azure** в hello **новый проект** диалогового **Python**.

![Диалоговое окно "Новый проект"](./media/cloud-services-python-ptvs/new-project-cloud-service.png)

В мастере hello облачной службы Azure можно создать новый веб- и рабочих ролей.

![Диалоговое окно Облачной службы Azure](./media/cloud-services-python-ptvs/new-service-wizard.png)

Hello рабочей роли шаблон содержит стандартный код tooconnect tooan учетной записи хранилища Azure или шины обслуживания Azure.

![Решение для Облачной службы](./media/cloud-services-python-ptvs/worker.png)

Можно добавить веб- и рабочих ролей tooan существующей облачной службы в любое время.  Можно выбрать tooadd существующие проекты в решении или создавать новые.

![Команда добавления роли](./media/cloud-services-python-ptvs/add-new-or-existing-role.png)

В облачной службе могут присутствовать роли, реализованные на различных языках программирования.  Например, это может быть веб-роль на Python, реализованная с помощью Django, с рабочими ролями на Python или C#.  С помощью очередей служебной шины или очередей хранилища можно легко обмениваться данными между ролями.

## <a name="install-python-on-hello-cloud-service"></a>Установка Python на hello облачной службы
> [!WARNING]
> сценарии установки Hello, которые устанавливаются вместе с Visual Studio (во время hello последнего обновления в этой статье) не работают. В этом разделе описывается обходное решение.
> 
> 

Основная проблема Hello сценариев установки hello — что не устанавливать python. Во-первых, определите два [задачи запуска](cloud-services-startup-tasks.md) в hello [ServiceDefinition.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) файла. Первая задача Hello (**PrepPython.ps1**) загружает и устанавливает среды выполнения Python hello. Вторая задача Hello (**PipInstaller.ps1**) выполняется tooinstall PIP-адрес может иметь зависимости.

Привет, следующие сценарии были написаны для различных версий Python 3.5. Если требуется, чтобы toouse hello версии 2.x Python, набор hello **PYTHON2** переменной файл слишком**на** для hello два запуска задач и задач среды выполнения hello: `<Variable name="PYTHON2" value="<mark>on</mark>" />`.

```xml
<Startup>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>
  </Task>

  <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
    <Environment>
      <Variable name="EMULATED">
        <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
      </Variable>
      <Variable name="PYTHON2" value="off" />
    </Environment>

  </Task>

</Startup>
```

Hello **PYTHON2** и **PYPATH** переменных должны быть добавлены toohello Рабочая задача запуска. Hello **PYPATH** переменная используется только в том случае, если hello **PYTHON2** переменной задано слишком**на**.

```xml
<Runtime>
  <Environment>
    <Variable name="EMULATED">
      <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
    </Variable>
    <Variable name="PYTHON2" value="off" />
    <Variable name="PYPATH" value="%SystemDrive%\Python27" />
  </Environment>
  <EntryPoint>
    <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
  </EntryPoint>
</Runtime>
```

#### <a name="sample-servicedefinitioncsdef"></a>Пример файла ServiceDefinition.csdef
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="AzureCloudServicePython" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
      <Setting name="Python2" />
    </ConfigurationSettings>
    <Startup>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PrepPython.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
      <Task executionContext="elevated" taskType="simple" commandLine="bin\ps.cmd PipInstaller.ps1">
        <Environment>
          <Variable name="EMULATED">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
          <Variable name="PYTHON2" value="off" />
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="EMULATED">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
        </Variable>
        <Variable name="PYTHON2" value="off" />
        <Variable name="PYPATH" value="%SystemDrive%\Python27" />
      </Environment>
      <EntryPoint>
        <ProgramEntryPoint commandLine="bin\ps.cmd LaunchWorker.ps1" setReadyOnProcessStart="true" />
      </EntryPoint>
    </Runtime>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
  </WorkerRole>
</ServiceDefinition>
```



Создайте hello **PrepPython.ps1** и **PipInstaller.ps1** файлы в hello **. / bin** папке роли.

#### <a name="preppythonps1"></a>Файл PrepPython.ps1
Скрипт в этом файле устанавливает Python. Если hello **PYTHON2** слишком задана переменная среды**на**, то устанавливается Python 2.7, в противном случае устанавливается Python 3.5.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if python is installed...$nl"
    if ($is_python2) {
        & "${env:SystemDrive}\Python27\python.exe"  -V | Out-Null
    }
    else {
        py -V | Out-Null
    }

    if (-not $?) {

        $url = "https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe"
        $outFile = "${env:TEMP}\python-3.5.2-amd64.exe"

        if ($is_python2) {
            $url = "https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64.msi"
            $outFile = "${env:TEMP}\python-2.7.12.amd64.msi"
        }

        Write-Output "Not found, downloading $url too$outFile$nl"
        Invoke-WebRequest $url -OutFile $outFile
        Write-Output "Installing$nl"

        if ($is_python2) {
            Start-Process msiexec.exe -ArgumentList "/q", "/i", "$outFile", "ALLUSERS=1" -Wait
        }
        else {
            Start-Process "$outFile" -ArgumentList "/quiet", "InstallAllUsers=1" -Wait
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Already installed"
    }
}
```

#### <a name="pipinstallerps1"></a>Файл PipInstaller.ps1
Этот скрипт вызывает копирование pip и устанавливает все зависимости hello в hello **requirements.txt** файла. Если hello **PYTHON2** слишком задана переменная среды**на**, то используется Python 2.7, в противном случае используется Python 3.5.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated){
    Write-Output "Checking if requirements.txt exists$nl"
    if (Test-Path ..\requirements.txt) {
        Write-Output "Found. Processing pip$nl"

        if ($is_python2) {
            & "${env:SystemDrive}\Python27\python.exe" -m pip install -r ..\requirements.txt
        }
        else {
            py -m pip install -r ..\requirements.txt
        }

        Write-Output "Done$nl"
    }
    else {
        Write-Output "Not found$nl"
    }
}
```

#### <a name="modify-launchworkerps1"></a>Изменение файла LaunchWorker.ps1
> [!NOTE]
> В случае hello **рабочей роли** проекта, **LauncherWorker.ps1** файл является файлом запуска требуется tooexecute hello. В **веб-роли** проекта, hello загрузочный файл вместо этого определяется в свойствах проекта hello.
> 
> 

Hello **bin\LaunchWorker.ps1** toodo много подготовки работать, но он не работает действительно был создан. Замените содержимое hello в этом файле hello, выполнив сценарий.

Этот скрипт вызывает hello **worker.py** файл из проекта python. Если hello **PYTHON2** слишком задана переменная среды**на**, то используется Python 2.7, в противном случае используется Python 3.5.

```powershell
$is_emulated = $env:EMULATED -eq "true"
$is_python2 = $env:PYTHON2 -eq "on"
$nl = [Environment]::NewLine

if (-not $is_emulated)
{
    Write-Output "Running worker.py$nl"

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
else
{
    Write-Output "Running (EMULATED) worker.py$nl"

    # Customize tooyour local dev environment

    if ($is_python2) {
        cd..
        iex "$env:PYPATH\python.exe worker.py"
    }
    else {
        cd..
        iex "py worker.py"
    }
}
```

#### <a name="pscmd"></a>Файл ps.cmd
шаблоны Visual Studio Hello должен быть создан **ps.cmd** файла в hello **. / bin** папки. Этот сценарий вызывает выше сценарии оболочки hello PowerShell и обеспечивает ведение журналов на основе имени hello вызывается оболочки PowerShell hello. Если этот файл не создан, вот данные, которые должны в нем содержаться: 

```bat
@echo off

cd /D %~dp0

if not exist "%DiagnosticStore%\LogFiles" mkdir "%DiagnosticStore%\LogFiles"
%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Unrestricted -File %* >> "%DiagnosticStore%\LogFiles\%~n1.txt" 2>> "%DiagnosticStore%\LogFiles\%~n1.err.txt"
```



## <a name="run-locally"></a>Локальный запуск
Если установить проекта облачной службы как запускаемый проект hello и нажмите клавишу F5, hello облачная служба выполняется в локальный эмулятор Azure hello.

Несмотря на то, что PTVS поддерживает запуск в эмуляторе hello, отладка (например, точки останова) не работает.

toodebug рабочих и веб-роли, можно задать проект роли hello hello запускаемым проектом и отладки, чтобы вместо.  В качестве запускаемых при включении можно указать несколько проектов.  Щелкните правой кнопкой мыши решение hello, а затем выберите **назначить запускаемые проекты**.

![Свойства запускаемого при включении проекта в решении](./media/cloud-services-python-ptvs/startup.png)

## <a name="publish-tooazure"></a>Публикация tooAzure
toopublish, щелкните правой кнопкой мыши проект облачной службы hello в решении hello, а затем выберите **публикации**.

![Вход для публикации в Microsoft Azure](./media/cloud-services-python-ptvs/publish-sign-in.png)

Выполните мастер hello. При необходимости включите удаленный рабочий стол. Удаленный рабочий стол полезно в том случае, если нужно toodebug что-то.

После завершения настройки параметров щелкните **Опубликовать**.

Некоторые ход выполнения отображается в окне вывода hello, то появится окно hello журнал действий Microsoft Azure.

![Окно журнала действий Microsoft Azure](./media/cloud-services-python-ptvs/publish-activity-log.png)

Развертывание принимает toocomplete несколько минут, затем веб-и/или запуск рабочих ролей в Azure!

### <a name="investigate-logs"></a>Изучение журналов
После hello облачной службы виртуальная машина запускается и устанавливает Python, можно просмотреть журналы toofind hello наличие сообщений о сбое. Эти журналы расположены в hello **C:\Resources\Directory\\\LogFiles {роль}** папки. **PrepPython.err.txt** содержит по крайней мере одна ошибка, то из при hello скрипт пытается toodetect, если установлены Python и **PipInstaller.err.txt** может жалуются устаревшей версией PIP-адрес.

## <a name="next-steps"></a>Дальнейшие действия
Более подробные сведения о работе с веб- и рабочих ролей в средства Python для Visual Studio см. в документации PTVS hello:

* [Azure Cloud Service Projects for Python][Cloud Service Projects] (Проекты для облачной службы Azure для Python)

Дополнительные сведения об использовании служб Azure из рабочих и веб-роли, например с помощью хранилища Azure или Service Bus см. следующие статьи hello.

* [Использование хранилища больших двоичных объектов Azure из Python][Blob Service]
* [Использование табличного хранилища из Python][Table Service]
* [Использование хранилища очередей из Python][Queue Service]
* [Как использовать очереди служебной шины][Service Bus Queues]
* [Как использовать разделы и подписки служебной шины][Service Bus Topics]

<!--Link references-->

[Информация об облачных службах]: cloud-services-choose-me.md
[execution model-web sites]: ../app-service-web/app-service-web-overview.md
[execution model-vms]:../virtual-machines/windows/overview.md
[execution model-cloud services]: cloud-services-choose-me.md
[Python Developer Center]: /develop/python/

[Blob Service]:../storage/blobs/storage-python-how-to-use-blob-storage.md
[Queue Service]: ../storage/queues/storage-python-how-to-use-queue-storage.md
[Table Service]:../cosmos-db/table-storage-how-to-use-python.md
[Service Bus Queues]: ../service-bus-messaging/service-bus-python-how-to-use-queues.md
[Service Bus Topics]: ../service-bus-messaging/service-bus-python-how-to-use-topics-subscriptions.md


<!--External Link references-->

[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure SDK Tools for VS 2013]: http://go.microsoft.com/fwlink/?LinkId=746482
[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=746481
[Azure SDK Tools for VS 2017]: http://go.microsoft.com/fwlink/?LinkId=746483
[Python 2.7 32-bit]: https://www.python.org/downloads/
[Python 3.5 32-bit]: https://www.python.org/downloads/
