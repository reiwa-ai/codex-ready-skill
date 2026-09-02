# codex-ready

日本語 / English

## 概要

`codex-ready` は、既存のソフトウェアリポジトリを AI コーディングエージェントで安全かつ継続的に編集しやすい状態へ整えるためのスキルです。

このスキルは、実装作業をすぐ始めることよりも先に、リポジトリの分類、ドキュメント整備、編集方針の明文化、テスト導線の整備を行うことを重視します。

主な成果物は以下です。

- `README.md`: 人間向けの概要、構成、セットアップ、主要ワークフロー
- `KNOWLEDGE.md`: エージェント向けの注意点、落とし穴、局所ルール
- `KNOWN_BUGS.md`: 調査中に見つけた問題の記録
- `AGENT.md`: そのリポジトリ専用の編集指示
- `.codex-ready/project-types/*.md`: 類型ごとの詳細指示
- 単体確認用の軽量テスト導線と、E2E テストの骨組みまたは方針

## Overview

`codex-ready` is a skill for preparing an existing software repository so AI coding agents can work on it more safely, consistently, and repeatedly.

Instead of jumping straight into implementation, the skill focuses on repository classification, documentation, editing rules, and test entrypoints first.

Its typical outputs are:

- `README.md`: human-facing overview, architecture, setup, and workflows
- `KNOWLEDGE.md`: agent-facing gotchas, invariants, and local rules
- `KNOWN_BUGS.md`: a log of issues found during inspection or testing
- `AGENT.md`: repository-specific instructions for future agents
- `.codex-ready/project-types/*.md`: type-specific guidance files
- lightweight unit-test entrypoints plus an end-to-end test skeleton or plan

## 何をするスキルか

このスキルは、対象リポジトリを一つの固定ラベルで扱いません。言語、フレームワーク、実行形態、運用面を見て、複数の類型にまたがって分類します。

たとえば次のような組み合わせを前提にできます。

- Python API サービス
- Node.js / TypeScript バックエンド
- React / Next.js / Vue 系フロントエンド
- CLI ツール
- モノレポ
- データ処理、ML、ノートブック、インフラ構成
- モバイル / デスクトップアプリ

その上で、将来のエージェントが編集前に読むべき repository-local な指示ファイルを生成する設計です。

## What The Skill Does

This skill does not force a repository into a single label. It classifies the project across multiple axes such as language, framework, runtime surface, and operational concerns.

Examples include:

- Python API services
- Node.js or TypeScript backends
- React, Next.js, or Vue frontends
- CLI tools
- monorepos
- data, ML, notebook, or infrastructure repositories
- mobile or desktop applications

It then turns those findings into repository-local guidance files that future agents are expected to read before editing.

## 設計方針

- 既存コードを尊重し、最小変更を基本にする
- 意図が曖昧なら推測で進めず、ユーザー確認を優先する
- バグを見つけたら、すぐ直す前に `KNOWN_BUGS.md` に記録する
- 人間向け文書とエージェント向け文書を分離する
- 単体テストと E2E テストを別責務として扱う
- 類型ごとの注意点は一枚の巨大な文書に押し込めず、分割した Markdown で管理する

## Design Principles

- respect existing code and prefer minimal edits
- ask the user when intent is unclear instead of guessing
- log discovered bugs in `KNOWN_BUGS.md` before attempting fixes
- separate human-facing documentation from agent-facing documentation
- treat unit tests and end-to-end tests as separate responsibilities
- keep type-specific guidance in focused Markdown files instead of one oversized instruction file

## リポジトリ構成

このリポジトリには、スキル本体と詳細リファレンスが含まれます。

```text
.
|-- SKILL.md
|-- README.md
`-- references/
    |-- baseline-workflow.md
    |-- project-taxonomy.md
    |-- ecosystem-python.md
    |-- ecosystem-js-ts.md
    |-- ecosystem-go-rust-java-dotnet.md
    |-- ecosystem-c-cpp-ruby-php.md
    |-- surface-web-ui.md
    |-- surface-mobile-desktop.md
    `-- surface-data-ml-infra.md
```

