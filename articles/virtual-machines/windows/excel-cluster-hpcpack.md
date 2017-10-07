---
title: "aaaHPC пакет кластера для Excel и SOA | Документы Microsoft"
description: "Приступая к работе с крупномасштабными рабочими нагрузками Excel и SOA в кластере пакета HPC в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Приступая к работе с рабочими нагрузками Excel и SOA в кластере пакета HPC в Azure
В этой статье показано, как toodeploy Microsoft HPC Pack 2012 R2 кластера на виртуальных машинах Azure с использованием шаблоном краткого руководства Azure, или при необходимости развертывания сценария Azure PowerShell. Hello кластер использует toorun виртуальной Машины Azure Marketplace образов разработана Microsoft Excel или рабочих нагрузок сервисноориентированной архитектуре (SOA) с пакетом HPC. Можно использовать toorun hello кластера HPC для Excel и служб SOA с клиентского компьютера в локальной среде. службы Excel HPC Hello включают разгрузки книги Excel и определяемые пользователем функции Excel или определяемые пользователем функции.

> [!IMPORTANT] 
> В этой статье используются функции, шаблоны и сценарии для пакета HPC 2012 R2. Этот сценарий пока не поддерживается для пакета HPC 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

На высоком уровне hello следующей диаграмме показан кластер HPC Pack hello создания.

![Кластер HPC с узлами, выполняющими рабочие нагрузки Excel][scenario]

