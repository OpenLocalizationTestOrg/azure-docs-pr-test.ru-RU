---
title: "aaaPortal подготовки для StorSimple Virtual Array | Документы Microsoft"
description: "Первый учебника toodeploy виртуального массива StorSimple заключается в подготовке hello портал Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Развертывание StorSimple Virtual Array — Подготовка hello портал Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Обзор

Это hello первой статье серии hello руководства по развертыванию необходимых toocompletely развернуть виртуальный массив в качестве файлового сервера или сервера iSCSI с помощью модели hello диспетчера ресурсов. В этой статье описывает toocreate подготовки необходимые hello и настройте предыдущих tooprovisioning каталога службы вашего устройства StorSimple виртуального массива. В этой статье также связывает out tooa настройки конфигурации и контрольный список необходимые условия для развертывания.

Необходимо, чтобы администратор права toocomplete hello процесса установки и настройки. Мы рекомендуем, изучите контрольный список для настройки развертывания hello перед началом. Подготовка портала Hello занимает менее 10 минут.

Информация Hello, опубликованы в этой статье относится развертывания toohello StorSimple виртуальных массивов в hello портал Azure и государственных облако Microsoft Azure.

### <a name="get-started"></a>Начало работы
Hello рабочий процесс развертывания состоит из подготовки портала hello, подготовку виртуальных массивов в виртуализованной среде и завершения установки hello. tooget работы по развертыванию StorSimple Virtual Array hello как файлового сервера или сервера iSCSI, необходимо toohello toorefer следующие табличный ресурсы.

#### <a name="deployment-articles"></a>Статьи по развертыванию

toodeploy виртуального массива StorSimple, см. следующие статьи в hello предписанные последовательности toohello.

