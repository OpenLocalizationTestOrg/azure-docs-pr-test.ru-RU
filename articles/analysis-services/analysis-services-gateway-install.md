---
title: "шлюз данных в локальной aaaInstall | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте локальный шлюз данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Установка и настройка локального шлюза данных
Локальный шлюз данных является обязательным, если один или несколько серверов Azure Analysis Services в hello же региона подключения tooon локальные источники данных. toolearn Дополнительные сведения о шлюзе hello. в разделе [локального шлюза данных](analysis-services-gateway.md).

## <a name="prerequisites"></a>Предварительные требования
**Минимальные требования:**

* .NET Framework 4.5;
* 64-разрядная версия Windows 7 / Windows Server 2008 R2 (или более новой версии).

**Рекомендуется:**

* 8-ядерный ЦП;
* 8 ГБ ОЗУ;
* 64-разрядная версия Windows 2012 R2 (или более поздняя версия).

**Важные сведения:**

* Во время установки Регистрация шлюза в Azure выбирается hello регион по умолчанию для вашей подписки. Вы можете выбрать другой регион. При наличии серверов в нескольких регионах необходимо установить шлюз для каждого региона. 
* Невозможно установить шлюз Hello на контроллере домена.
* На одном компьютере можно установить только один шлюз.
* Hello шлюз можно установите на компьютере, который остается на и не переходит в toosleep.
* Не устанавливайте шлюз hello в сети через беспроводное соединение подключенных tooyour. Это может стать причиной снижения производительности.


## <a name="download"></a>Загрузка
 [Загрузите шлюз hello](https://aka.ms/azureasgateway)

## <a name="install"></a>Установка

1. Запустите программу установки.

2. Выберите расположение, примите условия hello и нажмите кнопку **установить**.

   ![Расположение для установки и условия лицензии](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Установите флажок **On-premises data gateway (recommended)** (Локальный шлюз данных (рекомендуется)). Azure Analysis Services не поддерживает личный режим.

   ![Выбор типа шлюза](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Введите учетную запись toosign в tooAzure. Учетная запись Hello должна быть в вашего клиента Azure Active Directory. Эта учетная запись используется для hello администратору шлюза. 

   ![Введите учетную запись toosign в tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Если выполнить вход с учетной записью домена, он будет сопоставлен tooyour учетную запись организации в Azure AD. Администратор шлюза hello hello будет использоваться учетной записью вашей организации.

## <a name="register"></a>Регистрация
В порядке toocreate ресурс шлюза в Azure необходимо зарегистрировать локальный экземпляр hello, установленный с hello облачной службе шлюза. 

1.  Выберите **Регистрация нового шлюза на этом компьютере**.

    ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Введите имя и ключ восстановления для шлюза. По умолчанию hello шлюз использует область по умолчанию для вашей подписки. Если вам требуется tooselect другой регион, выберите **Смена региона**.

   ![регистрация;](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Создание ресурса шлюза Azure
После установки и регистрации шлюза необходимо toocreate ресурсов шлюза в подписке Azure. Вход tooAzure с hello же учетная запись, используемая при регистрации шлюза hello.

1. На портале Azure щелкните **Create a new service** (Создать службу) > **Enterprise Integration** (Интеграция Enterprise) > **Локальный шлюз данных** > **Создать**.

   ![Создание ресурса шлюза](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. В разделе **Create connection gateway** (Создать шлюз для подключения) введите следующие параметры:

    * **Имя.** Введите имя для вашего ресурса шлюза. 

    * **Подписки**: выберите hello tooassociate подписки Azure с этим ресурсом шлюза. 
    Это подписка должна быть hello серверы находятся в одной подписке.
   
      Подписка по умолчанию Hello основан на hello учетная запись Azure, который использовался toosign в.

    * **Группа ресурсов.** Создайте группу ресурсов Azure или выберите имеющуюся.

    * **Расположение**: регистрации шлюза в области выберите hello.

    * **Установка имя**: Если для установки шлюза еще не выбрана, выберите hello шлюз зарегистрирован. 

    Когда все будет готово, нажмите **Создать**.

## <a name="connect-servers"></a>Подключение серверов toohello шлюза ресурсов

1. В обзоре сервера Azure Analysis Services щелкните **Локальный шлюз данных**.

   ![Подключение сервера toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. В **выбрать локальный шлюз данных tooconnect**, выберите ресурс шлюза и нажмите кнопку **подключение шлюза**.

   ![Подключение сервера toogateway ресурсов](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Если шлюз не отображается в списке hello, сервер не скорее всего, в hello же регионе, что область hello, указанные при регистрации шлюза hello. 

Вот и все. Если требуются tooopen порты или выполнять устранение неполадок будет убедиться, что toocheck out [локального шлюза данных](analysis-services-gateway.md).

## <a name="next-steps"></a>Дальнейшие действия
* [Управление службами Analysis Services](analysis-services-manage.md)   
* [Получение данных из служб Azure Analysis Services](analysis-services-connect.md)
