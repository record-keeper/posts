# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-17T08:50:02.176536+09:00

### 次に取るべきアクション
> RED最優先: ⚠️ DB更新が20分前（run_cycle停止疑い・今レース時間帯） → ログ/DB確認

### 検出された問題
- 🔴 ⚠️ DB更新が20分前（run_cycle停止疑い・今レース時間帯）
- 🔴 CALIBRATION_DRIFT×20 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×12 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×2  [2026-04-17T08:30:02]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-13 017R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-14 024R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-14 029R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-12 0411R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-11 069R combo=1-5-4 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-12 066R combo=1-4-2 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-14 103R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-11 119R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|20260410 117R combo=1-4-3 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-11 144R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-11 1410R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-12 145R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-12 148R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-13 147R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-13 1411R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-14 142R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-11 159R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-12 155R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-17T03:11:49]
- key: `STRATEGY_COLLAPSE|2026-04-13 154R combo=2 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `657711d6153ff6f442c9436df8dd5201`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.99MB / last modified 2026-04-17T08:30:03.015484+09:00

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
 08:46:20,685 [INFO] run_cycle: fetched 21/1 [final]: 156 combos
2026-04-17 08:46:20,850 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-17 08:47:04,911 [INFO] run_cycle: === run_cycle 08:47:04 ===
2026-04-17 08:47:04,911 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-17 08:47:04,911 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-17 08:47:04,979 [INFO] predictor: Models loaded OK
2026-04-17 08:47:05,138 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-17 08:48:04,924 [INFO] run_cycle: === run_cycle 08:48:04 ===
2026-04-17 08:48:04,925 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-17 08:48:04,925 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-17 08:48:04,968 [INFO] predictor: Models loaded OK
2026-04-17 08:48:05,046 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-17 08:49:05,224 [INFO] run_cycle: === run_cycle 08:49:05 ===
2026-04-17 08:49:05,224 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-17 08:49:05,224 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-17 08:49:05,307 [INFO] predictor: Models loaded OK
2026-04-17 08:49:16,765 [INFO] scraper: odds3t: 120/120 parsed
2026-04-17 08:49:17,877 [INFO] scraper: odds3f: 20/20 parsed
2026-04-17 08:49:18,982 [INFO] scraper: odds2t: 30/30 parsed
2026-04-17 08:49:18,984 [INFO] scraper: odds2f: 14/15 parsed
2026-04-17 08:49:20,085 [INFO] scraper: odds_win: 5/6 parsed
2026-04-17 08:49:20,086 [INFO] scraper: fetch_race 23/2: boats=6 odds=189/191
2026-04-17 08:49:20,097 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-17 08:49:20,097 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-17 08:49:20,105 [INFO] run_cycle: fetched 23/2 [scan]: 155 combos
2026-04-17 08:49:20,187 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 4
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 4
  }
]
```

## Phase別通知記録 (24h)
{}

## アラート件数 (24h・種類別)
```
  CALIBRATION_DRIFT: 20
  CIRCUIT_BREAKER_TRIP: 12
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|

## 直近アラート (24h・新しい順)
```
[03:31:06] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S11", "n": 32, "roi_7d": 0.0, "cost": 4800, "payout": 0}
[03:31:06] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S03", "n": 75, "roi_7d": 0.312, "cost": 16300, "payout": 5090}
[03:31:06] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S02", "n": 137, "roi_7d": 0.226, "cost": 31000, "payout": 7000}
[03:31:06] CALIBRATION_DRIFT: {"kind": "CALIBRATION_DRIFT", "bt": "3t", "n": 60, "avg_pred": 0.0776, "avg_actual": 0, "overconf_pct": 100.0}
[03:31:06] CALIBRATION_DRIFT: {"kind": "CALIBRATION_DRIFT", "bt": "2t", "n": 35, "avg_pred": 0.1817, "avg_actual": 0, "overconf_pct": 100.0}
[03:31:05] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S11", "n": 32, "roi_7d": 0.0, "cost": 4800, "payout": 0}
[03:31:05] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S03", "n": 75, "roi_7d": 0.312, "cost": 16300, "payout": 5090}
[03:31:05] CIRCUIT_BREAKER_TRIP: {"kind": "CIRCUIT_BREAKER_TRIP", "sid": "S02", "n": 137, "roi_7d": 0.226, "cost": 31000, "payout": 7000}
[03:31:05] CALIBRATION_DRIFT: {"kind": "CALIBRATION_DRIFT", "bt": "3t", "n": 60, "avg_pred": 0.0776, "avg_actual": 0, "overconf_pct": 100.0}
[03:31:05] CALIBRATION_DRIFT: {"kind": "CALIBRATION_DRIFT", "bt": "2t", "n": 35, "avg_pred": 0.1817, "avg_actual": 0, "overconf_pct": 100.0}
```

## 本日残レース: 141件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|

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
_auto-generated by claude_snapshot.py at 2026-04-17T08:50:02.176536+09:00_