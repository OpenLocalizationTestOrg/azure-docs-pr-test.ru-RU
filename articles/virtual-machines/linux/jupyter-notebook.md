---
title: "aaaCreate книжки Jupyter и IPython | Документы Microsoft"
description: "Дополнительные сведения, способ создания toodeploy hello записной книжки Jupyter и IPython на виртуальной машине Linux с помощью модели развертывания диспетчера ресурсов hello в Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Создание виртуальной машины Azure, установка Jupyter и запуск Jupyter Notebook в Azure
Hello [проекта Jupyter](http://jupyter.org), ранее hello [IPython проекта](http://ipython.org), предоставляет набор средств для научных вычислений с помощью мощных интерактивный оболочек, объединяющие выполнения кода с помощью создания hello Динамическая вычислительных документа. Эти файлы записной книжки могут содержать произвольный текст, математические формулы, код ввода, результаты, графику, видео и любые другие виды носителей, которые может отображать современный веб-браузер. Вы будете абсолютно новый tooPython и требуется toolearn его в fun, интерактивную среду или выполните некоторые серьезные параллельного или технической вычислений, hello книжке Jupyter очень удобно.

![Снимок экрана](./media/jupyter-notebook/ipy-notebook-spectral.png) с помощью SciPy и Matplotlib пакетов tooanalyze hello структуры запись звука.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Два способа реализации Jupyter: Azure Notebook или пользовательское развертывание
Azure предоставляет службу, можно использовать слишком[быстро начать использовать Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  С помощью hello записной книжки службы Azure, можно легко получить tooJupyter доступ веб-интерфейса для масштабируемый вычислительные ресурсы со всех hello возможности Python и его многие библиотеки.  С момента установки hello обрабатывается службой hello, пользователи могут доступа к этим ресурсам без необходимости hello администрирования и настройки пользователем hello.

Если служба записной книжки hello не работает для вашего сценария продолжайте tooread в этой статье, который будет будет показано, как toodeploy hello книжке Jupyter на базе Microsoft Azure с помощью Linux виртуальных машин (ВМ).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Создание и настройка виртуальной машины в Azure
Hello первым шагом является toocreate виртуальной машины (VM), работающей в Azure.
Эта виртуальная машина является всей операционной системы в облаке hello и будет использоваться для запуска hello книжке Jupyter. Способен работающих виртуальных машин Linux и Windows Azure, и мы рассмотрим hello установки Jupyter и другие виртуальные машины.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Создание виртуальной Машины Linux и открытие порта для Jupyter
Следуйте инструкциям hello [здесь] [ portal-vm-linux] toocreate виртуальной машины из hello *Ubuntu* распространения. В этом учебнике используется Ubuntu Server 14.04 LTS. Предположим, имя пользователя hello *azureuser*.

После развертывает hello виртуальной машины необходимо tooopen правило безопасности для групп безопасности сети hello.  С hello портал Azure, откройте слишком**сетевых групп безопасности** и Привет открыть вкладку tooyour соответствующей группы безопасности hello виртуальной Машины. Требуется tooadd правило безопасности для входящего трафика с hello следующие параметры: **TCP** для протокола hello  **\***  для hello порт источника (public) и **9999** для порт назначения (private) Hello.

![Снимок экрана](./media/jupyter-notebook/azure-add-endpoint.png)

В группе безопасности сети, нажмите кнопку **сетевых интерфейсов** и Примечание hello **общедоступный IP-адрес** как необходимые tooconnect tooyour ВМ будет находиться в следующем шаге hello.

## <a name="install-required-software-on-hello-vm"></a>Установите необходимое программное обеспечение на hello виртуальной Машины
toorun Здравствуйте записной книжки Jupyter на нашем виртуальной Машины, нам необходимо сначала установить Jupyter и его зависимости. Подключите tooyour виртуальных машин linux с помощью ssh и hello пары имя пользователя и пароль, выбранный при создании hello виртуальной машины. В этом учебнике используется PuTTY и подключение из Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Установка Jupyter на Ubuntu
Установите распространения python обработки и анализа данных популярных, Anaconda, с помощью одного из hello ссылки из [компания Continuum Analytics](https://www.continuum.io/downloads).  На момент написания данного документа hello, hello следующие ссылки являются hello наиболее вверх toodate версии.

#### <a name="anaconda-installs-for-linux"></a>Дистрибутивы Anaconda для Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2,7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64-разрядная</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32-разрядная</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Установка 64-разрядной версии Anaconda 3 2.3.0 на Ubuntu
Приведем пример установки Anaconda на Ubuntu:

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Снимок экрана](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Настройка Jupyter и использование протокола SSL
После установки нужно tootake файлы конфигурации момент hello toosetup для Jupyter. Если возникают проблемы с настройкой Jupyter часто бывает полезно toolook на hello [сервер записной книжки Jupyter документации](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Далее мы `cd` toohello профиль directory toocreate нашей SSL-сертификат и изменить файл конфигурации профилей hello.

В Linux используйте следующую команду hello.

    cd ~/.jupyter

Используйте hello, следующая команда toocreate hello SSL-сертификат (Linux и Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Обратите внимание, что создания самозаверяющего сертификата SSL, при подключении записной книжки toohello браузере выдаст предупреждение системы безопасности.  Для долгосрочного применения в рабочей среде может потребоваться toouse должным образом подписанный сертификат, связанный с вашей организацией.  Так как сертификат управления выходит за область действия этой демонстрации hello, мы будем придерживаться tooa самозаверяющий сертификат сейчас.

В дополнение к этому toousing сертификат, необходимо также указать tooprotect пароль портативного компьютера от несанкционированного использования.  По соображениям безопасности Jupyter используется зашифрованные пароли в файле конфигурации, поэтому вам понадобится tooencrypt пароль сначала.  IPython предоставляет toodo программы. в командной строке выполните следующую команду hello.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Это предложит ввести пароль и подтверждение, а затем будет напечатать пароль hello. Запомнить, что даст hello.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Далее мы внесем изменения файла конфигурации hello профиля, который имеет `jupyter_notebook_config.py` в каталоге hello в файл.  Обратите внимание, что этот файл не существует — просто создать противном случае hello.  Этот файл содержит несколько полей, которые по умолчанию закомментированы.  Этот файл можно открыть в любом текстовом редакторе из желанию и следует убедиться, что он имеет по крайней мере Здравствуйте, после содержимого. **Быть убедиться, что c.NotebookApp.password tooreplace hello в hello конфигурации с помощью sha1 hello из предыдущего шага hello**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Запустите hello книжке Jupyter
На этом этапе не готов toostart hello книжке Jupyter. toodo это, перейдите в каталог toohello toostore записных книжек и начать hello server книжке Jupyter с hello следующую команду.

    /anaconda3/bin/jupyter-notebook

Теперь должна быть блокнота Jupyter по адресу hello может tooaccess `https://[PUBLIC-IP-ADDRESS]:9999`.

При первом обращении к записной страницы входа hello запрашивает пароль. И после входа, вы увидите «Мониторинга записной книжки Jupyter,» hello которого является центр непечатаемые для всех операций в записной книжке.  На этой странице можно создать новые записные книжки и открывать существующие:

![Снимок экрана](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>С помощью hello книжке Jupyter
Если щелкнуть hello **New** кнопки, вы увидите после открытия страницы приветствия.

![Снимок экрана](./media/jupyter-notebook/jupyter-untitled-notebook.png)

область Hello, отмеченные `In []:` является область ввода hello и здесь можно ввести любой допустимый код Python, и он будет выполняться при достижении `Shift-Enter` или щелкните значок «Play» hello (hello указывающий направо треугольник в hello инструментов).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Мощная парадигма: документы с вычислениями в режиме реального времени и богатыми возможностями мультимедиа
ноутбук Hello сам должно быть очень естественный tooanyone, который использовал Python и текстовые редакторы, так как он находится в некотором смысле их комбинацию: могут выполняться блоков кода Python, но могут также содержать заметки и другой текст, изменив слишком стиль hello в ячейке «Code» «Ma rkdown» с помощью hello раскрывающееся меню в панели инструментов.

Но это гораздо больше, чем текстовый процессор, так как Jupyter позволяет совмещать вычисления и широкие возможности мультимедиа (текст, графику, видео и практически любые данные, которые способен отображать современный браузер). Вы можете комбинировать текст, код, видео и многое другое!

![Снимок экрана](./media/jupyter-notebook/jupyter-editing-experience.png)

И мощность hello многие отлично библиотеки Python для научных и технических вычислений, в следующий снимок экрана, hello простых вычислений могут быть выполнены с hello облегчают же, как анализ сложную сеть, все в одной среде.

Это парадигма совпадением power hello современных веб-hello и динамической вычисление предлагает множество возможностей и идеально подходит для облака hello. можно использовать Hello записной книжки:

* Вычислительные пометок toorecord произвольного вместе на неполадки.
* tooshare результаты с коллегами в форме «live» вычислений или Бумажная копия форматов (HTML, PDF).
* toodistribute и присутствует динамической преподавателя материалов, которые включать в себя вычисления, поэтому учащихся немедленно можно поэкспериментировать с кодом реальных hello, измените его и повторно выполните ее интерактивном режиме.
* tooprovide «исполняемый документы», предоставляющие hello результаты запроса в виде, можно немедленно воспроизвести, проверки и расширены за счет других.
* Как платформу для совместной работы: несколько пользователи могут входить в toothe же записной книжки server tooshare динамической вычислительных сеанс.

При переходе в исходном коде toohello IPython [репозитория][repository], вы найдете весь каталог с примерами ноутбук, которых можно загрузить и затем поэкспериментировать с на виртуальной Машине Jupyter собственные Azure.  Просто загрузите hello `.ipynb` файлы из hello сайта и передать их в панель мониторинга hello записной виртуальной Машины Azure (или загрузить их непосредственно в hello виртуальной Машины).

## <a name="conclusion"></a>Заключение
Hello книжке Jupyter предоставляет мощный интерфейс для доступа к интерактивно power hello hello экосистемы Python в Azure.  Он охватывает широкий диапазон вариантов использования, включая простой просмотр и изучения Python, анализ данных и визуализацию, моделирование и параллельные вычисления. Hello итоговые записной книжки документы содержат полную запись hello вычислений, которые выполняются, а также можно использовать совместно с другими пользователями Jupyter.  Hello книжке Jupyter можно использовать в качестве локального приложения, но идеально подходит для развертывания в облаке в Azure

Основные функции Hello Jupyter также доступны в Visual Studio через [средства Python для Visual Studio] [ Python Tools for Visual Studio] (PTVS). PTVS является бесплатным подключаемым модулем с открытым кодом от корпорации Майкрософт, который превращает Visual Studio в среду разработки Python с расширенными возможностями, включающую редактор с интеграцией IntelliSense, средств отладки, профилирования и параллельных вычислений.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
