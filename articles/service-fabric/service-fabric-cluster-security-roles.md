---
title: "Защита кластера Service Fabric: роли клиента | Документация Майкрософт"
description: "В данной статье описываются две роли клиента и разрешения, предоставленные этим ролям."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 85935e60bba4b27972282700e2e9c9a22b403bdb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Контроль доступа на основе ролей для клиентов Service Fabric
Платформа Azure Service Fabric поддерживает два разных типа контроля доступа для клиентов, подключенных к кластеру Service Fabric: администраторский и пользовательский. Благодаря контролю доступа администратор кластера может ограничить доступ разных групп пользователей на выполнение определенных операций в кластере, повысив тем самым уровень безопасности кластера.  

**Администраторы** имеют полный доступ к возможностям управления (включая возможности чтения и записи). По умолчанию **пользователи** имеют доступ только на чтение к функциям управления (например, при работе с запросами) и возможность разрешения приложений и служб.

Во время создания кластера задаются две клиентские роли (администратора или клиента) путем предоставления отдельных сертификатов для каждой из них. Сведения о настройке защищенного кластера Service Fabric см. в статье [Защита кластера Service Fabric](service-fabric-cluster-security.md).

## <a name="default-access-control-settings"></a>Параметры контроля доступа по умолчанию
Тип контроля доступа администратора предусматривает полный доступ ко всем API-интерфейсам FabricClient. Вы можете выполнять любые операции чтения и записи в кластере Service Fabric, включая следующие.

### <a name="application-and-service-operations"></a>Операции с приложением и службой
* **CreateService**: создание службы.                             
* **CreateServiceFromTemplate**: создание службы из шаблона.                             
* **UpdateService**: обновления службы.                             
* **DeleteService**: удаление службы.                             
* **ProvisionApplicationType**: подготовка типа приложения.                             
* **CreateApplication**: создание приложения.                               
* **DeleteApplication**: удаление приложения.                             
* **UpgradeApplication**: запуск или прерывание обновлений приложения.                             
* **UnprovisionApplicationType**: отмена подготовки типа приложения.                             
* **MoveNextUpgradeDomain**: возобновление обновлений приложения с помощью явно указанного домена обновления.                             
* **ReportUpgradeHealth**: возобновление обновлений приложения с помощью текущего процесса обновления.                             
* **ReportHealth**: сообщение о работоспособности.                             
* **PredeployPackageToNode**: API предварительного развертывания.                            
* **CodePackageControl**: перезапуск пакетов кода.                             
* **RecoverPartition**: восстановление секции.                             
* **RecoverPartitions**: восстановление секций.                             
* **RecoverServicePartitions**: восстановление секций службы.                             
* **RecoverSystemPartitions**: восстановление секций системной службы.                             

### <a name="cluster-operations"></a>Операции с кластером
* **ProvisionFabric**: подготовка MSI и (или) манифеста кластера.                             
* **UpgradeFabric**: запуск обновлений кластера.                             
* **UnprovisionFabric**: отмена подготовки MSI и (или) манифеста кластера.                         
* **MoveNextFabricUpgradeDomain**: возобновление обновлений кластера с помощью явно указанного домена обновления.                             
* **ReportFabricUpgradeHealth**: возобновление обновлений кластера с помощью текущего процесса обновления.                             
* **StartInfrastructureTask**: запуск задач инфраструктуры.                             
* **FinishInfrastructureTask**: завершение задач инфраструктуры.                             
* **InvokeInfrastructureCommand**: команды управления задачами инфраструктуры.                              
* **ActivateNode**: активация узла.                             
* **DeactivateNode**: деактивация узла.                             
* **DeactivateNodesBatch**: деактивация нескольких узлов.                             
* **RemoveNodeDeactivations**: отмена деактивации нескольких узлов.                             
* **GetNodeDeactivationStatus**: проверка состояния деактивации.                             
* **NodeStateRemoved**: сообщение об удалении узла.                             
* **ReportFault**: сообщение об ошибке.                             
* **FileContent**: передача клиентского файла хранилища образов (вне кластера).                             
* **FileDownload**: инициация скачивания клиентского файла хранилища образов (вне кластера).                             
* **InternalList**: операция вывода списка клиентских файлов хранилища образов (внутренняя).                             
* **Delete**: операция удаления клиента хранилища образов.                              
* **Upload**: операция передачи клиента хранилища образов.                             
* **NodeControl**: запуск, остановка и перезапуск узлов.                             
* **MoveReplicaControl**: перемещение реплик с одного узла на другой.                             

### <a name="miscellaneous-operations"></a>Прочие операции
* **Ping**: проверка связи клиента.                             
* **Query**: разрешены все запросы.
* **NameExists**: проверки существования универсальных кодов ресурса (URI) именования.                             

Тип контроля доступа от имени пользователя по умолчанию ограничивается следующими операциями. 

* **EnumerateSubnames**: перечисление универсального кода ресурса (URI) именования.                             
* **EnumerateProperties**: перечисления свойств именования.                             
* **PropertyReadBatch**: операции чтения свойств именования.                             
* **GetServiceDescription**: уведомления о службах с длительным временем опроса и чтение описаний служб.                             
* **ResolveService**: разрешение служб на основе жалоб.                             
* **ResolveNameOwner**: разрешение владельца универсального кода ресурса (URI) именования.                             
* **ResolvePartition**: разрешение системных служб.                             
* **ServiceNotifications**: уведомления служб на основе событий.                             
* **GetUpgradeStatus**: опрос состояния обновления приложения.                             
* **GetFabricUpgradeStatus**: опрос состояния обновления кластера.                             
* **InvokeInfrastructureQuery**: запрос задач инфраструктуры.                             
* **List**: операция вывода списка клиентских файлов хранилища образов.                             
* **ResetPartitionLoad**: сброс нагрузки для единицы отработки отказа.                             
* **ToggleVerboseServicePlacementHealthReporting**: включение и выключение подробных отчетов о работоспособности размещения службы.                             

Контроль доступа от имени администратора также предусматривает доступ к приведенным выше операциям.

## <a name="changing-default-settings-for-client-roles"></a>Изменение параметров по умолчанию для ролей клиента
При необходимости в файле манифеста кластера клиенту можно предоставить возможность администрирования. Чтобы изменить значения по умолчанию, во время [создания кластера](service-fabric-cluster-creation-via-portal.md) перейдите к настройкам **Fabric Settings** (Параметры структуры), а затем укажите параметры, приведенные выше, в полях **Имя**, **Администратор**, **Пользователь** и **Значение**.

## <a name="next-steps"></a>Дальнейшие действия
[Защита кластера Service Fabric](service-fabric-cluster-security.md)

[Настройка кластера Service Fabric на портале Azure](service-fabric-cluster-creation-via-portal.md)

