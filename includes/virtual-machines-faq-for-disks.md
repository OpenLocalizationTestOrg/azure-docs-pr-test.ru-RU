# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="4f10a-101">Часто задаваемые вопросы о дисках виртуальных машин Azure IaaS, а также об управляемых и неуправляемых дисках уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="4f10a-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="4f10a-102">В этой статье представлены ответы на некоторые часто задаваемые вопросы о службе "Управляемые диски" Azure и хранилище уровня "Премиум" Azure.</span><span class="sxs-lookup"><span data-stu-id="4f10a-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="4f10a-103">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="4f10a-103">Managed Disks</span></span>

<span data-ttu-id="4f10a-104">**Что такое управляемые диски Azure?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="4f10a-105">Управляемые диски — это функция автоматического управления учетными записями хранения, которая упрощает управление дисками виртуальных машин Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="4f10a-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="4f10a-106">Дополнительные сведения см. в разделе [Обзор управляемых дисков Azure](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f10a-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="4f10a-107">**Сколько будет стоить создание управляемого диска уровня "Стандартный" из существующего VHD объемом 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="4f10a-108">Управляемый диск уровня "Стандартный", созданный на основе VHD объемом 80 ГБ, будет считаться диском уровня "Стандартный" следующего доступного размера, то есть S10.</span><span class="sxs-lookup"><span data-stu-id="4f10a-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="4f10a-109">За него будет взиматься плата согласно цене на диск S10.</span><span class="sxs-lookup"><span data-stu-id="4f10a-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="4f10a-110">Дополнительные сведения см. на [странице с расценками](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4f10a-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4f10a-111">**Взимается ли плата за транзакции для управляемых дисков класса "Стандартный"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="4f10a-112">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-112">Yes.</span></span> <span data-ttu-id="4f10a-113">Плата взимается за каждую транзакцию.</span><span class="sxs-lookup"><span data-stu-id="4f10a-113">You're charged for each transaction.</span></span> <span data-ttu-id="4f10a-114">Дополнительные сведения см. на [странице с расценками](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4f10a-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4f10a-115">**При использовании управляемого диска класса "Стандартный" я буду платить за фактический объем данных на диске или за подготовленную емкость диска?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="4f10a-116">Плата взимается за подготовленную емкость диска.</span><span class="sxs-lookup"><span data-stu-id="4f10a-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="4f10a-117">Дополнительные сведения см. на [странице с расценками](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4f10a-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4f10a-118">**Насколько отличается цена управляемых дисков уровня "Премиум" от цены неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="4f10a-119">Цены на управляемые и неуправляемые диски класса "Премиум" не отличаются.</span><span class="sxs-lookup"><span data-stu-id="4f10a-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="4f10a-120">**Могу ли я изменить тип учетной записи хранения ("Стандартный" или "Премиум") для своих управляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="4f10a-121">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-121">Yes.</span></span> <span data-ttu-id="4f10a-122">Тип учетной записи хранения для управляемых дисков можно изменить с помощью портала Azure, PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4f10a-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="4f10a-123">**Можно ли скопировать или экспортировать управляемый диск в частную учетную запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="4f10a-124">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-124">Yes.</span></span> <span data-ttu-id="4f10a-125">Вы можете экспортировать управляемые диски с помощью портала Azure, PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4f10a-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="4f10a-126">**Могу ли я использовать VHD-файл, размещенный в учетной записи хранения Azure, для создания управляемого диска в другой подписке?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="4f10a-127">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-127">No.</span></span>

<span data-ttu-id="4f10a-128">**Могу ли я использовать файл виртуального жесткого диска, размещенный в учетной записи хранения Azure, для создания управляемого диска в другом регионе?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="4f10a-129">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-129">No.</span></span>

<span data-ttu-id="4f10a-130">**Существуют ли какие-либо ограничения масштабирования для клиентов, использующих управляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="4f10a-131">Управляемые диски устраняют ограничения, связанные с учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="4f10a-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="4f10a-132">Но для одной подписки по умолчанию существует ограничение в 2000 управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="4f10a-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="4f10a-133">Вы можете обратиться в службу поддержки, чтобы увеличить это число.</span><span class="sxs-lookup"><span data-stu-id="4f10a-133">You can call support to increase this number.</span></span>

