---
title: "開始使用 Data Lake Store | Microsoft Docs"
description: "使用 Azure PowerShell 建立資料湖存放區帳戶，並執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/21/2016
ms.author: nitinme
translationtype: Human Translation
ms.sourcegitcommit: c157da7bf53e2d0762624e8e71e56e956db04a24
ms.openlocfilehash: 7663670bc4fe0612b9a22545f0fc036add1c48cd


---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>使用 Azure PowerShell 開始使用 Azure 資料湖分析存放區
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

了解如何使用 Azure PowerShell 建立 Azure 資料湖存放區帳戶並執行基本作業，例如建立資料夾、上傳和下載資料檔案、刪除您的帳戶等等。如需有關 Data Lake Store 的詳細資訊，請參閱 [Data Lake Store 概觀](data-lake-store-overview.md)。

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備下列條件：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure PowerShell 1.0 或更新版本**。 請參閱 [如何安裝和設定 Azure PowerShell](../powershell-install-configure.md)。

## <a name="authentication"></a>驗證
本文搭配使用較簡單的驗證方法與 Data Lake Store，系統會提示您輸入 Azure 帳號認證。 Data Lake Store 帳戶和檔案系統的存取層級則由已登入使用者的存取層級所控管。 不過，還有其他方法可向 Data Lake Store 進行驗證：**使用者驗證**或**服務對服務驗證**。 如需如何驗證的指示和詳細資訊，請參閱 [使用 Azure Active Directory 向 Data Lake Store 進行驗證](data-lake-store-authenticate-using-active-directory.md)。

## <a name="create-an-azure-data-lake-store-account"></a>建立 Azure 資料湖存放區帳戶
1. 從您的桌面上開啟新的 Windows PowerShell 視窗，輸入下列程式碼片段登入 Azure 帳戶、設定訂用帳戶，然後註冊 Data Lake Store 提供者。 系統提示您登入時，請使用其中一個訂用帳戶管理員/擁有者身分登入：
   
        # Log in to your Azure account
        Login-AzureRmAccount
   
        # List all the subscriptions associated to your account
        Get-AzureRmSubscription
   
        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>
   
        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Azure 資料湖存放區帳戶與 Azure 資源群組相關聯。 從建立 Azure 資源群組開始。
   
        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"
   
    ![建立 Azure 資源群組](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")
3. 建立 Azure 資料湖存放區帳戶。 您指定的名稱必須只包含小寫字母和數字。
   
        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"
   
    ![建立 Azure 資料湖存放區帳戶](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")
4. 確認已成功建立帳戶。
   
        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName
   
    輸出應為 **True**。

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>在您的 Azure 資料湖存放區中建立目錄結構
您可以在您的 Azure 資料湖存放區帳戶下建立用於管理與儲存資料的目錄。

1. 指定根目錄。
   
        $myrootdir = "/"
2. 在指定的根目錄下建立名為 **mynewdirectory** 的新目錄。
   
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. 確認已成功建立新目錄。
   
        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir
   
    應該會顯示類似下面的輸出畫面：
   
    ![確認目錄](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")

## <a name="upload-data-to-your-azure-data-lake-store"></a>將資料上傳至 Azure 資料湖存放區
您可以在根層級直接將資料上傳至資料湖存放區，或上傳至您在帳戶內建立的目錄。 下列程式碼範例說明如何將一些範例資料上傳至您在上一節中建立的目錄 (**mynewdirectory**)。

如果您要尋找一些可上傳的範例資料，您可以從 **Azure 資料湖 Git 儲存機制** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。 下載檔案並將它儲存在電腦的本機目錄上，例如 C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>重新命名、下載與刪除資料湖存放區中的資料
若要重新命名檔案，請使用下列命令：

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

若要下載檔案，請使用下列命令：

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

若要刪除檔案，請使用下列命令：

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

出現提示時，請輸入 **Y** 刪除項目。 如果您要刪除多個檔案，可以提供所有的路徑並以逗號分隔。

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>刪除 Azure 資料湖存放區帳戶
使用下列命令刪除資料湖存放區帳戶。

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

出現提示時，請輸入 **Y** 刪除帳戶。

## <a name="next-steps"></a>後續步驟
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配資料湖存放區使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)




<!--HONumber=Nov16_HO4-->


