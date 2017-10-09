---
title: "кластер tooan aaaSubmit заданий HPC Pack в Azure | Документы Microsoft"
description: "Узнайте, как tooset копию на локальном компьютере toosubmit заданий tooan кластера HPC Pack в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Отправка заданий HPC из кластера HPC Pack tooan компьютера в локальной среде, развернутой в Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Настройка задания локального компьютера клиента toosubmit tooa [пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029) кластера в Azure. В этой статье показано, как tooset настроить локальный компьютер с клиентом средств toosubmit задания через HTTPS toohello кластера в Azure. Таким образом, несколько пользователей кластера можно отправить задания tooa облачного пакета HPC кластера, но без непосредственное подключение к ВМ головного узла toohello или доступ к подписке Azure.

![Отправить задание tooa кластера в Azure][jobsubmit]

## <a name="prerequisites"></a>Предварительные требования
* **Головной узел пакета HPC, развернутых в Виртуальной машине Azure** -мы рекомендуем использовать такие как автоматические средства [шаблона Azure краткое руководство](https://azure.microsoft.com/documentation/templates/) или [скрипт Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello головного узла и кластер. Требуется DNS-имя головного узла hello hello и hello учетные данные администратора кластера для выполнения шагов hello в этой статье.
* **Клиентский компьютер**. Требуется клиентский компьютер под управлением Windows или Windows Server, который поддерживает запуск клиентских служебных программ для пакета HPC (ознакомьтесь с [требованиями к системе](https://technet.microsoft.com/library/dn535781.aspx)). Если требуется только toouse hello HPC Pack веб-портала или API-интерфейса REST toosubmit задания, можно использовать любой клиентский компьютер по своему усмотрению.
* **Установочный носитель пакета HPC** -tooinstall hello клиентских служебных программ пакета HPC, hello бесплатный установочный пакет для последней версии пакета HPC (HPC Pack 2012 R2) доступен в [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=328024). Убедитесь, что при загрузке hello же версии пакета HPC, установленной на ВМ головного узла hello.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Шаг 1: Установка и настройка hello веб-компонентов на головном узле hello
tooenable toohello заданий REST интерфейс toosubmit кластера по протоколу HTTPS, убедитесь, что веб-компонентов пакета HPC hello, настроены на головной узел пакета HPC hello. Если они не установлены, сначала установите hello веб-компоненты, запустив файл установки HpcWebComponents.msi hello. Затем настройте компоненты hello, запустив скрипт HPC PowerShell hello **Set-HPCWebComponents.ps1**.

Подробные инструкции см. в разделе [установить веб-компоненты hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Некоторые шаблоны Azure краткое руководство для пакета HPC установки и автоматической настройки веб-компоненты hello. Если вы используете hello [скрипт развертывания IaaS пакета HPC](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello кластера, при необходимости можно установить и настроить hello веб-компоненты как часть развертывания hello.
> 
> 

**веб-компоненты tooinstall hello**

1. Подключение toohello ВМ головного узла с помощью hello учетные данные администратора кластера.
2. Из папки установки пакета HPC hello запустите файл HpcWebComponents.msi на головном узле hello.
3. Выполните действия hello приветствия мастера tooinstall hello веб-компонентов

**веб-компоненты tooconfigure hello**

1. На головном узле hello запустите HPC PowerShell от имени администратора.
2. toochange toohello каталоге сценария настройки hello, тип hello следующую команду:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure hello интерфейс REST и запуска hello веб-службы HPC типа hello следующую команду:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Когда запрашиваемые tooselect сертификат, выберите сертификат hello, соответствующий открытому DNS-имени toohello hello головного узла. Например, при развертывании головного узла hello виртуальную Машину с помощью hello классической модели развертывания, имя сертификата hello выглядит CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. При использовании модели развертывания диспетчера ресурсов hello, имя сертификата hello выглядит CN =&lt;*HeadNodeDnsName*&gt;.&lt; *область*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Этот сертификат выбрать позднее при отправке задания toohello головного узла на локальном компьютере. Не выбирайте и не настраивайте сертификат, который соответствует имени компьютера toohello hello головного узла в домене Active Directory hello (например, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. tooconfigure hello веб-портал для отправки заданий, типа hello следующую команду:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. После завершения скрипта hello, остановите и перезапустите hello служба планировщика заданий HPC, введя hello, следующие команды:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Шаг 2: Установка клиентских служебных программ пакета HPC hello на локальном компьютере
Если вы хотите tooinstall hello HPC Pack клиентские служебные программы на компьютере, загрузить файлы установки пакета HPC (полная установка) из hello [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkId=328024). При установке hello, выберите вариант установки hello для hello **клиентских служебных программ пакета HPC**.

toouse hello HPC Pack клиентские средства toosubmit заданий toohello ВМ головного узла, также требуется tooexport сертификат из головного узла hello и установить его на клиентском компьютере hello. Hello сертификат должен находиться в. Формат CER.

**tooexport hello сертификат из головного узла hello**

1. На головном узле hello добавьте hello сертификатов оснастки tooa консоли управления для hello учетной записи локального компьютера. Оснастка tooadd hello, содержится [добавьте hello оснастку сертификатов tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. В дереве консоли hello, разверните **сертификаты — локальный компьютер** > **личных**, а затем нажмите кнопку **сертификаты**.
3. Найдите hello сертификат, настроенный для hello HPC Pack веб-компонентов в [шаг 1: Установка и настройка hello веб-компонентов на головном узле hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (например, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Щелкните правой кнопкой мыши сертификат hello и нажмите кнопку **все задачи** > **Экспорт**.
5. В окне приветствия мастера экспорта сертификатов нажмите кнопку **Далее**и убедитесь, что **нет, не экспортировать закрытый ключ hello** выбран.
6. Hello выполните оставшиеся действия мастера hello tooexport сертификата hello DER-кодировке X.509 (. Формат CER).

**tooimport hello сертификатов на клиентском компьютере hello**

1. Скопируйте экспортированный из папки tooa hello головного узла на клиентском компьютере hello hello сертификат.
2. На клиентском компьютере hello запустите certmgr.msc.
3. В диспетчере сертификатов разверните **Сертификаты — текущий пользователь** > **Доверенные корневые центры сертификации**, щелкните правой кнопкой мыши **Сертификаты** и щелкните **Все задачи** > **Импорт**.
4. В окне приветствия мастера импорта сертификатов нажмите кнопку **Далее** и выполните hello действия tooimport hello сертификат, экспортированный из головного узла toohello hello, хранилище доверенных корневых центров сертификации.

> [!TIP]
> Может появиться предупреждение о безопасности, поскольку hello центр сертификации на головном узле hello не распознаются hello клиентского компьютера. В целях тестирования можно игнорировать это предупреждения и завершения импорта сертификатов hello.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Шаг 3: Запуск тестовые задания в кластере hello
tooverify конфигурацию, повторите выполнение задания на hello кластера в Azure из hello локального компьютера. Например можно использовать средства графического интерфейса пользователя HPC Pack или командной строки toosubmit заданий toohello кластера. Также можно использовать веб-портала toosubmit заданий.

**toorun команд отправки заданий на клиентском компьютере hello**

1. На клиентском компьютере, где установлены клиентских служебных программ пакета HPC hello откройте командную строку.
2. Введите тестовую команду. Например toolist все задания в кластере hello введите tooone аналогичные команды из hello следующие, в зависимости от hello полное DNS-имя головного узла hello:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    или
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Используйте hello полное DNS-имя головного узла hello, не hello IP-адрес, в URL-адрес планировщика hello. При указании hello IP-адрес, отображается сообщение об ошибке примерно слишком "сертификат сервера hello должен tooeither имеет цепочку доверия или помещен в хранилище доверенных корневых hello toobe.»
   > 
   > 
3. При появлении запроса введите имя пользователя hello (в форме hello &lt;DomainName&gt;\\&lt;UserName&gt;) и пароль администратора кластера HPC hello или другого пользователя кластера, который вы настроили. Вы можете toostore hello учетные данные локально для других операций.
   
    Появится список заданий.

**toouse диспетчер заданий HPC на клиентском компьютере hello**

1. Если при отправке задания не ранее хранить учетные данные домена для пользователя кластера, можно добавить учетные данные hello в диспетчере учетных данных.
   
    а. На панели управления на клиентском компьютере hello запустите диспетчер учетных данных.
   
    b. Щелкните **Учетные данные Windows** > **Добавить общие учетные данные**.
   
    c. Укажите адрес в Интернете hello (например, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler "или" https://&lt;HeadNodeDnsName&gt;.&lt; область&gt;.cloudapp.azure.com/HpcScheduler) и имя пользователя hello (&lt;DomainName&gt;\\&lt;UserName&gt;) и пароль администратора кластера hello или другой пользователь кластера, вы настроили.
2. На клиентском компьютере hello запустите диспетчер заданий HPC.
3. В hello **Выбор головного узла** диалоговое окно, тип hello URL-адрес toohello головного узла в Azure (например, https://&lt;HeadNodeDnsName&gt;. cloudapp.net "или" https://&lt;HeadNodeDnsName&gt;. &lt;область&gt;. cloudapp.azure.com).
   
    Диспетчер заданий HPC открывается и отображается список заданий на головном узле hello.

**веб-портал toouse hello, работающих на головном узле hello**

1. Запуск веб-браузер на клиентском компьютере hello и введите одну из hello следующие адреса в зависимости от hello полное DNS-имя головного узла hello:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    или
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. В hello безопасности появившемся введите учетные данные администратора кластера HPC hello hello. (Вы также можете добавить пользователей кластера в разных ролях. Ознакомьтесь со статьей [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx)(Управление пользователями кластера.)
   
    веб-портал Hello откроется представление списка заданий toohello.
3. Щелкните toosubmit образец задания, возвращает строку hello «Hello World» из кластера hello **новое задание** hello левой навигационной панели.
4. На hello **новое задание** в разделе **со страниц отправки**, нажмите кнопку **HelloWorld**. Откроется страница отправки задания Hello.
5. Нажмите кнопку **Submit**(Отправить). При запросе введите учетные данные администратора кластера HPC hello hello. отправке задания Hello и hello идентификатор задания появится на hello **Мои задания** страницы.
6. Щелкните идентификатор задания hello результаты hello tooview hello отправленного задания и нажмите кнопку **Просмотр задач** tooview выходные данные команды hello (в разделе **выходные данные**).

## <a name="next-steps"></a>Дальнейшие действия
* Также можно отправлять задания toohello Azure кластер с hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Toosubmit кластерных заданий из клиента Linux, см hello Python в hello [HPC Pack 2012 R2 SDK и образцы кода](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