<span data-ttu-id="4f10a-134">**Могу ли я создать добавочный моментальный снимок управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="4f10a-135">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-135">No.</span></span> <span data-ttu-id="4f10a-136">В текущей реализации функция моментальных снимков создает полную копию управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="4f10a-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="4f10a-137">В будущем мы планируем реализовать поддержку добавочных моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="4f10a-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="4f10a-138">**Можно ли использовать для виртуальных машин в группе доступности сочетание управляемых и неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="4f10a-139">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-139">No.</span></span> <span data-ttu-id="4f10a-140">Все виртуальные машины в одной группе доступности должны использовать только управляемые или только неуправляемые диски.</span><span class="sxs-lookup"><span data-stu-id="4f10a-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="4f10a-141">Тип дисков, которые вы хотите использовать, можно выбрать при создании группы доступности.</span><span class="sxs-lookup"><span data-stu-id="4f10a-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="4f10a-142">**Являются ли управляемые диски вариантом по умолчанию на портале Azure?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="4f10a-143">Пока нет, но в будущем они будут использоваться по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4f10a-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="4f10a-144">**Могу ли я создать пустой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="4f10a-145">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-145">Yes.</span></span> <span data-ttu-id="4f10a-146">Пустой диск можно создать.</span><span class="sxs-lookup"><span data-stu-id="4f10a-146">You can create an empty disk.</span></span> <span data-ttu-id="4f10a-147">Управляемый диск можно создать независимо от виртуальной машины, например без подключения к ней.</span><span class="sxs-lookup"><span data-stu-id="4f10a-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="4f10a-148">**Сколько доменов сбоя поддерживается для группы доступности, использующей управляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="4f10a-149">В зависимости от региона размещения группы поддерживаемое количество доменов сбоя для группы доступности, использующей управляемые диски, равно 2 или 3.</span><span class="sxs-lookup"><span data-stu-id="4f10a-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="4f10a-150">**Как настроить учетную запись хранения класса "Стандартный" для диагностики?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="4f10a-151">Для диагностики виртуальной машины следует настроить частную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4f10a-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="4f10a-152">В будущем мы планируем также реализовать диагностику для управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="4f10a-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="4f10a-153">**Какого вида управление доступом на основе ролей поддерживается для службы "Управляемые диски"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="4f10a-154">Для управляемых дисков поддерживаются три основные роли по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="4f10a-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="4f10a-155">"Владелец" — может управлять всем, включая доступ.</span><span class="sxs-lookup"><span data-stu-id="4f10a-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="4f10a-156">"Участник" — может управлять всем, кроме доступа.</span><span class="sxs-lookup"><span data-stu-id="4f10a-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="4f10a-157">"Читатель" — может все просматривать, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="4f10a-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="4f10a-158">**Можно ли скопировать или экспортировать управляемый диск в частную учетную запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="4f10a-159">Для управляемого диска можно получить подписанный URL-адрес с доступом только для чтения, с помощью которого содержимое диска можно скопировать в личную учетную запись хранения или в локальное хранилище.</span><span class="sxs-lookup"><span data-stu-id="4f10a-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="4f10a-160">**Могу ли я создать копию управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="4f10a-161">Клиенты могут создать моментальный снимок управляемого диска, а затем использовать этот снимок для создания нового управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="4f10a-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="4f10a-162">**Поддерживаются ли еще неуправляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="4f10a-163">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-163">Yes.</span></span> <span data-ttu-id="4f10a-164">Сейчас мы поддерживаем и управляемые диски, и неуправляемые.</span><span class="sxs-lookup"><span data-stu-id="4f10a-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="4f10a-165">Мы рекомендуем для всех новых рабочих нагрузок использовать управляемые диски и перенести на них все существующие рабочие нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4f10a-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="4f10a-166">**Если я создам диск размером 128 ГБ, а затем увеличу размер до 130 ГБ, будет ли взиматься плата за следующий размер диска (512 ГБ)?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="4f10a-167">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-167">Yes.</span></span>

