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
# <a name="configure-security-policies-for-your-application"></a>Настройка политик безопасности для приложения
С помощью Azure Service Fabric, можно защитить приложения, запущенные в кластере hello с разными учетными записями. Service Fabric также помогает безопасного hello ресурсы, используемые приложениями во время hello развертывания под учетными записями пользователей hello — например, файлы, каталоги и сертификаты. Это позволяет изолировать друг от друга выполняемые приложения, даже если они запущены в общей среде.

По умолчанию приложения Service Fabric выполняются hello учетной записью, под которыми выполняется процесс Fabric.exe hello. Service Fabric также предоставляет возможность hello toorun приложений под учетной записью локального пользователя или учетной записи локальной системы, который указывается в манифесте приложения hello. Поддерживаются следующие типы учетных записей локальной системы: **LocalUser**, **NetworkService**, **LocalService** и **LocalSystem**.

 При запуске Service Fabric на Windows Server в центре обработки данных с помощью автономного установщика hello, можно использовать учетные записи домена Active Directory, включая групповые управляемые учетные записи службы.

Можно определить и создать группы пользователей, чтобы управлять toobe группы tooeach можно добавить одного или нескольких пользователей. Это полезно в тех случаях, когда несколько пользователей для точки входа для другой службы и требуется toohave определенные общие привилегии, доступные на уровне группы hello.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Настройка политики hello точку входа службы настройки
Как описано в hello [модель приложения](service-fabric-application-model.md), hello точку входа для программы установки, **SetupEntryPoint**, — это точка входа привилегированные, который выполняется с таким же учетные данные как Service Fabric hello (обычно hello *NetworkService* учетной записи) перед любой другой точки входа. Hello исполняемый файл, который задается параметром **EntryPoint** обычно является узел службы hello длительное время. Так что наличие точки входа отдельной установки позволяет избежать toorun узла службы hello исполняемый файл с высокими привилегиями на длительное время. Hello исполняемый файл, **EntryPoint** указывает, запускается после **SetupEntryPoint** успешно завершает работу. Hello результирующий процесс отслеживается и перезапустить и снова начинает с **SetupEntryPoint** Если когда-либо завершает или аварийно завершает работу.

Hello ниже приведен пример манифеста простой службы, показывает hello SetupEntryPoint и hello главной точки входа для службы hello.

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

### <a name="configure-hello-policy-by-using-a-local-account"></a>Настройка политики hello с помощью локальной учетной записи
После настройки службы hello toohave является точкой входа программы установки можно изменить разрешения безопасности hello, которые запускаются в манифесте приложения hello. Hello в следующем примере показано, как tooconfigure hello toorun службы в группе права администратора учетной записи.

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

Сначала создайте раздел **Principals** с именем пользователя, например SetupAdminUser. Это означает, что этот пользователь hello является членом группы системных администраторов hello.

Затем в разделе hello **ServiceManifestImport** статьи, настройте tooapply политики субъектом слишком**SetupEntryPoint**. Это указывает Service Fabric, когда hello **MySetup.bat** файл запускается, она должна быть `RunAs` с правами администратора. Учитывая, что у вас есть *не* применения политики toohello главную точку входа, кода hello в **MyServiceHost.exe** выполняется в системе hello **NetworkService** учетной записи. Это учетная запись по умолчанию hello, все точки входа службы должны выполняться в виде.

Теперь добавим hello файл MySetup.bat toohello Visual Studio проект tootest hello права администратора. В Visual Studio щелкните правой кнопкой мыши проект службы hello и добавьте новый файл с именем MySetup.bat.

Затем убедитесь, что этот файл MySetup.bat hello включается в пакет службы hello. По умолчанию он не включен. Выберите файл hello, щелкните правой кнопкой мыши tooget hello контекстное меню и выберите **свойства**. Убедитесь, что в диалоговом окне Свойства hello, **скопируйте каталог tooOutput** задано слишком**копировать, если новее**. См. следующий снимок экрана приветствия.

