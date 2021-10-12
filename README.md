## **aion-service-definitions** 
aion-service-definitions は、aion-core 上で機能する特定のリソースをデプロイ、稼働を行うためのマニフェストファイルです。  

aion-coreについては[こちら](https://github.com/latonaio/aion-core)をご覧ください。  

## 概要  
[aion-coreのセットアップ](https://github.com/latonaio/aion-core)で作成したDocker Imagesからこれらのマニフェストファイルを元に特定の関連リソースを構成します。  
[aion-core-manifests](https://github.com/latonaio/aion-core-manifests) では、aion-core および AION 関連リソースをまとめてdefault.yml に記載していますが、aion-service-definitions は、それらとは別に、services.yml へ特定のリソースを記載することで、プロジェクト固有のアプリケーション・システム・マイクロサービス等のデプロイ、稼働をさせることができます。  

## services.ymlの書き方  
本レポジトリには、services.ymlのサンプルとして、コンテナデプロイメントシステムのために必要なマイクロサービスの設定ファイルが含まれています。  
services.ymlの記述様式には、エッジアプリケーション・エッジシステムとして求められる固有の様式が、含まれます。  
本サンプルファイルにおいて、hera、irisはデバイスの名前、addrはエッジネットワーククラスター内におけるそれぞれのデバイスのIP、titaniadb-sentinelはマイクロサービスの名前です。
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