<span data-ttu-id="4f10a-168">**Можно ли создать управляемые диски локально избыточного хранилища, геоизбыточного хранилища и хранилища, избыточного в пределах зоны?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="4f10a-169">Служба "Управляемые диски" Azure сейчас поддерживает только управляемые диски локально избыточного хранилища.</span><span class="sxs-lookup"><span data-stu-id="4f10a-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="4f10a-170">**Можно ли сжимать управляемые диски или уменьшать их размер?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="4f10a-171">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-171">No.</span></span> <span data-ttu-id="4f10a-172">Сейчас такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4f10a-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="4f10a-173">**Можно ли изменить свойство имени компьютера, если для подготовки виртуальной машины используется специализированный диск операционной системы (не созданный с помощью средства SysPrep и не универсальный)?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="4f10a-174">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-174">No.</span></span> <span data-ttu-id="4f10a-175">Невозможно изменить свойство имени компьютера.</span><span class="sxs-lookup"><span data-stu-id="4f10a-175">You can't update the computer name property.</span></span> <span data-ttu-id="4f10a-176">Новая виртуальная машина наследует его из родительской виртуальной машины, которая использовалась для создания диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="4f10a-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="4f10a-177">**Где можно найти пример шаблонов Azure Resource Manager, чтобы создавать виртуальные машины с управляемыми дисками?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="4f10a-178">Список шаблонов с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="4f10a-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="4f10a-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="4f10a-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="4f10a-180">Управляемые диски и шифрование службы хранилища</span><span class="sxs-lookup"><span data-stu-id="4f10a-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="4f10a-181">**Включено ли шифрование службы хранилища Azure по умолчанию при создании управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="4f10a-182">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-182">Yes.</span></span>

<span data-ttu-id="4f10a-183">**Кто управляет ключами шифрования?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="4f10a-184">Ключами шифрования управляет корпорация Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4f10a-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="4f10a-185">**Можно ли отключить шифрование службы хранилища для моих управляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="4f10a-186">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-186">No.</span></span>

<span data-ttu-id="4f10a-187">**Шифрование службы хранилища доступно только в определенных регионах?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="4f10a-188">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-188">No.</span></span> <span data-ttu-id="4f10a-189">Оно доступно во всех регионах, где доступна служба "Управляемые диски".</span><span class="sxs-lookup"><span data-stu-id="4f10a-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="4f10a-190">Служба "Управляемые диски" доступна во всех общедоступных регионах, а также в Германии.</span><span class="sxs-lookup"><span data-stu-id="4f10a-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="4f10a-191">**Как узнать, шифруется ли мой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="4f10a-192">Можно узнать время создания управляемого диска с помощью портала Azure, Azure CLI или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f10a-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="4f10a-193">Если диск был создан после 9 июня 2017 года, то он шифруются.</span><span class="sxs-lookup"><span data-stu-id="4f10a-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="4f10a-194">**Как зашифровать мои диски, созданные до 10 июня 2017 года?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="4f10a-195">Начиная с 10 июня 2017 года все новые данные, записываемые на управляемые диски, автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="4f10a-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="4f10a-196">Мы планируем также шифрование существующих данных, которое будет выполняться асинхронно в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="4f10a-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="4f10a-197">Если вам нужно зашифровать существующие данные уже сейчас, создайте копию своего диска.</span><span class="sxs-lookup"><span data-stu-id="4f10a-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="4f10a-198">Новые диски будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="4f10a-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="4f10a-199">Копирование управляемых дисков с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f10a-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="4f10a-200">Копирование управляемых дисков с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f10a-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4f10a-201">**Шифруются ли управляемые моментальные снимки и образы?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="4f10a-202">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-202">Yes.</span></span> <span data-ttu-id="4f10a-203">Все управляемые моментальные снимки и образы, созданные после 9 июня 2017 года, автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="4f10a-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="4f10a-204">**Можно ли преобразовать виртуальные машины с неуправляемыми дисками, расположенные в учетных записях хранения, которые шифруются или уже зашифрованы, для использования управляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="4f10a-205">Да</span><span class="sxs-lookup"><span data-stu-id="4f10a-205">Yes</span></span>

