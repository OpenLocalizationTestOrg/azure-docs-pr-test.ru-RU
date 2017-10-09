---
title: "aaaCreate головной узел пакета HPC на виртуальной Машине Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure развертывания диспетчера ресурсов портала и hello модели toocreate Microsoft HPC Pack 2012 R2 головного узла на Виртуальной машине Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Создание hello головного узла кластера HPC Pack на ВМ Azure с помощью образа Marketplace
Используйте [образ виртуальной машины Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) из hello Azure Marketplace и hello Azure портала toocreate hello головного узла кластера HPC. Этот образ виртуальной машины пакета HPC основан на ОС Windows Server 2012 R2 Datacenter с предустановленным пакетом HPC 2012 R2 с обновлением 3. Используйте этот головной узел для экспериментального развертывания пакета HPC в Azure. Затем можно добавить вычислительных узлов toohello кластера toorun HPC рабочих нагрузок.

> [!TIP]
> toodeploy завершения кластера HPC Pack 2012 R2 в Azure, которая включает в себя hello головного узла и вычислительных узлов, рекомендуется использовать автоматизированную процедуру. Параметры включают в себя hello [скрипт развертывания IaaS пакета HPC](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) и шаблоны диспетчера ресурсов, таких как hello [кластера HPC Pack для рабочих нагрузок Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Шаблоны Resource Manager также доступны для [кластеров пакета Microsoft HPC 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Рекомендации относительно планирования
Как показано в следующий рисунок hello развертывании головного узла HPC Pack hello в домене Active Directory в виртуальной сети Azure.

![Головной узел пакета HPC][headnode]

* **Домен Active Directory**: hello HPC Pack 2012 R2 головной узел должен быть присоединен tooan домена Active Directory в Azure перед запуском служб HPC hello на hello виртуальной Машины. Как показано в этой статье для экспериментального развертывания, вы можете повысить уровень hello виртуальной Машине, созданной для головного узла hello как контроллер домена перед запуском служб HPC hello. Другой вариант — toodeploy контроллера домена в отдельном и леса в Azure toowhich объединении hello ВМ головного узла.

* **Модель развертывания**: в большинстве случаев новый, корпорация Майкрософт рекомендует использовать модель развертывания диспетчера ресурсов hello. В этой статье предполагается, что вы используете эту модель развертывания.

* **Виртуальная сеть Azure**: при использовании hello диспетчера ресурсов развертывания модели toodeploy hello головного узла, укажите, или создайте виртуальную сеть Azure. При необходимости toojoin hello головного узла tooan существующему домену Active Directory использовать hello виртуальной сети. Необходимо также его более поздней версии tooadd вычислительных узлов кластера toohello виртуальных машин.

## <a name="steps-toocreate-hello-head-node"></a>Действия toocreate hello головного узла
Ниже перечислены высокоуровневые действия toouse hello Azure портала toocreate ВМ для головного узла HPC Pack hello Azure с помощью модели развертывания диспетчера ресурсов hello. 

1. Если вы хотите toocreate нового леса Active Directory в Azure с контроллером домена отдельных виртуальных машин, один из вариантов — toouse [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Для простого экспериментального развертывания он имеет точный tooomit этот шаг и настройка головного узла hello самой ВМ как контроллер домена. Этот вариант описан далее в этой статье.
2. На hello [HPC Pack 2012 R2 на Windows Server 2012 R2 странице](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketplace, щелкните **создания виртуальной машины**. 
3. На hello hello портала **HPC Pack 2012 R2 на Windows Server 2012 R2** страницу, выберите hello **диспетчера ресурсов** модель развертывания, а затем нажмите кнопку **создать**.
   
    ![Образ пакета HPC][marketplace]
4. Используйте параметры hello портала tooconfigure hello и создайте hello виртуальной Машины. Если вы tooAzure новый, выполните действия из учебника hello [Создание виртуальной машины Windows в hello портал Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Для экспериментального развертывания можно обычно примите значение по умолчанию hello или рекомендуемые параметры.
   
   > [!NOTE]
   > Если вы хотите toojoin hello головного узла tooan существующего домена Active Directory в Azure, убедитесь, что при создании виртуальной Машины hello указывается hello виртуальной сети для этого домена.
   > 
   > 
5. После создания виртуальной Машины hello и hello Виртуальная машина запущена, [подключения toohello ВМ](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) с удаленного рабочего стола. 
6. Присоединение леса домена Active Directory tooan ВМ hello, выбрав один из следующих вариантов hello.
   
   * Если вы создали hello виртуальной Машины в виртуальной сети Azure с существующим лесом домена, присоедините леса toohello hello виртуальной Машины, используя стандартные средства диспетчера серверов или Windows PowerShell. Выполните перезапуск.
   * Если вы создали hello виртуальной Машины в новой виртуальной сети (без леса домена), затем преобразовывается hello виртуальной Машины контроллера домена. Используйте стандартные действия tooinstall и Настройка роли доменных служб Active Directory hello на головном узле hello. Подробные инструкции см. в разделе [Установка нового леса Active Directory в Windows Server 2012](https://technet.microsoft.com/library/jj574166.aspx).
7. После hello виртуальная машина запускается и не присоединены к домену tooan леса Active Directory запустите службы HPC Pack hello следующим образом:
   
    а. Подключение toohello головного узла виртуальной Машины, используя учетную запись домена, которая является членом локальной группы администраторов hello. Например используйте учетную запись администратора hello, настроенной при создании ВМ головного узла hello.
   
    b. Для настройки головного узла по умолчанию запустите Windows PowerShell с правами администратора и введите hello ниже:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Он может занять несколько минут для toostart служб HPC Pack hello.
   
    Для вывода сведений о дополнительных параметрах конфигурации головного узла введите `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Дальнейшие действия
* Теперь можно работать с головным узлом кластера HPC Pack hello. Например, запустите диспетчер кластеров HPC, а полный hello [списку задач развертывания](https://technet.microsoft.com/library/jj884141.aspx).
* Tooincrease hello кластера вычислений емкости по требованию, добавить [узлы повышения Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) в облачной службе. 
* Запустите тестовую рабочую нагрузку на кластере hello. Пример см. в разделе hello HPC Pack [руководство по началу работы](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
