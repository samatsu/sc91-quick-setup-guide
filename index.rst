.. Sitecore 9.1 quick set up guide documentation master file, created by
   sphinx-quickstart on Mon Nov  6 14:29:07 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Sitecore 9.1 クイックセットアップガイド
======================================================================
このドキュメントでは、Sitecore ９.1 の評価および開発用に、単一サーバーで動作するオールインワンの環境(XP0)を構築する手順を記載します。
インストール手順はSitecore 9.1の本体をダウンロードできるページの Quick Installation Guideをベースにしていますので、記載内容が不明な場合はそちらも併せて確認してください。

インストールに利用したソフトウェアのバージョンは次の通りです。


..  :OS: Windows Server 2016 Standard
  :Detabase:    SQL Server 2017 SP2 Developer Edition 
  :Sitecore:    9.1 Initial Release

.. csv-table:: セットアップに必要なソフトウェアとバージョン
   :header: "名前", "バージョン", "備考" 

   "Windows", "Winhdows Server 2016 Standard ","デスクトップエクスペリエンス"
   "SQL Server", "SQL Server 2017 Developer Edition", ""
   "Solr", "7.2.1", "バージョンに対応したJavaもインストールする必要があります"
   "Sitecore", "9.1 Initial Release", ""

.. note:: セットアップに必要なソフトウェアの種類とバージョンはセットアップを行うSitecoreのバージョン用のインストールドキュメントを参照してください。
          Sitecoreのバージョンごとに必要なソフトウェアのバージョンは`KBのサイト <https://kb.sitecore.net/articles/087164>`__を使用すると、一覧で確認することができます。

このドキュメントは Windows Server がクリーンインストールされた環境がある前提で、必要なミドルウェアおよびSitecoreのセットアップを行う手順を記載していきます。
本ドキュメントでは記載しませんが、Sitecore環境セットアップ後に、開発用にVisual Studioをセットアップしたい場合は、Visual Studio Community EditionをWebから
無償で入手することができます。SQL Server DeveloperエディションもWebから無償で入手できます。Sitecore, Solrに関しては、ドキュメントの中にダウンロード方法が記載されています。

.. note:: セットアップはインターネットに接続している環境で行ってください

.. warning:: スタンドアロン(XP0)環境を構築する場合は、 Windows Server 2016以降かWindows 10をご利用ください。

.. toctree::
   :maxdepth: 2
   :caption: コンテンツ:

   prerequisites/index
   installation/index
   misc/index



