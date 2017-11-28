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
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="abd39-103">Стандартные задачи запуска в облачной службе</span><span class="sxs-lookup"><span data-stu-id="abd39-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="abd39-104">В этой статье приведены некоторые примеры типичных задач запуска вы можете tooperform в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="abd39-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="abd39-105">Можно использовать операции tooperform запуска задачи до запуска роли.</span><span class="sxs-lookup"><span data-stu-id="abd39-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="abd39-106">Операции, вы можете tooperform включают установки компонента, регистрация компонентов COM, установка разделов реестра или запуск длительного процесса.</span><span class="sxs-lookup"><span data-stu-id="abd39-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="abd39-107">В разделе [в этой статье](cloud-services-startup-tasks.md) toounderstand работа задач запуска, и в частности как toocreate hello записей, которые определяют задачу запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="abd39-108">При запуске задачи не машины tooVirtual применимо, только tooCloud Service Web и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="abd39-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="abd39-109">Определение переменных среды до запуска роли</span><span class="sxs-lookup"><span data-stu-id="abd39-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="abd39-110">Переменные среды, заданные для конкретных задач, используйте hello [среды] элемент внутри hello [задачи] элемента.</span><span class="sxs-lookup"><span data-stu-id="abd39-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

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

<span data-ttu-id="abd39-111">Можно также использовать переменные [допустимое значение Azure XPath](cloud-services-role-config-xpath.md) tooreference что-нибудь о развертывании hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="abd39-112">Вместо использования hello `value` атрибута, следует определить [RoleInstanceValue] дочерний элемент.</span><span class="sxs-lookup"><span data-stu-id="abd39-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="abd39-113">Настройка запуска IIS с помощью AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="abd39-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="abd39-114">Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) средство командной строки может быть параметров IIS используется toomanage при запуске в Azure.</span><span class="sxs-lookup"><span data-stu-id="abd39-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="abd39-115">*AppCmd.exe* предоставляет удобный доступ командной строки tooconfiguration параметры для использования в задачах запуска в Azure.</span><span class="sxs-lookup"><span data-stu-id="abd39-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="abd39-116">С помощью *AppCmd.exe*можно добавить, изменить или удалить параметры веб-сайта для приложений и сайтов.</span><span class="sxs-lookup"><span data-stu-id="abd39-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="abd39-117">Однако существует несколько вещей toowatch out для использования hello в *AppCmd.exe* качестве задачи запуска:</span><span class="sxs-lookup"><span data-stu-id="abd39-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="abd39-118">Задачи запуска могут несколько раз выполняться между перезагрузками.</span><span class="sxs-lookup"><span data-stu-id="abd39-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="abd39-119">Например, при перезапуске роли.</span><span class="sxs-lookup"><span data-stu-id="abd39-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="abd39-120">Если действие *AppCmd.exe* выполняется несколько раз, может произойти ошибка.</span><span class="sxs-lookup"><span data-stu-id="abd39-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="abd39-121">Например, попытка tooadd раздел слишком*Web.config* дважды приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="abd39-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="abd39-122">Задачи запуска завершаются ошибкой, если они возвращают ненулевой код выхода или **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="abd39-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="abd39-123">Например, если *AppCmd.exe* выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="abd39-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="abd39-124">Он является хорошей практикой toocheck hello **errorlevel** после вызова *AppCmd.exe*, это просто toodo, если вызов Привет упаковкой слишком*AppCmd.exe* с *.cmd*  файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="abd39-125">При обнаружении известного ответа **errorlevel** его можно пропустить или вернуть.</span><span class="sxs-lookup"><span data-stu-id="abd39-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="abd39-126">Здравствуйте, errorlevel, возвращенных *AppCmd.exe* перечислены в файле winerror.h hello, а также можно увидеть на [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="abd39-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="abd39-127">Пример управления уровень ошибки hello</span><span class="sxs-lookup"><span data-stu-id="abd39-127">Example of managing hello error level</span></span>
<span data-ttu-id="abd39-128">В этом примере добавляется раздел сжатия и запись сжатия для JSON toohello *Web.config* файл, а обработка ошибок и ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="abd39-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="abd39-129">Здравствуйте, соответствующие разделы hello [ServiceDefinition.csdef] показаны ниже, включая задание hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) атрибут слишком`elevated` toogive *AppCmd.exe*  необходимых настроек разрешений toochange hello в hello *Web.config* файла:</span><span class="sxs-lookup"><span data-stu-id="abd39-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

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

