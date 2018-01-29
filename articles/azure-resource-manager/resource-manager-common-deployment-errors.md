---
title: "Устранение распространенных ошибок развертывания в Azure | Документация Майкрософт"
description: "Описывается устранение распространенных ошибок при развертывании ресурсов в Azure с помощью Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "ошибка развертывания, развертывание Azure, развернуть в Azure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2017
ms.author: tomfitz
ms.openlocfilehash: ca7e3cb541948e6cc0b8d077616f3611e3ab2477
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/20/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Устранение распространенных ошибок развертывания в Azure с помощью Azure Resource Manager | Microsoft Azure

В этой статье описаны некоторые распространенные ошибки при развертывании в Azure и предоставлены сведения об их устранении. Если не удается найти код ошибки развертывания, см. раздел [Поиск кода ошибки](#find-error-code).

## <a name="error-codes"></a>Коды ошибок

| Код ошибки | Устранение | Дополнительные сведения |
| ---------- | ---------- | ---------------- |
| AccountNameInvalid | Следуйте ограничениям для имен учетных записей хранения. | [Устранение ошибок, связанных с именами учетных записей хранения](resource-manager-storage-account-name-errors.md) |
| AccountPropertyCannotBeSet | Проверьте доступные свойства учетной записи хранения. | [Справочник по шаблонам Microsoft.Storage/storageAccounts](/azure/templates/microsoft.storage/storageaccounts) |
| AllocationFailed | Кластер или регион не имеют доступных ресурсов или не поддерживают запрашиваемый размер виртуальной машины. Повторите запрос позже или укажите другой размер виртуальной машины. | Проблемы подготовки и распределения для [Linux](../virtual-machines/linux/troubleshoot-deployment-new-vm.md) и [Windows](../virtual-machines/windows/troubleshoot-deployment-new-vm.md) |
| AnotherOperationInProgress | Дождитесь завершения параллельной операции. | |
| AuthorizationFailed | Учетная запись или субъект-служба не имеют необходимых прав доступа для выполнения развертывания. Проверьте роль, к которой принадлежит учетная запись, и ее права доступа к области развертывания. | [Управление доступом на основе ролей в Azure](../active-directory/role-based-access-control-configure.md) |
| BadRequest | Отправленные значения развертывания не соответствуют значениям, ожидаемым Resource Manager. Проверьте внутреннее сообщение о состоянии. Оно поможет вам в устранении неполадки. | [Справочник по шаблону](/azure/templates/) и [поддерживаемые расположения](resource-manager-templates-resources.md#location) |
| Конфликт | Запрашиваемая операция не разрешена в текущем состоянии ресурса. Например, изменение размера диска разрешено только при создании или освобождении виртуальной машины. | |
| DeploymentActive | Дождитесь завершения параллельного развертывания в эту группу ресурсов. | |
| DnsRecordInUse | Имя записи DNS должно быть уникальным. Предоставьте другое имя или измените имеющуюся запись. | |
| ImageNotFound | Проверьте параметры образа виртуальной машины. |  |
| InUseSubnetCannotBeDeleted | Эта ошибка возникает, когда вы пытаетесь обновить ресурс, но при обработке запроса удаляется и создается ресурс. Укажите все неизменяемые значения. | [Обновление ресурса](/azure/architecture/building-blocks/extending-templates/update-resource) |
| InvalidAuthenticationTokenTenant | Получите маркер доступа для соответствующего клиента. Маркер можно получить только из клиента, которому принадлежит учетная запись. | |
| InvalidContentLink | скорее всего была предпринята попытка связать недоступный вложенный шаблон. Внимательно проверьте URI, указанный для вложенного шаблона. Если шаблон существует в учетной записи хранения, убедитесь, что URI доступен. Возможно, понадобится передать маркер SAS. | [Связанные шаблоны](resource-group-linked-templates.md) |
| InvalidParameter | Одно из значений, предоставленных для ресурса, не соответствует ожидаемому значению. Эта ошибка может возникнуть в результате многих различных состояний. Например, пароля может быть недостаточно или имя большого двоичного объекта может быть неверным. Проверьте сообщение об ошибке, чтобы определить, какое значение необходимо исправить. | |
| InvalidRequestContent | Среди значений развертывания есть неожидаемые значения либо обязательные значения отсутствуют. Проверьте значения для типа ресурса. | [Справочник по шаблонам](/azure/templates/) |
| InvalidRequestFormat | Включите ведение журнала отладки при выполнении развертывания и проверьте содержимое запроса. | [Ведение журнала отладки](resource-manager-troubleshoot-tips.md#enable-debug-logging) |
| InvalidResourceNamespace | Проверьте пространство имен ресурсов, заданное в свойстве **type**. | [Справочник по шаблонам](/azure/templates/) |
| InvalidResourceReference | Ресурс не существует, или на него неверно ссылаются. Проверьте, следует ли добавить зависимость. Убедитесь, что для функции **reference** указаны параметры, необходимые для вашего сценария. | [Устранение ошибок, связанных с зависимостями](resource-manager-not-found-errors.md) |
| InvalidResourceType | Проверьте тип ресурсов, заданный в свойстве **type**. | [Справочник по шаблонам](/azure/templates/) |
| InvalidTemplate | Проверьте синтаксис шаблона на наличие ошибок. | [Устранение ошибок, связанных с недопустимым шаблоном](resource-manager-invalid-template-errors.md) |
| LinkedAuthorizationFailed | Проверьте, принадлежит ли учетная запись к тому же клиенту, что и группа ресурсов, в которую выполняется развертывание. | |
| LinkedInvalidPropertyId | Идентификатор ресурса не удается разрешить правильно. Убедитесь, что указаны все обязательные значения для идентификатора ресурса, включая идентификатор подписки, имя группы ресурсов, тип ресурса, имя родительского ресурса (если необходимо) и имя ресурса. | |
| LocationRequired | Укажите расположение ресурса. | [Определение расположения](resource-manager-templates-resources.md#location) |
| MissingRegistrationForLocation | Проверьте состояние регистрации поставщика ресурсов и поддерживаемые расположения. | [Устранение ошибок регистрации](resource-manager-register-provider-errors.md) |
| MissingSubscriptionRegistration | Зарегистрируйте подписку в поставщике ресурсов. | [Устранение ошибок регистрации](resource-manager-register-provider-errors.md) |
| NoRegisteredProviderFound | Проверьте состояние регистрации поставщика ресурсов. | [Устранение ошибок регистрации](resource-manager-register-provider-errors.md) |
| NotFound | Возможно, вы пытаетесь развернуть зависимый ресурс параллельно с родительским ресурсом. Проверьте, не нужно ли добавить зависимость. | [Устранение ошибок, связанных с зависимостями](resource-manager-not-found-errors.md) |
| OperationNotAllowed | Развертывание пытается выполнить операцию, которая превышает квоту для подписки, группы ресурсов или региона. Если это возможно, измените развертывание, чтобы не превышать квоты. В противном случае запросите изменение квот. | [Устранение ошибок квот ресурсов](resource-manager-quota-errors.md) |
| ParentResourceNotFound | Убедитесь, что имеется родительский ресурс, прежде чем создавать дочерние ресурсы. | [Устранение ошибок, связанных с родительскими ресурсами](resource-manager-parent-resource-errors.md) |
| PrivateIPAddressInReservedRange | Указанный IP-адрес включает диапазон адресов, необходимый Azure. Измените IP-адрес, чтобы не использовать зарезервированный диапазон. | [IP-адреса](../virtual-network/virtual-network-ip-addresses-overview-arm.md) |
| PrivateIPAddressNotInSubnet | Указанный IP-адрес находится вне диапазона подсети. Измените IP-адрес, чтобы он находился в пределах диапазона подсети. | [IP-адреса](../virtual-network/virtual-network-ip-addresses-overview-arm.md) |
| PropertyChangeNotAllowed | Некоторые свойства нельзя изменить в развернутом ресурсе. При обновлении ресурса измените только допустимые свойства. | [Обновление ресурса](/azure/architecture/building-blocks/extending-templates/update-resource) |
| RequestDisallowedByPolicy | Подписка включает в себя политику ресурсов, предотвращающую действие, которое вы пытаетесь выполнить во время развертывания. Найдите политику, которая блокирует действие. Измените развертывание в соответствии с ограничениями политики, если это возможно. | [Устранение ошибок с политиками](resource-manager-policy-requestdisallowedbypolicy-error.md) |
| ReservedResourceName | Укажите ресурс, имя которого не включает в себя зарезервированное имя. | [Зарезервированные имена ресурсов](resource-manager-reserved-resource-name.md) |
| ResourceGroupBeingDeleted | Дождитесь завершения удаления. | |
| ResourceGroupNotFound | Проверьте имя целевой группы ресурсов для развертывания. Оно уже должно существовать в подписке. Проверьте контекст подписки. | [Azure CLI](/cli/azure/account?#az_account_set), [PowerShell](/powershell/module/azurerm.profile/set-azurermcontext) |
| ResourceNotFound | Развертывание ссылается на ресурс, который не может быть разрешен. Убедитесь, что для функции **reference** указаны параметры, необходимые для вашего сценария. | [Устранение ошибок с поиском ресурсов](resource-manager-not-found-errors.md) |
| ResourceQuotaExceeded | Развертывание пытается создать ресурсы, которые превышают квоту для подписки, группы ресурсов или региона. Если возможно, измените инфраструктуру, чтобы не превышать квоты. В противном случае запросите изменение квот. | [Устранение ошибок квот ресурсов](resource-manager-quota-errors.md) |
| SkuNotAvailable | Выберите SKU (например, размер виртуальной машины), который доступен в выбранном расположении. | [Устранение ошибок, связанных с недоступностью номера SKU](resource-manager-sku-not-available-errors.md) |
| StorageAccountAlreadyExists | Предоставьте уникальное имя учетной записи хранения. | [Устранение ошибок, связанных с именами учетных записей хранения](resource-manager-storage-account-name-errors.md)  |
| StorageAccountAlreadyTaken | Предоставьте уникальное имя учетной записи хранения. | [Устранение ошибок, связанных с именами учетных записей хранения](resource-manager-storage-account-name-errors.md) |
| StorageAccountNotFound | Проверьте подписку, группу ресурсов и имя учетной записи хранения, которую вы хотите использовать. | |
| SubnetsNotInSameVnet | Виртуальная машина может иметь только одну виртуальную сеть. При развертывании нескольких сетевых адаптеров убедитесь, что они принадлежат той же виртуальной сети. | [Использование нескольких сетевых адаптеров](../virtual-machines/windows/multiple-nics.md) |

## <a name="find-error-code"></a>Поиск кода ошибки

Если во время развертывания возникает ошибка, Resource Manager возвращает код ошибки. Сообщение об ошибке можно просмотреть на портале, в PowerShell или Azure CLI. Внешнее сообщение об ошибке может быть слишком общим для устранения неполадок. Подробные сведения об ошибке приведены во внутреннем сообщении. Дополнительные сведения см. в разделе [Определение кода ошибки](resource-manager-troubleshoot-tips.md#determine-error-code).

## <a name="next-steps"></a>Дальнейшие действия
* Сведения о действиях аудита см. в статье [Операции аудита с помощью Resource Manager](resource-group-audit.md).
* Дополнительные сведения об определении ошибок во время развертывания см. в статье [Просмотр операций развертывания с помощью портала Azure](resource-manager-deployment-operations.md).
