---
title: "aaaCloud роль служб config XPath памятку | Документы Microsoft"
description: "Здравствуйте, различные параметры XPath, который можно использовать в tooexpose параметры конфигурации роли hello облачной службы в качестве переменной среды."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Предоставление параметров конфигурации ролей как переменной среды с помощью XPath
В hello облачной службы рабочего процесса или файл определения веб-роль службы можно предоставить значения конфигурации времени выполнения в переменных среды. поддерживаются следующие значения XPath Hello (что соответствует tooAPI значения).

Эти значения XPath также доступны через hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) библиотеки. 

## <a name="app-running-in-emulator"></a>Приложение, запущенное в эмуляторе
Указывает, что приложение hello выполняется в эмуляторе hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| Код |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>Идентификатор развертывания
Извлекает идентификатор hello развертывания для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| Код |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>Идентификатор роли
Возвращает идентификатор текущей роли hello для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| Код |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Обновление домена
Получает домен обновления hello hello экземпляра.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| Код |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Домен сбоя
Получает домен сбоя hello hello экземпляра.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| Код |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Имя роли
Возвращает имя роли hello hello экземпляров.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| Код |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Параметр конфигурации
Извлекает значение hello hello заданное параметром конфигурации.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| Код |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Путь к локальному хранилищу
Извлекает hello путь локального хранилища для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| Код |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>Размер локального хранилища
Получает размер hello hello локального хранилища для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| Код |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Протокол конечной точки
Извлекает hello протокол конечной точки для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| Код |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>IP-адрес конечной точки
Возвращает hello указан IP-адрес конечной точки.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| Код |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>Порт конечной точки
Извлекает hello порт конечной точки для экземпляра hello.

| Тип | Пример |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| Код |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>Пример
Ниже приведен пример рабочей роли, которая создает задачу запуска с переменной среды с именем `TestIsEmulated` задать toohello [ @emulated значение xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) файла.

Создайте пакет [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .

Включите [удаленный рабочий стол](cloud-services-role-enable-remote-desktop.md) для роли.

