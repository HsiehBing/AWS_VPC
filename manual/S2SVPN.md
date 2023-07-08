# Site-to-Site VPN 設定
## 最後更新日期：2023.07.08

1：建立客戶閘道

BGP ASN : 有點像port，地雲端要設不一樣

沒有難度，地端Public IP

2：建立目標閘道

建VGW，沒難度

建立完之後要右上角、連結VPC

3. Site-to-Site VPN

虛擬私有閘道、路由：動靜態都可、本機IPV4 遠端IPV4都設0.0.0.0/0

可能連不能DPD重新啟動

個別tunnel可以啟動VPN紀錄

4.設定路由

| 目的地 | 目標 | 狀態 | 紀錄備註 |
| --- | --- | --- | --- |
| 雲端VPC網段 | local |  | 預設會有 |
| 地端VPC網段 | 上面建立的VGW |  | 自己建 |

4：更新安全群組

EC2 security group inbound allow 地端的Private 網段

6：下載組態檔案

地端設備不同而不同

7：設定客戶閘道裝置
