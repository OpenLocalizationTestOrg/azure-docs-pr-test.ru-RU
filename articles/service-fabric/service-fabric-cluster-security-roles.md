---
title: "Защита кластера Service Fabric: роли клиента | Документация Майкрософт"
description: "Эта статья описывает два клиентских ролей hello и hello разрешения, предоставленные роли toohello."
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
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Контроль доступа на основе ролей для клиентов Service Fabric
Azure Service Fabric поддерживает два типа элемента управления различный уровень доступа для клиентов, подключенных tooa кластера Service Fabric: администратора и пользователя. Контроль доступа позволяет hello кластера администратора toolimit доступа toocertain кластера операции для разных групп пользователей, повышение безопасности кластера hello.  

**Администраторы** возможности toomanagement полный доступ (включая возможности чтения и записи). По умолчанию **пользователей** достаточно возможности toomanagement доступ для чтения (например, возможности работы с запросами), hello возможность tooresolve приложений и служб.

Укажите hello двух ролей клиента (администратора и клиента) во время создания кластера hello, предоставляя отдельных сертификатов. Сведения о настройке защищенного кластера Service Fabric см. в статье [Защита кластера Service Fabric](service-fabric-cluster-security.md).

## <a name="default-access-control-settings"></a>Параметры контроля доступа по умолчанию
типом управления доступом Hello администратора имеет полный доступ tooall hello FabricClient API-интерфейсы. Он может выполнять все операции чтения и записи на кластер Service Fabric hello, включая hello следующие операции:

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
* **ReportUpgradeHealth**: возобновление обновления приложения с текущего хода обновления hello                             
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
* **ReportFabricUpgradeHealth**: возобновление обновления кластера с текущего хода обновления hello                             
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
* **FileContent**: изображения передача файлов клиента хранилища (внешние toocluster)                             
* **FileDownload**: образа загрузки файла запуска (внешние toocluster) для хранилища клиента                             
* **InternalList**: операция вывода списка клиентских файлов хранилища образов (внутренняя).                             
* **Delete**: операция удаления клиента хранилища образов.                              
* **Upload**: операция передачи клиента хранилища образов.                             
* **NodeControl**: запуск, остановка и перезапуск узлов.                             
* **MoveReplicaControl**: переход с одного узла tooanother реплик                             

### <a name="miscellaneous-operations"></a>Прочие операции
* **Ping**: проверка связи клиента.                             
* **Query**: разрешены все запросы.
* **NameExists**: проверки существования универсальных кодов ресурса (URI) именования.                             

по умолчанию, типом управления доступом пользователя Hello является ограниченной toohello следующие операции: 

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

контроль доступа администратора Hello также имеет доступ toohello предыдущих операций.

## <a name="changing-default-settings-for-client-roles"></a>Изменение параметров по умолчанию для ролей клиента
В файле манифеста кластера hello чтобы обеспечить toohello возможности администрирования клиента при необходимости. Можно изменить значения по умолчанию hello, перейдя toohello **настройки структуры** во время [создание кластера](service-fabric-cluster-creation-via-portal.md)и предоставление hello предшествует параметры в hello **имя**, **администратора**, **пользователя**, и **значение** поля.

## <a name="next-steps"></a>Дальнейшие действия
[Защита кластера Service Fabric](service-fabric-cluster-security.md)

[Настройка кластера Service Fabric на портале Azure](service-fabric-cluster-creation-via-portal.md)

