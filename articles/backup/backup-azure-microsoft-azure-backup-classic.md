---
title: "aaaUse tooback Azure резервное копирование рабочих нагрузок tooAzure классического портала | Документы Microsoft"
description: "Убедитесь, что в вашей среде надлежащим образом подготовлена tooback копирование рабочих нагрузок, используя сервер резервного копирования Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "сервер службы архивации Azure; хранилище службы архивации"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Подготовка tooback копирование рабочих нагрузок, используя сервер резервного копирования Azure
> [!div class="op_single_selector"]
> * [Сервер службы архивации Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Сервер службы архивации Azure (классическая модель)](backup-azure-microsoft-azure-backup-classic.md)
> * [Диспетчер SCDPM (классическая модель)](backup-azure-dpm-introduction-classic.md)
>
>

Эта статья является о подготовке вашей среды tooback копирование рабочих нагрузок, используя сервер резервного копирования Azure. Используя сервер службы архивации Azure, вы можете создавать резервные копии рабочих нагрузок приложения, таких как виртуальные машины Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange и клиенты Windows, с помощью единой консоли.

> [!WARNING]
> Резервное копирование Azure сервера наследует функциональные возможности hello Data Protection Manager (DPM) для резервного копирования рабочей нагрузки. Вы найдете указатели tooDPM документации для некоторых из этих возможностей. Однако сервер службы архивации Azure не обеспечивает защиту данных с помощью ленточных накопителей и не интегрируется с System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Компьютер Windows Server
![Шаг 1](./media/backup-azure-microsoft-azure-backup/step1.png)

Hello первым шагом к начало hello Azure Backup Server и запуск — toohave компьютере с Windows Server.

