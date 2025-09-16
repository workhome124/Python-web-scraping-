# 自動スケジューラー

24時間ごとに `run_both.py` を自動実行するスケジューラーです。

## ファイル構成

- `scheduler.py` - メインのスケジューラープログラム
- `scheduler_config.py` - 設定ファイル（実行時刻やオプションをカスタマイズ）
- `start_scheduler.bat` - Windows用の起動バッチファイル
- `requirements.txt` - 必要なPythonパッケージ
- `scheduler.log` - 実行ログ（自動生成）

## セットアップ

1. **依存関係のインストール**
   ```bash
   pip install -r requirements.txt
   ```

2. **設定のカスタマイズ（オプション）**
   `scheduler_config.py` を編集して実行時刻やオプションを変更できます：
   ```python
   # 実行時刻設定 (24時間形式)
   SCHEDULE_TIME = "09:00"  # 午前9時
   
   # 初回実行するかどうか
   RUN_IMMEDIATELY = True
   
   # run_both.pyの実行オプション
   RUN_OPTIONS = {
       "site": "all",        # "amazon", "rakuten", "all"
       "no_scrape": False,   # Trueでスクレイピングをスキップ
       "no_analyze": False   # Trueで分析をスキップ
   }
   ```

## 実行方法

### Windows
```bash
# バッチファイルで実行（推奨）
start_scheduler.bat

# または直接実行
python scheduler.py
```

### Linux/Mac
```bash
python scheduler.py
```

## 機能

- **24時間ごとの自動実行**: 毎日同じ時刻に `run_both.py` を実行
- **初回実行**: スケジューラー開始時に即座に1回実行（設定可能）
- **ログ記録**: 実行結果を `scheduler.log` に記録
- **エラーハンドリング**: 実行失敗時もスケジューラーは継続
- **カスタマイズ可能**: 実行時刻やオプションを設定ファイルで変更

## 停止方法

- **Ctrl+C** を押してスケジューラーを停止

## ログ確認

実行ログは `scheduler.log` ファイルで確認できます：
```bash
# 最新のログを表示
tail -f scheduler.log

# 全ログを表示
cat scheduler.log
```

## 注意事項

- スケジューラーは継続的に動作するため、PCを常時起動しておく必要があります
- 長時間実行する場合は、PCの電源設定でスリープを無効にすることを推奨します
- ログファイルが大きくなりすぎる場合は、定期的に削除またはローテーションしてください

## トラブルシューティング

1. **Pythonが見つからない場合**
   - Pythonがインストールされているか確認
   - PATHにPythonが追加されているか確認

2. **依存関係エラー**
   ```bash
   pip install -r requirements.txt
   ```

3. **権限エラー**
   - ログファイルの書き込み権限を確認
   - 管理者権限で実行してみる

4. **実行時刻がずれる場合**
   - システム時刻を確認
   - タイムゾーン設定を確認
