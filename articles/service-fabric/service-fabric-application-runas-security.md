---
title: "Описание политик безопасности микрослужб Azure | Документация Майкрософт"
description: "Общие сведения о запуске приложения Service Fabric с использованием системных и локальных учетных записей безопасности, включая точку SetupEntry, если приложению перед запуском необходимо выполнить привилегированную операцию."
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
ms.openlocfilehash: b2ff715d8225bd0a9c7f6108f8804cdfa3189cc8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="configure-security-policies-for-your-application"></a>Настройка политик безопасности для приложения
Платформа Azure Service Fabric помогает защищать приложения, работающие в кластере под разными учетными записями. Кроме того, платформа помогает защищать ресурсы, используемые приложениями при развертывании с помощью учетных записей, например файлы, каталоги и сертификаты. Это позволяет изолировать друг от друга выполняемые приложения, даже если они запущены в общей среде.

По умолчанию приложения Service Fabric выполняются под учетной записью, используемой процессом Fabric.exe. Платформа также позволяет запускать приложения под учетной записью локального пользователя или локальной системы, указанной в манифесте приложения. Поддерживаются следующие типы учетных записей локальной системы: **LocalUser**, **NetworkService**, **LocalService** и **LocalSystem**.

 Если Service Fabric выполняется на сервере Windows Server в центре обработки данных с использованием автономного установщика, можно использовать учетные записи домена Active Directory, включая групповые управляемые учетные записи служб.

Вы можете определять и создавать группы пользователей, а затем добавлять в них пользователей для совместного управления. Это полезно, если для разных точек входа службы есть несколько пользователей и у них должны быть определенные общие права, доступные на уровне группы.

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a>Определение политики для точки входа настройки службы
Как описано в [службы манифестов приложения и](service-fabric-application-and-service-manifests.md), точкой входа программы установки, **SetupEntryPoint**, — это точка входа привилегированные, который выполняется с использованием учетных данных службы структуры (обычно *NetworkService* учетной записи) перед любой другой точки входа. Исполняемый файл, указанный для точки входа **EntryPoint**, обычно представлен длительно выполняемым узлом службы. Если у вас есть отдельная точка входа настройки, вы можете не запускать исполняемый файл узла службы с расширенными правами на длительный срок. Исполняемый файл, указанный для точки входа **EntryPoint**, запускается после успешного выхода из точки **SetupEntryPoint**. Созданный им процесс отслеживается и перезапускается (снова начиная с точки входа **SetupEntryPoint**), если произойдет непредвиденное завершение его работы или сбой.

Ниже приведен простой пример манифеста службы с отображением привилегированной точки входа SetupEntryPoint и главной точки входа EntryPoint для службы.

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

### <a name="configure-the-policy-by-using-a-local-account"></a>Настройка политики с использованием локальной учетной записи
Настроив службу для использования точки SetupEntryPoint, можно изменить разрешения безопасности, с которыми она выполняется в манифесте приложения. В приведенном ниже примере показано, как настроить службу для выполнения с правами учетной записи администратора пользователей.

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

Сначала создайте раздел **Principals** с именем пользователя, например SetupAdminUser. Это означает, что пользователь является членом системной группы "Администраторы".

Затем в разделе **ServiceManifestImport** настройте политику для применения этого субъекта к точке **SetupEntryPoint**. Теперь при выполнении файла **MySetup.bat** платформа Service Fabric будет использовать функцию `RunAs` с правами администратора. Если вы *не* применили другую политику к главной точке входа, код из файла **MyServiceHost.exe** будет запущен от имени системной учетной записи **NetworkService**. Это учетная запись по умолчанию, с использованием которой запускаются все точки входа службы.

Теперь добавим файл MySetup.bat в проект Visual Studio, чтобы проверить привилегии администратора. В Visual Studio щелкните правой кнопкой мыши проект службы и добавьте новый файл MySetup.bat.

