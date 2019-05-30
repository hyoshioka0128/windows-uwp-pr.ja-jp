---
title: マップ認証キーの要求
description: MapControl や Windows.Services.Maps 名前空間のマップ サービスをユニバーサル Windows アプリで使うには、そのアプリを認証する必要があります。
ms.assetid: 13B400D7-E13F-4F07-ACC3-9C34087F0F73
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10、UWP、マップ認証キー、マップ コントロール
ms.localizationpriority: medium
ms.openlocfilehash: 8f62ecfab5bd8d09092e5264831327b8c63666bc
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66370512"
---
# <a name="request-a-maps-authentication-key"></a><span data-ttu-id="f6f79-104">マップ認証キーの要求</span><span class="sxs-lookup"><span data-stu-id="f6f79-104">Request a maps authentication key</span></span>




<span data-ttu-id="f6f79-105">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) や [**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps) 名前空間のマップ サービスを [ユニバーサル Windows アプリ](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) で使うには、そのアプリを認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6f79-105">Your [Universal Windows app](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) must be authenticated before it can use the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) and map services in the [**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps) namespace.</span></span> <span data-ttu-id="f6f79-106">アプリを認証するには、マップ認証キーを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6f79-106">To authenticate your app, you must specify a maps authentication key.</span></span> <span data-ttu-id="f6f79-107">このトピックでは、[Bing Maps Developer Center](https://www.bingmapsportal.com/) にマップ認証キーを要求し、アプリに追加する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-107">This topic describes how to request a maps authentication key from the [Bing Maps Developer Center](https://www.bingmapsportal.com/) and add it to your app.</span></span>

<span data-ttu-id="f6f79-108">**ヒント** アプリで地図を使う方法について詳しくは、GitHub の [2Windows-universal-samples リポジトリ](https://go.microsoft.com/fwlink/p/?LinkId=619979) から次のサンプルをダウンロードしてください。</span><span class="sxs-lookup"><span data-stu-id="f6f79-108">**Tip** To learn more about using maps in your app, download the following sample from the [Windows-universal-samples repo](https://go.microsoft.com/fwlink/p/?LinkId=619979) on GitHub:</span></span>

-   [<span data-ttu-id="f6f79-109">ユニバーサル Windows プラットフォーム (UWP) の地図のサンプル</span><span class="sxs-lookup"><span data-stu-id="f6f79-109">Universal Windows Platform (UWP) map sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619977)

## <a name="get-a-key"></a><span data-ttu-id="f6f79-110">キーの取得</span><span class="sxs-lookup"><span data-stu-id="f6f79-110">Get a key</span></span>


<span data-ttu-id="f6f79-111">[Bing Maps Developer Center](https://www.bingmapsportal.com/) を使って、ユニバーサル Windows アプリ用のマップ認証キーを作成し管理します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-111">Create and manage map authentication keys for your Universal Windows apps using the [Bing Maps Developer Center](https://www.bingmapsportal.com/).</span></span>

<span data-ttu-id="f6f79-112">新しいキーを作成するには</span><span class="sxs-lookup"><span data-stu-id="f6f79-112">To create a new key</span></span>

1.  <span data-ttu-id="f6f79-113">ブラウザーで、Bing マップ デベロッパー センターに移動します ([https://www.bingmapsportal.com](https://www.bingmapsportal.com/))。</span><span class="sxs-lookup"><span data-stu-id="f6f79-113">In your browser, navigate to the Bing Maps Developer Center ([https://www.bingmapsportal.com](https://www.bingmapsportal.com/)).</span></span>

2.  <span data-ttu-id="f6f79-114">サインインを求められた場合は、Microsoft アカウントを入力して、 **[Sign in] (サインイン)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-114">If you are asked to sign in, enter your Microsoft account and click **Sign in**.</span></span>

3.  <span data-ttu-id="f6f79-115">Bing Maps アカウントに関連付けるアカウントを選びます。</span><span class="sxs-lookup"><span data-stu-id="f6f79-115">Choose the account to associate with your Bing Maps account.</span></span> <span data-ttu-id="f6f79-116">Microsoft アカウントを使う場合は、 **[Yes] (はい)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-116">If you want to use your Microsoft account, click **Yes**.</span></span> <span data-ttu-id="f6f79-117">それ以外の場合は、 **[Sign in with another account] (別のアカウントでサインイン)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-117">Otherwise, click **Sign in with another account**.</span></span>

4.  <span data-ttu-id="f6f79-118">Bing Maps アカウントを持っていない場合は、ここで新しく作成します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-118">If you don't already have a Bing Maps account, create a new Bing Maps account.</span></span> <span data-ttu-id="f6f79-119">**[Account Name] (アカウント名)** 、 **[Contact Name] (連絡先名)** 、 **[Company Name] (会社名)** 、 **[Email Address] (メール アドレス)** 、 **[Phone Number] (電話番号)** を入力します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-119">Enter the **Account Name**, **Contact Name**, **Company Name**, **Email Address**, and **Phone Number**.</span></span> <span data-ttu-id="f6f79-120">使用条件に同意してから、 **[Create] (作成)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-120">After accepting the terms of use, click **Create**.</span></span>

5.  <span data-ttu-id="f6f79-121">**[My account] (アカウント)** メニューで、 **[My Keys] (マイ キー)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-121">Under the **My account** menu, click **My Keys**.</span></span>

6.  <span data-ttu-id="f6f79-122">以前にキーを作成していた場合は、新しいキーを作成するためのリンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-122">If you have previously created a key, click on the link to create a new key.</span></span> <span data-ttu-id="f6f79-123">それ以外の場合は、[Create Key] (キーの作成) フォームに進みます。</span><span class="sxs-lookup"><span data-stu-id="f6f79-123">Otherwise proceed to the Create Key form.</span></span>

7.  <span data-ttu-id="f6f79-124">**[Create Key] (キーの作成)** フォームの入力が完了したら、 **[Create] (作成)** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f6f79-124">Complete the **Create Key** form and then click **Create**.</span></span>

    -   <span data-ttu-id="f6f79-125">**アプリケーション名:** アプリケーションの名前。</span><span class="sxs-lookup"><span data-stu-id="f6f79-125">**Application name:** The name of your application.</span></span>
    -   <span data-ttu-id="f6f79-126">**アプリケーションの URL (省略可能):** アプリケーションの URL。</span><span class="sxs-lookup"><span data-stu-id="f6f79-126">**Application URL (optional):** The URL of your application.</span></span>
    -   <span data-ttu-id="f6f79-127">**キーの種類:** 選択**基本的な**または**Enterprise**します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-127">**Key type:** Select **Basic** or **Enterprise**.</span></span>
    -   <span data-ttu-id="f6f79-128">**アプリケーションの種類:** 選択**ユニバーサル Windows アプリ**ユニバーサル Windows アプリで使用します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-128">**Application type:** Select **Universal Windows App** for use in your Universal Windows app.</span></span>

    <span data-ttu-id="f6f79-129">次に示すのは、フォームの例です。</span><span class="sxs-lookup"><span data-stu-id="f6f79-129">This is an example of what the form looks like.</span></span>

    ![[Create key] (キーの作成) フォームの例。](images/createkeydialog.png)

8.  <span data-ttu-id="f6f79-131">**[Create] (作成)** をクリックすると、新しいキーが **[Create Key] (キーの作成)** フォームの下に表示されます。</span><span class="sxs-lookup"><span data-stu-id="f6f79-131">After you click **Create**, the new key appears below the **Create Key** form.</span></span> <span data-ttu-id="f6f79-132">このキーを安全な場所にコピーするか、次の手順で説明するように、キーをすぐにアプリに追加します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-132">Copy it to a safe place or immediately add it to your app, as described in the next step.</span></span>

## <a name="add-the-key-to-your-app"></a><span data-ttu-id="f6f79-133">アプリへのキーの追加</span><span class="sxs-lookup"><span data-stu-id="f6f79-133">Add the key to your app</span></span>


<span data-ttu-id="f6f79-134">ユニバーサル Windows アプリで [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) やマップ サービス ([**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps)) を使うには、マップ認証キーが必要になります。</span><span class="sxs-lookup"><span data-stu-id="f6f79-134">The map authentication key is required to use the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) and map services ([**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps)) in your Universal Windows app.</span></span> <span data-ttu-id="f6f79-135">必要に応じて、マップ コントロールやマップ サービスのオブジェクトにキーを追加します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-135">Add it to the map control and map service objects, as applicable.</span></span>

### <a name="to-add-the-key-to-a-map-control"></a><span data-ttu-id="f6f79-136">マップ コントロールにキーを追加するには</span><span class="sxs-lookup"><span data-stu-id="f6f79-136">To add the key to a map control</span></span>

<span data-ttu-id="f6f79-137">[  **MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) を認証するには、[**MapServiceToken**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) プロパティを認証キー値に設定します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-137">To authenticate the [**MapControl**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl), set the [**MapServiceToken**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) property to the authentication key value.</span></span> <span data-ttu-id="f6f79-138">このプロパティは、必要に応じて、コードまたは XAML マークアップで設定できます。</span><span class="sxs-lookup"><span data-stu-id="f6f79-138">You can set this property in code or in XAML markup, depending on your preferences.</span></span> <span data-ttu-id="f6f79-139">**MapControl** の使用について詳しくは、「[2D、3D、Streetside ビューでの地図の表示](display-maps.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f6f79-139">For more info about using the **MapControl**, see [Display maps with 2D, 3D, and Streetside views](display-maps.md).</span></span>

-   <span data-ttu-id="f6f79-140">この例では、コードで **MapServiceToken** を認証キー値に設定しています。</span><span class="sxs-lookup"><span data-stu-id="f6f79-140">This example sets the **MapServiceToken** to the value of the authentication key in code.</span></span>

    ```cs
    MapControl1.MapServiceToken = "abcdef-abcdefghijklmno";
    ```

-   <span data-ttu-id="f6f79-141">この例では、XAML マークアップで **MapServiceToken** を認証キー値に設定しています。</span><span class="sxs-lookup"><span data-stu-id="f6f79-141">This example sets the **MapServiceToken** to the value of the authentication key in XAML markup.</span></span>

    ```xml
    <Maps:MapControl x:Name="MapControl1" MapServiceToken="abcdef-abcdefghijklmno"/>
    ```

### <a name="to-add-the-key-to-map-services"></a><span data-ttu-id="f6f79-142">マップ サービスにキーを追加するには</span><span class="sxs-lookup"><span data-stu-id="f6f79-142">To add the key to map services</span></span>

<span data-ttu-id="f6f79-143">[  **Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps) 名前空間のサービスを使うには、[**ServiceToken**](https://docs.microsoft.com/uwp/api/windows.services.maps.mapservice.servicetoken) プロパティを認証キー値に設定します。</span><span class="sxs-lookup"><span data-stu-id="f6f79-143">To use services in the [**Windows.Services.Maps**](https://docs.microsoft.com/uwp/api/Windows.Services.Maps) namespace, set the [**ServiceToken**](https://docs.microsoft.com/uwp/api/windows.services.maps.mapservice.servicetoken) property to the authentication key value.</span></span> <span data-ttu-id="f6f79-144">マップ サービスを使用する方法について詳しくは、「[ルートとルート案内の表示](routes-and-directions.md)」と「[ジオコーディングと逆ジオコーディングの実行](geocoding.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="f6f79-144">For more info about using map services, see [Display routes and directions](routes-and-directions.md) and [Perform geocoding and reverse geocoding](geocoding.md).</span></span>

-   <span data-ttu-id="f6f79-145">この例では、コードで **ServiceToken** を認証キー値に設定しています。</span><span class="sxs-lookup"><span data-stu-id="f6f79-145">This example sets the **ServiceToken** to the value of the authentication key in code.</span></span>

    ```cs
    MapService.ServiceToken = "abcdef-abcdefghijklmno";
    ```

## <a name="related-topics"></a><span data-ttu-id="f6f79-146">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f6f79-146">Related topics</span></span>

* [<span data-ttu-id="f6f79-147">Bing Maps Developer Center</span><span class="sxs-lookup"><span data-stu-id="f6f79-147">Bing Maps Developer Center</span></span>](https://www.bingmapsportal.com/)
* [<span data-ttu-id="f6f79-148">UWP の地図のサンプル</span><span class="sxs-lookup"><span data-stu-id="f6f79-148">UWP map sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619977)
* [<span data-ttu-id="f6f79-149">地図の設計ガイドライン</span><span class="sxs-lookup"><span data-stu-id="f6f79-149">Design guidelines for maps</span></span>](https://docs.microsoft.com/windows/uwp/maps-and-location/controls-map)
* [<span data-ttu-id="f6f79-150">Build 2015 のビデオ:Windows アプリでの電話、タブレット、PC で使用できるマップと位置情報の活用</span><span class="sxs-lookup"><span data-stu-id="f6f79-150">Build 2015 video: Leveraging Maps and Location Across Phone, Tablet, and PC in Your Windows Apps</span></span>](https://channel9.msdn.com/Events/Build/2015/2-757)
* [<span data-ttu-id="f6f79-151">UWP の交通情報アプリのサンプル</span><span class="sxs-lookup"><span data-stu-id="f6f79-151">UWP traffic app sample</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=619982)
