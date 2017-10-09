---
title: "Служба разделения слияния aaaDeploy | Документы Microsoft"
description: "Разбиение и объединение с помощью инструментов эластичной базы данных"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="d847a-103">Развертывание службы разбиения и объединения</span><span class="sxs-lookup"><span data-stu-id="d847a-103">Deploy a split-merge service</span></span>
<span data-ttu-id="d847a-104">средство разделения слияния Hello позволяет перемещать данные между сегментированных баз данных.</span><span class="sxs-lookup"><span data-stu-id="d847a-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="d847a-105">См. статью [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="d847a-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="d847a-106">Загрузить пакеты разделения слияния hello</span><span class="sxs-lookup"><span data-stu-id="d847a-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="d847a-107">Загрузка последней версии NuGet hello из [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="d847a-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="d847a-108">Откройте командную строку и перейдите в каталог toohello, который вы загрузили nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d847a-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="d847a-109">Hello загружаемый файл содержит PowerShell commmands.</span><span class="sxs-lookup"><span data-stu-id="d847a-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="d847a-110">Загрузите последнюю версию пакета разделения слияния hello в текущий каталог hello с hello ниже команду:</span><span class="sxs-lookup"><span data-stu-id="d847a-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="d847a-111">Hello файлы помещаются в каталог с именем **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** где *x.x.xxx.x* отражает hello номер версии.</span><span class="sxs-lookup"><span data-stu-id="d847a-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="d847a-112">Поиск файлов служба разделения слияния hello в hello **content\splitmerge\service** вложенный каталог и hello сценариев PowerShell разделения слияния (и необходимые клиентских библиотек) в hello **content\splitmerge\powershell** вложенный каталог.</span><span class="sxs-lookup"><span data-stu-id="d847a-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d847a-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d847a-113">Prerequisites</span></span>
1. <span data-ttu-id="d847a-114">Создание базы данных база данных SQL Azure, будет использоваться в качестве базы данных состояние разделения слияния hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="d847a-115">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d847a-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d847a-116">Создайте новую **Базу данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="d847a-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="d847a-117">Имя базы данных hello и создания нового администратора и пароль.</span><span class="sxs-lookup"><span data-stu-id="d847a-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="d847a-118">Быть убедиться, что toorecord hello имя и пароль для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="d847a-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="d847a-119">Убедитесь, что сервер базы данных SQL Azure позволяет tooit tooconnect служб Azure.</span><span class="sxs-lookup"><span data-stu-id="d847a-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="d847a-120">В hello hello портале **параметры брандмауэра**, убедитесь, что hello **разрешить доступ службы tooAzure** установлено слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="d847a-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="d847a-121">Щелкните hello значок «Сохранить».</span><span class="sxs-lookup"><span data-stu-id="d847a-121">Click hello "save" icon.</span></span>
   
   ![Допустимые службы][1]
