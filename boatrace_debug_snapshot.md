# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-15T12:10:02.193750+09:00

### 次に取るべきアクション
> RED 優先: CRITICAL_ODDS_COLLAPSE×132 (24h) → 該当ログ確認し原因特定

### 検出された問題
- 🔴 CRITICAL_ODDS_COLLAPSE×132 (24h)
- 🟡 LARGE_ODDS_DRIFT×56 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 LARGE_ODDS_DRIFT  ×56  [2026-04-15T12:03:27]
- key: `LARGE_ODDS_DRIFT|`
- **FIX**: 10%超ドリフト発生→情報として監視、閾値調整は config.json の statistical_tests.drift_alert_pct

### 🟡 HEALTH_CHECK_FAIL  ×4  [2026-04-15T11:30:02]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### 🔴 ROI_CRITICAL  ×1  [2026-04-15T06:03:28]
- key: `ROI_CRITICAL|TEST_AUDIT_PHASE2`
- **FIX**: 該当戦略を strategies.json で enabled:false に→N≥300 Wilson下限<1.0確定のため

### 🔴 ROI_CRITICAL  ×1  [2026-04-15T06:01:31]
- key: `ROI_CRITICAL|TEST_AUDIT_IGNORE`
- **FIX**: 該当戦略を strategies.json で enabled:false に→N≥300 Wilson下限<1.0確定のため

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 017R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 024R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 029R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 0411R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 069R combo=1-5-4 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 066R combo=1-4-2 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 103R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 119R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|20260410 117R combo=1-4-3 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 144R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 1410R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 145R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-12 148R combo=1 を 6 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 147R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-13 1411R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-14 142R combo=1 を 5 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `1193885b4bcdeb4c8d16955d7ee412db`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.69MB / last modified 2026-04-15T12:09:05.697218+09:00

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
```

### 直近 run_cycle ログ (末尾)
```
s3f: 20/20 parsed
2026-04-15 12:07:19,647 [INFO] scraper: odds2t: 30/30 parsed
2026-04-15 12:07:19,648 [INFO] scraper: odds2f: 15/15 parsed
2026-04-15 12:07:20,773 [INFO] scraper: odds_win: 5/6 parsed
2026-04-15 12:07:20,773 [INFO] scraper: fetch_race 02/4: boats=6 odds=190/191
2026-04-15 12:07:20,794 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 12:07:20,794 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-04-15 12:07:20,798 [INFO] run_cycle: fetched 02/4 [scan]: 155 combos
2026-04-15 12:07:20,831 [INFO] race_id: notif: nid=2026041502041214 sid=S11 phase=scan rank=GREEN
2026-04-15 12:07:21,138 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 12:07:21,479 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 12:07:21,526 [INFO] run_cycle: SCAN S11 戸田4R GREEN
2026-04-15 12:07:21,612 [INFO] run_cycle: run_cycle done: 1 notifications
2026-04-15 12:08:05,932 [INFO] run_cycle: === run_cycle 12:08:05 ===
2026-04-15 12:08:05,932 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 12:08:05,932 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 12:08:06,016 [INFO] predictor: Models loaded OK
2026-04-15 12:08:06,225 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-15 12:09:05,335 [INFO] run_cycle: === run_cycle 12:09:05 ===
2026-04-15 12:09:05,335 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 12:09:05,335 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 12:09:05,382 [INFO] predictor: Models loaded OK
2026-04-15 12:09:05,563 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-15 12:10:08,221 [INFO] run_cycle: === run_cycle 12:10:08 ===
2026-04-15 12:10:08,221 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 12:10:08,221 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 45, 'scan': 43}

## アラート件数 (24h・種類別)
```
  CRITICAL_ODDS_COLLAPSE: 132
  LARGE_ODDS_DRIFT: 56
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 8 | 10,700 | 3,270 | -7,430 | 0.306 |
| S01 | 7 | 0 | 2,600 | 0 | -2,600 | 0.0 |
| S02 | 133 | 8 | 29,800 | 4,530 | -25,270 | 0.152 |
| S03 | 73 | 6 | 15,700 | 2,620 | -13,080 | 0.167 |
| S04 | 10 | 0 | 3,500 | 0 | -3,500 | 0.0 |
| S05 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |
| S06 | 13 | 0 | 3,800 | 0 | -3,800 | 0.0 |
| S07 | 43 | 6 | 10,900 | 3,700 | -7,200 | 0.339 |
| S08 | 8 | 0 | 1,400 | 0 | -1,400 | 0.0 |
| S09 | 41 | 7 | 10,700 | 2,270 | -8,430 | 0.212 |
| S10 | 27 | 6 | 6,500 | 3,920 | -2,580 | 0.603 |
| S11 | 29 | 0 | 4,500 | 0 | -4,500 | 0.0 |
| S12 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |
| s1_3t_bomb | 3 | 0 | 300 | 0 | -300 | 0.0 |
| s2_2t_snipe | 15 | 0 | 1,500 | 0 | -1,500 | 0.0 |
| s3_3f_target | 87 | 14 | 8,700 | 6,880 | -1,820 | 0.791 |
| s4_3t_mid | 25 | 0 | 2,500 | 0 | -2,500 | 0.0 |

## 直近アラート (24h・新しい順)
```
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:09:05] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:09:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[12:09:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
```

## 本日残レース: 99件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S12 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:26 |
| S12 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:26 |
| S11 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:25 |
| S11 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:25 |
| S08 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:23 |
| S08 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:23 |
| S06 | 174R | 2t | 1-6 | 0.0787 | 94.3 | 7.42 | 200 | scan=- drift=- | 12:03:21 |
| S05 | 174R | 3t | 1-6-5 | 0.0208 | 628.3 | 13.05 | 100 | scan=707.5 drift=-11.2% | 12:03:20 |
| S05 | 174R | 3t | 1-6-3 | 0.0226 | 672.6 | 15.17 | 100 | scan=501.1 drift=+34.2% | 12:03:20 |
| S04 | 174R | 2t | 1-6 | 0.0787 | 94.3 | 7.42 | 200 | scan=- drift=- | 12:03:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 8 | +11.5% | -11.2% | +34.2% | 4 | 0 | 8 |
| win | 8 | -8.7% | -64.6% | +9.9% | 2 | 2 | 2 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-15T12:10:02.193750+09:00_