---
title: "aaaHow tooinstall главного целевого сервера под управлением Linux для отработки отказа из Azure tooon организациями | Документы Microsoft"
description: "Для повторного включения защиты виртуальной машины Linux необходим главный целевой сервер Linux. Узнайте, как tooinstall один."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="7199a-104">Установка главного целевого сервера Linux</span><span class="sxs-lookup"><span data-stu-id="7199a-104">Install a Linux master target server</span></span>
<span data-ttu-id="7199a-105">После отказа виртуальных машин, может произойти сбой назад hello виртуальные машины toohello на локальном сайте.</span><span class="sxs-lookup"><span data-stu-id="7199a-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="7199a-106">toofail обратно необходимо tooreprotect hello виртуальную машину из Azure toohello на локальном сайте.</span><span class="sxs-lookup"><span data-stu-id="7199a-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="7199a-107">Для этого процесса необходимо локально master tooreceive hello трафик от целевых серверов.</span><span class="sxs-lookup"><span data-stu-id="7199a-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="7199a-108">Если защита включается для виртуальной машины Windows, вам потребуется главный целевой сервер Windows.</span><span class="sxs-lookup"><span data-stu-id="7199a-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="7199a-109">Для виртуальной машины Linux необходим главный целевой сервер Linux.</span><span class="sxs-lookup"><span data-stu-id="7199a-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="7199a-110">Чтение hello следующие шаги toolearn как toocreate и установить Linux master target.</span><span class="sxs-lookup"><span data-stu-id="7199a-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7199a-111">Начиная с выпуска hello 9.10.0 главный целевой сервер, hello последнюю главный целевой сервер можно только установить на сервере Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="7199a-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="7199a-112">Новые экземпляры невозможно устанавливать на серверы CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="7199a-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="7199a-113">Тем не менее вы можете продолжить tooupgrade старого главного целевые серверы с помощью hello 9.10.0 версии.</span><span class="sxs-lookup"><span data-stu-id="7199a-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="7199a-114">Обзор</span><span class="sxs-lookup"><span data-stu-id="7199a-114">Overview</span></span>
<span data-ttu-id="7199a-115">Эта статья содержит инструкции по как tooinstall Linux главный целевой.</span><span class="sxs-lookup"><span data-stu-id="7199a-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="7199a-116">Разместить комментарии или вопросы в конце hello в этой статье, либо на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7199a-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7199a-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7199a-117">Prerequisites</span></span>