![Свойство CopyToOutput в Visual Studio для пакетного файла SetupEntryPoint][image1]

Теперь откройте файл MySetup.bat hello и добавить hello, следующие команды:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Затем постройте и разверните hello решения tooa локальному кластеру разработки. После запуска службы hello, как показано в обозреватель Service Fabric, вы увидите успешность этого файла MySetup.bat hello двумя способами. Откройте командную строку PowerShell и введите следующую команду.

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Запишите имя hello hello узла, где служба hello был развернут и запущен в обозреватель Service Fabric — например, узел 2. Далее перейдите toohello приложения экземпляра рабочие папки toofind hello файл out.txt, отображается значение hello **TestVariable**. Например, если эта служба была развернутой tooNode 2, затем можно перейти toothis путь для hello **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Настройка политики hello при помощи локальной системной учетной записи
Обычно это более предпочтительным, чем toorun hello запуска сценария с помощью учетной записи локальной системы, а не учетной записи администратора. Под управлением политики hello запуска от имени является членом группы "Администраторы" обычно не работает хорошо, поскольку машины имеют пользователя Access Control (UAC) включен по умолчанию приветствия. В таких случаях **hello рекомендуется hello toorun SetupEntryPoint как LocalSystem, вместо в группу локальных пользователей добавлены tooAdministrators**. Hello ниже приведен пример параметр hello SetupEntryPoint toorun учетной записью LocalSystem.

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Запуск команд PowerShell из точки входа настройки
toorun PowerShell из hello **SetupEntryPoint** точки, можно запустить **PowerShell.exe** в пакетном файле, который указывает tooa PowerShell файла. Например, сначала добавьте проект службы toohello файла PowerShell-- **MySetup.ps1**. Запомнить tooset hello *копировать, если новее* свойство так, чтобы этот файл hello также включается в пакет службы hello. Hello примере показан образец пакетный файл, который запускает файл PowerShell с именем MySetup.ps1, устанавливающее system переменную среды с именем **TestVariable**.

Toostart MySetup.bat файл PowerShell:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

Добавьте следующие системные переменные среды tooset hello hello PowerShell файла:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> По умолчанию при выполнении пакетного файла hello, он выполняет поиск папки приложения hello вызывается **работы** для файлов. В этом случае выполняется MySetup.bat, мы хотим hello этот toofind MySetup.ps1 файл hello же папку, которая является приложение hello **пакет кода** папки. toochange эта папка, набор hello рабочей папки:
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

## <a name="use-console-redirection-for-local-debugging"></a>Использование перенаправления консоли для локальной отладки
Иногда бывает полезным toosee hello вывод на консоль из выполнения скрипта в целях отладки. toodo это, можно задать политику перенаправления консоли, которая записывает файл tooa hello выходных данных. Hello файл вывода называется папка приложения письменного toohello **журнала** на узле hello, где развертывается и запускается приложение hello. (Где toofind на предшествующий пример hello.)

> [!WARNING]
> Никогда не используйте политику перенаправления консоли hello в приложении, которое развертывается в рабочей среде, так как это может повлиять на приложения hello перехода на другой ресурс. Используйте ее *только* для локальной разработки и отладки.  
> 
> 

Hello ниже приведен пример подключения консоли hello параметр со значением FileRetentionCount.

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Если теперь изменить файл toowrite hello MySetup.ps1 **Echo** команды запись toohello выходной файл для отладки:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Завершив отладку сценария, немедленно удалите эту политику перенаправления консоли.**

## <a name="configure-a-policy-for-service-code-packages"></a>Настройка политики для пакетов кода службы
В предыдущих шагах hello, вы узнали, как tooapply tooSetupEntryPoint политики запуска от имени. Давайте взглянем более детально в как toocreate разных участников, которые могут быть применены как службы политики.

