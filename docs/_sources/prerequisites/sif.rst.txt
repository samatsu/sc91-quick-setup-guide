================================================================
SIFのインストール
================================================================
SIF(Sitecore Install Framework) をインストールします。

.. warning:: Sitecoreのバージョンごとに必要となるPowerShellおよびSIFのバージョンが異なる可能性があります。


PowerShell のバージョン確認
================================================================

Sitecore 9.1の場合、PowerShell は5.1 以降のバージョンが必要です。 Windows Server 2016の場合特に問題ないと思いますが、念のため確認します。

PowerShellを起動して、``$PSVersionTable`` と入力して実行します。

.. figure:: /images/prerequisites/pre-sif01.png

SIFのインストール
====================================================================
Sitecore 9.2の場合は、SIF 2.0.0 以降のバージョンが必要です。
管理者としてPowerShell を起動し、次のコマンドを実行してリポジトリを登録します。
確認メッセージが表示されたら ``y`` を入力します。

.. code:: powershell

   Register-PSRepository -Name SitecoreGallery -SourceLocation https://sitecore.myget.org/F/sc-powershell/api/v2

リポジトリ登録後、SIFをインストールします。確認メッセージが表示されたら ``y`` を入力します。

.. code:: powershell

   Install-Module SitecoreInstallFramework

下記コマンドで、2.0.0 (またはそれ以降)がインストールされたことを確認します。

.. code:: powershell

   Get-Module SitecoreInstallFramework –ListAvailable

.. figure:: /images/prerequisites/pre-sif02.png


これでSIFのインストールは完了です。