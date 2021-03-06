# Dockerize

將原本的流程拆成三個部分

- Selenium Server

- Build Project

- Run Testing



接下來開始為這三個階段編寫其需求的容器配置

## Selenium Server

直接使用 selenium 提供的 image `selenium/standalone-firefox-debug:2.53.0`

> 要特別注意的是網路的設定，需要為 VNC 和 Selenium 留下通道

##### Selenium API Port

```yaml
    expose:
      - "4444" 
```

讓之後進行測試的容器可以透過這個 port，讓像 WebdriverIO 這樣的Selenium Client 遠端控制 Selenium Server 進行測試

##### VNC Port

```yaml
    ports:
      - "5900:5900"
```

這邊是做 Port Forwarding 讓電腦的 localhost:5900 導向到容器的 5900 port  
這樣可以透過 VNC 連線觀看瀏覽器測試的狀況


## Build Project Environment

```
  build:
    container_name: e2e_build
    image: node:7.6
    command:  bash -c "cd wd-ex01 && rm -rf node_modules && npm install && cd ../wd-ex02 && rm -rf node_modules && npm install"
    working_dir: /e2eSample
    volumes:
      - ./e2eSample:/e2eSample
```

#### 設定 volumes 掛載專案資料夾

容器應該是乾淨的執行環境
每次刪掉重啟都會是全新的
因此透過上面的 volumes 設定將本機的 e2eSample 資料夾掛載到容器中，容器中才能讀到專案程式碼

#### command 設定要執行的 script

有了專案程式碼之後就可以開始我們建置環境的 script 了，這個 sample 以 JavaScript 為例，而容器環境可能和本機不同，因此需要在容器中重新安裝 node_modules，如果專案有其他建置步驟也可將指令加入 command 中，在這階段一起完成

## Test Execution Environment

```yaml
  test-ex01:
    image: node:7.6
    command: "npm run test"
    working_dir: /e2eSample/wd-ex01
    volumes:
      - ./e2eSample:/e2eSample
    networks:
      - front-tier
```

這邊以執行 ex01 的測試檔案為例  
由於專案建置的步驟應該在上一個 `build` 階段就已經執行  
且因volume掛載同一個外部資料夾，因此安裝過的 modules 會保存下來  
因此這個容器只要需做執行測試的步驟



---

以上三個部分都配置好後

依序執行 

```bash
$ docker-compose up -d selenium # -d 表示在背景執行
$ docker-compose run --service-ports build
$ docker-compose run --service-ports test-ex01
```

