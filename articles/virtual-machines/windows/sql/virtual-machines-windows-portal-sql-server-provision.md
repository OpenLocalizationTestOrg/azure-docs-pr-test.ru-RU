---
title: "aaaProvision виртуальной машины SQL Server | Документы Microsoft"
description: "Создание и подключение виртуальной машины в Azure с помощью портала hello tooa SQL Server. В этом учебнике используется режим диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Подготовьте виртуальную машину SQL Server в hello портал Azure
> [!div class="op_single_selector"]
> * [Портал](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Этот учебник для начала до конца показано, как toouse hello Azure портала tooprovision виртуальной машины под управлением SQL Server.

Коллекция Hello Azure виртуальной машины (VM) содержит несколько образов, содержащих Microsoft SQL Server. С помощью нескольких щелчков можно выбрать одно из изображений SQL виртуальной Машины из коллекции hello приветствия и ее подготовки в вашей среде Azure.

Изучив данный учебник, вы научитесь:

* [Выберите образ виртуальной Машины SQL из коллекции hello](#select-a-sql-vm-image-from-the-gallery)
* [Настройка и создание hello виртуальной Машины](#configure-the-vm)
* [Открыть hello виртуальной Машины с помощью удаленного рабочего стола](#open-the-vm-with-remote-desktop)
* [Удаленное подключение tooSQL сервера](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Выберите образ виртуальной Машины SQL из коллекции hello

1. Войдите в toohello [портал Azure](https://portal.azure.com) под своей учетной записью.

   > [!NOTE]
   > Если у вас нет учетной записи Azure, используйте [бесплатную пробную версию Azure](https://azure.microsoft.com/pricing/free-trial/).

2. Щелкните hello портал Azure, **New**. Откроется портал Hello hello **New** окна.

3. В hello **New** окно, нажмите кнопку **вычислений** и нажмите кнопку **все**.

   ![Окно "Новое вычисление"](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. Введите в поле поиска hello **SQL Server**, и нажмите клавишу ВВОД.

5. Нажмите кнопку hello **фильтра** значок и выберите **Microsoft** для hello издателя. Нажмите кнопку **сделать** на результаты hello toofilter окна фильтрации hello tooMicrosoft опубликованных образов SQL Server.

   ![Окно "Виртуальные машины Azure"](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Просмотрите hello доступных образов SQL Server. Каждый образ определяет версию SQL Server и операционную систему.

6. Выберите hello изображение с именем **бесплатная лицензия: SQL Server 2016 Developer с пакетом обновления 1 в Windows Server 2016**.

   > [!TIP]
   > в этом учебнике используется Hello Developer edition, так как это полнофункциональный выпуск SQL Server, предоставляется бесплатно для разработки приложений в целях тестирования. Вы платите только за hello стоимость выполнения hello виртуальной Машины. Однако, свободного toochoose любой toouse hello изображения в этом учебнике.

   > [!TIP]
   > Образы виртуальных Машин SQL включить hello стоимости лицензирования для SQL Server в hello / мин стоимости hello виртуальной Машине, созданной (за исключением hello Developer, экспресс-выпуск и версии). Выпуск SQL Server Developer предоставляется бесплатно для разработки и тестирования (не для рабочей среды), а выпуск SQL Express предоставляется бесплатно для упрощенных рабочих нагрузок (требующих менее 1 ГБ памяти и 10 ГБ хранилища). Имеется другой параметр toobring--владельцем лицензии (BYOL) и оплата только для hello виртуальной Машины. Имена таких образов содержат префикс {BYOL}. 
   >
   > Дополнительные сведения об этих параметрах см. в [руководстве по выбору ценовой категории для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

7. В разделе **Выбор модели развертывания** выберите **Resource Manager**. Диспетчер ресурсов — hello, рекомендуется использовать модель развертывания для новых виртуальных машин. 

8. Щелкните **Создать**.

    ![Создание виртуальной машины SQL с помощью Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Настройка hello виртуальной Машины
Есть пять окон для настройки виртуальной машины SQL Server.

| Шаг | Описание |
| --- | --- |
| **Основы** |[Настройка основных параметров](#1-configure-basic-settings) |
| **Размер** |[Выбор размера виртуальной машины](#2-choose-virtual-machine-size) |
| **Параметры** |[Настройка дополнительных возможностей](#3-configure-optional-features) |
| **Параметры SQL Server** |[Настройка параметров SQL Server](#4-configure-sql-server-settings) |
| **Сводка** |[Просмотрите hello сводки](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Настройка основных параметров.

На hello **основы** окна, предоставляют hello следующую информацию:

* Введите уникальное **имя**виртуальной машины.

* Для оптимальной производительности выберите **SSD** в качестве типа диска виртуальной машины.

* Укажите **имя пользователя** hello учетной записи локального администратора на hello виртуальной Машины. Эта учетная запись также добавляется toohello SQL Server **sysadmin** предопределенной роли сервера.

* Введите надежный **пароль**.

* Если у вас несколько подписок, проверьте правильность hello подписки для hello новой виртуальной Машины.

* В hello **группы ресурсов** введите имя для новой группы ресурсов. Кроме того, toouse существующую группу ресурсов щелкните **использовать существующие**. Группа ресурсов — это коллекция связанных ресурсов в Azure (виртуальные машины, учетные записи хранения, виртуальные сети и т. д.).

  > [!NOTE]
  > Рекомендуется использовать новую группу ресурсов для тестирования или изучения процесса развертывания SQL Server в Azure. После завершения теста, удалите hello hello ресурсов группы tooautomatically удаления виртуальной Машины и все ресурсы, связанные с данной группой ресурсов. Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Выберите **расположение** для hello регион Azure, где будет размещаться этого развертывания.

* Нажмите кнопку **ОК** toosave hello параметры.

    ![Окно "Общие сведения об SQL"](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2) Выбор размера виртуальной машины.

На hello **размер** действии, выберите размер виртуальной машины в hello **выберите размер** окна. окно Hello сначала отображает размеры рекомендуемые машины, в зависимости от выбранного изображения hello.

> [!IMPORTANT]
> Hello предполагаемое месячные затраты на hello **выберите размер** окна не включает стоимость лицензирования SQL Server. Это стоимость hello hello виртуальной Машины отдельно. Hello Express Edition и Developer Edition сервера SQL Server это итоговая оценочная стоимость hello. Для других выпусков см hello [страница цен в виртуальных машинах](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) и выберите целевой выпуск SQL Server. См. также hello [цены рекомендации для виртуальных машин Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

![Варианты размеров виртуальной машины SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Для рабочих нагрузок см hello рекомендуемые размеры машины и конфигурации в [рекомендации по производительности для SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md). Если требуется, чтобы размер машины, который отсутствует в списке, нажмите кнопку hello **просмотра всех** кнопки.

> [!NOTE]
> Дополнительную информацию о размерах виртуальных машин см. в статье [Размеры виртуальных машин](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Укажите размер машины и нажмите кнопку **Выбрать**.

## <a name="3-configure-optional-features"></a>3. Настройка дополнительных возможностей

На hello **параметры** окна, Настройка хранилища Azure, сети и наблюдение за hello виртуальной машины.

* В разделе **Хранилище** выберите **Да** возле параметра "Использование **управляемых дисков**".

   > [!NOTE]
   > Корпорация Майкрософт рекомендует использовать управляемые диски для SQL Server. Управлять дисками управляет хранилищем фоновом hello. Кроме того, когда виртуальные машины с дисками управляемых находятся в hello одной группе доступности Azure распределяет соответствующие избыточности ресурсы хранилища tooprovide hello. Дополнительные сведения см. в [обзоре управляемых дисков Azure](../../../storage/storage-managed-disks-overview.md). Подробные сведения об управляемых дисках в группе доступности см. в статье [Управление доступностью виртуальных машин Windows в Azure](../manage-availability.md).

* В разделе **сети**, может принимать значения hello заполнено автоматически. Также можно щелкнуть каждый компонент toomanually Настройка hello **виртуальная сеть**, **подсети**, **общедоступный IP-адрес**, и **группы безопасности сети**. Для целей этого учебника hello оставьте значения по умолчанию hello.

* Azure позволяет **мониторинг** по умолчанию с одной учетной записи хранилища, предназначенные для hello ВМ hello. Эти параметры можно изменить.

* В разделе **набор доступности**, можно оставить значение по умолчанию hello **нет** для этого учебника. Если планируется tooset копирование группы доступности AlwaysOn SQL, Настройка hello доступности tooavoid воссоздание hello виртуальной машины.  Дополнительные сведения см. в разделе [hello Управление доступностью виртуальных машин](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Завершив настройку параметров, нажмите кнопку **OК**.

## <a name="4-configure-sql-server-settings"></a>4. Настройка параметров SQL Server
На hello **параметры SQL Server** окна, настроить определенные параметры и оптимизации для SQL Server. Hello параметры, которые можно настроить для SQL Server включают следующие hello.

| Настройка |
| --- |
| [Соединение](#connectivity) |
| [Аутентификация](#authentication) |
| [Конфигурация хранилища](#storage-configuration) |
| [Автоматическое исправление](#automated-patching) |
| [Автоматическая архивация](#automated-backup) |
| [Интеграция с хранилищем ключей Azure](#azure-key-vault-integration) |
| [Службы R](#r-services) |

### <a name="connectivity"></a>Соединение

В разделе **подключения SQL**, укажите тип hello доступа требуется экземпляр SQL Server toohello на этой виртуальной Машины. Для целей этого учебника hello, выберите **общей (Интернет)** tooSQL tooallow подключений сервера из машин или служб на hello Интернета. Этот параметр выбран Azure автоматически настраивает брандмауэр hello и трафик tooallow группы безопасности сети hello через порт 1433.

![Варианты подключений SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> По умолчанию сервер SQL Server ожидает передачи данных через стандартный порт **1433**. Для повышения безопасности измените номер порта hello в предыдущих toolisten диалоговое окно hello нестандартный порт, например 1401. После этого необходимо выполнить подключение, используя этот порт, с любого клиентского средства, например SSMS.

tooSQL tooconnect сервера через hello Интернета, также необходимо включить проверку подлинности SQL Server, который описан в следующем разделе hello.

Если вы предпочитаете toohello подключений toonot включить компонент Database Engine через Здравствуйте Интернета, выберите один из следующих вариантов hello:

* **Локальный (внутри ВМ)** tooSQL tooallow подключений сервера только из внутри hello виртуальной Машины.
* **Закрытый (в виртуальной сети)** tooSQL tooallow подключений сервера из машин или служб в hello одной виртуальной сети.

Как правило повышения безопасности, выбрав hello наиболее строгие взаимодействия, что сценарий позволяет. Но все параметры hello защищаемый через правил сетевой группы безопасности и проверки подлинности Windows или SQL. Группы безопасности сети можно изменить после hello создания виртуальной Машины. Дополнительные сведения см. в статье [Вопросы безопасности SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-security.md).

> [!NOTE]
> образ виртуальной машины Hello для SQL Server Express edition не происходит автоматического включения протокола hello TCP/IP. Это справедливо даже для hello подключение частных и общедоступных параметров. Для экспресс-выпуск, необходимо использовать диспетчер конфигурации SQL Server слишком[вручную включить протокол hello TCP/IP](#configure-sql-server-to-listen-on-the-tcp-protocol) после создания hello виртуальной Машины.

### <a name="authentication"></a>Аутентификация

Если требуется проверка подлинности SQL Server, выберите для параметра **Включить** under **Включить**.

![проверка подлинности SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Если планируется tooaccess SQL Server через hello Интернета (т. е. hello возможность подключения к общедоступным параметр), необходимо включить проверку подлинности SQL здесь. Общий доступ toohello SQL Server необходимо использовать hello проверки подлинности SQL.
> 
> 

Если вы включаете проверку подлинности SQL Server, укажите **имя для входа** и **пароль**. Это имя пользователя настроен в качестве имени входа для проверки подлинности SQL Server и членом hello **sysadmin** предопределенной роли сервера. Дополнительные сведения о режимах проверки подлинности см. в статье [Выбор режима проверки подлинности](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode).

Если не включить проверку подлинности SQL Server, можно использовать hello локальной учетной записи администратора на экземпляре SQL Server toohello tooconnect виртуальной Машины hello.

### <a name="storage-configuration"></a>Конфигурация хранилища

Нажмите кнопку **конфигурации хранилища** toospecify требования к хранилищу hello.

![Конфигурация хранилища SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Если вы вручную настроили стандартное хранилище toouse виртуальной Машины, этот параметр недоступен. Автоматическая оптимизация доступна только для хранилища класса Premium.

> [!TIP]
> Hello число останавливается и верхних пределов hello каждого ползунка зависит hello размер виртуальной Машины, которые вы выбрали. Виртуальная машина крупных и более мощных является может tooscale вверх.

Вы можете указать такие требования, как количество операций ввода-вывода в секунду (IOPs), пропускная способность в МБ/с и общий размер хранилища. Настройте эти значения с помощью hello скользящий шкал. Вы можете изменить эти параметры хранилища в зависимости от рабочей нагрузки. Hello портал автоматически вычисляет количество дисков tooattach hello и настроить в соответствии с этими требованиями.

В разделе **хранилища, обеспечивающее**, выберите один из следующих вариантов hello:

* **Общие** hello по умолчанию и поддерживает большинство рабочих нагрузок.
* **Транзакций** обработки оптимизирует хранение hello для рабочих нагрузок OLTP традиционных баз данных.
* **Хранение данных** оптимизирует хранение hello для рабочих нагрузок, анализа и создания отчетов.

### <a name="automated-patching"></a>Автоматическое исправление

**Automated patching** включен по умолчанию. Автоматических исправлений позволяет Azure tooautomatically исправление для SQL Server и hello операционной системы. Укажите день недели hello, время и длительность периода обслуживания. Azure устанавливает исправления в период обслуживания. расписание окна обслуживания Hello использует языковой стандарт hello виртуальной Машины для времени. Если требуется запретить Azure tooautomatically исправление для SQL Server и hello операционной системы, нажмите кнопку **отключить**.  

![Автоматическая установка исправлений SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Дополнительные сведения см. в статье [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Автоматическая архивация

Включите автоматическую архивацию для всех баз данных в разделе **Автоматическая архивация**. По умолчанию автоматическая архивация отключена.

При включении автоматической архивации SQL можно настроить следующие hello.

* срок хранения (в днях) для резервных копий;
* Toouse учетной записи хранилища для резервных копий
* параметр шифрования и пароль для резервных копий.
* архивация системных баз данных;
* настройка расписания архивации баз данных.

резервного копирования нажмите hello tooencrypt **включить**. Затем укажите hello **пароль**. Azure создает сертификат tooencrypt hello резервные копии с указанием hello использует tooprotect пароль сертификата.

![Автоматическая архивация SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Дополнительную информацию см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Интеграция с хранилищем ключей Azure

Щелкните toostore секретные данные безопасности в Azure для шифрования, **интеграции хранилища ключей Azure** и нажмите кнопку **включить**.

![Интеграция SQL с хранилищем ключей Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Hello следующей таблице перечислены необходимые tooconfigure параметры hello интеграция хранилища ключей Azure.

| ПАРАМЕТР | Описание | ПРИМЕР |
| --- | --- | --- |
| **URL-адрес хранилища ключей** |расположение хранилища ключей hello Hello. |https://contosokeyvault.vault.azure.net/ |
| **Имя субъекта** |Имя субъекта-службы Azure Active Directory. Это имя также является ссылка tooas hello идентификатор клиента. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Секрет субъекта** |Секрет субъекта-службы Azure Active Directory. Этот секрет также является ссылка tooas hello секрет клиента. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Имя учетных данных** |**Имя учетных данных**: интеграция с хранилищем ключей AZURE создает учетные данные в SQL Server, позволяя hello ВМ toohave доступа toohello хранилища ключей. Выберите имя для этих учетных данных. |mycred1 |

Дополнительные сведения см. в статье [Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).

### <a name="r-services"></a>Службы R

У вас есть hello параметр tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx). Это позволяет toouse advanced analytics с SQL Server 2016. Нажмите кнопку **включить** на hello **параметры сервера SQL Server** окна.

> [!NOTE]
> Для SQL Server 2016 Developer Edition этот параметр отключен неправильно порталом hello. Для выпуска Developer Edition необходимо включить службы R вручную после создания виртуальной машины.

![Включение служб R SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Настроив параметры SQL Server, нажмите кнопку **ОК**.

## <a name="5-review-hello-summary"></a>5. Просмотрите hello сводки

На hello **сводки** , просмотрите hello сводки и выберите команду **покупки** toocreate SQL Server, группа ресурсов и ресурсов, указанное для этой виртуальной Машины.

Вы можете отслеживать развертывание hello из hello портал Azure. Hello **уведомления** кнопка hello верхней части экрана приветствия показывает основное состояние развертывания hello.

> [!NOTE]
> tooprovide можно представить в развертывании время ожидания, я развернул регионе Восток США toohello виртуальной Машине SQL с параметрами по умолчанию. Это тестовое развертывание заняла 26 минут toocomplete. Время развертывания зависит от региона и выбранных параметров.

## <a name="open-hello-vm-with-remote-desktop"></a>Открыть hello виртуальной Машины с помощью удаленного рабочего стола

Используйте следующие шаги tooconnect toohello виртуальной машины SQL Server с удаленным рабочим столом hello.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

После подключения виртуальной машины SQL Server toohello можно запустить SQL Server Management Studio и подключитесь с проверкой подлинности Windows, используя учетные данные локального администратора. Если включена проверка подлинности SQL Server, можно также подключиться с проверкой подлинности SQL, используя имя входа SQL hello и пароль, которые настроены во время инициализации.

Машины toohello доступа позволяет toodirectly изменение компьютера и параметры SQL Server, на основе требований. Например можно настроить параметры брандмауэра hello или изменения параметров конфигурации SQL Server.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>Включение TCP/IP для выпусков Developer и Express

При подготовке новой виртуальной Машины SQL Server, Azure не происходит автоматического включения протокола TCP/IP hello для разработчиков SQL Server и выпусках Express. описанные действия Hello, как включить toomanually TCP/IP, чтобы удаленно подключиться по IP-адресу.

Здравствуйте, выполнив действия, используйте **диспетчер конфигурации SQL Server** tooenable протокола hello TCP/IP для разработчиков SQL Server и выпусках Express.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>Удаленное подключение tooSQL сервера

В этом учебнике мы выбрали **открытый** доступа для виртуальной машины hello и **проверки подлинности SQL Server**. Эти подключения параметры автоматически настроенного hello виртуальной машины tooallow SQL Server из любого клиента через hello Интернета (при условии, что они имеют правильные учетные данные SQL hello).

> [!NOTE]
> Если вы не выбрали открытым во время подготовки, можно изменить параметры подключения к SQL через портал hello после подготовки. Дополнительные сведения см. в разделе [об изменении параметров подключения SQL](virtual-machines-windows-sql-connect.md#change).

Hello в следующих разделах показано, как экземпляр SQL Server tooyour tooconnect на ВМ с другого компьютера через hello Интернета.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Дальнейшие действия

Другие сведения об использовании SQL Server в Azure см. в разделе [SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md) и hello [вопросы и ответы](virtual-machines-windows-sql-server-iaas-faq.md).
