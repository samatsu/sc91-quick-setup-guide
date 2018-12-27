================================================================
インストール後の処理
================================================================
Sitecoreをインストールしたら、 Installation Guide (Quick Installation Guideではありません)の内容に従って、後処理を実施します。Sitecore 9.1 Initial Release用の Installation Guideの6章の手順に従って、後処理を実施していきます。バージョンによって作業が異なる可能性があるので、利用するSitecoreのバージョンのInstalltion GuideのSitecore XP Post-Installation Stepsを参照するようにしてください。

Sitecoreの初期化処理
================================================================
ラウンチパッドにログインし、 **Control Panel** を起動します。今回のケースでは、ブラウザーで ``http://sc910.sc/sitecore`` にアクセスし、adminユーザーでログイン後に表示される
ラウンチパッドの Control Panel をクリックします。
Indexing Manager を起動して、すべてのインデックスを選択して、**Rebuild** をクリックしてリビルドします。

.. figure:: /images/installation/ins-post01.png

次に、**Reibuid link databases** をクリックして、リンクデータベースをリビルドします。

.. figure:: /images/installation/ins-post02.png

次に、**Deploy marketing definitions** をクリックして、マーケティング定義をデプロイします。
ポップアップダイアログですべての項目選択して、**Deploy** をクリックします。
この処理を完了するには数分時間がかかります。

.. figure:: /images/installation/ins-post03.png

IISの静的コンテンツのキャッシュの設定
================================================================
IIS管理マネージャーを起動します(`Win+r` で ``inetmgr`` をタイプして起動できます)。Sitecore本題が動作しているサイトを選択します。今回の場合は **sc910.sc** です。
中央の画面で **HTTP応答ヘッダー** をダブルクリックします。

.. figure:: /images/installation/ins-post04.png

右側の操作ペインの **共通のヘッダー** をクリックして、静的コンテンツの有効期間を 7日間 に設定して、 **OK** をクリックします。

.. figure:: /images/installation/ins-post05.png

パフォーマンスカウンター用のセキュリティー設定
================================================================
各アプリケーションプールのユーザー(デフォルトのままの場合 IIS AppPool\sc910.sc, IIS AppPool\sc910.xconnect, IIS AppPool\sc910.identity) をビルトインの
Performance Monitor Users グループのメンバーにします。

.. figure:: /images/installation/ins-post06.png

これでポストステップは完了です。IISを再起動するか(iisreset) 、コンピューターを再起動します。