Затем убедитесь, что файл MySetup.bat включен в пакет службы. По умолчанию он не включен. Щелкните файл правой кнопкой мыши, чтобы открыть контекстное меню, и выберите **Свойства**. Убедитесь, что в диалоговом окне "Свойства" параметр **Копировать в выходной каталог** имеет значение **Копировать, если новее**. Экран должен выглядеть следующим образом.

![Свойство CopyToOutput в Visual Studio для пакетного файла SetupEntryPoint][image1]

Теперь откройте файл MySetup.bat и добавьте следующие команды.

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Затем скомпилируйте и разверните решение в кластере локальной разработки. После запуска службы (это будет видно в Service Fabric Explorer) вы можете убедиться в успешном выполнении файла MySetup.bat двумя способами. Откройте командную строку PowerShell и введите следующую команду.

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

В Service Fabric Explorer запишите имя узла, в котором развернута и запущена служба (например Node 2). Затем перейдите в рабочую папку экземпляра приложения и найдите файл out.txt, в котором хранится значение **TestVariable**. Например, если служба была развернута на узле Node 2, для приложения **MyApplicationType** используйте такой путь:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a>Настройка политики с использованием учетных записей локальной системы
Выполнять скрипты запуска обычно лучше с помощью учетной записи локальной системы, а не учетной записи администратора. Выполнять политику запуска от имени с учетными записями из группы администраторов обычно невозможно, так как на компьютерах по умолчанию включено управление доступом на уровне пользователей. В таких случаях **рекомендуется выполнять SetupEntryPoint с учетной записью LocalSystem, а не от имени локального пользователя из группы администраторов**. В следующем примере показана настройка SetupEntryPoint для запуска с учетной записью LocalSystem.

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

Чтобы запустить службу или точку входа установки в качестве **корня** на кластерах Linux, можно указать для **AccountType** значение **LocalSystem**.

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Запуск команд PowerShell из точки входа настройки
Чтобы запустить PowerShell из точки входа **SetupEntryPoint**, запустите **PowerShell.exe** в пакетном файле, который указывает на файл PowerShell. Сначала добавьте файл PowerShell в проект службы, например с именем **MySetup.ps1**. Не забудьте указать свойство *Копировать, если новее* , чтобы включить этот файл в состав пакета службы. В следующем примере показан пакетный файл для запуска файла PowerShell с именем MySetup.ps1, который задает системную переменную среды с именем **TestVariable**.

Файл MySetup.bat для запуска файла PowerShell.

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

В файле PowerShell добавьте следующую команду, чтобы задать системную переменную среды.

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> По умолчанию пакетный файл ищет файлы в папке приложения с именем **work**. В этом примере нам нужно, чтобы пакетный файл MySetup.bat при запуске нашел файл MySetup.ps1 в той же папке, в которой расположен **пакет кода** приложения. Чтобы изменить эту папку, задайте рабочую папку:
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
Иногда при отладке нужно просмотреть вывод консоли, в которой выполняется скрипт. Для этого можно определить политику перенаправления консоли, которая записывает выходные данные в файл. Выходной файл сохраняется в папку приложения с именем **log** на том узле, где развертывается и выполняется приложение. (Сведения о том, как найти этот узел, см. в примере выше.)

> [!WARNING]
> Никогда не используйте политику перенаправления консоли для приложений в рабочей среде, так как она может повлиять на отработку отказа приложения. Используйте ее *только* для локальной разработки и отладки.  
> 
> 

В приведенном ниже примере показано, как установить для перенаправления консоли значение FileRetentionCount.

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Если теперь изменить файл MySetup.ps1 для вывода данных командой **Echo**, эти данные будут записаны в выходной файл, который можно использовать для отладки.

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

**Завершив отладку сценария, немедленно удалите эту политику перенаправления консоли.**

## <a name="configure-a-policy-for-service-code-packages"></a>Настройка политики для пакетов кода службы
Выше мы описали, как применить к точке входа SetupEntryPoint политику запуска от имени. Теперь давайте подробнее рассмотрим процесс создания разных субъектов, которые могут применяться в качестве политик служб.

