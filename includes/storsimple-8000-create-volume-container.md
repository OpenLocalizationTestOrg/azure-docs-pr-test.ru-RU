<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a><span data-ttu-id="15b90-101">toocreate контейнер тома</span><span class="sxs-lookup"><span data-stu-id="15b90-101">toocreate a volume container</span></span>
1. <span data-ttu-id="15b90-102">Перейдите в службе диспетчера StorSimple устройство tooyour и щелкните **устройств**.</span><span class="sxs-lookup"><span data-stu-id="15b90-102">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="15b90-103">Табличный список устройств hello hello выберите и щелкните устройства.</span><span class="sxs-lookup"><span data-stu-id="15b90-103">From hello tabular listing of hello devices, select and click a device.</span></span> 

    ![Колонка "Контейнер томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="15b90-105">В панели мониторинга устройства hello, щелкните **+ добавить контейнер тома**</span><span class="sxs-lookup"><span data-stu-id="15b90-105">In hello device dashboard, click **+ Add volume container**</span></span>

    ![Колонка "Контейнер томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="15b90-107">В hello **добавить контейнер томов** колонки:</span><span class="sxs-lookup"><span data-stu-id="15b90-107">In hello **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="15b90-108">устройство Hello выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="15b90-108">hello device is automatically selected.</span></span>
   2. <span data-ttu-id="15b90-109">В поле **Имя** укажите имя контейнера томов.</span><span class="sxs-lookup"><span data-stu-id="15b90-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="15b90-110">Hello имя должно быть 3 знаков too32.</span><span class="sxs-lookup"><span data-stu-id="15b90-110">hello name must be 3 too32 characters long.</span></span> <span data-ttu-id="15b90-111">Контейнер тома нельзя переименовать после его создания.</span><span class="sxs-lookup"><span data-stu-id="15b90-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="15b90-112">Выберите **включить шифрование облачного хранилища** шифрования tooenable hello данных, отправленных из облака toohello hello устройства.</span><span class="sxs-lookup"><span data-stu-id="15b90-112">Select **Enable Cloud Storage Encryption** tooenable encryption of hello data sent from hello device toohello cloud.</span></span>
   4. <span data-ttu-id="15b90-113">Укажите и подтвердите **ключ шифрования облачного хранилища** то есть 8 too32 символов.</span><span class="sxs-lookup"><span data-stu-id="15b90-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 too32 characters long.</span></span> <span data-ttu-id="15b90-114">Этот ключ используется hello устройства tooaccess зашифрованные данные.</span><span class="sxs-lookup"><span data-stu-id="15b90-114">This key is used by hello device tooaccess encrypted data.</span></span>
   5. <span data-ttu-id="15b90-115">Выберите **учетной записи хранилища** tooassociate с этим контейнером томов.</span><span class="sxs-lookup"><span data-stu-id="15b90-115">Select a **Storage Account** tooassociate with this volume container.</span></span> <span data-ttu-id="15b90-116">Можно выбрать существующую учетную запись хранилища или учетной записи по умолчанию hello, который создается во время создания службы hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-116">You can choose an existing storage account or hello default account that is generated at hello time of service creation.</span></span> <span data-ttu-id="15b90-117">Можно также использовать hello **добавить новую** toospecify параметр учетной записи хранилища, не соответствующая подписка toothis службы.</span><span class="sxs-lookup"><span data-stu-id="15b90-117">You can also use hello **Add new** option toospecify a storage account that is not linked toothis service subscription.</span></span>
   6. <span data-ttu-id="15b90-118">Выберите **неограниченное количество** в hello **укажите пропускную способность** раскрывающегося списка, если вы хотите tooconsume всю доступную полосу пропускания hello.</span><span class="sxs-lookup"><span data-stu-id="15b90-118">Select **Unlimited** in hello **Specify bandwidth** drop-down list if you wish tooconsume all hello available bandwidth.</span></span> <span data-ttu-id="15b90-119">Этот параметр можно также установить слишком**настраиваемый** tooemploy элементов управления пропускной способностью и укажите значение в диапазоне от 1 до 1000 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="15b90-119">You can also set this option too**Custom** tooemploy bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="15b90-120">При наличии доступных сведений об использовании пропускной способности может быть может tooallocate пропускной способности на основе расписания, указав **выбрать шаблон пропускной способности**.</span><span class="sxs-lookup"><span data-stu-id="15b90-120">If you have your bandwidth usage information available, you may be able tooallocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="15b90-121">Пошаговые инструкции см. слишком[Добавление шаблона полосы пропускания](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span><span class="sxs-lookup"><span data-stu-id="15b90-121">For a step-by-step procedure, go too[Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![Колонка "Контейнер томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="15b90-123">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="15b90-123">Click **Create**.</span></span>

        ![Колонка "Контейнер томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="15b90-125">Вы будете оповещены, если контейнер томов hello успешно создана.</span><span class="sxs-lookup"><span data-stu-id="15b90-125">You are notified when hello volume container is successfully created.</span></span>

       ![Уведомление о создании контейнера томов](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="15b90-127">вновь созданные контейнера томов Hello входит в список hello контейнеров томов для устройства.</span><span class="sxs-lookup"><span data-stu-id="15b90-127">hello newly created volume container is listed in hello list of volume containers for your device.</span></span>

   ![Колонка "Добавить контейнер томов"](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


