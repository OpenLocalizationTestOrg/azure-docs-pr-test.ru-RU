---
title: "Памятка по конфигурации XPath для роли облачных служб | Документация Майкрософт"
description: "Различные параметры XPath можно использовать в конфигурации роли облачной службы, чтобы предоставить их в качестве переменных среды."
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
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="1038d-103">Предоставление параметров конфигурации ролей как переменной среды с помощью XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="1038d-104">В файле определения службы рабочей роли или веб-роли облачной службы можно предоставить значения конфигурации среды выполнения как переменные среды.</span><span class="sxs-lookup"><span data-stu-id="1038d-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="1038d-105">Поддерживаются следующие значения XPath (которые соответствуют значениям API).</span><span class="sxs-lookup"><span data-stu-id="1038d-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="1038d-106">Эти значения XPath также можно использовать с помощью библиотеки [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1038d-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="1038d-107">Приложение, запущенное в эмуляторе</span><span class="sxs-lookup"><span data-stu-id="1038d-107">App running in emulator</span></span>
<span data-ttu-id="1038d-108">Указывает, что приложение выполняется в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="1038d-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="1038d-109">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-109">Type</span></span> | <span data-ttu-id="1038d-110">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-111">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-111">XPath</span></span> |<span data-ttu-id="1038d-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="1038d-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="1038d-113">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-113">Code</span></span> |<span data-ttu-id="1038d-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="1038d-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="1038d-115">Идентификатор развертывания</span><span class="sxs-lookup"><span data-stu-id="1038d-115">Deployment ID</span></span>
<span data-ttu-id="1038d-116">Получает идентификатор развертывания для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="1038d-117">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-117">Type</span></span> | <span data-ttu-id="1038d-118">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-119">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-119">XPath</span></span> |<span data-ttu-id="1038d-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="1038d-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="1038d-121">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-121">Code</span></span> |<span data-ttu-id="1038d-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="1038d-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="1038d-123">Идентификатор роли</span><span class="sxs-lookup"><span data-stu-id="1038d-123">Role ID</span></span>
<span data-ttu-id="1038d-124">Получает идентификатор текущей роли для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="1038d-125">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-125">Type</span></span> | <span data-ttu-id="1038d-126">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-127">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-127">XPath</span></span> |<span data-ttu-id="1038d-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="1038d-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="1038d-129">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-129">Code</span></span> |<span data-ttu-id="1038d-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="1038d-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="1038d-131">Обновление домена</span><span class="sxs-lookup"><span data-stu-id="1038d-131">Update domain</span></span>
<span data-ttu-id="1038d-132">Получает домен обновления для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="1038d-133">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-133">Type</span></span> | <span data-ttu-id="1038d-134">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-135">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-135">XPath</span></span> |<span data-ttu-id="1038d-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="1038d-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="1038d-137">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-137">Code</span></span> |<span data-ttu-id="1038d-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="1038d-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="1038d-139">Домен сбоя</span><span class="sxs-lookup"><span data-stu-id="1038d-139">Fault domain</span></span>
<span data-ttu-id="1038d-140">Получает домен сбоя для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="1038d-141">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-141">Type</span></span> | <span data-ttu-id="1038d-142">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-143">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-143">XPath</span></span> |<span data-ttu-id="1038d-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="1038d-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="1038d-145">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-145">Code</span></span> |<span data-ttu-id="1038d-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="1038d-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="1038d-147">Имя роли</span><span class="sxs-lookup"><span data-stu-id="1038d-147">Role name</span></span>
<span data-ttu-id="1038d-148">Получает имя роли для экземпляров.</span><span class="sxs-lookup"><span data-stu-id="1038d-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="1038d-149">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-149">Type</span></span> | <span data-ttu-id="1038d-150">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-151">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-151">XPath</span></span> |<span data-ttu-id="1038d-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="1038d-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="1038d-153">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-153">Code</span></span> |<span data-ttu-id="1038d-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="1038d-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="1038d-155">Параметр конфигурации</span><span class="sxs-lookup"><span data-stu-id="1038d-155">Config setting</span></span>
<span data-ttu-id="1038d-156">Получает значение указанного параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1038d-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="1038d-157">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-157">Type</span></span> | <span data-ttu-id="1038d-158">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-159">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-159">XPath</span></span> |<span data-ttu-id="1038d-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="1038d-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="1038d-161">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-161">Code</span></span> |<span data-ttu-id="1038d-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="1038d-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="1038d-163">Путь к локальному хранилищу</span><span class="sxs-lookup"><span data-stu-id="1038d-163">Local storage path</span></span>
<span data-ttu-id="1038d-164">Получает путь к локальному хранилищу для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="1038d-165">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-165">Type</span></span> | <span data-ttu-id="1038d-166">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-167">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-167">XPath</span></span> |<span data-ttu-id="1038d-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="1038d-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="1038d-169">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-169">Code</span></span> |<span data-ttu-id="1038d-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="1038d-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="1038d-171">Размер локального хранилища</span><span class="sxs-lookup"><span data-stu-id="1038d-171">Local storage size</span></span>
<span data-ttu-id="1038d-172">Получает размер локального хранилища для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="1038d-173">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-173">Type</span></span> | <span data-ttu-id="1038d-174">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-175">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-175">XPath</span></span> |<span data-ttu-id="1038d-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="1038d-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="1038d-177">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-177">Code</span></span> |<span data-ttu-id="1038d-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="1038d-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="1038d-179">Протокол конечной точки</span><span class="sxs-lookup"><span data-stu-id="1038d-179">Endpoint protocol</span></span>
<span data-ttu-id="1038d-180">Получает протокол конечной точки для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="1038d-181">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-181">Type</span></span> | <span data-ttu-id="1038d-182">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-183">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-183">XPath</span></span> |<span data-ttu-id="1038d-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="1038d-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="1038d-185">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-185">Code</span></span> |<span data-ttu-id="1038d-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="1038d-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="1038d-187">IP-адрес конечной точки</span><span class="sxs-lookup"><span data-stu-id="1038d-187">Endpoint IP</span></span>
<span data-ttu-id="1038d-188">Получает IP-адрес указанной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="1038d-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="1038d-189">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-189">Type</span></span> | <span data-ttu-id="1038d-190">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-191">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-191">XPath</span></span> |<span data-ttu-id="1038d-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="1038d-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="1038d-193">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-193">Code</span></span> |<span data-ttu-id="1038d-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="1038d-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="1038d-195">Порт конечной точки</span><span class="sxs-lookup"><span data-stu-id="1038d-195">Endpoint port</span></span>
<span data-ttu-id="1038d-196">Получает порт конечной точки для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1038d-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="1038d-197">Тип</span><span class="sxs-lookup"><span data-stu-id="1038d-197">Type</span></span> | <span data-ttu-id="1038d-198">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1038d-199">XPath</span><span class="sxs-lookup"><span data-stu-id="1038d-199">XPath</span></span> |<span data-ttu-id="1038d-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="1038d-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="1038d-201">Код</span><span class="sxs-lookup"><span data-stu-id="1038d-201">Code</span></span> |<span data-ttu-id="1038d-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="1038d-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="1038d-203">Пример</span><span class="sxs-lookup"><span data-stu-id="1038d-203">Example</span></span>
<span data-ttu-id="1038d-204">Ниже приведен пример рабочей роли, создающей задачу запуска с переменной среды `TestIsEmulated`, которой присваивается [значение XPath @emulated](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="1038d-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="1038d-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1038d-205">Next steps</span></span>
<span data-ttu-id="1038d-206">Узнайте больше о файле [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) .</span><span class="sxs-lookup"><span data-stu-id="1038d-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="1038d-207">Создайте пакет [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="1038d-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="1038d-208">Включите [удаленный рабочий стол](cloud-services-role-enable-remote-desktop.md) для роли.</span><span class="sxs-lookup"><span data-stu-id="1038d-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

