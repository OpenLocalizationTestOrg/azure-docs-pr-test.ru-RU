## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Как toocreate классической виртуальной сети в hello портал Azure
toocreate классической виртуальной сети, в зависимости от варианта hello выше, выполните шаги hello.

1. В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.
2. Нажмите кнопку **NEW** > **сети** > **виртуальная сеть**, обратите внимание, что hello **выберите модель развертывания** представлен список уже **классический**, а затем нажмите кнопку **создать**, как показано в приведенном ниже рисунке hello.
   
    ![Создание виртуальной сети на портале Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. На hello **виртуальная сеть** колонки, тип hello **имя** hello виртуальной сети, а затем нажмите кнопку **адресное пространство**. Настройте параметры пространства адресов hello виртуальной сети и ее первая подсеть, а затем нажмите кнопку **ОК**. на следующем рисунке Hello показаны параметры блок CIDR hello в нашем сценарии.
   
    ![Колонка адресного пространства](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Нажмите кнопку **группы ресурсов** и выберите tooadd группы ресурсов виртуальной сети для hello, или нажмите кнопку **создать группу ресурсов** tooadd hello виртуальной сети tooa новую группу ресурсов. Hello на следующем рисунке показана hello ресурсов группы параметры для новой группы ресурсов с именем **TestRG**. Дополнительные сведения о группах ресурсов см. в разделе "Группы ресурсов" [обзора Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Колонка создания группы ресурсов](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. При необходимости измените hello **подписки** и **расположение** параметры для виртуальной сети. 
6. Если требуется запретить toosee hello виртуальной сети в качестве плитки в hello **начальной панели**, отключите **tooStartboard ПИН-кода**. 
7. Нажмите кнопку **создать** и плитки приветствия уведомления с именем **Создание виртуальной сети** как показано на следующем рисунке hello.
   
    ![Создание виртуальной сети в портале](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Дождитесь hello toobe виртуальная сеть создана, и при появлении hello плитку ниже, нажмите кнопку tooadd другие подсети.
   
    ![Создание виртуальной сети в портале](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Вы увидите hello **конфигурации** для вашей виртуальной сети, как показано ниже. 
   
    ![Создание виртуальной сети в портале](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Выберите пункты **Подсети** > **Добавить**, введите **имя** и укажите **диапазон адресов (блок CIDR)** для подсети, а затем нажмите кнопку **ОК**. на следующем рисунке Hello показывает hello параметры для нашей текущего сценария.
    
    ![Создание виртуальной сети на портале Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

