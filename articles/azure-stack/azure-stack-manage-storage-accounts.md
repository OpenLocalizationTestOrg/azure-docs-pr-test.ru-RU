---
title: "учетные записи хранения Azure стека aaaManage | Документы Microsoft"
description: "Узнайте, как toofind, управление, восстановление и освободить учетных записей хранилища Azure стека"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a>Управление учетными записями хранения в стек Azure
Узнайте, как восстановить toomanage учетные записи хранения в toofind стека Azure и освобождения пространства хранения, исходя из потребностей бизнеса.

## <a name="find"></a>Найти учетную запись хранения
список учетных записей хранения в регионе hello Hello можно просмотреть в Azure стека с помощью:

1. В веб-браузер перейдите к https://adminportal.local.azurestack.external.
2. Войдите в toohello портала администрирования Azure стека как оператор облака (с использованием учетных данных, предоставленные во время развертывания)
3. На панели мониторинга по умолчанию hello — найти hello **область управления** списке и нажмите кнопку область hello требуется tooexplore. Например **(локальный**).
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. Выберите **хранения** из hello **поставщиков ресурсов** списка.
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. Теперь, в колонке администратора поставщика ресурсов хранилища hello – прокрутите вниз до hello **учетные записи хранения** и щелкните его.
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   Полученная страница Hello — hello список учетных записей хранения в этом регионе.
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

По умолчанию hello первые 10 отображаются учетные записи. Вы можете toofetch несколько, щелкнув hello **дополнительной загрузки** ссылке hello нижней части списка hello.

ИЛИ

Если вы заинтересованы в определенной учетной записи хранения — вы можете **фильтра и fetch hello соответствующие счета** только.


**toofilter для учетных записей:**

1. Нажмите кнопку **фильтра** hello верхней части колонки hello.
2. В колонке hello фильтр, он позволяет toospecify **имя учетной записи**, **идентификатор подписки** или **состояние** список hello toofine настройки хранилища учетных записей toobe отображается. Используйте их соответствующим образом.
3. Нажмите кнопку **Обновить**. Обновление списка Hello следует соответствующим образом.
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. Фильтр hello tooreset: щелкните **фильтра**, очистить выбранные элементы и обновлять.

поле поиска Hello (на hello в верхней части колонки список учетных записей хранилища hello) позволяет выделять hello выбран текст hello список учетных записей. Это очень удобно в случае hello в тех случаях, когда hello полное имя или идентификатор не легко доступны.

Можно использовать произвольный текст здесь toohelp найти hello учетной записи, которые вас интересуют.

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a>Просмотрите сведения об учетной записи
После нахождения hello учетных записей, что вы заинтересованы в просмотре можно щелкнуть tooview hello определенную учетную запись некоторые сведения. Новая колонка открывается с hello учетные данные, такие как: hello тип учетной записи hello, время создания, расположение, и т. д.

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a>Восстановление удаленной учетной записи
В ситуации, когда необходимо toorecover может быть удаленной учетной записи.

В стеке Azure является toodo очень простым способом:

