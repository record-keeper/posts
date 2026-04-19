# ClaudeDebug スナップショット

## 🟢 現状: GREEN

**生成**: 2026-04-19T17:00:02.419246+09:00

### 次に取るべきアクション
> 特になし。運用継続。

### 問題なし、運用継続してOK。

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×1  [2026-04-19T17:00:03]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### 🟡 ORPHAN_SCAN  ×1  [2026-04-19T06:00:06]
- key: `ORPHAN_SCAN|1 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `657711d6153ff6f442c9436df8dd5201`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.99MB / last modified 2026-04-19T17:00:03.302638+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup
```

### 直近 run_cycle ログ (末尾)
```
 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-19 16:59:05,591 [INFO] predictor: Models loaded OK
2026-04-19 16:59:16,952 [INFO] scraper: odds3t: 120/120 parsed
2026-04-19 16:59:18,021 [INFO] scraper: odds3f: 20/20 parsed
2026-04-19 16:59:19,088 [INFO] scraper: odds2t: 30/30 parsed
2026-04-19 16:59:19,089 [INFO] scraper: odds2f: 15/15 parsed
2026-04-19 16:59:20,156 [INFO] scraper: odds_win: 5/6 parsed
2026-04-19 16:59:20,156 [INFO] scraper: fetch_race 24/5: boats=6 odds=190/191
2026-04-19 16:59:20,169 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-19 16:59:20,169 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-19 16:59:20,176 [INFO] run_cycle: fetched 24/5 [final]: 155 combos
2026-04-19 16:59:23,582 [INFO] scraper: odds3t: 120/120 parsed
2026-04-19 16:59:24,659 [INFO] scraper: odds3f: 20/20 parsed
2026-04-19 16:59:25,761 [INFO] scraper: odds2t: 30/30 parsed
2026-04-19 16:59:25,762 [INFO] scraper: odds2f: 15/15 parsed
2026-04-19 16:59:26,824 [INFO] scraper: odds_win: 4/6 parsed
2026-04-19 16:59:26,824 [INFO] scraper: fetch_race 20/5: boats=6 odds=189/191
2026-04-19 16:59:26,833 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-19 16:59:26,833 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-04-19 16:59:26,841 [INFO] run_cycle: fetched 20/5 [scan]: 154 combos
2026-04-19 16:59:30,238 [INFO] scraper: odds3t: 120/120 parsed
2026-04-19 16:59:31,343 [INFO] scraper: odds3f: 20/20 parsed
2026-04-19 16:59:32,418 [INFO] scraper: odds2t: 30/30 parsed
2026-04-19 16:59:32,419 [INFO] scraper: odds2f: 15/15 parsed
2026-04-19 16:59:33,481 [INFO] scraper: odds_win: 6/6 parsed
2026-04-19 16:59:33,481 [INFO] scraper: fetch_race 06/12: boats=6 odds=191/191
2026-04-19 16:59:33,491 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-19 16:59:33,493 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-19 16:59:33,499 [INFO] run_cycle: fetched 06/12 [scan]: 156 combos
2026-04-19 16:59:33,686 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[]
```

## Phase別通知記録 (24h)
{}

## アラート件数 (24h・種類別)
```
  (なし)
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 2 | 0 | 600 | 0 | -600 | 0.0 |

## 直近アラート (24h・新しい順)
```
```

## 本日残レース: 42件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 094R | win | 1 | 0.4781 | 9.0 | 4.30 | 300 | scan=- drift=- | 12:07:21 |
| S00 | 092R | win | 1 | 0.4219 | 7.7 | 3.25 | 300 | scan=- drift=- | 11:05:20 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 0s |
| **Latency** (scan→final max) | 0s |
| **Traffic** (notifications 24h) | 0 |
| **Errors** (send fail rate) | ✅ 0.0% |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 0 | 0.35 |
| win | <10.0 | ⚠️fallback | 0 | 0.32 |
| win | <20.0 | ⚠️fallback | 0 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-04-19T17:00:02.419246+09:00_