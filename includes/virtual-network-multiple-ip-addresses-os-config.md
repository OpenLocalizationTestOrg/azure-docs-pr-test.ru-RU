## <span data-ttu-id="37622-101"><a name="os-config"></a>Добавьте IP адресов tooa ВМ операционной системы</span><span class="sxs-lookup"><span data-stu-id="37622-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="37622-102">Подключите и tooa входа в систему виртуальной Машины, созданные с помощью нескольких частных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="37622-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="37622-103">Необходимо вручную добавить все hello частных IP-адресов (включая hello первичный), которые добавлены toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="37622-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="37622-104">Выполните следующие шаги для вашей операционной системы виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="37622-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="37622-105">Windows</span><span class="sxs-lookup"><span data-stu-id="37622-105">Windows</span></span>

1. <span data-ttu-id="37622-106">В командной строке введите *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="37622-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="37622-107">Вы видите только hello *основной* частный IP-адрес (через службу DHCP).</span><span class="sxs-lookup"><span data-stu-id="37622-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="37622-108">Тип *ncpa.cpl* в hello tooopen командную строку hello **сетевые подключения** окна.</span><span class="sxs-lookup"><span data-stu-id="37622-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="37622-109">Открыть свойства hello соответствующий адаптер hello: **подключение по локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="37622-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="37622-110">Дважды щелкните "Протокол IP версии 4 (IPv4)".</span><span class="sxs-lookup"><span data-stu-id="37622-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="37622-111">Выберите **hello использовать следующий IP-адрес** и введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="37622-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="37622-112">**IP-адрес**: Введите hello *основной* частный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="37622-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="37622-113">**Маска подсети**— в зависимости от своей подсети.</span><span class="sxs-lookup"><span data-stu-id="37622-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="37622-114">Например, если hello подсеть — / 24 подсети, а затем hello подсети 255.255.255.0 — маска.</span><span class="sxs-lookup"><span data-stu-id="37622-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="37622-115">**Шлюз по умолчанию**: hello первый IP-адрес в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="37622-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="37622-116">Если в подсети 10.0.0.0/24, IP-адрес шлюза hello — 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="37622-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="37622-117">Нажмите кнопку **hello использовать следующие адреса DNS-серверов** и введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="37622-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="37622-118">**Предпочитаемый DNS-сервер.** Введите 168.63.129.16, если собственный DNS-сервер не используется.</span><span class="sxs-lookup"><span data-stu-id="37622-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="37622-119">При использовании собственного DNS-сервера введите hello IP-адрес сервера.</span><span class="sxs-lookup"><span data-stu-id="37622-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="37622-120">Нажмите кнопку hello **Дополнительно** и добавьте дополнительные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="37622-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="37622-121">Добавьте каждый hello получателя частные IP-адреса перечисленных в шаге 8 toohello сетевого Адаптера с одной подсети, указанный для основного IP-адреса hello hello.</span><span class="sxs-lookup"><span data-stu-id="37622-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="37622-122">Если не следовать приведенным выше шагам hello правильно, можно потерять tooyour подключения к виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="37622-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="37622-123">Убедитесь, что перед продолжением точна hello сведения, введенные на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="37622-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="37622-124">Нажмите кнопку **ОК** tooclose параметры hello TCP/IP и затем **ОК** снова tooclose параметры адаптера hello.</span><span class="sxs-lookup"><span data-stu-id="37622-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="37622-125">После этого подключение к удаленному рабочему столу будет восстановлено.</span><span class="sxs-lookup"><span data-stu-id="37622-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="37622-126">В командной строке введите *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="37622-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="37622-127">Отобразятся все добавленные IP-адреса, а DHCP будет отключен.</span><span class="sxs-lookup"><span data-stu-id="37622-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="37622-128">Проверка (Windows)</span><span class="sxs-lookup"><span data-stu-id="37622-128">Validation (Windows)</span></span>

