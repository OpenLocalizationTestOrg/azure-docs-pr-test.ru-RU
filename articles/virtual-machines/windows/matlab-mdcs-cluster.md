---
title: "aaaMATLAB кластеров на виртуальных машинах | Документы Microsoft"
description: "Использование виртуальных машин Microsoft Azure toocreate toorun кластеры MATLAB Distributed Computing Server MATLAB рабочих нагрузок параллельных вычислений"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Создание кластеров MATLAB Distributed Computing Server на виртуальных машинах Azure
Используйте Microsoft Azure виртуальных машин toocreate один или несколько MATLAB Distributed Computing Server кластеры toorun MATLAB рабочих нагрузок параллельных вычислений. Установите программное обеспечение MATLAB Distributed Computing Server на toouse виртуальной Машины в качестве базового образа и использовать быстрый запуск Azure шаблона или сценария Azure PowerShell (на [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy hello кластеру и управлять им. После развертывания подключаться toorun кластера toohello рабочих нагрузок.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>О MATLAB и MATLAB Distributed Computing Server
Hello [MATLAB](http://www.mathworks.com/products/matlab/) платформы оптимизирован для решения проблем проектирования и научных исследований. Пользователи MATLAB крупномасштабных моделирования и задач обработки данных могут использовать параллельных MathWorks, вычислений toospeed продуктов вверх их рабочих нагрузок с большим объемом вычислений, используя преимущества вычислительных кластеров и службы сетки. [Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) позволяет пользователям MATLAB параллелизировать приложения и задействовать преимущества многоядерных процессоров, графических процессоров и вычислительных кластеров. [MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) позволяет пользователям tooutilize MATLAB много компьютеров в кластере вычислений.

С помощью виртуальных машин Azure, можно создавать кластеры MATLAB Distributed Computing Server, у которых имеются hello же параллельной работы механизмов toosubmit доступны как на локальных кластерах, например интерактивного задания, выполнение пакетных заданий, независимых задач и связи задачи. Использование Azure вместе с платформой MATLAB hello имеет множество преимуществ по сравнению tooprovisioning и с помощью традиционных локальных оборудования: размер диапазона виртуальной машины, создание кластеров по запросу, вы платите только за вычислительные ресурсы hello используется, и Hello модели tootest возможности масштабирования.  

## <a name="prerequisites"></a>Предварительные требования
* **Клиентский компьютер** -вам потребуется toocommunicate компьютер клиента на основе Windows Azure и hello MATLAB Distributed Computing Server кластера после развертывания.
* **Azure PowerShell** -разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) tooinstall его на клиентском компьютере.
* **Подписка Azure** — если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/free/) . Для больших кластеров можно использовать подписку с оплатой по мере использования или другие варианты приобретения.
* **Квота ядер** -core квоты tooincrease hello toodeploy может потребоваться большой кластер или более чем одном кластере MATLAB Distributed Computing Server. квоты tooincrease [откройте запрос поддержки сети клиента](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) бесплатно.
* **Лицензии MATLAB, элементов параллельных вычислений и MATLAB Distributed Computing Server** -скрипты hello предполагается, что hello [диспетчера лицензий размещенных MathWorks](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) используется для всех лицензий.  
* **Программное обеспечение MATLAB Distributed Computing Server** -будет установлен на виртуальной Машине, которая будет использоваться как базовый образ виртуальной Машины hello для hello кластера виртуальных машин.

## <a name="high-level-steps"></a>Шаги высокого уровня
toouse виртуальные машины Azure для вашей кластеров MATLAB Distributed Computing Server hello требуются следующие общие этапы. Подробные инструкции приведены в hello документации шаблоном краткого руководства hello и скрипты на [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Создание базового образа виртуальной машины**  

   * Загрузите и установите программное обеспечение MATLAB Distributed Computing Server на эту виртуальную машину.

     > [!NOTE]
     > Этот процесс может занять несколько часов, но имеется только toodo его после использования для каждой версии MATLAB.   
     >
     >
2. **Создание одного или нескольких кластеров**  

   * Использовать сценарий PowerShell предоставленный hello или hello примеры использования шаблона toocreate кластер из базового образа виртуальной Машины hello.   
   * Управление кластерами hello, с помощью сценария PowerShell указано hello, позволяющий toolist, приостановки, возобновления и удаления кластеров.

## <a name="cluster-configurations"></a>Конфигурации кластеров
В настоящее время скрипт создания кластера hello и шаблона позволяет toocreate топологии с одной MATLAB Distributed Computing Server. При необходимости можно создать один или несколько дополнительных кластеров; при этом в каждом кластере может быть разное число рабочих виртуальных машин, различные размеры виртуальных машин и т. д.

### <a name="matlab-client-and-cluster-in-azure"></a>Клиент и кластер MATLAB в Azure
рис. узел клиента MATLAB Hello, планировщик заданий MATLAB узел и MATLAB Distributed Computing Server узлы настраиваются как виртуальные машины Azure в виртуальной сети, как показано в следующих hello «рабочих».


* toouse hello кластер, подключите узлом toohello клиента удаленного рабочего стола. узел клиента Hello запуск hello MATLAB клиента.
* узел клиента Hello имеет общую папку, доступную всех рабочих процессов.
* Диспетчер лицензий размещенных MathWorks используется для проверки лицензии hello для всех программ, например MATLAB.
* По умолчанию в рабочем процессе hello виртуальных машин создается один рабочий процесс MATLAB Distributed Computing Server на ядро, но можно указать любое число.

## <a name="use-an-azure-based-cluster"></a>Использование кластера на базе Azure
Как и другие типы кластеров MATLAB Distributed Computing Server необходимо hello toouse профиль диспетчера кластеров в hello MATLAB клиента (на клиенте hello ВМ) toocreate профиль кластера MATLAB планировщик заданий.

![Диспетчер профилей кластеров](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Дальнейшие действия
* Для toodeploy подробные инструкции и позволяющая управлять кластерами MATLAB Distributed Computing Server в Azure см. в разделе hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) репозиторий, содержащий шаблоны hello и сценариев.
* Go toohello [MathWorks сайта](http://www.mathworks.com/) подробную документацию для MATLAB и MATLAB Distributed Computing Server.
