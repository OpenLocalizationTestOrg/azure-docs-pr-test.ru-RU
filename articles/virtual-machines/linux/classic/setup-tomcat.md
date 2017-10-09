---
title: "aaaSet копирование Apache Tomcat на виртуальной машине Linux | Документы Microsoft"
description: "Узнайте, как tooset копирование Apache Tomcat7 с помощью Azure виртуальных машин Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Настройка Tomcat7 на виртуальной машине Linux с использованием Azure
Apache Tomcat (или просто Tomcat, также называемая ранее Tomcat Джакарта) является открытым исходным кодом веб-сервера и контейнера сервлетов, разработанный hello Foundation программного обеспечения Apache ASF. Tomcat реализует hello сервлетов Java и спецификации JavaServer страниц (JSP) hello компании Sun Microsystems. Tomcat предоставляет чисто среде Java HTTP веб-сервера в какие toorun код Java. В простейшую конфигурацию hello Tomcat выполняется в процессе одной операционной системы. Этот процесс запускает виртуальную машину Java. Каждый запрос HTTP tooTomcat браузера обрабатывается как отдельный поток в процессе Tomcat hello.  

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../../../resource-manager-deployment-model.md). В этой статье рассказывается, как toouse hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов. toouse toodeploy шаблона диспетчера ресурсов Виртуальной машине Ubuntu с Open JDK и Tomcat, в разделе [в этой статье](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

В этой статье показано, как установить Tomcat7 в образе Linux и развернуть его в службе Azure.  

Вы узнаете:  

* Как toocreate виртуальную машину в Azure.
* Как tooprepare hello виртуальной машины для Tomcat7.
* Как tooinstall Tomcat7.

Предполагается, что у вас уже есть подписка Azure.  Если нет, можно зарегистрироваться для получения бесплатной пробной версии на [hello веб-сайте Azure](https://azure.microsoft.com/). Если у вас есть подписка MSDN, сведения о специальных ценах Microsoft Azure на MSDN, MPN и Bizspark см. на [этой странице](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn Дополнительные сведения о Azure, в разделе [что такое Azure?](https://azure.microsoft.com/overview/what-is-azure/).

В этой статье предполагается, что вы располагаете достаточными знаниями по работе с Tomcat и Linux.  

## <a name="phase-1-create-an-image"></a>Этап 1. Создание образа
На этом этапе вы создадите виртуальную машину с помощью образа Linux в Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Шаг 1. Создание ключа проверки подлинности SSH
SSH — это важный инструмент для системных администраторов. Однако для настройки безопасности доступа не рекомендуется использовать пароль, определенный пользователем. Злоумышленники могут взломать ненадежный пароль и проникнуть в вашу систему, использовав имя пользователя.

хорошие новости Hello является способом tooleave удаленного доступа откройте и не беспокоиться о пароли. Этот метод состоит в проверке подлинности с асимметричным шифрованием. Hello закрытого ключа пользователя — hello, который предоставляет hello проверки подлинности. Можно даже заблокировать учетную запись пользователя hello toonot разрешить проверку подлинности пароль.

Еще одним преимуществом использования этого метода является toosign разные пароли в toodifferent серверов не требуется. Вы можете проверять подлинность с помощью hello личных закрытый ключ на всех серверах, что позволяет избежать tooremember несколько паролей.



Выполните эти шаги ключ toogenerate hello SSH проверки подлинности.

1. Загрузите и установите PuTTYgen hello следующие расположения: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Запустите Puttygen.exe.
3. Нажмите кнопку **формирования** toogenerate hello ключей. В процессе hello можно увеличить случайности, движения мыши hello на пустую область hello в окне приветствия.  
   ![Кнопка нового ключа создания puTTY генератор ключа снимок экрана, показывающий hello][1]
4. После hello создать процесс, Puttygen.exe покажет нового открытого ключа.  
   ![PuTTY генератор ключа снимок экрана, показывающий новый открытый ключ hello "и" hello "Сохранить" закрытого ключа][2]
5. Выберите и скопируйте hello открытый ключ и сохранить его в файл с именем publicKey.pem. Не щелкайте **сохранить открытый ключ**, так как hello сохраненного формата файла открытого ключа, отличается от hello открытый ключ, нам нужно.
6. Нажмите кнопку **Save private key** (Сохранить закрытый ключ) и сохраните его в файл с именем privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Шаг 2: Создание образа hello в hello портал Azure
1. В hello [портала](https://portal.azure.com/), нажмите кнопку **New** в hello задач панели toocreate изображения. Выберите образ hello Linux, в зависимости от потребностей. Hello следующем примере hello Ubuntu 14.04 изображения.
![Снимок экрана: hello портал, который показывает hello новая кнопка][3]

2. Для **имя узла**, укажите имя hello hello URL-адрес, Интернет-клиенты будут использовать и tooaccess этой виртуальной машины. Определите последнюю часть hello DNS-имя, например, tomcatdemo hello. Azure затем создаст hello URL-адрес, что tomcatdemo.cloudapp.net.  

3. Для **ключ SSH проверки подлинности**, скопируйте значение ключа hello из hello publicKey.pem файл, содержащий открытый ключ hello созданные PuTTYgen.  
![Введите ключ проверки подлинности SSH в портале hello][4]

4. При необходимости настройте другие параметры и нажмите кнопку **Создать**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Этап 2. Подготовка виртуальной машины для Tomcat7
На этом этапе будет настроить конечную точку для трафика Tomcat и подключитесь tooyour новой виртуальной машины.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Шаг 1: Откройте hello HTTP порт tooallow web access
Конечные точки в Azure состоят из протокола (TCP или UDP), а также общего и частного порта. частный порт Hello — порт hello, что hello служба ожидает tooon hello виртуальной машины. Общий порт Hello — tooexternally для входящего трафика на Интернет-прослушивает порт hello, hello Azure облачной службы.  

TCP-порт 8080 — номер порта по умолчанию hello, что Tomcat использует toolisten. Открытие этого порта с помощью конечной точки Azure обеспечивает вам и другим интернет-клиентам доступ к страницам Tomcat.  

1. На портале hello щелкните **Обзор** > **виртуальные машины**и нажмите кнопку hello виртуальную машину, созданную.  
   ![Снимок экрана: hello каталог виртуальные машины][5]
2. tooadd конечная точка tooyour виртуальной машине, щелкните hello **конечные точки** поле.
   ![Снимок экрана, показывающий поля hello конечных точек][6]
3. Щелкните **Добавить**.  

   1. Для конечной точки hello, введите имя для конечной точки hello в **конечной точки**, а затем введите 80 в **общий порт**.  

      Если задано too80, нет необходимости номер порта tooinclude hello в hello URL-адрес, используемый tooaccess Tomcat. Например, http://tomcatdemo.cloudapp.net.    

      Если задать значение tooanother, например 81, необходимо tooadd hello порт номер toohello URL-адрес tooaccess Tomcat. Например, http://tomcatdemo.cloudapp.net:81/.
   2. Введите 8080 в поле **Частный порт**. По умолчанию Tomcat прослушивает TCP-порт 8080. Если вы изменили hello по умолчанию прослушивания порта Tomcat, необходимо обновить **частный порт** toobe hello так же, как hello порт прослушивания Tomcat.  
      ![Снимок экрана пользовательского интерфейса, где отображается команда "Добавить" и поля "Общий порт" и "Частный порт"][7]
4. Нажмите кнопку **ОК** tooadd hello конечной точки tooyour виртуальной машины.

### <a name="step-2-connect-toohello-image-you-created"></a>Шаг 2: Подключение toohello образ, созданный
Можно выбрать любой SSH средство tooconnect tooyour виртуальной машины. В этом примере мы используем средство PuTTY.  

1. Получите hello DNS-имя виртуальной машины из портала hello.
    1. Щелкните **Обзор** > **Виртуальные машины**.
    2. Выберите имя hello виртуальной машины и нажмите кнопку **свойства**.
    3. В hello **свойства** плитки, поиск в hello **доменное имя** поле tooget hello DNS-имя.  

2. Получить номер порта hello для соединений по протоколу SSH с hello **SSH** поле.  
![Снимок экрана, показывающий номер порта для подключения SSH hello][8]

3. Скачайте [PuTTY](http://www.putty.org/).  

4. После загрузки запустите исполняемый файл hello Putty.exe. В PuTTY конфигурации настроить основные параметры hello hello имя узла и порта номер, полученный из свойства hello виртуальной машины.   
![Снимок экрана, показывающий параметры имя и порт hello PuTTY конфигурации узла][9]

5. Hello левой панели щелкните **подключения** > **SSH** > **Auth**, а затем нажмите кнопку **Обзор** toospecify расположение файла privateKey.ppk hello Hello. файл privateKey.ppk Hello содержит hello закрытый ключ, созданный ранее в hello PuTTYgen «этап 1: Создание образа» этой статьи.  
![Снимок экрана, показывающий иерархии каталогов подключения hello и кнопку обзора][10]

6. Щелкните **Открыть**. Может отобразиться оповещение в окне сообщения. Если вы настроили hello DNS-имя и номер порта правильно, нажмите кнопку **Да**.
![Снимок экрана, показывающий hello уведомления][11]

7. Вы являются запрашиваемые tooenter свое имя пользователя.  
![Снимок экрана, показывающий, где имя пользователя tooenter][12]

8. Введите имя пользователя hello, которое вы использовали toocreate hello виртуальной машины в hello «этап 1: Создание образа» ранее в этой статье. Вы увидите примерно hello следующим образом:  
![Снимок экрана, показывающий подтверждения подлинности hello][13]

## <a name="phase-3-install-software"></a>Этап 3. Установка программного обеспечения
На этом этапе установки среды выполнения Java hello, Tomcat7 и других компонентов Tomcat7.  

### <a name="java-runtime-environment"></a>Среда выполнения Java
Программное обеспечение Tomcat написано на языке Java. Есть два вида комплектов Java Development Kit (JDK) — OpenJDK и Oracle JDK. Можно выбрать необходимый hello.  

> [!NOTE]
> Оба пакетов JDK имеют практически hello же код для классов hello в hello Java API, но код hello для hello виртуальной машины отличается. OpenJDK, как правило, открытые библиотеки toouse, пока Oracle JDK, как правило, toouse закрыто историй. В Oracle JDK доступно больше классов и в нем исправлены некоторые ошибки. К тому же Oracle JDK работает стабильнее, чем OpenJDK.

#### <a name="install-openjdk"></a>Установка OpenJDK  

Используйте следующие команды toodownload OpenJDK hello.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate directory toocontain hello JDK файлов:  

        sudo mkdir /usr/lib/jvm  
* файлы JDK tooextract hello в hello/usr/lib/виртуальной машины Java/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Установка Oracle JDK


Используйте следующую команду toodownload Oracle JDK из веб-сайте Oracle hello hello.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate directory toocontain hello JDK файлов:  

        sudo mkdir /usr/lib/jvm  
* файлы JDK tooextract hello в hello/usr/lib/виртуальной машины Java/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset JDK Oracle как hello виртуальной машины Java по умолчанию:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Убедитесь, что установка Java выполнена успешно.
Можно использовать такую команду hello следующие tootest, если среда выполнения Java hello установлена правильно:  

    java -version  

Если вы установили OpenJDK, вы увидите сообщение hello следующим образом: ![сообщения OpenJDK успешной установки][14]

Если вы установили Oracle JDK, вы увидите сообщение hello следующим образом: ![сообщения установки успешно JDK Oracle][15]

### <a name="install-tomcat7"></a>Установка Tomcat7
Используйте следующие команды tooinstall Tomcat7 hello.  

    sudo apt-get install tomcat7  

Если вы не используете Tomcat7, используйте аналогичную hello этой команды.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Убедитесь, что Tomcat7 успешно установлен.
toocheck после успешной установки Tomcat7 Обзор сервера Tomcat tooyour DNS-имя. В этой статье пример hello URL-адреса — http://tomcatexample.cloudapp.net/. Если появится сообщение следующего вида hello, Tomcat7 установлена правильно.
![Сообщение об успешной установке Tomcat7][16]

### <a name="install-other-tomcat7-components"></a>Установка других компонентов Tomcat7
Существуют другие дополнительные компоненты Tomcat, которые вы можете установить.  

Используйте hello **tomcat7 поиска apt кэша sudo** команда toosee все доступные компоненты hello. Используйте следующие команды tooinstall hello некоторые полезные компоненты.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Этап 4. Настройка Tomcat7
На этом этапе вы узнаете о том, как управлять Tomcat.

### <a name="start-and-stop-tomcat7"></a>Запуск и остановка Tomcat7
сервер Tomcat7 Hello запускается автоматически при установке. Можно также запустить с hello следующую команду:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

состояние hello tooview Tomcat7:

    sudo /etc/init.d/tomcat7 status

службы toorestart Tomcat: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Администрирование Tomcat7
Можно изменить файл конфигурации tooset для hello Tomcat пользователя копирование свои учетные данные администратора. Hello используйте следующую команду:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Пример:  
![Снимок экрана, показывающий выходные данные команды vi sudo hello][17]  

> [!NOTE]
> Создайте надежный пароль для пользователя с правами администратора hello.  

После изменения этого файла, следует перезапустить службы Tomcat7 с hello, следующая команда tooensure, что hello изменения вступили в силу:  

    sudo /etc/init.d/tomcat7 restart  

Откройте браузер и введите **http://<your tomcat server DNS name>html-manager/** как hello URL-адрес. Например hello в этой статье hello URL-адрес является http://tomcatexample.cloudapp.net/manager/html.  

После подключения вы увидите нечто похожее toohello следующее:  
![Снимок экрана: hello Диспетчер приложений Tomcat Web][18]

## <a name="common-issues"></a>Распространенные проблемы
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Hello виртуальную машину с Tomcat и Moodle нельзя получить доступ из Интернета hello
#### <a name="symptom"></a>Симптом  
  Tomcat выполняется, но не отображается страница по умолчанию hello Tomcat с браузером.
#### <a name="possible-root-cause"></a>Возможная основная причина   

  * порт прослушивания Tomcat Hello не является hello аналогично hello частный порт конечной точки виртуальной машины для трафика Tomcat.  

     Порт прослушивания проверьте общий порт и частного порта параметры конечной точки и убедитесь, частный порт hello Здравствуйте, так же, как hello Tomcat. Дополнительные инструкции по настройке конечных точек см. в разделе "Этап 1. Создание образа" этой статьи.  

     toodetermine hello Tomcat порт прослушивания, откройте /etc/httpd/conf/httpd.conf (Red Hat выпуск) или /etc/tomcat7/server.xml (Debian выпуск). По умолчанию hello порт прослушивания Tomcat — 8080. Пример:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     При использовании виртуальной машины, как Debian и Ubuntu и вы хотите toochange hello по умолчанию порт из Tomcat ожидания передачи данных (например 8081), также следует открыть порт hello для hello операционной системы. Во-первых откройте hello профиля:  

        sudo vi /etc/default/tomcat7  

     Затем удалите комментарий последнюю строку hello и измените «no» слишком «Да».  

        AUTHBIND=yes
  2. брандмауэр Hello отключил прослушивания hello порт Tomcat.

     Только вы увидите страницу по умолчанию hello Tomcat из локального узла hello. проблема Hello, скорее всего, hello порт, который является прослушиваемом tooby Tomcat, заблокирован брандмауэром hello. Можно использовать веб-страницу приветствия w3m средство toobrowse hello. Hello следующие команды установки w3m и перейдите на страницу по умолчанию Tomcat toohello:  


        sudo yum  install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>Решение

  * Если порт прослушивания Tomcat hello не является hello таким же как частный порт hello hello конечной точки для виртуальной машины toohello трафика, необходимо изменить частный порт hello toobe hello так же, как hello порт прослушивания Tomcat.   
  2. Если hello проблема вызвана брандмауэра или утилита iptables, добавьте следующие строки слишком/д/sysconfig/утилита iptables hello. Вторая строка Hello требуется только для трафика https:  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > Убедитесь, что hello предыдущих строк позиционируются над все строки, глобально ограничит доступа, например hello следующее: -j ОТКЛОНИТЬ--отклонить-с помощью запрета сервера icmp - ввод



Утилита iptables tooreload hello, запустите hello следующую команду:

    service iptables restart

Протестировано в CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Отказано в разрешении при загрузке проекта файлы слишком/var/lib/tomcat7/веб-приложений и
#### <a name="symptom"></a>Симптом
  При использовании SFTP клиента (например, FileZilla) tooconnect tooyour виртуальной машине и перейдите слишком/var/lib/tomcat7/веб-приложений и toopublish веб-сайта, вы получаете ошибки сообщения аналогичные toohello следующее:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Возможная основная причина
  У вас нет разрешения tooaccess hello /var/lib/tomcat7/webapps папки.  
#### <a name="solution"></a>Решение  
  Требуется разрешение tooget из учетной записи root hello. Можно изменить владельца hello этой папке от корневого имени пользователя toohello, используемые при подготовке компьютера hello. Ниже приведен пример hello azureuser учетной записи:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Используйте hello -R параметр tooapply hello разрешения для всех файлов в каталоге.  

  Эта команда также работает для каталогов. изменения параметров Hello -R hello разрешения для всех файлов и каталогов в каталоге hello. Пример:  

     sudo chown -R username:group directory  

  Эта команда изменяет владельца (пользователей и групп) для всех файлов и папок, вложенных в каталог hello.  

  Hello следующая команда изменяет только разрешение hello hello папки каталога. Hello файлы и папки в каталоге hello не изменяются.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
