---
title: "Что такое модель и пакет облачной службы | Документация Майкрософт"
description: "Описание модели (CSDEF-файл, CSCFG-файл) и пакета облачной службы (CSPKG-файл) в Azure"
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a>Что такое модель облачных служб и как создать ее пакет?
Облачная служба создается из трех компонентов: определения службы *(CSDEF-файл)*, конфигурации службы *(CSCFG-файл)* и пакета службы *(CSPKG-файл)*. Файлы **ServiceDefinition.csdef** и **ServiceConfig.cscfg** являются XML-файлами, которые описывают структуру облачной службы и ее конфигурацию. В совокупности это называется моделью. **ServicePackage.cspkg** — это ZIP-файл, который создается на основе файла **ServiceDefinition.csdef** и который, помимо прочего, содержит все необходимые зависимости в двоичном формате. Azure создает облачную службу из двух файлов: **ServicePackage.cspkg** и **ServiceConfig.cscfg**.

После запуска облачной службы в Azure вы можете перенастроить ее с помощью файла **ServiceConfig.cscfg** , но вы не сможете изменить определение.

## <a name="what-would-you-like-to-know-more-about"></a>Что еще вы хотите узнать?
* Я хочу узнать больше о файлах [ServiceDefinition.csdef](#csdef) и [ServiceConfig.cscfg](#cscfg).
* Я уже знаю об этих файлах, покажите мне [примеры](#next-steps) того, что я могу настроить.
* Я хочу создать файл [ServicePackage.cspkg](#cspkg).
* Я использую Visual Studio и хочу выполнить следующие действия.
  * [Создать облачную службу.][vs_create]
  * [Изменить конфигурацию существующей облачной службы.][vs_reconfigure]
  * [Развернуть проект облачной службы.][vs_deploy]
  * [Настроить удаленный рабочий стол для экземпляра облачной службы.][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Файл **ServiceDefinition.csdef** задает параметры, используемые Azure для настройки облачной службы. [Схема определения службы Azure (CSDEF-файл)](https://msdn.microsoft.com/library/azure/ee758711.aspx) предоставляет допустимый формат для файла определения службы. В следующем примере показаны параметры, которые могут быть определены для веб-ролей и рабочих ролей.

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

Чтобы лучше понять используемую здесь схему XML, изучите статью [Схема определения службы](https://msdn.microsoft.com/library/azure/ee758711.aspx). В ней приводится краткое описание некоторых элементов.

**Sites**  
Содержит определения для веб-сайтов или веб-приложений, размещаемых в IIS7.

**InputEndpoints**  
Содержит определения для конечных точек, используемых для связи с облачной службой.

**InternalEndpoints**  
Содержит определения для конечных точек, используемых экземплярами роли для взаимодействия друг с другом.

**ConfigurationSettings**  
Содержит определения параметров для функций конкретной роли.

**Certificates**  
Содержит определения для сертификатов, которые необходимы для роли. В предыдущем примере кода показан сертификат, используемый для настройки Azure Connect.

**LocalResources**  
Содержит определения для локальных ресурсов хранилища. Локальный ресурс хранилища — это зарезервированный каталог в файловой системе виртуальной машины, в которой выполняется экземпляр роли.

**Imports**  
Содержит определения для импортированных модулей. В предыдущем примере кода показаны модули для удаленного рабочего стола и Azure Connect.

**Startup**  
Содержит задачи, которые выполняются при запуске роли. Задачи определены в CMD-файле или исполняемом файле.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
Настройка параметров для облачной службы определяется значениями в файле **ServiceConfiguration.cscfg** . Вы указываете количество экземпляров, которые необходимо развернуть для каждой роли в этом файле. Значения для параметров конфигурации, которые определены в файле определения службы, добавляются в файл конфигурации службы. Отпечатки всех сертификатов управления, связанных с облачной службы, также добавляются в файл. [Схема конфигурации службы Azure (CSCFG-файл)](https://msdn.microsoft.com/library/azure/ee758710.aspx) предоставляет допустимый формат файла конфигурации службы.

Файл конфигурации службы не упакован с приложением; он передается в Azure как отдельный файл и используется для конфигурации облачной службы. Вы можете отправить новый файл конфигурации службы без повторного развертывания облачной службы. Значения конфигурации для облачной службы можно изменить во время работы облачной службы. В следующем примере показаны параметры конфигурации, которые можно определить для рабочих ролей и веб-ролей.

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

Чтобы лучше понять используемую здесь схему XML, см. статью [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) (Схема конфигурации службы). В этой статье приводится краткое описание некоторых элементов.

**Экземпляры**  
Задает количество запущенных экземпляров для роли. Чтобы предотвратить возможную недоступность облачной службы во время обновлений, рекомендуется развернуть несколько экземпляров веб-ролей. Развертывая более одного экземпляра, вы выполните рекомендации [Соглашения об уровне обслуживания Azure Compute](http://azure.microsoft.com/support/legal/sla/), что гарантирует 99,95 % внешней доступности для ролей с выходом в Интернет, если для службы развернуто два (или более) экземпляра роли.

**ConfigurationSettings**  
Настраивает параметры для запущенных экземпляров роли. Имена элементов `<Setting>` должны соответствовать определениям параметров в файле определения службы.

**Certificates**  
Настраивает сертификаты, используемые службой. В предыдущем примере кода показано, как определить сертификат для модуля RemoteAccess. Значение атрибута *thumbprint* должно быть присвоено отпечатку сертификата, который будет использоваться.

<p/>

> [!NOTE]
> Отпечаток сертификата можно добавить в файл конфигурации с помощью текстового редактора. Или можно добавить соответствующее значение на вкладку **Сертификаты** страницы **Свойства** роли в Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Определение портов для экземпляров ролей
Azure разрешает только одну точку входа для веб-роли. Это означает, что весь трафик идет через один IP-адрес. Можно сделать так, чтобы веб-сайты совместно использовали порт. Для этого нужно настроить заголовок узла так, чтобы он направлял запрос в нужное расположение. Можно также настроить приложения для прослушивания известных портов по IP-адресу.

Следующий пример показывает конфигурацию для веб-роли с веб-сайтом и веб-приложением. Веб-сайт настроен как расположение входа по умолчанию с использованием порта 80. Веб-приложения настроены на получение запросов из альтернативного заголовка узла с именем mail.mysite.cloudapp.net.

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


## <a name="changing-the-configuration-of-a-role"></a>Изменение конфигурации роли
Вы можете обновить конфигурацию облачной службы, запущенной в Azure, не переводя службу в автономный режим. Чтобы изменить сведения о конфигурации, можно отправить новый файл конфигурации. Также можно изменить файл конфигурации локально и применить его к работающей службе. В конфигурацию службы можно внести следующие изменения.

* **Изменение значений параметров конфигурации.**  
  После изменения параметра конфигурации экземпляр роли может применить изменение во время работы экземпляра в сети. Или же он может предусмотрительно перезапустить экземпляр и применить изменение, пока экземпляр запущен в автономном режиме.
* **Изменение топологии службы экземпляров роли.**  
  Изменения топологии не влияют на выполняемые экземпляры, кроме случаев, когда экземпляр удаляется. Все остальные экземпляры обычно не нуждаются в перезапуске. Тем не менее можно выбрать перезапуск экземпляров роли в ответ на изменение топологии.
* **Изменение отпечатка сертификата.**  
  Вы можете обновлять сертификат, только когда экземпляр роли запущен в автономном режиме. Если сертификат добавлен, удален или изменен, когда экземпляр роли подключен к сети, Azure предусмотрительно переводит экземпляр в автономный режим для обновления сертификата. После применения изменения экземпляр снова подключается к сети.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Обработка изменений конфигурации с помощью событий среды выполнения службы
[Библиотека среды выполнения Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) содержит пространство имен [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx), которое предоставляет классы для взаимодействия со средой Azure из роли. Класс [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) определяет следующие события, которые вызываются до и после изменения конфигурации.

* Событие **[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)**.  
  Это событие происходит до применения изменения конфигурации к указанному экземпляру роли, предоставляя экземпляру роли возможность освободить экземпляры роли при необходимости.
* Событие **[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx)**.  
  Это событие происходит после применения изменения конфигурации к указанному экземпляру роли.

> [!NOTE]
> Поскольку изменения сертификата всегда переводят экземпляры роли в автономный режим, они не вызывают событий RoleEnvironment.Changing и RoleEnvironment.Changed.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
Чтобы развернуть приложение как облачную службу в Azure, необходимо вначале упаковать приложение в соответствующий формат. Можно использовать программу командной строки **CSPack** (устанавливается вместе с [Azure SDK](https://azure.microsoft.com/downloads/)) для создания файла пакета в качестве альтернативы Visual Studio.

**CSPack** использует содержимое файла определения службы и файла конфигурации службы для определения содержимого пакета. **CSPack** создает файл пакета приложения (CSPKG-файл), который можно отправить в Azure с помощью [портала Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). По умолчанию пакет называется `[ServiceDefinitionFileName].cspkg`, но вы можете указать другое имя, используя параметр `/out` в программе командной строки **CSPack**.

Расположение **CSPack** приведено ниже.  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> Чтобы найти файл CSPack.exe (в Windows), запустите ярлык **Командная строка Microsoft Azure** , который устанавливается вместе с пакетом SDK.  
> 
> Запустите программу CSPack.exe отдельно, чтобы просмотреть документацию обо всех возможных параметрах и командах.
> 
> 

<p />

> [!TIP]
> Запустите облачную службу локально в **эмуляторе вычислений Microsoft Azure**, использовав параметр **/copyonly**. При указании этого параметра двоичные файлы приложения копируются в структуру каталогов, из которой они могут выполняться в эмуляторе вычислений.
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a>Пример команды для упаковки облачной службы
В следующем примере создается пакет приложения, содержащий информацию для веб-роли. Команда задает используемый файл определения службы, а также каталог, в котором находятся двоичные файлы, и имя файла пакета.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Если приложение содержит веб-роль и рабочую роль, используется следующая команда.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Здесь переменные определены следующим образом.

| Переменная | Значение |
| --- | --- |
| \[DirectoryName\] |Подкаталог в корневом каталоге проекта, который содержит CSDEF-файл проекта Azure. |
| \[ServiceDefinition\] |Имя файла определения службы. По умолчанию этот файл называется ServiceDefinition.csdef. |
| \[OutputFileName\] |Имя создаваемого файла пакета. Как правило, ему присваивается имя приложения. Если имя файла не указано, создаваемому пакету приложения с расширением CSPKG присваивается \[имя приложения\]. |
| \[RoleName\] |Имя роли, определенное в файле определения службы. |
| \[RoleBinariesDirectory] |Расположение двоичных файлов для роли. |
| \[VirtualPath\] |Физические каталоги для каждого виртуального пути, определенного в разделе «Сайты» определения службы. |
| \[PhysicalPath\] |Физические каталоги содержимого для каждого виртуального пути, заданного в узле «Сайт» определения службы. |
| \[RoleAssemblyName\] |Имя двоичного файла для роли. |

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
