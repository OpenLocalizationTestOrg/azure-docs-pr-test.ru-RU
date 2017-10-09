#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate общедоступные конечные точки в облаке устройстве hello

1. Войдите в систему toohello портал Azure.
2. Go слишком**виртуальные машины**, выберите и нажмите кнопку hello виртуальную машину, которая используется как вашим устройством в облаке.
    
3. Необходимо toocreate сетевой безопасности группы (NSG) правило toocontrol hello поток трафика и из него виртуальную машину. Выполните следующие шаги toocreate правило NSG hello.
    1. Щелкните **Группа безопасности сети**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Выберите группы безопасности сети по умолчанию hello, представленные.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Выберите **Правила безопасности для входящего трафика**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Нажмите кнопку **+ добавить** toocreate правило безопасности для входящего трафика.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        В колонке правила безопасности для входящего трафика добавить hello:

        1. Для hello **имя**, hello введите следующее имя для конечной точки hello: WinRMHttps.
        
        2. Для hello **приоритет**выберите номер меньше 1000 (hello приоритет для правила по умолчанию hello). Чем выше значение hello, более низкий приоритет hello.

        3. Набор hello **источника** слишком**любой**.

        4. Для hello **службы**выберите **WinRM**. Hello **протокола** автоматически устанавливается слишком**TCP** и hello **диапазон портов** задано слишком**5986**.

        5. Нажмите кнопку **ОК** toocreate hello правило.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. Последняя операция — tooassociate группы безопасности сети с подсетью или определенного сетевого интерфейса. Выполните следующие шаги tooassociate hello сетевой группы безопасности с подсетью.
    1. Go слишком**подсети**.
    2. Щелкните **+ Associate** (+ Связать).
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Выберите виртуальной сети, а затем выберите соответствующую подсеть hello.
    4. Нажмите кнопку **ОК** toocreate hello правило.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

После создания правила hello, можно просмотреть его сведения toodetermine hello открытый виртуальный IP-адресов (VIP) адрес. Запишите этот адрес.


