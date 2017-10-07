---
title: "aaaInstall Trend Micro Deep Security на виртуальной Машине | Документы Microsoft"
description: "В этой статье описывается как tooinstall и настройка Trend Micro безопасности на виртуальной Машине, созданные hello классической модели развертывания в Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Как tooinstall и настройка Trend Micro Deep Security в качестве службы на виртуальной Машине Windows
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В этой статье показано, как tooinstall и настройка Trend Micro Deep Security как службы на новой или существующей виртуальной машины (VM) под управлением Windows Server. Deep Security как услуга включает защиту от вредоносных программ, брандмауэр, систему предотвращения вторжений и мониторинг целостности.

Клиент Hello устанавливается как расширение безопасности через hello агент виртуальной Машины. На новой виртуальной машины установите hello Deep Security Agent, как hello агент виртуальной Машины автоматически создается по hello портал Azure.

Существующей виртуальной Машины, созданные с помощью классического портала hello, hello Azure CLI или PowerShell могут не иметь агент виртуальной Машины. Для существующей виртуальной машины, у которого нет hello агент виртуальной Машины требуется toodownload и сначала установить. В данной статье рассматриваются обе ситуации.

При наличии действующей подписки из Trend Micro локального решения, его можно использовать toohelp защиты виртуальных машин Azure. Если у вас еще нет подписки, можно зарегистрироваться для получения пробной подписки. Дополнительные сведения об этом решении см. в разделе блога hello Trend Micro [Microsoft Azure VM агент расширения для Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Установите hello Deep Security Agent на новой виртуальной Машины

Hello [портал Azure](http://portal.azure.com) позволяет устанавливать расширения безопасности Trend Micro hello при использовании образа с hello **Marketplace** toocreate hello виртуальной машины. При создании одной виртуальной машины с помощью портала hello является легко tooadd защиту Trend Micro.

С помощью записи из hello **Marketplace** открывает мастер, который помогает настроить hello виртуальную машину. Использовать hello **параметры** колонки, третья панель hello приветствия мастера tooinstall hello Trend Micro модуль безопасности.  Общие инструкции см. в разделе [создать виртуальную машину под управлением Windows в hello портал Azure](tutorial.md).

При получении toohello **параметры** колонке мастера hello hello следующие действия:

1. Нажмите кнопку **расширения**, нажмите кнопку **добавить расширение** в следующую область hello.

   ![Приступите к добавлению расширения hello][1]

2. Выберите **Deep Security Agent** в hello **новый ресурс** области. В области hello Deep Security Agent щелкните **создать**.

   ![Поиск агента Deep Security][2]

3. Введите hello **идентификатор клиента** и **пароль активации клиента** для расширения hello. При необходимости можно ввести значение **Security Policy Identifier** (Идентификатор политики безопасности). Нажмите кнопку **ОК** tooadd hello клиента.

   ![Ввод данных расширения][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Установите hello Deep Security Agent на существующей виртуальной Машины
агент hello tooinstall на существующей виртуальной Машине, необходимо hello следующих элементов:

* модуль Azure PowerShell Hello, версии 0.8.2 или более новую, установленных на локальном компьютере. Можно проверить версию hello Azure PowerShell, установленный с помощью hello **Get-Module azure | format-table версии** команды. Инструкции и ссылки toohello последнюю версию, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Вход с использованием подписки Azure tooyour `Add-AzureAccount`.
* Hello hello целевой виртуальной машине установлен агент виртуальной Машины.

Сначала проверьте, что приветствия уже установлен агент виртуальной Машины. Заполните hello имя облачной службы и имя виртуальной машины, а затем запустите следующие команды в командной строке Azure PowerShell администраторские hello. Замените все содержимое в кавычках hello, включая hello < и > символов.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Если вы не знаете hello облачной службы и имя виртуальной машины, выполните **Get-AzureVM** toodisplay hello, сведения для всех виртуальных машин в вашей текущей подписки.

Если hello **write-host** возвращает **True**, hello установлен агент виртуальной Машины. Если он возвращает **False**, см. инструкции hello и toohello ссылку загрузить в Azure в блоге hello [агент ВМ и расширения — часть 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Если установлен hello агент виртуальной Машины, выполните следующие команды.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Дальнейшие действия
Он занимает несколько минут для hello агента toostart выполняется при его установке. После этого вам требуется tooactivate Deep Security на виртуальной машине hello, им можно управлять с глубокой диспетчер безопасности. См. следующие статьи для получения дополнительных инструкций hello.

* статья Trend об этом решении, [Мгновенное включение облачной защиты для Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* Объект [пример сценария Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello виртуальной машины
* [Инструкции](http://go.microsoft.com/fwlink/?LinkId=404099) для образца hello

## <a name="additional-resources"></a>Дополнительные ресурсы
[Как toolog на tooa виртуальной машине под управлением Windows Server]

[Расширения и компоненты виртуальных машин Azure]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Как toolog на tooa виртуальной машине под управлением Windows Server]:connect-logon.md
[Расширения и компоненты виртуальных машин Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
