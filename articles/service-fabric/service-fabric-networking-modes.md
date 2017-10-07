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
# <a name="service-fabric-container-networking-modes"></a>Сетевые режимы контейнеров Service Fabric

Hello сетевой режим по умолчанию предлагаемые hello Service Fabric кластера для контейнера служб — hello `nat` сетевой режим. С hello `nat` режиме, имеющих более одного ожидающего toohello службы контейнеров к сети же порт результаты в ошибки развертывания. Для запуска нескольких служб, прослушивающие этот же порт, Service Fabric поддерживает hello hello `open` сетевой режим (версии 5.7 или более поздней версии). С hello `open` сети режиме, каждый контейнер службы получает динамически назначаемых IP-адресов, внутренне, позволяя toohello toolisten несколько служб одного порта.   

Таким образом, с типом одной службы со статическим конечной точке, заданной в манифест службы hello новые службы могут быть созданы и удален без ошибок при развертывании с помощью hello `open` сетевой режим. Аналогичным образом можно использовать таким же hello `docker-compose.yml` файл сопоставлений статических портов для создания нескольких служб.

С помощью службы toodiscover IP, динамически назначаемый hello не рекомендуется с момента изменения IP-адреса hello при hello служба перезапускается или перемещает tooanother узла. Использовать только hello **служба именования Service Fabric** или hello **служба DNS** для обнаружения службы. 


> [!WARNING]
> Для каждой виртуальной сети в Azure допускается максимум 4096 IP-адресов. Таким образом, сумма hello hello числом узлов и hello количество экземпляров службы контейнера (с `open` сети) не может превышать 4096 в виртуальной сети. Для таких сценариев высокой плотности, hello `nat` рекомендуется сетевой режим.
>

## <a name="setting-up-open-networking-mode"></a>Настройка режима сети open

1. Настройка шаблона Azure Resource Manager hello путем включения службы DNS и hello поставщика IP-адресов в разделе `fabricSettings`. 

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

2. Настройте несколько IP-адресов, настроенных на каждом узле кластера hello toobe раздел tooallow hello сетевой профиль. Hello следующий пример настраивает пять IP-адресов для каждого узла (таким образом может быть пять экземпляров службы, прослушиваемого порта toohello на каждом узле) для кластера Windows Service Fabric.

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

    Для кластеров Linux дополнительный открытый IP-адрес добавляется tooallow исходящие подключения. Hello следующий фрагмент устанавливает пять IP-адресов для каждого узла для кластеров Linux:

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

3. Для Windows, кластеры, настроенных NSG правило, открывая порт UDP/53 для hello виртуальной сети с hello следующие значения:

   | Приоритет |    Имя    |    Источник      |  Место назначения   |   служба    | Действие |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | Виртуальная сеть | Виртуальная сеть | DNS (UDP/53) | РАЗРЕШИТЬ  |


4. Укажите сетевой режим hello в манифесте приложения hello для каждой службы `<NetworkConfig NetworkType="open">`.  режим Hello `open` приводит к службе hello начало выделенный IP-адрес. Если режим не указан, то по умолчанию toohello основные `nat` режим. Таким образом, в следующий манифеста пример hello `NodeContainerServicePackage1` и `NodeContainerServicePackage2` можно каждого toohello прослушивания одного порта (прослушивают обе службы `Endpoint1`).

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
Вы можете комбинировать и сопоставлять разные сетевые режимы для использования со службами в рамках приложения для кластера Windows. Таким образом, некоторые службы будут работать в режиме `open`, а некоторые — в режиме `nat`. Если служба настроена с `nat`, это toomust прослушивающего порт hello быть уникальными. Использование разных сетевых режимов для разных служб не поддерживается в кластерах Linux. 


## <a name="next-steps"></a>Дальнейшие действия
Из этой статьи вы узнали о сетевых режимах, поддерживаемых Service Fabric.  

* [Модель приложений Service Fabric](service-fabric-application-model.md)
* [Ресурсы манифеста службы Service Fabric](service-fabric-application-model.md)
* [Развертывание tooService контейнера Windows Fabric на Windows Server 2016](service-fabric-get-started-containers.md)
* [Развертывание tooService контейнера Docker структуры в Linux](service-fabric-get-started-containers-linux.md)
