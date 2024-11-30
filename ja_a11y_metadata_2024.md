---
title: アクセシブルなEPUBの日本語関連メタ情報のガイドライン version 0.2
author: 日本デイジーコンソーシアム 技術委員会
date: 2024年11月30日
paper: a4
---

# ■ 1 はじめに

EPUBに適切なアクセシビリティ関連のメタ情報が付与されていると、障害者は自分の読書方法に適合するEPUB書籍を見つけられるようになります。アクセシブルなEPUBを規定するEPUB アクセシビリティ 1.0（JIS X 23761:2022、ISO/IEC 23761:2021）あるいはEPUB アクセシビリティ 1.1では適切なメタ情報の付与が必須です。

この文書はアクセシブルなEPUBの日本語関連のメタ情報を中心に2024年時点の現状を整理したもので、日本語関連のメタ情報を付与する際に参考となるガイドラインです。

現在、日本語に関するメタ情報としては以下の要素があります。

- ルビ
- 分かち書き
- 縦組・横組表示

いずれもAccessibilityFeatureというメタ情報に対象となるEPUBでの対応状況を記載します。

詳細な仕様は、次の文書に記載されています。

・[https://www.w3.org/community/reports/a11y-discov-vocab/CG-FINAL-vocabulary-20240906/ : Schema.org Accessibility Properties for Discoverability Vocabulary, W3C Final Community Group Report 06 September 2024](https://www.w3.org/community/reports/a11y-discov-vocab/CG-FINAL-vocabulary-20240906/)

# ■ 2 ルビに関するメタ情報

ルビが無いと読書が困難な場合、あるいは逆にルビがあると親文字と混同して読みにくいなど、ルビの表示に関する要望は障害に応じ様々です。

ルビについては次のメタ情報で表現します。

- rubyAnnotations
- fullRubyAnnotations

## ◆ 2.1 rubyAnnotations

rubyAnnotationsは、本文中の一部の読みが難しい語についてのみルビが振られている状況（以下、パラルビ）を示します。

例2.1-1
```{.html}
<meta property="schema:accessibilityFeature">rubyAnnotations</meta>
```

## ◆ 2.2 fullRubyAnnotations

fullRubyAnnotationsは、本文中に総ルビでルビが付与されていることを示します。

例2.2-1
```{.html}
<meta property="schema:accessibilityFeature">fullRubyAnnotations</meta>
```

## ◆ 2.3 パラルビ、総ルビの表示の切り替えが行えるEPUBの場合

リーディングシステムの設定によって、パラルビ、総ルビの表示の切り替えが行えるEPUBの場合には、次の例のように前述の両方のメタ情報を付与します。

例2.3-1
```{.html}
<meta property="schema:accessibilityFeature">rubyAnnotations</meta>
<meta property="schema:accessibilityFeature">fullRubyAnnotations</meta>
```

メタ情報とは直接関係ありませんが、今のところ、本文のXHTMLでどのようにパラルビと総ルビを区別して表現するかについての規約は存在しません。XHTMLの中でどのようにパラルビと総ルビを区別するかは今後の課題です。（デイジー教科書では独自ルールを用いてパラルビと総ルビを区別して製作しています。）

## ◆ 2.4 ルビに関するメタ情報が無い場合

前述のrubyAnnotations、fullRubyAnnotationsのどちらのメタ情報も付与されていない場合には、ルビに関する情報は不明という扱いになります。不明には、ルビ情報が無い状態も含みます。

ルビがあると読みにくい読者にとっては、ルビ無しの表示を示すメタ情報があると良いのですが、現状ではこのためのメタ情報は定義されていせん。ルビが無しの表示が可能であることを示すメタ情報は今後の課題です。

## ◆ 2.5 底本通りのルビ

底本（あるいは原本）通りのルビ表示が可能であることを示すメタ情報は存在しません。

# ■ 3 分かち書きに関するメタ情報

分かち書きの有無について次のメタ情報で表現します。

- withAdditionalWordSegmentation
- withoutAdditionalWordSegmentation

## ◆ 3.1 withAdditionalWordSegmentation

withAdditionalWordSegmentationは、分かち書き有りの表示に対応していることを示します。

例3.1-1
```{.html}
<meta property="schema:accessibilityFeature">withAdditionalWordSegmentation</meta>
```

次の2つのどちらかの方法で分かち書きを表現している場合等に、このメタ情報を設定します。

- XHTMLの本文中で空白文字を用いて分かち書き部分を表現している場合
- &lt;wbr&gt;のタグを用いて分かち書き部分を表現している場合

空白文字を用いて分かち書き部分を表現している場合は、リーディングシステムで分かち書きを表示しないように表示できませんが、&lt;wbr&gt;を用いて分かち書きが表現されている場合にはリーディングシステムによっては表示設定で、分かち書き表示を行う・行わないを切り替えられます。

## ◆ 3.2 withoutAdditionalWordSegmentation

withoutAdditionalWordSegmentationは、分かち書き無しの表示に対応していることを示します。

例3.2-1
```{.html}
<meta property="schema:accessibilityFeature">withoutAdditionalWordSegmentation</meta>
```

次のどちらかの方法を用いて分かち書き無しの状態が表現されている場合に用います。

- 本文上に分かち書き情報がまったく無い場合
- &lt;wbr&gt;のタグを用いて分かち書き部分を表現している場合

&lt;wbr&gt;のタグを用いて分かち書き部分を表現している場合には、リーディングシステムによっては分かち書きを表示しない設定にできるため、こちらのメタ情報も設定します。

# ■ 4 縦組・横組表示に関するメタ情報

縦組だと読みにくい、あるいは横組だと読みにくいという方がいます。
対象のEPUBが縦組表示が行えるか、あるいは横組表示を行えるかについて次のメタ情報で表現します。

- verticalWriting
- horizontalWriting

## ◆ 4.1 verticalWriting

verticalWritingは、縦組による表示に対応していることを示します。

例4.1-1
```{.html}
<meta property="schema:accessibilityFeature">verticalWriting</meta>
```

## ◆ 4.2 horizontalWriting

horizontalWritingは、横組による表示に対応していることを示します。

例4.2-1
```{.html}
<meta property="schema:accessibilityFeature">horizontalWriting</meta>
```

## ◆ 4.3 縦組・横組の両方の表示に対応している場合

縦組・横組の両方の表示に対応している場合には、次の例のように前述の両方のメタ情報を付与します。

例4.3-1
```{.html}
<meta property="schema:accessibilityFeature">verticalWriting</meta>
<meta property="schema:accessibilityFeature">horizontalWriting</meta>
```

縦組・横組の表示切り替え機能を持つリーディングシステムは、この二つのメタ情報を元に縦組・横組の表示切り替え機能を有効にできます。

縦組・横組の両方に対応するには、縦組用のCSSと横組用のCSSの両方EPUBに組み込まれている必要があります。組み込み方法については次の文書「Alternate Style Tags 1.1」を参照してください。

・[https://www.w3.org/submissions/altss-tags/ : Alternate Style Tags 1.1, W3C Member Submission 25 January 2017](https://www.w3.org/submissions/altss-tags/)

・[https://imagedrive.github.io/Submission/altss-tags/ : Alternate Style Tags 1.1, W3C Member Submission 2017年1月25日（日本語訳）](https://imagedrive.github.io/Submission/altss-tags/)

上記の「Alternate Style Tags 1.1」ではどちらを優先するかをXHTMLのレベルで規定しています。縦組と横組の両方に対応している場合、メタデータではどちらを優先的にデフォルト表示するかは規定されていませんが、メタ情報の記述順番はこの「Alternate Style Tags 1.1」で示される順番に合わせ、優先する方を先に記載してください。

EPUBではページのめくり方向が規定されています。縦組・横組の両方に対応しているEPUBについて、どのようにめくり方向を適用するかについての仕様はありません。

# ■ 5 accessibilitySummary

定型的な枠組みでは表現できないアクセシビリティ対応や特別な注意喚起が必要な場合には、accessibilitySummaryに、このような情報を人間が理解できるテキストの表現で記載します。

対象のEPUBにおいて、ルビ、分かち書き、縦組・横組表示に関して上記のメタデータでは表現できないような特殊対応を行っている場合には、その内容をaccessibilitySummaryのメタデータに記載すると良いでしょう。

例5-1：
```{.html}
<meta property="schema:accessibilitySummary">
本文中の分かち書き部分は｜の記号を用いています。
</meta>
```

例5-2：
```{.html}
<meta property="schema:accessibilitySummary">
本文中のルビはローマ字で表現されています。
</meta>
```

# ■ 6 リーディングシステムへの要求事項

上記のようなメタ情報が付与されたEPUBについて、次のような機能が提供されることがリーディングシステムに対して期待されます。

・メタ情報の読者への提示機能：
リーディングシステムの内部で、上記のようなメタ情報についてなんらかの方法で、読者に提示する機能が期待されます。

・ルビの表示切り替え機能：
パラルビ、総ルビの両方のメタ情報が付与されたEPUBの場合、ルビの表示をパラルビ、総ルビで切り替える機能が期待されます。

・分かち書き表示の切り替え機能：
分かち書きの有りと、分かち書き無しの両方のメタ情報が付与されたEPUBの場合、分かち書き表示を切り替え機能機能が期待されます。

・縦組と横組の切り替え機能：
縦組・横組の両方の表示に対応しているEPUBの場合、縦組と横組の表示を切り替える機能が期待されます。