<span data-ttu-id="abd39-130">Hello *Startup.cmd* пакетного файла используется *AppCmd.exe* tooadd раздел сжатия и запись сжатия для JSON toohello *Web.config* файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="abd39-131">Ожидается Hello **errorlevel** 183 приравнивается toozero hello УБЕДИТЕСЬ с помощью. EXE-файла программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="abd39-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="abd39-132">Непредвиденные errorlevels являются tooStartupErrorLog.txt журнала.</span><span class="sxs-lookup"><span data-stu-id="abd39-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

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

## <a name="add-firewall-rules"></a><span data-ttu-id="abd39-133">Добавление правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="abd39-133">Add firewall rules</span></span>
<span data-ttu-id="abd39-134">Фактически в Azure есть два брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="abd39-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="abd39-135">Hello брандмауэр управляет соединениями между виртуальной машиной hello и hello за пределами системы.</span><span class="sxs-lookup"><span data-stu-id="abd39-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="abd39-136">Этот брандмауэр управляется hello [конечные точки] элемент в hello [ServiceDefinition.csdef] файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="abd39-137">Hello другой брандмауэр управляет соединениями между виртуальной машиной hello и процессы hello в этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="abd39-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="abd39-138">Брандмауэр может управляться hello `netsh advfirewall firewall` средство командной строки.</span><span class="sxs-lookup"><span data-stu-id="abd39-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="abd39-139">Azure создает правила брандмауэра для hello процессов, запущенных с помощью ролей.</span><span class="sxs-lookup"><span data-stu-id="abd39-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="abd39-140">Например при запуске службы или программы, Azure автоматически создает tooallow правила брандмауэра, необходимые hello toocommunicate этой службы с hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="abd39-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="abd39-141">Однако, если создать службу, которая запускается процессом вне роли (например, службы COM + или запланированную задачу), необходимо toomanually создать службу toothat доступа tooallow правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="abd39-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="abd39-142">Эти правила брандмауэра можно создавать с помощью задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="abd39-143">У задачи запуска, которая создает правило брандмауэра, должен быть [executionContext][задачи] со значением **elevated**.</span><span class="sxs-lookup"><span data-stu-id="abd39-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="abd39-144">Добавить hello после запуска задачи toohello [ServiceDefinition.csdef] файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="abd39-145">правило брандмауэра hello tooadd, необходимо использовать соответствующий hello `netsh advfirewall firewall` команды в пакетном файле запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="abd39-146">В этом примере hello задачи запуска требуется безопасность и шифрование для TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="abd39-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="abd39-147">Блокирование определенного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="abd39-147">Block a specific IP address</span></span>
<span data-ttu-id="abd39-148">Вы можете ограничить доступ tooa Azure web роли набором указанных IP-адресов, изменяя служб IIS **web.config** файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="abd39-149">Необходимо также toouse командный файл, разблокирующий hello **ipSecurity** раздел hello **ApplicationHost.config** файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="abd39-150">toodo разблокировать hello **ipSecurity** раздел hello **ApplicationHost.config** создайте командный файл, который выполняется при запуске роли.</span><span class="sxs-lookup"><span data-stu-id="abd39-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="abd39-151">Создайте папку на корневом уровне hello вызывается веб-роли **запуска** и в этой папке создайте пакетный файл под названием **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="abd39-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="abd39-152">Добавьте проект Visual Studio tooyour этот файл и задайте свойства hello слишком**всегда Копировать** tooensure, что она включена в пакет.</span><span class="sxs-lookup"><span data-stu-id="abd39-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="abd39-153">Добавить hello после запуска задачи toohello [ServiceDefinition.csdef] файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

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

