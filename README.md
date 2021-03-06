# E2E Website Testing Dojo

**協力單位：創科資訊**

### 緣由

在現今的 web 開發，軟體技術推成出新，開發方式也不停的進化，唯有測試是在開發的過程中，最容易被忽略，一但專案啟動時未考量到對於品質的控管，在開發的中後期要在加入，將會困難重重...

但技術的演進，也讓測試的進行更加的容易，期望透過簡單體驗的形式，讓大家可以了解 web e2e 測試的運作沒有想像中的複雜，並且搭配 CI 自動化程序進行自動化測試，除了自己測試之外，也讓 CI 自動進行整體自動化測試，也經由這樣的體驗，了解測試其實不難，在相關測試技術的幫忙下，可以有效率的進行，進而提高測試導入的意願。

### 預計計畫

以兩個電腦為一組

電腦 A：CI 持續整合 server
電腦 B：使用者編寫 e2e 測試

預計將會設計一個測試情境，讓使用者完成事先定義好的測試案例

然後會準備三個情境

本機開發 e2e 測試- develop
docker 本機開發 e2e 測試 - production
搭配 CI 執行 e2e 測試- test

透過相關環境的預先建置，省去使用者要進行測試時需要進行環境建置的麻煩。

另外會有一組解說，環境建置的細節。

### 期望效果

透過此練習，讓學員可以認識 e2e 測試也可以很簡單，也讓學員了解到測試如何在持續整合中進行自動化測試，並且進一步加強相關課程的宣傳。

### E2E Website Testing Dojo

體驗技術最快的方式，莫過於自己動手做，測試在一定程度複雜的專案都知道其必要性，但卻最常被忽略，一但專案啟動時未考量到對於品質的控管，在開發的中後期要在加入，將會困難重重...

所幸技術的演進，也讓測試的進行更加的容易，透過設計好的 Hands-On Labs，讓大家了解 E2E Website 測試的運作
並且搭配 CI（持續整合）進行自動化測試，體驗在專案的開發上，根據不同狀況盡讓測試協助開發。

* [Dojo 1：develop Auto testing mode: 前端 E2E Testing](e2eSample)

開發離不開測試，透過此 Dojo 了解在工程師的開發環境下，如何撰寫 E2E Testing

* Dojo 2：前端 E2E (End to End) Testing with Docker

實際動手做，了解如何使用 Docker 進行自動化的 E2E 前端測試，讓前端測試更容易進行，即使沒有桌面環境，透過 Docker 的協助，只要有 Docker 的運作環境，可在任何地方進行前端測試。

* Dojo 3：Run Auto testing mode: 前端 E2E Testing With CI

E2E Testing 透過 CI 搭配 Docker 運行，讓 CI 即使沒有安裝 UI 環境或是 Browser 即可以進行前端自動化測試，更靈活地搭配 Docker 進行部署與測試、強化開發流程。

# Setup

```
# build project
$ docker-compose up build
```

# Run

```
# 1. up selenium server
$ docker-compose up selenium

# 2. test
$ docker-compose up test-ex01
$ docker-compose up test-ex02
```

# VNC

vnc://localhost:5900
password: secret