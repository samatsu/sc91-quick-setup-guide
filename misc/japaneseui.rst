================================================================
日本語化の設定
================================================================
Sitecoreの編集環境とデフォルトのライブサイトのデフォルトの言語を日本語にする方法を記載します。

手順としては次の2つの方法があります。

方法 1: InstallLanguage.aspxを使用する
================================================================
InstallLanguage 管理ツールを使用して編集ツールや編集言語のデフォルトを日本語にすることができます。
ツールは /sitecore/admin/InstallLanguage.aspx というパスでアクセスできます。今回の例では、 ``http://sc910.sc/sitecore/admin/InstallLanguage.aspx`` にアクセスします。
このページで、Japanese(Japan)を選択します。 `Run the website an the Sitecore UI in this language` をチェックして、 **Install** をクリックします。

.. figure:: /images/misc/misc-japanese-ui03.png

処理に成功すると、Sitecoreがインストールされたフォルダー(今回の場合 `C:\\inetpub\\wwwroot\\sc910.sc` ) の `App_Config\\Include\\` フォルダー配下に 
**Sitecore.DefaultLanguage.config** という名前のパッチファイルが作成されます。


方法 2: 手動で日本語アイテムを作成し、ja-jp.config ファイルを有効化
==========================================================================
Sitecoreの編集画面から、日本語の言語アイテムを作成し、サンプルのja-jp.config.example を
有効化することでデフォルトの言語を日本語にすることができます。

日本語の言語アイテムの追加
----------------------------------------------------------------
Sitecoreの編集環境にログインして **Control Panel** を起動します。
Control Panel の中の **LOCALIZATION > Add a new language** を選択します。
ここで日本語を選択して追加します。

.. figure:: /images/misc/misc-japanese-ui01.png


日本語をデフォルトにするインクルードファイルを有効化
----------------------------------------------------------------
インクルートファイルを有効化することで、次の言語をデフォルトで日本語にします。

* Sitecore クライアントインタフェースの言語
* 編集するコンテンツのデフォルトの言語
* デフォルトのライブサイトのデフォルトの言語

Sitecore がインストールされたフォルダーの ``App_Config\Include\Examples`` をエクスプローラーで開きます。 例えば、 ``C:\inetpub\wwwroot\sc910.sc\App_Config\Include\Examples`` となります。
フォルダーの、``ja-JP.config.example`` を ``ja-JP.config`` にリネームします。

.. figure:: /images/misc/misc-japanese-ui02.png

ファイルを開くと、shell のサイト(コンテンツエディターなどの編集環境でのデフォルトの編集言語)やライブサイト(website)のデフォルトの言語バージョン、ClientLanguage(編集ツール自身のデフォルトの言語)が ja-jp となるようにパッチが構成されていることがわかります。

これで、ライブサイトや、編集環境のUIおよび編集用のコンテンツの言語がデフォルトで日本語になります。

