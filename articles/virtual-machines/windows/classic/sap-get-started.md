---
title: "aaaUsing SAP на виртуальных машинах | Документы Microsoft"
description: "Узнайте об использовании SAP на виртуальных машинах Windows в Microsoft Azure."
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Использование SAP на виртуальных машинах Windows в Azure
Облачные вычисления — это широко используемый термин, который приобретает все большее значение в пределах hello ИТ-индустрии, от малых компаний вверх toolarge транснациональных корпораций. Microsoft Azure — hello платформа облачных служб Майкрософт, которая предлагает широкий спектр новых возможностей. Теперь заказчики могут toorapidly подготовки и Отмена подготовки приложений как облачных служб, так, чтобы они не только tootechnical или бюджетные ограничения. Вместо того чтобы тратить время и бюджет на аппаратную инфраструктуру, компании могут сосредоточить внимание на приложения hello, бизнес-процессов и его преимущества для клиентов и пользователей.

Корпорация Майкрософт предоставляет виртуальные машины Microsoft Azure как комплексную платформу "инфраструктура как услуга" (IaaS). Виртуальные машины Azure (IaaS) поддерживают приложения на основе SAP NetWeaver. технические документы Hello ниже описывают, как tooplan и реализуйте SAP NetWeaver приложения, основанные на виртуальных машинах Windows Azure. Приложения на основе SAP NetWeaver можно также реализовать в [виртуальных машинах Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver в Azure — высокая доступность
Заголовок: aaaSAP NetWeaver в Azure — SAP ASCS/SCS экземпляров службы кластеризации с помощью отказоустойчивого кластера Windows Server в Azure с помощью sios DataKeeper

Сводка: "в этом документе описывается способ tooset SIOS DataKeeper toouse высокодоступной конфигурации SAP ASCS/SCS в Azure. SAP защищает компоненты, являющиеся единой точкой отказа, например SAP ASCS/SCS или службы Enqueue Replication Services, с помощью конфигураций отказоустойчивых кластеров Windows Server, для которых используются общие диски. Эти компоненты SAP важны для hello функциональных возможностей системы SAP. Таким образом toobe помещены в функции высокой доступности требуется разместить toomake убедиться, что эти компоненты можно сохранять работоспособность при сбое сервера или виртуальной Машины как в конфигурациях кластера Windows для ОС и среды Hyper-V. Начиная с августа 2015 г. Azure сама по себе не поддерживает высокодоступных конфигураций, необходимых для важных компонентов SAP на основе общих дисков, которые требуются для hello Windows. Однако с помощью hello hello продукта DataKeeper от компании SIOS, можно построить конфигурации отказоустойчивого кластера Windows Server, при необходимости для SAP ASCS/SCS на платформе Azure IaaS hello. Этот документ описывает подход к пошаговое как tooinstall конфигурации отказоустойчивого кластера Windows Server с общим диском, предоставляемым SIOS Datakeeper в Azure. Hello приводятся детальные сведения о конфигурации на стороне Azure, Windows и SAP hello, который работает оптимальным образом конфигурации высокого уровня доступности hello. Hello документ дополняет hello документацию по установке SAP и примечаниях SAP, которые представляют Привет основные ресурсы для установки и развертывания программного обеспечения SAP в заданный платформы.

Последнее обновление: август 2015 г.

[Загрузить руководство](http://go.microsoft.com/fwlink/?LinkId=613056)

