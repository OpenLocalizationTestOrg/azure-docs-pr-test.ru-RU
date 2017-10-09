---
title: "виртуальные машины aaaMigrate tooResource диспетчера с помощью Azure CLI | Документы Microsoft"
description: "Этой статье рассматриваются hello поддерживается платформой миграции ресурсов от классических tooAzure диспетчера ресурсов с помощью Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Перенос ресурсов IaaS в классическом tooAzure диспетчера ресурсов с помощью Azure CLI
Следующие шаги показывают, как toouse Azure командной строки (CLI) команды toomigrate инфраструктуры как услуги (IaaS) ресурсы из hello классической модели toohello диспетчера ресурсов Azure развертывания модели развертывания. статья Hello требует hello [Azure CLI](../../cli-install-nodejs.md).

> [!NOTE]
> Все операции hello, описанные здесь являются идемпотентными. Если имеются неполадки, отличные от неподдерживаемое свойство или ошибка конфигурации, рекомендуется повторить попытку hello подготовки, отмены или фиксации операции. Затем платформа Hello пытается hello действие еще раз.
> 
> 

<br>
Ниже приведен порядок hello tooidentify блок-схемы, в котором действия требуется toobe выполнен во время процесса миграции

![Снимок экрана, показывающий шагов миграции hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Шаг 1. Подготовка к переносу
Вот несколько рекомендаций, рекомендуется при оценке миграции IaaS ресурсов от классических tooResource диспетчера.

* Прочтите hello [списка неподдерживаемых конфигураций или функции](../windows/migration-classic-resource-manager-overview.md). При наличии виртуальных машин, использующих неподдерживаемые конфигурации или компоненты, рекомендуется отложить hello/конфигурация компонентов поддержки toobe было объявлено. Кроме того можно удалить эти компоненты или выйти из миграции tooenable этой конфигурации, если он соответствует вашим потребностям.
* Если у вас есть автоматизированные скрипты, которые сегодня развертывание инфраструктуры и приложений, попробуйте toocreate аналогичную программу установки теста с помощью этих скриптов для миграции. Кроме того можно настроить образец сред с помощью портала Azure hello.

> [!IMPORTANT]
> Шлюзы приложений для миграции с классической tooResource Manager в настоящее время не поддерживаются. Перед запуском сети hello toomove операции подготовки toomigrate классической виртуальной сети с шлюза приложения, удалить шлюз hello. После завершения миграции hello переподключение hello шлюза в диспетчере ресурсов Azure. 
>
>Шлюзов ExpressRoute подключение tooExpressRoute цепи в другую подписку невозможно перенести автоматически. В таких случаях удалить шлюз ExpressRoute hello, миграция виртуальной сети hello и повторного создания шлюза hello. См. в разделе [перенести ExpressRoute каналов и связанные виртуальные сети из модели развертывания диспетчера ресурсов hello классический toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) для получения дополнительной информации.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Шаг 2: Задайте подписку и регистрации поставщика hello
Для сценариев миграции tooset необходимо настроить среду для обоих классический и диспетчер ресурсов. [Установите интерфейс командной строки Azure](../../cli-install-nodejs.md) (Azure CLI) и [выберите подписку](../../xplat-cli-connect.md).

Учетная запись входа tooyour.

    azure login

Здравствуйте, выберите подписку Azure, используя следующую команду hello.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> Регистрация заключается в один раз шаги но нуждается toobe один раз, прежде чем миграции. Без регистрации вы увидите сообщение об ошибке после hello 
> 
> *Неправильный запрос: Подписка не зарегистрирована для миграции.* 
> 
> 

Зарегистрировать поставщик ресурсов hello миграции с помощью hello следующую команду. Обратите внимание, что в некоторых случаях время ожидания этой команды истекает. Тем не менее будет успешной регистрации hello.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Подождите пять минут для регистрации toofinish hello. Можно проверить состояние hello hello утверждения с помощью hello следующую команду. Убедитесь, что RegistrationState имеет значение `Registered` , прежде чем продолжить.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Теперь, переключитесь CLI toohello `asm` режим.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Шаг 3: Убедитесь, что недостаточно ядер виртуальная машина Azure Resource Manager hello Azure область текущего развертывания или виртуальной сети
Для этого шага необходимо tooswitch слишком`arm` режим. Для этого hello следующую команду.

```
azure config mode arm
```

Можно использовать следующие CLI команда toocheck hello текущее количество ядер, имеющегося в диспетчере ресурсов Azure hello. toolearn Дополнительные сведения об основных квоты, в разделе [ограничения и hello диспетчера ресурсов Azure](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

После завершения проверки того, этот шаг, можно переключиться обратно слишком`asm` режим.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Шаг 4. Вариант 1: миграция виртуальных машин в облачной службе
Получение списка hello облачные службы, используя следующую команду hello и подбору hello облачной службы, которые должны toomigrate. Обратите внимание, что если hello виртуальных машин в облачной службе hello в виртуальной сети или если они имеют рабочих и веб-роли, вы получите сообщение об ошибке.

    azure service list

Запустите следующую имя команды tooget hello развертывания для облачной службы hello из подробный вывод hello hello. В большинстве случаев hello имя развертывания является hello то же, что имя облачной службы hello.

    azure service show <serviceName> -vv

Во-первых проверки, при переносе hello облачной службы, с помощью hello, следующие команды:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Подготовка виртуальных машин hello в облачную службу hello для миграции. У вас есть два toochoose параметры из.

Toomigrate hello виртуальные машины tooa платформы созданную виртуальную сеть, используйте следующую команду hello.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Tooan toomigrate существующую виртуальную сеть в модели развертывания диспетчера ресурсов hello, используйте следующую команду hello.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

После подготовки hello операция завершилась успешно, можно просмотреть hello подробный вывод tooget hello состояние миграции hello виртуальные машины и убедитесь, что они находятся в hello `Prepared` состояния.

    azure vm show <vmName> -vv

Проверьте конфигурацию hello для hello подготовить ресурсы с помощью CLI или hello портал Azure. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.

    azure service deployment abort-migration <serviceName> <deploymentName>

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Шаг 4. Вариант 2: миграция виртуальных машин в виртуальной сети
Подбор hello виртуальной сети, которые должны toomigrate. Обратите внимание, что если виртуальная сеть hello содержит рабочих и веб-ролей или виртуальных машин с неподдерживаемых конфигураций, вы получите сообщение об ошибке проверки.

Получите все виртуальные сети hello в подписке hello, используя следующую команду hello.

    azure network vnet list

Hello результат будет выглядеть примерно следующим образом:

![Снимок экрана приветствия командной строки с выделенным именем hello всю виртуальную сеть.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

В приведенном выше примере hello, hello **virtualNetworkName** — полное имя hello **«Classicubuntu16 classicubuntu16 группы»**.

Во-первых проверки, при переносе hello виртуальной сети с помощью hello следующую команду:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Подготовьте hello виртуальной сети по своему усмотрению для миграции с помощью hello следующую команду.

    azure network vnet prepare-migration <virtualNetworkName>

Проверьте конфигурацию hello для hello подготовить виртуальные машины с помощью CLI или hello портал Azure. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.

    azure network vnet abort-migration <virtualNetworkName>

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Шаг 5. Перенос учетной записи хранения
После завершения переноса виртуальных машин hello, мы рекомендуем перенести hello учетной записи хранилища.

Подготовка учетной записи хранилища hello для миграции с помощью hello следующую команду

    azure storage account prepare-migration <storageAccountName>

Проверьте конфигурацию hello для hello подготовить учетную запись хранения с помощью CLI или hello портал Azure. Если вы не готовы к миграции и требуется toogo задней toohello старое состояние, используйте следующую команду hello.

    azure storage account abort-migration <storageAccountName>

Если хорошее hello подготовленного конфигурации, можно перемещаться вперед и зафиксировать hello ресурсы с помощью hello следующую команду.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Дальнейшие действия

* [Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Использовать ресурсы IaaS PowerShell toomigrate из классической tooAzure диспетчера ресурсов](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Средства сообщества соблюдения миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Распространенные ошибки миграции](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
