---
title: "aaaLearn о политиках безопасности Azure микрослужбами | Документы Microsoft"
description: "Общие сведения о том, как toorun приложения Service Fabric в системе и локальными учетными записями безопасности, включая точку SetupEntry hello, если приложению необходима tooperform некоторые работы в привилегированном режиме действия перед началом"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="751e2-103">Настройка политик безопасности для приложения</span><span class="sxs-lookup"><span data-stu-id="751e2-103">Configure security policies for your application</span></span>
<span data-ttu-id="751e2-104">С помощью Azure Service Fabric, можно защитить приложения, запущенные в кластере hello с разными учетными записями.</span><span class="sxs-lookup"><span data-stu-id="751e2-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="751e2-105">Service Fabric также помогает безопасного hello ресурсы, используемые приложениями во время hello развертывания под учетными записями пользователей hello — например, файлы, каталоги и сертификаты.</span><span class="sxs-lookup"><span data-stu-id="751e2-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="751e2-106">Это позволяет изолировать друг от друга выполняемые приложения, даже если они запущены в общей среде.</span><span class="sxs-lookup"><span data-stu-id="751e2-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="751e2-107">По умолчанию приложения Service Fabric выполняются hello учетной записью, под которыми выполняется процесс Fabric.exe hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="751e2-108">Service Fabric также предоставляет возможность hello toorun приложений под учетной записью локального пользователя или учетной записи локальной системы, который указывается в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="751e2-109">Поддерживаются следующие типы учетных записей локальной системы: **LocalUser**, **NetworkService**, **LocalService** и **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="751e2-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="751e2-110">При запуске Service Fabric на Windows Server в центре обработки данных с помощью автономного установщика hello, можно использовать учетные записи домена Active Directory, включая групповые управляемые учетные записи службы.</span><span class="sxs-lookup"><span data-stu-id="751e2-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="751e2-111">Можно определить и создать группы пользователей, чтобы управлять toobe группы tooeach можно добавить одного или нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="751e2-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="751e2-112">Это полезно в тех случаях, когда несколько пользователей для точки входа для другой службы и требуется toohave определенные общие привилегии, доступные на уровне группы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="751e2-113">Настройка политики hello точку входа службы настройки</span><span class="sxs-lookup"><span data-stu-id="751e2-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="751e2-114">Как описано в hello [модель приложения](service-fabric-application-model.md), hello точку входа для программы установки, **SetupEntryPoint**, — это точка входа привилегированные, который выполняется с таким же учетные данные как Service Fabric hello (обычно hello *NetworkService* учетной записи) перед любой другой точки входа.</span><span class="sxs-lookup"><span data-stu-id="751e2-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="751e2-115">Hello исполняемый файл, который задается параметром **EntryPoint** обычно является узел службы hello длительное время.</span><span class="sxs-lookup"><span data-stu-id="751e2-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="751e2-116">Так что наличие точки входа отдельной установки позволяет избежать toorun узла службы hello исполняемый файл с высокими привилегиями на длительное время.</span><span class="sxs-lookup"><span data-stu-id="751e2-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="751e2-117">Hello исполняемый файл, **EntryPoint** указывает, запускается после **SetupEntryPoint** успешно завершает работу.</span><span class="sxs-lookup"><span data-stu-id="751e2-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="751e2-118">Hello результирующий процесс отслеживается и перезапустить и снова начинает с **SetupEntryPoint** Если когда-либо завершает или аварийно завершает работу.</span><span class="sxs-lookup"><span data-stu-id="751e2-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="751e2-119">Hello ниже приведен пример манифеста простой службы, показывает hello SetupEntryPoint и hello главной точки входа для службы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="751e2-120">Настройка политики hello с помощью локальной учетной записи</span><span class="sxs-lookup"><span data-stu-id="751e2-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="751e2-121">После настройки службы hello toohave является точкой входа программы установки можно изменить разрешения безопасности hello, которые запускаются в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="751e2-122">Hello в следующем примере показано, как tooconfigure hello toorun службы в группе права администратора учетной записи.</span><span class="sxs-lookup"><span data-stu-id="751e2-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="751e2-123">Сначала создайте раздел **Principals** с именем пользователя, например SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="751e2-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="751e2-124">Это означает, что этот пользователь hello является членом группы системных администраторов hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="751e2-125">Затем в разделе hello **ServiceManifestImport** статьи, настройте tooapply политики субъектом слишком**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="751e2-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="751e2-126">Это указывает Service Fabric, когда hello **MySetup.bat** файл запускается, она должна быть `RunAs` с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="751e2-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="751e2-127">Учитывая, что у вас есть *не* применения политики toohello главную точку входа, кода hello в **MyServiceHost.exe** выполняется в системе hello **NetworkService** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="751e2-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="751e2-128">Это учетная запись по умолчанию hello, все точки входа службы должны выполняться в виде.</span><span class="sxs-lookup"><span data-stu-id="751e2-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="751e2-129">Теперь добавим hello файл MySetup.bat toohello Visual Studio проект tootest hello права администратора.</span><span class="sxs-lookup"><span data-stu-id="751e2-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="751e2-130">В Visual Studio щелкните правой кнопкой мыши проект службы hello и добавьте новый файл с именем MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="751e2-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="751e2-131">Затем убедитесь, что этот файл MySetup.bat hello включается в пакет службы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="751e2-132">По умолчанию он не включен.</span><span class="sxs-lookup"><span data-stu-id="751e2-132">By default, it is not.</span></span> <span data-ttu-id="751e2-133">Выберите файл hello, щелкните правой кнопкой мыши tooget hello контекстное меню и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="751e2-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="751e2-134">Убедитесь, что в диалоговом окне Свойства hello, **скопируйте каталог tooOutput** задано слишком**копировать, если новее**.</span><span class="sxs-lookup"><span data-stu-id="751e2-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="751e2-135">См. следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="751e2-135">See hello following screenshot.</span></span>