<span data-ttu-id="abd39-154">Добавление этой команды toohello **startup.cmd** файла:</span><span class="sxs-lookup"><span data-stu-id="abd39-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="abd39-155">Эта задача заставляет hello **startup.cmd** пакетного файла toobe выполнять каждый раз при инициализации hello веб-роли, обеспечивая hello, что необходимые **ipSecurity** разблокирован раздел.</span><span class="sxs-lookup"><span data-stu-id="abd39-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="abd39-156">Наконец, измените hello [раздел System.WebServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) веб-роли **web.config** файл tooadd список IP-адресов, которым предоставлен доступ, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="abd39-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="abd39-157">Этот образец настройки **позволяет** все IP-адреса tooaccess hello server за исключением двух определенных hello</span><span class="sxs-lookup"><span data-stu-id="abd39-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

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

<span data-ttu-id="abd39-158">Этот образец настройки **запрещает** все IP-адреса по доступу к серверу hello, за исключением двух определенных hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

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

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="abd39-159">Создание задачи запуска PowerShell</span><span class="sxs-lookup"><span data-stu-id="abd39-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="abd39-160">Скрипты Windows PowerShell нельзя вызывать непосредственно из hello [ServiceDefinition.csdef] файл, но они могут быть вызваны из пакетного файла запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="abd39-161">PowerShell по умолчанию не запускает неподписанные сценарии.</span><span class="sxs-lookup"><span data-stu-id="abd39-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="abd39-162">Если вы подписываете сценарий, требуется tooconfigure PowerShell toorun неподписанные сценарии.</span><span class="sxs-lookup"><span data-stu-id="abd39-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="abd39-163">toorun неподписанные сценарии, hello **ExecutionPolicy** необходимо задать слишком**Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="abd39-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="abd39-164">Hello **ExecutionPolicy** параметр зависит от версии Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="abd39-165">Если вы используете гостевой ОС, которая работает PowerShell 2.0 или 1.0 можно принудительно toorun версии 2, а если эта кнопка недоступна, используется версия 1.</span><span class="sxs-lookup"><span data-stu-id="abd39-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="abd39-166">Создание файлов в локальном хранилище из задачи запуска</span><span class="sxs-lookup"><span data-stu-id="abd39-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="abd39-167">Можно использовать локальное хранилище ресурсов toostore файлов, созданных при последующем доступе к приложению задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="abd39-168">toocreate Здравствуйте локального ресурса хранилища, добавьте [LocalResources] toohello раздел [ServiceDefinition.csdef] файл и затем добавить hello [LocalStorage] дочерний элемент.</span><span class="sxs-lookup"><span data-stu-id="abd39-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="abd39-169">Предоставьте ресурс локального хранилища hello уникальное имя и соответствующий размер для задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="abd39-170">toouse ресурс локального хранилища в задаче запуска необходимо toocreate среды переменной tooreference hello расположение локального ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="abd39-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="abd39-171">Затем hello задачи запуска и приложение hello может tooread и записи файлов toohello локального ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="abd39-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="abd39-172">Здравствуйте, соответствующие разделы hello **ServiceDefinition.csdef** показаны ниже:</span><span class="sxs-lookup"><span data-stu-id="abd39-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

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

