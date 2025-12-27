# Lab02: Router-on-a-Stick

## 概要
Router-on-a-Stick構成により、VLAN間通信を実現する。

## 目的
- VLAN10 ↔ VLAN20 の通信を可能にする
- Default Gateway の役割を理解する

## 構成予定
- Router ×1
- Switch ×1
- PC ×2

## 学習ポイント
- trunk / access
- サブインターフェース
- 802.1Q

## トラブルシューティング・確認ポイント

### ping が最初に失敗した理由
- 初回の ping は ARP 解決が未完了のため失敗する場合がある
- 2回目以降の ping で成功するのは正常な挙動

### 確認したポイント
- Switch ⇔ Router 間ポートが trunk（802.1Q）になっていること
- VLAN10 / VLAN20 が trunk で許可されていること
- Router 側でサブインターフェース（G0/0.10, G0/0.20）が up/up であること
- PC の Default Gateway が Router のサブインターフェース IP に設定されていること

### 使用した確認コマンド
```txt
show vlan brief
show interfaces trunk
show ip interface brief

### 学習メモ
    •    VLAN 間通信では L2（Switch）と L3（Router）の役割分担が明確
    •    Switch はフレーム転送のみ、ルーティング判断は Router が行う
    •    Router-on-a-Stick は VLAN 数が少ない環境で有効な構成
