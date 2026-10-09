---
name: character-kajael-generator
description: Kajaelのプロフィールとアシュランドでの行動パターンに基づき、時間・場所・服装を決定し、Higgsfield MCPを呼び出して画像・動画を生成します。
metadata:
  openclaw:
    allowedTools:
      - "mcp__higgsfield__generate_image"
      - "mcp__higgsfield__generate_video"
---

# Kajael (カジャエル) 画像・動画生成スキル (外部MCP連携版)

オレゴン州アシュランド在住のシンガーソングライター Kajael の日常と音楽活動のワンシーンを定義し、Higgsfield MCP ツールを直接呼び出して高品質な画像および動画プロンプトを自動生成・レンダリングします。

## 実行ワークフロー

### Step 1: コンテキストと条件の整理
1. `{baseDir}/references/kajael_profile.md`,`{baseDir}/references/kajael_ashland_life reserch.md`を読み込みます。
2. ユーザー指示から「指定時間（または時間帯）」「場所」「服装」を抽出します。具体的な指示が無い場合は読み込んだファイルを元に、「場所」「時間」「行動」「服装」を高精度に生成します。
3. **時間帯未指定時の自動指定（決定木）**:
   - **08:00 - 09:30（朝の準備）**: 自宅アパート。オーガニック朝食。服装: オーバーサイズパーカーまたは部屋着。
   - **10:00 - 12:30（作詞・人間観察）**: Noble Coffee Roasting（Railroad District）。窓辺でコーヒーとノート。服装: 白のオーバーサイズシャツ、カーディガン、デニム。
   - **13:00 - 14:30（ストリートライブ）**: Lithia Park（Butler-Perozzi Fountain近く）。TaylorアコースティックギターとEVポータブルPA。服装: リラックスフィットデニム、スニーカー。
   - **15:00 - 16:30（散策・リフレッシュ）**: Bloomsbury Books または Oredson-Todd Woods の森林トレイル。
   - **17:30 - 20:30（ホームレコーディング）**: 自宅スタジオ。マイク（Neumann TLM 103）とApollo Twin Xに向かって歌唱・ラップ録音。
   - **21:00 - 23:00（夜の交流）**: Oberon's または Local 31。仲間とのリラックスした打ち合わせ。

### Step 2: Higgsfield (SOUL ID) 用英文プロンプトの構築ルール
プロンプトはすべて**英語**で組み立てます。

1. **SOUL ID識別子**: `[SOUL_ID: soul_kajael_v1_ashland]`
2. **人物特徴**: `24-year-old female singer-songwriter, slender build (163cm, 54kg), dark brown semi-long hair with natural soft waves, gentle and shy expression, natural minimal makeup`
3. **場面・行動・小道具**: 指定時間帯に応じた具体的な行動（例: `writing lyrics in a worn notebook with a mug of coffee by the window`, `playing acoustic guitar on a wooden bench under sycamore trees`）
4. **服装・スタイル**: カジュアルなPNWスタイル（例: `oversized white organic cotton shirt, chunky knit cardigan, relaxed-fit straight denim, classic Converse Chuck Taylor sneakers`）
5. **ロケーション・光の演出**: アシュランドの地理的特徴（例: `warm natural indoor lighting, Pacific Northwest morning atmosphere`, `golden hour sunlight filtering through autumn leaves in Lithia Park`）
6. **画質・スタイルパラメータ**: `cinematic lighting, photorealistic, 8k resolution, highly detailed texture, film grain, organic aesthetics, Higgsfield quality`

### Step 3: Higgsfield MCPツールの直接呼び出し
構築した英文プロンプトを引数にして、接続されているHiggsfield MCPツールを実行します。

- **静止画生成時**:
  - **Tool**: `mcp__higgsfield__generate_image`
  - **Arguments**:
    - `prompt`: Step 2で構築した英文プロンプト
    - `soul_id`: "soul_kajael_v1_ashland"
- **動画生成時**（ユーザーから動画・モーションの指示がある場合）:
  - **Tool**: `mcp__higgsfield__generate_video`
  - **Arguments**:
    - `prompt`: Step 2で構築した英文プロンプト（カメラワークや動作指示を含む）
    - `soul_id`: "soul_kajael_v1_ashland"
