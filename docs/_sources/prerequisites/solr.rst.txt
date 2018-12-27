================================================================
Solrのセットアップ
================================================================
SitecoreのアイテムおよびxDBのデータを検索する検索エンジンとして使用するSolrをセットアップします。


Javaのインストール
================================================================
Solr 7.2.1 が動作するには Java 8 以降がインストールされている必要があります。Java 1.8の実行環境をインストールします。

`こちらから <http://www.oracle.com/technetwork/jp/java/javase/downloads/jre8-downloads-2133155.html>`__  Java 1.8の最新のバージョンをダウンロードします。
今回は、ページ内の 8u192のセクションで、 **Accept License Agreement** を選択して、 Windows x64用のオフラインインストーラー( ``jre-8u192-windows-x64.exe`` )をダウンロードした前提で説明を記載します。

ダウンロードしたファイルを **右クリック > プロパティ** をクリックます。プロパティ画面で、**ブロックの解除** を選択して、**適用ボタン** をクリックします。

``jre-8u192-windows-x64.exe`` をダブルクリックします。ウィザードが起動したら、**インストール** ボタンをクリック。

.. figure:: /images/prerequisites/pre-solr01.png

インストールが終わったら、 **閉じる** ボタンをクリックしてインストールを完了します。
デフォルトのインストールオプションのままインストールした場合は、``C:\Program Files\Java\jre1.8.0_192\bin`` にjavaのプログラムがインストールされます。

.. figure:: /images/prerequisites/pre-solr02.png

コマンドプロンプトを起動して、``java -version`` コマンドを実行して、インストールされたバージョンを確認します。

.. code-block:: bat

  C:\>java -version
  java version "1.8.0_192"

.. note:: 以降の Solr のインストールや動作確認がうまくいかない場合は JAVA_HOMEという名前の環境変数を定義して、Javaがインストールされたパスを指定してください。


Solrのインストール
================================================================
続いて、Solrをインストールします。基本的にはzipファイルをダウンロードして展開するだけです。

`ここ <http://archive.apache.org/dist/lucene/solr/7.2.1/>`__ から、 ``solr-7.2.1.zip`` をダウンロードします。

ダウンロードしたファイルを **右クリック > プロパティ** で、 **ブロックの解除** を選択して、**適用ボタン** をクリックします。

zipファイルを展開し、適当な場所に配置します。今回は、 ``C:\`` 直下に、展開した ``solr-7.2.1`` フォルダーにzipファイルを展開した前提で、手順を記載します。

.. figure:: /images/prerequisites/pre-solr03.png

Solrの構成
================================================================
SitecoreおよびxConnectとSolr間でSSLを使用した通信を行えるように、Solrの構成を変更します。

.. note:: SolrでSSL通信を行う環境のセットアップ方法については `enabling ssl <https://lucene.apache.org/solr/guide/7_2/enabling-ssl.html>`__ も参照してください。

Solrで使用する自己証明書を作成します。java に付属する ``keytool.exe`` を使って証明書を作成します。コマンドプロンプトで、keytool.exe をファイル名だけで実行できるようにPATHを通します。

.. code-block:: bat

 set PATH=C:\Program Files\Java\jre1.8.0_192\bin;%PATH%

.. note:: binフォルダーまでのパスはインストールしたバージョンによって異なります。

次に、Solrで使用する jks ファイルを作成します。

.. code-block:: bat

 keytool -genkeypair -alias solr-ssl -keyalg RSA -keysize 2048 -keypass secret -storepass secret -validity 9999 -keystore solr-ssl.keystore.jks -ext SAN=DNS:localhost,IP:127.0.0.1 -dname "CN=localhost"
 
keypass および storepass オプションで、今回は ``secret`` というパスワードを指定しています。このパスワードは以降のコマンドやウィザードで使用します。

jksファイルから、p12 ファイルを作成します。

.. code-block:: bat

 keytool -importkeystore -srckeystore solr-ssl.keystore.jks -destkeystore solr-ssl.keystore.p12 -srcstoretype jks -deststoretype pkcs12

このとき、コマンドプロンプトで次のパスワードを入力するようにプロンプトが表示されますが、今回はすべてに ``secret`` と入力します。

* 出力先キーストアのパスワードを入力してください:
* 新規パスワードを再入力してください:
* ソース・キーストアのパスワードを入力してください:

次の図がコマンドの実行例です。

.. figure:: /images/prerequisites/pre-solr04.png

コマンドを実行したフォルダーに ``solr-ssl.keystore.jks`` および、 ``solr-ssl.keystore.p12`` ファイルが作成されていることを確認してください。

作成した証明書は、Sitecoreおよび、xConnectが動作するサーバーにインストールします。今回は、スタンドアロン環境なので、Solrをセットアップしたマシンにインストールします。

p12ファイルを右クリックし、 **PFXのインストール** をクリックします。

.. figure:: /images/prerequisites/pre-solr05.png


証明書のインポート ウィザード が開始されるので、 保存場所に **ローカル コンピューター** を選択して、 **次へ** をクリックします。

.. figure:: /images/prerequisites/pre-solr06.png

