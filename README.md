# tex_docker_alpine
devcontainer for texlive
[tex_docker](https://github.com/momijiyuki/tex_docker)をベースにAlpine Linuxに変更

## 使用したコレクション

- `a, b, c, f, g, m, x, D, F, J, K`
  - 必須プログラムとファイル
  - BibTeXの追加スタイル
    - ref.bibが使えるようになる
  - TeX外部プログラム
    - latexmk
  - 推奨フォント
  - 画像およびフォントのユーティリティ
  - 日中韓(base)
  - 日本語
  - LaTeX基本パッケージ
  - LaTeX推奨パッケージ
  - 画像と図表
  - Plain(La)TeXパッケージ
- ドキュメントとソースツリーの除外

## 参考元

- [TEX Live ガイド 2023](https://www.tug.org/texlive/doc/texlive-ja/texlive-ja.pdf)
- [インストーラプロファイルを用いてTeX Liveをインストールしよう](https://qiita.com/munepi/items/f2eaa30f0cd00a9a68f8)
- [TeX Live ドキュメント #PROFILES](https://tug.org/texlive/doc/install-tl.html#PROFILES)
- [VSCode で最高の LaTeX 環境を作る](https://qiita.com/rainbartown/items/d7718f12d71e688f3573)
  - `settings.json`や`.latexmkrc`を参考
- [Tex Liveのクソデカ容量を削減したい！](https://blog.loliver.net/archive/texlive_minimal_install/)
  - コレクションの選定の参考に
- [texliveの最強環境を作ったよ](https://zenn.dev/tbistr/articles/texlive-devcontainer-repost)
  - `Dockerfileの記法等を参考

<!-- [LaTeXで作るA0poster](http://www.math.kobe-u.ac.jp/a0poster/) -->
