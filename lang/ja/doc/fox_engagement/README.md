#Force Operation X 
Android向け
F.O.Xエンゲージメント配信

## 1. 概要
本ドキュメントでは、Force Operation X SDK(以下F.O.X)におけるF.O.Xエンゲージメント配信およびCriteoとの連携を行う際に必要となる実装を説明します。対応しているF.O.X SDKのバージョンは **v2.16g** 以上となります。F.O.Xエンゲージメント配信連携を行う場合は同一の箇所にLTVとアクセス解析のそれぞれの計測処理を実装する必要があります。

### 1.1.	SDK仕様
F.O.X SDKアクセス解析機能を利用することにより媒体を横断したイベント計測連携を行います。計測は内容に応じて各種メソッドを実行することで行います。
|:----------:|:-----------:|:------------|
eventName|String|計測を行うイベント種別に応じて、指定されたイベント名を設定します。
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。 
<span style="color:#b8b8b8">label	|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
eventInfo内にアクションに付随する情報をJson形式で設定することで、ダイナミックな配信連携が可能になります。

| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
 
### 1.3. リアルタイムデータフィード更新仕様

| 引数 |必須|型 | 概要 |
|:----------:|:-------:|:----:|:------------|

### 1.4. イベント情報の送信方法

AnalyticsManagerクラスをインポートします。
```java
import jp.appAdForce.android.AnalyticsManager;
```

