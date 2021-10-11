## **aion-service-definitions** 
aion-service-definitions は、aion-core 上で機能する特定のリソースをデプロイ、稼働を行うためのマニフェストファイルです。  

aion-coreについては[こちら](https://github.com/latonaio/aion-core)をご覧ください。  

## 概要  
[aion-coreのセットアップ](https://github.com/latonaio/aion-core)で作成したDocker Imagesからこれらのマニフェストファイルを元に特定の関連リソースを構成します。  
[aion-core-manifests](https://github.com/latonaio/aion-core-manifests) は、aion-core および AION 関連リソースをまとめてdefault.yml に記載していますが、aion-service-definitions は、services.yml へ特定のリソースを記載することで、デプロイ、稼働をさせることができます。  

## services.ymlの書き方  
hera、irisはデバイスの名前、titaniadb-sentinelはマイクロサービスの名前です。

```
devices:
  hera:
    addr: xxx.xxx.xxx.xxx
    aionHome: /var/lib/aion
  iris:
    addr: xxx.xxx.xxx.xxx
    aionHome: /var/lib/aion
microservices:
  titaniadb-sentinel:
    startup: yes
    always: yes
    withoutKanban: yes
    serviceAccount: controller-serviceaccount
    env:
      MY_NODE_NAME: YOUR_DEVICE_NAME
```
