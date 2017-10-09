---
title: "aaaEndorsed дистрибутивов Linux | Документы Microsoft"
description: "Узнайте о рекомендованных дистрибутивах Linux в Azure, включая рекомендации по Ubuntu, CentOS, Oracle и SUSE."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Дистрибутивы Linux, рекомендованные для использования в Azure
Партнеры предоставляют образов Linux в Azure Marketplace hello. Мы сотрудничаем с различными tooadd сообщества Linux список одобренных распространения toohello еще больше разновидности. В hello между тем, для распределения, которые не доступны из hello Marketplace, вы можете всегда перевести собственные Linux, следуя правилам hello в [Создание и передача виртуального жесткого диска, который содержит операционную систему Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Поддерживаемые дистрибутивы и версии
Hello следующей таблице перечислены дистрибутивы Linux hello и версии, поддерживаемые в Azure. См. слишком[образы поддержка Linux в Microsoft Azure](https://support.microsoft.com/en-us/kb/2941892) более подробные сведения.

Службы интеграции Linux (LIS) драйверы Hello Hyper-V и Azure, модули ядра Microsoft непосредственно участвует toohello вышестоящего ядра Linux.  Некоторые драйверы LIS встроены ядра hello распространения по умолчанию. Более старые дистрибутивы на основе Red Hat Enterprise (RHEL) и CentOS можно отдельно скачать на странице [служб интеграции Linux (LIS) 4.1 для Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). В разделе [требования ядра Linux](create-upload-generic.md#linux-kernel-requirements) Дополнительные сведения о драйверах LIS hello.

Hello Azure Linux Agent уже предварительно установлен на hello Azure Marketplace образов и обычно находится из репозитория hello распространения пакета. Исходный код можно найти на сайте [GitHub](https://github.com/azure/walinuxagent).

| Дистрибутив | Version (версия) | Драйверы | Агент |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3: [загрузка LIS](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 и более поздних версий: в ядре |Пакет: в [репозитории](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) в разделе WALinuxAgent <br/>Исходный код: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0 + |В ядре |Исходный код: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9+, 8.2+ |В ядре |Пакет: в репозитории в разделе WAAgent  <br/>Исходный код: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |В ядре |Пакет: в репозитории в разделе WALinuxAgent  <br/>Исходный код: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux. |RHEL 6.7 или более поздней версии, 7.1 или более поздней версии |В ядре |Пакет: в репозитории в разделе WALinuxAgent  <br/>Исходный код: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES или SLES for SAP<br>11 SP4<br>12 SP1 или более поздняя версия|В ядре |Пакет:<p> для версии 11: в репозитории [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools);<br>для версии 12: входит в состав модуля Public Cloud в python-azure-agent.<br/>Исходный код: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |В ядре |Пакет: в репозитории [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) под именем python-azure-agent <br/>Исходный код: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |В ядре |Пакет: в репозитории в разделе WALinuxAgent  <br/>Исходный код: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>Партнеры

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

С веб-сайта CoreOS hello:

*Операционная система CoreOS обеспечивает безопасность, согласованность и надежность при работе. Вместо установки пакетов через yum или apt, CoreOS использует toomanage Linux контейнеры служб на более высоком уровне абстракции. Единый код службы и все зависимости упакованы в контейнер, который может выполняться на одном или нескольких компьютерах под управлением CoreOS.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ — это независимые консультаций и службе компании, специализирующейся на hello разработки и реализации профессиональных решений с помощью бесплатного программного обеспечения. Эксперты Credative получили международное признание многих использующих наши услуги ИТ-отделов как ведущие специалисты по открытому коду. Сейчас Credativ совместно с Майкрософт готовит соответствующие образы Debian для Debian 8 (Jessie) и версий, предшествующих Debian 7 (Wheezy). Оба изображения являются специальный toorun в Azure и можно легко управлять с помощью платформы hello. Credativ тоже будут поддерживать hello долгосрочного обслуживания и обновлении образов Debian hello Azure через центры поддержки источника его открыть.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle стратегией является toooffer целый ряд решений для общедоступных и частных облаков. Стратегия Hello дает пользователям возможность выбора и гибкость в том, как развертывать программное обеспечение Oracle в облаках Oracle и других облаков. Oracle в сотрудничестве с корпорацией Майкрософт позволяет клиентам toodeploy программное обеспечение Oracle в общедоступных и частных облаков Майкрософт уверенно hello сертификации и поддержки по сравнению с Oracle.  Заинтересованность компании Oracle и ее инвестиции в решения для общедоступных и частных облаков Oracle остаются неизменными.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Здравствуйте мире ведущим поставщиком решения с открытым кодом, Red Hat помогает более 90% из списка Fortune 500 решения бизнес-задач, выровняйте ИТ и бизнес-стратегий и подготовка для будущих hello технологии. Для этого Red Hat предлагает защищенные решения, используя открытую бизнес-модель и доступную, прогнозируемую модель подписки.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server в Azure — проверенная платформа, предоставляющая высокую степень надежности и безопасности для работы в облаке. Универсальный платформы Linux SUSE легко интегрируется с Azure облачной службы toodeliver легко управляемые облачной среде. С более чем 9,200 сертифицированным приложениям из более 1800 независимых поставщиков программного обеспечения для SUSE Linux Enterprise Server SUSE гарантирует, что нагрузок, поддерживаемых в центре обработки данных hello можно уверенно развернутое в Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Инженерно-техническое открытое сообщество Canonical способствует успешному распространению Ubuntu в клиентских, серверных и облачных средах, включая персональные облачные службы для потребителей. Концепция канонические в единой, свободного платформы в Ubuntu, из phone toocloud предоставляет семейство согласованного интерфейсы для hello телефон, планшет, ТВ и рабочего стола. Эту концепцию делает Ubuntu hello первый вариант для различных учреждений из производители toohello поставщиков общедоступных облачных бытовой электроники и Избранное между отдельными технологов.

С разработчиками и инженерных сосредоточено вокруг Здравствуй, мир канонические является уникальным образом позиционированные toopartner производители оборудования, toomarket решений Ubuntu toobring разработчики программного обеспечения для ПК, серверами и портативные устройства и поставщики содержимого.
