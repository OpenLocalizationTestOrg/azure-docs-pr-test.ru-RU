---
title: "aaaHow tooinstall главного целевого сервера под управлением Linux для отработки отказа из Azure tooon организациями | Документы Microsoft"
description: "Для повторного включения защиты виртуальной машины Linux необходим главный целевой сервер Linux. Узнайте, как tooinstall один."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Установка главного целевого сервера Linux
После отказа виртуальных машин, может произойти сбой назад hello виртуальные машины toohello на локальном сайте. toofail обратно необходимо tooreprotect hello виртуальную машину из Azure toohello на локальном сайте. Для этого процесса необходимо локально master tooreceive hello трафик от целевых серверов. 

Если защита включается для виртуальной машины Windows, вам потребуется главный целевой сервер Windows. Для виртуальной машины Linux необходим главный целевой сервер Linux. Чтение hello следующие шаги toolearn как toocreate и установить Linux master target.

> [!IMPORTANT]
> Начиная с выпуска hello 9.10.0 главный целевой сервер, hello последнюю главный целевой сервер можно только установить на сервере Ubuntu 16.04. Новые экземпляры невозможно устанавливать на серверы CentOS6.6. Тем не менее вы можете продолжить tooupgrade старого главного целевые серверы с помощью hello 9.10.0 версии.

## <a name="overview"></a>Обзор
Эта статья содержит инструкции по как tooinstall Linux главный целевой.

Разместить комментарии или вопросы в конце hello в этой статье, либо на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Предварительные требования

* определить узла hello toochoose какие toodeploy hello главного целевого сервера, если восстановление размещения hello будет toobe tooan существующих локальных виртуальных машин или tooa новой виртуальной машины. 
    * Для существующей виртуальной машины узла hello hello главного целевого объекта должны иметь хранилищ данных toohello доступа hello виртуальной машины.
    * Если hello локальной виртуальной машины не существует, hello восстановления размещения виртуальной машины создается на hello же размещаться hello главного целевого сервера. Можно выбрать любой узел ESXi главного целевого tooinstall hello.
* Hello главный целевой сервер должен быть в сети, который может взаимодействовать с сервером обработки hello и сервер конфигурации hello.
* версия Hello hello главного целевого сервера должна быть равна tooor более ранних, чем версии hello hello сервера обработки и сервер конфигурации hello. Например если версия сервера конфигурации hello hello 9.4, версию hello hello главного целевого объекта можно 9.4 или 9.3, но не 9,5.
* Hello главного целевого сервера может быть только виртуальной машины VMware и физического сервера.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Создать главный целевой объект hello в соответствии с toohello правила изменения размера

Создание главного целевого сервера в соответствии с инструкциями изменения размера hello hello:
- **ОЗУ**: 6 ГБ или больше.
- **Размер диска операционной системы**: 100 ГБ или больше (tooinstall CentOS6.6)
- **Дополнительное пространство для диска хранения**: 1 ТБ.
- **Ядра ЦП**: 4 ядра или больше.

поддерживает следующие Hello Ubuntu поддерживаемых ядер.


|Серии ядер  |Поддерживает систему слишком |
|---------|---------|
|4.4.      |4.4.0-81-generic         |
|4.8      |4.8.0-56-generic         |
|4.10     |4.10.0-24-generic        |


## <a name="deploy-hello-master-target-server"></a>Развернуть главный целевой сервер hello

### <a name="install-ubuntu-16042-minimal"></a>Минимальная установка Ubuntu 16.04.2

Принимать hello, следуя hello действия tooinstall hello Ubuntu 16.04.2 64-разрядной операционной системе.

**Шаг 1.** Go toohello [ссылка для загрузки](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) и выберите ближайший зеркальной hello из которой загрузить Ubuntu 16.04.2 минимальной 64-разрядных ISO-ОБРАЗА.

Хранить Ubuntu 16.04.2 минимальной 64-разрядных ISO-ОБРАЗА в hello DVD-диска и запуска системы hello.

**Шаг 2.** Выберите **Русский** в качестве предпочтительного языка и нажмите клавишу **ВВОД**.

