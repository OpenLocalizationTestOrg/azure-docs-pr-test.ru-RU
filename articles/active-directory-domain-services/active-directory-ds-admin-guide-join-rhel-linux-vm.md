---
title: "Azure доменных служб Active Directory: Присоединиться к управляемому домену tooa ВМ RHEL | Документы Microsoft"
description: "Присоединить виртуальную машину с Red Hat Enterprise Linux tooAzure AD доменных служб"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="86078-103">Присоединить к виртуальной машине Red Hat Enterprise Linux 7 tooa управляемого домену</span><span class="sxs-lookup"><span data-stu-id="86078-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="86078-104">В этой статье показано, как toojoin tooan виртуальной машины Red Hat Enterprise Linux (RHEL) 7 доменные службы Azure AD управление домена.</span><span class="sxs-lookup"><span data-stu-id="86078-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="86078-105">Подготовка виртуальной машины Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="86078-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="86078-106">Выполните следующие шаги tooprovision RHEL 7 виртуальной машины с помощью портала Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="86078-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="86078-107">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86078-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Панель мониторинга портала Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="86078-109">Нажмите кнопку **New** на hello оставить область и тип **Red Hat** в hello панель поиска, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="86078-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="86078-110">В результатах поиска hello отображаются записи для Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="86078-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="86078-111">Щелкните **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="86078-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Выбор RHEL в результатах](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="86078-113">Результаты поиска Hello в hello **все** области должны быть перечислены hello Red Hat Enterprise Linux 7.2 изображения.</span><span class="sxs-lookup"><span data-stu-id="86078-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="86078-114">Нажмите кнопку **Red Hat Enterprise Linux 7.2** tooview Дополнительные сведения о hello образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Выбор RHEL в результатах](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="86078-116">В hello **Red Hat Enterprise Linux 7.2** области, вы увидите Дополнительные сведения о hello образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="86078-117">В hello **выберите модель развертывания** раскрывающийся список, выберите **классический**.</span><span class="sxs-lookup"><span data-stu-id="86078-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="86078-118">Нажмите кнопку hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="86078-118">Then click hello **Create** button.</span></span>

    ![Просмотр сведений об образе](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="86078-120">В hello **основы** страница hello **создать виртуальную машину** мастера введите hello **имя узла** для hello новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="86078-121">Также укажите имя пользователя локального администратора в hello **имя пользователя** поля и **пароль**.</span><span class="sxs-lookup"><span data-stu-id="86078-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="86078-122">Вы также можете toouse пользователя локального администратора hello tooauthenticate ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="86078-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="86078-123">Кроме того, выбрать **ценовую категорию** для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Мастер создания виртуальной машины: страница основных сведений](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="86078-125">В hello **размер** страница hello **создать виртуальную машину** приветствия мастера, выберите размер виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="86078-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Мастер создания виртуальной машины: выбор размера](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="86078-127">В hello **параметры** страница hello **создать виртуальную машину** приветствия мастера, выберите учетную запись хранения для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="86078-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="86078-128">Нажмите кнопку **виртуальной сети** следует развернуть ВМ Linux toowhich hello tooselect hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="86078-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="86078-129">В hello **виртуальной сети** колонки, выберите hello виртуальной сети, в которой доступно доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86078-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="86078-130">В этом примере мы выберите виртуальную сеть «MyPreviewVNet» hello.</span><span class="sxs-lookup"><span data-stu-id="86078-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Создание виртуальной машины — выбор виртуальной сети](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="86078-132">На hello **Сводка** страница hello **создать виртуальную машину** приветствия мастера просмотрите и нажмите кнопку **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="86078-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Создание виртуальной машины — виртуальная сеть выбрана](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="86078-134">Следует запустить развертывание hello новой виртуальной машины на основе образа hello RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="86078-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Создание виртуальной машины — развертывание начато](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="86078-136">Через несколько минут hello виртуальная машина должна была успешно развернута и готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="86078-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Создание виртуальной машины — развернута](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="86078-138">Удаленное подключение к виртуальной машине Linux toohello обслуживаемого</span><span class="sxs-lookup"><span data-stu-id="86078-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="86078-139">подготовлено Hello RHEL 7.2 виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="86078-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="86078-140">Следующая задача Hello-tooconnect удаленно toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="86078-141">**Подключите виртуальную машину toohello RHEL 7.2** , следуйте инструкциям статьи hello в hello [как toolog на tooa виртуальной машине под управлением Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86078-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="86078-142">Hello остальные шаги hello предполагается, что используется hello PuTTY SSH клиентской tooconnect toohello RHEL виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="86078-143">Дополнительные сведения см. в разделе hello [странице загрузки PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="86078-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="86078-144">Откройте hello PuTTY программы.</span><span class="sxs-lookup"><span data-stu-id="86078-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="86078-145">Введите hello **имя узла** для только что создана виртуальная машина RHEL hello.</span><span class="sxs-lookup"><span data-stu-id="86078-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="86078-146">В этом примере наши виртуальная машина имеет hello имя узла «contoso rhel.cloudapp .net».</span><span class="sxs-lookup"><span data-stu-id="86078-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="86078-147">Если вы не уверены в правильности имени узла hello вашей виртуальной машины, см. toohello мониторинга виртуальных Машин на hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="86078-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Подключение PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="86078-149">Войдите в систему виртуальной машины toohello, используя учетные данные локального администратора hello, которое было указано при создании hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86078-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="86078-150">В этом примере мы использовали учетной записи локального администратора hello «mahesh».</span><span class="sxs-lookup"><span data-stu-id="86078-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Окно входа PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="86078-152">Установить необходимые пакеты на виртуальной машине Linux hello</span><span class="sxs-lookup"><span data-stu-id="86078-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="86078-153">После подключения виртуальной машины toohello hello следующей задачей является tooinstall пакеты, необходимые для присоединения к домену на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="86078-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="86078-154">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="86078-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="86078-155">**Установить realmd:** hello realmd пакет используется для присоединения к домену.</span><span class="sxs-lookup"><span data-stu-id="86078-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="86078-156">В терминале PuTTY введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86078-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="86078-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="86078-157">sudo yum install realmd</span></span>

    ![Установка realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="86078-159">Через несколько минут hello realmd пакет должен получить установлен на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="86078-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="86078-161">**Установить sssd:** hello realmd пакета зависит от операций соединения sssd tooperform домена.</span><span class="sxs-lookup"><span data-stu-id="86078-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="86078-162">В терминале PuTTY введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86078-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="86078-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="86078-163">sudo yum install sssd</span></span>

    ![Установка sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="86078-165">Через несколько минут hello sssd пакет должен получить установлен на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="86078-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="86078-167">**Установка kerberos:** в терминале PuTTY введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86078-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="86078-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="86078-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Установка kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="86078-170">Через несколько минут hello realmd пакет должен получить установлен на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="86078-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos установлен](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="86078-172">Присоединение управляемого домена виртуальной машины Linux toohello hello</span><span class="sxs-lookup"><span data-stu-id="86078-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="86078-173">Теперь, когда требуется hello пакеты устанавливаются на виртуальной машине Linux hello, следующая задача hello-toojoin hello виртуальной машины toohello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="86078-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="86078-174">Обнаружение управляемого домена доменных служб AAD hello.</span><span class="sxs-lookup"><span data-stu-id="86078-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="86078-175">В терминале PuTTY введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86078-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="86078-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="86078-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="86078-178">Если **область обнаружения** — не удается toofind ваш управляемый домен, убедитесь, этот домен hello доступен из виртуальной машины hello (try ping).</span><span class="sxs-lookup"><span data-stu-id="86078-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="86078-179">Обеспечьте наличие этой виртуальной машине hello действительно был развернутой toohello одной виртуальной сети, в какие hello управляемый домен недоступен.</span><span class="sxs-lookup"><span data-stu-id="86078-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="86078-180">Инициализируйте kerberos.</span><span class="sxs-lookup"><span data-stu-id="86078-180">Initialize kerberos.</span></span> <span data-ttu-id="86078-181">В терминале PuTTY введите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="86078-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="86078-182">Убедитесь, что пользователь, принадлежащий группы администраторов контроллера домена, toohello «AAD».</span><span class="sxs-lookup"><span data-stu-id="86078-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="86078-183">Только эти пользователи могут присоединен к домену управляемых компьютеров toohello.</span><span class="sxs-lookup"><span data-stu-id="86078-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="86078-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="86078-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="86078-186">Убедитесь, что указано имя домена hello заглавными буквами, else kinit завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="86078-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="86078-187">Присоединен к домену toohello машины hello.</span><span class="sxs-lookup"><span data-stu-id="86078-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="86078-188">В терминале PuTTY введите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="86078-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="86078-189">Укажите hello того же пользователя, указанных в предшествующих шаг (kinit) hello.</span><span class="sxs-lookup"><span data-stu-id="86078-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="86078-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="86078-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Присоединение к realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="86078-192">Должно появиться сообщение («Регистрация выполнена успешно машина в сфере») при hello машина успешно присоединена toohello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="86078-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="86078-193">Проверка присоединения к домену</span><span class="sxs-lookup"><span data-stu-id="86078-193">Verify domain join</span></span>
<span data-ttu-id="86078-194">Можно быстро узнать, была ли успешно присоединена toohello управляемый домен компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="86078-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="86078-195">Подключение toohello вновь RHEL виртуальной Машины с помощью SSH и учетная запись пользователя домена и затем toosee проверку, если правильно разрешить учетной записи пользователя hello присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="86078-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="86078-196">В терминалов, PuTTY типа hello, следующая команда tooconnect toohello вновь домену RHEL виртуальной машины с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="86078-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="86078-197">Использовать учетную запись домена, к которому относится toohello управляемого домена (например, "bob@CONTOSO100.COM" в этом случае.)</span><span class="sxs-lookup"><span data-stu-id="86078-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="86078-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="86078-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="86078-199">В PuTTY терминала введите следующие команды toosee Если hello домашний каталог был правильно инициализирован hello.</span><span class="sxs-lookup"><span data-stu-id="86078-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="86078-200">pwd</span><span class="sxs-lookup"><span data-stu-id="86078-200">pwd</span></span>
3. <span data-ttu-id="86078-201">Введите подписку toosee команду, если членство в группах hello устраняются правильно hello в терминале PuTTY.</span><span class="sxs-lookup"><span data-stu-id="86078-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="86078-202">id</span><span class="sxs-lookup"><span data-stu-id="86078-202">id</span></span>

<span data-ttu-id="86078-203">Ниже приведен пример выходных данных этих команд:</span><span class="sxs-lookup"><span data-stu-id="86078-203">A sample output of these commands follows:</span></span>

![Проверка присоединения к домену](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="86078-205">Устранение неполадок при присоединении к домену</span><span class="sxs-lookup"><span data-stu-id="86078-205">Troubleshooting domain join</span></span>
<span data-ttu-id="86078-206">См. toohello [Устранение неполадок присоединения к домену](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) статьи.</span><span class="sxs-lookup"><span data-stu-id="86078-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="86078-207">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="86078-207">Related Content</span></span>
* [<span data-ttu-id="86078-208">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="86078-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="86078-209">К домену Windows Server виртуальной машины tooan доменные службы Azure AD управляемого</span><span class="sxs-lookup"><span data-stu-id="86078-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="86078-210">[Как toolog на tooa виртуальной машине под управлением Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86078-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="86078-211">Installing Kerberos (Установка Kerberos)</span><span class="sxs-lookup"><span data-stu-id="86078-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="86078-212">Red Hat Enterprise Linux 7: Windows Integration Guide (Red Hat Enterprise Linux 7: руководство по интеграции Windows)</span><span class="sxs-lookup"><span data-stu-id="86078-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