### <a name="create-local-user-groups"></a>Создание локальных групп пользователей
Вы можете определять и создавать группы пользователей, в которые можно добавить одного или нескольких пользователей. Это полезно, если для разных точек входа службы есть несколько пользователей и у них должны быть определены общие права, доступные на уровне группы. В следующем примере представлена локальная группа с именем **LocalAdminGroup** и привилегиями администратора. В нее входят два пользователя: Customer1 и Customer2.

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
Можно создать локального пользователя и использовать его для защиты службы в приложении. Если в разделе Principals манифеста приложения указан тип учетной записи **LocalUser** , платформа Service Fabric создает учетные записи локальных пользователей на компьютерах с развернутым приложением. По умолчанию эти учетные записи не соответствуют именам, указанным в манифесте приложения (например, Customer3 в примере ниже). Вместо этого они создаются динамически и имеют случайные пароли.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Если для приложения требуется, чтобы учетная запись и пароль пользователя совпадали на всех компьютерах (например, чтобы включить аутентификацию NTLM), в манифесте кластера для параметра NTLMAuthenticationEnabled должно быть задано значение true. В нем также должен быть задан параметр NTLMAuthenticationPasswordSecret, который используется для создания одинакового пароля на всех компьютерах.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a>Назначение политик пакетам кода службы
В разделе **RunAsPolicy** для **ServiceManifestImport** определяется учетная запись из раздела Principals, которая будет использоваться для выполнения пакета кода. Также это позволяет связать пакеты кода из манифеста службы с учетными записями пользователей в разделе Principals. Это можно сделать для точки входа Setup или Main. Также можно указать значение `All`, чтобы применить настройки к обеим точкам входа. Следующий пример демонстрирует применение разных политик.

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Если параметр **EntryPointType** не указан, по умолчанию используется EntryPointType="Main". Параметр **SetupEntryPoint** особенно полезен, если для установки нужно выполнить действия с расширенными правами от имени системной учетной записи. Фактический код может выполняться под учетной записью с более низкими привилегиями.

### <a name="apply-a-default-policy-to-all-service-code-packages"></a>Применение политики по умолчанию ко всем пакетам кода службы
С помощью раздела **DefaultRunAsPolicy** можно указать учетную запись пользователя по умолчанию для всех пакетов кода, для которых не определен раздел **RunAsPolicy**. Иногда большую часть пакетов кода, указанных в используемых приложением манифестах служб, нужно запускать от имени одной и той же учетной записи пользователя. В таком случае в приложении можно определить стандартную политику запуска от имени этой учетной записи пользователя. Следующий пример устанавливает такие правила: если для пакета кода не указана политика **RunAsPolicy**, он будет запускаться под учетной записью **MyDefaultAccount**, указанной в разделе Principals.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Использование групп и пользователей домена Active Directory
Если экземпляр Service Fabric установлен на Windows Server с помощью автономного установщика, вы можете запустить службу с учетными данными группы или пользователя Active Directory. Речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD). С помощью пользователей или групп домена вы можете обращаться к другим ресурсам в домене (например, к общим файловым ресурсам), для которых предоставлены разрешения на доступ.

В следующем примере представлена учетная запись пользователя Active Directory с именем *TestUser* и паролем, зашифрованным с помощью сертификата с именем *MyCert*. Можно использовать команду PowerShell `Invoke-ServiceFabricEncryptText` для создания секретного зашифрованного текста. Дополнительные сведения см. в статье [Управление секретами в приложениях Service Fabric](service-fabric-application-secret-management.md).

