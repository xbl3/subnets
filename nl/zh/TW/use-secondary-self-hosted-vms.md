---
copyright:
  years: 1994, 2017, 2018, 2019
lastupdated: "2018-02-28"

keywords: Ms IP addresses, Use Secondary Subnets, own virtual machines

subcollection: subnets

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在自行管理的 VM 上使用次要子網路
{:#use-secondary-subnets-self-hosted-vms}

管理您自己的虛擬機器，且想要那些虛擬機器成為 {{site.data.keyword.BluSoftlayer_notm}} 網路上的頭等公民時，必須利用**次要子網路**。我們將討論有彈性的方式，使用一個以上虛擬機器主機為您的
VM 提供 IP 位址，不論是否參與叢集配置。

在此情境的整個過程中，請參閱[關於子網路](/docs/infrastructure/subnets?topic=subnets-about-subnets-and-ips)以取得關於所說明子網路類型的詳細資料。

因此，假設您有兩部裸機伺服器，讓我們稱為 `aunt` 及 `uncle`。兩者都會在您自己的虛擬機器管理，且各有自己的 IP 位址（從**主要子網路**指派）。您的虛擬機器需要額外的 IP 位址。您可以使用任何類型的次要子網路來達到該目的，但我們建議使用**可攜式次要子網路**作為您 VM 所使用位址的來源。可攜式子網路同時提供 `aunt` 及 `uncle` 對子網路所定義 IP 位址的存取。如此，您便可以在兩部伺服器之間共用那些 IP 位址，且如果您為您的
VM 利用移轉技術，便可以平順地在那些伺服器之間轉移 VM。

現在，假設您已建立兩台虛擬機器 `VPS1` 及 `VPS2`、購買可攜式子網路 129.42.0.0/29，並從其中指派兩個位址給您的虛擬機器。IP 位址的使用會看似如下：

129.42.0.0/29 - 可攜式次要子網路
```
129.42.0.0 – Network
129.42.0.1 – Gateway
129.42.0.2 –
129.42.0.3 – VPS1
129.42.0.4 –
129.42.0.5 – VPS2
129.42.0.6 –
129.42.0.7 – Broadcast
```

現在，假設您想要 VPS1 有更多 IP 位址可以隔離它提供的服務。您絕對可以從 129.42.0.0/29 子網路指派更多位址，但您可能想要只使用該個子網路來讓 VM 上線，而不用於它們的服務。您有兩個選項：1) 購買另一個可攜式子網路 2) 購買靜態子網路。如果您還記得[關於子網路](/docs/infrastructure/subnets?topic=subnets-about-subnets-and-ips)中的可攜式與靜態子網路說明，您將知道雖然可攜式子網路提供彈性，它們同時也並未提供您對所有
IP 位址的存取。如果您只需要比如四個額外的 IP 位址，購買靜態子網路便是有效率的選項。讓我們來試試。

您購買靜態子網路，並收到 129.42.0.100/30。您在購買期間將它遞送至 129.42.0.3，也就是此情境中的 VPS1。這麼做會提供您所有四個 IP 位址以用於伺服器回應 129.42.0.3 的一切內容。同樣地，那目前是 VPS1，但您可以隨時將 129.42.0.3 轉移給 VPS2，而那四個來自 129.42.0.100/30 的新 IP 位址也會跟隨著！讓我們再看一次 IP 位址使用：

129.42.0.0/29 - 可攜式次要子網路
```
129.42.0.0 – Network
129.42.0.1 – Gateway
129.42.0.2 –
129.42.0.3 – VPS1
129.42.0.4 –
129.42.0.5 – VPS2
129.42.0.6 –
129.42.0.7 – Broadcast
```

129.42.0.100/30 - 靜態次要子網路
```
129.42.0.100 – 129.42.0.3 (aka VPS1)
129.42.0.101 – 129.42.0.3 (aka VPS1)
129.42.0.102 – 129.42.0.3 (aka VPS1)
129.42.0.103 – 129.42.0.3 (aka VPS1)
```

簡要地說，我們使用了可攜式子網路來讓 IP 位址可供所有虛擬機器主機使用，然後透過利用靜態子網路，讓更多 IP 位址可供虛擬機器使用。您當然可以使用來自原始可攜式子網路的位址，也可以乾脆新增另一個可攜式子網路。我們希望這個情境說明了不只可以遞送靜態子網路至可攜式子網路上的 IP 位址，實際上這麼做也是有效率又實用。