# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="0581b-101">Часто задаваемые вопросы о дисках виртуальных машин Azure IaaS, а также об управляемых и неуправляемых дисках уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="0581b-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="0581b-102">В этой статье представлены ответы на некоторые часто задаваемые вопросы о службе "Управляемые диски" Azure и хранилище уровня "Премиум" Azure.</span><span class="sxs-lookup"><span data-stu-id="0581b-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="0581b-103">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="0581b-103">Managed Disks</span></span>

<span data-ttu-id="0581b-104">**Что такое управляемые диски Azure?**</span><span class="sxs-lookup"><span data-stu-id="0581b-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="0581b-105">Управляемые диски — это функция автоматического управления учетными записями хранения, которая упрощает управление дисками виртуальных машин Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="0581b-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="0581b-106">Дополнительные сведения см. в разделе hello [Общие сведения о дисках управляемых](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0581b-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="0581b-107">**Сколько будет стоить создание управляемого диска уровня "Стандартный" из существующего VHD объемом 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="0581b-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="0581b-108">Стандартного управляемого диска, созданные на основе на виртуальный жесткий ДИСК 80 ГБ считается hello Далее свободного стандартный размер, — S10 диск.</span><span class="sxs-lookup"><span data-stu-id="0581b-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="0581b-109">Будет взиматься плата соответствующим toohello — S10 диска цены.</span><span class="sxs-lookup"><span data-stu-id="0581b-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="0581b-110">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="0581b-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="0581b-111">**Взимается ли плата за транзакции для управляемых дисков класса "Стандартный"?**</span><span class="sxs-lookup"><span data-stu-id="0581b-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="0581b-112">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-112">Yes.</span></span> <span data-ttu-id="0581b-113">Плата взимается за каждую транзакцию.</span><span class="sxs-lookup"><span data-stu-id="0581b-113">You're charged for each transaction.</span></span> <span data-ttu-id="0581b-114">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="0581b-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="0581b-115">**Для стандартного управляемого диска будет ли взиматься плата для hello фактический размер данных hello на диске hello или подготовить hello емкости диска hello?**</span><span class="sxs-lookup"><span data-stu-id="0581b-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="0581b-116">Выставляются в зависимости от hello подготовки емкости диска hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="0581b-117">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="0581b-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="0581b-118">**Насколько отличается цена управляемых дисков уровня "Премиум" от цены неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="0581b-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="0581b-119">Hello цены premium управляемых дисков hello то же, что диски неуправляемые premium.</span><span class="sxs-lookup"><span data-stu-id="0581b-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="0581b-120">**Можно изменить hello тип учетной записи хранения (Standard или Premium) my управляемых дисков**</span><span class="sxs-lookup"><span data-stu-id="0581b-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="0581b-121">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-121">Yes.</span></span> <span data-ttu-id="0581b-122">Тип учетной записи хранения hello управляемого диски можно изменить с помощью hello портал Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="0581b-123">**Есть ли способ, что я можно копировать или экспортировать управляемого диска tooa личная учетная запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="0581b-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="0581b-124">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-124">Yes.</span></span> <span data-ttu-id="0581b-125">Можно экспортировать управляемый дисков с помощью hello портал Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="0581b-126">**Можно использовать файл виртуального жесткого диска в toocreate учетной записи хранилища Azure управляемого диска с помощью другой подписки**</span><span class="sxs-lookup"><span data-stu-id="0581b-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="0581b-127">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-127">No.</span></span>

<span data-ttu-id="0581b-128">**Можно использовать в toocreate учетной записи хранилища Azure управляемого диска VHD-файл в другом регионе?**</span><span class="sxs-lookup"><span data-stu-id="0581b-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="0581b-129">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-129">No.</span></span>

<span data-ttu-id="0581b-130">**Существуют ли какие-либо ограничения масштабирования для клиентов, использующих управляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="0581b-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="0581b-131">Управляемый диски устраняет hello ограничения, связанные с учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="0581b-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="0581b-132">Тем не менее hello число управляемых дисков для каждой подписки: ограниченный too2, 000 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0581b-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="0581b-133">Это число может вызывать tooincrease поддержки.</span><span class="sxs-lookup"><span data-stu-id="0581b-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="0581b-134">**Могу ли я создать добавочный моментальный снимок управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="0581b-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="0581b-135">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-135">No.</span></span> <span data-ttu-id="0581b-136">текущий моментальный снимок возможность Hello обеспечивает поддержку полную копию управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0581b-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="0581b-137">Тем не менее, мы планируем toosupport добавочных моментальных снимков в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="0581b-138">**Можно ли использовать для виртуальных машин в группе доступности сочетание управляемых и неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="0581b-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="0581b-139">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-139">No.</span></span> <span data-ttu-id="0581b-140">Hello виртуальные машины в группу доступности необходимо использовать диски все управляемые или неуправляемые на всех дисках.</span><span class="sxs-lookup"><span data-stu-id="0581b-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="0581b-141">При создании группы доступности, можно выбрать, какие типы дисков требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="0581b-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="0581b-142">**Параметр по умолчанию hello управляемых дисков находится в hello портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="0581b-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="0581b-143">В настоящее время не но она становится по умолчанию hello в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="0581b-144">**Могу ли я создать пустой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="0581b-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="0581b-145">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-145">Yes.</span></span> <span data-ttu-id="0581b-146">Пустой диск можно создать.</span><span class="sxs-lookup"><span data-stu-id="0581b-146">You can create an empty disk.</span></span> <span data-ttu-id="0581b-147">Управляемого диска могут создаваться независимо от виртуальной Машины, например, не присоединяя его tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0581b-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="0581b-148">**Что такое hello поддерживается число доменов сбоя для группы доступности управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="0581b-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="0581b-149">В зависимости от региона hello, где находится группа доступности hello управляемого диска число доменов сбоя hello поддерживается — 2 или 3.</span><span class="sxs-lookup"><span data-stu-id="0581b-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="0581b-150">**Как обеспечивается hello Стандартная учетная запись хранения для настройки диагностики?**</span><span class="sxs-lookup"><span data-stu-id="0581b-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="0581b-151">Для диагностики виртуальной машины следует настроить частную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0581b-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="0581b-152">В будущем hello, мы планируем диагностики tooswitch tooManaged дисков.</span><span class="sxs-lookup"><span data-stu-id="0581b-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="0581b-153">**Какого вида управление доступом на основе ролей поддерживается для службы "Управляемые диски"?**</span><span class="sxs-lookup"><span data-stu-id="0581b-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="0581b-154">Для управляемых дисков поддерживаются три основные роли по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="0581b-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="0581b-155">"Владелец" — может управлять всем, включая доступ.</span><span class="sxs-lookup"><span data-stu-id="0581b-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="0581b-156">"Участник" — может управлять всем, кроме доступа.</span><span class="sxs-lookup"><span data-stu-id="0581b-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="0581b-157">"Читатель" — может все просматривать, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="0581b-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="0581b-158">**Есть ли способ, что я можно копировать или экспортировать управляемого диска tooa личная учетная запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="0581b-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="0581b-159">Подпись общего доступа только для чтения URI для управляемых hello диск и использовать его можно получить toocopy hello содержимое tooa закрытого хранения учетных данных локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="0581b-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="0581b-160">**Могу ли я создать копию управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="0581b-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="0581b-161">Клиентов можно сделать снимок их управляемых дисков и затем использовать toocreate моментального снимка hello другого управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0581b-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="0581b-162">**Поддерживаются ли еще неуправляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="0581b-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="0581b-163">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-163">Yes.</span></span> <span data-ttu-id="0581b-164">Сейчас мы поддерживаем и управляемые диски, и неуправляемые.</span><span class="sxs-lookup"><span data-stu-id="0581b-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="0581b-165">Рекомендуется использовать управляемый диски для новых рабочих нагрузок и миграции текущего дисков toomanaged рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="0581b-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="0581b-166">**Если создать диск размером 128 ГБ, а затем увеличьте hello размер too130 ГБ, будет ли взиматься плата за hello Далее места на диске (512 ГБ)?**</span><span class="sxs-lookup"><span data-stu-id="0581b-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="0581b-167">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-167">Yes.</span></span>

<span data-ttu-id="0581b-168">**Можно ли создать управляемые диски локально избыточного хранилища, геоизбыточного хранилища и хранилища, избыточного в пределах зоны?**</span><span class="sxs-lookup"><span data-stu-id="0581b-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="0581b-169">Служба "Управляемые диски" Azure сейчас поддерживает только управляемые диски локально избыточного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0581b-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="0581b-170">**Можно ли сжимать управляемые диски или уменьшать их размер?**</span><span class="sxs-lookup"><span data-stu-id="0581b-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="0581b-171">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-171">No.</span></span> <span data-ttu-id="0581b-172">Сейчас такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0581b-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="0581b-173">**Можно ли изменить свойство имени компьютера hello при специальных (не создан с помощью средства подготовки системы hello или обобщить) операционной системы диска используется tooprovision виртуальной Машины?**</span><span class="sxs-lookup"><span data-stu-id="0581b-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="0581b-174">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-174">No.</span></span> <span data-ttu-id="0581b-175">Не удается обновить свойство имени компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-175">You can't update hello computer name property.</span></span> <span data-ttu-id="0581b-176">Hello новой виртуальной Машины наследует его от родительского hello виртуальную Машину, которая была диск операционной системы используется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="0581b-177">**Где найти toocreate шаблоны Azure Resource Manager образец виртуальные машины с дисками управляемого**</span><span class="sxs-lookup"><span data-stu-id="0581b-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="0581b-178">Список шаблонов с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="0581b-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="0581b-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="0581b-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="0581b-180">Управляемые диски и шифрование службы хранилища</span><span class="sxs-lookup"><span data-stu-id="0581b-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="0581b-181">**Включено ли шифрование службы хранилища Azure по умолчанию при создании управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="0581b-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="0581b-182">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-182">Yes.</span></span>

<span data-ttu-id="0581b-183">**Управляющий hello ключи шифрования?**</span><span class="sxs-lookup"><span data-stu-id="0581b-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="0581b-184">Корпорация Майкрософт управляет hello ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="0581b-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="0581b-185">**Можно ли отключить шифрование службы хранилища для моих управляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="0581b-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="0581b-186">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-186">No.</span></span>

<span data-ttu-id="0581b-187">**Шифрование службы хранилища доступно только в определенных регионах?**</span><span class="sxs-lookup"><span data-stu-id="0581b-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="0581b-188">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-188">No.</span></span> <span data-ttu-id="0581b-189">Он доступен во всех регионах hello, где доступен управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="0581b-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="0581b-190">Служба "Управляемые диски" доступна во всех общедоступных регионах, а также в Германии.</span><span class="sxs-lookup"><span data-stu-id="0581b-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="0581b-191">**Как узнать, шифруется ли мой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="0581b-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="0581b-192">Чтобы узнать время hello создания управляемого диска из hello портал Azure, hello Azure CLI и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0581b-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="0581b-193">Если время hello после 9 июня 2017 г., на диске шифруется.</span><span class="sxs-lookup"><span data-stu-id="0581b-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="0581b-194">**Как зашифровать мои диски, созданные до 10 июня 2017 года?**</span><span class="sxs-lookup"><span data-stu-id="0581b-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="0581b-195">Начиная с 10 июня 2017 г. управляемых tooexisting диски записываются новые данные автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="0581b-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="0581b-196">Кроме того, мы планируем tooencrypt существующих данных и шифрования hello произойдет асинхронно в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="0581b-197">Если вам нужно зашифровать существующие данные уже сейчас, создайте копию своего диска.</span><span class="sxs-lookup"><span data-stu-id="0581b-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="0581b-198">Новые диски будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="0581b-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="0581b-199">Копирование дисков, управляемых с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0581b-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="0581b-200">Копирование управляемых дисков с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0581b-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="0581b-201">**Шифруются ли управляемые моментальные снимки и образы?**</span><span class="sxs-lookup"><span data-stu-id="0581b-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="0581b-202">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-202">Yes.</span></span> <span data-ttu-id="0581b-203">Все управляемые моментальные снимки и образы, созданные после 9 июня 2017 года, автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="0581b-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="0581b-204">**Можно преобразовать виртуальных машин с неуправляемой диски, расположенные на учетные записи хранения, которые были ранее зашифрованные toomanaged дисков или**</span><span class="sxs-lookup"><span data-stu-id="0581b-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="0581b-205">Да</span><span class="sxs-lookup"><span data-stu-id="0581b-205">Yes</span></span>

<span data-ttu-id="0581b-206">**Будет ли также зашифрован экспортированный VHD из управляемого диска или моментального снимка?**</span><span class="sxs-lookup"><span data-stu-id="0581b-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="0581b-207">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-207">No.</span></span> <span data-ttu-id="0581b-208">Но если экспортировать VHD tooan шифрование учетной записи хранилища из управляемого зашифрованного диска или моментальный снимок, а затем он зашифрован.</span><span class="sxs-lookup"><span data-stu-id="0581b-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="0581b-209">Управляемые и неуправляемые диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="0581b-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="0581b-210">**Если для виртуальной машины используется размер, который поддерживает хранилище уровня "Премиум" (например, DSv2), можно ли подключить к ней одновременно диски данных уровня "Стандартный" и "Премиум"?**</span><span class="sxs-lookup"><span data-stu-id="0581b-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="0581b-211">Да.</span><span class="sxs-lookup"><span data-stu-id="0581b-211">Yes.</span></span>

<span data-ttu-id="0581b-212">**Можно ли подключить premium и стандартного дисков tooa размер набора данных, не поддерживают хранилище класса Premium, серии D "," Dv2 "," G "или" F?**</span><span class="sxs-lookup"><span data-stu-id="0581b-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="0581b-213">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-213">No.</span></span> <span data-ttu-id="0581b-214">Можно присоединить только стандартные данные диски tooVMs, которые не используют размер ряда, которое поддерживает хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="0581b-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="0581b-215">**Сколько будет стоить создание диска данных уровня "Премиум" из существующего VHD, который имел размер 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="0581b-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="0581b-216">Диск данных premium, созданные на основе на виртуальный жесткий ДИСК 80 ГБ рассматривается как hello Далее доступной расширенной диск размером, равным P10 диска.</span><span class="sxs-lookup"><span data-stu-id="0581b-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="0581b-217">Будет взиматься плата соответствующим toohello P10 диска цены.</span><span class="sxs-lookup"><span data-stu-id="0581b-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="0581b-218">**Существуют toouse затраты на транзакции хранилища Premium?**</span><span class="sxs-lookup"><span data-stu-id="0581b-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="0581b-219">Для каждого размера диска установлена фиксированная стоимость и определенные ограничения пропускной способности и операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="0581b-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="0581b-220">Hello других расходов, являются исходящей пропускной способности и емкость моментального снимка, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="0581b-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="0581b-221">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="0581b-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="0581b-222">**Что такое hello ограничения для операций ввода-ВЫВОДА и пропускную способность, можно получить из кэша диска hello**</span><span class="sxs-lookup"><span data-stu-id="0581b-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="0581b-223">Здравствуйте, объединенный ограничений для кэша и локальный SSD серии DS 4 000 операций ввода-ВЫВОДА на ядро и 33 МБ в секунду на ядро.</span><span class="sxs-lookup"><span data-stu-id="0581b-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="0581b-224">Hello серии GS предлагает 5 000 операций ввода-ВЫВОДА на ядро и 50 МБ в секунду на ядро.</span><span class="sxs-lookup"><span data-stu-id="0581b-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="0581b-225">**— Hello локальный SSD поддерживается для управляемых дисков виртуальной Машины?**</span><span class="sxs-lookup"><span data-stu-id="0581b-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="0581b-226">Hello локальный SSD — временное хранилище, которое входит в состав управляемых дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0581b-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="0581b-227">Никакая дополнительная плата за него не взимается.</span><span class="sxs-lookup"><span data-stu-id="0581b-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="0581b-228">Рекомендуется не использовать этот локальный SSD toostore данные приложения, так как он не сохранен в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0581b-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="0581b-229">**Существует все последствия для hello используйте из TRIM на диски premium?**</span><span class="sxs-lookup"><span data-stu-id="0581b-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="0581b-230">Нет не используется toohello недостаток TRIM на диски Azure в либо premium или стандартные диски.</span><span class="sxs-lookup"><span data-stu-id="0581b-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="0581b-231">Размеры новых управляемых и неуправляемых дисков</span><span class="sxs-lookup"><span data-stu-id="0581b-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="0581b-232">**Что такое hello поддерживается для операционной системы и дисков данных наибольший размер диска**</span><span class="sxs-lookup"><span data-stu-id="0581b-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="0581b-233">Тип раздела Hello, который поддерживает Azure для диска операционной системы — hello основная загрузочная запись (MBR).</span><span class="sxs-lookup"><span data-stu-id="0581b-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="0581b-234">формат MBR Hello поддерживает размер диска вверх too2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="0581b-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="0581b-235">Максимальный объем Hello, который поддерживает Azure для диска операционной системы составляет 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="0581b-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="0581b-236">Azure поддерживает до too4 ТБ для дисков данных.</span><span class="sxs-lookup"><span data-stu-id="0581b-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="0581b-237">**Что такое hello наибольшее страницы размер большого двоичного объекта, поддерживаемый?**</span><span class="sxs-lookup"><span data-stu-id="0581b-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="0581b-238">Hello наибольшее страницы размер большого двоичного объекта, поддерживающий Azure — 8 ТБ (8191 ГБ).</span><span class="sxs-lookup"><span data-stu-id="0581b-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="0581b-239">Мы не поддерживаем страничные большие двоичные объекты размером более 4 ТБ (4095 ГБ) присоединенного tooa виртуальной Машины, данные и дисков операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0581b-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="0581b-240">**Требуется новая версия toouse toocreate средства Azure присоединения, изменение размера и отправка дисков размером более 1 ТБ?**</span><span class="sxs-lookup"><span data-stu-id="0581b-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="0581b-241">Не требуется tooupgrade вашей существующей toocreate инструменты Azure, присоединить или изменить размер дисков размером более 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="0581b-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="0581b-242">tooupload файл вашего виртуального жесткого диска из локальной непосредственно tooAzure как страничный BLOB-объект или неуправляемые диска, необходимо toouse hello последние наборы инструментов:</span><span class="sxs-lookup"><span data-stu-id="0581b-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="0581b-243">Инструменты Azure</span><span class="sxs-lookup"><span data-stu-id="0581b-243">Azure tools</span></span>      | <span data-ttu-id="0581b-244">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="0581b-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="0581b-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0581b-245">Azure PowerShell</span></span> | <span data-ttu-id="0581b-246">Версия 4.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="0581b-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="0581b-247">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0581b-247">Azure CLI v1</span></span>     | <span data-ttu-id="0581b-248">Версия 0.10.13: выпуск за май 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="0581b-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="0581b-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="0581b-249">AzCopy</span></span>           | <span data-ttu-id="0581b-250">Версия 6.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="0581b-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="0581b-251">Поддержка Hello Azure CLI v2 и обозреватель хранилищ Azure ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="0581b-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="0581b-252">**Поддерживаются ли размеры диска P4 и P6 для неуправляемых дисков или страничных BLOB-объектов?**</span><span class="sxs-lookup"><span data-stu-id="0581b-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="0581b-253">Нет.</span><span class="sxs-lookup"><span data-stu-id="0581b-253">No.</span></span> <span data-ttu-id="0581b-254">Размеры диска P4 (32 ГБ) и P6 (64 ГБ) поддерживаются только для управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="0581b-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="0581b-255">Поддержка этих размеров для неуправляемых дисков и страничных BLOB-объектов ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="0581b-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="0581b-256">**Если моей существующей premium управляемых на диске меньше, чем 64 ГБ был создан до включения небольшой диск hello (около 15 июня 2017 г.), как он оплачивается?**</span><span class="sxs-lookup"><span data-stu-id="0581b-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="0581b-257">Существующие диски premium небольшой меньше 64 ГБ по-прежнему toobe плата соответствующим toohello P10 ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="0581b-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="0581b-258">**Как переключаться hello диска уровня диски premium небольшой меньше 64 ГБ из P10 tooP4 или P6**</span><span class="sxs-lookup"><span data-stu-id="0581b-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="0581b-259">Можно сделать снимок небольшие диски и создайте hello коммутатора tooautomatically диска, цены tooP4 уровня или P6 в зависимости от размера подготовить hello.</span><span class="sxs-lookup"><span data-stu-id="0581b-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="0581b-260">Мне не удалось найти ответ на свой вопрос. Что делать?</span><span class="sxs-lookup"><span data-stu-id="0581b-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="0581b-261">Если вашего вопроса нет в списке, сообщите нам об этом, и мы поможем найти ответ.</span><span class="sxs-lookup"><span data-stu-id="0581b-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="0581b-262">В комментариях hello можно разместить вопрос в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0581b-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="0581b-263">tooengage с группой хранилища Azure hello и другими участниками сообщества о в этой статье используется hello MSDN [форум хранилища Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="0581b-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="0581b-264">функции toorequest отправить на запросы и идеи toohello [форуме обратной связи хранилища Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="0581b-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
