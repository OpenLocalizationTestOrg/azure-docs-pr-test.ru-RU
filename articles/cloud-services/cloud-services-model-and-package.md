---
title: "aaaWhat — это модель облачной службы и пакета | Документы Microsoft"
description: "Описывает модель облачной службы hello (.csdef, .cscfg) и пакет (cspkg-файл) в Azure"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Что такое hello модели облачной службы и как его упаковки?
Облачная служба создается из трех компонентов, определение службы hello *(.csdef)*, hello файла конфигурации службы *(.cscfg)*и пакет службы *(.cspkg)*. Оба hello **ServiceDefinition.csdef** и **ServiceConfig.cscfg** файлы основаны на XML и описывают структуру hello hello облачной службы и как оно настроено; под общим названием hello модели. Hello **ServicePackage.cspkg** является ZIP-файл, созданный из hello **ServiceDefinition.csdef** и помимо прочего, содержит все необходимые hello двоичном формате зависимости. Azure создает облачную службу из обоих hello **ServicePackage.cspkg** и hello **ServiceConfig.cscfg**.

После запуска hello облачной службы в Azure можно перенастроить ее через hello **ServiceConfig.cscfg** файла, но его невозможно изменить определение hello.

## <a name="what-would-you-like-tooknow-more-about"></a>Как Дополнительные сведения о tooknow?
* Требуется больше о hello tooknow [ServiceDefinition.csdef](#csdef) и [ServiceConfig.cscfg](#cscfg) файлов.
* Я уже знаю об этих файлах, покажите мне [примеры](#next-steps) того, что я могу настроить.
* Я хочу toocreate hello [ServicePackage.cspkg](#cspkg).
* Я использую Visual Studio и хочу выполнить следующие действия.
  * [Создать облачную службу.][vs_create]
  * [Изменить конфигурацию существующей облачной службы.][vs_reconfigure]
  * [Развернуть проект облачной службы.][vs_deploy]
  * [Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Hello **ServiceDefinition.csdef** файл задает hello параметры, используемые Azure tooconfigure облачной службы. Hello [схема определения службы Azure (.csdef файла)](https://msdn.microsoft.com/library/azure/ee758711.aspx) предоставляет hello допустимый формат файла определения службы. Hello ниже приведен пример hello параметры, которые могут быть определены для hello Web и рабочих ролей.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Можно ссылаться toohello [схема определения службы](https://msdn.microsoft.com/library/azure/ee758711.aspx) для лучшего понимания hello XML-схемы, используемые здесь, однако здесь приводится краткое описание некоторых hello элементов:

**Sites**  
Содержит определения hello для веб-сайтов или веб-приложений, размещаемых в IIS7.

**InputEndpoints**  
Содержит определения hello для конечных точек, которые используются toocontact hello облачной службы.

**InternalEndpoints**  
Содержит определения hello для конечных точек, используемых toocommunicate экземпляры роли друг с другом.

**ConfigurationSettings**  
Содержит определения параметров hello для функций определенной роли.

**Сертификаты**  
Содержит определения hello для сертификатов, которые необходимы для роли. Предыдущий пример кода Hello показан сертификат, используемый для настройки hello Azure Connect.

**LocalResources**  
Содержит определения hello для локальных ресурсов хранения. Ресурс локального хранилища представляет собой зарезервированный каталог в файловой системе hello hello виртуальной машины, в которой выполняется экземпляр роли.

**Imports**  
Содержит определения hello для импортированных модулей. Предыдущий пример кода Hello содержит модули, hello для удаленного рабочего стола и Azure Connect.

**Startup**  
Содержит задачи, которые выполняются при запуске роли hello. Hello задачи определяются в файле CMD или исполняемого файла.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
Настройка Hello hello параметров для облачной службы определяется значениями hello в hello **ServiceConfiguration.cscfg** файла. Указать hello число экземпляров, что требуется toodeploy для каждой роли в этом файле. Hello значения для параметров конфигурации hello, которые определены в файле определения службы hello добавляются toohello файла конфигурации службы. Hello отпечатки всех сертификатов управления, связанные с hello облачной службы также добавляются в файл toohello. Hello [схема конфигурации службы Azure (csfg файла)](https://msdn.microsoft.com/library/azure/ee758710.aspx) предоставляет hello допустимый формат файла конфигурации службы.

Hello службы файл конфигурации не упаковывается с приложением hello, но загруженного tooAzure как отдельный файл и — используется tooconfigure hello облачной службы. Вы можете отправить новый файл конфигурации службы без повторного развертывания облачной службы. значения параметров конфигурации Hello hello облачной службы можно изменить во время выполнения hello облачной службы. Hello ниже приведен пример hello параметры конфигурации, которые могут быть определены для hello Web и рабочих ролей.

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Можно ссылаться toohello [схема конфигурации службы](https://msdn.microsoft.com/library/azure/ee758710.aspx) для улучшения понимания hello схемы XML, используемый здесь, однако здесь приводится краткое описание hello элементов:

**Экземпляры**  
Задает количество запущенных экземпляров роли hello hello. tooprevent вашей облачной службы из потенциально становится недоступным во время обновления, рекомендуется развернуть более одного экземпляра вашего веб-ролей. Развертывая более одного экземпляра, вы придерживаетесь toohello рекомендации в hello [Azure вычислений службы соглашения об уровне](http://azure.microsoft.com/support/legal/sla/), это гарантирует 99,95% внешней доступности для ролей с выходом в Интернет, когда два или несколько ролей экземпляры будут развернуты для службы.

**ConfigurationSettings**  
Настраивает параметры hello hello запущенных экземпляров роли. Имя Hello hello `<Setting>` элементов должен соответствовать hello определения параметров в файле определения службы hello.

**Сертификаты**  
Настраивает hello сертификаты, используемые службой hello. Hello предыдущий пример кода показывает, как toodefine hello сертификат для модуля RemoteAccess hello. Здравствуйте, значение hello *отпечаток* атрибут должен быть задан toohello отпечаток сертификата toouse hello.

<p/>

> [!NOTE]
> Hello отпечаток сертификата hello можно добавить файл конфигурации toohello, используя текстовый редактор. Или может быть добавлено значение hello hello **сертификаты** вкладка hello **свойства** страницы приветствия роли в Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Определение портов для экземпляров ролей
Azure позволяет только одна запись tooa точка веб-роли. Это означает, что весь трафик идет через один IP-адрес. Ваш веб-сайтов tooshare порт можно настроить путем настройки hello узла заголовок toodirect hello запроса toohello правильное расположение. Можно также настроить порты toowell известного toolisten вашего приложения hello IP-адреса.

Hello ниже приведен пример hello конфигурации для веб-роли с веб-сайта и веб-приложения. Hello веб-сайт настроен как расположение входа по умолчанию hello на порт 80, а hello веб-приложения, настроенные tooreceive запросов из альтернативного заголовка узла, называется «mail.mysite.cloudapp.net».

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Изменение конфигурации роли hello
Можно обновить конфигурацию hello облачной службы, запущенной в Azure, не отключая службы hello. toochange сведения о конфигурации, можно либо отправить новый файл конфигурации, или изменить файл конфигурации hello в поместите и применить его tooyour, на котором выполняется служба. Hello внесены следующие изменения могут быть toohello конфигурации службы:

* **Изменение hello значений параметров конфигурации**  
  При конфигурации изменения, параметров экземпляра роли можно изменить hello tooapply, когда экземпляр hello находится в сети, или экземпляр hello toorecycle надлежащим образом и применить изменение hello в том случае, когда экземпляр hello отключен от сети.
* **Изменение топологии службы hello экземпляров ролей**  
  Изменения топологии не влияют на выполняемые экземпляры, кроме случаев, когда экземпляр удаляется. Все остальные экземпляры обычно не обязательно toobe перезапуску; Тем не менее вы можете toorecycle экземпляров роли в изменение топологии tooa ответа.
* **Изменение отпечатка сертификата hello**  
  Вы можете обновлять сертификат, только когда экземпляр роли запущен в автономном режиме. Если сертификат добавлен, удален или изменен, когда экземпляр роли находится в оперативном режиме, Azure надлежащим образом принимает сертификат hello tooupdate автономного экземпляра hello и подключить его обратно после завершения изменений hello.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Обработка изменений конфигурации с помощью событий среды выполнения службы
Hello [библиотека времени выполнения Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) включает hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) пространства имен, которое предоставляет классы для взаимодействия с hello средой Azure из роли. Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) класс определяет hello следующие события, которые вызываются до и после изменения конфигурации:

* Событие **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**.  
  Это происходит до примененных tooa указанного экземпляра роли, предоставляя возможность tootake работу экземпляров роли hello при необходимости изменения конфигурации hello.
* Событие **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**.  
  Происходит после изменения конфигурации hello примененных tooa указанного экземпляра роли.

> [!NOTE]
> Поскольку изменения сертификата всегда отключите hello экземпляров роли, они не вызывают событий RoleEnvironment.Changing и RoleEnvironment.Changed hello.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy приложения как облачной службы в Azure необходимо первого пакета приложения hello в соответствующем формате hello. Можно использовать hello **CSPack** средство командной строки (установлен с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello пакета файл в качестве альтернативного tooVisual Studio.

**CSPack** использует hello содержимое hello службы определение файловые службы и службы содержимое файла конфигурации toodefine hello hello пакета. **CSPack** создает файл пакета приложения (cspkg-файл), вы можете отправить tooAzure с помощью hello [портал Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). По умолчанию с именем пакета hello `[ServiceDefinitionFileName].cspkg`, но можно указать другое имя с помощью hello `/out` параметр **CSPack**.

Расположение **CSPack** приведено ниже.  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> Доступна CSPack.exe (в windows), запустив hello **командной строки пакета Microsoft Azure** ярлык, который устанавливается вместе с hello SDK.  
> 
> Запустите программу CSPack.exe hello сам по себе toosee документации о всех возможных параметрах hello и команд.
> 
> 

<p />

> [!TIP]
> Запустить облачную службу локально в hello **эмулятор вычислений Microsoft Azure**, использовать hello **/copyonly** параметр. Этот параметр копирует hello двоичные файлы для hello приложения tooa каталог макета, из которого они могут выполняться в эмуляторе вычислений hello.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Пример команды toopackage облачной службы
Hello следующий пример создает пакет приложения, содержащий hello сведения для веб-роли. Команда Hello указывает toouse файла определения службы hello, hello каталог, где двоичные файлы могут быть найдены и hello имя файла пакета hello.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Если приложение hello содержит веб-роли и рабочей роли, hello следующая команда используется:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Где hello переменные определены следующим образом:

| Переменная | Значение |
| --- | --- |
| \[DirectoryName\] |Hello вложенную Привет корневого каталога проекта, содержащий файл csdef hello hello проекта Azure. |
| \[ServiceDefinition\] |Имя файла определения службы hello Hello. По умолчанию этот файл называется ServiceDefinition.csdef. |
| \[OutputFileName\] |Имя Hello hello создан файл пакета. Как правило этот параметр задается имя toohello приложения hello. Если имя файла не указано, пакет приложения hello создается как \[ApplicationName\]cspkg-файл. |
| \[RoleName\] |Имя роли hello, заданное в файле определения службы hello Hello. |
| \[RoleBinariesDirectory] |расположение Hello hello двоичные файлы для роли hello. |
| \[VirtualPath\] |Hello физические каталоги для каждого виртуального пути, заданные в разделе сайтов hello hello определения службы. |
| \[PhysicalPath\] |физические каталоги Hello hello содержимого для каждого виртуального пути, определенные в узел hello hello определения службы. |
| \[RoleAssemblyName\] |Имя Hello hello двоичного файла для роли hello. |

## <a name="next-steps"></a>Дальнейшие действия
Я создаю пакет облачной службы и я хочу выполнить следующие действия.

* [Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]
* [Развернуть проект облачной службы.][deploy]

Я использую Visual Studio и хочу выполнить следующие действия.

* [Создать новую облачную службу.][vs_create]
* [Изменить конфигурацию существующей облачной службы.][vs_reconfigure]
* [Развернуть проект облачной службы.][vs_deploy]
* [Настроить удаленный рабочий стол для экземпляра облачной службы.][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
