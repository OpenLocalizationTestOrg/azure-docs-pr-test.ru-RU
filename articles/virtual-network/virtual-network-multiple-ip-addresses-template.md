---
title: "aaaMultiple IP-адресов для виртуальных машин Azure - шаблона | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальной машины с помощью шаблона диспетчера ресурсов Azure."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Назначение нескольких IP-адресов toovirtual машины с помощью шаблона диспетчера ресурсов Azure

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью развертывания диспетчера ресурсов Azure hello модели с помощью шаблона диспетчера ресурсов. Несколько общедоступных и частных IP-адресов нельзя назначить toohello одного сетевого Адаптера при развертывании ВМ с помощью hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Описание шаблона

Развертывание шаблона позволяет tooquickly и постоянно создать ресурсы Azure со значениями другой конфигурации. Чтение hello [Пошаговое руководство диспетчера ресурсов шаблона](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статью, если вы не знакомы с использованием шаблонов диспетчера ресурсов Azure. Hello [развертывание виртуальной Машины с несколькими IP-адресами](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) шаблон используется в этой статье.

<a name="resources"></a>Развертывание шаблона hello создает hello следующие ресурсы:

|Ресурс|Имя|Описание|
|---|---|---|
|Сетевой интерфейс|*myNic1*|Hello три IP-конфигурации, описанной в разделе сценарии hello в этой статье создания и назначения toothis сетевого адаптера.|
|Ресурс общедоступного IP-адреса|Создаются два имени: *myPublicIP* и *myPublicIP2*|Эти ресурсы назначаются статические общедоступные IP-адреса и назначаются toohello *IPConfig 1* и *IPConfig 2* IP-конфигурации, описанной в сценарии hello.|
|ВМ|*myVM1*|Виртуальная машина Standard DS3.|
|Виртуальная сеть|*myVNet1*|Виртуальная сеть с одной подсетью с именем *mySubnet*.|
|Учетная запись хранения|Уникальный toohello развертывания|Учетная запись хранения.|

<a name="parameters"></a>При развертывании шаблона hello, необходимо указать значения для hello следующие параметры:

|Имя|Описание|
|---|---|
|adminUsername|Имя пользователя администратора. должно соответствовать имени пользователя Hello [требования Azure имени пользователя](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Пароль hello пароль администратора должен соответствовать [требования к паролю Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|DNS-имя для PublicIPAddressName1. Hello DNS-имя разрешается tooone hello открытый IP-адресов, назначенных toohello виртуальной Машины. Hello имя должно быть уникальным в пределах hello Azure регионом (расположением) создается hello виртуальной Машины в.|
|dnsLabelPrefix1|DNS-имя для PublicIPAddressName2. Hello DNS-имя разрешается tooone hello открытый IP-адресов, назначенных toohello виртуальной Машины. Hello имя должно быть уникальным в пределах hello Azure регионом (расположением) создается hello виртуальной Машины в.|
|OSVersion|версия Windows и Linux Hello hello виртуальной Машины. Hello операционной системы — это полностью исправленную образ hello заданной выбранной версии Windows и Linux.|
|imagePublisher|Hello издателя образа Windows и Linux для hello выбранной виртуальной Машины.|
|imageOffer|изображение приветствия Windows и Linux для hello выбранной виртуальной Машины.|

Для каждого из ресурсов hello, предоставляемым hello шаблона следует настроить несколько параметров по умолчанию. Можно просмотреть эти параметры, одним из следующих методов hello:

- **Просмотр шаблона hello на GitHub:** Если вы знакомы с использованием шаблонов, можно просмотреть параметры hello в hello [шаблона](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Просмотр параметров hello после развертывания:** Если вы не знакомы с использованием шаблонов, можно развернуть шаблон hello, используя действия в одной из следующих разделах hello и просмотрите параметры hello после развертывания.

Можно использовать hello портал Azure, PowerShell или hello Azure командной строки (CLI) toodeploy hello шаблона. Все методы производят hello того же результата. шаблон toodeploy hello, hello завершения действия в одном из следующих разделах hello.

## <a name="deploy-using-hello-azure-portal"></a>Развертывание с помощью портала Azure hello

шаблон toodeploy hello, используя hello портал Azure завершения hello следующие шаги:

1. Измените шаблон hello, если требуется. шаблон Hello развертывает hello ресурсы и параметры, перечисленные в hello [ресурсов](#resources) этой статьи. Дополнительные сведения о шаблонах toolearn и как tooauthor их, прочитайте hello [шаблоны разработки Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)статьи.
2. Развертывание hello шаблона с одним из следующих методов hello:
    - **Шаблон SELECT hello в портале hello:** hello завершения шагов в hello [развертывания ресурсов на основе пользовательского шаблона](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) статьи. Выберите существующий шаблон hello с именем *101-vm несколько ipconfig*.
    - **Напрямую:** щелкните следующий шаблон hello tooopen кнопки непосредственно на портале hello hello:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Независимо от метода hello выбран, вам потребуется toosupply значения для hello [параметры](#parameters) описанных ранее в этой статье. После развертывания виртуальной Машины hello подключения toohello ВМ и добавление hello частного IP адресов toohello операционной системы развертывания, выполнив hello шагов в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

## <a name="deploy-using-powershell"></a>Развертывание с помощью PowerShell

шаблон hello toodeploy с помощью PowerShell, полные hello, следующие шаги:

1. Развертывание шаблона hello, выполнив шаги hello в hello [развертывания шаблона с помощью PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) статьи. Hello статье описывается несколько вариантов развертывания шаблона. Если выбрать с помощью hello toodeploy `-TemplateUri parameter`, hello URI для этого шаблона является *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Если выбрать с помощью hello toodeploy `-TemplateFile` параметра, скопируйте содержимое hello hello [файл шаблона](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) из GitHub в новый файл на компьютере. Измените содержимое шаблона hello, если требуется. шаблон Hello развертывает hello ресурсы и параметры, перечисленные в hello [ресурсов](#resources) этой статьи. Дополнительные сведения о шаблонах toolearn и как tooauthor их, прочитайте hello [шаблоны разработки Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)статьи.

    Независимо от того, hello выбранного варианта toodeploy hello шаблон с необходимо указать значения для hello значения параметров, перечисленных в hello [параметры](#parameters) этой статьи. При выборе параметров toosupply, с помощью файла параметров, скопируйте содержимое hello hello [файл параметров](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) из GitHub в новый файл на компьютере. Измените значения hello в файле hello. Используйте файл hello, созданный в качестве значения hello hello `-TemplateParameterFile` параметра.

    toodetermine допустимые значения для hello OSVersion, ImagePublisher и imageOffer параметров, hello завершения шагов в hello [перейдите и выберите статью образов виртуальной Машины Windows](../virtual-machines/windows/cli-ps-findimage.md) статьи.

    >[!TIP]
    >Если вы не уверены, доступен ли dnslabelprefix, введите hello `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind команду out. Если это возможно, команда hello вернет `True`.

2. После развертывания виртуальной Машины hello подключения toohello ВМ и добавление hello частного IP адресов toohello операционной системы развертывания, выполнив hello шагов в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

## <a name="deploy-using-hello-azure-cli"></a>Развертывание с помощью hello Azure CLI

toodeploy hello шаблона с использованием hello Azure CLI 1.0 завершения hello, следующие шаги:

1. Развертывание шаблона hello, выполнив шаги hello в hello [развертывания шаблона с hello Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) статьи. Hello статье описывается несколько вариантов развертывания шаблона hello. Если выбрать с помощью hello toodeploy `--template-uri` (-f), hello URI для этого шаблона является *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Если выбрать с помощью hello toodeploy `--template-file` (-f) параметра, скопируйте содержимое hello hello [файл шаблона](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) из GitHub в новый файл на компьютере. Измените содержимое шаблона hello, если требуется. шаблон Hello развертывает hello ресурсы и параметры, перечисленные в hello [ресурсов](#resources) этой статьи. Дополнительные сведения о шаблонах toolearn и как tooauthor их, прочитайте hello [шаблоны разработки Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)статьи.

    Независимо от того, hello выбранного варианта toodeploy hello шаблон с необходимо указать значения для hello значения параметров, перечисленных в hello [параметры](#parameters) этой статьи. При выборе параметров toosupply, с помощью файла параметров, скопируйте содержимое hello hello [файл параметров](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) из GitHub в новый файл на компьютере. Измените значения hello в файле hello. Используйте файл hello, созданный в качестве значения hello hello `--parameters-file` (-e) параметра.

    toodetermine допустимые значения для hello OSVersion, ImagePublisher и imageOffer параметров, hello завершения шагов в hello [перейдите и выберите статью образов виртуальной Машины Windows](../virtual-machines/windows/cli-ps-findimage.md) статьи.

2. После развертывания виртуальной Машины hello подключения toohello ВМ и добавление hello частного IP адресов toohello операционной системы развертывания, выполнив hello шагов в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
