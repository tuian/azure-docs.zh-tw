---
title: 在邏輯應用程式中使用 BizTalk 一般檔案編碼器 | Microsoft Docs
description: BizTalk 一般檔案編碼器 API 應用程式或連接器
services: logic-apps
documentationcenter: .net,nodejs,java
author: rajram
manager: erikre
editor: ''

ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 04/20/2016
ms.author: rajram

---
# BizTalk 一般檔案編碼器
[!INCLUDE [app-service-logic-version-message](../../includes/app-service-logic-version-message.md)]

使用 BizTalk 一般檔案編碼連接器可在一般檔案資料 (例如 Excel 或 CSV 檔案) 與 XML 資料之間交互操作。它可以將指定的一般檔案執行個體轉換成 XML，反之亦然。

## 使用 BizTalk 一般檔案編碼器
若要使用 BizTalk 一般檔案編碼器，您必須先建立 BizTalk 一般檔案編碼器 API 應用程式的執行個體。在建立邏輯應用程式時進行內嵌，或從 Azure Marketplace 選取 BizTalk 一般檔案編碼器 API 應用程式，即可完成此作業。以下是從 Azure Marketplace 建立 BizTalk 一般檔案編碼器 API 應用程式的一些步驟：

1. 登入 Azure 入口網站 (http://portal.azure.com)
2. 選取 [新增 > Marketplace > 所有項目]
3. 在搜尋方塊中搜尋「BizTalk 一般檔案編碼器」
4. 從結果清單中選取 BizTalk 一般檔案編碼器
5. 選取 [建立]，然後提供名稱和其他必要的詳細資訊
6. 選取 [建立]。您將會重新導向至起始頁，在該處您可以看到建立程序。這可能需要一些時間才能完成。您會在完成時收到通知。

### 設定 BizTalk 一般檔案編碼器
建立 API App 之後，您可以直接從 Azure 入口網站的起始頁啟動它，或是在建立 Logic App 時從設計工具的介面啟動它。

若要從 Azure 起始頁啟動它，您可以輸入您建立 BizTalk 一般檔案編碼器時提供給它的名稱來搜尋。方法如下：

1. 在 Auzre 入口網站的搜尋方塊中輸入您的 BizTalk 一般檔案編碼器的名稱來搜尋
2. 接著，從清單中選取您的 BizTalk 一般檔案編碼器。這會開啟 API App 刀鋒視窗，您可在該處設定您的 BizTalk 一般檔案編碼器 API App。若要開始設定，您要透過下列方式新增結構描述：
3. 選取 [結構描述] 元件 ![BizTalk 一般檔案編碼器的結構描述組件][2]
4. 然後在開啟的 [結構描述] 刀鋒視窗上選取 [新增] ![BizTalk 一般檔案編碼器的動作清單][7]
5. 選取三個選項中的其一來提供您的結構描述。選項包括 [上傳新的結構描述]、[從 JSON 產生] 和 [從一般檔案產生] ![BizTalk 一般檔案編碼器的動作清單][8]
6. 根據您在上一步中的選項，按步驟提供您的結構描述。您接著會看到結構描述已上傳：![BizTalk 一般檔案編碼器的動作清單][9]

### 在設計介面中使用 BizTalk 一般檔案編碼器
設定 Biztalk 一般檔案編碼器之後，接著是在 Logic App 中使用它。若要開始，請建立一個新的邏輯應用程式或啟動您事先建立的現有邏輯應用程式，然後執行下列步驟：

1. 在 [啟動邏輯] 卡中，按一下 [手動執行此邏輯]。
2. 選取您稍早在資源庫中建立的 BizTalk 一般檔案編碼器 API 應用程式 (您會在螢幕右邊的 API Apps 中找到建立的 BizTalk 一般檔案編碼器)。
3. 選取黑色的向右箭號。會顯示兩個可用的動作 (一般檔案轉 Xml 和 Xml 轉一般檔案)：![BizTalk 一般檔案編碼器的動作清單][1] ![BizTalk 一般檔案編碼器的動作清單][4]

根據您選取的動作按下列步驟執行。

#### 一般檔案至 Xml
![BizTalk 一般檔案編碼器的動作清單][5]

| 參數 | 類型 | 參數說明 |
| --- | --- | --- |
| 一般檔案 |字串 |輸入一般檔案的內容 |
| 結構描述名稱 |字串 |表示輸入一般檔案的結構描述名稱 |
| 根節點名稱 |字串 |一般檔案結構描述的根節點名稱 |

此動作會以字串形式傳回輸出 - 輸出 Xml。輸出 Xml 包含輸入一般檔案內容的 xml 表示法。

#### Xml 至一般檔案
![BizTalk 一般檔案編碼器的動作清單][6]

| 參數 | 類型 | 參數說明 |
| --- | --- | --- |
| 輸入 Xml |字串 |輸入 Xml 內容 |

此動作會以字串形式傳回輸出 - 一般檔案。輸出包含輸入 xml 內容的一般檔案表示法。

<!-- References -->
[1]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.ClickToConfigure.PNG
[2]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.SchemasPart.PNG
[3]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.SchemaUpload.PNG
[4]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.ListOfActions.PNG
[5]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.FlatFileToXml.PNG
[6]: ./media/app-service-logic-flatfile-encoder/FlatFileEncoder.XmlToFlatFile.PNG
[7]: ./media/app-service-logic-flatfile-encoder/flatfileencoder.addschema.PNG
[8]: ./media/app-service-logic-flatfile-encoder/flatfileencoder.selectschemauploadoption.PNG
[9]: ./media/app-service-logic-flatfile-encoder/flatfileencoder.shemauploaded.PNG



<!---HONumber=AcomDC_0803_2016-->