### <a name="create-local-user-groups"></a>Создание локальных групп пользователей
Можно определить и создать группы пользователей, которые допускает использование одного или нескольких пользователей toobe добавлены tooa группы. Это полезно в том случае, если имеется несколько пользователей для точки входа другую службу, и требуется toohave определенные общие привилегии, доступные на уровне группы hello. Hello пример локальной группы с именем **LocalAdminGroup** , обладающей правами администратора. В нее входят два пользователя: Customer1 и Customer2.

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

### <a name="create-local-users"></a>Создание локальных пользователей
Можно создать локального пользователя, который может быть используется toohelp безопасной службы приложения hello. Когда **LocalUser** тип учетной записи задается в разделе субъекты hello манифеста приложения hello, Service Fabric создает учетные записи локальных пользователей на компьютерах, где развернуто приложение hello. По умолчанию эти учетные записи имеют одинаковые имена, которые указаны в приложение hello манифеста (например, Customer3 в следующий образец hello) hello. Вместо этого они создаются динамически и имеют случайные пароли.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Если приложение требует, что hello учетной записи пользователя и пароль совпадать на всех компьютерах (например, tooenable проверка подлинности NTLM), hello манифест кластера необходимо задать NTLMAuthenticationEnabled tootrue. Hello манифест кластера необходимо также указать NTLMAuthenticationPasswordSecret, который используется toogenerate hello пароль на всех компьютерах.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Назначение политики toohello пакетов кода службы
Hello **элемент RunAsPolicy** , в разделе **ServiceManifestImport** указывает hello учетную запись из раздела hello участников, которые должны быть toorun используемый пакет кода. Он также связывает кода манифеста пакетов из службы hello с учетными записями пользователей в разделе субъекты hello. Это можно указать для установки hello или основными точками входа, или можно указать `All` tooapply его tooboth. Hello ниже приведен пример применения различных политик.

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Если **EntryPointType** не указан, по умолчанию hello значение tooEntryPointType = «Main». Указание **SetupEntryPoint** особенно полезна при необходимости toorun определенных операций по установке высоким уровнем привилегий учетной записи system. Hello фактический код службы запускаются под учетной записью с низкими правами доступа.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Применять пакеты обновления кода по умолчанию политики tooall
Использовать hello **DefaultRunAsPolicy** toospecify раздел учетную запись пользователя по умолчанию все пакеты кода, которые не имеют определенного **элемент RunAsPolicy** определен. Если большинство пакетов кода hello, указанных в манифесте hello службы, используемой приложением требуется toorun под hello одного пользователя hello приложения можно просто определить политику запуска от имени по умолчанию с этой учетной записи пользователя. Hello следующий пример указывает, что если пакет кода не имеет **элемент RunAsPolicy** указано, пакет кода hello должна выполняться с использованием hello **MyDefaultAccount** заданы в разделе субъекты hello.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Использование групп и пользователей домена Active Directory
Для экземпляра Service Fabric, который был установлен на Windows Server с помощью автономного установщика hello можно запустить службу hello hello учетными данными для учетной записи пользователя или группы Active Directory. Речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD). С помощью пользователя домена или группы, затем доступны другие ресурсы hello домена (например, общие файловые ресурсы), которые были предоставлены разрешения.

Hello пример пользователя Active Directory с именем *TestUser* в своем домене называется пароль зашифрован с помощью сертификата *MyCert*. Можно использовать hello `Invoke-ServiceFabricEncryptText` текста шифра секретный hello toocreate команды PowerShell. Дополнительные сведения см. в статье [Управление секретами в приложениях Service Fabric](service-fabric-application-secret-management.md).

Закрытый ключ hello hello сертификат toodecrypt hello пароль toohello локального компьютера необходимо развернуть с помощью метода по каналу (в Azure, это посредством Azure Resource Manager). Затем когда Service Fabric развертывает компьютере toohello пакета службы hello, – секрет hello может toodecrypt и (вместе с именем пользователя hello) проверки подлинности в Active Directory toorun этими учетными данными.

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
### <a name="use-a-group-managed-service-account"></a>Используйте групповую управляемую учетную запись службы.
Для экземпляра Service Fabric, который был установлен на Windows Server с помощью автономного установщика hello службу hello можно выполнять как группу управляемой учетной записи службы (gMSA). Обратите внимание, что речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD). С помощью групповую нет пароля или зашифрованный пароль, которые хранятся в hello `Application Manifest`.

