# WEB サイト制作用 Vite テンプレート

## 仕様

### CSS に関する設定

#### Sass(SCSS)を使う

#### CSS ビルド時に PostCSS によるオプション設定を追加する

ベンダープレフィックスを付与したり様々なオプションを追加することが可能になる。
postcss.config.cjs で設定

#### autoprefixer の追加

autoprefixer はベンダープレフィックスを自動付与してくれる PostCSS のプラグイン

#### browserslist の設定

package.json に対象となるブラウザ範囲「browserslist」を追記

```
{
  〜省略〜
  "devDependencies": {
   〜省略〜
  },
  "browserslist": [
    "last 3 versions",
    "> 5%",
    "Firefox ESR",
    "not dead"
  ]
}
```

#### autoprefixer を有効化する

postcss.config.cjs に追記

```
module.exports = {
  plugins: {
    autoprefixer: {},
  },
}
```

#### postcss-sort-media-queries

メディアクエリをソートして 1 つにまとめてくれる PostCSS のプラグイン

```
module.exports = {
  plugins: {
    autoprefixer: {},
    'postcss-sort-media-queries': {},
  },
}
```

#### css-declaration-sorter

CSS プロパティの順番をソートする PostCSS のプラグイン

```
module.exports = {
  plugins: {
    autoprefixer: {},
    'postcss-sort-media-queries': {},
    'css-declaration-sorter':{order:'smacss'},
  },
}
```

### HTML に関する設定

#### HTML を複数出力する設定

vite.config.js に./src 配下にある html ファイル一式を取得し自動出力する記述を vite.config.js にて設定。

#### HTML ファイルを ejs のように扱う（ハンドルバー化する）

vite-plugin-handlebars を導入し、HTML を ejs のように扱うことができる。
各ページで利用するコンポーネントファイル用のディレクトリを「components」とし、src 内に作成。
例として heaer.html を置く。
vite-plugin-handlebars を読み込む設定を vite.config に追記。

設定以外にも以下のリファレンスから参照可能
https://handlebarsjs.com/guide/

### 変換しないファイルを格納する public/ディレクトリの設定

「npm run build」時に変換対象にしたくないファイル（そのまま使いたいファイル）は、メインの HTML ファイルと同じ階層に public/ ディレクトリを作成しそこへ内包する。

publicのファイルを参照する時はpublicを除いてパスを記述する

```
<img src="./assets/images/hoge.jpg" alt="">
<script src="./assets/js/fuga.js"></script>
```