<span data-ttu-id="37622-129">tooensure вы можете tooconnect toohello, Интернет с вашей дополнительную IP-конфигурацию через hello связанные общедоступный IP-адрес, после добавления правильно с помощью шагов выше, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="37622-130">Для вторичных IP-конфигурации только командой ping toohello Интернет Если hello конфигурации содержит общедоступный IP-адрес, связанный с ним.</span><span class="sxs-lookup"><span data-stu-id="37622-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="37622-131">Для основной IP-конфигурации общедоступный IP-адрес не требуется tooping toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="37622-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="37622-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="37622-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="37622-133">Откройте окно терминала.</span><span class="sxs-lookup"><span data-stu-id="37622-133">Open a terminal window.</span></span>
2. <span data-ttu-id="37622-134">Убедитесь, что вы являетесь hello привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="37622-134">Make sure you are hello root user.</span></span> <span data-ttu-id="37622-135">Если вы не введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="37622-136">Обновите файл конфигурации hello hello сетевого интерфейса (при условии, что «eth0»).</span><span class="sxs-lookup"><span data-stu-id="37622-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="37622-137">Сохраните существующий элемент строку hello для dhcp.</span><span class="sxs-lookup"><span data-stu-id="37622-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="37622-138">Hello основной IP-адрес остается настроенных не изменилось.</span><span class="sxs-lookup"><span data-stu-id="37622-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="37622-139">Добавление конфигурации для дополнительных статический IP-адрес с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="37622-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="37622-140">Должен отобразиться CFG-файл.</span><span class="sxs-lookup"><span data-stu-id="37622-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="37622-141">Привет открыть файл.</span><span class="sxs-lookup"><span data-stu-id="37622-141">Open hello file.</span></span> <span data-ttu-id="37622-142">Вы должны увидеть следующие строки в конце hello файл hello hello.</span><span class="sxs-lookup"><span data-stu-id="37622-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="37622-143">Добавьте следующие строки после hello строк, которые существуют в этом файле hello:</span><span class="sxs-lookup"><span data-stu-id="37622-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="37622-144">Сохраните файл hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="37622-145">Сброс hello сетевой интерфейс с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="37622-146">Запустите ifdown и ifup в hello же строки, если с помощью удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="37622-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="37622-147">Убедитесь, что сетевой интерфейс toohello добавляется hello IP-адрес с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="37622-148">Вы увидите hello IP адрес был добавлен как часть списка hello.</span><span class="sxs-lookup"><span data-stu-id="37622-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="37622-149">Linux (Redhat, CentOS и другие)</span><span class="sxs-lookup"><span data-stu-id="37622-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="37622-150">Откройте окно терминала.</span><span class="sxs-lookup"><span data-stu-id="37622-150">Open a terminal window.</span></span>
2. <span data-ttu-id="37622-151">Убедитесь, что вы являетесь hello привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="37622-151">Make sure you are hello root user.</span></span> <span data-ttu-id="37622-152">Если вы не введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="37622-153">Введите пароль и следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="37622-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="37622-154">Когда вы будете hello привилегированного пользователя, перейдите toohello сетевую папку скриптов с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="37622-155">Список hello связанные файлы ifcfg, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="37622-156">Вы увидите *ifcfg eth0* как один из файлов hello.</span><span class="sxs-lookup"><span data-stu-id="37622-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="37622-157">tooadd IP-адрес, создайте файл конфигурации для него, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="37622-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="37622-158">Обратите внимание, что такой файл должен быть создан для каждой IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="37622-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="37622-159">Откройте hello *ifcfg-eth0:0* файл с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="37622-160">Добавьте файл содержимого toohello *eth0:0* в этом случае с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="37622-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="37622-161">Сведения о том, tooupdate исходя из IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="37622-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="37622-162">Сохраните файл hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="37622-163">Перезапустите службы hello сети и убедитесь, что изменения hello выполняются успешно, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="37622-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="37622-164">Вы увидите hello IP адрес добавленный *eth0:0*, в возвращенном списке hello.</span><span class="sxs-lookup"><span data-stu-id="37622-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="37622-165">Проверка (Linux)</span><span class="sxs-lookup"><span data-stu-id="37622-165">Validation (Linux)</span></span>

<span data-ttu-id="37622-166">связанные Интернет с вашей дополнительную IP-конфигурацию через общедоступный IP-адрес hello, может tooconnect toohello tooensure его, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="37622-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="37622-167">Для вторичных IP-конфигурации только командой ping toohello Интернет Если hello конфигурации содержит общедоступный IP-адрес, связанный с ним.</span><span class="sxs-lookup"><span data-stu-id="37622-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="37622-168">Для основной IP-конфигурации общедоступный IP-адрес не требуется tooping toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="37622-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="37622-169">Для виртуальных машин Linux, при попытке toovalidate исходящие подключения из дополнительный сетевой Адаптер может потребоваться tooadd соответствующие маршруты.</span><span class="sxs-lookup"><span data-stu-id="37622-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="37622-170">Существует много способов toodo это.</span><span class="sxs-lookup"><span data-stu-id="37622-170">There are many ways toodo this.</span></span> <span data-ttu-id="37622-171">Дополнительные сведения по дистрибутиву Linux см. в соответствующей документации.</span><span class="sxs-lookup"><span data-stu-id="37622-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="37622-172">следующие Hello это один метод tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="37622-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="37622-173">Быть tooreplace убедиться, что:</span><span class="sxs-lookup"><span data-stu-id="37622-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="37622-174">**10.0.0.5** с hello частными IP-адрес, который имеет открытый IP-адрес адрес связанного tooit</span><span class="sxs-lookup"><span data-stu-id="37622-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="37622-175">**10.0.0.1** tooyour шлюз по умолчанию</span><span class="sxs-lookup"><span data-stu-id="37622-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="37622-176">**eth2** toohello имя вашей дополнительный сетевой Адаптер</span><span class="sxs-lookup"><span data-stu-id="37622-176">**eth2** toohello name of your secondary NIC</span></span>
