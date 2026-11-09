# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-10T05:10:01.127057+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×33 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×124 (24h)
- 🔴 PSI_DRIFT_DETECTED×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×39  [2026-11-09T23:21:09]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-11-09T23:21:09]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-11-09T20:08:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T18:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T17:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T17:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T16:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T16:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T14:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 13 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-09T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-09T12:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-09T12:05:13]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-11-09T11:15:15]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_DROP  ×17  [2026-11-09T10:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-09T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-09T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-09T06:00:08]
- key: `ORPHAN_SCAN|188 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-09T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3218 actual=0.1333 gap=+0.1885`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.76MB / last modified 2026-11-10T05:00:10.212569+09:00

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

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
51 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-09 23:55:03,851 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-09 23:55:03,881 [INFO] predictor: Models loaded OK
2026-11-09 23:55:03,883 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-09 23:56:03,864 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-11-09 23:56:03,864 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-09 23:56:03,864 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-09 23:56:03,893 [INFO] predictor: Models loaded OK
2026-11-09 23:56:03,895 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-09 23:57:03,639 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-11-09 23:57:03,639 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-09 23:57:03,639 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-09 23:57:03,667 [INFO] predictor: Models loaded OK
2026-11-09 23:57:03,669 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-09 23:58:03,586 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-11-09 23:58:03,586 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-09 23:58:03,586 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-09 23:58:03,630 [INFO] predictor: Models loaded OK
2026-11-09 23:58:03,634 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-09 23:59:03,507 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-11-09 23:59:03,507 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-09 23:59:03,507 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-09 23:59:03,537 [INFO] predictor: Models loaded OK
2026-11-09 23:59:03,539 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 30
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 30
  }
]
```

## Phase別通知記録 (24h)
{'final': 8, 'result': 4, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 232
  FINAL_MISSING: 124
  PSI_DRIFT_DETECTED: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 8 | 1 | 2,400 | 540 | -1,860 | 0.225 |
| S01_NAKAANA1 | 17 | 8 | 3,400 | 4,800 | +1,400 | 1.412 |
| S02_TETSUBAN | 11 | 5 | 2,200 | 1,560 | -640 | 0.709 |

## 直近アラート (24h・新しい順)
```
[23:54:03] FINAL_MISSING: {"deadline": "2026-11-09T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110902021112", "sid": "S00"}
[23:49:04] FINAL_MISSING: {"deadline": "2026-11-09T13:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110914061308", "sid": "S00"}
[23:43:04] FINAL_MISSING: {"deadline": "2026-11-09T12:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110921081202", "sid": "S00"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-11-09T11:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110923081153", "sid": "S00"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-11-09T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110905041155", "sid": "S01_NAKAANA1"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-11-09T11:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110905041155", "sid": "S00"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-11-09T16:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110902121600", "sid": "S01_NAKAANA1"}
[23:29:04] FINAL_MISSING: {"deadline": "2026-11-09T12:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110905061253", "sid": "S02_TETSUBAN"}
[23:29:04] FINAL_MISSING: {"deadline": "2026-11-09T10:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110902011045", "sid": "S00"}
[23:25:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 310, "n_recent": 36, "psi": 1.364}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 078R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.1 drift=+9.5% | 18:21:25 |
| S02_TETSUBAN | 055R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=2.6 drift=+7.7% | 12:22:03 |
| S00 | 085R | win | 1 | 0.5123 | 5.8 | 2.97 | 300 | scan=6.3 drift=-7.9% | 12:08:50 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=- drift=- | 10:44:01 |
| S01_NAKAANA1 | 196R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=3.4 drift=+17.6% | 17:36:24 |
| S02_TETSUBAN | 0311R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=2.1 drift=+4.8% | 15:28:25 |
| S02_TETSUBAN | 057R | win | 1 | 0.5719 | 2.3 | 1.32 | 200 | scan=- drift=- | 13:20:23 |
| S00 | 087R | win | 1 | 0.0295 | 7.7 | 0.23 | 300 | scan=- drift=- | 13:05:48 |
| S00 | 083R | win | 1 | 0.3177 | 7.2 | 2.29 | 300 | scan=21.7 drift=-66.8% | 11:08:23 |
| S00 | 112R | win | 1 | 0.3177 | 8.5 | 2.70 | 300 | scan=- drift=- | 10:53:11 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 20 | -4.4% | -66.8% | +17.6% | 5 | 1 | 9 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 467.6s |
| **Latency** (scan→final max) | 649.2s |
| **Traffic** (notifications 24h) | 30 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 346 | 0.4746 | 0.3150 | +0.1596 | 🟡+34% | 0.2294 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 140 | 0.4279 | 0.2571 | 0.2083 | 🔴-0.09 | 0.676 |
| S01_NAKAANA1 | win | 146 | 0.4868 | 0.3082 | 0.2371 | 🔴-0.11 | 0.755 |
| S02_TETSUBAN | win | 60 | 0.5538 | 0.4667 | 0.2599 | 🔴-0.04 | 1.053 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 8 | 0.2290 | 0.1250 | 🔴+0.1040 |
| 0.30-0.50 | 126 | 0.4121 | 0.2778 | 🔴+0.1343 |
| 0.50+ | 199 | 0.5453 | 0.3668 | 🔴+0.1785 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 202 | 0.807 |
| win | <5.0 | ✅learned | 369 | 0.742 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-11-10T05:10:01.127057+09:00_