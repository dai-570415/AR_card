# A-frameでAR名刺を作ろう
実現を最優先にした記事構成にしています。
細かい内容は参考記事から参照してください。

## A-Frameとは
Web上でVR・ARが実現できるJavascriptのライブラリ。
HTMLベースで書けるため、比較的気軽に扱えて便利。

### 読み込み

```html
<head>
    <!-- A-Frame本体 -->
    <script src="https://aframe.io/releases/0.8.2/aframe.min.js"></script>
    <!-- AR.js -->
    <script src="https://cdn.rawgit.com/jeromeetienne/AR.js/1.6.2/aframe/build/aframe-ar.js"></script>
    <!-- A-Frame内でリンクをつけるのに必要 -->
    <script src="https://rawgit.com/gasolin/aframe-href-component/master/dist/aframe-href-component.min.js"></script>
</head>
```

# 3D空間にする
- a-scene: body直下に`<a-scene>`タグでくくる
- a-marker: マーカー指定のタグ
デフォルトで良い場合はこちらのタグにする`<a-marker preset="hiro">`
カスタムマーカー作り方は下記に記載
- a-entity: エンティティー要素

```html
<a-scene embedded arjs="debugUIEnabled:false;">
    <a-marker type='pattern' url='./marker/pattern-profile.patt'>
        <a-entity
            link="href: https://dais-official-site.web.app/; title: Official Site;"
            position="0 .5 0"
        ></a-entity>
    </a-marker>
</a-scene>
```

[カスタムマーカージェネレーター](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)

#### カスタムマーカージェネレーターHow To Use
1. UPROADボタンから好きな画像アップ
2. DOWNROAD IMAGEからマーカー画像をダウンロードしておく（アプリでかざす対象になります）
3. DOWNROAD MARKERでダウンロードしたファイル名で指定する
`url='./marker/<fileName>.patt'`
※url指定しているのでローカルにデータを置く必要はありません。

### カメラ指定

```html
<a-entity camera look-controls wasd-controls>
    <a-entity cursor="fuse: true;"
    position="0 0 -1"
    geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
    material="color: blue; shader: flat">
    <a-animation begin="click" easing="ease-in" attribute="scale" dur="150"
        fill="forwards" from="0.1 0.1 0.1" to="1 1 1"></a-animation>
    <a-animation begin="cursor-fusing" easing="ease-in" attribute="scale" dur="1500"
        fill="backwards" from="1 1 1" to="0.1 0.1 0.1"></a-animation>
    </a-entity>
</a-entity>
```

### 全体

```html
<!DOCTYPE html>
<head>
  <script src="https://aframe.io/releases/0.8.2/aframe.min.js"></script>
  <script src="https://cdn.rawgit.com/jeromeetienne/AR.js/1.6.2/aframe/build/aframe-ar.js"></script>
  <script src="https://rawgit.com/gasolin/aframe-href-component/master/dist/aframe-href-component.min.js"></script>
</head>
<body style='margin: 0; overflow: hidden;'>

  <a-scene embedded arjs="debugUIEnabled:false;">
    <a-marker type='pattern' url='./marker/pattern-profile.patt'>
      <a-entity
        link="href: https://dais-official-site.web.app/; title: Official Site;"
        position="0 .5 0"
      ></a-entity>
    </a-marker>

    <a-marker type='pattern' url='./marker/pattern-tw.patt'>
      <a-entity
        link="href: https://twitter.com/dai_designing; title: Twitter;"
        position="0 .5 0"
      ></a-entity>
    </a-marker>

    <a-marker type='pattern' url='./marker/pattern-fb.patt'>
      <a-entity
        link="href: https://www.facebook.com/daisuke.mori.374; title: Facebook;"
        position="0 .5 0"
      ></a-entity>
    </a-marker>

    <a-marker type='pattern' url='./marker/pattern-qiita.patt'>
      <a-entity
        link="href: https://qiita.com/dai_designing; title: Qiita;"
        position="0 .5 0"
      ></a-entity>
    </a-marker>

    <a-marker type='pattern' url='./marker/pattern-git.patt'>
      <a-entity
        link="href: https://github.com/dai-570415; title: Git Hub;"
        position="0 .5 0"
      ></a-entity>
    </a-marker>

    <a-entity camera look-controls wasd-controls>
      <a-entity cursor="fuse: true;"
        position="0 0 -1"
        geometry="primitive: ring; radiusInner: 0.02; radiusOuter: 0.03"
        material="color: blue; shader: flat">
        <a-animation begin="click" easing="ease-in" attribute="scale" dur="150"
            fill="forwards" from="0.1 0.1 0.1" to="1 1 1"></a-animation>
        <a-animation begin="cursor-fusing" easing="ease-in" attribute="scale" dur="1500"
            fill="backwards" from="1 1 1" to="0.1 0.1 0.1"></a-animation>
      </a-entity>
    </a-entity>

    <p>更新2020.10.7 18:20</p>
  </a-scene>

</body>
</html>
```

ここまでできたらGithub PagesやFirebaseなどでデプロイすると動くのでやってみてください。

### 参考
- [A-Frame公式](https://aframe.io/)
- [ブラウザで動くAR名刺を作った（執筆中）](https://qiita.com/Khmer495/items/1b7a2855347187dd0880)
- [【A-Frame】a-linkでVRページ間を移動する](https://keeponrockin.hatenablog.com/entry/2018/12/26/102726)
- [「AR.js」でオリジナルのマーカーを設定する方法](https://liginc.co.jp/457071)
- [AR.js Marker Training](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html)