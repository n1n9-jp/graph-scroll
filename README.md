# graph-scroll.js

[d3](https://github.com/mbostock/d3) グラフのシンプルなスクロール イベント。[stack](https://github.com/mbostock/stack.git) に基づいています。

### [Demo/Documentation](http://1wheel.github.io/graph-scroll/)

*graph-scroll* は、説明テキスト セクションの選択を受け取り、異なるセクションがスクロールされて表示されると `active` イベントを送信します。これらの `active` イベントは、チャートの状態を更新するために使用できます。

```
d3.graphScroll()
    .sections(d3.selectAll('#sections > div'))
    .on('active', function(i){ console.log(i + 'th section active') })
```

完全にスクロールされて表示される一番上の要素は、`graph-scroll-active` クラスに分類されます。これにより、CSS を使用してアクティブなセクションを簡単に強調表示できます:

```
#sections > div{
	opacity: .3
} 

#sections div.graph-scroll-active{
	opacity: 1;
}
```

ヘッダーと紹介画像/テキストをサポートするために、説明テキストとグラフを含むコンテナ要素を使用します。

```
<h1>Page Title</div>
<div id='container'>
  <div id='graph'></div>
  <div id='sections'>
    <div>Section 0</div>
    <div>Section 1</div>
    <div>Section 2</div>
  </div>
</div>
<h1>Footer</h1>
```

これらの要素が `container` と `graph` による選択として graphScroll に渡された場合、コンテナーの上部が表示範囲外にある場合、グラフ選択内のすべての要素は `graph-scroll-graph` に分類されます。

```
d3.graphScroll()
	.graph(d3.selectAll('#graph'))
	.container(d3.select('#container'))
  .sections(d3.selectAll('#sections > div'))
  .on('active', function(i){ console.log(i + 'th section active') })

```

グラフがスクロールして表示されなくなると、`p​​osition: sticky` により、テキストがスクロールする間、グラフ要素がページの上部に固定されたままになります。

```
#container{
  position: relative;
}

#sections{
  width: 340px;
}

#graph{
  margin-left: 40px;
  width: 500px;
  position: sticky;
  top: 0px;
  float: right;
}
```


モバイルでは、グラフとセクションを中央に配置し、最初のスライドにいくらかのパディングを追加するのが良いオプションです。

```
@media (max-width: 925px)  {
  #graph{
    width: 100%;
    margin-left: 0px;
    float: none;
  }

  #sections{
    position: relative;
    margin: 0px auto;
    padding-top: 400px;
  }
}
```

新しいセクションがトリガーされる前のピクセル数を調整することも、モバイルでは役立ちます (デフォルトは 200 ピクセル)。

```
graphScroll.offset(300)
```

graphScroll インスタンスを更新または置換するには、文字列を `eventId` に渡して古いイベントリスナーを削除します。

```
graphScroll.eventId('uniqueId1')
```
