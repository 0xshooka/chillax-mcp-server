# Chillax MCP Server 🌤️🎬

天気に基づいて最適なYouTube動画を提案するMCPサーバーです。外は晴れ？それならアウトドア動画を。雨が降ってる？ジャズを聴きながら読書はいかが？あなたの一日を、天気に合わせて最高のものにするお手伝いをします。

## 🌟 特徴

- **天気連動**: OpenWeatherMap APIで取得した天気情報に基づいて動画を提案
- **多言語対応**: 都市名から自動的に言語を判定（現在対応しているのは日本語、英語、韓国語、中国語）
- **きめ細かい提案**: 晴れ、雨、猛暑、極寒、嵐など、様々な天候に対応
- **カスケード処理**: APIの結果を次のAPIの入力として使用する実践的な例

## 📋 必要なもの

- Python 3.10以上
- [OpenWeatherMap API Key](https://openweathermap.org/api) （無料プランでOK）
- [YouTube Data API v3 Key](https://developers.google.com/youtube/v3/getting-started) （無料枠あり）
- [uv](https://github.com/astral-sh/uv) （Pythonパッケージマネージャー）

## 🚀 クイックスタート

### 1. リポジトリのクローン

```bash
git clone https://github.com/0xshooka/chillax-mcp-server.git
cd chillax-mcp-server
```

### 2. 環境のセットアップ

```bash
# 実行環境向け依存関係インストール
uv sync

# 開発環境向けの依存関係インストール
uv sync --only-dev
```

### 3. APIキーの設定

`.env`ファイルを作成し、取得したAPIキーを設定します。

```bash
# .env
OPENWEATHER_API_KEY=your_openweather_api_key_here
YOUTUBE_API_KEY=your_youtube_api_key_here
```

## 🔧 使い方

### Claude Desktopでの設定

`claude_desktop_config.json`に以下の記述を追加します。

```json
{
    "mcpServers": {
        "chillax-mcp-server": {
        "command": "/path/to/uv", <!-- uvの絶対パスを指定してください -->
        "args": [
                "--directory",
                "/path/to/chillax-mcp-server", <!-- chillax-mcp-serverの絶対パスを指定してください -->
                "run",
                "chillax.py"
            ]
        }
    }
}
```

### 利用可能なツール

#### `get_activity_suggestion`
天気取得と動画提案をカスケード式に行います。(天気取得→動画提案の順番)

```
パラメータ:
- city: 都市名
- days_ahead: 何日後か

戻り値:
- 天気情報と動画提案の統合結果
```

### 使用例

```
You: 明日の東京の過ごし方を提案して

LLM: 明日の東京の天気を確認して、最適な過ごし方を提案しますね。

[get_activity_suggestion関数を実行]

明日の東京は晴れ時々曇り、最高気温24℃の過ごしやすい天気になりそうです！
外出を楽しむのに最適な日ですね。

おすすめの動画をご紹介します：
1. 「東京の隠れた公園散歩スポット10選」- 都内の穴場公園を紹介
2. 「初心者向けサイクリングコース 多摩川編」- 気持ちいい川沿いコース
...
```

## 🧪 開発

### コード品質チェック

```bash
# リンター
uv run ruff check .

# フォーマッター
uv run black .

# 型チェック
uv run mypy .
```

### テスト

```bash
# 全テスト実行
uv run pytest

# カバレッジ付き
uv run pytest --cov
```

## 📝 カスタマイズ

### 新しい言語の追加

`CITY_LANGUAGE_MAP`に都市と言語のマッピングを追加する記述例は以下の通りです。

```python
CITY_LANGUAGE_MAP = {
    # フランス
    "paris": Language.FR,
    "lyon": Language.FR,
    ...
}
```

### 天候カテゴリのカスタマイズ

`categorize_weather`関数で、新しい天候判定ロジックを追加できます。

### 検索クエリの調整

`SEARCH_QUERIES`辞書を編集して、各天候に対する検索キーワードをカスタマイズできます。

## 🤝 コントリビューション

プルリクエスト大歓迎です！

1. このリポジトリをフォーク
2. フィーチャーブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'Add some amazing feature'`)
4. ブランチにプッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを作成

## 📄 ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は[LICENSE](LICENSE)ファイルをご覧ください。

## 🙏 謝辞

- [OpenWeatherMap](https://openweathermap.org/) - 天気データAPI
- [YouTube Data API](https://developers.google.com/youtube) - 動画検索API
- [FastMCP](https://github.com/jlowin/fastmcp) - MCP サーバー実装フレームワーク

## 📞 お問い合わせ

ご質問や提案がありましたら、[Issues](https://github.com/0xshooka/chillax-mcp-server/issues)までお気軽にどうぞ！

---

**Enjoy your perfect day with Chillax! 🌈**