| Расположение | Минимальные требования | Дополнительные инструкции |
| --- | --- | --- |
| Таблицы Azure |Виртуальная машина IaaS Azure<br><br>Standard A2: 2 ядра, 3,5 ГБ ОЗУ |Можно начать с простого образа коллекции центра обработки данных Windows Server 2012 R2. [Защита рабочих нагрузок IaaS с помощью сервера службы архивации Azure (DPM)](https://technet.microsoft.com/library/jj852163.aspx) имеет свои особенности. Убедитесь, что статьи hello полностью прочитать перед развертыванием машины hello. |
| Локальная система |Виртуальная машина Hyper-V,<br> виртуальная машина VMware<br> или физический узел<br><br>2 ядра и 4 ГБ ОЗУ |Можно дедупликация хранилища DPM hello, с помощью Дедупликация Windows Server. См. дополнительные сведения об использовании [DPM и дедупликации](https://technet.microsoft.com/library/dn891438.aspx) при развертывании на виртуальных машинах Hyper-V. |

> [!NOTE]
> Рекомендуется установить сервер службы архивации Azure на компьютере с центром обработки данных Windows Server 2012 R2. Большой объем необходимых компонентов hello автоматически рассматриваются hello последней версии операционной системы Windows hello.
>
>

Если планируется toojoin Azure Backup Server tooa домена, рекомендуется присоединить hello физический сервер или виртуальной машины toohello домена перед установкой программного обеспечения hello Azure Backup Server. Перемещение сервера резервного копирования Azure tooa новый домен, после развертывания — *не поддерживается*.

## <a name="2-backup-vault"></a>2. Хранилище службы архивации
![Шаг 2](./media/backup-azure-microsoft-azure-backup/step2.png)

Отправить tooAzure резервного копирования данных или сохранить его локально, hello резервное копирование Azure должен ли хранилище зарегистрированного tooa. Если новый пользователь Azure Backup и требуется toouse резервное копирование Azure, в разделе hello Azure портала версию этой статьи — [Подготовка tooback копирование рабочих нагрузок, используя сервер резервного копирования Azure](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> Запуск марта 2017 г., можно использовать больше не hello классического портала toocreate резервное копирование хранилищ.
> Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии. Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md). Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.<br/> После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ. **К 1 ноября 2017 года**:
>- Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.
>- Вы не будет возможности tooaccess данные резервной копии hello классического портала. Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.
>



## <a name="3-software-package"></a>3. Программный пакет
![Шаг 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Загрузка пакета программного обеспечения hello
Аналогичные toovault учетные данные, вы можете загрузить службы архивации Microsoft Azure для рабочих нагрузок приложений из hello **"Быстрый запуск"** hello резервного хранилища.

1. Нажмите кнопку **для рабочих нагрузок приложений (диск tooDisk tooCloud)**. Это займет toohello страницы центра загрузки, из которой можно загрузить пакет программного обеспечения hello.

    ![Резервное копирование Microsoft Azure: экран приветствия](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Щелкните элемент **Загрузить**.

    ![Центр загрузки 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Выберите все файлы hello и нажмите кнопку **Далее**. Здравствуйте, все файлы, поступающие из страницу загрузки Microsoft Azure Backup hello загрузки и месте, в котором все hello файлы в hello одной папке.
   ![Центр загрузки 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Поскольку hello размер всех файлов hello вместе > 3G, на ссылку для загрузки 10 Мбит/с может занять too60 минут hello Загрузите toocomplete.

### <a name="extracting-hello-software-package"></a>Извлечение пакета программного обеспечения hello
После загрузки всех файлов hello, нажмите кнопку **MicrosoftAzureBackupInstaller.exe**. Это приведет к запуску hello **мастер установки Microsoft Azure Backup** файлы установки hello tooextract tooa расположении, указанном пользователем. Продолжайте работу мастера hello и щелкнет hello **извлечь** кнопку toobegin процесс извлечения hello.

> [!WARNING]
> По крайней мере 4 ГБ свободного места — файлы программы установки требуется tooextract hello.
>
>

![мастер установки службы архивации Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Один раз полный процесс извлечения hello, проверка hello поле toolaunch hello недавно извлечены *setup.exe* toobegin установки Microsoft Azure Backup Server и выберите команду hello **Готово** кнопки.

### <a name="installing-hello-software-package"></a>Установка пакета программного обеспечения hello
1. Нажмите кнопку **архивации Microsoft Azure** мастер установки toolaunch hello.

    ![мастер установки службы архивации Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. На экране приветствия hello щелкните hello **Далее** кнопки. После этого вы перейдете toohello *Prerequisite Checks* раздела. На этом экране щелкните hello **проверки** кнопку toodetermine, если выполнены hello оборудованию и программному обеспечению для сервера Azure Backup. Если все компоненты являются приветствия выполнены успешно, появится сообщение, указывающее, что машины hello требованиям hello. Щелкните hello **Далее** кнопки.

    ![Сервер службы архивации Azure — приветствие и проверка готовности](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure Backup Server требуется SQL Server Standard, а пакет установки hello Azure Backup Server предусмотрен объединенной hello соответствующие SQL Server двоичные файлы, необходимые. При новой установке сервера резервного копирования Azure, необходимо выбрать параметр hello **установки нового экземпляра SQL Server с помощью этой программы** и нажмите кнопку hello **проверить и установить** кнопки. После успешной установки необходимых компонентов hello, нажмите кнопку **Далее**.

    ![Сервер службы архивации Azure — проверка SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Если происходит сбой с компьютером рекомендацию toorestart hello, сделать это и нажмите кнопку **проверку**.

   > [!NOTE]
   > Сервер службы архивации Azure не поддерживает использование удаленного экземпляра SQL Server. экземпляр Hello используется сервером резервного копирования Azure должен toobe локальной.
   >
   >

4. Укажите расположение для установки hello файлов сервера архивации Microsoft Azure и нажмите кнопку **Далее**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    расположение для вспомогательной Hello является обязательным для резервного копирования tooAzure. Убедитесь, что расположение временных файлов hello — минимум 5% данных hello планового резервного копирования облака toohello toobe. Для защиты диска отдельные диски должны настроить после завершения установки hello toobe. Дополнительные сведения о пулах носителей см. в статье [Настройка пулов носителей и дискового хранилища](https://technet.microsoft.com/library/hh758075.aspx).
5. Введите надежный пароль для локальных учетных записей пользователей с ограниченными правами и нажмите кнопку **Далее**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Выберите, следует ли использовать toouse *центра обновления Майкрософт* toocheck для обновления и нажмите кнопку **Далее**.

   > [!NOTE]
   > Мы советуем перенаправления tooMicrosoft обновления, что имеются обновления безопасности и важные обновления для Windows и других продуктов, таких как Microsoft Azure Backup Server центра обновления Windows.
   >
   >

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Просмотрите hello *Сводка настроек* и нажмите кнопку **установить**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. Hello установки происходит поэтапно. В первый этап hello hello агента служб восстановления Microsoft Azure установлен на сервере hello. Hello мастер также проверяет возможность подключения к Интернету. При наличии подключения к Интернету можно продолжить установку, в противном случае необходимо tooconnect-toohello сведения tooprovide прокси-сервера Интернета.

    Hello следующим шагом является tooconfigure hello агента служб восстановления Microsoft Azure. Как часть конфигурации hello вы должны будете tooprovide hello хранилище учетных данных tooregister hello машины toohello резервного хранилища. Будет необходимо также указать данные hello tooencrypt и расшифровки парольную фразу, передаваемые между Azure и локальной. Вы можете сгенерировать парольную фразу автоматически или ввести ее вручную. Она должна включать не менее 16 символов. Продолжайте работу с мастером hello, пока hello агент был настроен.

    ![PreReq2 сервера службы архивации Azure](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. После успешного завершения регистрации сервера архивации Microsoft Azure hello hello общую мастер установки продолжает работу toohello установки и настройки SQL Server и компоненты Azure Backup Server hello. После завершения установки компонентов SQL Server hello hello Azure Backup не установлены компоненты сервера.

    ![Сервер службы архивации Azure](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

По завершении шага установки hello hello значки рабочего стола продукта будет создано также. Дважды щелкните hello значок toolaunch hello продукта.

### <a name="add-backup-storage"></a>Добавление хранилища службы архивации
Hello первая резервная копия хранится на подключенном хранилище toohello машины сервер службы архивации Azure. Дополнительные сведения о добавлении дисков см. в статье [Настройка пулов носителей и дискового хранилища](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Необходимо tooadd хранения резервных копий, даже если планируется tooAzure toosend данных. В текущей архитектуре hello резервного копирования сервера Azure, Azure резервного хранилища hello содержит hello *второй* копия данных hello, а hello локальное хранилище содержит hello первый (и обязательна) резервной копии.  
>
>

## <a name="4-network-connectivity"></a>4. Сетевое подключение
![Шаг 4](./media/backup-azure-microsoft-azure-backup/step4.png)

Сервер резервного копирования Azure требует подключения toohello службы архивации Azure для hello toowork продукта успешно. toovalidate ли компьютер hello имеет tooAzure подключения hello, использовать hello ```Get-DPMCloudConnection``` командлет в консоли сервера резервного копирования Azure PowerShell hello. Если hello выходные данные командлетов для hello имеет значение TRUE, то существует подключение, в противном случае отсутствует подключение.

В hello одновременно hello подписки Azure должен toobe в работоспособном состоянии. toofind out hello состояние подписки и toomanage его вход toohello [портала подписки](https://account.windowsazure.com/Subscriptions).

Узнав hello состояние подключения к Azure hello и hello подписки Azure, воспользуйтесь таблицей hello ниже toofind out hello влияние на функции резервного копирования и восстановления hello, предоставляемой.

| Состояние подключения | Подписка Azure | TooAzure резервного копирования | Toodisk резервного копирования | Восстановление из Azure | Восстановление с диска |
| --- | --- | --- | --- | --- | --- |
| Подключено |Активна |Разрешено |Разрешено |Разрешено |Разрешено |
| Подключено |Срок действия истек |Остановлено |Остановлено |Разрешено |Разрешено |
| Подключено |Отозвана |Остановлено |Остановлено |Остановлено; точки восстановления Azure удалены |Остановлено |
| Подключение потеряно на 15 и более дней |Активна |Остановлено |Остановлено |Разрешено |Разрешено |
| Подключение потеряно на 15 и более дней |Срок действия истек |Остановлено |Остановлено |Разрешено |Разрешено |
| Подключение потеряно на 15 и более дней |Отозвана |Остановлено |Остановлено |Остановлено; точки восстановления Azure удалены |Остановлено |

### <a name="recovering-from-loss-of-connectivity"></a>Восстановление после потери подключения
Если у вас есть брандмауэр или прокси-сервера, не является tooAzure доступ, необходимо toowhitelist hello следующие адреса домена в профиле hello брандмауэра или прокси-сервера:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

После подключения к tooAzure машины восстановленного toohello резервное копирование Azure, hello операции, которые могут быть выполнены определяются hello состояния подписки Azure. Hello приведенной выше таблице содержит сведения об операциях hello допускается после машины hello «подключения».

### <a name="handling-subscription-states"></a>Сведения о состояниях подписки
Это подписка Azure из возможных tootake *истек* или *Deprovisioned* toohello состояние *Active* состояния. Однако это влияет на некоторые на поведение продукта hello хотя состояние hello не *Active*:

* Объект *Deprovisioned* подписки утрачивает функции hello период, который выполняется отмена ее провизионирования. На включение *Active*, восстановлен hello продукта функциональные возможности резервного копирования и восстановления. Hello резервного копирования данных на локальном диске hello также можно получить, если оно было сохранено с достаточно большой период удержания. Тем не менее, безвозвратно потеряны hello резервного копирования данных в Azure после hello подписка переходит hello *Deprovisioned* состояния.
* Если подписка находится в состоянии *Срок действия истек*, функциональные возможности теряются только до восстановления состояния *Активная*. Все резервные копии запланированного периода hello, hello подписки был *истек* не запустится.

## <a name="troubleshooting"></a>Устранение неполадок
В случае сбоя сервера службы архивации Microsoft Azure с ошибками во время этапа установки hello (или backup или restore) ссылаться toothis [ошибка кодов документов](https://support.microsoft.com/kb/3041338) для получения дополнительной информации.
Можно также ссылаться слишком[часто задаваемые вопросы, связанные с Azure Backup](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Дальнейшие действия
Можно получить подробные сведения о [Подготовка среды для DPM](https://technet.microsoft.com/library/hh758176.aspx) на сайте Microsoft TechNet hello. На этом сайте также содержатся сведения о поддерживаемых конфигурациях, при которых можно развернуть и использовать сервер службы архивации Azure.

Можно использовать эти статьи toogain более глубокого понимания защита рабочей нагрузки с помощью сервера архивации Microsoft Azure.

* [Резервное копирование сервера SQL Server](backup-azure-backup-sql.md)
* [Резервное копирование сервера SharePoint](backup-azure-backup-sharepoint.md)
* [Резервное копирование альтернативного сервера](backup-azure-alternate-dpm-server.md)
