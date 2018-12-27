================================================================
インストール用パッケージのダウンロードとライセンスの配置
================================================================
スタンドアロンインストール(開発環境)用のパッケージをダウンロードします。

パッケージのダウンロード
================================================================
`https://dev.sitecore.net <https://dev.sitecore.net>`_ から、インストール対象のSitecoreのバージョンのページに移動します。
`Download options for On Premises deployment` セクションの `Packages for XP Single` をクリックしてXP0用のインストールモジュールをダウンロードします。

.. figure:: /images/installation/ins-down01.png

.. warning:: ダウンロードするには、開発者向けの認定試験に合格している必要があります。

今回の場合は Sitecore 9.1 Initial Releaseを対象としているので、Sitecore 9.1.0 rev. 001564 (WDP XP0 packages).zip をダウンロードした前提で説明を記載します。

.. note:: ダウンロードするパッケージファイルの名前はSitecoreのバージョンによって変わります。

zipファイルを ``右クリック > プロパティ``  を選択してブロックを解除した後に、ダウンロードしたファイルを展開します。


ファイルの配置
================================================================
展開したファイルの中にある、XP0 Configuration files 9.1.0 rev. 001564.zip を展開します。
展開したフォルダーの中にあるすべてのファイルを、``C:\resourcefiles`` **直下** に移動します。

.. figure:: /images/installation/ins-down02.png

ダウンロードしたzipファイルのあった、残りの Sitecore, Xconnect, IdentityServer 用の WDPパッケージも ``C:\resourcefiles`` **直下** に移動します。

.. figure:: /images/installation/ins-down03.png


ライセンスファイルの配置
================================================================
ライセンスファイル(license.xml)も ``C:\resourcefiles`` に配置します。

これでインストール用のファイルの準備完了です。