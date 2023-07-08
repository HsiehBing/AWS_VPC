# VPC peering 設定
## 更新日期:2023.07.08
## 建置設定

1. VPC建置

說明：

- 可以選擇VPC only介面，這個介面比較是用來在一個AZ中建立多個subnet使用。

如果選擇VPC and more 可以一次建立Subnet、Route tables、Network connection(IGW、NAT gateway)

- 選擇IPv4的CIDR可以有三個大方向選：10.0.0.0/8、172.16.0.0/12、192.168.0.0/16 可以根據需求選擇
- 選擇AZ，以及public以及private subnet數量
- NAT gateway可以用來將資料由private 單向傳出
- DNS options 預設開啟

需要至兩個region都設定VPC

額外說明：如果使用private subnet 可以由NAT Gateway將資料傳出，但是如果要造放需要透過跳板機、SSM等方法才能登入，跳板機的使用是另外在public subnet開一台EC2，先ssh到跳板機再ssh到private subnet。

1. Peering connection 設定
- 至vpc peering connectio設定，設定名稱以及選擇剛剛設定的VPC，以及預對街的VPC，設定完後至另一個Region的VPC中點選確認。
- 至該VPC 的 private subnet 的Route Table加上 peering的範圍以及peering，加上後即可連線。

### VPC Route table 設定

1.在public subnet與private subnet 各需要一張route table。在public subnet需要用IGW、private NAT gateway


## 安裝套件

sudo yum install cronie -y

sudo service crond start

sudo yum install tree -y

## 操作設定

mtr會需要透過crontab去執行，ping的話可以設定時間以及背景執行所以不用
```
mtr設定:

/usr/sbin/mtr -i 5 -c 60 -r {IP}  &> /home/ec2-user/MTRTest/public/S2TPublic_$(date +%m-%d_%H:%M).txt

crontab設定:

sh /home/ec2-user/MTRTest/public/S2Tpublic.sh

ping:

ping -i 60 {IP} 2>&1 | while IFS= read -r line; do echo "$(date +"%m-%d %H:%M") $line"; done >>S2Tpublic.txt &
```

## 資料下載

關鍵字：scp -i 

