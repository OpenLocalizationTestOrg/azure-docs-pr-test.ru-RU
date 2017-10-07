---
title: "aaaCreate ферм серверов SharePoint в Azure | Документы Microsoft"
description: "Быстро создаете новую ферму SharePoint 2013 или SharePoint 2016 в Azure с помощью hello Azure marketplace портала."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Создание фермы серверов SharePoint с помощью hello Azure marketplace портала

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Фермы SharePoint 2013
С помощью Microsoft Azure marketplace hello портала можно быстро создать предварительно настроенного фермы SharePoint Server 2013. Такой подход может сэкономить много времени, когда в среде разработки и тестирования нужна базовая или высокодоступная ферма SharePoint или когда SharePoint Server 2013 рассматривается в качестве решения для совместной работы в рамках организации.

> [!NOTE]
> Hello **фермы серверов SharePoint** был удален элемент hello Azure Marketplace hello портал Azure. Он был заменен hello **фермы SharePoint 2013 не - HA** и **высокой ДОСТУПНОСТИ фермы SharePoint 2013** элементов.
>
>

Hello основные ферма SharePoint состоит из трех виртуальных машин в этой конфигурации.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Ферму такой конфигурации можно использовать в качестве упрощенной установки для разработки приложений SharePoint или первоначальной оценки SharePoint 2013.

toocreate hello основные () SharePoint фермы с тремя серверами:

1. Щелкните [здесь](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Щелкните **Развернуть**.
3. На hello **фермы SharePoint 2013 не - HA** области, нажмите кнопку **создать**.
4. Укажите параметры на шаги hello hello **создать ферму SharePoint 2013 не - высокой НАДЕЖНОСТИ** , а затем щелкните **создать**.

ферма SharePoint Hello высокого уровня доступности состоит из девяти виртуальные машины в этой конфигурации.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Это более высокие нагрузки клиента фермы конфигурации tootest, высокий уровень доступности hello внешний сайт SharePoint и группы доступности AlwaysOn SQL Server можно использовать для фермы SharePoint. Кроме того, такая конфигурация подходит для разработки приложений SharePoint в высокодоступной среде.

toocreate hello высокого уровня доступности (9) SharePoint фермы с серверами:

1. Щелкните [здесь](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Щелкните **Развернуть**.
3. На hello **высокой ДОСТУПНОСТИ фермы SharePoint 2013** области, нажмите кнопку **создать**.
4. Укажите параметры на hello семь шагов hello **создания фермы SharePoint 2013 HA** , а затем щелкните **создать**.

> [!NOTE]
> Не удается создать hello **фермы SharePoint 2013 не - HA** или **высокой ДОСТУПНОСТИ фермы SharePoint 2013** с бесплатной пробной версии Azure.
>
>

Hello портал Azure создает оба эти фермы в виртуальной сети только для облака с веб-приложения с выходом в Интернет. Имеется не сеть сеть VPN или ExpressRoute подключения задней tooyour организации сетей.

> [!NOTE]
> При создании hello основные или фермах SharePoint высокого уровня доступности с помощью hello портал Azure, нельзя указать существующую группу ресурсов. toowork обойти это ограничение, создайте эти ферм с помощью Azure PowerShell. Дополнительные сведения см. в разделе [Создание ферм разработки и тестирования SharePoint 2013 с помощью Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Фермы SharePoint 2016
В разделе [в этой статье](https://technet.microsoft.com/library/mt723354.aspx) hello инструкции toobuild hello после одного сервера SharePoint Server 2016 фермы.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Управление фермами hello
Администрирование серверов hello этих ферм через подключения удаленного рабочего стола. Дополнительные сведения см. в разделе [входа на виртуальную машину toohello](quick-create-portal.md#connect-to-virtual-machine).

С сайта центра администрирования SharePoint hello можно настроить узлы, приложения SharePoint и другие функциональные возможности. Дополнительные сведения см. в статье [Настройка SharePoint 2013](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с дополнительными [конфигурациями SharePoint](https://technet.microsoft.com/library/dn635309.aspx) в службах инфраструктуры Azure.
