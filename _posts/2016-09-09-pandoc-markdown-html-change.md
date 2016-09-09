---
layout: post
title: pandocでMarkdown形式をHTMLに一発変換
---

## pandocって？

> Pandocは Haskell で書かれたライブラリおよびコマンドラインツールであり、 あるマークアップ形式で書かれた文書を別の形式へ変換するものです。
[Pandoc ユーザーズガイド 日本語版](http://sky-y.github.io/site-pandoc-jp/users-guide/)

## 対応書式

対応している入力形式は以下の通りです：

- markdown
- Textile （のサブセット、以下同様）
- reStructuredText
- HTML
- LaTeX
- MediaWiki markup
- Haddock markup
- OPML
- Emacs Org-mode
- DocBook

出力形式は以下の通りです：

- プレーンテキスト
- markdown
- reStructuredText
- XHTML
- HTML 5
- LaTeX （beamerスライドショーを含む）
- ConTeXt
- RTF
- OPML
- DocBook
- OpenDocument
- ODT
- Word docx
- GNU Texinfo
- MediaWiki markup
- EPUB (v2またはv3)
- FictionBook2
- Textile
- groff manページ
- Emacs Org-Mode
- AsciiDoc
- InDesign ICML
- HTMLスライドショー：Slidy、Slideous、DZSlides、reveal.js、S5
- PDF出力（LaTeXがインストールされているシステムで使用できます）

## pandocのインストール

### Mac
`brew install pandoc`

### Linux

#### Yum
`sudo yum install pandoc`

#### apt-get
`sudo apt-get install pandoc`

## pandocの使い方

### CSSを指定してMarkdownからHTMLを生成する
`pandoc -c style.css input.md -o output.html`