次のsendEventメソッドを利用し、イベント情報を送信します。
public static void sendEvent(Context context, 
				String eventName,
```
    
　　
　　
　　
　　　　
## 2.イベント計測の実装
F.O.X SDKで対応しているF.O.XエンゲージメントおよびCriteoのイベント計測は以下の５つとなっています。

- View Home イベント

### 2.1	View Home(アプリトップ訪問イベント)実装方法

```java
JSONObject json = new JSONObject("{'din':'2016-01-02','dout':'2016-01-05',
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
eventName|String|“\_view\_toppage”を指定してください。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">int|<span style="color:#b8b8b8">使用しません。
eventInfo(din/dout)|JSONObject|日付の指定がある場合は入力（任意）
eventInfo(criteo_partner_id)|JSONObject|CriteoアカウントIDが同一アプリで異なる場合は入力(任意)
eventInfo(fox_cvpoint)|JSONObject|F.O.Xの成果地点IDを設定します。(任意)
　　
　　　　
### 2.2	View Listing（複数商品閲覧イベント）実装方法

```java
JSONObject json = new JSONObject("{
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">int|<span style="color:#b8b8b8">使用しません。
eventInfo(product)|JSONObject|Product をキーとして商品IDを配列で設定します。
eventInfo(product[].id)|JSONObject|商品IDを設定します。<br>データフィードと同じ商品IDを使⽤してください。
eventInfo(product[].category)|JSONObject|商品カテゴリを設定します。<br>データフィードと同じ商品カテゴリを使用してください。<br>１商品に対して複数カテゴリある場合はカンマ「,」区切り、階層がある場合は「>」で分割します。<br>例）映画、ビデオ>DVD>スポーツ、レジャーnullでも構いません。
eventInfo(din/dout)|JSONObject|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|JSONObject|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)
eventInfo(fox_cvpoint)|JSONObject|F.O.Xの成果地点IDを設定します。
　　
　　　　
### 2.3	View Product（商品閲覧イベント）実装方法

```java
JSONObject json = new JSONObject("{
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">int|<span style="color:#b8b8b8">使用しません。
eventInfo(fox_cvpoint)|JSONObject|F.O.Xの成果地点IDを設定します。
eventInfo(product[].id)|JSONObject|閲覧した商品IDを設定します。
eventInfo(din/dout)|JSONObject|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|JSONObject|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)
　　
　　　　
### 2.4	View Basket（買い物かご）実装方法

```java
JSONObject json = new JSONObject("{
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">value|<span style="color:#b8b8b8">int|<span style="color:#b8b8b8">使用しません。
eventInfo(fox_cvpoint)|JSONObject|F.O.Xの成果地点IDを設定します。
eventInfo(product[].id)|JSONObject|商品ID<br>データフィードと同じ商品IDを使用してください。
eventInfo(product[].price)|JSONObject|該当商品の価格を設定します。
eventInfo(product[].quantity)|JSONObject|該当商品を買った個数を設定します。
eventInfo(currency)|JSONObject|通貨<br>Nil/Nullの場合、デフォルト “JPY”
eventInfo(din/dout)|JSONObject|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|JSONObject|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)
　　
　　　　
### 2.5	Track Transaction（商品購入イベント）実装方法

```java
JSONObject json = new JSONObject("{
```

#### 引数詳細
| 引数 | 型 | 概要 |
|:----------:|:-----------:|:------------|
<span style="color:#b8b8b8">action|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
<span style="color:#b8b8b8">label|<span style="color:#b8b8b8">String|<span style="color:#b8b8b8">使用しません。
orderID|String|（任意）注⽂番号等を指定します。
sku|String|（任意）商品コード等を指定します。
itemName|String|使用しません。
price|double|商品総額を指定します。<br><span style="color:red">※必ず price * quantity の値が商品総額となるよう指定ください
quantity|int|1を指定してください。
currency|int|通貨コードを指定します。<br>nullの場合は”JPY”が指定されます。
eventInfo(fox_cvpoint)|JSONObject|F.O.Xの成果地点IDを設定します。
eventInfo(transaction.id)|JSONObject|注文番号、問い合わせ番号などのトランザクションID
eventInfo(product[].id)|JSONObject|商品IDデータフィードと同じ商品IDを使用してください。
eventInfo(product[].price)|JSONObject|該当商品の価格を設定します。
eventInfo(product[].quantity)|JSONObject|該当商品を買った個数を設定します。
eventInfo(din/dout)|JSONObject|⽇付の指定がある場合は⼊⼒してください。（任意）
eventInfo(criteo_partner_id)|JSONObject|Criteo アカウントID が同⼀アプリで異なる場合は⼊⼒(任意)<br>以下、このアクションによってデータフィードが変動する場合に設定します。
eventInfo(datafeed.product)|JSONObject|変動するデータフィードを設定します。
eventInfo(datafeed.product[].id)|JSONObject|データフィードのアイテムを一意に識別するIDです。
eventInfo(datafeed.product[].action)|JSONObject|データフィードをどのように変更するかを入力します。<br>U:追加もしくは編集　D:削除
eventInfo(datafeed.product[].name)|JSONObject|アイテム名です。<br>以下全て、削除の際はnullで構いません。
eventInfo(datafeed.product[].expire)|JSONObject|アイテムの有効期限です。<br>「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。nullでも構いません。
eventInfo(datafeed.product[].effective)|JSONObject|アイテムの公開日時です。<br>これが設定された場合、公開日時になるまで商品はでません表示されません。<br>「yyyy-MM-dd HH:mm:ss」もしくは「yyyy-MM-dd」の書式で日付を入力してください。nullでも構いません。
eventInfo(datafeed.product[].img)|JSONObject|アイテムの画像URLです。<br>nullでも構いません。
eventInfo(datafeed.product[].category1)|JSONObject|第一階層のカテゴリを指定します。<br>nullでも構いません。
eventInfo(datafeed.product[].category2)|JSONObject|第二階層のカテゴリを指定します。<br>nullでも構いません。
eventInfo(datafeed.product[].category3)|JSONObject|第三階層のカテゴリを指定します。<br>nullでも構いません。
eventInfo(datafeed.product[].price)|JSONObject|アイテムの価格を指定します。<br>nullでも構いません。
eventInfo(datafeed.product[].currency)|JSONObject|アイテムの通貨コードを指定します。<br>nullの場合、JPYが適用されます。
eventInfo(datafeed.product[].{任意})|JSONObject|その他配信、分析に使用する項目を指定します。

