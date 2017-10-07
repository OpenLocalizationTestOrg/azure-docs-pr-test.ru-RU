---
title: "Краткое руководство для развертывания пакета средств разработки стека aaaAzure | Документы Microsoft"
description: "Узнайте, как toodeploy hello пакет средств разработки стек Azure"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 7f9fcd3a620e2916a24e57990d93dc9ace2b1129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-deployment-quickstart"></a>Краткое руководство по развертыванию набора разработки Azure Stack

Hello [пакет средств разработки Azure стека](azure-stack-poc.md) — среда тестирования и разработки, можно развернуть tooevaluate и демонстрируют возможности стека Azure и служб. tooget его и запущены, будет нужно tooprepare hello среды оборудования и выполнять некоторые сценарии (это займет несколько часов). После этого можно вход toohello администратора и клиента toomanage порталов Azure стека и тестирования предложений. 

1. [**Планирование оборудования, программного обеспечения и сети**](azure-stack-deploy.md). Hello компьютера, на котором размещен пакет средств разработки hello (узел комплект средств для разработки hello) должен соответствовать оборудования, программного обеспечения и требования к сети. Кроме того, необходимо выбрать с помощью служб федерации Active Directory или Azure Active Directory. Быть toocomply убедиться, что эти условия перед началом развертывания, чтобы процесс установки hello работу. 

2. [**Загрузите и извлеките пакет развертывания hello**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit). Вы можете загрузить пакет узел разработки toohello hello развертывания пакета или tooa другой компьютер. Hello извлеченные файлы занимают 60 ГБ свободного места на диске, поэтому с помощью другого компьютера может помочь снизить требования к оборудованию hello hello development kit узла развертывания.

3. [**Подготовка узла комплект средств для разработки hello** ](azure-stack-run-powershell-script.md#prepare-the-development-kit-host) с помощью установщика hello. После выполнения этого шага узел комплект средств для разработки hello загрузится toohello Cloudbuilder.vhdx (виртуальный жесткий диск содержит загрузочную операционную систему и hello Azure стека установки файлов).

4. [**Развертывание пакета средств разработки hello** ](azure-stack-run-powershell-script.md#deploy-the-development-kit) на узле комплект средств для разработки hello.

5. Если развертывание стека Azure использует Azure Active Directory, необходимо [Azure стеком регистров с помощью Azure](azure-stack-register.md) , чтобы пользователь мог [загрузки элементов Azure marketplace](azure-stack-download-azure-marketplace-item.md) tooAzure стека.

После выполнения этих действий вы получите комплект среды разработки с администратора и клиента порталов. Далее можно [Подключитесь и выполните вход](azure-stack-connect-azure-stack.md) toohello портала. Можно приступать к развертыванию поставщиков ресурсов, создание [предлагает](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions), и заполнение hello Azure стека [marketplace](azure-stack-marketplace.md).