На локальном компьютере следует развернуть закрытый ключ сертификата, что позволит расшифровывать на нем пароль с использованием внешних средств (в Azure для этого используется Azure Resource Manager). Тогда Service Fabric сможет расшифровать секретный код при развертывании пакета службы на компьютере и использовать его вместе с именем пользователя для проверки подлинности в Active Directory.

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
Если экземпляр Service Fabric установлен на Windows Server с помощью автономного установщика, вы можете запустить службу в качестве групповой управляемой учетной записи службы (gMSA). Обратите внимание, что речь идет о локальной службе Active Directory в домене, а не Azure Active Directory (Azure AD). При использовании групповой управляемой учетной записи службы в `Application Manifest` не сохраняется ни обычный, ни зашифрованный пароль.

В следующем примере показано, как создать групповую управляемую учетную запись службы *svc-Test$*, развернуть эту учетную запись на узлах кластера и настроить субъект-пользователь.

##### <a name="prerequisites"></a>Предварительные требования.
- Домену нужен корневой ключ KDS.
- Домен должен иметь функциональный уровень Windows Server 2012 или выше.

##### <a name="example"></a>Пример
1. Попросите администратора домена Active Directory создать групповую управляемую учетную запись службы с помощью командлета `New-ADServiceAccount` и убедитесь, что `PrincipalsAllowedToRetrieveManagedPassword` включает в себя все узлы кластера Service Fabric. Обратите внимание, что `AccountName`, `DnsHostName` и `ServicePrincipalName` должны быть уникальными.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Установите и протестируйте групповую управляемую учетную запись на каждом из узлов кластера Service Fabric (например, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`).
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Настройте субъекта-пользователя, а также тег RunAsPolicy, чтобы он указывал на этого пользователя.
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
Если к службе применяется политика запуска от имени, а манифест службы объявляет в качестве ресурсов конечные точки, использующие протокол HTTP, вам нужно указать **SecurityAccessPolicy**. Это гарантирует, что к выделенным для этих конечных точек портам будут правильно применены списки управления доступом для той учетной записи, от имени которой выполняется служба. В противном случае файл **http.sys** не получит доступа к службе, а вызовы от клиента будут завершаться ошибками. В следующем примере учетная запись Customer1 применяется к конечной точке с именем **EndpointName**, предоставляя ей права полного доступа.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Для конечной точки HTTPS необходимо также указать имя сертификата, который будет возвращен клиенту. Это можно сделать с помощью политики **EndpointBindingPolicy**и сертификата, определенного в разделе Certificates в манифесте приложения.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Обновление нескольких приложений с помощью конечных точек HTTPS
Не используйте **один и тот же порт** для разных экземпляров одного и того же приложения при использовании HTTP**S**. Это связано с тем, что Service Fabric не сможет обновить сертификат одного из экземпляров приложения. Например, если для приложений 1 и 2 необходимо обновить сертификат 1 до сертификата 2. При обновлении Service Fabric может очистить данные регистрации сертификата 1 с помощью процесса http.sys, даже если он используется другим приложением. Чтобы избежать этого, Service Fabric определяет, что другой экземпляр приложения уже зарегистрирован на порте с сертификатом (из-за http.sys) и завершает операцию.

Поэтому Service Fabric не поддерживает обновление двух разных служб, использующих **один порт** в разных экземплярах приложения. Другими словами нельзя использовать один сертификат для разных служб в одном порте. Если необходимо иметь сертификат с общим доступом в одном порте, убедитесь, что службы размещены на разных компьютерах с ограничениями на размещение. Или по возможности используйте динамические порты Service Fabric для каждой службы в экземпляре приложения. 

Если при обновлении произойдет ошибка HTTP, появится предупреждение о том, что API сервера HTTP Windows не поддерживает несколько сертификатов для приложений, которые совместно используют порт.

## <a name="a-complete-application-manifest-example"></a>Полный пример манифеста приложения
В следующем манифесте приложения показано, как можно использовать разные параметре.

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
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


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
* [Сведения о модели приложения](service-fabric-application-model.md)
* [Указание ресурсов в манифесте службы](service-fabric-service-manifest-resources.md)
* [Развертывание приложения](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