## <a name="prerequisites"></a>Предварительные требования
* **Клиентский компьютер** -вам потребуется клиента на основе Windows компьютер toosubmit образец Excel и SOA задания toohello кластер. Необходимо также hello toorun компьютера Windows Azure PowerShell сценария развертывания кластера (при выборе этого метода развертывания).
* **Подписка Azure.** Если ее нет, можно за пару минут создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* **Квота ядер** -может потребоваться tooincrease hello квоту ядер, особенно в том случае, если вы развертываете несколько узлов кластера с несколькими ядрами размеры виртуальных Машин. При использовании шаблона Azure краткое руководство по регионам Azure — hello квоту ядер в диспетчере ресурсов. В этом случае может потребоваться Квота tooincrease hello в определенном регионе. Ознакомьтесь со статьей [Пределы, квоты и ограничения подписок на Azure](../../azure-subscription-service-limits.md). квоты tooincrease [откройте запрос поддержки сети клиента](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) бесплатно.
* **Лицензия Microsoft Office.** В случае развертывания вычислительных узлов с помощью образа виртуальной машины пакета HPC 2012 R2 с Microsoft Excel из Marketplace будет установлена 30-дневная ознакомительная версия Microsoft Excel профессиональный плюс 2013. После hello ознакомительного периода необходимо tooprovide допустимым Microsoft Office лицензии tooactivate Excel toocontinue toorun рабочих нагрузок. Ознакомьтесь с разделом [Активация Excel](#excel-activation) далее в этой статье. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Шаг 1. Настройка кластера пакета HPC в Azure
Далее показано два tooset параметры кластера HPC Pack 2012 R2 hello: во-первых, с помощью шаблона Azure краткое руководство и hello портал Azure; Во-вторых, с помощью сценария развертывания Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Вариант 1. Использование шаблона быстрого запуска
Использование шаблона Azure краткое руководство tooquickly развертывание кластере HPC Pack в hello портал Azure. При открытии шаблона hello в портале hello, вы получаете простой пользовательский Интерфейс, куда вводится hello параметры для кластера. Ниже приведены шаги, hello. 

> [!TIP]
> При необходимости используйте [шаблон Azure Markeplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) , который создает аналогичный кластер специально для рабочих нагрузок Excel. действия Hello немного отличаются от следующих hello.
> 
> 

1. Посетите hello [страницы шаблона создать кластер HPC на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Если требуется, просмотрите сведения о шаблона hello и hello исходного кода.
2. Нажмите кнопку **развертывание tooAzure** toostart развертывания с помощью шаблона hello в hello портал Azure.
   
   ![Развертывание шаблона tooAzure][github]
3. На портале hello выполните эти шаги tooenter hello параметры для шаблона кластера HPC hello.
   
   а. На hello **параметры** введите или измените значения для параметров шаблона hello. (Щелкните значок Далее tooeach приветствия сведения справки.) В следующий экран приветствия будут показаны примеры значений. В этом примере создается кластер с именем *hpc01* в hello *hpc.local* домен, состоящий из головного узла и 2 вычислительных узлов. Hello вычислительные узлы создаются из виртуальной Машины HPC Pack образ, включающий Microsoft Excel.
   
   ![Ввод параметров][parameters-new-portal]
   
   > [!NOTE]
   > Hello головного узла виртуальной Машины автоматически создается на основе hello [последние образа Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC Pack 2012 R2 на Windows Server 2012 R2. В настоящее время образ hello основан на HPC Pack 2012 R2 с обновлением 3.
   > 
   > ВМ вычислительных узлов создаются на основе hello последний образ hello выбран вычислительного узла семейства. Выберите hello **ComputeNodeWithExcel** параметр для hello последнюю пакета HPC образ вычислительного узла, включающий ознакомительной версии Microsoft Excel профессиональный плюс 2013. toodeploy кластера для общие SOA сеансов или Разгрузка Excel UDF, выберите hello **ComputeNode** параметр (без установки Excel).
   > 
   > 
   
   b. Выберите подписку hello.
   
   c. Создание группы ресурсов кластера hello, таких как *hpc01RG*.
   
   d. Выберите расположение для hello группы ресурсов, таких как центральной части США.
   
   д. На hello **условия** Проверьте условия hello. Если вы согласны с ними, щелкните **Приобрести**. Когда вы закончите задание hello значений для параметров шаблона hello, нажмите кнопку **создать**.
4. После завершения развертывания hello (обычно занимает около 30 минут), экспортируйте файл сертификата hello кластера из головного узла кластера hello. В более позднем этапе вы импортируете сертификат открытого на hello tooprovide hello стороне сервера проверки подлинности клиентского компьютера для безопасной привязкой HTTP.
   
   а. На hello портал Azure, перейдите toohello панели мониторинга, выберите hello головного узла и нажмите кнопку **Connect** вверху hello tooconnect страницы приветствия, с помощью удаленного рабочего стола.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Используйте стандартные процедуры в диспетчер сертификатов tooexport hello головного узла сертификат (расположенный в Cert: \LocalMachine\My) без закрытого ключа hello. В этом примере экспортируйте *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Экспорт сертификата hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Вариант 2. Использовать скрипт развертывания IaaS пакета HPC hello
Hello скрипт развертывания IaaS пакета HPC предоставляет другим универсальным способом toodeploy кластере HPC Pack. Он создает кластер hello классической модели развертывания, в то время как шаблон hello использует модель развертывания диспетчера ресурсов Azure hello. Кроме того сценарий hello совместим с подписки в hello Azure Global или Azure China службы.

**Дополнительные требования**

* **Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.
* **Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949). Проверьте версию hello hello сценария, выполнив команду `New-HPCIaaSCluster.ps1 –Version`. Эта статья основана на версии 4.5.0 или более поздней hello сценария.

**Создать файл конфигурации hello**

 Hello скрипт развертывания IaaS пакета HPC использует файл конфигурации XML в качестве входных данных, описывающий hello инфраструктура кластера HPC hello. в кластере, состоящем из головного узла и 18 вычислительные узлы, созданные на основе образ hello вычислительного узла, который включает Microsoft Excel toodeploy заменить значения для вашей среды в hello следующий образец файла конфигурации. Дополнительные сведения о файле конфигурации hello см. в разделе файла Manual.rtf hello в папке скрипта hello и [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Примечания о файле конфигурации hello**

* Hello **VMName** головного узла hello **должен** быть hello же, как hello **ServiceName**, или toorun сбой заданий SOA.
* Убедитесь, что указан **EnableWebPortal** , чтобы hello головного узла сертификат создается и экспортировать.
* файл Hello указывает сценарий PowerShell после конфигурации PostConfig.ps1, работающей на головном узле hello. Hello следующий образец скрипта настраивает hello строка подключения хранилища Azure, удаляет hello роли вычислительного узла из головного узла hello и переводит все узлы в оперативный режим, если они развернуты. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Запустите сценарий hello**

1. Откройте консоль PowerShell hello hello клиентского компьютера с правами администратора.
2. Измените скрипт в папку toohello каталога (E:\IaaSClusterScript в этом примере).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. hello HPC Pack toodeploy кластера, запустите следующую команду hello. В этом примере предполагается, что этот файл конфигурации hello находится в E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

сценарий развертывания пакета HPC Hello выполняется некоторое время. Один сценарий hello самое делает — tooexport и загрузить сертификат кластера hello и сохраните его в папке "документы" hello текущего пользователя на клиентском компьютере hello. Hello сценарий создает сообщение аналогичные toohello следующее. На следующем шаге нужно импортировать сертификат hello в hello соответствующее хранилище сертификатов.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Шаг 2. Разгрузка книг Excel и выполнение пользовательских функций из локального клиента
### <a name="excel-activation"></a>Активация Excel
При использовании образа виртуальной Машины ComputeNodeWithExcel hello для рабочих нагрузок, необходимо tooprovide допустимым Microsoft Office лицензионного ключа tooactivate Excel на вычислительных узлах hello. В противном случае hello ознакомительной версии Excel истекает через 30 дней, и запускать книги Excel будут завершаться hello COMException (0x800AC472). 

Excel может rearm еще на 30 дней оценки времени: вход toohello головного узла и clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` на все Excel вычислительных узлов через диспетчер кластеров HPC. Возвращаться к исходному состоянию активации можно не более двух раз. После этого необходимо будет указать действительный лицензионный ключ Office.

Hello Office профессиональный плюс 2013 установлен на hello образа виртуальной Машины представляет собой версию тома с универсальным тома лицензии ключ установки (GVLK). Вы можете активировать его, воспользовавшись службой управления ключами (KMS), активацией с помощью Active Directory (AD-BA) или ключом многократной активации (MAK). 

    * toouse KMS/AD-бизнес-Аналитики, использовать существующий сервер KMS, или настройте его с помощью hello пакет Microsoft Office 2013 корпоративного лицензирования. (Если вы хотите задайте hello server на головном узле hello.) После этого активируйте ключ узла KMS hello через hello Интернет или по телефону. Затем clusrun `ospp.vbs` tooset hello и порт сервера службы KMS и активировать Office на всех узлах вычисления Excel hello. 

    * toouse MAK первый clusrun `ospp.vbs` tooinput hello ключ, а затем активировать все узлы вычислений Excel hello через hello Интернет или по телефону. 

> [!NOTE]
> Розничные ключи продукта для Office профессиональный плюс 2013 невозможно использовать с этим образом виртуальной машины. Если у вас имеются действительные ключи и установочный носитель для выпусков Office или Excel, отличных от этого корпоративного выпуска Office профессиональный плюс 2013, то вы можете использовать имеющиеся выпуски. Сначала удалите этот том выпуск и установите hello от имеющегося выпуска. Hello переустановлен Excel вычислительных узлов, можно захватить как настраиваемые toouse образ виртуальной Машины в развертывании в масштабе.
> 
> 

### <a name="offload-excel-workbooks"></a>Разгрузка книг Excel
Выполните эти шаги toooffload книги Excel, чтобы он запускался на кластере HPC Pack hello в Azure. toodo это, необходимо иметь Excel 2010 или 2013, уже установлен на клиентском компьютере hello.

1. С помощью одного из параметров hello в шаге 1 toodeploy кластере HPC Pack с hello Excel вычислений изображение узла. Получите hello кластера файл сертификата (.cer) кластера имя пользователя и пароль.
2. На клиентском компьютере hello импортируйте сертификат кластера hello в Cert: \CurrentUser\Root.
3. Убедитесь, что установлен Excel. Создайте файл Excel.exe.config с hello, следуя содержимое в hello же папке, что и Excel.exe на клиентском компьютере hello. Этот шаг гарантирует, что успешной загрузки этого hello HPC Pack 2012 R2 Excel надстройки.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Установка пакета HPC hello клиента toosubmit заданий toohello кластера. Один из вариантов — полный hello toodownload [установки HPC Pack 2012 R2 с обновлением 3](http://www.microsoft.com/download/details.aspx?id=49922) и установить клиент HPC Pack hello. Можно также загрузить и установить hello [HPC Pack 2012 R2 с обновлением 3 клиентские служебные программы](https://www.microsoft.com/download/details.aspx?id=49923) и hello соответствующие Visual C++ 2010 распространяемого пакета для компьютера ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. В этом примере мы используем пример книги Excel — ConvertiblePricing_Complete.xlsb. Его можно скачать [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Скопируйте hello Excel книги tooa например D:\Excel\Run рабочей папки.
7. Откройте книгу Excel hello. На hello **разработка** ленты, нажмите кнопку **надстройки COM** и подтвердите, hello HPC Pack Excel надстройка успешно загружается.
   
   ![Надстройка Excel для пакета HPC][addin]
8. Макрос VBA hello редактирования HPCControlMacros в Excel, изменив hello комментарии как показано в hello, выполнив сценарий. Подставьте соответствующие значения для вашей среды.
   
   ![Макрос Excel для пакета HPC][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Скопируйте каталог hello Excel книги tooan передачи, например D:\Excel\Upload. Этот каталог задается в константа HPC_DependsFiles hello в макрос VBA hello.
10. Книга hello toorun hello кластере в Azure, щелкните hello **кластера** кнопку на листе hello.

### <a name="run-excel-udfs"></a>Выполнение пользовательских функций Excel
toorun UDF Excel следуйте hello предыдущих шагах 1 – 3 tooset копирование hello клиентского компьютера. Для определяемых пользователем функций Excel не требуется на вычислительных узлах установлено приложение Excel toohave hello. Поэтому при создании кластера вычислительных узлов, можно выбрать образ обычный вычислительного узла вместо hello вычислений изображение узла с помощью Excel.

> [!NOTE]
> Имеется 34 знаков в hello Excel 2010 и 2013 диалоговое окно соединитель кластера. Использовании этого диалогового окна поле toospecify hello кластера под управлением hello определяемые пользователем функции. Если длиннее hello полное имя кластера (например, hpcexcelhn01.southeastasia.cloudapp.azure.com), не помещается в диалоговое окно «hello». Hello решение — tooset переменной компьютера, такие как *CCP_IAASHN* со значением hello hello кластера длинное имя. Затем введите *% CCP_IAASHN %* в диалоговом окне приветствия как hello имя головного узла кластера. 
> 
> 

После успешно развернут кластер hello, выполните следующие шаги toorun hello встроенный образец определяемой пользователем функции в Excel. Настраиваемые пользовательские функции Excel, просмотрите эти [ресурсов](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL и их развертывание в кластере IaaS hello.

1. Откройте новую книгу Excel. На hello **разработка** ленты, нажмите кнопку **надстройки**. В диалоговом окне приветствия нажмите кнопку **Обзор**, перейдите в папку %CCP_HOME%Bin\XLL32 toohello и выберите образец hello ClusterUDF32.xll. Если hello ClusterUDF32 не существует на компьютере клиента hello, скопируйте его из папки %CCP_HOME%Bin\XLL32 hello на головном узле hello.
   
   ![Выберите hello определяемой пользователем функции.][udf]
2. Щелкните **Файл** > **Параметры** > **Дополнительно**. В разделе **формулы**, проверьте **разрешить определяемой пользователем функции toorun XLL вычислительного кластера**. Нажмите кнопку **параметры** и введите hello полное имя кластера в **имя головного узла кластера**. (Как отмечено выше ранее это поле является ограниченной too34 символов, так много имя_кластера может не поместиться. Здесь для длинного имени кластера можно использовать переменную уровня компьютера.)
   
   ![Настройка hello определяемой пользователем функции.][options]
3. Щелкните ячейку hello с =XllGetComputerNameC() значение toorun hello вычисления определяемой пользователем функции в кластере hello и нажмите клавишу ВВОД. функция Hello просто получает имя hello hello вычислительных узлов, на какие hello определяемая пользователем Функция выполняется. Диалоговое окно учетных данных для первого запуска hello, запрашивает hello имя пользователя и пароль tooconnect toohello IaaS кластера.
   
   ![Запуск пользовательской функции][run]
   
   После многих toocalculate ячейки нажмите клавишу Alt, Shift, Ctrl + F9 toorun hello вычисления всех ячеек.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Шаг 3. Запуск рабочей нагрузки SOA из локального клиента
Сначала toorun Общие приложения SOA в кластере IaaS пакета HPC hello, используйте один из методов hello в кластере hello toodeploy шаг 1. В этом случае укажите образ универсального вычислительного узла, так как не требуется Excel на вычислительных узлах hello. Затем выполните следующие действия.

1. После получения сертификата кластера hello, импортируйте его на клиентском компьютере hello в Cert: \CurrentUser\Root.
2. Установка hello [HPC Pack 2012 R2 обновление 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) и [HPC Pack 2012 R2 с обновлением 3 клиентские служебные программы](https://www.microsoft.com/download/details.aspx?id=49923). Эти средства позволяют toodevelop и запустите SOA клиентских приложений.
3. Загрузите hello HelloWorldR2 [пример кода](https://www.microsoft.com/download/details.aspx?id=41633). Откройте hello HelloWorldR2.sln в Visual Studio 2010 или 2012. (В настоящее время этот пример несовместим с более поздними версиями Visual Studio.)
4. Первая сборка проекта EchoService hello. Разверните кластер IaaS toohello службы hello в hello так же, как tooan локального кластера. Подробные инструкции см. в разделе hello readme.doc для в HelloWordR2. Изменение и выполнение сборки hello HellWorldR2 и в других проектах, как описано в следующий раздел toogenerate hello SOA клиентских приложений, работающих на кластере Azure IaaS hello.

### <a name="use-http-binding-with-azure-storage-queue"></a>Использование привязки HTTP с очередью хранилища Azure
Привязка Http toouse с очередь хранилища Azure внести некоторые изменения, toohello образец кода.

* Обновите имя кластера hello.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* При необходимости использовать по умолчанию hello TransportScheme в SessionStartInfo или явно задать tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Используйте привязку по умолчанию для hello BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Или явно с помощью hello basicHttpBinding.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* При необходимости задайте tootrue флаг UseAzureQueue hello в SessionStartInfo. В противном случае набор, оно будет иметь значение tootrue по умолчанию при суффиксы доменов Azure имеет имя кластера hello и hello TransportScheme Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Использование привязки HTTP без очереди хранилища Azure
Привязка Http toouse без очередь хранилища Azure, а явно набор hello UseAzureQueue флаг toofalse в hello SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Использование привязки NetTcp
toouse NetTcp hello конфигурации привязки, — примерно tooconnecting tooan локального кластера. Необходимо tooopen несколько конечных точек на ВМ головного узла hello. Если используется кластер hello toocreate скрипт развертывания hello IaaS пакета HPC, например, установке конечных точек hello в hello портал Azure следующим образом.

1. Остановите hello виртуальной Машины.
2. Добавьте TCP-порты hello 9090, 9087, 9091, 9094 для сеанса, hello компонента Service Broker, соответственно брокера рабочего процесса и службы данных
   
    ![Настройка конечных точек][endpoint-new-portal]
3. Запустите hello виртуальной Машины.

Hello SOA клиентское приложение не требует изменений за исключением изменения hello головного toohello IaaS кластера полное имя.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о запуске рабочих нагрузок Excel с помощью пакета HPC см. в [этих ресурсах](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx).
* Дополнительные сведения о развертывании служб SOA и управлении ими с помощью пакета HPC см. в статье [Управление службами SOA в пакете Microsoft HPC](https://technet.microsoft.com/library/ff919412.aspx).

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