* <span data-ttu-id="7199a-118">определить узла hello toochoose какие toodeploy hello главного целевого сервера, если восстановление размещения hello будет toobe tooan существующих локальных виртуальных машин или tooa новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7199a-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="7199a-119">Для существующей виртуальной машины узла hello hello главного целевого объекта должны иметь хранилищ данных toohello доступа hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7199a-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="7199a-120">Если hello локальной виртуальной машины не существует, hello восстановления размещения виртуальной машины создается на hello же размещаться hello главного целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="7199a-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="7199a-121">Можно выбрать любой узел ESXi главного целевого tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="7199a-122">Hello главный целевой сервер должен быть в сети, который может взаимодействовать с сервером обработки hello и сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="7199a-123">версия Hello hello главного целевого сервера должна быть равна tooor более ранних, чем версии hello hello сервера обработки и сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="7199a-124">Например если версия сервера конфигурации hello hello 9.4, версию hello hello главного целевого объекта можно 9.4 или 9.3, но не 9,5.</span><span class="sxs-lookup"><span data-stu-id="7199a-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="7199a-125">Hello главного целевого сервера может быть только виртуальной машины VMware и физического сервера.</span><span class="sxs-lookup"><span data-stu-id="7199a-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="7199a-126">Создать главный целевой объект hello в соответствии с toohello правила изменения размера</span><span class="sxs-lookup"><span data-stu-id="7199a-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="7199a-127">Создание главного целевого сервера в соответствии с инструкциями изменения размера hello hello:</span><span class="sxs-lookup"><span data-stu-id="7199a-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="7199a-128">**ОЗУ**: 6 ГБ или больше.</span><span class="sxs-lookup"><span data-stu-id="7199a-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="7199a-129">**Размер диска операционной системы**: 100 ГБ или больше (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="7199a-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="7199a-130">**Дополнительное пространство для диска хранения**: 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="7199a-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="7199a-131">**Ядра ЦП**: 4 ядра или больше.</span><span class="sxs-lookup"><span data-stu-id="7199a-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="7199a-132">поддерживает следующие Hello Ubuntu поддерживаемых ядер.</span><span class="sxs-lookup"><span data-stu-id="7199a-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="7199a-133">Серии ядер</span><span class="sxs-lookup"><span data-stu-id="7199a-133">Kernel Series</span></span>  |<span data-ttu-id="7199a-134">Поддерживает систему слишком</span><span class="sxs-lookup"><span data-stu-id="7199a-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="7199a-135">4.4.</span><span class="sxs-lookup"><span data-stu-id="7199a-135">4.4</span></span>      |<span data-ttu-id="7199a-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="7199a-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="7199a-137">4.8</span><span class="sxs-lookup"><span data-stu-id="7199a-137">4.8</span></span>      |<span data-ttu-id="7199a-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="7199a-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="7199a-139">4.10</span><span class="sxs-lookup"><span data-stu-id="7199a-139">4.10</span></span>     |<span data-ttu-id="7199a-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="7199a-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="7199a-141">Развернуть главный целевой сервер hello</span><span class="sxs-lookup"><span data-stu-id="7199a-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="7199a-142">Минимальная установка Ubuntu 16.04.2</span><span class="sxs-lookup"><span data-stu-id="7199a-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="7199a-143">Принимать hello, следуя hello действия tooinstall hello Ubuntu 16.04.2 64-разрядной операционной системе.</span><span class="sxs-lookup"><span data-stu-id="7199a-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="7199a-144">**Шаг 1.** Go toohello [ссылка для загрузки](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) и выберите ближайший зеркальной hello из которой загрузить Ubuntu 16.04.2 минимальной 64-разрядных ISO-ОБРАЗА.</span><span class="sxs-lookup"><span data-stu-id="7199a-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="7199a-145">Хранить Ubuntu 16.04.2 минимальной 64-разрядных ISO-ОБРАЗА в hello DVD-диска и запуска системы hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="7199a-146">**Шаг 2.** Выберите **Русский** в качестве предпочтительного языка и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7199a-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Выбор языка](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="7199a-148">**Шаг 3.** выберите **Install Ubuntu Server** (Установить сервер Ubuntu) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7199a-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Выбор установки сервера Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="7199a-150">**Шаг 4.** Выберите **Русский** в качестве предпочтительного языка и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7199a-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Выбор русского в качестве предпочтительного языка](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="7199a-152">**Шаг 5.** Здравствуйте, выберите соответствующий вариант из hello **часовой пояс** список параметров, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Выберите правильный часовой пояс hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="7199a-154">**Шаг 6.** выберите **нет** (hello параметр по умолчанию), а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Настройка сочетания hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="7199a-156">**Шаг 7.** выберите **английского языка (США)** как hello Страна происхождения hello клавиатуре, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Выберите США как Страна происхождения hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="7199a-158">**Шаг 8.** выберите **английского языка (США)** как hello раскладки клавиатуры, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Выберите в качестве раскладки клавиатуры hello английский (США)](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="7199a-160">**Шаг 9.** введите hello узла для сервера в hello **Hostname** поле, а затем выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Введите имя узла hello сервера](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="7199a-162">**Шаг 10.** toocreate учетной записи пользователя, введите имя пользователя hello и выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Создание учетной записи пользователя](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="7199a-164">**Шаг 11.** пароль hello hello новой учетной записи пользователя, а затем выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Введите пароль hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="7199a-166">**Шаг 12.** подтверждение пароля hello для hello нового пользователя, а затем выберите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Подтверждение пароля hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="7199a-168">**Шаг 13.** выберите **нет** (hello параметр по умолчанию), а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Настройка пользователей и паролей](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="7199a-170">**Шаг 14.** Если правильно hello часового пояса, которое отображается, выберите **Да** (hello параметр по умолчанию), а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="7199a-171">tooreconfigure свой часовой пояс, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="7199a-171">tooreconfigure your time zone, select **No**.</span></span>

![Настройка часов hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="7199a-173">**Шаг 15.** hello метод параметры секционирования, выберите **интерактивной - использовать весь диск**, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Выберите вариант метод секционирования hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="7199a-175">**Шаг 16.** Здравствуйте, выберите соответствующий диск из hello **выберите диск toopartition** параметры, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Выберите диск hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="7199a-177">**Этап 17:** выберите **Да** toowrite hello toodisk изменения, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Запись изменений toodisk hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="7199a-179">**Шаг 18.** параметр используется по умолчанию hello, выберите **Продолжить**, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Выберите параметр по умолчанию hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="7199a-181">**Шаг 19:** выберите hello соответствующий параметр для обновления в системе управления, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Выберите, каким образом обновляет toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="7199a-183">Поскольку hello Azure Site Recovery главный целевой сервер требует очень конкретной версии hello Ubuntu, вам потребуется tooensure, ядра hello обновления отключены для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7199a-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="7199a-184">Если они включены все регулярные обновления вызвать hello главного целевого сервера toomalfunction.</span><span class="sxs-lookup"><span data-stu-id="7199a-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="7199a-185">Необходимо выбрать hello **без автоматического обновления** параметр.</span><span class="sxs-lookup"><span data-stu-id="7199a-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="7199a-186">**Шаг 20.** Выберите параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7199a-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="7199a-187">OpenSSH SSH-подключения, выберите hello **OpenSSH server** , а затем установите **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Выбор программного обеспечения](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="7199a-189">**Шаг 21.** Щелкните **Да**, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="7199a-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Загрузчик GRUB hello установки](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="7199a-191">**Шаг 22:** Здравствуйте, выберите соответствующее устройство для установки начальной загрузки hello (предпочтительно **/dev/sda**), а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="7199a-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Выбор устройства для установки загрузчика](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="7199a-193">**Шаг 23:** выберите **Продолжить**, а затем выберите **ввод** toofinish hello установки.</span><span class="sxs-lookup"><span data-stu-id="7199a-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Завершите установку hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="7199a-195">После завершения процесса установки hello, войдите в toohello виртуальной Машины с новыми учетными данными пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="7199a-196">(См. слишком**шаг 10** подробнее.)</span><span class="sxs-lookup"><span data-stu-id="7199a-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="7199a-197">Занять hello шаги, описанные в следующий снимок экрана tooset hello КОРНЕВОЙ hello пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="7199a-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="7199a-198">Затем войдите как привилегированный пользователь.</span><span class="sxs-lookup"><span data-stu-id="7199a-198">Then sign in as ROOT user.</span></span>

![Пароль пользователя КОРНЕВОГО набора hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="7199a-200">Подготовка машины hello для конфигурации как главный целевой сервер</span><span class="sxs-lookup"><span data-stu-id="7199a-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="7199a-201">Далее Подготовьте машину hello для конфигурации как главный целевой сервер.</span><span class="sxs-lookup"><span data-stu-id="7199a-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="7199a-202">Идентификатор hello tooget для каждого жесткого диска SCSI на виртуальной машине Linux, включите hello **диска. EnableUUID = TRUE** параметра.</span><span class="sxs-lookup"><span data-stu-id="7199a-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="7199a-203">tooenable, этот параметр hello выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7199a-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="7199a-204">Завершите работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7199a-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="7199a-205">Щелкните правой кнопкой мыши запись hello hello виртуальной машины в левой области hello, а затем выберите **изменение параметров**.</span><span class="sxs-lookup"><span data-stu-id="7199a-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="7199a-206">Выберите hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="7199a-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="7199a-207">Hello левой панели выберите **Дополнительно** > **Общие**и затем выберите hello **параметры конфигурации** кнопку hello правой нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="7199a-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Вкладка "Параметры"](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="7199a-209">Hello **параметры конфигурации** параметр недоступен, когда машина hello работает.</span><span class="sxs-lookup"><span data-stu-id="7199a-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="7199a-210">toomake на этой вкладке active, hello виртуальной машины завершена.</span><span class="sxs-lookup"><span data-stu-id="7199a-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="7199a-211">Посмотрите, есть ли строка с параметром **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="7199a-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="7199a-212">Если значение hello существует и имеет значение слишком**False**, измените значение hello слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="7199a-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="7199a-213">(hello значениях регистр не учитывается.)</span><span class="sxs-lookup"><span data-stu-id="7199a-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="7199a-214">Если значение hello существует и имеет значение слишком**True**выберите **отменить**.</span><span class="sxs-lookup"><span data-stu-id="7199a-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="7199a-215">Если значение hello не существует, выберите **добавить строку**.</span><span class="sxs-lookup"><span data-stu-id="7199a-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="7199a-216">В столбце Имя hello, добавьте **диска. EnableUUID**и задайте значение hello слишком**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="7199a-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Проверка наличия параметра disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="7199a-218">Отключение обновления ядра</span><span class="sxs-lookup"><span data-stu-id="7199a-218">Disable kernel upgrades</span></span>

<span data-ttu-id="7199a-219">Azure Site Recovery главный целевой сервер требует очень конкретной версии hello Ubuntu, убедитесь, что обновления ядра hello отключены для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7199a-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="7199a-220">Если включены обновления ядра, какие-либо регулярного обновления вызвать hello главного целевого сервера toomalfunction.</span><span class="sxs-lookup"><span data-stu-id="7199a-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="7199a-221">Скачивание и установка дополнительных пакетов</span><span class="sxs-lookup"><span data-stu-id="7199a-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="7199a-222">Убедитесь, что toodownload подключения к Интернету и установить дополнительные пакеты.</span><span class="sxs-lookup"><span data-stu-id="7199a-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="7199a-223">Если у вас нет подключения к Интернету, необходимо toomanually эти пакеты RPM найти и установить их.</span><span class="sxs-lookup"><span data-stu-id="7199a-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="7199a-224">Получить hello установщика для установки</span><span class="sxs-lookup"><span data-stu-id="7199a-224">Get hello installer for setup</span></span>

<span data-ttu-id="7199a-225">Если ваш главный целевой имеет подключение к Интернету, можно использовать следующие шаги toodownload hello установщика hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="7199a-226">В противном случае можно скопировать hello установщика с сервера обработки hello и установите его.</span><span class="sxs-lookup"><span data-stu-id="7199a-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="7199a-227">Загрузить пакеты установки hello главного целевого сервера</span><span class="sxs-lookup"><span data-stu-id="7199a-227">Download hello master target installation packages</span></span>

<span data-ttu-id="7199a-228">[Загрузить последние элементы в установки Linux главного целевого сервера hello](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="7199a-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="7199a-229">toodownload его с помощью Linux, тип:</span><span class="sxs-lookup"><span data-stu-id="7199a-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="7199a-230">Убедитесь, что вы загрузите и распакуйте установщика hello в домашнем каталоге.</span><span class="sxs-lookup"><span data-stu-id="7199a-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="7199a-231">Если вы Распакуйте слишком**/usr/Local**, происходит сбой установки hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="7199a-232">Установщик hello доступ с сервера обработки hello</span><span class="sxs-lookup"><span data-stu-id="7199a-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="7199a-233">На сервере процесса hello, перейти слишком**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86)**.</span><span class="sxs-lookup"><span data-stu-id="7199a-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="7199a-234">Скопируйте файл установщика необходимых hello с сервера обработки hello и сохраните его в **latestlinuxmobsvc.tar.gz** в домашнем каталоге.</span><span class="sxs-lookup"><span data-stu-id="7199a-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="7199a-235">Применение изменений настраиваемой конфигурации</span><span class="sxs-lookup"><span data-stu-id="7199a-235">Apply custom configuration changes</span></span>

<span data-ttu-id="7199a-236">tooapply пользовательские изменения конфигурации, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7199a-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="7199a-237">Запустите hello, следующая команда toountar hello binary.</span><span class="sxs-lookup"><span data-stu-id="7199a-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Снимок экрана: команда toorun hello](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="7199a-239">Выполните следующие команды toogive разрешение hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="7199a-240">Запустите следующий сценарий hello toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="7199a-241">Запустите сценарий hello только один раз на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="7199a-242">Завершите работу сервера hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-242">Shut down hello server.</span></span> <span data-ttu-id="7199a-243">Затем перезапустите hello сервер после добавления дисков, как описано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="7199a-244">Добавить виртуальную машину главного целевого сервера Linux хранения диска toohello</span><span class="sxs-lookup"><span data-stu-id="7199a-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="7199a-245">Используйте следующие шаги toocreate диска хранения hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="7199a-246">Подключите новый диск размером 1 ТБ toohello главный целевой виртуальной машине Linux, а затем запустите машины hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="7199a-247">Используйте hello **многоканального -ll** toolearn hello многоканального ИД диска хранения hello команды.</span><span class="sxs-lookup"><span data-stu-id="7199a-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Hello многоканального идентификатор диска хранения hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="7199a-249">Отформатировать диск hello и затем создать файловую систему на новый диск hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Создание файловой системы на диске hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="7199a-251">После создания hello файловой системы, подключите диск хранения hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Подключение диска хранения hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="7199a-253">Создать hello **fstab** входа toomount hello диск для хранения каждый раз при запуске системы hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="7199a-254">Выберите **вставить** toobegin редактирования файла hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="7199a-255">Создать новую строку и вставьте следующий текст hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="7199a-256">Изменения многоканального идентификатор hello диска на основе идентификатора многоканального hello выделяются из предыдущей команды hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="7199a-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="7199a-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="7199a-258">Выберите **Esc**, а затем введите **: wq** (записи и выйти из программы) окна редактора tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="7199a-259">Установить главный целевой сервер hello</span><span class="sxs-lookup"><span data-stu-id="7199a-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7199a-260">версия Hello hello главного целевого сервера должна быть равна tooor более ранних, чем версии hello hello сервера обработки и сервер конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="7199a-261">Если это условие не соблюдено, то включить защиту удастся, однако репликация завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7199a-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="7199a-262">Прежде чем устанавливать hello главный целевой сервер, проверьте что hello **/etc/hosts** файл на виртуальной машине hello содержит записи, которые сопоставляют hello toohello локальному имени узла IP-адресов, связанных со всеми сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="7199a-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="7199a-263">Скопируйте hello парольная фраза, из **Recovery\private\connection.passphrase узла Azure C:\ProgramData\Microsoft** на сервере конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="7199a-264">Затем сохраните его как **passphrase.txt** в hello один локальный каталог, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7199a-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="7199a-265">Пример:</span><span class="sxs-lookup"><span data-stu-id="7199a-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="7199a-266">Обратите внимание, IP-адрес сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="7199a-267">Необходимо в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="7199a-268">Запустите hello, следующая команда tooinstall hello главный целевой сервер и зарегистрируйте сервер hello с сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="7199a-269">Пример:</span><span class="sxs-lookup"><span data-stu-id="7199a-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="7199a-270">Дождитесь завершения сценария hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-270">Wait until hello script finishes.</span></span> <span data-ttu-id="7199a-271">Если главный целевой сервер hello регистрирует успешно, hello главного целевого сервера присутствует в hello **инфраструктура Site Recovery** страницы портала hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="7199a-272">Установка hello главного целевого сервера с помощью интерактивной установки</span><span class="sxs-lookup"><span data-stu-id="7199a-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="7199a-273">Следующая команда tooinstall hello главный целевой выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="7199a-274">Роль агента hello, выберите **главного целевого**.</span><span class="sxs-lookup"><span data-stu-id="7199a-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="7199a-275">Выберите расположение установки по умолчанию hello, а затем выберите **ввод** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7199a-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Выбор расположения по умолчанию для установки главного целевого сервера](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="7199a-277">После завершения установки hello Зарегистрируйте сервер конфигурации hello с помощью командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="7199a-278">Обратите внимание, hello IP-адрес сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="7199a-279">Необходимо в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="7199a-280">Запустите hello, следующая команда tooinstall hello главный целевой сервер и зарегистрируйте сервер hello с сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="7199a-281">Пример:</span><span class="sxs-lookup"><span data-stu-id="7199a-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="7199a-282">Дождитесь завершения сценария hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-282">Wait until hello script finishes.</span></span> <span data-ttu-id="7199a-283">Если hello главный целевой сервер успешно зарегистрированного, hello главного целевого сервера присутствует в hello **инфраструктура Site Recovery** страницы портала hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="7199a-284">Обновление главного целевого сервера hello</span><span class="sxs-lookup"><span data-stu-id="7199a-284">Upgrade hello master target</span></span>

<span data-ttu-id="7199a-285">Запустите установщик hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-285">Run hello installer.</span></span> <span data-ttu-id="7199a-286">Он автоматически определяет, hello агент установлен на главном целевом сервере hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="7199a-287">tooupgrade, выберите **Y**.  После завершения установки hello, проверьте версию hello hello главного целевого сервера, установленного с помощью hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7199a-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="7199a-288">Видно, что hello **версии** поле дает номер версии hello hello главного целевого объекта.</span><span class="sxs-lookup"><span data-stu-id="7199a-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="7199a-289">Установить средства VMware на главном целевом сервере hello</span><span class="sxs-lookup"><span data-stu-id="7199a-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="7199a-290">Средства VMware tooinstall hello главного целевого сервера необходимо, чтобы он мог находить hello хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="7199a-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="7199a-291">Если не установлены средства hello, экрана приветствия повторной защиты не отображается в хранилищах данных hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="7199a-292">После установки средства VMware hello необходимо toorestart.</span><span class="sxs-lookup"><span data-stu-id="7199a-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7199a-293">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7199a-293">Next steps</span></span>
<span data-ttu-id="7199a-294">После установки hello и регистрации hello главного целевого объекта имеет finsihed, вы увидите главного целевого сервера hello отображаются на hello **главного целевого** статьи **инфраструктура Site Recovery**, в разделе hello Общие сведения о конфигурации сервера.</span><span class="sxs-lookup"><span data-stu-id="7199a-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="7199a-295">Теперь можно настроить [повторную защиту](site-recovery-how-to-reprotect.md) и выполнить восстановление размещения.</span><span class="sxs-lookup"><span data-stu-id="7199a-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="7199a-296">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="7199a-296">Common issues</span></span>

* <span data-ttu-id="7199a-297">Убедитесь, что Storage vMotion не используется для компонентов системы управления, например для главного целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="7199a-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="7199a-298">Если после успешной повторной защиты перемещает hello главного целевого сервера, не может быть отсоединен hello диски виртуальной машины (VMDKs).</span><span class="sxs-lookup"><span data-stu-id="7199a-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="7199a-299">В этом случае восстановление размещения завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7199a-299">In this case, failback fails.</span></span>

* <span data-ttu-id="7199a-300">главный целевой сервер Hello не следует все моментальные снимки на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="7199a-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="7199a-301">Если существуют моментальные снимки, восстановление размещения завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7199a-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="7199a-302">Из-за toosome пользовательские конфигурации сетевых Адаптеров на некоторые клиенты hello сетевой интерфейс отключен во время запуска и не удалось инициализировать агент hello главного целевого сервера.</span><span class="sxs-lookup"><span data-stu-id="7199a-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="7199a-303">Убедитесь, что hello следующие свойства заданы правильно.</span><span class="sxs-lookup"><span data-stu-id="7199a-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="7199a-304">Проверьте /etc/sysconfig/network-scripts/ifcfg файла карты для этих свойств в hello Ethernet-eth *.</span><span class="sxs-lookup"><span data-stu-id="7199a-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="7199a-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="7199a-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="7199a-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="7199a-306">ONBOOT=yes</span></span>
