---
title: "aaaSet копирование Oracle ASM на виртуальной машине Azure Linux | Документы Microsoft"
description: "Быстрая подготовка и запуск Oracle ASM в среде Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Настройка Oracle ASM в виртуальной машине Linux в Azure  

Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду. В этом учебнике описано развертывание основных Azure виртуальной машины, в сочетании с hello установки и настройки из Oracle автоматического хранения данных управления (ASM).  Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать и присоединить tooan виртуальной Машины базы данных Oracle
> * Установка и настройка Oracle ASM.
> * Установка и настройка Oracle Grid Infrastructure.
> * Инициализация установки Oracle ASM.
> * Создание базы данных Oracle под управлением ASM.


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Подготовка среды hello

### <a name="create-a-resource-group"></a>Создание группы ресурсов

использовать toocreate группу ресурсов hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. В этом примере имя группы ресурсов *myResourceGroup* в hello *eastus* области.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Создание виртуальной машины

toocreate виртуальной машины на основе образа hello базы данных Oracle и настройте его toouse Oracle ASM, использовать hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает виртуальную Машину с именем myVM, имеет размер Standard_DS2_v2 с четырьмя подключенными дисками данных 50 ГБ. Если они еще не существуют в ключевое расположение по умолчанию hello, он также создает ключи SSH.  toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

После создания виртуальной Машины hello Azure CLI отображает toohello аналогичные сведения, следующий пример. Запомните значение hello для `publicIpAddress`. Используется этот адрес tooaccess hello виртуальной Машины.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Подключение toohello виртуальной Машины

toocreate сеанс SSH с hello виртуальной Машины и настроить дополнительные параметры, используйте следующую команду hello. Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной Машины.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Установка Oracle ASM

tooinstall ASM Oracle, полный hello следующие шаги. 

Дополнительные сведения об установке Oracle ASM см. в статье [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Скачиваемые компоненты Oracle ASMLib для Oracle Linux 6).  

1. Требуется toologin как корневой элемент в порядке toocontinue с установкой ассемблерного кода:

   ```bash
   sudo su -
   ```
   
2. Выполните эти дополнительные команды tooinstall Oracle ASM компоненты:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Убедитесь, что служба Oracle ASM установлена:

   ```bash
   rpm -qa |grep oracleasm
   ```

    Hello выходные данные этой команды должен содержать hello следующие компоненты:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM требует определенных пользователей и ролей в порядке toofunction правильно. hello необходимых учетных записей и групп, создайте Hello, следующие команды: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Убедитесь, что пользователи и группы созданы правильно:

   ```bash
   id grid
   ```

    Hello выходные данные этой команды должны содержать следующие hello пользователей и групп:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Создайте папку для пользователя *сетки* и сменить владельца hello:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Настройка Oracle ASM

В этом учебнике — пользователя по умолчанию hello *сетки* и группа по умолчанию hello *asmadmin*. Убедитесь, что hello *oracle* пользователь является членом группы asmadmin hello. tooset копирование установку Oracle ASM завершения hello, следующие шаги:

1. Настройка библиотеки драйвера hello Oracle ASM заключается в определении пользователя по умолчанию hello (сетка) и группа по умолчанию (asmadmin) и настройка toostart hello диска во время загрузки (выберите y) и tooscan для дисков во время загрузки (выберите y). Требуется tooanswer запросы hello hello следующую команду:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   Hello выходные данные этой команды должен выглядеть примерно toohello следующие, остановка с toobe приглашения ответов на.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Просмотр конфигурации диска hello:
   ```bash
   cat /proc/partitions
   ```

   Hello выходные данные этой команды должен выглядеть примерно toohello следующий список доступных дисков

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Отформатировать диск *иметь идентификатор/dev/sdc* , выполнив hello следующую команду и ответы на hello приглашения с:
   - *n* — новый раздел;
   - *p* — основной раздел;
   - *1* tooselect hello первую секцию
   - Нажмите клавишу `enter` для первого цилиндра по умолчанию hello
   - Нажмите клавишу `enter` для последнего цилиндра по умолчанию hello
   - Нажмите клавишу *w* toowrite hello изменения toohello секции таблицы  

   ```bash
   fdisk /dev/sdc
   ```
   
   Используя приведенные выше ответы hello, должен выглядеть hello выходные данные команды fdisk hello hello следующим образом:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Повторите hello предшествующий команды fdisk для `/dev/sdd`, `/dev/sde`, и `/dev/sdf`.