<span data-ttu-id="abd39-173">Например это **Startup.cmd** пакетный файл использует hello **PathToStartupStorage** файла hello toocreate переменной среды **MyTest.txt** в локальном хранилище hello расположение.</span><span class="sxs-lookup"><span data-stu-id="abd39-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="abd39-174">Локальное хранилище папки доступен с hello Azure SDK с помощью hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="abd39-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="abd39-175">Запустить в эмуляторе hello или облака</span><span class="sxs-lookup"><span data-stu-id="abd39-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="abd39-176">Возможно выполнение различных действий при работе в toowhen облаке, в отличие hello в эмуляторе вычислений hello, задача запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="abd39-177">Например может потребоваться toouse новую копию данных SQL, только при выполнении в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="abd39-178">Или вы можете toodo некоторые оптимизации производительности для облака hello, что нет необходимости toodo при выполнении в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="abd39-179">Это возможность tooperform различные действия на hello эмулятор вычислений и hello облаке реализуется путем создания переменной среды в hello [ServiceDefinition.csdef] файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="abd39-180">Затем переменная проверяется в задаче запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="abd39-181">переменная среды toocreate hello, добавить hello [переменной]/[RoleInstanceValue] элемент и создать значение XPath `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="abd39-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="abd39-182">Здравствуйте, значение hello **% ComputeEmulatorRunning %** переменная среды `true` при выполнении в эмуляторе вычислений hello, и `false` при выполнении в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

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

<span data-ttu-id="abd39-183">Задача Hello, теперь можно проверить hello **% ComputeEmulatorRunning %** различных действий среды переменной tooperform зависимости от того, работает ли роли hello в hello облачной или hello эмулятора.</span><span class="sxs-lookup"><span data-stu-id="abd39-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="abd39-184">Вот CMD-файл сценария оболочки для проверки этой переменной среды.</span><span class="sxs-lookup"><span data-stu-id="abd39-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="abd39-185">Обнаружение запуска задачи</span><span class="sxs-lookup"><span data-stu-id="abd39-185">Detect that your task has already run</span></span>
<span data-ttu-id="abd39-186">Hello роли может перезапустить без перезагрузки снова вызывает вашей toorun задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="abd39-187">Нет не tooindicate флаг, который задача уже был запущен на размещение виртуальных Машин hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="abd39-188">Возможно, для некоторых задач не важно, сколько раз они выполняются.</span><span class="sxs-lookup"><span data-stu-id="abd39-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="abd39-189">Тем не менее можно запустить в ситуации, когда необходимо tooprevent задачи запуска несколько раз.</span><span class="sxs-lookup"><span data-stu-id="abd39-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="abd39-190">Простейший способ toodetect Hello, задача уже выполнена является toocreate файл в hello **% TEMP %** папки при успешной задачу hello и просмотрите hello для его запуска задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="abd39-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="abd39-191">Ниже приведен пример CMD-файла сценария оболочки, который это делает.</span><span class="sxs-lookup"><span data-stu-id="abd39-191">Here is a sample cmd shell script that does that for you.</span></span>

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

