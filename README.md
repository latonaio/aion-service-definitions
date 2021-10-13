## **aion-service-definitions** 
aion-service-definitions は、aion-core 上で機能する特定のリソースをデプロイ、稼働を行うためのマニフェストファイルです。  

aion-coreについては[こちら](https://github.com/latonaio/aion-core)をご覧ください。  

## 前提条件  
[aion-coreのセットアップ](https://github.com/latonaio/aion-core)でaion-coreをセットアップします。  
[aion-core-manifests](https://github.com/latonaio/aion-core-manifests) では、aion-core および AION 関連リソースをまとめて、template>各サービスのymlファイル（⇒マニフェスト生成後のサンプルファイルとしては default.yml） に記載していますが、aion-service-definitions は、それらとは別に、services.yml へ特定のリソースを記載することで、プロジェクト固有のアプリケーション・システム・マイクロサービス等のデプロイ、稼働をさせることができます。  

## aion-service-definitionsで定義されたマイクロサービスの立ち上げ・稼働  
aion-service-definitionsのservices.ymlで定義されたマイクロサービスは、AION Core の Service Broker により立ち上げ・稼働が制御されます。  

[aion-core](https://github.com/latonaio/aion-core)のcmd>service-broker下のDockerfile-service-brokerに、本レポジトリに該当するマイクロサービスを読み込むためのコンフィグ設定が記載されています。  

```
CMD ["./service-broker", "-c", "config/services.yml"]
```

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

