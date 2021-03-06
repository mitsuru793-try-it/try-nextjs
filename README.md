TODO
* [ ] https://nextjs.org/learn/basics/data-fetching
* [ ] hydrationという処理
* [ ] TTFB
* [ ] SWR(React hook)
* [ ] dangerouslySetInnerHTML
* [ ] Preview Mode
* [ ] Jamstack
* [ ] Serverless Functions

This is a starter template for [Learn Next.js](https://nextjs.org/learn).

```shell
npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"
```

[インタラクティブな公式チュートリアル](https://nextjs.org/learn/basics/create-nextjs-app)


## Setup

```
yarn install
npm run dev
```

open http://localhost:3000/

## Production

```
yarn build
# .nextが生成される
```

## Vercel

* 前会社 ZEIT
* Github Apps「Vercel」をリポジトリにインストール
  * organizationにVercelをインストールする時は、パーソナルアカウントが選択肢に表示されるが使えない。Vercelにteamを作る必要がある。

Githubにpushするとステージングに自動デプロイされて、PRにコメントされる。
* https://vercel.com/mitsuru793-try-it/try-nextjs/kpr9uwgx7
* PRをマージすると、Vercelのpreviewからそのブランチが自動で消える。

## Note

### pages
* default exportが必須
* \<Link>でクライアントサイドにJSでナビゲーションさせることによって、クライアントサイドのナビゲーションより速くなる。
  * HTTPリクエストが発生しないため
  * bodyのcss backgroundを変更してトランジションしても、維持される。
* \<Link>はnextjsのbuiltin。ルーティングライブラリは不要。
  * [Routing: Introduction \| Next\.js](https://nextjs.org/docs/routing/introduction)
  * [next/link \| Next\.js](https://nextjs.org/docs/api-reference/next/link)
  
### CSS

[vercel/styled\-jsx: Full CSS support for JSX without compromises](https://github.com/vercel/styled-jsx)

```html
<style jsx>{`
  …
`}</style>
```

* CSS Moduleを使うとクラス名がユニークで生成されるので、衝突がない。
  * `<div className={styles.container}>{children}</div>`
* `pages/_app.js`にしかglobal cssを書けない理由は、a -> bへナビゲーションした時、aのCSSがbにも適用されないようにするため。
* Next.js compiles CSS using PostCSS.
* you can create a top-level file called postcss.config.js.
  
### data fetching

* nextjsは静的生成とサーバサイドレンダリングどちらも可能。ページごとに選べる。
* 最初に1回DBやFile Systemからfetchする場合は、データ付きで静的生成が可能。
* getStaticPropsは開発時はリクエストごと走る。
  * page/でexport functionする。Reactがレンダリングの前にデータを知る必要があるため。
* getServerSideProps

Dynamic Routing

Pageは次を含む。
* React component
* getStaticPaths()
  * パスパラメータを返す。\[id].jsならidを返す
* getStaticProps({ params })
  * idのdataを返す

### 登場したライブラリ

* date-fns 
* gray-matter
* remark
* remark-html
* tailwindcss

### Etc
* \<html lang>を修正する時は\<Head>ではなく、\<Document>を使う。
* pages/_app.jsを追加した後はサーバーを再起動
* chrome developer consoleでcmd + shift + pでアクションパレットが開く。
* The DPS Workflow: Develop, Preview, and Ship.

 