---
title: "кластер aaaSet копирование гибридного пакета HPC в Azure | Документы Microsoft"
description: "Узнайте, как toouse пакета Microsoft HPC и Azure tooset вверх небольшой, высокая производительность гибридного вычислительных кластера (HPC)"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Настройка гибридного кластера высокопроизводительных вычислительных систем (HPC) с помощью пакета Microsoft HPC и вычислительных узлов Azure по требованию
Используйте Microsoft HPC Pack 2012 R2 и Azure tooset копирование небольшого гибридного высокопроизводительных вычислительных систем (HPC) кластера. Hello кластера, приведенными в этой статье состоит из локального головного узла HPC Pack и некоторые вычислительные узлы развертывания по запросу в Azure облачной службы. Вычислительные задания можно выполнять на hello гибридный кластер.

![Гибридный кластер высокопроизводительных вычислений (HPC)][Overview] 

Это учебник показывает один из подходов, иногда называют кластера «прорыв toohello облако» toouse масштабируемых, по запросу ресурсы Azure toorun ресурсоемких приложений.

В этом учебнике предполагается, что у читателя нет опыта работы с вычислительными кластерами или пакетом HPC. Это предполагаемое только toohelp развертывание гибридный вычислительный кластер быстро для демонстрационных целей. Рекомендации и шаги toodeploy гибридных HPC Pack кластера с масштабом больше в рабочей среде или toouse 2016 пакета HPC, см. в разделе hello [подробное руководство](http://go.microsoft.com/fwlink/p/?LinkID=200493). Другие сценарии использования пакета HPC, включая автоматизированное развертывание кластера в виртуальных машинах Azure, см. в статье [Варианты создания в Azure кластера HPC под управлением Windows и управления им с помощью пакета HPC](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Предварительные требования
* **Подписка Azure.** Если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/free/).
* **На локальном компьютере под управлением Windows Server 2012 R2 или Windows Server 2012** -использовать этот компьютер в качестве головного узла кластера HPC hello hello. Если вы еще не установили Windows Server, вы можете скачать и установить [ознакомительную версию](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * Hello компьютер должен быть присоединены к домену tooan домена Active Directory. Для целей тестирования можно настроить компьютере головного узла hello как контроллер домена. tooadd hello роли сервера служб домена Active Directory и повысить уровень компьютера головного узла hello как контроллер домена см. в разделе hello документации по Windows Server.
  * toosupport пакета HPC, hello операционной системы должен быть установлен в одном из этих языков: английский, японский и китайский (упрощенное письмо).
  * Убедитесь, что установлены важные и критические обновления.
* **HPC Pack 2012 R2** - [загрузки](http://go.microsoft.com/fwlink/p/?linkid=328024) hello установочный пакет для последней версии hello без издержек и скопируйте компьютере головного узла hello файлы toohello. Выберите файлы установки в hello же языке, что и установку Windows Server.

    >[!NOTE]
    > Если вы хотите toouse HPC Pack 2016 вместо HPC Pack 2012 R2, требуется дополнительная настройка. В разделе hello [подробное руководство](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Учетная запись домена** -этой учетной записи должны быть настроены права локального администратора на tooinstall hello головного узла HPC Pack.
* **Подключение TCP на порту 443** из tooAzure hello головного узла.

## <a name="install-hpc-pack-on-hello-head-node"></a>Установка пакета HPC на головном узле hello
Сначала установите пакет Microsoft HPC на локальном компьютере под управлением Windows Server, Этот компьютер становится hello головного узла кластера hello.

1. Войдите на головном узле toohello, используя учетную запись домена, имеющую права локального администратора.

2. Запустите мастер установки пакета HPC hello Setup.exe из файлов установки пакета HPC hello.

3. На hello **установки HPC Pack 2012 R2** щелкните **новую установку или добавьте новые компоненты tooan существующей установки**.

    ![Установка пакета HPC 2012][install_hpc1]

4. На hello **страницы условия пользовательского соглашения на использование программного обеспечения Microsoft**, нажмите кнопку **Далее**.

5. На hello **Выбор типа установки** нажмите кнопку **Создание нового кластера HPC, создайте головной узел**, а затем нажмите кнопку **Далее**.

6. несколько тестов предустановки запускается мастер Hello. Нажмите кнопку **Далее** на hello **правила установки** страницы, если все тесты пройдены. В противном случае просмотрите информация hello и внесите необходимые изменения в вашей среде. Затем выполните тесты hello еще раз или при необходимости запуска hello мастер установки еще раз.
7. На hello **конфигурация HPC DB** убедитесь, что **головного узла** выбран для всех баз данных HPC и нажмите кнопку **Далее**. 

    ![Конфигурация базы данных][install_hpc4]

8. Примите значения по умолчанию на оставшихся страницах мастера hello hello. На hello **установить обязательные компоненты** щелкните **установить**.
   
    ![Установить][install_hpc6]

9. После завершения установки hello, снимите флажок **запустить диспетчер кластеров HPC** и нажмите кнопку **Готово**. (Вы запустите диспетчер кластеров HPC позднее.)
   
    ![Готово][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Подготовка hello подписки Azure
Выполните следующие шаги в hello hello [портал Azure](https://portal.azure.com) с подпиской Azure. После выполнения этих действий, вы можете развернуть узлы Azure с hello локального головного узла. 
  
  > [!NOTE]
  > Также запишите идентификатор подписки Azure, который понадобится позже. Найти идентификатор hello в **подписки** hello портала.
  > 

### <a name="upload-hello-default-management-certificate"></a>Отправка сертификата управления по умолчанию hello
Пакет HPC устанавливает самозаверяющий сертификат на головном узле hello, вызывается hello по умолчанию Microsoft HPC Azure сертификат управления, который можно отправить как сертификат управления Azure. Этот сертификат предоставляется для тестирования и hello подтверждение концепции развертываний toosecure hello подключения между головным узлом и Azure.

1. Головной узел компьютера hello вход toohello [портал Azure](https://portal.azure.com).

2. Выберите **Подписки** > *имя_вашей_подписки*.

3. Выберите **Сертификаты управления** > **Отправить**.4. Перейдите на головной узел hello файл C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello. Затем выберите **Отправить**.

   
Hello **по умолчанию управления HPC Azure** сертификат отображается в списке hello сертификатов управления.

### <a name="create-an-azure-cloud-service"></a>Создание облачной службы Azure
> [!NOTE]
> Для повышения производительности рекомендуется создать облачную службу hello и hello учетной записи хранения (в дальнейшем) в hello одной географической области.
> 
> 

1. На портале hello щелкните **облачные службы (классические)** > **+ добавить**.

2.  Введите имя DNS для службы hello, выберите группу ресурсов и расположение и нажмите кнопку **создать**.


### <a name="create-an-azure-storage-account"></a>Создание учетной записи хранения Azure
1. На портале hello щелкните **учетные записи хранения (классические)** > **+ добавить**.

2. Введите имя учетной записи hello и выберите hello **классический** модели развертывания.

3. Выберите группу ресурсов и расположение. Для остальных параметров оставьте значения по умолчанию. Затем щелкните **Создать**.

## <a name="configure-hello-head-node"></a>Настройка головного узла hello
toouse toodeploy диспетчера кластеров HPC узлы Azure и задания toosubmit сначала выполнить некоторые действия по настройке кластера требуется.

1. На головном узле hello запустите диспетчер кластеров HPC. Если hello **Выбор головного узла** диалоговое окно, нажмите кнопку **локального компьютера**. Hello **списку задач развертывания** отображается.

2. В разделе **Необходимые задачи развертывания** щелкните **Настроить сеть**.
   
    ![Настройка сети][config_hpc2]

3. В окне приветствия мастера настройки сети выберите **все узлы только в сети предприятия** (топологии 5). Эта конфигурация сети — hello простой для демонстрационных целей.
   
    ![Топология 5][config_hpc3]
   
4. Нажмите кнопку **Далее** tooaccept значения по умолчанию на оставшихся страницах мастера hello hello. Затем на hello **проверки** щелкните **Настройка** toocomplete hello сетевая конфигурация.

5. В hello **списку задач развертывания**, нажмите кнопку **учетные данные установки**.

6. В hello **учетных данных установки** диалоговом hello введите учетные данные учетной записи домена hello использования tooinstall пакета HPC. Нажмите кнопку **ОК**. 
   
    ![Учетные данные установки][config_hpc6]
   
7. В hello **списку задач развертывания**, нажмите кнопку **настройте именование новых узлов hello**.

8. В hello **укажите серии именования узлов** диалоговое окно примите именования рядов и нажмите кнопку по умолчанию hello **ОК**. Выполнение этого действия, несмотря на то, что hello узлов Azure, добавляемое в этом учебнике присваиваются автоматически.
   
    ![Именование узлов][config_hpc8]
   
9. В hello **списку задач развертывания**, нажмите кнопку **создайте шаблон узла**. Далее в учебнике hello используйте toohello кластера узлов Azure tooadd hello узла шаблона.

10. В hello мастер создания шаблона узла, выполните hello следующие действия.
    
    а. На hello **выберите тип шаблона узла** щелкните **шаблона узла Windows Azure**, а затем нажмите кнопку **Далее**.
    
    ![Шаблон узла][config_hpc10]
    
    b. Нажмите кнопку **Далее** tooaccept hello по умолчанию имя шаблона.
    
    c. На hello **предоставляют сведения о подписке** введите идентификатор подписки Azure (доступно в сведениях учетной записи Azure). Затем в разделе **Сертификат управления** найдите **сертификат управления Microsoft HPC Azure по умолчанию.** Нажмите кнопку **Далее**.
    
    ![Шаблон узла][config_hpc12]
    
    d. На hello **предоставляют сведения о службе** страницу, выберите hello облачной службы и учетной записи хранилища hello, созданный на предыдущем шаге. Нажмите кнопку **Далее**.
    
    ![Шаблон узла][config_hpc13]
    
    д. Нажмите кнопку **Далее** tooaccept значения по умолчанию на оставшихся страницах мастера hello hello. Затем на hello **проверки** щелкните **создать** шаблона узла toocreate hello.
    
    > [!NOTE]
    > По умолчанию hello шаблона узла Azure включает параметры для toostart (провизионирование) и остановка узлов hello вручную, с помощью диспетчера кластеров HPC. При необходимости можно настроить toostart расписание и остановить hello узлов Azure автоматически.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Добавление узлов Azure toohello кластера
Теперь можно используйте toohello кластера узлов Azure tooadd hello узла шаблона. Добавление кластера toohello узлы hello хранит сведения о конфигурации, чтобы можно было запускать (подготавливать) их в любое время в облачной службе hello. Подписки только возвращает взимается плата за узлов Azure после запущенных экземпляров hello в облачной службе hello.

Выполните эти шаги tooadd небольшой узлами.

1. В диспетчере кластеров HPC выберите **Node Management** (Управление узлами) (в текущей версии пакета HPC **Управление ресурсами**) > **Добавить узел**.
   
    ![Добавить узел][add_node1]

2. В hello мастер добавления узла в hello **Выбор метода развертывания** нажмите кнопку **узлов Windows Azure, добавить**, а затем нажмите кнопку **Далее**.
   
    ![Добавление узла Azure][add_node1_1]

3. На hello **укажите новые узлы** страницу, выберите hello шаблона узла Azure, созданной ранее (вызывается по умолчанию **шаблоном AzureNode по умолчанию**). Затем укажите **2** **мелких** узла и нажмите кнопку **Далее**.
   
    ![Указание узлов][add_node2]
   
4. На hello **Здравствуйте, завершение работы мастера добавления узла** щелкните **Готово**.
    
     Два узла Azure с именем **AzureCN-0001** и **AzureCN-0002** появятся в диспетчере кластеров HPC. Обе они находятся в hello **не развернуто** состояния.
   
    ![Добавленные узлы][add_node3]

## <a name="start-hello-azure-nodes"></a>Запуск hello узлов Azure
При необходимости ресурсы кластера hello toouse в Azure, используйте диспетчер кластеров HPC toostart (провизионирование) узлов Azure hello и перевести в оперативный режим.

1. В диспетчере кластера HPC, нажмите кнопку **управления узлами** (называется **управление ресурсами** в текущей версии пакета HPC), и выберите hello узлов Azure.

2. Выберите **Запустить**, а затем нажмите кнопку **ОК**.
   
   ![Запуск узлов][add_node4]
   
    узлы Hello переход toohello **Provisioning** состояния. Представление hello подготовки hello tootrack журнала ход выполнения подготовки.
   
    ![Подготовка узлов][add_node6]

3. Через несколько минут hello узлов Azure завершения подготовки и находятся в hello **Offline** состояния. В этом состоянии hello экземпляров роли выполняются, но еще не может принимать задания кластера.

4. Запуск tooconfirm, hello экземпляров роли в hello портал Azure, щелкните **облачные службы (классические)** > *your_cloud_service_name*.
   
   Вы увидите два **HpcWorkerRole** экземпляров (узлов), выполняемых в службе hello. Пакет HPC также автоматически развертывает два **HpcProxy** экземпляров (размер среднего) toohandle взаимодействия между головным узлом hello и Azure.

   ![Выполняющиеся экземпляры][view_instances1]

5. online toorun toobring hello Azure узлы кластера заданий, выберите hello узлов, щелкните правой кнопкой мыши и выберите команду **перевести в оперативный режим**.
   
    ![Автономные узлы][add_node7]
   
    Диспетчер кластеров HPC означает, что узлы hello в hello **Online** состояния.

## <a name="run-a-command-across-hello-cluster"></a>Выполнение команды в кластере hello
toocheck hello установки, используйте hello HPC Pack **clusrun** toorun команда команды или приложения на одном или нескольких узлах кластера. В качестве простого примера используйте **clusrun** tooget hello IP-конфигурации hello узлов Azure.

1. На головном узле hello откройте командную строку с правами администратора.

2. Введите следующую команду hello:
   
    `clusrun /nodes:azurecn* ipconfig`

3. При появлении запроса введите пароль администратора кластера. Вы увидите примерно следующие toohello, выходных данных команды.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>Выполнение тестового задания
Теперь можно отправьте тестовое задание, запускаемую hello гибридный кластер. Этот пример является простым заданием параметрического анализа (тип классических параллельных вычислений). В этом примере выполняется подзадачи, добавить tooitself целое число со знаком, используя hello **set /a** команды. Все узлы hello кластера hello contribute подзадачи hello toofinishing для целых чисел от 1 too100.

1. В диспетчере кластеров HPC выберите **Управление заданиями** > **New Parametric Sweep Job** (Создать задание параметрического анализа).
   
    ![Новое задание][test_job1]

2. В hello **новое параметрической очистки задание** диалогового **командной строки**, тип `set /a *+*` (перезапись hello по умолчанию появится командной строки). Оставьте значения по умолчанию для оставшихся параметров hello и нажмите кнопку **отправить** toosubmit hello задания.
   
    ![Параметрический анализ][param_sweep1]

3. После завершения задания hello дважды щелкните hello **Мои задачи очистки** задания.

4. Нажмите кнопку **Просмотр задач**, а затем нажмите кнопку выходных данных вычисляется hello подзадаче tooview том же уровне.
   
    ![Результаты выполнения задачи][view_job361]

5. Нажмите кнопку toosee, какой из узлов для этой вложенной задачи выполняется вычисление hello **выделенных узлов**. (Кластер может показывать другое имя узла).
   
    ![Результаты выполнения задачи][view_job362]

## <a name="stop-hello-azure-nodes"></a>Остановить hello узлов Azure
После испытать hello кластера, остановите hello узлов Azure tooavoid ненужные расходы tooyour учетной записи. Этот шаг останавливает hello облачной службы и удаляет экземпляры роли Azure hello.

1. В диспетчере кластеров HPC в разделе **Node Management** (Управление узлами) (в предыдущих версиях пакета HPC он называется **Управление ресурсами**) выберите оба узла Azure. Затем щелкните **Остановить**.
   
    ![Остановка узлов][stop_node1]

2. В hello **узлов Windows Azure остановить** диалоговое окно, нажмите кнопку **остановить**. 
   
3. узлы Hello переход toohello **остановка** состояния. Через несколько минут диспетчера кластеров HPC показывает, что узлы hello **не развернуто**.
   
    ![Неразвернутые узлы][stop_node4]

4. Здравствуйте, tooconfirm, экземпляры роли hello больше не выполняется в Azure, в Azure, щелкните **облачные службы (классические)** > *your_cloud_service_name*. Экземпляры не будут развернуты в рабочей среде hello. 
   
    На этом учебник hello.

## <a name="next-steps"></a>Дальнейшие действия
* Просмотр документации hello для [HPC Pack](https://technet.microsoft.com/library/cc514029).
* tooset копирование гибридного развертывания кластера HPC Pack в масштабе выше, в разделе [прорыв tooAzure экземпляров рабочей роли с помощью пакета Microsoft HPC](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Для других способов toocreate кластере HPC Pack в Azure, включая использование шаблонов диспетчера ресурсов Azure, см. в [параметры кластера HPC с помощью пакета Microsoft HPC в Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
