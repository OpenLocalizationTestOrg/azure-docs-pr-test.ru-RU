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
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="eb713-103">Предоставление параметров конфигурации ролей как переменной среды с помощью XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="eb713-104">В hello облачной службы рабочего процесса или файл определения веб-роль службы можно предоставить значения конфигурации времени выполнения в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="eb713-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="eb713-105">поддерживаются следующие значения XPath Hello (что соответствует tooAPI значения).</span><span class="sxs-lookup"><span data-stu-id="eb713-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="eb713-106">Эти значения XPath также доступны через hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="eb713-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="eb713-107">Приложение, запущенное в эмуляторе</span><span class="sxs-lookup"><span data-stu-id="eb713-107">App running in emulator</span></span>
<span data-ttu-id="eb713-108">Указывает, что приложение hello выполняется в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="eb713-109">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-109">Type</span></span> | <span data-ttu-id="eb713-110">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-111">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-111">XPath</span></span> |<span data-ttu-id="eb713-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="eb713-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="eb713-113">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-113">Code</span></span> |<span data-ttu-id="eb713-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="eb713-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="eb713-115">Идентификатор развертывания</span><span class="sxs-lookup"><span data-stu-id="eb713-115">Deployment ID</span></span>
<span data-ttu-id="eb713-116">Извлекает идентификатор hello развертывания для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="eb713-117">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-117">Type</span></span> | <span data-ttu-id="eb713-118">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-119">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-119">XPath</span></span> |<span data-ttu-id="eb713-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="eb713-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="eb713-121">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-121">Code</span></span> |<span data-ttu-id="eb713-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="eb713-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="eb713-123">Идентификатор роли</span><span class="sxs-lookup"><span data-stu-id="eb713-123">Role ID</span></span>
<span data-ttu-id="eb713-124">Возвращает идентификатор текущей роли hello для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="eb713-125">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-125">Type</span></span> | <span data-ttu-id="eb713-126">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-127">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-127">XPath</span></span> |<span data-ttu-id="eb713-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="eb713-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="eb713-129">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-129">Code</span></span> |<span data-ttu-id="eb713-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="eb713-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="eb713-131">Обновление домена</span><span class="sxs-lookup"><span data-stu-id="eb713-131">Update domain</span></span>
<span data-ttu-id="eb713-132">Получает домен обновления hello hello экземпляра.</span><span class="sxs-lookup"><span data-stu-id="eb713-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="eb713-133">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-133">Type</span></span> | <span data-ttu-id="eb713-134">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-135">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-135">XPath</span></span> |<span data-ttu-id="eb713-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="eb713-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="eb713-137">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-137">Code</span></span> |<span data-ttu-id="eb713-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="eb713-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="eb713-139">Домен сбоя</span><span class="sxs-lookup"><span data-stu-id="eb713-139">Fault domain</span></span>
<span data-ttu-id="eb713-140">Получает домен сбоя hello hello экземпляра.</span><span class="sxs-lookup"><span data-stu-id="eb713-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="eb713-141">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-141">Type</span></span> | <span data-ttu-id="eb713-142">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-143">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-143">XPath</span></span> |<span data-ttu-id="eb713-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="eb713-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="eb713-145">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-145">Code</span></span> |<span data-ttu-id="eb713-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="eb713-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="eb713-147">Имя роли</span><span class="sxs-lookup"><span data-stu-id="eb713-147">Role name</span></span>
<span data-ttu-id="eb713-148">Возвращает имя роли hello hello экземпляров.</span><span class="sxs-lookup"><span data-stu-id="eb713-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="eb713-149">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-149">Type</span></span> | <span data-ttu-id="eb713-150">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-151">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-151">XPath</span></span> |<span data-ttu-id="eb713-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="eb713-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="eb713-153">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-153">Code</span></span> |<span data-ttu-id="eb713-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="eb713-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="eb713-155">Параметр конфигурации</span><span class="sxs-lookup"><span data-stu-id="eb713-155">Config setting</span></span>
<span data-ttu-id="eb713-156">Извлекает значение hello hello заданное параметром конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eb713-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="eb713-157">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-157">Type</span></span> | <span data-ttu-id="eb713-158">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-159">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-159">XPath</span></span> |<span data-ttu-id="eb713-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="eb713-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="eb713-161">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-161">Code</span></span> |<span data-ttu-id="eb713-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="eb713-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="eb713-163">Путь к локальному хранилищу</span><span class="sxs-lookup"><span data-stu-id="eb713-163">Local storage path</span></span>
<span data-ttu-id="eb713-164">Извлекает hello путь локального хранилища для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="eb713-165">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-165">Type</span></span> | <span data-ttu-id="eb713-166">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-167">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-167">XPath</span></span> |<span data-ttu-id="eb713-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="eb713-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="eb713-169">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-169">Code</span></span> |<span data-ttu-id="eb713-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="eb713-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="eb713-171">Размер локального хранилища</span><span class="sxs-lookup"><span data-stu-id="eb713-171">Local storage size</span></span>
<span data-ttu-id="eb713-172">Получает размер hello hello локального хранилища для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="eb713-173">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-173">Type</span></span> | <span data-ttu-id="eb713-174">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-175">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-175">XPath</span></span> |<span data-ttu-id="eb713-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="eb713-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="eb713-177">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-177">Code</span></span> |<span data-ttu-id="eb713-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="eb713-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="eb713-179">Протокол конечной точки</span><span class="sxs-lookup"><span data-stu-id="eb713-179">Endpoint protocol</span></span>
<span data-ttu-id="eb713-180">Извлекает hello протокол конечной точки для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="eb713-181">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-181">Type</span></span> | <span data-ttu-id="eb713-182">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-183">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-183">XPath</span></span> |<span data-ttu-id="eb713-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="eb713-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="eb713-185">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-185">Code</span></span> |<span data-ttu-id="eb713-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="eb713-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="eb713-187">IP-адрес конечной точки</span><span class="sxs-lookup"><span data-stu-id="eb713-187">Endpoint IP</span></span>
<span data-ttu-id="eb713-188">Возвращает hello указан IP-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="eb713-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="eb713-189">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-189">Type</span></span> | <span data-ttu-id="eb713-190">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-191">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-191">XPath</span></span> |<span data-ttu-id="eb713-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="eb713-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="eb713-193">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-193">Code</span></span> |<span data-ttu-id="eb713-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="eb713-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="eb713-195">Порт конечной точки</span><span class="sxs-lookup"><span data-stu-id="eb713-195">Endpoint port</span></span>
<span data-ttu-id="eb713-196">Извлекает hello порт конечной точки для экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="eb713-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="eb713-197">Тип</span><span class="sxs-lookup"><span data-stu-id="eb713-197">Type</span></span> | <span data-ttu-id="eb713-198">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="eb713-199">XPath</span><span class="sxs-lookup"><span data-stu-id="eb713-199">XPath</span></span> |<span data-ttu-id="eb713-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="eb713-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="eb713-201">Код</span><span class="sxs-lookup"><span data-stu-id="eb713-201">Code</span></span> |<span data-ttu-id="eb713-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="eb713-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="eb713-203">Пример</span><span class="sxs-lookup"><span data-stu-id="eb713-203">Example</span></span>
<span data-ttu-id="eb713-204">Ниже приведен пример рабочей роли, которая создает задачу запуска с переменной среды с именем `TestIsEmulated` задать toohello [ @emulated значение xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="eb713-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="eb713-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb713-205">Next steps</span></span>
<span data-ttu-id="eb713-206">Дополнительные сведения о hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) файла.</span><span class="sxs-lookup"><span data-stu-id="eb713-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="eb713-207">Создайте пакет [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="eb713-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="eb713-208">Включите [удаленный рабочий стол](cloud-services-role-enable-remote-desktop.md) для роли.</span><span class="sxs-lookup"><span data-stu-id="eb713-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