インポートファイルが適切に選択されていることを確認したら **次へ** をクリックします。

.. figure:: /images/prerequisites/pre-solr07.png

秘密キーの保護画面が表示されたら、 パスワードを入力します。 手順に従っている場合、 ``secret`` を入力します。

.. figure:: /images/prerequisites/pre-solr08.png

証明書ストアを選択する画面で、 **証明書をすべて次のストアに配置する** を選択。**参照** ボタンをクリックして **信頼されたルート証明機関** を選択して、 **OK** をクリックし、
選択ダイアログを閉じます。 **次へ** をクリックします。

.. figure:: /images/prerequisites/pre-solr09.png

証明書インポートウィザードの完了 画面が表示されたら、 **完了** をクリックします。

.. figure:: /images/prerequisites/pre-solr10.png

下記ダイアログが表示されたら **OK** をクリックしてます。

.. figure:: /images/prerequisites/pre-solr11.png

solrでjks ファイルを使用するので作成した jks ファイルをコピーしておきます。

.. code-block:: bat

 copy solr-ssl.keystore.jks C:\solr-7.2.1\server\etc

Solrで、jksファイルを使用するように設定ファイルを変更します。``C:\solr-7.2.1\bin\solr.in.cmd``  をメモ帳で開きます。

デフォルトで次のように設定されている場所を見つけ、コメントを解除します。

.. code-block:: bat

  REM set SOLR_SSL_KEY_STORE=etc/solr-ssl.keystore.jks
  REM set SOLR_SSL_KEY_STORE_PASSWORD=secret
  REM set SOLR_SSL_KEY_STORE_TYPE=JKS
  REM set SOLR_SSL_TRUST_STORE=etc/solr-ssl.keystore.jks
  REM set SOLR_SSL_TRUST_STORE_PASSWORD=secret
  REM set SOLR_SSL_TRUST_STORE_TYPE=JKS
  REM set SOLR_SSL_NEED_CLIENT_AUTH=false
  REM set SOLR_SSL_WANT_CLIENT_AUTH=false

変更後、次のようにになります。ファイル名やjksファイルを配置している場所やパスワードは環境に応じて適宜変更してください。

.. code-block:: bat

  set SOLR_SSL_KEY_STORE=etc/solr-ssl.keystore.jks
  set SOLR_SSL_KEY_STORE_PASSWORD=secret
  set SOLR_SSL_KEY_STORE_TYPE=JKS
  set SOLR_SSL_TRUST_STORE=etc/solr-ssl.keystore.jks
  set SOLR_SSL_TRUST_STORE_PASSWORD=secret
  set SOLR_SSL_TRUST_STORE_TYPE=JKS
  set SOLR_SSL_NEED_CLIENT_AUTH=false
  set SOLR_SSL_WANT_CLIENT_AUTH=false

これで準備完了です。コマンドプロンプトを起動して、 solr start と入力して起動することを確認します。下図は実行例です。

.. figure:: /images/prerequisites/pre-solr12.png

ブラウザーを起動して、 ``https://localhost:8983/solr`` にアクセスして画面が表示されることを確認します。

.. figure:: /images/prerequisites/pre-solr13.png

これでSolrをコマンドプロンプトから起動できるようになりました。次のコマンドを実行してSolrを停止します。

.. code-block:: bat

  solr stop -all

SolrをWindowsサービスとして動作するように構成
================================================================
`NSSM <https://nssm.cc>`__ を使用して、SolrをWindowsサービスとして動作するようにします。

`ダウンロードページ <https://nssm.cc/download>`__ にアクセスして、最新のプログラムをダウンロードします。本ドキュメント作成時点の最新のバージョンは2.24です。
``nssm-2.24.zip`` を展開します。今回は、次の図のように ``C:\Program Files\nssm-2.24`` に展開したファイルを配置しました。

.. figure:: /images/prerequisites/pre-solr14.png

管理者としてコマンドンプロンプトを起動し、次のコマンドを実行します。

.. code:: bat

  nssm install solr-7.2.1

.. figure:: /images/prerequisites/pre-solr15.png

ダイアログが表示されるので、 **Application** タブのPath, Startup directory, Argument, Service nameを設定します。必要に応じて適宜パラメーターを変更してください。


パラメーターを設定後 **Install service** ボタンをクリックします。

.. csv-table:: パラメーター
   :header: "名前", "設定値例" 

    "Path", "C:\\solr-7.2.1\\bin\\solr.cmd"
    "Startup directory", "C:\\solr-7.2.1\\bin"
    "Arguments", "start -f -p 8983"
    "Service name", "solr-7.2.1"

.. figure:: /images/prerequisites/pre-solr16.png

成功メッセージが表示されます。

.. figure:: /images/prerequisites/pre-solr17.png

``Win+r`` をタイプして **ファイル名を指定して実行** を表示して、``services.msc`` を入力して、サービススナップインを起動します。solr-7.2.1 を見つけて、
開始し、 ``https://localhost:8983/solr`` にアクセスできることを確認します。

.. figure:: /images/prerequisites/pre-solr18.png

これでSolrのセットアップは完了です。