![Свойство CopyToOutput в Visual Studio для пакетного файла SetupEntryPoint][image1]

<span data-ttu-id="751e2-137">Теперь откройте файл MySetup.bat hello и добавить hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="751e2-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="751e2-138">Затем постройте и разверните hello решения tooa локальному кластеру разработки.</span><span class="sxs-lookup"><span data-stu-id="751e2-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="751e2-139">После запуска службы hello, как показано в обозреватель Service Fabric, вы увидите успешность этого файла MySetup.bat hello двумя способами.</span><span class="sxs-lookup"><span data-stu-id="751e2-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="751e2-140">Откройте командную строку PowerShell и введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="751e2-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="751e2-141">Запишите имя hello hello узла, где служба hello был развернут и запущен в обозреватель Service Fabric — например, узел 2.</span><span class="sxs-lookup"><span data-stu-id="751e2-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="751e2-142">Далее перейдите toohello приложения экземпляра рабочие папки toofind hello файл out.txt, отображается значение hello **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="751e2-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="751e2-143">Например, если эта служба была развернутой tooNode 2, затем можно перейти toothis путь для hello **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="751e2-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="751e2-144">Настройка политики hello при помощи локальной системной учетной записи</span><span class="sxs-lookup"><span data-stu-id="751e2-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="751e2-145">Обычно это более предпочтительным, чем toorun hello запуска сценария с помощью учетной записи локальной системы, а не учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="751e2-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="751e2-146">Под управлением политики hello запуска от имени является членом группы "Администраторы" обычно не работает хорошо, поскольку машины имеют пользователя Access Control (UAC) включен по умолчанию приветствия.</span><span class="sxs-lookup"><span data-stu-id="751e2-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="751e2-147">В таких случаях **hello рекомендуется hello toorun SetupEntryPoint как LocalSystem, вместо в группу локальных пользователей добавлены tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="751e2-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="751e2-148">Hello ниже приведен пример параметр hello SetupEntryPoint toorun учетной записью LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="751e2-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="751e2-149">Запуск команд PowerShell из точки входа настройки</span><span class="sxs-lookup"><span data-stu-id="751e2-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="751e2-150">toorun PowerShell из hello **SetupEntryPoint** точки, можно запустить **PowerShell.exe** в пакетном файле, который указывает tooa PowerShell файла.</span><span class="sxs-lookup"><span data-stu-id="751e2-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="751e2-151">Например, сначала добавьте проект службы toohello файла PowerShell-- **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="751e2-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="751e2-152">Запомнить tooset hello *копировать, если новее* свойство так, чтобы этот файл hello также включается в пакет службы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="751e2-153">Hello примере показан образец пакетный файл, который запускает файл PowerShell с именем MySetup.ps1, устанавливающее system переменную среды с именем **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="751e2-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="751e2-154">Toostart MySetup.bat файл PowerShell:</span><span class="sxs-lookup"><span data-stu-id="751e2-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="751e2-155">Добавьте следующие системные переменные среды tooset hello hello PowerShell файла:</span><span class="sxs-lookup"><span data-stu-id="751e2-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="751e2-156">По умолчанию при выполнении пакетного файла hello, он выполняет поиск папки приложения hello вызывается **работы** для файлов.</span><span class="sxs-lookup"><span data-stu-id="751e2-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="751e2-157">В этом случае выполняется MySetup.bat, мы хотим hello этот toofind MySetup.ps1 файл hello же папку, которая является приложение hello **пакет кода** папки.</span><span class="sxs-lookup"><span data-stu-id="751e2-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="751e2-158">toochange эта папка, набор hello рабочей папки:</span><span class="sxs-lookup"><span data-stu-id="751e2-158">toochange this folder, set hello working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="751e2-159">Использование перенаправления консоли для локальной отладки</span><span class="sxs-lookup"><span data-stu-id="751e2-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="751e2-160">Иногда бывает полезным toosee hello вывод на консоль из выполнения скрипта в целях отладки.</span><span class="sxs-lookup"><span data-stu-id="751e2-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="751e2-161">toodo это, можно задать политику перенаправления консоли, которая записывает файл tooa hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="751e2-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="751e2-162">Hello файл вывода называется папка приложения письменного toohello **журнала** на узле hello, где развертывается и запускается приложение hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="751e2-163">(Где toofind на предшествующий пример hello.)</span><span class="sxs-lookup"><span data-stu-id="751e2-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="751e2-164">Никогда не используйте политику перенаправления консоли hello в приложении, которое развертывается в рабочей среде, так как это может повлиять на приложения hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="751e2-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="751e2-165">Используйте ее *только* для локальной разработки и отладки.</span><span class="sxs-lookup"><span data-stu-id="751e2-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="751e2-166">Hello ниже приведен пример подключения консоли hello параметр со значением FileRetentionCount.</span><span class="sxs-lookup"><span data-stu-id="751e2-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="751e2-167">Если теперь изменить файл toowrite hello MySetup.ps1 **Echo** команды запись toohello выходной файл для отладки:</span><span class="sxs-lookup"><span data-stu-id="751e2-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="751e2-168">**Завершив отладку сценария, немедленно удалите эту политику перенаправления консоли.**</span><span class="sxs-lookup"><span data-stu-id="751e2-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="751e2-169">Настройка политики для пакетов кода службы</span><span class="sxs-lookup"><span data-stu-id="751e2-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="751e2-170">В предыдущих шагах hello, вы узнали, как tooapply tooSetupEntryPoint политики запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="751e2-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="751e2-171">Давайте взглянем более детально в как toocreate разных участников, которые могут быть применены как службы политики.</span><span class="sxs-lookup"><span data-stu-id="751e2-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="751e2-172">Создание локальных групп пользователей</span><span class="sxs-lookup"><span data-stu-id="751e2-172">Create local user groups</span></span>
<span data-ttu-id="751e2-173">Можно определить и создать группы пользователей, которые допускает использование одного или нескольких пользователей toobe добавлены tooa группы.</span><span class="sxs-lookup"><span data-stu-id="751e2-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="751e2-174">Это полезно в том случае, если имеется несколько пользователей для точки входа другую службу, и требуется toohave определенные общие привилегии, доступные на уровне группы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="751e2-175">Hello пример локальной группы с именем **LocalAdminGroup** , обладающей правами администратора.</span><span class="sxs-lookup"><span data-stu-id="751e2-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="751e2-176">В нее входят два пользователя: Customer1 и Customer2.</span><span class="sxs-lookup"><span data-stu-id="751e2-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="751e2-177">Создание локальных пользователей</span><span class="sxs-lookup"><span data-stu-id="751e2-177">Create local users</span></span>
<span data-ttu-id="751e2-178">Можно создать локального пользователя, который может быть используется toohelp безопасной службы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="751e2-179">Когда **LocalUser** тип учетной записи задается в разделе субъекты hello манифеста приложения hello, Service Fabric создает учетные записи локальных пользователей на компьютерах, где развернуто приложение hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="751e2-180">По умолчанию эти учетные записи имеют одинаковые имена, которые указаны в приложение hello манифеста (например, Customer3 в следующий образец hello) hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="751e2-181">Вместо этого они создаются динамически и имеют случайные пароли.</span><span class="sxs-lookup"><span data-stu-id="751e2-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="751e2-182">Если приложение требует, что hello учетной записи пользователя и пароль совпадать на всех компьютерах (например, tooenable проверка подлинности NTLM), hello манифест кластера необходимо задать NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="751e2-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="751e2-183">Hello манифест кластера необходимо также указать NTLMAuthenticationPasswordSecret, который используется toogenerate hello пароль на всех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="751e2-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="751e2-184">Назначение политики toohello пакетов кода службы</span><span class="sxs-lookup"><span data-stu-id="751e2-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="751e2-185">Hello **элемент RunAsPolicy** , в разделе **ServiceManifestImport** указывает hello учетную запись из раздела hello участников, которые должны быть toorun используемый пакет кода.</span><span class="sxs-lookup"><span data-stu-id="751e2-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="751e2-186">Он также связывает кода манифеста пакетов из службы hello с учетными записями пользователей в разделе субъекты hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="751e2-187">Это можно указать для установки hello или основными точками входа, или можно указать `All` tooapply его tooboth.</span><span class="sxs-lookup"><span data-stu-id="751e2-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="751e2-188">Hello ниже приведен пример применения различных политик.</span><span class="sxs-lookup"><span data-stu-id="751e2-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="751e2-189">Если **EntryPointType** не указан, по умолчанию hello значение tooEntryPointType = «Main».</span><span class="sxs-lookup"><span data-stu-id="751e2-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="751e2-190">Указание **SetupEntryPoint** особенно полезна при необходимости toorun определенных операций по установке высоким уровнем привилегий учетной записи system.</span><span class="sxs-lookup"><span data-stu-id="751e2-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="751e2-191">Hello фактический код службы запускаются под учетной записью с низкими правами доступа.</span><span class="sxs-lookup"><span data-stu-id="751e2-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="751e2-192">Применять пакеты обновления кода по умолчанию политики tooall</span><span class="sxs-lookup"><span data-stu-id="751e2-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="751e2-193">Использовать hello **DefaultRunAsPolicy** toospecify раздел учетную запись пользователя по умолчанию все пакеты кода, которые не имеют определенного **элемент RunAsPolicy** определен.</span><span class="sxs-lookup"><span data-stu-id="751e2-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="751e2-194">Если большинство пакетов кода hello, указанных в манифесте hello службы, используемой приложением требуется toorun под hello одного пользователя hello приложения можно просто определить политику запуска от имени по умолчанию с этой учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="751e2-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="751e2-195">Hello следующий пример указывает, что если пакет кода не имеет **элемент RunAsPolicy** указано, пакет кода hello должна выполняться с использованием hello **MyDefaultAccount** заданы в разделе субъекты hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="751e2-196">Использование групп и пользователей домена Active Directory</span><span class="sxs-lookup"><span data-stu-id="751e2-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="751e2-197">Для экземпляра Service Fabric, который был установлен на Windows Server с помощью автономного установщика hello можно запустить службу hello hello учетными данными для учетной записи пользователя или группы Active Directory.</span><span class="sxs-lookup"><span data-stu-id="751e2-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="751e2-198">Речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="751e2-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="751e2-199">С помощью пользователя домена или группы, затем доступны другие ресурсы hello домена (например, общие файловые ресурсы), которые были предоставлены разрешения.</span><span class="sxs-lookup"><span data-stu-id="751e2-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="751e2-200">Hello пример пользователя Active Directory с именем *TestUser* в своем домене называется пароль зашифрован с помощью сертификата *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="751e2-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="751e2-201">Можно использовать hello `Invoke-ServiceFabricEncryptText` текста шифра секретный hello toocreate команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="751e2-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="751e2-202">Дополнительные сведения см. в статье [Управление секретами в приложениях Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="751e2-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="751e2-203">Закрытый ключ hello hello сертификат toodecrypt hello пароль toohello локального компьютера необходимо развернуть с помощью метода по каналу (в Azure, это посредством Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="751e2-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="751e2-204">Затем когда Service Fabric развертывает компьютере toohello пакета службы hello, – секрет hello может toodecrypt и (вместе с именем пользователя hello) проверки подлинности в Active Directory toorun этими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="751e2-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="751e2-205">Используйте групповую управляемую учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="751e2-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="751e2-206">Для экземпляра Service Fabric, который был установлен на Windows Server с помощью автономного установщика hello службу hello можно выполнять как группу управляемой учетной записи службы (gMSA).</span><span class="sxs-lookup"><span data-stu-id="751e2-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="751e2-207">Обратите внимание, что речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="751e2-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="751e2-208">С помощью групповую нет пароля или зашифрованный пароль, которые хранятся в hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="751e2-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="751e2-209">Hello следующий пример показывает, как toocreate групповой управляемой учетной записи вызывать *svc-Test$*; toodeploy, управляются узлов кластера toohello учетной записи службы; и как tooconfigure hello участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="751e2-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="751e2-210">Предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="751e2-210">Prerequisites.</span></span>
- <span data-ttu-id="751e2-211">Hello домена должен корневого ключа KDS.</span><span class="sxs-lookup"><span data-stu-id="751e2-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="751e2-212">Hello домена должен toobe в Windows Server 2012 или более поздней версии на функциональном уровне.</span><span class="sxs-lookup"><span data-stu-id="751e2-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="751e2-213">Пример</span><span class="sxs-lookup"><span data-stu-id="751e2-213">Example</span></span>
1. <span data-ttu-id="751e2-214">Попросите администратора домена active directory создайте учетную запись службы группы управляемых с помощью hello `New-ADServiceAccount` командлет и убедитесь, что hello `PrincipalsAllowedToRetrieveManagedPassword` включает все узлы кластера hello service fabric.</span><span class="sxs-lookup"><span data-stu-id="751e2-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="751e2-215">Обратите внимание, что `AccountName`, `DnsHostName` и `ServicePrincipalName` должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="751e2-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="751e2-216">На каждом из узлов кластера hello службы структуры (например, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), установить и протестировать hello групповой управляемой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="751e2-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="751e2-217">Настройте hello участника-пользователя и пользователь hello tooreference элемент RunAsPolicy hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="751e2-218">Назначение политики безопасности доступа для конечных точек HTTP и HTTPS</span><span class="sxs-lookup"><span data-stu-id="751e2-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="751e2-219">Если применить политики tooa запуска от имени службы и манифест службы hello объявляет ресурсы конечной точки с протоколом hello HTTP, необходимо указать **SecurityAccessPolicy** tooensure, что порты выделяется toothese конечные точки не правильно Управление доступом для hello списке учетная запись запуска от имени, запускаются службы hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="751e2-220">В противном случае **http.sys** не установлена служба toohello доступа и получить сбоев с вызовов от клиента hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="751e2-221">Hello следующий пример применяет hello Customer1 учетной записи tooan конечная точка с именем **EndpointName**, что дает права на полный доступ.</span><span class="sxs-lookup"><span data-stu-id="751e2-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="751e2-222">Для конечной точки HTTPS hello также имеется имя hello tooindicate tooreturn toohello hello сертификат клиента.</span><span class="sxs-lookup"><span data-stu-id="751e2-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="751e2-223">Это можно сделать с помощью **EndpointBindingPolicy**, сертификатом hello, определенные в разделе сертификатов в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="751e2-224">Обновление нескольких приложений с помощью конечных точек HTTPS</span><span class="sxs-lookup"><span data-stu-id="751e2-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="751e2-225">Необходимо соблюдать осторожность toobe не toouse hello **тот же порт** для различных экземпляров hello одного приложения, при использовании http**s**.</span><span class="sxs-lookup"><span data-stu-id="751e2-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="751e2-226">Hello обусловлено тем, Service Fabric не сможет может tooupgrade hello сертификата для одного из экземпляров приложения hello.</span><span class="sxs-lookup"><span data-stu-id="751e2-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="751e2-227">Например, если приложение 1 или приложения 2 обоих tooupgrade их toocert cert 1 2.</span><span class="sxs-lookup"><span data-stu-id="751e2-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="751e2-228">Когда происходит обновление hello, Service Fabric может очистки hello cert 1 регистрации в http.sys несмотря на то, что hello приложение по-прежнему использует его.</span><span class="sxs-lookup"><span data-stu-id="751e2-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="751e2-229">tooprevent, Service Fabric обнаруживает, что уже зарегистрирован на порту hello с сертификатом hello другой экземпляр приложения (из-за toohttp.sys) и происходит сбой hello операции.</span><span class="sxs-lookup"><span data-stu-id="751e2-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="751e2-230">Поэтому Service Fabric не поддерживает обновление с помощью двух разных служб **hello тот же порт** в экземплярах другого приложения.</span><span class="sxs-lookup"><span data-stu-id="751e2-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="751e2-231">Другими словами, нельзя использовать hello же сертификатов на различные службы на hello тот же порт.</span><span class="sxs-lookup"><span data-stu-id="751e2-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="751e2-232">Если вам требуется toohave общий сертификат на hello же порт, необходимо tooensure, hello службы размещаются на разных компьютерах с ограничения размещения.</span><span class="sxs-lookup"><span data-stu-id="751e2-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="751e2-233">Или по возможности используйте динамические порты Service Fabric для каждой службы в экземпляре приложения.</span><span class="sxs-lookup"><span data-stu-id="751e2-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="751e2-234">Если сбой обновления с помощью протокола https, отображается ошибка, предупреждение о том, «hello HTTP-сервера Windows API не поддерживает несколько сертификатов для приложения, использующие тот же порт.»</span><span class="sxs-lookup"><span data-stu-id="751e2-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="751e2-235">Полный пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="751e2-235">A complete application manifest example</span></span>
<span data-ttu-id="751e2-236">Следуя манифест приложения Hello показаны различные hello разные параметры:</span><span class="sxs-lookup"><span data-stu-id="751e2-236">hello following application manifest shows many of hello different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="751e2-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="751e2-237">Next steps</span></span>
* [<span data-ttu-id="751e2-238">Понять модель приложения hello</span><span class="sxs-lookup"><span data-stu-id="751e2-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="751e2-239">Указание ресурсов в манифесте службы</span><span class="sxs-lookup"><span data-stu-id="751e2-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="751e2-240">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="751e2-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
