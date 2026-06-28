# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-29T02:30:01.669912+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×41 (24h)
- 🔴 PSI_DRIFT_DETECTED×27 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×7 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-29T01:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×44  [2026-06-28T23:16:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×50  [2026-06-28T23:10:11]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-06-28T23:10:11]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×50  [2026-06-28T23:10:11]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-06-28T18:20:10]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-28T18:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 KS_ODDS_DRIFT  ×26  [2026-06-28T13:02:40]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CALIBRATION_DRIFT  ×51  [2026-06-28T11:01:46]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-06-28T11:00:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-06-28T10:40:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=23 pred=0.3214 actual=0.2174 gap=+0.1040`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S00: n=167 hit%=25.1% hit_CI[Bonf]=[16.8,35.9]% ROI=0.65 ROI_boot95=[0.46,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=29.2% hit_CI[Bonf]=[19.4,41.3]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=28.8% hit_CI[Bonf]=[16.3,45.6]% ROI=0.45 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.36MB / last modified 2026-06-29T02:30:03.732242+09:00

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
40 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 23:55:06,740 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 23:55:06,812 [INFO] predictor: Models loaded OK
2026-06-28 23:55:06,818 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-28 23:56:04,518 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-06-28 23:56:04,518 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 23:56:04,518 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 23:56:04,590 [INFO] predictor: Models loaded OK
2026-06-28 23:56:04,596 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-28 23:57:05,890 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-06-28 23:57:05,890 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 23:57:05,890 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 23:57:05,959 [INFO] predictor: Models loaded OK
2026-06-28 23:57:05,966 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-28 23:58:06,089 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-28 23:58:06,089 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 23:58:06,090 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 23:58:06,164 [INFO] predictor: Models loaded OK
2026-06-28 23:58:06,172 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-28 23:59:05,553 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-28 23:59:05,553 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 23:59:05,553 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 23:59:05,594 [INFO] predictor: Models loaded OK
2026-06-28 23:59:05,601 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 30, 'result': 15, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 199
  FINAL_MISSING: 41
  KS_ODDS_DRIFT: 31
  PSI_DRIFT_DETECTED: 27
  CIRCUIT_BREAKER_TRIP: 26
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 7
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 10 | 13,200 | 7,020 | -6,180 | 0.532 |
| S01_NAKAANA1 | 33 | 12 | 6,600 | 6,120 | -480 | 0.927 |
| S02_TETSUBAN | 6 | 2 | 1,200 | 600 | -600 | 0.5 |

## 直近アラート (24h・新しい順)
```
[23:55:06] FINAL_MISSING: {"deadline": "2026-06-28T15:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062802101521", "sid": "S00"}
[23:34:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 294, "n_recent": 83, "psi": 0.263}
[23:23:06] FINAL_MISSING: {"deadline": "2026-06-28T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062802011047", "sid": "S00"}
[23:11:05] FINAL_MISSING: {"deadline": "2026-06-28T14:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062805071436", "sid": "S00"}
[23:10:09] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:10:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:01:05] FINAL_MISSING: {"deadline": "2026-06-28T13:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062804041325", "sid": "S00"}
[22:59:06] CIRCUIT_BREAKER_TRIP: {"cost": 13200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 7020, "roi_7d": 0.532, "sid": "S00"}
[22:55:06] FINAL_MISSING: {"deadline": "2026-06-28T15:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062802101521", "sid": "S00"}
[22:33:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 294, "n_recent": 83, "psi": 0.263}
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
| S01_NAKAANA1 | 074R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=3.3 drift=+9.1% | 17:10:35 |
| S00 | 012R | win | 1 | 0.2290 | 8.6 | 1.97 | 300 | scan=18.3 drift=-53.0% | 15:59:22 |
| S02_TETSUBAN | 1311R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=2.3 drift=-4.3% | 15:36:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.7 drift=+2.1% | 15:25:22 |
| S01_NAKAANA1 | 056R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=3.5 drift=+0.0% | 14:01:20 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=3.3 drift=-3.0% | 13:23:28 |
| S00 | 054R | win | 1 | 0.5701 | 15.9 | 9.06 | 300 | scan=25.0 drift=-36.4% | 13:00:43 |
| S02_TETSUBAN | 034R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 12:33:20 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.3 drift=-9.1% | 12:21:30 |
| S01_NAKAANA1 | 174R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=3.1 drift=+0.0% | 12:18:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +25.4% | -67.9% | +482.2% | 16 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 429.0s |
| **Latency** (scan→final max) | 624.8s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 377 | 0.4795 | 0.2918 | +0.1877 | 🟡+39% | 0.2424 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4397 | 0.2761 | 0.2291 | 🔴-0.15 | 0.718 |
| S01_NAKAANA1 | win | 139 | 0.4912 | 0.3022 | 0.2436 | 🔴-0.16 | 0.796 |
| S02_TETSUBAN | win | 75 | 0.5440 | 0.3067 | 0.2692 | 🔴-0.27 | 0.48 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 12 | 0.2253 | 0.0833 | 🔴+0.1420 |
| 0.30-0.50 | 127 | 0.4252 | 0.2362 | 🔴+0.1889 |
| 0.50+ | 224 | 0.5442 | 0.3348 | 🔴+0.2093 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 48 | 0.732 |
| win | <5.0 | ✅learned | 102 | 0.725 |
| win | <10.0 | ✅learned | 60 | 0.489 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-29T02:30:01.669912+09:00_