- `SKILL.md` はスキルのエントリポイントです。
- `references/` には、必要なときだけ読む詳細ガイドを置いています。

## Repository Layout

This repository contains the skill entrypoint and a set of focused reference documents.

```text
.
|-- SKILL.md
|-- README.md
`-- references/
    |-- baseline-workflow.md
    |-- project-taxonomy.md
    |-- ecosystem-python.md
    |-- ecosystem-js-ts.md
    |-- ecosystem-go-rust-java-dotnet.md
    |-- ecosystem-c-cpp-ruby-php.md
    |-- surface-web-ui.md
    |-- surface-mobile-desktop.md
    `-- surface-data-ml-infra.md
```

- `SKILL.md` is the skill entrypoint.
- `references/` contains detailed guides that are loaded only when relevant.

## 使い方

1. このリポジトリをスキルとして利用できる場所に配置するか、スキルファイルとしてアップロードします。
2. 対象の既存リポジトリに対して、このスキルを使って準備作業を依頼します。
3. スキルはまずリポジトリを調査し、適用すべき類型を抽出します。
4. その結果をもとに、`AGENT.md`、`KNOWLEDGE.md`、`KNOWN_BUGS.md`、類型別 Markdown、テスト導線を整備します。
5. 将来の編集では、生成された `AGENT.md` と類型別 Markdown を先に読む運用を想定します。

## How To Use

1. Place this repository where your skill runner can access it, or upload it as a skill package.
2. Use the skill on an existing repository that needs preparation for agent-driven editing.
3. The skill first inspects the repository and determines all applicable project types.
4. Based on that classification, it prepares `AGENT.md`, `KNOWLEDGE.md`, `KNOWN_BUGS.md`, project-type Markdown files, and test entrypoints.
5. Future editing sessions are expected to read the generated `AGENT.md` and project-type files before making changes.

## このスキルが重視する点

- リポジトリを `git` 管理下に置いて差分を追いやすくすること
- ドキュメントを厚くして、後続エージェントの探索コストを減らすこと
- 既存テストが無い場合でも、まずはモックや骨組みから E2E 導線を作ること
- Python では `__name__ == "__main__"` を使うような軽量な単体確認導線も検討すること
- 類型ごとの注意点を repository-local に保持し、再利用できる形にすること

## What This Skill Emphasizes

- putting the repository under `git` when needed so changes are traceable
- improving documentation to reduce rediscovery cost for later agents
- creating end-to-end test scaffolding even when a full suite does not exist yet
- adding lightweight function-level execution paths when the stack benefits from them
- keeping project-type guidance local to the prepared repository so it can be reused across later edits

## 対象外

このスキルは、特定フレームワーク専用の実装生成スキルではありません。準備と整備が主目的です。

次のような用途は主目的ではありません。

- 単発のバグ修正だけをすぐ行うこと
- 大規模リファクタリングを自動で進めること
- 既存コードの意図を未確認のまま書き換えること
- リポジトリ固有事情を無視して汎用テンプレートを押し付けること

## Non-Goals

This is not a framework-specific implementation generator. Its primary purpose is preparation and repository hardening for future agent work.

It is not mainly intended for:

- immediate one-off bug fixing
- automatic large-scale refactors
- rewriting existing code without clarified intent
- forcing a generic template onto repository-specific workflows

## 公開メモ

このリポジトリは Markdown 中心のスキルプロジェクトとして構成されています。改善提案は、`SKILL.md` の過不足、類型の網羅性、`references/` の粒度、将来の `AGENT.md` 生成品質という観点で歓迎します。

## Notes For Contributors

This repository is intentionally Markdown-heavy because the main deliverable is the skill itself. Useful contributions usually improve one of these areas: the scope of `SKILL.md`, the quality of the project taxonomy, the precision of the reference files, or the reliability of the generated repository guidance.
