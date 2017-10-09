---
title: "изображений aaaCreate и отправки ВМ FreeBSD | Документы Microsoft"
description: "Узнайте, toocreate и отправка виртуального жесткого диска (VHD), содержащий toocreate операционной системе FreeBSD hello виртуальной машине Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Создание и отправка tooAzure FreeBSD виртуального жесткого диска
В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello FreeBSD операционной системы. После загрузки, его можно использовать как toocreate собственный образ виртуальной машины (VM) в Azure.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения о загрузке VHD с помощью модели hello диспетчера ресурсов см. в разделе [здесь](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что hello следующих элементов:

* **Подписка Azure**. Если у вас нет учетной записи, то ее можно создать, что займет всего лишь несколько минут. Если у вас есть подписка MSDN, см. страницу [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). В противном случае — Узнайте, каким образом слишком[создать бесплатную пробную учетную запись](https://azure.microsoft.com/pricing/free-trial/).  
* **Средства Azure PowerShell**--hello Azure PowerShell модуль должен быть установлен и настроен toouse подписки Azure. модуль toodownload hello, в разделе [загрузки Azure](https://azure.microsoft.com/downloads/). Учебник, в котором описывается как tooinstall и настроить модуль hello доступен здесь. Используйте hello [загрузки Azure](https://azure.microsoft.com/downloads/) hello tooupload командлет виртуального жесткого диска.
* **FreeBSD операционной системы, установленной в VHD-файл**--поддерживаемой операционной системе FreeBSD должен быть установлен tooa виртуального жесткого диска. Существуют несколько средства toocreate VHD-файлы. Например можно использовать решение виртуализации, таких как Hyper-V toocreate hello VHD-файл и установить hello операционной системы. Инструкции о том, как tooinstall и использование Hyper-V, на экране [Установка Hyper-V и создание виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hello более новый формат VHDX не поддерживается в Azure. Вы можете преобразования формата tooVHD hello диска с помощью диспетчера Hyper-V или командлета hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Кроме того, [учебник на MSDN о том, как toouse FreeBSD в Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Эта задача включает hello следующие пять шагов:

## <a name="step-1-prepare-hello-image-for-upload"></a>Шаг 1: Подготовка образа hello для передачи
На виртуальной машине hello установленным hello FreeBSD операционной системы выполните hello следующих процедур.

1. Включите DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Включите SSH.

    Убедитесь, что hello SSH сервер установлен и настроен toostart во время загрузки. Он включается по умолчанию после установки с диска FreeBSD. 
3. Настройте последовательную консоль.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Установите sudo.

    Учетная запись root Hello отключен в Azure. Это означает, что необходимо tooutilize sudo с помощью команд toorun непривилегированного пользователя с повышенными привилегиями.

        # pkg install sudo
   
5. Необходимые условия для агента Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Установите агент Azure.

    Hello последний выпуск hello агент Azure всегда находятся на [github](https://github.com/Azure/WALinuxAgent/releases). Здравствуйте, версия 2.0.10 + официально поддерживающей FreeBSD 10 & 10.1 и версии hello 2.1.4 Установка + (включая 2.2.x) официально поддерживающей FreeBSD 10.2 и более поздних версий.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    В качестве примера версии 2.0 будем использовать версию 2.0.16.

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    В качестве примера версии 2.1 будем использовать версию 2.1.4.

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > После установки агента Azure очень хорошее представление tooverify, на котором он выполняется:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Сделать hello системы.

    Отзыв hello системы tooclean его и внести он подходит для инициализацию. Hello следующая команда также удаляет hello последнего подготовленных учетную запись и hello связанных данных:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Теперь вы можете завершить работу виртуальной машины.

## <a name="step-2-create-a-storage-account-in-azure"></a>Шаг 2. Создание учетной записи хранения в Azure
Необходимо учетной записи хранилища в Azure tooupload VHD-файл, чтобы его можно использовать toocreate виртуальной машины. Можно использовать hello Azure классического портала toocreate учетной записи хранилища.

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Выберите на панели команд hello, **New**.
3. Последовательно выберите **Службы данных** > **Хранилище** > **Быстрое создание**.

    ![Быстрое создание учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Заполните поля hello, как показано ниже:

   * В hello **URL-адрес** введите имя дочернего домена toouse в URL-адрес учетной записи хранилища hello. запись Hello могут содержать от 3 до 24 цифры и буквы в нижнем регистре. Это имя становится именем узла hello в hello URL-адреса, используемые tooaddress хранилища больших двоичных объектов Azure, хранилища очередей Azure или ресурсами хранилища таблиц Azure для подписки hello.
   * В hello **расположение или территориальная группа** раскрывающееся меню, выберите hello **расположение или территориальная группа** для учетной записи хранения hello. Территориальная группа позволяет поместить облачных служб и хранилища в hello одного центра обработки данных.
   * В hello **репликации** определите ли toouse **Геоизбыточное** репликации для учетной записи хранения hello. По умолчанию георепликация включена. Этот параметр реплицируется на данных tooa вторичного расположения, в tooyou без затрат, чтобы хранилища при сбое toothat расположении при крупном сбое происходит hello основного расположения. вторичное расположение Hello присваивается автоматически и не может быть изменено. Если требуется больший контроль над расположение hello облачного хранилища из-за требований toolegal или политика организации географическую репликацию можно отключить. Однако имейте в виду, что если позже включить географическую репликацию данных будет взиматься однократного входящий трафик передачи данных tooreplicate плата имеющееся местоположение вторичного toohello данных. Службы хранения без георепликации предлагаются со скидкой. Дополнительные сведения об управлении георепликацией учетных записей хранения см. в статье [Репликация службы хранилища Azure](../../../storage/common/storage-redundancy.md).

     ![Введите сведения об учетной записи хранения](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Щелкните **Создать учетную запись хранения**. Hello учетной записи теперь отображается в списке **хранения**.

    ![Учетная запись хранения успешно создана](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Теперь создайте контейнер для переданных VHD-файлов. Выберите имя учетной записи хранения hello, а затем выберите **контейнеры**.

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Щелкните **Создать контейнер**.

    ![Информация об учетной записи хранения](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. В hello **имя** введите имя для контейнера. Затем в hello **доступа** раскрывающееся меню, выберите тип политики доступа, требуется.

    ![Имя контейнера](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > По умолчанию hello контейнер является закрытым и может осуществляться только владельцем учетной записи hello. tooallow общего доступа на чтение toohello BLOB-объектов в контейнере hello, но toohello свойства контейнера и метаданные, использовать hello **большой двоичный объект открытого** параметр. tooallow полный открытый доступ чтения для hello контейнера и больших двоичных объектов, используйте hello **открытый контейнер** параметр.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Шаг 3: Подготовка tooAzure подключения hello
Перед отправкой VHD-файл, необходимо tooestablish безопасное подключение между компьютером и вашей подписке Azure. Можно использовать метод hello Azure Active Directory (Azure AD) или hello toodo метод сертификата его.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Используйте метод hello Azure AD tooupload VHD-файл
1. Откройте hello консоли Azure PowerShell.
2. Введите следующую команду hello:  
    `Add-AzureAccount`

    После выполнения команды откроется окно входа и вы сможете войти, используя свою рабочую или учебную учетную запись.

    ![Окно PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure выполняет проверку подлинности и сохраняет hello учетные данные. Затем он закрывает окно приветствия.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Используйте tooupload метод сертификат hello VHD-файл
1. Откройте hello консоли Azure PowerShell.
2. Введите `Get-AzurePublishSettingsFile`.
3. Окно браузера откроется и предлагает вам toodownload hello файл PUBLISHSETTINGS. Этот файл содержит сведения и сертификат для подписки Azure.

    ![Страница скачивания браузера](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Сохраните файл PUBLISHSETTINGS hello.
5. Тип: `Import-AzurePublishSettingsFile <PathToFile>`, где `<PathToFile>` — файл PUBLISHSETTINGS toohello hello полный путь.

   Дополнительные сведения см. в статье [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx) (Начало работы с командлетами Azure).

   Дополнительные сведения об установке и настройке PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Шаг 4: Отправка hello VHD-файл
При передаче hello VHD-файл, его можно поместить в любом месте в хранилище BLOB-объектов. Ниже приведены некоторые термины, которые будут использоваться при отправке файла hello.

* **BlobStorageURL** hello URL-адрес для учетной записи хранения hello, созданный на шаге 2.
* **YourImagesFolder** — контейнер hello в хранилище больших двоичных объектов, место toostore изображений.
* **VHDName** — hello метка, которая отображается в hello Azure классического портала tooidentify hello виртуального жесткого диска.
* **PathToVHDFile** hello полный путь и имя hello VHD-файл.

Из окна Azure PowerShell hello, использованные в предыдущем шаге hello введите:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Шаг 5: Создайте виртуальную Машину с hello загруженный VHD-файл
После загрузки hello VHD-файл можно добавить его как изображение toohello список пользовательских образов, связанных с подпиской и создать виртуальную машину с этого пользовательского образа.

1. Из окна Azure PowerShell hello, использованные в предыдущем шаге hello введите:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Используйте в качестве типа hello операционной системы Linux. Текущая версия Azure PowerShell Hello принимает в качестве параметра только «Linux» или «Windows».
   >
   >
2. После выполнения предыдущих шагов hello hello новое изображение отображается при выборе hello **изображения** вкладку на hello классический портал Azure.  

    ![Выбор образа](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Создание виртуальной машины из коллекции hello. Этот новый образ теперь доступен в разделе **Мои образы**.
4. Выбор нового образа hello. Далее выполните tooset приглашения hello имя узла, пароль, ключа SSH и т. д.

    ![Пользовательский образ](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. После завершения подготовки hello, вы увидите FreeBSD ВМ в Azure.

    ![Образ FreeBSD в Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
