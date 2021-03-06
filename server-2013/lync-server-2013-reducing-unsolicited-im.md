﻿---
title: Lync Server 2013：減少來路不明的 IM
TOCTitle: 減少 Lync Server 2013 來路不明的 IM
ms:assetid: d2998708-e699-4465-a918-e1d9ea4c49c3
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Dn518335(v=OCS.15)
ms:contentKeyID: 60471201
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 減少 Lync Server 2013 來路不明的 IM

 

_**上次修改主題的時間：** 2013-12-05_

智慧型 IM 篩選器應用程式可協助保護您的 Microsoft Lync Server 2013 部署，防止最常見的病毒，並且將對使用者經驗的影響降至最低。智慧型 IM 篩選器提供下列功能：

  - 增強型 URL 篩選

  - 增強型檔案傳輸篩選

使用智慧型 IM 篩選器可以設定篩選器，以封鎖來自企業防火牆外部未知端點之來路不明或潛在有害的立即訊息。 您可以指定用於判斷應封鎖之項目的條件來設定篩選器，例如封鎖內含超連結或具特定副檔名之檔案的即時訊息。

部署智慧型 IM 訊息篩選器應用程式之前，必須先了解將訊息從 Lync Server 2013 伺服器路由傳送至另一個伺服器時套用篩選選項的方式。無論伺服器位於單一組織內，或是涵蓋多個組織界限，套用這些篩選選項的方式是一樣的。這種一致性適用於自訂通知和警告文字插入訊息及跨伺服器傳送的方式。

建議的篩選選項是允許含有超連結的立即訊息，但要求智慧型 IM 篩選器在該連結前面插入底線來停用連結。如果選擇這個選項，您還可以另外撰寫要在每條含有超連結之立即訊息開頭出現的使用者通知。

第二個篩選選項可允許含有未修改超連結的立即訊息。如果您選擇這個選項，則可以另外撰寫 (建議使用) 會插入在每一條訊息中的使用者警告。

第三個選項可封鎖所有包含超連結的立即訊息。如果您選擇這個選項，伺服器就會傳送警告給使用者。您必須撰寫這個警告。

