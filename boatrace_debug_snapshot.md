# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-15T13:48:27.260458+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×2 (24h) → ログ/DB確認

### 検出された問題
- 🟡 LARGE_ODDS_DRIFT×8 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×2 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 LARGE_ODDS_DRIFT  ×360  [2026-04-15T13:03:33]
- key: `LARGE_ODDS_DRIFT|`
- **FIX**: 10%超ドリフト発生→情報として監視、閾値調整は config.json の statistical_tests.drift_alert_pct

### 🟡 ORPHAN_SCAN  ×1  [2026-04-15T13:00:27]
- key: `ORPHAN_SCAN|6 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-13 017R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-14 024R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-14 029R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-12 0411R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-11 069R combo=1-5-4 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-12 066R combo=1-4-2 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-14 103R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-11 119R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|20260410 117R combo=1-4-3 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-11 144R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-11 1410R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-12 145R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-12 148R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-13 147R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-13 1411R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-14 142R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-11 159R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×3  [2026-04-15T12:57:06]
- key: `STRATEGY_COLLAPSE|2026-04-12 155R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `1193885b4bcdeb4c8d16955d7ee412db`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.99MB / last modified 2026-04-15T13:48:25.269678+09:00

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
cycle 13:47:06 ===
2026-04-15 13:47:06,058 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 13:47:06,058 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 13:47:06,129 [INFO] predictor: Models loaded OK
2026-04-15 13:47:17,683 [INFO] scraper: odds3t: 120/120 parsed
2026-04-15 13:47:18,795 [INFO] scraper: odds3f: 20/20 parsed
2026-04-15 13:47:19,902 [INFO] scraper: odds2t: 30/30 parsed
2026-04-15 13:47:19,903 [INFO] scraper: odds2f: 15/15 parsed
2026-04-15 13:47:20,982 [INFO] scraper: odds_win: 6/6 parsed
2026-04-15 13:47:20,982 [INFO] scraper: fetch_race 22/4: boats=6 odds=191/191
2026-04-15 13:47:20,993 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 13:47:20,994 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-15 13:47:21,000 [INFO] run_cycle: fetched 22/4 [scan]: 156 combos
2026-04-15 13:47:21,127 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-15 13:48:05,962 [INFO] run_cycle: === run_cycle 13:48:05 ===
2026-04-15 13:48:05,963 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 13:48:05,963 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 13:48:06,009 [INFO] predictor: Models loaded OK
2026-04-15 13:48:18,604 [INFO] scraper: odds3t: 120/120 parsed
2026-04-15 13:48:19,740 [INFO] scraper: odds3f: 20/20 parsed
2026-04-15 13:48:20,844 [INFO] scraper: odds2t: 28/30 parsed
2026-04-15 13:48:20,845 [INFO] scraper: odds2f: 14/15 parsed
2026-04-15 13:48:21,912 [INFO] scraper: odds_win: 4/6 parsed
2026-04-15 13:48:21,912 [INFO] scraper: fetch_race 16/7: boats=6 odds=186/191
2026-04-15 13:48:21,924 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 13:48:21,925 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-04-15 13:48:21,932 [INFO] run_cycle: fetched 16/7 [scan]: 152 combos
2026-04-15 13:48:22,185 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 2.5 | 0.55 | True |
| S01 | A | 2t | 5.0 | 0.6 | True |
| S02 | S | win | 5.0 | 0.1 | True |
| S03 | S | win | 5.0 | 0.2 | True |
| S04 | A | 2t | 5.0 | 0.55 | True |
| S05 | B | 3t | 10.0 | 0.4 | True |
| S06 | A | 2t | 5.0 | 0.5 | True |
| S07 | S | win | 3.0 | 0.5 | True |
| S08 | B | 3t | 10.0 | 0.5 | True |
| S09 | S | win | 2.5 | 0.55 | True |
| S10 | S | win | 2.25 | 0.6 | True |
| S11 | B | 3t | 10.0 | 0.2 | True |
| S12 | B | 3t | 10.0 | 0.4 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 129
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 129
  }
]
```

## Phase別通知記録 (24h)
{'final': 63, 'scan': 66}

## アラート件数 (24h・種類別)
```
  LARGE_ODDS_DRIFT: 8
  CRITICAL_ODDS_COLLAPSE: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 19 | 10,700 | 10,420 | -280 | 0.974 |
| S01 | 7 | 0 | 2,600 | 0 | -2,600 | 0.0 |
| S02 | 134 | 14 | 30,100 | 7,000 | -23,100 | 0.233 |
| S03 | 74 | 12 | 16,000 | 5,090 | -10,910 | 0.318 |
| S04 | 11 | 0 | 3,700 | 0 | -3,700 | 0.0 |
| S05 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |
| S06 | 14 | 0 | 4,000 | 0 | -4,000 | 0.0 |
| S07 | 43 | 17 | 10,900 | 8,860 | -2,040 | 0.813 |
| S08 | 8 | 0 | 1,400 | 0 | -1,400 | 0.0 |
| S09 | 41 | 19 | 10,700 | 10,420 | -280 | 0.974 |
| S10 | 27 | 15 | 6,500 | 7,420 | +920 | 1.142 |
| S11 | 31 | 0 | 4,700 | 0 | -4,700 | 0.0 |
| S12 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |

## 直近アラート (24h・新しい順)
```
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[11:03:29] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:03:29] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
```

## 本日残レース: 74件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S06 | 176R | 2t | 1-5 | 0.1223 | 44.3 | 5.42 | 200 | scan=48.7 drift=-9.0% | 13:03:21 |
| S04 | 176R | 2t | 1-5 | 0.1223 | 44.3 | 5.42 | 200 | scan=48.7 drift=-9.0% | 13:03:20 |
| S03 | 164R | win | 3 | 0.1414 | 36.0 | 5.09 | 300 | scan=- drift=- | 12:27:21 |
| S02 | 164R | win | 3 | 0.1414 | 36.0 | 5.09 | 300 | scan=- drift=- | 12:27:20 |
| S11 | 109R | 3t | 1-6-4 | 0.0515 | 213.6 | 11.01 | 100 | scan=209.1 drift=+2.2% | 12:22:21 |
| S11 | 024R | 3t | 4-1-2 | 0.0568 | 193.8 | 11.01 | 100 | scan=180.5 drift=+7.4% | 12:11:21 |
| S12 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:26 |
| S12 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:26 |
| S11 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:25 |
| S11 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 2t | 2 | -9.0% | -9.0% | -9.0% | 0 | 0 | 0 |
| 3t | 10 | +10.2% | -11.2% | +34.2% | 4 | 0 | 8 |
| win | 8 | -8.7% | -64.6% | +9.9% | 2 | 2 | 2 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-15T13:48:27.260458+09:00_