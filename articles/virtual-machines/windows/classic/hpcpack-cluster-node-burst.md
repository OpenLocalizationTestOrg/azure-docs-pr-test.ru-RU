---
title: "aaaAdd повышение узлы tooan HPC Pack кластера | Документы Microsoft"
description: "Узнайте, как кластер tooexpand HPC Pack в Azure по запросу путем добавления экземпляров рабочей роли, запускаемые в облачной службе"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>Добавить кластер по требованию «повышение» узлы tooan пакета HPC в Azure
Если вы настроили [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) кластера в Azure, может потребоваться возможность емкость кластера масштабирования hello tooquickly вверх или вниз, не поддерживая набор предварительно настроенных ВМ вычислительных узлов. В этой статье рассказывается, как tooadd по требованию узлов «повышения» (экземпляры рабочей роли в облачной службе) как вычислительных ресурсов tooa головного узла в Azure. 

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

![Расширительные узлы][burst]

в этой статье инструкциям Hello помогают быстро добавить узлы Azure tooa облачного головной узел пакета HPC виртуальной Машины для теста или подтверждение концепции развертывания. перечислены основные действия Hello hello же, как действия hello слишком «повышение tooAzure» tooadd облачных вычислений емкость tooan локального пакета HPC кластера. Руководство см. в разделе [Установка гибридного вычислительного кластера с помощью пакета Microsoft HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Подробные инструкции и рекомендации для рабочих развертываний см. в разделе [прорыв tooAzure с пакетом Microsoft HPC](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Предварительные требования
* **Головной узел пакета HPC развернут на виртуальной машине Azure**. Можно использовать изолированную или входящую в состав большого кластера виртуальную машину головного узла. toocreate автономного головного узла в разделе [развертывания головного узла HPC Pack на ВМ Azure](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Автоматических параметры развертывания кластера HPC Pack см. в разделе [параметры toocreate и управлять кластером Windows HPC в Azure с пакетом Microsoft HPC](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Если вы используете hello [скрипт развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md) toocreate hello кластер в Azure, можно включить узлы повышения Azure в автоматического развертывания. Примеры hello в этой статье.
  > 
  > 
* **Подписка Azure** -tooadd Azure узлов, можно выбрать hello ту же подписку, которая использовалась toodeploy hello ВМ головного узла, или другую подписку (или подписок).
* **Квота ядер** -может потребоваться tooincrease hello квоту ядер, особенно в том случае, если выбрано несколько узлов Azure с несколькими ядрами размеры toodeploy. квоты tooincrease [откройте запрос поддержки сети клиента](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) бесплатно.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Шаг 1: Создание облачной службы и учетной записи хранения для hello узлов Azure
Используйте классический портал Azure hello или эквивалентными средствами tooconfigure hello следующие ресурсы, необходимые toodeploy узлов Azure:

* Новая облачная служба Azure
* Новая учетная запись хранения Azure

> [!NOTE]
> Не используйте повторно уже существующую облачную службу в подписке. 
> 
> 

**Рекомендации**

* Настройте отдельную облачную службу для каждого шаблона узла Azure, что планирование toocreate. Тем не менее, можно использовать одну учетную запись хранилища для нескольких шаблонов узлов hello.
* Рекомендуется размещать hello облачной службы и учетной записи хранилища hello для развертывания hello в hello же регионе Azure.

## <a name="step-2-configure-an-azure-management-certificate"></a>Шаг 2. Настройка сертификата управления Azure
tooadd Azure узлов как вычислительных ресурсов, требуется сертификат управления на головном узле hello и передачи соответствующего сертификата toohello подписку Azure, используемую для развертывания hello.

В этом сценарии можно выбирать hello **по умолчанию сертификат управления HPC Azure** , пакет HPC устанавливается и настраивается автоматически, на головном узле. Этот сертификат удобен для тестирования и экспериментальных развертываний. toouse это сертификат, загрузите файл C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer из головного узла hello toothe подписки виртуальной Машины. сертификат tooupload hello в hello [классический портал Azure](https://manage.windowsazure.com), нажмите кнопку **параметры** > **сертификаты управления**.

Сертификат управления hello tooconfigure Дополнительные параметры, в разделе [сценариев tooConfigure hello сертификата управления Azure для развертываний повышения в Azure](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Шаг 3: Развертывание кластера toohello узлов Azure
Здравствуйте, tooadd действия и запустите Azure узлов в этом сценарии обычно являются hello таким же как шаги hello и локального головного узла. Дополнительные сведения см. в разделе hello в следующих разделах в [действия tooDeploy узлов Azure с пакетом Microsoft HPC](https://technet.microsoft.com/library/gg481758.aspx):

* Создание шаблона узла Azure
* Добавление узлов Azure кластер Windows HPC toohello
* Запуск (Подготовка) узлов Azure hello

После добавления и запуска узлов hello они готовы toouse toorun кластерных заданий.

Если при развертывании узлов Azure возникли проблемы, ознакомьтесь со статьей [Устранение неполадок развертываний узлов Azure с помощью пакета Microsoft HPC](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* toouse размер экземпляр большим объемом вычислений для hello прорыв узлов см. в разделе вопросы hello в [высокопроизводительных вычислений размеры виртуальных Машин](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Если вы хотите автоматического увеличения или сжатия hello Azure вычислительные ресурсы в соответствии с рабочей нагрузки кластера hello см. в разделе [автоматическое увеличение и уменьшение вычислительных ресурсов Azure в кластере HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png
