# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-15T11:40:01.943507+09:00

### 次に取るべきアクション
> RED 優先: CRITICAL_ODDS_COLLAPSE×74 (24h) → 該当ログ確認し原因特定

### 検出された問題
- 🔴 CRITICAL_ODDS_COLLAPSE×74 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×2  [2026-04-15T11:30:02]
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

### 🔴 STRATEGY_COLLAPSE  ×5  [2026-04-15T05:37:57]
- key: `STRATEGY_COLLAPSE|2026-04-11 159R combo=1 を 4 戦略が同時採用 → 分散効果ゼロ`
- **FIX**: 4戦略以上が同 combo を採用。v18 仕様的には許容。気になれば資金配分で分散制御


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `1193885b4bcdeb4c8d16955d7ee412db`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.66MB / last modified 2026-04-15T11:39:21.678122+09:00

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
/120 parsed
2026-04-15 11:38:32,042 [INFO] scraper: odds3f: 20/20 parsed
2026-04-15 11:38:33,213 [INFO] scraper: odds2t: 30/30 parsed
2026-04-15 11:38:33,214 [INFO] scraper: odds2f: 15/15 parsed
2026-04-15 11:38:34,321 [INFO] scraper: odds_win: 6/6 parsed
2026-04-15 11:38:34,321 [INFO] scraper: fetch_race 10/8: boats=6 odds=191/191
2026-04-15 11:38:34,324 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 11:38:34,324 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-15 11:38:34,328 [INFO] run_cycle: fetched 10/8 [scan]: 156 combos
2026-04-15 11:38:34,426 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-15 11:39:05,273 [INFO] run_cycle: === run_cycle 11:39:05 ===
2026-04-15 11:39:05,273 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 11:39:05,273 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 11:39:05,345 [INFO] predictor: Models loaded OK
2026-04-15 11:39:17,799 [INFO] scraper: odds3t: 120/120 parsed
2026-04-15 11:39:18,886 [INFO] scraper: odds3f: 20/20 parsed
2026-04-15 11:39:20,136 [INFO] scraper: odds2t: 30/30 parsed
2026-04-15 11:39:20,137 [INFO] scraper: odds2f: 15/15 parsed
2026-04-15 11:39:21,235 [INFO] scraper: odds_win: 6/6 parsed
2026-04-15 11:39:21,235 [INFO] scraper: fetch_race 03/2: boats=6 odds=191/191
2026-04-15 11:39:21,256 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 11:39:21,256 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-15 11:39:21,260 [INFO] run_cycle: fetched 03/2 [final]: 156 combos
2026-04-15 11:39:21,510 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-15 11:40:08,062 [INFO] run_cycle: === run_cycle 11:40:08 ===
2026-04-15 11:40:08,062 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-15 11:40:08,062 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-15 11:40:08,189 [INFO] predictor: Models loaded OK

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 39, 'scan': 37}

## アラート件数 (24h・種類別)
```
  CRITICAL_ODDS_COLLAPSE: 74
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 8 | 10,700 | 3,270 | -7,430 | 0.306 |
| S01 | 7 | 0 | 2,600 | 0 | -2,600 | 0.0 |
| S02 | 133 | 8 | 29,800 | 4,530 | -25,270 | 0.152 |
| S03 | 73 | 6 | 15,700 | 2,620 | -13,080 | 0.167 |
| S04 | 9 | 0 | 3,300 | 0 | -3,300 | 0.0 |
| S05 | 8 | 0 | 1,700 | 0 | -1,700 | 0.0 |
| S06 | 12 | 0 | 3,600 | 0 | -3,600 | 0.0 |
| S07 | 43 | 6 | 10,900 | 3,700 | -7,200 | 0.339 |
| S08 | 6 | 0 | 1,200 | 0 | -1,200 | 0.0 |
| S09 | 41 | 7 | 10,700 | 2,270 | -8,430 | 0.212 |
| S10 | 27 | 6 | 6,500 | 3,920 | -2,580 | 0.603 |
| S11 | 27 | 0 | 4,300 | 0 | -4,300 | 0.0 |
| S12 | 8 | 0 | 1,700 | 0 | -1,700 | 0.0 |
| s1_3t_bomb | 3 | 0 | 300 | 0 | -300 | 0.0 |
| s2_2t_snipe | 16 | 0 | 1,600 | 0 | -1,600 | 0.0 |
| s3_3f_target | 91 | 14 | 9,100 | 6,880 | -2,220 | 0.756 |
| s4_3t_mid | 25 | 0 | 2,500 | 0 | -2,500 | 0.0 |

## 直近アラート (24h・新しい順)
```
[11:39:21] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:39:21] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:38:34] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:38:34] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:37:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:37:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:36:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:36:05] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:35:27] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:35:27] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
```

## 本日残レース: 107件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S03 | 172R | win | 2 | 0.2151 | 25.7 | 5.53 | 300 | scan=72.7 drift=-64.6% | 11:03:21 |
| S02 | 172R | win | 2 | 0.2151 | 25.7 | 5.53 | 300 | scan=72.7 drift=-64.6% | 11:03:20 |
| S10 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:39 |
| S09 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:37 |
| S07 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:36 |
| S03 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:35 |
| S02 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:32 |
| S00 | 146R | win | 1 | 0.4096 | 25.5 | 10.44 | 300 | scan=23.2 drift=+9.9% | 10:54:31 |
| S02 | 171R | win | 2 | 0.1365 | 39.3 | 5.36 | 300 | scan=- drift=- | 10:36:21 |
| S03 | 105R | win | 2 | 0.2473 | 27.6 | 6.82 | 300 | scan=- drift=- | 10:15:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 8 | -8.7% | -64.6% | +9.9% | 2 | 2 | 2 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-15T11:40:01.943507+09:00_