1. Просмотрите список учетных записей хранилища toohello. В разделе [найти учетную запись хранения](#find) в этом разделе для получения дополнительной информации.
2. Найти этой конкретной учетной записи в списке hello. Может потребоваться toofilter.
3. Проверьте hello *состояние* hello учетной записи. Должно быть указано **Deleted**.
4. Выберите учетную запись hello, который открывает колонку сведения учетной записи hello.
5. На основе этой колонки найдите hello **восстановить** кнопку и щелкните его.
6. Нажмите кнопку **Да** tooconfirm.
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. Hello восстановления находится в *обработать... Подождите* для указывает на то, что она выполнена успешно.
   Можно также щелкнуть значок «звонка» hello вверху hello hello портал, чтобы просмотреть ход выполнения указаний.
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   После восстановления hello учетная запись успешно синхронизирован, он может использоваться повторно.

### <a name="some-gotchas"></a>Некоторые проблемы
* Учетной записи удаленных отобразится состояние в качестве **за пределы хранения**.
  
  Это означает, что учетная запись удалена hello hello срок хранения превысил и не может быть восстановлен.
* Ваш удаленной учетной записи не отображается в списке учетных записей hello.
  
  Это может означать hello удалена учетная запись уже была сбора мусора. В этом случае его будет невозможно. В разделе [освобождения пространства](#reclaim) в этом разделе.

## <a name="set-hello-retention-period"></a>Настроить срок хранения hello
Настройка срока хранения Hello позволяет toospecify оператор облако период времени в днях (от 0 до 9999 дней) во время любой удаленной учетную запись, которая потенциально может быть восстановлен. Hello срок хранения по умолчанию имеет значение too15 дней. Установка значения hello слишком «0» означает, что любой удаленной учетной записи немедленно выходит за хранение и помеченных для периодическую сборку мусора.

**срок хранения toochange hello:**

1. В веб-браузер перейдите к https://adminportal.local.azurestack.external.
2. Войдите в toohello портала администрирования Azure стека как оператор облака (с использованием учетных данных, предоставленные во время развертывания)
3. На панели мониторинга по умолчанию hello — найти hello **область управления** списке и нажмите кнопку область hello требуется tooexplore — например **(локальный**).
4. Выберите **хранения** из hello **поставщиков ресурсов** списка.
5. Нажмите кнопку **параметры** в колонке параметр hello top tooopen hello.
6. Нажмите кнопку **конфигурации** измените значение срока хранения hello.

   Задайте hello количество дней, а затем сохраните его.
   
   Это значение немедленно и задать для всего региона.

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a>Освобождения пространства
Одна из hello побочные эффекты с периодом хранения — что удаленной учетной записи продолжается tooconsume емкости, пока они поступают из срока хранения hello. Как облако оператора, может потребоваться hello tooreclaim способом удален места учетной записи, хотя еще не истек срок хранения hello.

Емкость можно освободить с помощью портала hello или PowerShell.

**емкость tooreclaim с помощью портала hello:**
1. Перейдите в колонку учетные записи хранения toohello. В разделе [найти учетную запись хранения](#find).
2. Нажмите кнопку **освобождения пространства** hello верхней части колонки hello.
3. Прочтите сообщение hello и нажмите кнопку **ОК**.

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. Дождитесь значок колокольчика hello см. в разделе уведомления успеха на портале hello.

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. Обновите страницу учетных записей хранилища hello. Hello удалены учетные записи больше не отображаются в списке hello, так как они были удалены.

Можно также использовать PowerShell tooexplicitly переопределение hello срок и немедленно освобождения пространства.

**емкость tooreclaim с помощью PowerShell:**   

1. Убедитесь, что Azure PowerShell установлен и настроен. В противном случае используется hello, следуя инструкциям: 
   * tooinstall hello последнюю версию Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).
   Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)
2. Выполните следующий командлет hello.

> [!NOTE]
> При выполнении этого командлета можно удалить без возможности восстановления hello учетной записи и ее содержимое. Восстановить его будет невозможно. Это следует используйте с осторожностью.


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


Дополнительные сведения см. в разделе слишком[документацию по powershell Azure стека.](https://msdn.microsoft.com/library/mt637964.aspx)
 

## <a name="migrate-a-container"></a>Перенос контейнера
Из-за toouneven хранилища, используемые клиентами оператор облако может найти один или более базовых клиента общих папок с помощью больше места, чем другие. В этом случае оператор облака hello может попытаться выполнить toofree достаточно места на общем ресурсе нагрузкой hello путем переноса некоторые папки tooanother контейнеров больших двоичных объектов вручную. 

Необходимо использовать контейнеры toomigrate PowerShell.
> [!NOTE]
>Миграция контейнер больших двоичных объектов не поддерживает динамическую миграцию и в настоящее время является операцией вне сети. Во время миграции и до завершения hello базового BLOB-объектов в этом контейнере не может использоваться и «вне сети». 

**toomigrate контейнеры с помощью PowerShell.**

1. Убедитесь, что Azure PowerShell установлен и настроен. В противном случае используется hello, следуя инструкциям:
    * tooinstall hello последнюю версию Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/). Дополнительные сведения о командлетах Azure Resource Manager см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkId=394767)
2. Получите имя фермы hello: 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. Получите общие папки hello: 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. Получите контейнеры hello для одного общего ресурса. Обратите внимание, что количество и намерением необязательные параметры:
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   Затем проверьте $containers:

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. Получите hello, наиболее общие папки назначения для миграции hello контейнера:

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    Затем проверьте $destinationshares:

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. Начнем миграции для контейнера, обратите внимание, что это реализацию async, поэтому можно использовать один цикл все контейнеры общими ресурсами и отслеживать состояние hello, с помощью идентификатора задания, возвращаемый hello.

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    Затем проверьте $jobId:

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. Проверьте состояние задания миграции hello по идентификатору задания. По завершении миграции контейнера hello MigrationStatus задано слишком «завершение».

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. Вы можете отменить задание миграции в процессе выполнения. Это является асинхронной операцией и могут отслеживаться с помощью $jobid еще раз:

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    Можно проверить состояние hello hello отмены миграции еще раз:

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  