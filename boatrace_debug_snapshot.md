# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-05T04:50:01.507586+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×50 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×50 (24h)
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T04:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T04:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T04:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×153  [2026-06-04T23:09:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×153  [2026-06-04T23:09:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×51  [2026-06-04T23:09:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×48  [2026-06-04T18:50:44]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-04T17:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-04T11:50:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-04T09:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.4286 gap=-0.2059`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S00: n=160 hit%=30.0% hit_CI[Bonf]=[20.7,41.2]% ROI=0.90 ROI_boot95=[0.65,1.20]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=123 hit%=30.1% hit_CI[Bonf]=[19.7,43.0]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=123<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=44.8% hit_CI[Bonf]=[28.8,61.9]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.24MB / last modified 2026-06-05T04:30:03.418508+09:00

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
07 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 23:55:06,107 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 23:55:06,179 [INFO] predictor: Models loaded OK
2026-06-04 23:55:06,191 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-04 23:56:05,996 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-04 23:56:05,996 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 23:56:05,997 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 23:56:06,061 [INFO] predictor: Models loaded OK
2026-06-04 23:56:06,065 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-04 23:57:06,609 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-04 23:57:06,609 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 23:57:06,609 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 23:57:06,674 [INFO] predictor: Models loaded OK
2026-06-04 23:57:06,677 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-04 23:58:05,686 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-06-04 23:58:05,686 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 23:58:05,686 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 23:58:05,753 [INFO] predictor: Models loaded OK
2026-06-04 23:58:05,756 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-04 23:59:05,584 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-04 23:59:05,584 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-04 23:59:05,585 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-04 23:59:05,651 [INFO] predictor: Models loaded OK
2026-06-04 23:59:05,653 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 59
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 59
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 13, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 186
  CIRCUIT_BREAKER_TRIP: 50
  CIRCUIT_BREAKER_NO_ACTION: 39
  FINAL_MISSING: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 6 | 10,200 | 3,390 | -6,810 | 0.332 |
| S01_NAKAANA1 | 34 | 10 | 6,800 | 4,260 | -2,540 | 0.626 |
| S02_TETSUBAN | 21 | 6 | 4,200 | 1,640 | -2,560 | 0.39 |

## 直近アラート (24h・新しい順)
```
[23:48:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:44:05] FINAL_MISSING: {"deadline": "2026-06-04T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060403031208", "sid": "S00"}
[23:43:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:40:09] FINAL_MISSING: {"deadline": "2026-06-04T15:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060413101505", "sid": "S00"}
[23:37:06] CIRCUIT_BREAKER_TRIP: {"cost": 4200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 21, "payout": 1640, "roi_7d": 0.39, "sid": "S02_TETSUBAN"}
[23:28:05] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3390, "roi_7d": 0.332, "sid": "S00"}
[23:10:09] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:10:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:02:06] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4260, "roi_7d": 0.626, "sid": "S01_NAKAANA1"}
[22:47:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
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
| S01_NAKAANA1 | 2012R | win | 1 | 0.4989 | 4.2 | 2.10 | 200 | scan=3.2 drift=+31.2% | 20:28:20 |
| S01_NAKAANA1 | 245R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.1 drift=-3.2% | 19:27:21 |
| S02_TETSUBAN | 075R | win | 1 | 0.5891 | 2.5 | 1.47 | 200 | scan=- drift=- | 17:34:21 |
| S02_TETSUBAN | 138R | win | 1 | 0.5476 | 2.3 | 1.26 | 200 | scan=- drift=- | 14:03:22 |
| S00 | 088R | win | 1 | 0.5735 | 11.5 | 6.59 | 300 | scan=- drift=- | 13:42:20 |
| S02_TETSUBAN | 137R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 13:35:29 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 13:30:25 |
| S00 | 087R | win | 1 | 0.5476 | 36.7 | 20.10 | 300 | scan=33.7 drift=+8.9% | 13:12:33 |
| S02_TETSUBAN | 096R | win | 1 | 0.5259 | 2.1 | 1.10 | 200 | scan=2.8 drift=-25.0% | 13:02:45 |
| S02_TETSUBAN | 135R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.1 drift=+19.0% | 12:30:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | +21.9% | -61.1% | +432.7% | 12 | 5 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.9s |
| **Latency** (scan→final max) | 660.0s |
| **Traffic** (notifications 24h) | 59 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 349 | 0.4642 | 0.3181 | +0.1461 | 🟡+32% | 0.2379 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 151 | 0.4190 | 0.2781 | 0.2223 | 🔴-0.11 | 0.846 |
| S01_NAKAANA1 | win | 126 | 0.4861 | 0.3016 | 0.2450 | 🔴-0.16 | 0.753 |
| S02_TETSUBAN | win | 72 | 0.5204 | 0.4306 | 0.2582 | 🔴-0.05 | 0.775 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 6 | 0.2216 | 0.5000 | 🔴-0.2784 |
| 0.30-0.50 | 137 | 0.4173 | 0.2701 | 🔴+0.1473 |
| 0.50+ | 187 | 0.5411 | 0.3690 | 🔴+0.1721 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 31 | 0.746 |
| win | <5.0 | ✅learned | 57 | 0.745 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 12 | 0.197 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-05T04:50:01.507586+09:00_