3. <span data-ttu-id="d847a-123">Создайте учетную запись хранения Azure, которая будет использоваться для вывода диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="d847a-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="d847a-124">Go toohello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d847a-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="d847a-125">Hello левой панели щелкните **New**, нажмите кнопку **данные + хранилище**, затем **хранения**.</span><span class="sxs-lookup"><span data-stu-id="d847a-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="d847a-126">Создайте облачную службу Azure для размещения службы разбиения и объединения.</span><span class="sxs-lookup"><span data-stu-id="d847a-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="d847a-127">Go toohello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d847a-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="d847a-128">Hello левой панели щелкните **New**, затем **вычислений**, **облачной службы**, и **создать**.</span><span class="sxs-lookup"><span data-stu-id="d847a-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="d847a-129">Настройка службы разбиения и объединения</span><span class="sxs-lookup"><span data-stu-id="d847a-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="d847a-130">Настройка службы разбиения и объединения</span><span class="sxs-lookup"><span data-stu-id="d847a-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="d847a-131">В папке hello, куда вы загрузили сборки hello разделения слияния создайте копию hello **ServiceConfiguration.Template.cscfg** файл, который входит в состав **SplitMergeService.cspkg** и переименуйте его в **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="d847a-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="d847a-132">Откройте **ServiceConfiguration.cscfg** в текстовом редакторе, например Visual Studio, которая проверяет входные данные, такие как формат hello отпечатки сертификата.</span><span class="sxs-lookup"><span data-stu-id="d847a-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="d847a-133">Создать новую базу данных или выберите существующий tooserve базы данных в качестве базы данных состояние hello операции разделения слияния и получения строки соединения hello этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="d847a-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="d847a-134">В настоящее время базы данных состояние hello необходимо использовать параметры сортировки Latin hello (SQL\_Latin1\_Общие\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="d847a-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="d847a-135">Дополнительные сведения см. в статье [Имя параметров сортировки Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="d847a-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="d847a-136">С базу данных SQL Azure строка подключения hello обычно имеет форму hello:</span><span class="sxs-lookup"><span data-stu-id="d847a-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="d847a-137">Введите эту строку подключения в файле cscfg hello в обоих hello **SplitMergeWeb** и **SplitMergeWorker** роли подразделы ElasticScaleMetadata приветствия.</span><span class="sxs-lookup"><span data-stu-id="d847a-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="d847a-138">Для hello **SplitMergeWorker** роли, введите допустимое соединение хранилища tooAzure строку hello **WorkerRoleSynchronizationStorageAccountConnectionString** параметр.</span><span class="sxs-lookup"><span data-stu-id="d847a-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="d847a-139">Настройка безопасности</span><span class="sxs-lookup"><span data-stu-id="d847a-139">Configure security</span></span>
<span data-ttu-id="d847a-140">Подробные инструкции tooconfigure hello безопасность службы hello, см. в разделе toohello [конфигурация безопасности разделения слияния](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d847a-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="d847a-141">Hello целях простое тестовое развертывание для этого учебника минимальный набор конфигурации, шаги будут выполнены tooget hello служба создана и запущена.</span><span class="sxs-lookup"><span data-stu-id="d847a-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="d847a-142">Следующие действия включить только hello одного компьютера или учетной записи выполнение их toocommunicate со службой hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d847a-143">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="d847a-143">Create a self-signed certificate</span></span>
<span data-ttu-id="d847a-144">Создать новый каталог и из следующие команды с помощью execute hello этот каталог система [Командная строка разработчика для Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) окна:</span><span class="sxs-lookup"><span data-stu-id="d847a-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="d847a-145">Предлагается ввести пароль tooprotect hello закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="d847a-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="d847a-146">Введите надежный пароль и подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="d847a-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="d847a-147">Затем запрашивается hello toobe пароль, используемый еще раз после этого.</span><span class="sxs-lookup"><span data-stu-id="d847a-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="d847a-148">Нажмите кнопку **Да** в конец tooimport hello его toohello хранилище доверенных корневых центров сертификации.</span><span class="sxs-lookup"><span data-stu-id="d847a-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="d847a-149">Создание PFX-файла</span><span class="sxs-lookup"><span data-stu-id="d847a-149">Create a PFX file</span></span>
<span data-ttu-id="d847a-150">Выполните следующую команду из hello hello же окно, в котором был выполнен makecert; Используйте hello пароль можно использовать toocreate hello сертификата:</span><span class="sxs-lookup"><span data-stu-id="d847a-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="d847a-151">Импортируйте сертификат клиента hello в личном хранилище hello</span><span class="sxs-lookup"><span data-stu-id="d847a-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="d847a-152">В проводнике Windows дважды щелкните **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="d847a-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="d847a-153">В hello **мастер импорта сертификатов** выберите **текущего пользователя** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d847a-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="d847a-154">Проверьте путь к файлу hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d847a-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="d847a-155">Введите пароль hello, оставьте **включают все расширенные свойства** этот флажок установлен и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d847a-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="d847a-156">Оставьте **hello автоматически выбрать хранилище сертификатов [...]**  этот флажок установлен и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d847a-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="d847a-157">Нажмите кнопки **Готово** и **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d847a-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="d847a-158">Отправка hello PFX файл toohello облачной службы</span><span class="sxs-lookup"><span data-stu-id="d847a-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="d847a-159">Go toohello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d847a-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d847a-160">Выберите **Облачные службы**.</span><span class="sxs-lookup"><span data-stu-id="d847a-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="d847a-161">Выберите облачную службу hello, созданной выше для hello служба разделения или слияния.</span><span class="sxs-lookup"><span data-stu-id="d847a-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="d847a-162">Нажмите кнопку **сертификаты** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="d847a-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="d847a-163">Нажмите кнопку **отправить** hello нижней панели.</span><span class="sxs-lookup"><span data-stu-id="d847a-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="d847a-164">Выберите файл PFX hello и введите hello того же пароля.</span><span class="sxs-lookup"><span data-stu-id="d847a-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="d847a-165">После завершения копирования hello отпечаток сертификата из hello новую запись в списке hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="d847a-166">Обновить файл конфигурации службы hello</span><span class="sxs-lookup"><span data-stu-id="d847a-166">Update hello service configuration file</span></span>
<span data-ttu-id="d847a-167">Вставьте отпечаток сертификата hello выше копируется hello отпечаток значение атрибута из этих параметров.</span><span class="sxs-lookup"><span data-stu-id="d847a-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="d847a-168">Для hello рабочей роли:</span><span class="sxs-lookup"><span data-stu-id="d847a-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="d847a-169">Для hello веб-роли:</span><span class="sxs-lookup"><span data-stu-id="d847a-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="d847a-170">Обратите внимание, в производственной среде следует использовать отдельные сертификаты для hello ЦС, для шифрования, hello сертификата сервера и клиентских сертификатов.</span><span class="sxs-lookup"><span data-stu-id="d847a-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="d847a-171">Подробные указания см. в статье [Настройка параметров безопасности для службы разбиения и объединения](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d847a-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="d847a-172">Развертывание службы</span><span class="sxs-lookup"><span data-stu-id="d847a-172">Deploy your service</span></span>
1. <span data-ttu-id="d847a-173">Go toohello [портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d847a-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d847a-174">Нажмите кнопку hello **облачные службы** hello левой части экрана и выберите hello облачной службы, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="d847a-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="d847a-175">Нажмите на кнопку **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="d847a-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="d847a-176">Выберите hello в промежуточной среде, а затем нажмите кнопку **отправить новое промежуточное развертывание**.</span><span class="sxs-lookup"><span data-stu-id="d847a-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Промежуточная][3]
5. <span data-ttu-id="d847a-178">В диалоговом окне приветствия введите метку развертывания.</span><span class="sxs-lookup"><span data-stu-id="d847a-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="d847a-179">Для «Пакета» и «Конфигурация» щелкните «Из локальной» и выберите hello **SplitMergeService.cspkg** файла и cscfg-файле ранее.</span><span class="sxs-lookup"><span data-stu-id="d847a-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="d847a-180">Убедитесь, что флажок hello **развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** проверяется.</span><span class="sxs-lookup"><span data-stu-id="d847a-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="d847a-181">Нажмите кнопку деления hello в hello нижней правой toobegin hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="d847a-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="d847a-182">Ожидает ее tootake toocomplete несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d847a-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Отправить][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="d847a-184">Устранение неполадок развертывания hello</span><span class="sxs-lookup"><span data-stu-id="d847a-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="d847a-185">Веб-роли в случае toocome сети, существует вероятность проблемы с конфигурацией безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="d847a-186">Убедитесь, что hello SSL настроен, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="d847a-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="d847a-187">Рабочей роли toocome сети, но веб-роли завершается успешно, это скорее проблемы с подключением toohello состояние базы данных, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="d847a-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="d847a-188">Убедитесь, что строка подключения hello в вашей .cscfg точности.</span><span class="sxs-lookup"><span data-stu-id="d847a-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="d847a-189">Проверьте существование hello сервера и базы данных, и что hello идентификатор пользователя и пароль указаны правильно.</span><span class="sxs-lookup"><span data-stu-id="d847a-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="d847a-190">Для баз данных SQL Azure строка hello подключения должен иметь вид hello:</span><span class="sxs-lookup"><span data-stu-id="d847a-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="d847a-191">Убедитесь, что имя сервера hello не начинается с **https://**.</span><span class="sxs-lookup"><span data-stu-id="d847a-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="d847a-192">Убедитесь, что сервер базы данных SQL Azure позволяет tooit tooconnect служб Azure.</span><span class="sxs-lookup"><span data-stu-id="d847a-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="d847a-193">toodo это, откройте https://manage.windowsazure.com, щелкните «Базы данных SQL» hello слева, нажмите кнопку «Серверы» в верхнем hello и выберите сервер.</span><span class="sxs-lookup"><span data-stu-id="d847a-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="d847a-194">Нажмите кнопку **Настройка** в hello top и убедитесь, что hello **служб Azure** установлено слишком «Да».</span><span class="sxs-lookup"><span data-stu-id="d847a-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="d847a-195">(См. предварительные требования hello раздел hello верхней части этой статьи).</span><span class="sxs-lookup"><span data-stu-id="d847a-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="d847a-196">Тестирование развертывания службы hello</span><span class="sxs-lookup"><span data-stu-id="d847a-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="d847a-197">Подключение с помощью веб-браузера</span><span class="sxs-lookup"><span data-stu-id="d847a-197">Connect with a web browser</span></span>
<span data-ttu-id="d847a-198">Определите hello web конечной точки службы разделения слияния.</span><span class="sxs-lookup"><span data-stu-id="d847a-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="d847a-199">Его можно найти в hello классический портал Azure с переходом toohello **мониторинга** облачной службы и в разделе **URL-адрес сайта** hello правой стороны.</span><span class="sxs-lookup"><span data-stu-id="d847a-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="d847a-200">Замените **http://** с **https://** так, как параметры безопасности по умолчанию hello отключить конечную точку hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="d847a-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="d847a-201">Страница приветствия нагрузки этот URL-адрес в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="d847a-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="d847a-202">Тестирование с помощью скриптов PowerShell</span><span class="sxs-lookup"><span data-stu-id="d847a-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="d847a-203">развертывания Hello и среду можно проверить, запустив hello включены примеры скриптов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d847a-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="d847a-204">Включенные файлы скриптов Hello — это:</span><span class="sxs-lookup"><span data-stu-id="d847a-204">hello script files included are:</span></span>

1. <span data-ttu-id="d847a-205">**SetupSampleSplitMergeEnvironment.ps1** — задает уровень данных тестирования для разбиения и объединения (подробное описание см. в таблице ниже).</span><span class="sxs-lookup"><span data-stu-id="d847a-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="d847a-206">**ExecuteSampleSplitMerge.ps1** -выполняет операций тестирования, тестовом hello уровня данных (см. таблицу ниже для подробного описания)</span><span class="sxs-lookup"><span data-stu-id="d847a-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="d847a-207">**GetMappings.ps1** — верхнего уровня образец скрипта, который выводит текущее состояние сопоставления сегментов hello hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="d847a-208">**ShardManagement.psm1** -вспомогательный сценарий, который создает оболочку для hello ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="d847a-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="d847a-209">**SqlDatabaseHelpers.psm1** — это вспомогательный сценарий для создания баз данных SQL и управления ими.</span><span class="sxs-lookup"><span data-stu-id="d847a-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="d847a-210">Файл PowerShell</span><span class="sxs-lookup"><span data-stu-id="d847a-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="d847a-211">Действия</span><span class="sxs-lookup"><span data-stu-id="d847a-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="d847a-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="d847a-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="d847a-213">Создает базу данных диспетчера сопоставления сегментов.</span><span class="sxs-lookup"><span data-stu-id="d847a-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="d847a-214">Создает 2 сегментированные базы данных.</span><span class="sxs-lookup"><span data-stu-id="d847a-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="d847a-215">Создает сопоставление сегментов для этих баз данных (удаляет любые существующие сопоставления сегментов в этих базах данных).</span><span class="sxs-lookup"><span data-stu-id="d847a-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="d847a-216">Создает небольшой образец таблицы в обоих сегментов hello и заполняет таблицу hello в одном из сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="d847a-217">Объявляет hello SchemaInfo для сегментированной таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="d847a-218">Файл PowerShell</span><span class="sxs-lookup"><span data-stu-id="d847a-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="d847a-219">Действия</span><span class="sxs-lookup"><span data-stu-id="d847a-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="d847a-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="d847a-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="d847a-221">Отправляет разбиение запроса toohello разделения слияния службы веб-клиента, разбивающего половина данных hello из hello первого сегмента toohello второй сегментов.</span><span class="sxs-lookup"><span data-stu-id="d847a-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="d847a-222">Опрашивает hello веб-клиентом для разбиения состояние запроса и ожидает до завершения запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="d847a-223">Отправляет слияния запроса toohello разделения слияния службы веб-клиента, который перемещает данные hello из hello второй сегмент задней toohello первого сегмента.</span><span class="sxs-lookup"><span data-stu-id="d847a-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="d847a-224">Веб-клиентом hello опрашивает состояние запроса слияния hello и ожидание завершения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="d847a-225">Используйте PowerShell tooverify развертывания</span><span class="sxs-lookup"><span data-stu-id="d847a-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="d847a-226">Открытие нового окна PowerShell и перейдите в каталог toohello, который вы загрузили hello разделения слияния пакет и перейдите в каталог «powershell» hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="d847a-227">Создать сервер базы данных Azure SQL (или выберите существующий сервер) где диспетчера карты сегментов hello и сегменты будут созданы.</span><span class="sxs-lookup"><span data-stu-id="d847a-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d847a-228">Hello SetupSampleSplitMergeEnvironment.ps1 скрипт создает эти базы данных на hello того же сервера с простой сценарий hello tookeep по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d847a-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="d847a-229">Это не является ограничением для hello служба разделения слияния сам.</span><span class="sxs-lookup"><span data-stu-id="d847a-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="d847a-230">Учетные данные проверки подлинности SQL с toohello доступа чтения и записи, баз данных SQL Server необходимо указать для hello данных toomove разделения слияния службы и сопоставление сегментов hello обновления.</span><span class="sxs-lookup"><span data-stu-id="d847a-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="d847a-231">Поскольку hello разделения слияния служба работает в облаке hello, он не поддерживает встроенную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d847a-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="d847a-232">Убедитесь, что сервер Azure SQL hello настроен доступ tooallow из hello IP-адрес компьютера hello, выполнять эти скрипты.</span><span class="sxs-lookup"><span data-stu-id="d847a-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="d847a-233">Этот параметр в разделе hello Azure SQL server можно найти / configuration / разрешенные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d847a-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="d847a-234">Выполнение образца hello SetupSampleSplitMergeEnvironment.ps1 сценария toocreate hello среды.</span><span class="sxs-lookup"><span data-stu-id="d847a-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="d847a-235">Выполнение этого скрипта будет очищают все существующие данные управления карты сегментов структуры в базе данных диспетчера карты сегментов hello и hello сегментов.</span><span class="sxs-lookup"><span data-stu-id="d847a-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="d847a-236">Полезные toorerun hello скрипт может при желании карта сегментов hello toore инициализации или сегментов.</span><span class="sxs-lookup"><span data-stu-id="d847a-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="d847a-237">Пример командной строки:</span><span class="sxs-lookup"><span data-stu-id="d847a-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="d847a-238">Выполнение hello Getmappings.ps1 сценария tooview hello сопоставления, которые в настоящий момент находятся в среде образец hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="d847a-239">Выполните сценарий tooexecute hello ExecuteSampleSplitMerge.ps1 операции split (перенос hello первого сегмента toohello второй сегмент половины данных hello), а затем операции слияния (hello данных обратное перемещение на первый сегмент hello).</span><span class="sxs-lookup"><span data-stu-id="d847a-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="d847a-240">Если вы настроили SSL и левой hello конечной точки http отключен, убедитесь, вместо этого используйте конечную точку https:// hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="d847a-241">Пример командной строки:</span><span class="sxs-lookup"><span data-stu-id="d847a-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="d847a-242">Получив hello ниже ошибка, скорее всего это проблема с сертификатом конечной точки веб.</span><span class="sxs-lookup"><span data-stu-id="d847a-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="d847a-243">Попробуйте подключиться toohello сетевую конечную точку с избранных веб-браузере и проверьте, существует ли сообщение об ошибке сертификата.</span><span class="sxs-lookup"><span data-stu-id="d847a-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="d847a-244">Если выполнено успешно, hello вывод должен выглядеть как hello ниже:</span><span class="sxs-lookup"><span data-stu-id="d847a-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="d847a-245">Поэкспериментируйте с другими типами данных!</span><span class="sxs-lookup"><span data-stu-id="d847a-245">Experiment with other data types!</span></span> <span data-ttu-id="d847a-246">Все эти сценарии принимают дополнительный параметр - ShardKeyType, который позволяет вам тип ключа toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="d847a-247">по умолчанию Hello Int32, но можно также указать Int64, Guid или двоичный.</span><span class="sxs-lookup"><span data-stu-id="d847a-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="d847a-248">Создание запросов</span><span class="sxs-lookup"><span data-stu-id="d847a-248">Create requests</span></span>
<span data-ttu-id="d847a-249">Hello службы можно с помощью веб-hello пользовательского интерфейса или путем импорта и с помощью модуля SplitMerge.psm1 PowerShell hello, который будет отправлять запросы через hello веб-роли.</span><span class="sxs-lookup"><span data-stu-id="d847a-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="d847a-250">Hello службы можно переместить данные в таблицах сегментированных и ссылочных таблиц.</span><span class="sxs-lookup"><span data-stu-id="d847a-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="d847a-251">Сегментированная таблица содержит ключевой столбец сегментирования и различные строчные данные в каждом сегменте.</span><span class="sxs-lookup"><span data-stu-id="d847a-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="d847a-252">Ссылочная таблица не сегментированных, он содержит hello же строки данных на каждый сегмент.</span><span class="sxs-lookup"><span data-stu-id="d847a-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="d847a-253">Ссылочные таблицы полезны для часто не изменяется и используется tooJOIN с сегментированными таблицами в запросах данных.</span><span class="sxs-lookup"><span data-stu-id="d847a-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="d847a-254">Tooperform порядок разбиения слияние необходимо объявить сегментированными таблицами hello и ссылочные таблицы, которые нужно переместить toohave.</span><span class="sxs-lookup"><span data-stu-id="d847a-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="d847a-255">Это осуществляется с помощью hello **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="d847a-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="d847a-256">Этот API является в hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="d847a-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="d847a-257">Создайте для каждой сегментированной таблицы **ShardedTableInfo** объект, описывающий имя схемы таблицы hello родительского (необязательно, по умолчанию слишком «dbo»), hello имя таблицы и имя столбца в таблицы, который содержит ключ сегментирования hello hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="d847a-258">Создайте для каждой таблицы ссылок **ReferenceTableInfo** описывающие имя схемы таблицы hello родительского объекта (необязательно, по умолчанию слишком «dbo») и имя таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="d847a-259">Добавить hello выше новый tooa объектов TableInfo **SchemaInfo** объекта.</span><span class="sxs-lookup"><span data-stu-id="d847a-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="d847a-260">Получить tooa ссылку **ShardMapManager** и вызовите **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="d847a-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="d847a-261">Добавить hello **SchemaInfo** toohello **SchemaInfoCollection**, указав имя сопоставления сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="d847a-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="d847a-262">Примером этого может отображаться в hello SetupSampleSplitMergeEnvironment.ps1 сценария.</span><span class="sxs-lookup"><span data-stu-id="d847a-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="d847a-263">Hello разделения слияния службы не создать целевую базу данных hello (или схемы для всех таблиц в базе данных hello).</span><span class="sxs-lookup"><span data-stu-id="d847a-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="d847a-264">Они должны быть предварительно созданы перед отправкой запроса на обслуживание toohello.</span><span class="sxs-lookup"><span data-stu-id="d847a-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d847a-265">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d847a-265">Troubleshooting</span></span>
<span data-ttu-id="d847a-266">Может появиться hello следующее сообщение при выполнении скриптов powershell образец hello:</span><span class="sxs-lookup"><span data-stu-id="d847a-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="d847a-267">Эта ошибка означает, что SSL-сертификат настроен неправильно.</span><span class="sxs-lookup"><span data-stu-id="d847a-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="d847a-268">Следуйте инструкциям раздела, hello «Соединения с использованием веб-браузер».</span><span class="sxs-lookup"><span data-stu-id="d847a-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="d847a-269">Если не удается отправить запросы, может появиться такое сообщения:</span><span class="sxs-lookup"><span data-stu-id="d847a-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="d847a-270">В этом случае проверьте файл конфигурации, в определенной приветствия для **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="d847a-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="d847a-271">Эта ошибка обычно означает, что рабочая роль, hello не удалось инициализировать успешно hello базы данных метаданных при первом использовании.</span><span class="sxs-lookup"><span data-stu-id="d847a-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

