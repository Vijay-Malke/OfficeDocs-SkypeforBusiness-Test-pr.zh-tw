﻿---
title: Lync Server 2013：定義監控需求
TOCTitle: 定義組織的監控需求
ms:assetid: d587ff04-9af6-4ac1-ad42-076e7a40ac75
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205284(v=OCS.15)
ms:contentKeyID: 49890333
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中定義監控需求

 

_**上次修改主題的時間：** 2012-09-05_

簡化部署和安裝 Microsoft Lync Server 2013 中的監控功能，也會簡化關於定義組織監控需求的程序。不過，在您開始安裝和設定 Lync Server 2013 之前，還有幾個應該解決的重要問題：

**您要監控哪一類型的資料？** Lync Server 2013 可讓您監控兩種不同類型的資料：詳細通話記錄 (CDR) 資料與經驗品質 (QoE) 資料。詳細通話記錄讓您能夠追蹤 Lync Server 功能的使用情況，這些功能包括 Voice over IP (VoIP) 通話、立即訊息 (IM)、檔案傳輸、音訊/視訊 (A/V) 會議，以及應用程式工作階段。此資訊可幫助您了解要使用哪些 Lync Server 功能 (而不使用哪些功能)，以及提供要在何時使用這些功能的資訊。經驗品質資料可讓您維護在組織中撥打的音訊和視訊電話品質的記錄，包括遺失的網路封包數量、背景雜訊和「抖動」(封包延遲差異) 量。

如果選擇要啟用 Lync Server 2013 中的監控功能，您可以同時啟用 CDR 監控與 QoE 監控功能，或者選擇啟用一種監控功能，而讓另一類型的功能保持停用。例如，假設使用者只使用即時訊息與檔案傳輸，而不會撥打音訊或視訊電話。在那種情況下，沒有必要啟用 QoE 監控功能。同樣地，在部署監控功能之後， Lync Server 可以輕鬆啟用和停用監控功能。例如，您選擇部署監控功能，但一開始讓 QoE 監控功能處於停用狀態。如果使用者開始遇到音訊或視訊電話的問題，您再啟用 QoE 監控功能，然後使用該資料協助您疑難排解和解決那些問題。

在安裝 Lync Server 時，同時安裝監控功能與在 Lync Server 安裝之後才安裝監控功能，並無特殊的優點 (或缺點)。請記住一點，在安裝監控功能之前，您必須選取要裝載後端監控存放區的電腦，還必須在該電腦上安裝和設定的支援 SQL Server 版本，之後才能使用電腦提供監控功能。如果您已在電腦上安裝 SQL Server，而且電腦就緒可供使用，您可以在安裝 Lync Server 時，同時安裝監控功能。如果尚未備妥後端電腦，您可以繼續安裝 Lync Server，然後等到後端電腦就緒可供使用後，再安裝監控功能。

**您希望何時安裝監控功能？** 您可以在安裝和設定 Lync Server 2013 時，同時安裝和設定監控功能；您可以在安裝期間，利用 Lync Server 部署精靈讓前端集區與監控資料庫產生關聯。或者，您可以在安裝 Lync Server 之後，再安裝監控功能；執行方法是使用拓撲建置器讓前端集區與具備監控資料庫的伺服器產生關聯，然後發行修訂後的拓撲。

**您需要幾個後端監控資料庫？** 單一監控資料庫可支援數萬名使用者 (對於 Microsoft Lync Server 2010，用於監控和封存用途的組合資料庫預估可支援 240,000 名使用者)。此外，單一監控資料庫可供多個前端集區使用；如果組織中有三個前端集區，您可以讓這三個集區全部都與同一個後端存放區產生關聯。

這只是表示對於許多組織而言，在決定所需的後端監控資料庫數目時，資料庫容量並非決定要素。網路速度反而是更重要的考量要點。假設您有三個前端集區，但其中一個集區的網路連線速度緩慢。在那種情況下，您可能會想要使用兩個監控資料庫：一個資料庫處理網路連線良好的兩個集區，而另一個資料庫處理網路連線較慢的集區。

規劃監控基礎結構時，您也應該考慮讓 Lync Server 2013 支援使用鏡像資料庫。「資料庫鏡像功能」讓您能夠同時維護兩個分別位於不同伺服器上的資料庫複本。每當資料寫入主要資料庫時，也會將相同的資料寫入鏡像資料庫。萬一主要資料庫發生失敗或是無法使用，您可以使用簡單的 Lync Server 命令，容錯移轉到鏡像資料庫。例如：

    Invoke-CsDatabaseFailover -PoolFqdn atl-cs-001.litwareinc.com -DatabaseType "Monitoring" -NewPrincipal "Mirror"

這是進行規劃時的要點，因為鏡像功能會讓您所需的資料庫數目加倍：每一個主要資料庫都將需要一個做為鏡像的次要資料庫。

**Lync Server 網站是否需要自訂的監控設定？** 當您安裝 Lync Server 2013 時，也會安裝通用的 CDR 與 QoE 組態設定集合；這些全域集合讓您能在整個組織套用相同的 CDR 與 QoE 設定。在許多情況下，這樣便足夠：您通常會想為所有使用者啟用 CDR 監控功能。

不過，有時候您會想讓不同的網站套用不同的設定。例如，您也許想要在 Redmond 網站使用 CDR 與 QoE 監控功能，但在 Dublin 網站只使用 CDR 監控功能。同樣的，您可能想讓監控資料在 Redmond 網站上保留 60 天，但這類型的資料在 Dublin 網站只需保留 30 天。 Lync Server 2013 可讓您在網站範圍建立個別的 CDR 與 QoE 組態設定集合，進而能以不同的方式管理各個網站 (這包括啟用和停用監控功能，以及設定管理設定，例如，要保留資料的時間長度)。

請注意，您可以在部署監控功能之前或之後決定做法。例如，您可以部署監控功能，然後使用全域設定來管理整個組織。如果您稍後改變心意，可以建立個別的設定集合 (假設要用於 Redmond 網站)，然後使用那些設定來管理 Redmond 的監控功能 (在網站範圍套用的設定一律優先於在全域範圍套用的設定)。如果您再次改變心意，只要刪除 Redmond 網站套用的組態設定即可。在移除網站設定集合時，該網站將會自動套用全域的設定集合。