<span data-ttu-id="4f10a-206">**Будет ли также зашифрован экспортированный VHD из управляемого диска или моментального снимка?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="4f10a-207">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-207">No.</span></span> <span data-ttu-id="4f10a-208">Но если в учетную запись хранения экспортировать VHD из зашифрованного управляемого диска или моментального снимка, то он тоже будет зашифрован.</span><span class="sxs-lookup"><span data-stu-id="4f10a-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="4f10a-209">Управляемые и неуправляемые диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="4f10a-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="4f10a-210">**Если для виртуальной машины используется размер, который поддерживает хранилище уровня "Премиум" (например, DSv2), можно ли подключить к ней одновременно диски данных уровня "Стандартный" и "Премиум"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="4f10a-211">Да.</span><span class="sxs-lookup"><span data-stu-id="4f10a-211">Yes.</span></span>

<span data-ttu-id="4f10a-212">**Можно ли подключить диски данных уровня "Стандартный" и "Премиум" к виртуальной машине, размер которой не поддерживает хранилище уровня "Премиум" (например, серии D, Dv2, G или F)?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="4f10a-213">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-213">No.</span></span> <span data-ttu-id="4f10a-214">К виртуальным машинам, размер которых не поддерживает хранилище уровня "Премиум", можно подключить только диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="4f10a-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="4f10a-215">**Сколько будет стоить создание диска данных уровня "Премиум" из существующего VHD, который имел размер 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="4f10a-216">Диск данных уровня "Премиум", созданный на основе VHD объемом 80 ГБ, считается диском уровня "Премиум" следующего доступного размера — P10.</span><span class="sxs-lookup"><span data-stu-id="4f10a-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="4f10a-217">За него будет взиматься плата согласно цене на диск P10.</span><span class="sxs-lookup"><span data-stu-id="4f10a-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="4f10a-218">**Применяется ли плата за транзакции при использовании хранилища уровня "Премиум"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="4f10a-219">Для каждого размера диска установлена фиксированная стоимость и определенные ограничения пропускной способности и операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="4f10a-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="4f10a-220">Дополнительная плата взимается только за пропускную способность для исходящих данных и емкость моментальных снимков (если применимо).</span><span class="sxs-lookup"><span data-stu-id="4f10a-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="4f10a-221">Дополнительные сведения см. на [странице с расценками](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="4f10a-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="4f10a-222">**Какие ограничения пропускной способности и операций ввода-вывода в секунду установлены для кэша диска?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="4f10a-223">Совокупные ограничения для кэша и локального SSD для серии DS составляют 4000 операций ввода-вывода в секунду на ядро и 33 МБ в секунду на ядро,</span><span class="sxs-lookup"><span data-stu-id="4f10a-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="4f10a-224">а у серии GS — 5000 операций ввода-вывода в секунду на ядро и 50 МБ в секунду на ядро.</span><span class="sxs-lookup"><span data-stu-id="4f10a-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="4f10a-225">**Поддерживается ли локальный SSD для виртуальной машины, использующей службу "Управляемые диски"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="4f10a-226">Локальный SSD представляет собой временное хранилище, которое входит в состав виртуальной машины, использующей службу "Управляемые диски".</span><span class="sxs-lookup"><span data-stu-id="4f10a-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="4f10a-227">Никакая дополнительная плата за него не взимается.</span><span class="sxs-lookup"><span data-stu-id="4f10a-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="4f10a-228">Мы рекомендуем не использовать этот локальный SSD для хранения данных приложения, так как данные на нем не сохраняются в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4f10a-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="4f10a-229">**Существуют ли какие-либо последствия использования TRIM на дисках уровня "Премиум"?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="4f10a-230">Использование TRIM на дисках Azure уровня "Премиум" и "Стандартный" не имеет негативных последствий.</span><span class="sxs-lookup"><span data-stu-id="4f10a-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="4f10a-231">Размеры новых управляемых и неуправляемых дисков</span><span class="sxs-lookup"><span data-stu-id="4f10a-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="4f10a-232">**Какой наибольший размер поддерживается для дисков операционной системы и дисков данных?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="4f10a-233">Для диска операционной системы Azure поддерживает раздел MBR (основная загрузочная запись).</span><span class="sxs-lookup"><span data-stu-id="4f10a-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="4f10a-234">Формат MBR поддерживает диски размером до 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="4f10a-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="4f10a-235">Максимальный размер диска операционной системы, который поддерживает Azure, составляет 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="4f10a-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="4f10a-236">Azure поддерживает диски данных, размер которых не превышает 4 ТБ.</span><span class="sxs-lookup"><span data-stu-id="4f10a-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="4f10a-237">**Какой максимальный размер страничного BLOB-объекта поддерживается?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="4f10a-238">Максимальный размер страничного BLOB-объекта, поддерживаемый Azure, составляет 8 ТБ (8191 ГБ).</span><span class="sxs-lookup"><span data-stu-id="4f10a-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="4f10a-239">Мы не поддерживаем подключение к виртуальной машине страничных BLOB-объектов, размер которых превышает 4 ТБ (4095 ГБ), в качестве дисков данных или дисков операционной системы.</span><span class="sxs-lookup"><span data-stu-id="4f10a-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="4f10a-240">**Требуется ли использовать новую версию инструментов Azure для создания, подключения, изменение размера и передачи дисков размером более 1 ТБ?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="4f10a-241">Не нужно обновлять существующие инструменты Azure, чтобы создавать или подключать диски размером более 1 ТБ либо изменять их размер.</span><span class="sxs-lookup"><span data-stu-id="4f10a-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="4f10a-242">Для передачи VHD-файла из локальной среды напрямую в Azure в качестве страничного BLOB-объекта или неуправляемого диска необходимо использовать последние наборы инструментов.</span><span class="sxs-lookup"><span data-stu-id="4f10a-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="4f10a-243">Инструменты Azure</span><span class="sxs-lookup"><span data-stu-id="4f10a-243">Azure tools</span></span>      | <span data-ttu-id="4f10a-244">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="4f10a-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="4f10a-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f10a-245">Azure PowerShell</span></span> | <span data-ttu-id="4f10a-246">Версия 4.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="4f10a-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="4f10a-247">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4f10a-247">Azure CLI v1</span></span>     | <span data-ttu-id="4f10a-248">Версия 0.10.13: выпуск за май 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="4f10a-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="4f10a-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="4f10a-249">AzCopy</span></span>           | <span data-ttu-id="4f10a-250">Версия 6.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="4f10a-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="4f10a-251">Поддержка Azure CLI 2.0 и Azure Storage Explorer ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="4f10a-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="4f10a-252">**Поддерживаются ли размеры диска P4 и P6 для неуправляемых дисков или страничных BLOB-объектов?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="4f10a-253">Нет.</span><span class="sxs-lookup"><span data-stu-id="4f10a-253">No.</span></span> <span data-ttu-id="4f10a-254">Размеры диска P4 (32 ГБ) и P6 (64 ГБ) поддерживаются только для управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="4f10a-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="4f10a-255">Поддержка этих размеров для неуправляемых дисков и страничных BLOB-объектов ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="4f10a-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="4f10a-256">**Если мой управляемый диск уровня "Премиум", размер которого меньше 64 ГБ, был создан до того, как маленький размер диска стал доступен (накануне 15 июня 2017 года), то как он оплачивается?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="4f10a-257">Существующие маленькие диски уровня "Премиум" менее 64 ГБ по-прежнему оплачиваются по ценовой категории P10.</span><span class="sxs-lookup"><span data-stu-id="4f10a-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="4f10a-258">**Как переключить уровень маленьких дисков уровня "Премиум", размер которых не превышает 64 ГБ, с P10 на P4 или P6?**</span><span class="sxs-lookup"><span data-stu-id="4f10a-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="4f10a-259">Можно создать моментальный снимок этих маленьких дисков, а затем создать диск, чтобы автоматически переключить ценовую категорию на P4 или P6 в зависимости от подготовленного размера.</span><span class="sxs-lookup"><span data-stu-id="4f10a-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="4f10a-260">Мне не удалось найти ответ на свой вопрос. Что делать?</span><span class="sxs-lookup"><span data-stu-id="4f10a-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="4f10a-261">Если вашего вопроса нет в списке, сообщите нам об этом, и мы поможем найти ответ.</span><span class="sxs-lookup"><span data-stu-id="4f10a-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="4f10a-262">В комментариях в конце этой статьи можно задать вопрос.</span><span class="sxs-lookup"><span data-stu-id="4f10a-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="4f10a-263">Чтобы обратиться к команде разработчиков службы хранилища Azure и другим участникам сообщества с вопросом об этой статье, воспользуйтесь [форумом по службе хранилища Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="4f10a-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="4f10a-264">Чтобы запросить функции, отправьте свои запросы и предложения на [форум обратной связи по службе хранилища Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="4f10a-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