5. Проверьте конфигурацию диска hello.

   ```bash
   cat /proc/partitions
   ```

   Hello выходные данные команды hello должен выглядеть hello следующим образом:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Проверьте состояние службы Oracle ассемблерного кода hello и запустить службу hello Oracle ASM:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   Hello выходные данные команды hello должен выглядеть hello следующим образом:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Создайте диски Oracle ASM:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   Hello выходные данные команды hello должен выглядеть hello следующим образом:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Выведите список дисков Oracle ASM:

   ```bash
   service oracleasm listdisks
   ```   

   выходные данные Hello hello команды должны содержать off hello следующие диски Oracle ASM:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Измените пароли hello для пользователей hello корневой сервер, oracle и сетки. **Запишите эти новые пароли** как с помощью их позднее, во время установки hello.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Измените разрешения папки hello:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Скачивание и подготовка Oracle Grid Infrastructure

toodownload и подготовки программного обеспечения Oracle сетки инфраструктуры hello, полный hello, следующие шаги:

1. Загрузить hello инфраструктуры сетки Oracle [страницы загрузки Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   В разделе загрузок hello под названием **Oracle Database 12c выпуск 1 сетки инфраструктуры (12.1.0.2.0) для Linux x86-64**, загрузите hello два ZIP-файлов.

2. После загрузки hello .zip файлы tooyour клиентского компьютера, можно использовать протокол Secure копии (SCP) toocopy hello файлы tooyour виртуальной Машины:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH обратно в Oracle ВМ в Azure в порядке toomove hello ZIP-файлы в hello / opt папки. Затем измените владельца hello hello файлов:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Распакуйте файлы hello. (Hello установки Linux Распакуйте средство, если он еще не установлен.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Измените разрешение:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Обновите настроенную область буфера. Компоненты Oracle сетки требуется по крайней мере 6,8 ГБ пространства подкачки tooinstall сетки. размер файла подкачки по умолчанию Hello для изображений Oracle Linux в Azure — 2048 МБ памяти. Требуется tooincrease `ResourceDisk.SwapSizeMB` в hello `/etc/waagent.conf` файл и перезапустите службу WALinuxAgent hello в порядке для hello обновлены параметры tootake эффекта. Так как он является файлом только для чтения, необходимо разрешение на запись tooenable разрешения toochange файла.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Поиск `ResourceDisk.SwapSizeMB` и измените значение hello слишком**8192**. Вам потребуется toopress `insert` режим вставки tooenter, введите значение hello **8192** и нажмите клавишу `esc` tooreturn toocommand режим. toowrite hello изменения и закройте hello, тип файла `:wq` и нажмите клавишу `enter`.
   
   > [!NOTE]
   > Настоятельно рекомендуется всегда использовать `WALinuxAgent` tooconfigure пространство подкачки, чтобы он всегда создается hello локальных временных диска (временный диск) для достижения оптимальной производительности. Дополнительные сведения о разделе [как файл tooadd переключения на виртуальных машинах Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Подготовить локального клиента и виртуальной Машины toorun x11
Настройка Oracle ASM требуется графический интерфейс toocomplete hello установки и конфигурации. Мы используем toofacilitate протокола hello x11 этой установки. Если вы используете клиентскую систему (Mac или Linux), которая уже имеет X11 возможности включена и настроена — можно пропустить эту конфигурацию и настройки машин монопольного tooWindows. 

1. [Загрузить PuTTY](http://www.putty.org/) и [загрузки Xming](https://xming.en.softonic.com/) tooyour компьютер Windows. Вам необходима установка toocomplete hello оба приложения со значениями по умолчанию hello, прежде чем продолжить.

2. После установки PuTTY, откройте командную строку, перейдите в hello PuTTY папки (например, C:\Program Files\PuTTY) и запустите `puttygen.exe` чтобы toogenerate ключа.

3. В генераторе ключей PuTTY сделайте следующее:
   
   1. Создать ключ, выбрав hello `Generate` кнопки.
   2. Скопируйте содержимое hello hello ключ (сочетание клавиш Ctrl + C).
   3. Выберите hello `Save private key` кнопки.
   4. Пропустить hello предупреждение о защите hello ключ с помощью парольной фразы, а затем выберите `OK`.

   ![Снимок экрана генератора ключей PuTTY](./media/oracle-asm/puttykeygen.png)

4. В виртуальной машине выполните следующие команды:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Создайте файл с именем `authorized_keys`. Вставьте содержимое hello hello ключ в этом файле, а затем сохраните файл hello.

   > [!NOTE]
   > Hello ключ должен содержать строку hello `ssh-rsa`. Кроме того содержимое hello hello ключа должно быть одну строку текста.
   >  

6. В клиентской системе запустите PuTTY. В hello **категории** панели перейдите слишком**подключения** > **SSH** > **Auth**. В hello **файла закрытого ключа для проверки подлинности** поле, найдите toohello ключ, который был создан ранее.

   ![Снимок экрана параметров проверки подлинности SSH hello](./media/oracle-asm/setprivatekey.png)

7. В hello **категории** панели перейдите слишком**подключения** > **SSH** > **X11**. Выберите hello **включить X11 пересылку** флажок.

   ![Снимок экрана: hello SSH X11 параметры пересылки](./media/oracle-asm/enablex11.png)

8. В hello **категории** панели перейдите слишком**сеанса**. Введите ВМ ASM Oracle `<publicIPaddress>` hello имя диалоговом окне узла, заполните в новый `Saved Session` имя и нажмите кнопку на `Save`.  После сохранения щелкните `open` tooconnect tooyour Oracle ASM виртуальной машины.  Hello первом подключении вам предупреждение указывает на то что hello удаленной системе не кэшируются в реестре. Щелкните `yes` tooadd его и продолжить.

   ![Снимок экрана параметров сеанса PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Установка Oracle Grid Infrastructure

tooinstall инфраструктуры сетки Oracle, полный hello, следующие шаги:

1. Выполните вход в качестве пользователя **grid**. (Вы должны иметь доступ toosign в без необходимости вводить пароль.) 

   > [!NOTE]
   > Если вы используете Windows, убедитесь, что вы запустили Xming перед началом установки hello.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Откроется установщик Oracle Grid Infrastructure 12c Release 1. (Может занять несколько минут для hello установщика toostart.)

2. На hello **выберите вариант установки** выберите **Установка и Настройка инфраструктуры сетки Oracle для автономного сервера**.

   ![Снимок экрана со страницей выберите вариант установки установщика hello](./media/oracle-asm/install01.png)

3. На hello **выберите языки продукта** Убедитесь **английского** или выбран нужный язык hello.  Щелкните `next`.

4. На hello **создать группу дисков ASM** страницы:
   - Введите имя для группы дисков hello.
   - В разделе **Redundancy** (Избыточность) выберите **External** (Внешняя).
   - В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.
   - В разделе **Add Disks** (Добавление дисков) выберите **ORCLASMSP**.
   - Щелкните `next`.

5. На hello **укажите пароль ASM** страницу, выберите hello **использовать одинаковые пароли для этих учетных записей** и введите пароль.

   ![Снимок экрана со страницей укажите пароль ассемблерного кода hello установщика](./media/oracle-asm/install04.png)

6. На hello **Указание параметров управления** страницы, у вас есть tooconfigure hello параметр EM облака управления. Этот параметр будет пропущено - щелкните `next` toocontinue. 

7. На hello **привилегированных групп ОС** , используйте параметры по умолчанию hello. Нажмите кнопку `next` toocontinue.

8. На hello **укажите место установки** , используйте параметры по умолчанию hello. Нажмите кнопку `next` toocontinue.

9. На hello **создать инвентаризации** измените hello инвентаризации каталога слишком`/u01/app/grid/oraInventory`. Нажмите кнопку `next` toocontinue.

   ![Снимок экрана со страницей создать инвентаризации hello установщика](./media/oracle-asm/install08.png)

10. На hello **конфигурация выполнения сценария корневого** страницу, выберите hello **автоматически запускать скрипты настройки** флажок. Выберите hello **использовать учетные данные пользователя «root»** и введите пароль пользователя root hello.

    ![Снимок экрана установщика hello корневой сценария выполнения страницы "Конфигурация"](./media/oracle-asm/install09.png)

11. На hello **выполнения проверки готовности к установке** странице hello текущей настройки будут завершаться с ошибками. Это ожидаемое поведение. Выберите `Fix & Check Again`.

12. В hello **адресная привязка скрипта** диалоговое окно, нажмите кнопку `OK`.

13. На hello **Сводка** страницы, просмотрите выбранные параметры и нажмите кнопку `Install`.

    ![Снимок экрана: hello установщика страница «Сводка»](./media/oracle-asm/install12.png)

14. Диалоговое окно предупреждения отображается информирования сценариев настройки требуется toobe запуска от имени привилегированного пользователя. Нажмите кнопку `Yes` toocontinue.

15. На hello **Готово** щелкните `Close` toofinish hello установки.

## <a name="set-up-your-oracle-asm-installation"></a>Настройка установки Oracle ASM

tooset копирование установку Oracle ASM завершения hello, следующие шаги:

1. Убедитесь, что в сеансе X11 по-прежнему используется пользователь **grid**. Может потребоваться toohit `enter` toorevive hello терминалов. Затем запустите hello Oracle автоматическое хранилище управления помощник по настройке:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Откроется Oracle ASM Configuration Assistant.

2. В hello **Настройка ASM: группы дисков** диалогового окна выберите hello `Create` , а затем нажмите `Show Advanced Options`.

3. В hello **создать группу дисков** диалоговое окно:

   - Введите имя группы диска hello **данные**.
   - В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_DATA** и **ORCL_DATA1**.
   - В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.
   - Нажмите кнопку `ok` группы дисков toocreate hello.
   - Нажмите кнопку `ok` окно подтверждения tooclose hello.

   ![Снимок экрана диалогового окна создания группы дисков hello](./media/oracle-asm/asm02.png)

4. В hello **Настройка ASM: группы дисков** диалогового окна выберите hello `Create` , а затем нажмите `Show Advanced Options`.

5. В hello **создать группу дисков** диалоговое окно:

   - Введите имя группы диска hello **FRA**.
   - В разделе **Redundancy** (Избыточность) выберите **External (none)** (Внешняя(нет)).
   - В разделе **Select Member Disks** (Выбор дисков-участников) выберите **ORCL_FRA**.
   - В списке **Allocation Unit Size** (Размер единицы распределения) выберите значение **4**.
   - Нажмите кнопку `ok` группы дисков toocreate hello.
   - Нажмите кнопку `ok` окно подтверждения tooclose hello.

   ![Снимок экрана диалогового окна создания группы дисков hello](./media/oracle-asm/asm04.png)

6. Выберите **выхода** tooclose ASM Configuration Assistant.

   ![Снимок экрана: hello, настройте ASM: диалоговое окно группы дисков с кнопки выхода](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Создание базы данных hello

Hello программное обеспечение базы данных Oracle уже установлены на изображении hello Azure Marketplace. toocreate базы данных полный hello, следующие шаги:

1. Переключение пользователей toohello Oracle суперпользователя, а затем инициализируйте hello прослушивателя для ведения журнала:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Откроется Database Configuration Assistant.

2. На hello **операции базы данных** щелкните `Create Database`.

3. На hello **режимом создания** страницы:

   - Введите имя для базы данных hello.
   - Выберите **Automatic Storage Management (ASM)** в качестве **типа хранилища**.
   - Для **расположение файлов базы данных**, использовать значение по умолчанию hello ASM предложенные расположения.
   - Для **быстрого восстановления области**, использовать значение по умолчанию hello ASM предложенные расположения.
   - Введите **пароль администратора** и **подтвердите его**.
   - Убедитесь, что выбран параметр `create as container database`.
   - Введите значение `pluggable database name`.

4. На hello **Сводка** страницы, просмотрите выбранные параметры и нажмите кнопку `Finish` базы данных toocreate hello.

   ![Снимок экрана: hello страница «Сводка»](./media/oracle-asm/createdb03.png)

5. Hello базы данных был создан. На hello **Готово** предусмотрена hello параметр toouse toounlock дополнительные учетные записи этой базы данных и изменения паролей hello. Toodo так, выберите **управления паролями** -в противном случае щелкните `close`.

## <a name="delete-hello-vm"></a>Удалить hello виртуальной Машины

Автоматическое управление хранилищем для Oracle успешно настроена на изображении hello база данных Oracle из hello Azure Marketplace.  Если вам больше не требуется этой виртуальной Машины, можно использовать hello следующая команда tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

[Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux](configure-oracle-dataguard.md)

[Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux](Configure-oracle-golden-gate.md)

Ознакомьтесь со статьей [Разработка базы данных Oracle и ее внедрение в Azure](oracle-design.md)