## <a name="task-best-practices"></a><span data-ttu-id="abd39-192">Рекомендации по задачам</span><span class="sxs-lookup"><span data-stu-id="abd39-192">Task best practices</span></span>
<span data-ttu-id="abd39-193">Ниже приведены некоторые рекомендации, которые необходимо выполнять при настройке задачи для рабочей роли или веб-роли.</span><span class="sxs-lookup"><span data-stu-id="abd39-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="abd39-194">Всегда ведите журнал операций запуска</span><span class="sxs-lookup"><span data-stu-id="abd39-194">Always log startup activities</span></span>
<span data-ttu-id="abd39-195">Visual Studio не предоставляет toostep отладчик выполнения пакетных файлов, поэтому очень хорошо tooget объема данных hello операции пакетных файлов, как можно.</span><span class="sxs-lookup"><span data-stu-id="abd39-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="abd39-196">Ведение журнала выходных данных пакетных файлов, hello и **stdout** и **stderr**, можно предоставить вам важную информацию, при попытке toodebug и исправления пакетных файлов.</span><span class="sxs-lookup"><span data-stu-id="abd39-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="abd39-197">toolog оба **stdout** и **stderr** toohello файл StartupLog.txt hello указывает tooby directory hello **% TEMP %** переменной среды, добавьте текст hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`toohello конец конкретной строки, вы хотите toolog.</span><span class="sxs-lookup"><span data-stu-id="abd39-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="abd39-198">Например, tooexecute setup.exe в hello **% PathToApp1Install %** каталога:</span><span class="sxs-lookup"><span data-stu-id="abd39-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="abd39-199">toosimplify xml, можно создать оболочку *cmd* файла, который вызывает все загрузочного задачи, а также ведение журнала и гарантирует общих папок каждая дочерняя задача hello же переменных среды.</span><span class="sxs-lookup"><span data-stu-id="abd39-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="abd39-200">Может оказаться менее раздражающих toouse `>> "%TEMP%\StartupLog.txt" 2>&1` на конце hello каждой задачи запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="abd39-201">Чтобы настроить принудительную регистрацию задач, можно создать оболочку, которая выполняет ведение журнала автоматически.</span><span class="sxs-lookup"><span data-stu-id="abd39-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="abd39-202">Эта оболочка вызывает hello реальные пакетный файл, требуется toorun.</span><span class="sxs-lookup"><span data-stu-id="abd39-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="abd39-203">Любые выходные данные hello целевой пакетный файл будет перенаправленный toohello *Startuplog.txt* файла.</span><span class="sxs-lookup"><span data-stu-id="abd39-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="abd39-204">Привет, в следующем примере показано, как tooredirect все выходные данные из пакетного файла запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="abd39-205">В этом примере hello файл ServerDefinition.csdef создает задачу запуска, который вызывает *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="abd39-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="abd39-206">*logwrap.cmd* вызовы *Startup2.cmd*, перенаправляя весь вывод слишком**% TEMP %\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="abd39-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="abd39-207">ServiceDefinition.cmd:</span><span class="sxs-lookup"><span data-stu-id="abd39-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="abd39-208">**logwrap.cmd:**</span><span class="sxs-lookup"><span data-stu-id="abd39-208">**logwrap.cmd:**</span></span>

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

<span data-ttu-id="abd39-209">**Startup2.cmd:**</span><span class="sxs-lookup"><span data-stu-id="abd39-209">**Startup2.cmd:**</span></span>

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

<span data-ttu-id="abd39-210">Пример выходных данных в hello **StartupLog.txt** файла:</span><span class="sxs-lookup"><span data-stu-id="abd39-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="abd39-211">Hello **StartupLog.txt** файл находится в hello *C:\Resources\temp\\\RoleTemp {идентификатор роли}* папки.</span><span class="sxs-lookup"><span data-stu-id="abd39-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="abd39-212">Правильная настройка executionContext для задач запуска</span><span class="sxs-lookup"><span data-stu-id="abd39-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="abd39-213">Задать привилегии, необходимые для запуска задачи hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="abd39-214">Иногда задачи запуска должны работать с повышенными привилегиями, даже если роль hello выполняется с обычным уровнем привилегий.</span><span class="sxs-lookup"><span data-stu-id="abd39-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="abd39-215">Hello [executionContext][задачи] атрибут задает уровень прав доступа задачи запуска hello hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="abd39-216">С помощью `executionContext="limited"` означает имеет задачу запуска hello hello одинаковом уровне привилегий, как роль hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="abd39-217">С помощью `executionContext="elevated"` означает задачи запуска hello имеет права администратора, что позволяет hello запуска задач администратора tooperform задачи без предоставления прав tooyour роли администратора.</span><span class="sxs-lookup"><span data-stu-id="abd39-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="abd39-218">Пример задачи запуска, которая требует повышенных прав доступа — задача запуска, который использует **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="abd39-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="abd39-219">**AppCmd.exe** требуется `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="abd39-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="abd39-220">Используйте подходящий taskType hello</span><span class="sxs-lookup"><span data-stu-id="abd39-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="abd39-221">Hello [taskType][задачи] атрибут определяет, выполняется задача запуска hello hello способом.</span><span class="sxs-lookup"><span data-stu-id="abd39-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="abd39-222">Он имеет три значения: **simple**, **background** и **foreground**.</span><span class="sxs-lookup"><span data-stu-id="abd39-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="abd39-223">Hello задачи фона и переднего плана запускаются асинхронно, а затем hello простые задачи выполняются синхронно по одному.</span><span class="sxs-lookup"><span data-stu-id="abd39-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="abd39-224">С **простой** задачи запуска можно задать порядок hello в которой запускаются задачи hello hello порядок, в которой hello задачи перечислены в файле ServiceDefinition.csdef hello.</span><span class="sxs-lookup"><span data-stu-id="abd39-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="abd39-225">Если **простой** задача завершается с ненулевым код выхода, а затем hello останавливается процедуры запуска и hello роль не запускается.</span><span class="sxs-lookup"><span data-stu-id="abd39-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="abd39-226">Здравствуйте разницу между **фона** задачи запуска и **переднего плана** том, что **переднего плана** задачи сохранить hello роли выполняется до hello  **передний план** завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="abd39-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="abd39-227">Это также означает, что если hello **переднего плана** задач зависает или дает сбой, hello роль не обновляется до hello **переднего плана** задача принудительно закрыто.</span><span class="sxs-lookup"><span data-stu-id="abd39-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="abd39-228">По этой причине **фона** рекомендуется использовать для асинхронных задач запуска, если не требуется эта функция hello **переднего плана** задачи.</span><span class="sxs-lookup"><span data-stu-id="abd39-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="abd39-229">Завершайте пакетные файлы командой EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="abd39-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="abd39-230">Hello роль будет запускать, только если hello **errorlevel** от каждого вашего простого запуска задач равно нулю.</span><span class="sxs-lookup"><span data-stu-id="abd39-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="abd39-231">Не все программы устанавливают hello **errorlevel** (код завершения) правильно, поэтому hello пакетного файла должно заканчиваться `EXIT /B 0` Если все, что выполнена правильно.</span><span class="sxs-lookup"><span data-stu-id="abd39-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="abd39-232">Недостающий `EXIT /B 0` hello конец пакетного файла запуска является распространенной причиной роли, которые не запускаются.</span><span class="sxs-lookup"><span data-stu-id="abd39-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="abd39-233">Замечено, вложенные пакетные файлы иногда зависания при использовании hello `/B` параметра.</span><span class="sxs-lookup"><span data-stu-id="abd39-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="abd39-234">Вы можете убедиться, что проблема зависания не произойдет при другой пакетный файл вызывает текущий пакетный файл, например при использовании hello toomake [оболочки журнала](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="abd39-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="abd39-235">Можно опустить hello `/B` параметра в данном случае.</span><span class="sxs-lookup"><span data-stu-id="abd39-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="abd39-236">Ожидается, что при запуске задачи toorun более одного раза</span><span class="sxs-lookup"><span data-stu-id="abd39-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="abd39-237">Не все перезапуски роли включают в себя перезагрузку, но все они вызывают выполнение всех задач запуска.</span><span class="sxs-lookup"><span data-stu-id="abd39-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="abd39-238">Это означает, что задачи запуска должны быть toorun может несколько раз между перезагрузками без проблем.</span><span class="sxs-lookup"><span data-stu-id="abd39-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="abd39-239">Это описано в hello [предшествующий раздел](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="abd39-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="abd39-240">Использовать локальное хранилище toostore файлы, которые должны быть доступны в роли hello</span><span class="sxs-lookup"><span data-stu-id="abd39-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="abd39-241">Если toocopy или создайте файл во время задачи запуска, затем доступны tooyour роли, то этот файл должен быть размещен в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="abd39-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="abd39-242">В разделе hello [предшествующий раздел](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="abd39-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="abd39-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="abd39-243">Next steps</span></span>
<span data-ttu-id="abd39-244">Просмотрите hello облака [модели и пакета службы](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="abd39-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="abd39-245">Узнайте, как работают [задачи](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="abd39-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="abd39-246">[Создайте и разверните](cloud-services-how-to-create-deploy-portal.md) свой пакет облачной службы.</span><span class="sxs-lookup"><span data-stu-id="abd39-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

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
