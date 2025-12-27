# Lab01: VLAN 基本構成

## 概要
Switch上でVLANを作成し、ポートごとにVLANを分離する。

## ネットワーク構成
- Switch: Cisco 2960
- PC ×2
  - PC1 → VLAN10
  - PC2 → VLAN20

## IPアドレス設計
| デバイス | VLAN | IPアドレス | サブネット |
|--------|------|-----------|-----------|
| PC1 | VLAN10 | 192.168.10.10 | /24 |
| PC2 | VLAN20 | 192.168.20.10 | /24 |

※ Router未使用のため Default Gateway は未設定

## Switch設定
```txt
vlan 10
 name VLAN10
vlan 20
 name VLAN20

interface fa0/1
 switchport mode access
 switchport access vlan 10

interface fa0/2
 switchport mode access
 switchport access vlan 20

確認コマンド
show vlan brief

動作確認
    •    PC1 → PC2 ping：失敗（仕様通り）
    •    VLAN間通信にはL3機器が必要

学んだこと
    •    VLANはブロードキャストドメインを分割する
    •    Switch（L2）だけではVLAN間通信はできない
    •    VLAN作成だけでなくポート割り当てが重要
EOF