Hello следующий пример показывает, как toocreate групповой управляемой учетной записи вызывать *svc-Test$*; toodeploy, управляются узлов кластера toohello учетной записи службы; и как tooconfigure hello участника-пользователя.

##### <a name="prerequisites"></a>Предварительные требования.
- Hello домена должен корневого ключа KDS.
- Hello домена должен toobe в Windows Server 2012 или более поздней версии на функциональном уровне.

##### <a name="example"></a>Пример
1. Попросите администратора домена active directory создайте учетную запись службы группы управляемых с помощью hello `New-ADServiceAccount` командлет и убедитесь, что hello `PrincipalsAllowedToRetrieveManagedPassword` включает все узлы кластера hello service fabric. Обратите внимание, что `AccountName`, `DnsHostName` и `ServicePrincipalName` должны быть уникальными.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. На каждом из узлов кластера hello службы структуры (например, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), установить и протестировать hello групповой управляемой учетной записи.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Настройте hello участника-пользователя и пользователь hello tooreference элемент RunAsPolicy hello.
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Назначение политики безопасности доступа для конечных точек HTTP и HTTPS
Если применить политики tooa запуска от имени службы и манифест службы hello объявляет ресурсы конечной точки с протоколом hello HTTP, необходимо указать **SecurityAccessPolicy** tooensure, что порты выделяется toothese конечные точки не правильно Управление доступом для hello списке учетная запись запуска от имени, запускаются службы hello. В противном случае **http.sys** не установлена служба toohello доступа и получить сбоев с вызовов от клиента hello. Hello следующий пример применяет hello Customer1 учетной записи tooan конечная точка с именем **EndpointName**, что дает права на полный доступ.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Для конечной точки HTTPS hello также имеется имя hello tooindicate tooreturn toohello hello сертификат клиента. Это можно сделать с помощью **EndpointBindingPolicy**, сертификатом hello, определенные в разделе сертификатов в манифесте приложения hello.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Обновление нескольких приложений с помощью конечных точек HTTPS
Необходимо соблюдать осторожность toobe не toouse hello **тот же порт** для различных экземпляров hello одного приложения, при использовании http**s**. Hello обусловлено тем, Service Fabric не сможет может tooupgrade hello сертификата для одного из экземпляров приложения hello. Например, если приложение 1 или приложения 2 обоих tooupgrade их toocert cert 1 2. Когда происходит обновление hello, Service Fabric может очистки hello cert 1 регистрации в http.sys несмотря на то, что hello приложение по-прежнему использует его. tooprevent, Service Fabric обнаруживает, что уже зарегистрирован на порту hello с сертификатом hello другой экземпляр приложения (из-за toohttp.sys) и происходит сбой hello операции.

Поэтому Service Fabric не поддерживает обновление с помощью двух разных служб **hello тот же порт** в экземплярах другого приложения. Другими словами, нельзя использовать hello же сертификатов на различные службы на hello тот же порт. Если вам требуется toohave общий сертификат на hello же порт, необходимо tooensure, hello службы размещаются на разных компьютерах с ограничения размещения. Или по возможности используйте динамические порты Service Fabric для каждой службы в экземпляре приложения. 

Если сбой обновления с помощью протокола https, отображается ошибка, предупреждение о том, «hello HTTP-сервера Windows API не поддерживает несколько сертификатов для приложения, использующие тот же порт.»

## <a name="a-complete-application-manifest-example"></a>Полный пример манифеста приложения
Следуя манифест приложения Hello показаны различные hello разные параметры:

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
## <a name="next-steps"></a>Дальнейшие действия
* [Понять модель приложения hello](service-fabric-application-model.md)
* [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md)
* [Развертывание приложения](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
