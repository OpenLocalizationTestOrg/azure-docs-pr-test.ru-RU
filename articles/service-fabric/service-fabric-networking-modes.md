---
title: "aaaConfigure сетевых режимов для служб Azure Service Fabric контейнеров | Документы Microsoft"
description: "Узнайте, как toosetup hello различные сетевые режимы, Azure Service Fabric поддерживает."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="7f128-103">Сетевые режимы контейнеров Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f128-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="7f128-104">Hello сетевой режим по умолчанию предлагаемые hello Service Fabric кластера для контейнера служб — hello `nat` сетевой режим.</span><span class="sxs-lookup"><span data-stu-id="7f128-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="7f128-105">С hello `nat` режиме, имеющих более одного ожидающего toohello службы контейнеров к сети же порт результаты в ошибки развертывания.</span><span class="sxs-lookup"><span data-stu-id="7f128-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="7f128-106">Для запуска нескольких служб, прослушивающие этот же порт, Service Fabric поддерживает hello hello `open` сетевой режим (версии 5.7 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="7f128-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="7f128-107">С hello `open` сети режиме, каждый контейнер службы получает динамически назначаемых IP-адресов, внутренне, позволяя toohello toolisten несколько служб одного порта.</span><span class="sxs-lookup"><span data-stu-id="7f128-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="7f128-108">Таким образом, с типом одной службы со статическим конечной точке, заданной в манифест службы hello новые службы могут быть созданы и удален без ошибок при развертывании с помощью hello `open` сетевой режим.</span><span class="sxs-lookup"><span data-stu-id="7f128-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="7f128-109">Аналогичным образом можно использовать таким же hello `docker-compose.yml` файл сопоставлений статических портов для создания нескольких служб.</span><span class="sxs-lookup"><span data-stu-id="7f128-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="7f128-110">С помощью службы toodiscover IP, динамически назначаемый hello не рекомендуется с момента изменения IP-адреса hello при hello служба перезапускается или перемещает tooanother узла.</span><span class="sxs-lookup"><span data-stu-id="7f128-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="7f128-111">Использовать только hello **служба именования Service Fabric** или hello **служба DNS** для обнаружения службы.</span><span class="sxs-lookup"><span data-stu-id="7f128-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="7f128-112">Для каждой виртуальной сети в Azure допускается максимум 4096 IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="7f128-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="7f128-113">Таким образом, сумма hello hello числом узлов и hello количество экземпляров службы контейнера (с `open` сети) не может превышать 4096 в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7f128-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="7f128-114">Для таких сценариев высокой плотности, hello `nat` рекомендуется сетевой режим.</span><span class="sxs-lookup"><span data-stu-id="7f128-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="7f128-115">Настройка режима сети open</span><span class="sxs-lookup"><span data-stu-id="7f128-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="7f128-116">Настройка шаблона Azure Resource Manager hello путем включения службы DNS и hello поставщика IP-адресов в разделе `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="7f128-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="7f128-117">Настройте несколько IP-адресов, настроенных на каждом узле кластера hello toobe раздел tooallow hello сетевой профиль.</span><span class="sxs-lookup"><span data-stu-id="7f128-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="7f128-118">Hello следующий пример настраивает пять IP-адресов для каждого узла (таким образом может быть пять экземпляров службы, прослушиваемого порта toohello на каждом узле) для кластера Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7f128-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="7f128-119">Для кластеров Linux дополнительный открытый IP-адрес добавляется tooallow исходящие подключения.</span><span class="sxs-lookup"><span data-stu-id="7f128-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="7f128-120">Hello следующий фрагмент устанавливает пять IP-адресов для каждого узла для кластеров Linux:</span><span class="sxs-lookup"><span data-stu-id="7f128-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="7f128-121">Для Windows, кластеры, настроенных NSG правило, открывая порт UDP/53 для hello виртуальной сети с hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="7f128-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="7f128-122">Приоритет</span><span class="sxs-lookup"><span data-stu-id="7f128-122">Priority</span></span> |    <span data-ttu-id="7f128-123">Имя</span><span class="sxs-lookup"><span data-stu-id="7f128-123">Name</span></span>    |    <span data-ttu-id="7f128-124">Источник</span><span class="sxs-lookup"><span data-stu-id="7f128-124">Source</span></span>      |  <span data-ttu-id="7f128-125">Место назначения</span><span class="sxs-lookup"><span data-stu-id="7f128-125">Destination</span></span>   |   <span data-ttu-id="7f128-126">служба</span><span class="sxs-lookup"><span data-stu-id="7f128-126">Service</span></span>    | <span data-ttu-id="7f128-127">Действие</span><span class="sxs-lookup"><span data-stu-id="7f128-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="7f128-128">2000</span><span class="sxs-lookup"><span data-stu-id="7f128-128">2000</span></span> | <span data-ttu-id="7f128-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="7f128-129">Custom_Dns</span></span> | <span data-ttu-id="7f128-130">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7f128-130">VirtualNetwork</span></span> | <span data-ttu-id="7f128-131">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7f128-131">VirtualNetwork</span></span> | <span data-ttu-id="7f128-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="7f128-132">DNS (UDP/53)</span></span> | <span data-ttu-id="7f128-133">РАЗРЕШИТЬ</span><span class="sxs-lookup"><span data-stu-id="7f128-133">Allow</span></span>  |


4. <span data-ttu-id="7f128-134">Укажите сетевой режим hello в манифесте приложения hello для каждой службы `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="7f128-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="7f128-135">режим Hello `open` приводит к службе hello начало выделенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7f128-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="7f128-136">Если режим не указан, то по умолчанию toohello основные `nat` режим.</span><span class="sxs-lookup"><span data-stu-id="7f128-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="7f128-137">Таким образом, в следующий манифеста пример hello `NodeContainerServicePackage1` и `NodeContainerServicePackage2` можно каждого toohello прослушивания одного порта (прослушивают обе службы `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="7f128-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="7f128-138">Вы можете комбинировать и сопоставлять разные сетевые режимы для использования со службами в рамках приложения для кластера Windows.</span><span class="sxs-lookup"><span data-stu-id="7f128-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="7f128-139">Таким образом, некоторые службы будут работать в режиме `open`, а некоторые — в режиме `nat`.</span><span class="sxs-lookup"><span data-stu-id="7f128-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="7f128-140">Если служба настроена с `nat`, это toomust прослушивающего порт hello быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="7f128-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="7f128-141">Использование разных сетевых режимов для разных служб не поддерживается в кластерах Linux.</span><span class="sxs-lookup"><span data-stu-id="7f128-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7f128-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f128-142">Next steps</span></span>
<span data-ttu-id="7f128-143">Из этой статьи вы узнали о сетевых режимах, поддерживаемых Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7f128-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="7f128-144">Модель приложений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f128-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="7f128-145">Ресурсы манифеста службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7f128-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="7f128-146">Развертывание tooService контейнера Windows Fabric на Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f128-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="7f128-147">Развертывание tooService контейнера Docker структуры в Linux</span><span class="sxs-lookup"><span data-stu-id="7f128-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
