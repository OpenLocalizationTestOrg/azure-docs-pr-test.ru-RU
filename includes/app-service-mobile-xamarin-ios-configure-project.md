#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="68ed3-101">Настройка проекта iOS hello в Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="68ed3-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="68ed3-102">В Xamarin.Studio, откройте **Info.plist**и обновление hello **идентификатор пакета** с hello объединить идентификатор, созданный ранее с свой новый идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="68ed3-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="68ed3-103">Прокрутите список вниз слишком**фоновые режимы**.</span><span class="sxs-lookup"><span data-stu-id="68ed3-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="68ed3-104">Выберите hello **Включение фоновых режимов** поле и hello **удаленного уведомления** поле.</span><span class="sxs-lookup"><span data-stu-id="68ed3-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="68ed3-105">Дважды щелкните проект в tooopen панель решения hello **параметры проекта**.</span><span class="sxs-lookup"><span data-stu-id="68ed3-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="68ed3-106">В разделе **построения**, выберите **подписывание пакета iOS**и выберите hello соответствующих идентификаторов и подготовительный профиль можно просто настроить для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="68ed3-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="68ed3-107">Это гарантирует, что этот проект hello использует hello новый профиль для подписи кода.</span><span class="sxs-lookup"><span data-stu-id="68ed3-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="68ed3-108">Hello подготовки документации официальный устройств Xamarin, в разделе [Xamarin подготовки устройств].</span><span class="sxs-lookup"><span data-stu-id="68ed3-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="68ed3-109">Настроить проект iOS hello в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68ed3-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="68ed3-110">В Visual Studio, щелкните правой кнопкой мыши проект hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="68ed3-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="68ed3-111">На страницах свойств hello выберите hello **приложение iOS** вкладка и обновление hello **идентификатор** с Идентификатором hello, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="68ed3-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="68ed3-112">В hello **подписывание пакета iOS** вкладке, выберите hello соответствующих идентификаторов и подготовки вы просто набор профилей вверх для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="68ed3-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="68ed3-113">Это гарантирует, что этот проект hello использует hello новый профиль для подписи кода.</span><span class="sxs-lookup"><span data-stu-id="68ed3-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="68ed3-114">Hello подготовки документации официальный устройств Xamarin, в разделе [Xamarin подготовки устройств].</span><span class="sxs-lookup"><span data-stu-id="68ed3-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="68ed3-115">Дважды щелкните Info.plist tooopen и затем включите **RemoteNotifications** под **фоновые режимы**.</span><span class="sxs-lookup"><span data-stu-id="68ed3-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin подготовки устройств]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/ (Подготовка устройства)
