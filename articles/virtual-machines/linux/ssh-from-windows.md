---
title: "ключи aaaUse SSH с Windows для виртуальных машин Linux | Документы Microsoft"
description: "Узнайте, как ключи toogenerate и использование SSH на компьютере tooconnect tooa Linux виртуальной машине в Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Как tooUse SSH ключей с Windows в Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux или Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

При подключении tooLinux виртуальных машин (ВМ) в Azure, следует использовать [шифровании с открытым ключом](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide более безопасный способ toolog в tooyour виртуальной Машины с Linux. Этот процесс включает открытые и закрытые обмен ключами с помощью команды tooauthenticate hello безопасного shell (SSH) самостоятельно вместо имени пользователя и пароля. Пароли являются уязвимыми toobrute атаки, особенно на виртуальных машинах с выходом в Интернет, например веб-серверов. В этой статье общие ключи SSH, и как toogenerate hello соответствующих ключей на компьютере Windows.

## <a name="overview-of-ssh-and-keys"></a>Общие сведения о SSH и ключах
Вы можете безопасно войти tooyour виртуальных Машин Linux с помощью открытого и закрытого ключей:

* Hello **открытый ключ** помещается на ВМ Linux или любой другой службы, что вы хотите toouse с открытым ключом.
* Hello **закрытый ключ** — теми, которые присутствуют tooyour виртуальной Машины Linux при входе в tooverify вашу личность. Его нужно защищать и нельзя никому предоставлять.

Открытые и закрытые ключи можно использовать на нескольких виртуальных машинах или в нескольких службах. Пары ключей для каждой виртуальной Машины или службы, которые вы хотите tooaccess необязательно. Дополнительные сведения о шифровании с открытым ключом см. [здесь](https://wikipedia.org/wiki/Public-key_cryptography).

SSH — это протокол зашифрованного подключения, позволяющий безопасно входить в систему через незащищенные соединения. Это hello протокола связи по умолчанию для виртуальных машин Linux, размещенные в Azure. Несмотря на то, что сам SSH обеспечивает зашифрованное соединение, с помощью паролей с соединений по протоколу SSH по-прежнему оставляет hello ВМ уязвимым toobrute атаки или взлома паролей. Повышение безопасности и предпочтительный метод подключения tooa виртуальную Машину с помощью SSH — с помощью этих открытых и закрытых ключей, также известные как ключи SSH.

Если вы не toouse ключи SSH, вы можете по-прежнему войти tooyour виртуальных машин Linux с помощью пароля. Если ВМ не предоставляется toohello Интернета, использование паролей может быть достаточно. Тем не менее вы по-прежнему требуется toomanage пароли для каждой виртуальной Машины Linux и обслуживания политики работоспособности паролей и рекомендации, такие как минимальная длина пароля и регулярно выполняется их обновление. Hello использование ключей SSH снижает сложность hello управление отдельными учетными данными между несколькими виртуальными машинами.

## <a name="windows-packages-and-ssh-clients"></a>Пакеты Windows и SSH-клиенты
Подключение tooand управление виртуальными машинами Linux в Azure с помощью **клиент SSH**. Но на компьютерах Windows, как правило, SSH-клиент не установлен. Hello Юбилейного обновления Windows 10 добавлен Bash для Windows, и hello последнее обновление создатели 10 Windows предоставляет дополнительные обновления. Этой подсистемы Windows для Linux можно toorun и доступ таких служебных программ, клиент SSH в собственном коде в командной оболочке Bash. После этого можно отследить все документы Linux hello, таких как [созданием пар toogenerate SSH-ключ для Linux](mac-create-ssh-keys.md). Bash для Windows находится на стадии разработки, и сейчас доступен бета-выпуск. Дополнительные сведения о Bash для Windows см. в записи блога [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about) (Bash для Ubuntu в Windows).

При желании toouse что-то отличное от Bash Windows общих Windows SSH клиентов, которое можно установить, включаются в hello следующие пакеты:

* [Git для Windows](https://git-for-windows.github.io/);
* [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/);
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Который ключевых файлов необходимо toocreate?
В Azure необходимо использовать по крайней 2048-разрядные открытые и закрытые ключи в формате **ssh-rsa**. Если вы управляете ресурсы Azure с помощью hello классической модели развертывания, необходимо также toogenerate PEM (`.pem` файла).

Ниже приведены сценарии развертывания hello и типы файлов, используемых в каждом hello.

1. **SSH-rsa** требуются ключи для любого развертывания с помощью hello [портал Azure](https://portal.azure.com)и развертывания диспетчера ресурсов, с помощью hello [Azure CLI](../../cli-install-nodejs.md).
   * Обычно эти ключи нужны большинству пользователей.
2. Объект `.pem` файл является toocreate необходимые виртуальные машины, использующие hello классического развертывания. Эти ключи поддерживаются в классическом развертывании при использовании hello [портал Azure](https://portal.azure.com) или [Azure CLI](../../cli-install-nodejs.md).
   * Требуется только toocreate эти дополнительные ключи и сертификаты при управлении ресурсы, созданные с помощью hello классической модели развертывания.

## <a name="install-git-for-windows"></a>Установка Git для Windows
Hello предыдущего раздела в списке несколько пакетов, которые включают hello `openssl` средство для Windows. Это средство можно необходимые toocreate открытый и закрытый ключи. Здравствуйте, следующие примеры сведений, как tooinstall и использовать **Git для Windows**, хотя можно выбрать любой пакет, который вы предпочитаете. **Git для Windows** предоставляет вам доступ toosome дополнительное программное обеспечение с открытым исходным кодом ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) средств и служебных программ, которые могут быть полезны при работе с виртуальными машинами Linux.

1. Загрузите и установите **Git для Windows** из hello следующие расположения: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Примите параметры по умолчанию hello во время hello процесс установки, если вам не нужна toochange их.
3. Запустите **Git Bash** из hello **меню "Пуск"** > **Git** > **Git Bash**. консоль Hello выглядит примерно toohello в следующем примере:

    ![Оболочка Bash Git для Windows](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Создание закрытого ключа
1. В вашей **Git Bash** окна, используйте `openssl.exe` toocreate закрытый ключ. Hello следующий пример создает раздел с именем `myPrivateKey` и сертификат с именем `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    Hello выходные данные выглядят аналогично toohello в следующем примере:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Если bash сообщает об ошибке, попробуйте открыть новое окно **Git Bash** с повышенными привилегиями. Перезапустите hello `openssl` команды.

2. Hello ответов запрашивает название страны, расположение, название организации, и т. д.
3. Новый закрытый ключ и сертификат будут созданы в текущей рабочей папке. Из соображений безопасности необходимо задать разрешения hello на ваш закрытый ключ, чтобы только вы имели доступ:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Hello [разделу](#create-a-private-key-for-putty) сведения с помощью PuTTYgen tooboth просмотреть и использовать открытый ключ hello и создавать специальные PuTTY tooSSH tooLinux виртуальных машин с помощью закрытого ключа. Hello следующая команда создает файл открытого ключа с именем `myPublicKey.key` , который можно использовать сразу:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Если необходимо также toomanage классический ресурсы преобразовать hello `myCert.pem` слишком`myCert.cer` (в кодировке DER X509 сертификата). Это действие необязательно только в том случае, если вам требуется toospecifically управления ресурсами старые классическом.

    Преобразуйте hello сертификат, с помощью hello следующую команду:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Создание закрытого ключа для PuTTY
PuTTY — это общераспространенный SSH-клиент для Windows. Вы являются свободного toouse любой клиент SSH, по которой необходима. toouse PuTTY необходимо toocreate еще один тип ключа - PuTTY закрытый ключ (PPK). Если вы не готовы toouse PuTTY, пропустите этот раздел.

Hello примере ниже создается специально для PuTTY toouse дополнительных закрытый ключ.

1. Используйте **Git Bash** tooconvert ваш закрытый ключ закрытый ключ RSA понятно, что PuTTYgen. Hello следующий пример создает раздел с именем `myPrivateKey_rsa` из hello существующий ключ с именем `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Из соображений безопасности необходимо задать разрешения hello на ваш закрытый ключ, чтобы только вы имели доступ:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Загрузите и запустите PuTTYgen из hello следующие расположения: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Щелкните меню hello: **файл** > **загрузки закрытого ключа**
4. Найдите закрытый ключ (`myPrivateKey_rsa` в предыдущем примере hello). каталог по умолчанию Hello при запуске **Git Bash** — `C:\Users\%username%`. Изменить фильтр tooshow hello файл **все файлы (\*.\*)** :

    ![Загрузка PuTTYgen hello существующий закрытый ключ](./media/ssh-from-windows/load-private-key.png)
5. Щелкните **Открыть**. Запрос указывает, что разделу hello успешно импортировано:

    ![Успешно импортировано tooPuTTYgen ключа](./media/ssh-from-windows/successfully-imported-key.png)
6. Нажмите кнопку **ОК** tooclose hello строки.
7. открытый ключ Hello отображается вверху hello hello **PuTTYgen** окна. Скопируйте и вставьте этот открытый ключ в hello портал Azure или шаблона диспетчера ресурсов Azure, при создании виртуальной Машины Linux. Можно также щелкнуть **сохранить открытый ключ** toosave компьютер tooyour копирования:

    ![Сохранение файла PuTTY с открытым ключом](./media/ssh-from-windows/save-public-key.png)

    Hello следующем примере показано, как бы скопировать и вставить этот открытый ключ в hello портал Azure, при создании виртуальной Машины Linux. открытый ключ Hello обычно сохраняется в `~/.ssh/authorized_keys` на новой виртуальной Машины.

    ![Использовать открытый ключ при создании виртуальной Машины в hello портал Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Вернитесь к **PuTTYgen** и нажмите кнопку **Save private Key** (Сохранить закрытый ключ):

    ![Сохранение файла PuTTY с закрытым ключом](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Появится запрос, если вы хотите toocontinue без ввода парольную фразу для ключа. Парольная фраза аналогично вложенного tooyour пароль закрытого ключа. Даже если кто-то было tooobtain ваш закрытый ключ, они по-прежнему не будет возможности tooauthenticate, используя только ключ hello. Они также требуется парольная фраза hello. Без парольную фразу Если кто-то получает свой закрытый ключ, они войдите в tooany виртуальной Машины или службы, использующий этот ключ. Мы рекомендуем создать ее. Однако если вы забудете парольную фразу hello, нет не toorecover способом его.
   >
   >

    Tooenter парольную фразу, нажмите кнопку **нет**, введите парольную фразу в главном окне PuTTYgen hello и нажмите кнопку **Сохранить закрытый ключ** еще раз. В противном случае нажмите кнопку **Да** toocontinue без предоставления необязательно hello парольную фразу.
9. Введите имя и расположение toosave PPK файл.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Использовать Putty tooSSH tooa компьютер Linux
Отметим еще раз, PuTTY — это общераспространенный SSH-клиент для Windows. Вы являются свободного toouse любой клиент SSH, по которой необходима. Здравствуйте, как следующие шаги подробно toouse вашего закрытого ключа tooauthenticate с ВМ Azure с помощью SSH. Hello шаги похожи на другие ключа SSH-клиенты с точки зрения необходимости tooload вашей hello tooauthenticate закрытого ключа SSH-подключения.

1. Здравствуйте, загрузки и выполнения putty из следующие расположения: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Заполните hello имя узла или IP-адрес виртуальной Машины из портала Azure hello.

    ![Открытие нового подключения PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Прежде чем нажать **Open** (Открыть) щелкните узел **Connection** (Подключение)  > **SSH** > вкладка **Auth** (Проверка подлинности). Обзор tooand выберите ваш закрытый ключ.

    ![Выбор закрытого ключа PuTTY для проверки подлинности](./media/ssh-from-windows/putty-auth-dialog.png)
4. Нажмите кнопку **откройте** tooconnect tooyour виртуальной машины

## <a name="next-steps"></a>Дальнейшие действия
Также можно создать открытый и закрытый ключи hello [с помощью OS X и Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Дополнительные сведения о Bash для Windows и hello преимущества готовые средства операционные системы на компьютере Windows см. в разделе [Bash на Ubuntu на Windows](https://msdn.microsoft.com/commandline/wsl/about).

Если возникли проблемы с помощью SSH tooconnect tooyour виртуальных машин Linux, см. раздел [Устранение SSH подключений tooan виртуальной Машине Linux Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
