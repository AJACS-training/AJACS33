# 遺伝子発現DB・解析ツールの紹介};　　　　担当： 内藤 雄樹


----

## 遺伝子のDB・ウェブツールの基礎 

### 遺伝子をさがす（基礎） 
- NCBI Entrez -- http://www.ncbi.nlm.nih.gov/ → Nucleotideで検索
- 絞り込み
	- 検索窓にキーワードを追加、ブラケットでフィールド指定
		- ... AND “Homo sapiens”[Organism] (ダブルクオートでフレーズ検索)
		- ... AND Vimentin[Gene Name]
		- ... AND patent[Title]
	- または、[Advanced search](http://www.ncbi.nlm.nih.gov/nuccore/advanced)に行く

### 遺伝子の ID とは？ 
1. Accession Number
	- GenBank/EMBL/DDBJ の国際塩基配列データベースに登録された塩基配列のID
	- A12345 や AB123456 の形式をしている
		- 参考：[アルファベットの部分の割り当て](http://www.ddbj.nig.ac.jp/sub/prefix.html)
	- A12345.1 のようにバージョンを表示。UTRが延長されたりエラーが修正されて A12345.2 のようにアップデートされる
	- 正確な表現ではないが、俗に「GenBankの」Accessionと呼ばれることもある
1. RefSeq ID
	- 三大データバンクの配列を元にtranscriptごとに1個登録 → RefSeq データベース（遺伝子の百科事典のようなもの）
	- 選択的スプライシングで生じるvariant には別々のIDが付与されている
	- NM_012345.6 の形式をしている。広義には（実用上は）Accession番号の一種
1. SymbolとGene ID
	- 遺伝子ごとに付与される遺伝子名と番号
	- Symbolは慣用名と一致しないこともある（ヒトp53 → TP53）
	- 種でダブる可能性も
	- Gene ID は種と遺伝子を特定できる
	
| 慣用名 | Symbol | Gene ID |
|----|----|---:|
| ヒトcadherin | CDH1 | 999 |
| マウスcadherin | Cdh1 | 12550 |
| ラットcadherin | Cdh1 | 83502 |
 
1. それぞれの関係
## ref(IDs.png)

### 配列から遺伝子をさがす 
- aatgagggtttgaatcgtgaccatttcttaagttttgcgtggtgcgtttatgataagctt (シロイヌナズナ)
- tgaatgaagacgatcgactcaaattcacagctccacaggatggaattcttcttaacaaagctcgacaattcgga (線虫)
- NCBI BLAST -- http://www.ncbi.nlm.nih.gov/BLAST/
- UCSC BLAT -- http://genome.ucsc.edu/ → BLATへ

### 統合遺伝子検索GGRNA 
http://ggrna.dbcls.jp/
- [【統合TV】GGRNAで遺伝子をGoogleのように検索する](http://togotv.dbcls.jp/20120124.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
- [【新着レビュー】統合遺伝子検索GGRNA：遺伝子をGoogleのように検索できるウェブサーバ](http://first.lifesciencedb.jp/from_dbcls/e0001)
- GGRNAとは？
	- RefSeqを全文検索
	- 塩基配列も簡単検索、3ミスマッチを許容
	- ヒト、マウス、ラット、ニワトリ、ツメガエル、ゼブラ、ホヤ、ハエ、線虫、シロイヌナズナ、イネ、出芽酵母、分裂酵母（現在13種）
- 【実習1】簡単な検索例
	- トップページを参考に各自で遺伝子名、フレーズ、各種ID、塩基配列などを検索
	- 参考：検索時間はヒット件数に比例するため、ものすごくヒット件数が多い場合は時間がかかるかもしれません。
- 【実習2】配列検索：ヒトのある遺伝子に対してRT-PCRを掛けようとしたらなぜかバンドが2本。これはいったい？
	- primer(F): agctcattactttatcagtgca
	- primer(R): tgacgtattcactcttctggtt
	- 増幅遺伝子のSymbol、Refseq ID、予想されるバンドのサイズを調べてみる
		- DGCR8, NM_001190326, 402bp
		- DGCR8, NM_022720, 501bp
		- 同じ遺伝子の2つのvariantが増えてしまったらしい。
- 【実習3】マイクロアレイのプローブの場所を知りたい。
	- Affymetrix社 GeneChipマイクロアレイの場合、1遺伝子につき25塩基×11対のプローブで検出
	- プローブセットと呼ぶ。例：262888_at → [GGRNAで検索](http://ggrna.dbcls.jp/at/search.cgi?query=262888_at)
		- PM (perfect match) probe
		- MM (mismatch) probe (補正に使う)
## ref(Affyprobe.png)

----

## [NCBI Gene Expression Omnibus (GEO)](http://www.ncbi.nlm.nih.gov/geo/) 
世界最大の遺伝子発現（[マイクロアレイ](http://ja.wikipedia.org/wiki/DNA%E3%83%9E%E3%82%A4%E3%82%AF%E3%83%AD%E3%82%A2%E3%83%AC%E3%82%A4)）データベース（レポジトリ）

### 【実習4】GEOを使って、自分の興味のある遺伝子の（ある実験条件下における）発現状況を調べる 
- [【統合TV】NCBI GEOの使い方2～遺伝子プロファイルの検索・処理済みデータの取得～ 2011](http://togotv.dbcls.jp/20111020.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
1. [http://www.ncbi.nlm.nih.gov/geo/](http://www.ncbi.nlm.nih.gov/geo/) を開きます。
1.「Gene profiles」に自分の検索したい遺伝子名を入力します。
1. 今回は例として「[nanog](http://www.google.co.jp/search?hl=ja&q=Nanog%E9%81%BA%E4%BC%9D%E5%AD%90)」という遺伝子を検索してみましょう。入力終了後、「GO」をクリックします。
1. GEOに登録されている様々な実験条件で行なわれたマイクロアレイ実験における「nanog」遺伝子の発現データが表示されます。
1. 検索結果の右端にある画像をクリックすると、[発現データの詳細をみる](http://www.ncbi.nlm.nih.gov/geo/tools/profileGraph.cgi?ID=GDS3262:220184_at)ことができます。
1. [このサンプル](http://www.ncbi.nlm.nih.gov/sites/GDSbrowser?acc=GDS3262)では、nanogはどういう細胞のどういう実験条件で発現が増減しているか調べてみましょう。
1. ページ下部の「samples」に列挙された[リンク](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM267499)をクリックすると、そのサンプル（一枚のマイクロアレイ）の詳細を閲覧できます。
1. [リンク先のページ](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM267499)の中ほどにある[「series」のリンク](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE10615)をクリックすると、この実験全体の詳細情報が見られます。
1. [この実験全体の詳細情報ページ](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE10615)の下部にある[「Series Matrix File(s)」](ftp://ftp.ncbi.nih.gov/pub/geo/DATA/SeriesMatrix/GSE10615/)をクリックすると、この実験の正規化補正済みのマイクロアレイデータをダウンロードすることができます。

### 【実習5】Dataset browserを利用して、GEOに登録されているマイクロアレイデータを解析する 
- [【統合TV】NCBI GEOの使い方3～データセットブラウザの使い方1～ 2012](http://togotv.dbcls.jp/20120128.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
- [【統合TV】NCBI GEOの使い方4～データセットブラウザの使い方2～ 2012](http://togotv.dbcls.jp/20120227.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
1. [http://www.ncbi.nlm.nih.gov/geo/](http://www.ncbi.nlm.nih.gov/geo/)を開きます。
1.「Gene profiles」に自分の検索したい遺伝子名を入力します。
1. 今回は例として「[nanog](http://www.google.co.jp/search?hl=ja&q=Nanog%E9%81%BA%E4%BC%9D%E5%AD%90)」という遺伝子を検索してみましょう。入力終了後、「GO」をクリックします。
1. GEOに登録されている様々な実験条件で行なわれたマイクロアレイ実験における「nanog」遺伝子の発現データが表示されます。
1. 検索結果の[アクセッション番号（今回は GDS3262）](http://www.ncbi.nlm.nih.gov/sites/GDSbrowser?acc=GDS3262)をクリックすると、解析用の「データセットブラウザ」が開きます。
1. 「[Expression profiles](http://www.ncbi.nlm.nih.gov/geoprofiles?term=GDS3262[ACCN)]」をクリックすると、[この実験データセットにおける個々の遺伝子発現状況を検索できるページ](http://www.ncbi.nlm.nih.gov/sites/entrez?db=geo&cmd=search&term=GDS2294[ACCN)に飛びます。
1. 検索窓に表示されているアクセッション番号の後に続けて遺伝子名を追加（今回は例として [Oct4](http://www.google.co.jp/search?q=Oct4) ）すると、この実験データセット内におけるその遺伝子の発現データが検索できます。
1. 「データセットブラウザ」の「[Data Analysis Tools](http://www.ncbi.nlm.nih.gov/sites/GDSbrowser?acc=GDS3262#details)」では詳細なデータ解析が可能です。
1. 「Find gene name or symbol:」のところに自分の興味ある遺伝子名を入れてみましょう。
- 10. 「Find genes that are up/down for this condition(s):」の「GO」をクリックするとどのような遺伝子がヒットするでしょうか。
- 11. 「Compare 2 sets of samples」では2群間で発現に差のある遺伝子を（統計学的に）検索できます。step1で発現量の違いを検出する方法を設定します。step.2で比較する2群の設定をします。step.3の「Query Group A vs. B」をクリックすると、検索が始まります。
- 12. 「Cluster heatmaps」では、マイクロアレイデータ解析でよく用いられる[ヒートマップ](http://images.google.co.jp/images?q=ヒートマップ)でのデータ表示が行なえます。分類方法としてHierarchical、Partitional (K-means/K-medians)、By location on chromosomeの3種類が選べますが、それぞれどのようにデータが分類されるか試してみましょう。
- 13. ヒートマップ上をクリックすると領域選択が開始されます。リサイズや移動で範囲を決定した後、Stack up をクリックすると選択した範囲が拡大されます。 
- 14. サンプルの内容とIDの対応は、元のページに戻って、Sample Subsets から確認できます。
- 15. さらに範囲選択して、Plot values をクリックすると、各遺伝子のサンプルごとの発現の様子がプロットで確認できます。 
- 16. 範囲選択して、View in Entrez をクリックすると、選択範囲内のデータを棒グラフで見られます。 
- 17. 範囲選択して、Download をクリックすると、選択範囲内のデータがテキスト形式でダウンロードできます。 
- 18.  「Experiment design and value distribution」では実験データにおける発現の分布を参照できます。これにより、各サンプルのデータが互いに比較可能か（実験上のミスがないか）チェックすることができます。

### 【実習6】GEOを使って、自分の興味のあるマイクロアレイ実験データセットを検索&生データをダウンロードする 
- [【統合TV】NCBI GEOの使い方1～マイクロアレイデータの検索・取得～ 2011](http://togotv.dbcls.jp/20110711.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
1. [http://www.ncbi.nlm.nih.gov/geo/](http://www.ncbi.nlm.nih.gov/geo/)を開きます。
1. 画面中央の「Platforms」をクリックします。
1. Platform(マイクロアレイの種類)の一覧画面が現れるので、上部の「FIND PLATFORM」をクリックします。
1. [platformの検索画面](http://www.ncbi.nlm.nih.gov/geo/query/browse.cgi?mode=findplatform)が現れるので、「Company name」に「Affymetrix」、「organism」に「Homo sapiens」を選択し、「FIND PLATFORM」をクリックします。
1. [Affymetrixのヒトのマイクロアレイの検索結果](http://www.ncbi.nlm.nih.gov/geo/query/browse.cgi?mode=foundplatform)が表示されるので、中程にある「Affymetrix GeneChip Human Genome U133 Plus 2.0 Array」の左端にある[「GPL570」というID](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GPL570)をクリックします。
1. [表示された画面](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GPL570)の真ん中あたりにある「series」下の「More...」をクリックすると、登録されているデータセットを閲覧できます。
1. ブラウザの検索ボタンなどを使って「reprogramming」という単語を検索するとどういうデータがヒットするでしょうか？
1. ヒットしたデータの左端にあるIDをクリックすると、[そのデータセットの詳細情報](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE9832)が閲覧できます
1. ページ下部の「Download family」の中にある「Series Matrix File(s)」をクリックすると正規化済みのデータのダウンロードリンクが表示されます。
- 10. ページ最下部の「Supplementary file」にあるリンクから生データをダウンロードすることができます。
- 11. 自分の研究テーマに近い、また興味のあるマイクロアレイデータが利用可能か検索してみましょう。

## [遺伝子発現バンク(GEO)目次、通称「GEO目次」](http://lifesciencedb.jp/geo/) 
- [使い方参考動画 遺伝子発現バンク(GEO)目次を使い倒す－その壱](http://togotv.dbcls.jp/20080623.html#p01) http://lifesciencedb.jp/image/small_video_icon.png
- NCBI GEO を日本語のインターフェイスで快適に使い、データの全容を俯瞰するための仕組みです。数多く登録されている遺伝子発現データの大まかな傾向をつかむのに役に立つことでしょう。
- 検索結果のRSS配信機能があるので、これを活用して、遺伝子発現データの新規登録の有無をチェックできる！

## [DAVID: The Database for Annotation, Visualization and Integrated Discovery](http://david.abcc.ncifcrf.gov/) 
&color(green){マイクロアレイデータの生物学的な解釈};

http://david.abcc.ncifcrf.gov/

- マイクロアレイ実験の一般的な目的は、実験条件によって得られたある遺伝子群の発現が生物学的にどういう意味を持つかを考えることです。
## ref(AJACS14/thecla/microarray.analysis.005.png)
- 今回は、その方法の一つとして、マイクロアレイの結果に[Gene Ontology](http://www.google.co.jp/url?sa=t&source=web&cd=4&ved=0CEEQFjAD&url=http%3A%2F%2Fja.wikipedia.org%2Fwiki%2F%25E9%2581%25BA%25E4%25BC%259D%25E5%25AD%2590%25E3%2582%25AA%25E3%2583%25B3%25E3%2583%2588%25E3%2583%25AD%25E3%2582%25B8%25E3%2583%25BC&ei=ve9QTd6XMtG6cbeW1KUH&usg=AFQjCNF8U-O4ktlMGoR9DNC0wKltmbjtmw)の用語を付与することで、生物学的な解釈を行います。
- [【統合TV】DAVIDを使ってマイクロアレイデータを解析する(※これも古いので近日中に番組アップデート予定)](http://togotv.dbcls.jp/20090925.html#p01) http://lifesciencedb.jp/image/small_video_icon.png

### マイクロアレイデータの準備 
サンプルデータとして、[NCBI GEO](http://www.ncbi.nlm.nih.gov/geo/)より取得した公共の遺伝子発現データを用います。このデータは、ある実験の前後の2群間で有意に発現減少した遺伝子群のリストです。
## ref(AJACS24/hono/110208_IDlist.txt,left)
（右クリックして「新しいタブで開く」もしくは「名前を付けてリンク先を保存」してください。）
&br;
このデータは、どのような実験から得られたデータなのか、どのように解釈できるのかをDAVIDを使って考察してみましょう！

### 【実習7】DAVIDを用いて、発現データの結果を生物学的に解釈する [#v732ec60]
1. 上部メニューの「Start Analysis」をクリックします。
1. 画面左側バーで、probe IDリストをコピペ or ファイルを指定します。
1. リストのIDの種類タイプを選択します。 … 今回は、「AFFYMETRIX_3PRIME_IVT_ID」と「Gene List」
1. Submit List をクリックするとリストが読み込まれます。
1. アップロードしたリストは、左側バーの「List Manager」で「Uploaded List_1」等として保存されています。削除やrenameもできます。
1. 解析を続けます。真ん中の「Functional Annotation Tool」をクリックします。
1. 「Gene Ontology」をクリックすると、Gene Ontologyを用いた解析の細かいメニューが表示されます。
1. 今回は、GOTERM_BP_FAT (BP=Biological Process)に注目します。その右の「Chart」をクリックすると結果がポップアップされます。
1. P-value を2回クリックしてp-valueが小さい（統計的に有意である）順にしてみましょう … p-value小さい順は、一度やればしばらく覚えているので、次からはしばらくは必要ないです
## fold(結果,#ref(AJACS24/hono/david_go_bp.png));
- [応用編] Pathways > KEGG_PATHWAY や Tissue Expression > UP_TISSUE なども見てみましょう。生物学的にどういうことが言えるでしょうか。
### fold(サンプルデータの答え,Arabidopsis thaliana (シロイヌナズナ)の植物細胞と細胞壁分解酵素を用いて取り除いた植物細胞（[プロトプラスト](http://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%83%88%E3%83%97%E3%83%A9%E3%82%B9%E3%83%88)）との比較（植物細胞の[脱分化](http://ja.wikipedia.org/wiki/%E3%82%AB%E3%83%AB%E3%82%B9_%28%E6%A4%8D%E7%89%A9%29)前・後）[GSE15515](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE15515));

----

## 【参考】遺伝子発現データベースに関する統合TV 
- [統合TVの「発現情報」タグをクリック！ ](http://togotv.dbcls.jp/?category=%C8%AF%B8%BD%BE%F0%CA%F3)
- [統合TV Curatedの発現制御解析から探す](http://togotv-curated.dbcls.jp/contents/category/expression#%E9%81%BA%E4%BC%9D%E5%AD%90%E3%83%BB%E3%82%BF%E3%83%B3%E3%83%91%E3%82%AF%E8%B3%AA%E7%99%BA%E7%8F%BE%E3%82%92%E7%B6%B2%E7%BE%85%E7%9A%84%E3%81%AB%E8%AA%BF%E3%81%B9%E3%81%9F%E3%81%84)