| **#** | **Шаг** | **Выполняемые действия** | **Справочная документация** |
| --- | --- | --- | --- |
| 1. |**Настройка hello портал Azure** |Создайте и настройте предыдущих tooprovisioning каталога службы вашего устройства StorSimple StorSimple Virtual Array. |[Подготовка hello портала](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Подготовить hello Virtual Array** |Для Hyper-V подготовки и подключите tooa StorSimple Virtual Array в системе узла, под управлением Hyper-V Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2. <br></br> <br></br> Для VMware подготовки и подключите tooa StorSimple Virtual Array в системе узла, под управлением VMware ESXi 5.5 и более поздних версий.<br></br> |[Развертывание виртуального массива StorSimple — подготовка виртуального массива в Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Развертывание виртуального массива StorSimple — подготовка виртуального массива в VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Настройка виртуального массива hello** |Для файлового сервера выполнения начальной настройки, регистрации StorSimple файлового сервера и выполните настройку hello. Затем подготовьте к работе общие папки SMB. <br></br> <br></br> Для сервера iSCSI выполнения начальной настройки, регистрации сервера iSCSI StorSimple и завершить настройку устройства hello. Затем подготовьте к работе тома iSCSI. |[Развертывание виртуального массива StorSimple — установка в качестве файлового сервера](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Развертывание виртуального массива StorSimple — настройка виртуального устройства в качестве сервера iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Теперь можно начинать tooset копирование hello портал Azure.

## <a name="configuration-checklist"></a>Контрольный список для настройки

Контрольный список для настройки Hello описывает hello информацию необходимо toocollect перед настройкой hello программного обеспечения на ваш StorSimple Virtual Array. Подготовка этой информации опережает время помогает оптимизировать hello процесс развертывания устройства StorSimple hello в вашей среде. Зависимости, развернут ли виртуального массива StorSimple в качестве файлового сервера или сервера iSCSI, требуется один из следующих контрольных списках hello.

* Загрузите hello [StorSimple виртуального массива файл конфигурации контрольный список сервера](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Загрузите hello [StorSimple Virtual Array iSCSI контрольный список для настройки сервера](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Предварительные требования

Здесь можно найти hello предварительные требования конфигурации для службы диспетчера StorSimple устройство, StorSimple Virtual Array и hello сети центра обработки данных.

### <a name="for-hello-storsimple-device-manager-service"></a>Для hello службой диспетчера устройств StorSimple

Перед тем как начать, убедитесь в следующем.

* Имеется учетная запись Майкрософт и данные для доступа к ней.
* Имеется учетная запись хранения Microsoft Azure и данные для доступа к ней.
* В вашей подписке Microsoft Azure настроена служба диспетчера устройств StorSimple.

### <a name="for-hello-storsimple-virtual-array"></a>Для hello StorSimple Virtual Array

Перед развертыванием виртуального массива выполните указанные ниже условия.

* У вас есть доступ tooa компьютерной системе под управлением Hyper-V в Windows Server 2008 R2 или более поздней версии или VMware (ESXi 5.5 или более поздней версии), можно использовать tooa подготовки устройства.
* Hello система узла — может toodedicate hello следующие ресурсы tooprovision виртуального массива:
  
  * Не менее 4 ядер.
  * Не менее 8 ГБ ОЗУ. Если планируется tooconfigure hello виртуального массива как файловый сервер, 8 ГБ поддерживает 2 миллионов файлов. Необходимо 2-4 миллиона toosupport файла по 16 ГБ ОЗУ.
  * Один сетевой интерфейс.
  * Виртуальный диск размером 500 ГБ для системных данных.

### <a name="for-hello-datacenter-network"></a>Для hello сети центра обработки данных

Перед тем как начать, убедитесь в следующем.

* согласно hello сетевые требования для устройства StorSimple, необходимо настроить сеть Hello в центре обработки данных. Дополнительные сведения см. в разделе hello [требования к системе StorSimple виртуального массива](storsimple-ova-system-requirements.md).
* Виртуальный массив StorSimple всегда подключен к выделенному интернет-каналу с пропускной способностью не менее 5 Мбит/с. Эту пропускную способность не следует использовать совместно с другими приложениями.

## <a name="step-by-step-preparation"></a>Пошаговая подготовка

Используйте следующие пошаговые инструкции tooprepare hello портал для hello службы диспетчера StorSimple устройство.

## <a name="step-1-create-a-new-service"></a>Шаг 1. Создание новой службы

Один экземпляр службы диспетчера StorSimple устройство hello можно управлять нескольких виртуальных массивов StorSimple. Выполните следующие шаги toocreate экземпляр службы диспетчера StorSimple устройство hello hello. При наличии существующего toomanage службы диспетчера StorSimple устройство виртуального массивах, пропустите этот шаг и перейти слишком[шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Если вы не включили hello автоматическое создание учетной записи хранилища в службе, необходимо будет toocreate по крайней мере одну учетную запись хранения после успешного создания службы.
> 
> * Если не была автоматически создана учетная запись хранения, перейдите в слишком[настроить новую учетную запись хранилища для службы hello](#optional-step-configure-a-new-storage-account-for-the-service) подробные инструкции.
> * Если вы включили hello автоматическое создание учетной записи хранилища, перейдите в слишком[шаг 2: ключ регистрации службы hello Get](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Шаг 2: Получение ключа регистрации службы hello

После hello службы диспетчера StorSimple устройство работает, потребуется ключ регистрации службы tooget hello. Этот ключ используется tooregister и подключите устройство StorSimple со службой hello.

Выполните следующие шаги в hello hello [портал Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Hello регистрационный ключ службы является используется tooregister все hello устройства StorSimple устройства, которые требуют tooregister в службе диспетчера StorSimple устройство.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Шаг 3: Загрузите образ виртуального массива hello

После того как вы hello ключ регистрации службы, необходимо будет toodownload hello соответствующий виртуальный массив изображения tooprovision виртуального массива в главной системе. образы виртуальных массивов Hello конкретной операционной системы и можно загрузить на странице быстрого запуска hello в hello портал Azure.

> [!IMPORTANT]
> Hello программного обеспечения hello StorSimple Virtual Array может использоваться только с hello службы диспетчера StorSimple устройство.
> 
> 

Выполните следующие шаги в hello hello [портал Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>образ виртуального массива tooget hello

1. Вход в hello [портал Azure](https://portal.azure.com/). 
2. В hello портал Azure, щелкните **Обзор > диспетчеры устройств StorSimple**.
3. Выберите имеющуюся службу диспетчера устройств StorSimple. В hello **устройства StorSimple** колонка, щелкните **быстрый запуск**. 
4. Щелкните hello ссылку toohello образы, которые должны toodownload из центра загрузки Майкрософт hello. файлы изображений Hello, примерно 4,8 ГБ.
   
   * VHDX для Hyper-V в Windows Server 2012 и более поздней версии.
   * VHDX для Hyper-V в Windows Server 2008 R2 и более поздней версии.
   * VMDK для VMWare ESXi 5.5 и более поздней версии.
5. Загрузите и распакуйте hello файл tooa локального диска, создания заметки из которой находится файл распакованную hello.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Необязательный шаг: настройте новую учетную запись хранилища для службы hello

Этот шаг является необязательным и должно выполняться только в том случае, если вы не включили hello автоматическое создание учетной записи хранилища в службе.

При необходимости toocreate учетную запись хранилища Azure в другом регионе. в разделе [как toocreate учетной записи хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) пошаговые инструкции.

Выполните следующие шаги в hello hello [портал Azure](https://ms.portal.azure.com/) на страницу службы tooadd существующую учетную запись хранения Microsoft Azure для hello устройства StorSimple.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd учетные данные учетной записи хранилища с hello ту же подписку Azure hello службы диспетчера устройств

1. Перейдите tooyour службы Диспетчер устройств, выберите и дважды щелкните его. При этом откроется hello **Обзор** колонку.
2. Выберите **учетные данные хранилища** внутри hello **конфигурации** раздела.
3. Щелкните **Добавить**.
4. В hello **добавить учетную запись хранилища** колонке hello следующие:
   
    1. Для параметра **Подписка** выберите значение **Текущая**.
   
    2. Укажите имя hello вашей учетной записи хранилища Azure.
   
    3. Выберите **включить** toocreate защищенный канал сетевого взаимодействия между облачной StorSimple устройство и hello. Если используется частное облако, выберите параметр **Отключить**.
   
    4. Щелкните **Добавить**. Вы будете оповещены после успешного создания учетной записи хранилища hello.<br></br>
   
     ![Добавление учетных данных имеющейся учетной записи хранения](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Дальнейшие действия

Hello следующим шагом является tooprovision виртуальной машины для виртуального массива StorSimple. В зависимости от операционной системе узла. в разделе hello подробные инструкции в:

* [Развертывание виртуального массива StorSimple — подготовка виртуального массива в Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Развертывание виртуального массива StorSimple — подготовка виртуального массива в VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