![Выбор языка](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Шаг 3.** выберите **Install Ubuntu Server** (Установить сервер Ubuntu) и нажмите клавишу **ВВОД**.

![Выбор установки сервера Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Шаг 4.** Выберите **Русский** в качестве предпочтительного языка и нажмите клавишу **ВВОД**.

![Выбор русского в качестве предпочтительного языка](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Шаг 5.** Здравствуйте, выберите соответствующий вариант из hello **часовой пояс** список параметров, а затем выберите **ввод**.

![Выберите правильный часовой пояс hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Шаг 6.** выберите **нет** (hello параметр по умолчанию), а затем выберите **ввод**.


![Настройка сочетания hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Шаг 7.** выберите **английского языка (США)** как hello Страна происхождения hello клавиатуре, а затем выберите **ввод**.

![Выберите США как Страна происхождения hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Шаг 8.** выберите **английского языка (США)** как hello раскладки клавиатуры, а затем выберите **ввод**.

![Выберите в качестве раскладки клавиатуры hello английский (США)](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Шаг 9.** введите hello узла для сервера в hello **Hostname** поле, а затем выберите **Продолжить**.

![Введите имя узла hello сервера](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Шаг 10.** toocreate учетной записи пользователя, введите имя пользователя hello и выберите **Продолжить**.

![Создание учетной записи пользователя](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Шаг 11.** пароль hello hello новой учетной записи пользователя, а затем выберите **Продолжить**.

![Введите пароль hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Шаг 12.** подтверждение пароля hello для hello нового пользователя, а затем выберите **Продолжить**.

![Подтверждение пароля hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Шаг 13.** выберите **нет** (hello параметр по умолчанию), а затем выберите **ввод**.

![Настройка пользователей и паролей](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Шаг 14.** Если правильно hello часового пояса, которое отображается, выберите **Да** (hello параметр по умолчанию), а затем выберите **ввод**.

tooreconfigure свой часовой пояс, выберите **нет**.

![Настройка часов hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Шаг 15.** hello метод параметры секционирования, выберите **интерактивной - использовать весь диск**, а затем выберите **ввод**.

![Выберите вариант метод секционирования hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Шаг 16.** Здравствуйте, выберите соответствующий диск из hello **выберите диск toopartition** параметры, а затем выберите **ввод**.


![Выберите диск hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Этап 17:** выберите **Да** toowrite hello toodisk изменения, а затем выберите **ввод**.

![Запись изменений toodisk hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Шаг 18.** параметр используется по умолчанию hello, выберите **Продолжить**, а затем выберите **ввод**.

![Выберите параметр по умолчанию hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Шаг 19:** выберите hello соответствующий параметр для обновления в системе управления, а затем выберите **ввод**.

![Выберите, каким образом обновляет toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Поскольку hello Azure Site Recovery главный целевой сервер требует очень конкретной версии hello Ubuntu, вам потребуется tooensure, ядра hello обновления отключены для hello виртуальной машины. Если они включены все регулярные обновления вызвать hello главного целевого сервера toomalfunction. Необходимо выбрать hello **без автоматического обновления** параметр.


**Шаг 20.** Выберите параметры по умолчанию. OpenSSH SSH-подключения, выберите hello **OpenSSH server** , а затем установите **Продолжить**.

![Выбор программного обеспечения](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Шаг 21.** Щелкните **Да**, а затем нажмите клавишу **ВВОД**.

![Загрузчик GRUB hello установки](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Шаг 22:** Здравствуйте, выберите соответствующее устройство для установки начальной загрузки hello (предпочтительно **/dev/sda**), а затем выберите **ввод**.

![Выбор устройства для установки загрузчика](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Шаг 23:** выберите **Продолжить**, а затем выберите **ввод** toofinish hello установки.

![Завершите установку hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

После завершения процесса установки hello, войдите в toohello виртуальной Машины с новыми учетными данными пользователя hello. (См. слишком**шаг 10** подробнее.)

Занять hello шаги, описанные в следующий снимок экрана tooset hello КОРНЕВОЙ hello пароль пользователя. Затем войдите как привилегированный пользователь.

![Пароль пользователя КОРНЕВОГО набора hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Подготовка машины hello для конфигурации как главный целевой сервер
Далее Подготовьте машину hello для конфигурации как главный целевой сервер.

Идентификатор hello tooget для каждого жесткого диска SCSI на виртуальной машине Linux, включите hello **диска. EnableUUID = TRUE** параметра.

tooenable, этот параметр hello выполните следующие шаги:

1. Завершите работу виртуальной машины.

2. Щелкните правой кнопкой мыши запись hello hello виртуальной машины в левой области hello, а затем выберите **изменение параметров**.

3. Выберите hello **параметры** вкладки.

4. Hello левой панели выберите **Дополнительно** > **Общие**и затем выберите hello **параметры конфигурации** кнопку hello правой нижней части экрана приветствия.

    ![Вкладка "Параметры"](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Hello **параметры конфигурации** параметр недоступен, когда машина hello работает. toomake на этой вкладке active, hello виртуальной машины завершена.

5. Посмотрите, есть ли строка с параметром **disk.EnableUUID**.

    - Если значение hello существует и имеет значение слишком**False**, измените значение hello слишком**True**. (hello значениях регистр не учитывается.)

    - Если значение hello существует и имеет значение слишком**True**выберите **отменить**.

    - Если значение hello не существует, выберите **добавить строку**.

    - В столбце Имя hello, добавьте **диска. EnableUUID**и задайте значение hello слишком**TRUE**.

    ![Проверка наличия параметра disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Отключение обновления ядра

Azure Site Recovery главный целевой сервер требует очень конкретной версии hello Ubuntu, убедитесь, что обновления ядра hello отключены для hello виртуальной машины.

Если включены обновления ядра, какие-либо регулярного обновления вызвать hello главного целевого сервера toomalfunction.

#### <a name="download-and-install-additional-packages"></a>Скачивание и установка дополнительных пакетов

> [!NOTE]
> Убедитесь, что toodownload подключения к Интернету и установить дополнительные пакеты. Если у вас нет подключения к Интернету, необходимо toomanually эти пакеты RPM найти и установить их.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Получить hello установщика для установки

Если ваш главный целевой имеет подключение к Интернету, можно использовать следующие шаги toodownload hello установщика hello. В противном случае можно скопировать hello установщика с сервера обработки hello и установите его.

#### <a name="download-hello-master-target-installation-packages"></a>Загрузить пакеты установки hello главного целевого сервера

[Загрузить последние элементы в установки Linux главного целевого сервера hello](https://aka.ms/latestlinuxmobsvc).

toodownload его с помощью Linux, тип:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Убедитесь, что вы загрузите и распакуйте установщика hello в домашнем каталоге. Если вы Распакуйте слишком**/usr/Local**, происходит сбой установки hello.


#### <a name="access-hello-installer-from-hello-process-server"></a>Установщик hello доступ с сервера обработки hello

1. На сервере процесса hello, перейти слишком**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86)**.

2. Скопируйте файл установщика необходимых hello с сервера обработки hello и сохраните его в **latestlinuxmobsvc.tar.gz** в домашнем каталоге.


### <a name="apply-custom-configuration-changes"></a>Применение изменений настраиваемой конфигурации

tooapply пользовательские изменения конфигурации, hello используйте следующие шаги:


1. Запустите hello, следующая команда toountar hello binary.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Снимок экрана: команда toorun hello](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Выполните следующие команды toogive разрешение hello.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Запустите следующий сценарий hello toorun hello.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Запустите сценарий hello только один раз на сервере hello. Завершите работу сервера hello. Затем перезапустите hello сервер после добавления дисков, как описано в следующем разделе hello.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Добавить виртуальную машину главного целевого сервера Linux хранения диска toohello

Используйте следующие шаги toocreate диска хранения hello.

1. Подключите новый диск размером 1 ТБ toohello главный целевой виртуальной машине Linux, а затем запустите машины hello.

2. Используйте hello **многоканального -ll** toolearn hello многоканального ИД диска хранения hello команды.

    ```
    multipath -ll
    ```
    ![Hello многоканального идентификатор диска хранения hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Отформатировать диск hello и затем создать файловую систему на новый диск hello.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Создание файловой системы на диске hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. После создания hello файловой системы, подключите диск хранения hello.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Подключение диска хранения hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Создать hello **fstab** входа toomount hello диск для хранения каждый раз при запуске системы hello.
    ```
    vi /etc/fstab
    ```
    Выберите **вставить** toobegin редактирования файла hello. Создать новую строку и вставьте следующий текст hello. Изменения многоканального идентификатор hello диска на основе идентификатора многоканального hello выделяются из предыдущей команды hello.

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    Выберите **Esc**, а затем введите **: wq** (записи и выйти из программы) окна редактора tooclose hello.

### <a name="install-hello-master-target"></a>Установить главный целевой сервер hello

> [!IMPORTANT]
> версия Hello hello главного целевого сервера должна быть равна tooor более ранних, чем версии hello hello сервера обработки и сервер конфигурации hello. Если это условие не соблюдено, то включить защиту удастся, однако репликация завершится ошибкой.


> [!NOTE]
> Прежде чем устанавливать hello главный целевой сервер, проверьте что hello **/etc/hosts** файл на виртуальной машине hello содержит записи, которые сопоставляют hello toohello локальному имени узла IP-адресов, связанных со всеми сетевыми адаптерами.

1. Скопируйте hello парольная фраза, из **Recovery\private\connection.passphrase узла Azure C:\ProgramData\Microsoft** на сервере конфигурации hello. Затем сохраните его как **passphrase.txt** в hello один локальный каталог, запустив hello следующую команду:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Пример: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Обратите внимание, IP-адрес сервера конфигурации hello. Необходимо в следующем шаге hello.

3. Запустите hello, следующая команда tooinstall hello главный целевой сервер и зарегистрируйте сервер hello с сервера конфигурации hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Пример: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Дождитесь завершения сценария hello. Если главный целевой сервер hello регистрирует успешно, hello главного целевого сервера присутствует в hello **инфраструктура Site Recovery** страницы портала hello.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Установка hello главного целевого сервера с помощью интерактивной установки

1. Следующая команда tooinstall hello главный целевой выполнения hello. Роль агента hello, выберите **главного целевого**.

    ```
    ./install
    ```

2. Выберите расположение установки по умолчанию hello, а затем выберите **ввод** toocontinue.

    ![Выбор расположения по умолчанию для установки главного целевого сервера](./media/site-recovery-how-to-install-linux-master-target/image17.png)

После завершения установки hello Зарегистрируйте сервер конфигурации hello с помощью командной строки hello.

1. Обратите внимание, hello IP-адрес сервера конфигурации hello. Необходимо в следующем шаге hello.

2. Запустите hello, следующая команда tooinstall hello главный целевой сервер и зарегистрируйте сервер hello с сервера конфигурации hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Пример: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Дождитесь завершения сценария hello. Если hello главный целевой сервер успешно зарегистрированного, hello главного целевого сервера присутствует в hello **инфраструктура Site Recovery** страницы портала hello.


### <a name="upgrade-hello-master-target"></a>Обновление главного целевого сервера hello

Запустите установщик hello. Он автоматически определяет, hello агент установлен на главном целевом сервере hello. tooupgrade, выберите **Y**.  После завершения установки hello, проверьте версию hello hello главного целевого сервера, установленного с помощью hello следующую команду.

    ```
    cat /usr/local/.vx_version
    ```

Видно, что hello **версии** поле дает номер версии hello hello главного целевого объекта.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Установить средства VMware на главном целевом сервере hello

Средства VMware tooinstall hello главного целевого сервера необходимо, чтобы он мог находить hello хранилищ данных. Если не установлены средства hello, экрана приветствия повторной защиты не отображается в хранилищах данных hello. После установки средства VMware hello необходимо toorestart.

## <a name="next-steps"></a>Дальнейшие действия
После установки hello и регистрации hello главного целевого объекта имеет finsihed, вы увидите главного целевого сервера hello отображаются на hello **главного целевого** статьи **инфраструктура Site Recovery**, в разделе hello Общие сведения о конфигурации сервера.

Теперь можно настроить [повторную защиту](site-recovery-how-to-reprotect.md) и выполнить восстановление размещения.

## <a name="common-issues"></a>Распространенные проблемы

* Убедитесь, что Storage vMotion не используется для компонентов системы управления, например для главного целевого сервера. Если после успешной повторной защиты перемещает hello главного целевого сервера, не может быть отсоединен hello диски виртуальной машины (VMDKs). В этом случае восстановление размещения завершится ошибкой.

* главный целевой сервер Hello не следует все моментальные снимки на виртуальной машине hello. Если существуют моментальные снимки, восстановление размещения завершится ошибкой.

* Из-за toosome пользовательские конфигурации сетевых Адаптеров на некоторые клиенты hello сетевой интерфейс отключен во время запуска и не удалось инициализировать агент hello главного целевого сервера. Убедитесь, что hello следующие свойства заданы правильно. Проверьте /etc/sysconfig/network-scripts/ifcfg файла карты для этих свойств в hello Ethernet-eth *.
    * BOOTPROTO=dhcp
    * ONBOOT=yes
