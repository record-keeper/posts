# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-11T20:00:01.910886+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 PSI_DRIFT_DETECTED×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T20:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-11-11T19:38:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T19:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×25  [2026-11-11T19:23:52]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-11-11T19:23:52]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T19:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T16:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T15:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 12 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T14:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-11T13:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-11-11T11:14:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-11-11T10:58:35]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-11T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-11T06:00:12]
- key: `ORPHAN_SCAN|196 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-11T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-11T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=8 pred=0.2290 actual=0.1250 gap=+0.1040`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-11T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3219 actual=0.1034 gap=+0.2185`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-11T06:00:12]
- key: `ROI_STAT|S00: n=135 hit%=26.7% hit_CI[Bonf]=[17.3,38.8]% ROI=0.70 ROI_boot95=[0.49,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-11T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=135<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-11T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=144 hit%=31.2% hit_CI[Bonf]=[21.4,43.2]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.86MB / last modified 2026-11-11T20:00:04.555604+09:00

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
-11 19:56:01,965 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-11 19:56:01,973 [INFO] run_cycle: fetched 19/11 [scan]: 156 combos
2026-11-11 19:56:02,188 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-11 19:57:05,029 [INFO] run_cycle: === run_cycle 19:57:05 ===
2026-11-11 19:57:05,029 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-11 19:57:05,030 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-11 19:57:05,099 [INFO] predictor: Models loaded OK
2026-11-11 19:57:05,230 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-11 19:58:05,737 [INFO] run_cycle: === run_cycle 19:58:05 ===
2026-11-11 19:58:05,737 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-11 19:58:05,737 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-11 19:58:05,796 [INFO] predictor: Models loaded OK
2026-11-11 19:58:05,932 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-11 19:59:04,832 [INFO] run_cycle: === run_cycle 19:59:04 ===
2026-11-11 19:59:04,832 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-11 19:59:04,832 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-11 19:59:04,899 [INFO] predictor: Models loaded OK
2026-11-11 19:59:33,521 [INFO] scraper: odds3t: 120/120 parsed
2026-11-11 19:59:42,622 [INFO] scraper: odds3f: 20/20 parsed
2026-11-11 19:59:53,634 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=11&jcd=19&hd=20261111: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-11 20:00:04,703 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=11&jcd=19&hd=20261111: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 7, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 242
  FINAL_MISSING: 78
  PSI_DRIFT_DETECTED: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 8 | 2 | 2,400 | 2,250 | -150 | 0.938 |
| S01_NAKAANA1 | 15 | 4 | 3,000 | 2,560 | -440 | 0.853 |
| S02_TETSUBAN | 10 | 6 | 2,000 | 1,820 | -180 | 0.91 |

## 直近アラート (24h・新しい順)
```
[19:58:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 400}
[19:57:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 412}
[19:56:02] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 289, "n_recent": 33, "psi": 0.976}
[19:53:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 415}
[19:51:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 417}
[19:48:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 423}
[19:47:13] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 418}
[19:45:16] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 413}
[19:43:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 421}
[19:42:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 422}
```

## 本日残レース: 5件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 139件 締切済
- 通知発射: scan=19 nid / final=14 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 196R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=4.5 drift=-15.6% | 17:35:35 |
| S01_NAKAANA1 | 194R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=- drift=- | 16:42:25 |
| S00 | 194R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=10.0 drift=-60.0% | 16:42:24 |
| S01_NAKAANA1 | 243R | win | 1 | 0.3177 | 4.0 | 1.27 | 200 | scan=- drift=- | 16:20:47 |
| S00 | 192R | win | 1 | 0.5123 | 13.8 | 7.07 | 300 | scan=13.7 drift=+0.7% | 15:44:13 |
| S02_TETSUBAN | 052R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 10:55:37 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=2.7 drift=-11.1% | 08:59:12 |
| S01_NAKAANA1 | 1111R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.2 drift=-9.5% | 15:12:39 |
| S01_NAKAANA1 | 098R | win | 1 | 0.4989 | 4.0 | 2.00 | 200 | scan=4.7 drift=-14.9% | 13:56:47 |
| S01_NAKAANA1 | 105R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=4.3 drift=-30.2% | 10:33:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 21 | -8.0% | -66.8% | +17.6% | 7 | 3 | 11 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 414.2s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 322 | 0.4739 | 0.3261 | +0.1478 | 🟡+31% | 0.2291 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 128 | 0.4284 | 0.2891 | 0.2088 | 🔴-0.02 | 0.784 |
| S01_NAKAANA1 | win | 141 | 0.4858 | 0.3050 | 0.2356 | 🔴-0.11 | 0.743 |
| S02_TETSUBAN | win | 53 | 0.5522 | 0.4717 | 0.2606 | 🔴-0.05 | 1.089 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 7 | 0.2290 | 0.1429 | 🔴+0.0862 |
| 0.30-0.50 | 121 | 0.4141 | 0.2893 | 🔴+0.1248 |
| 0.50+ | 182 | 0.5442 | 0.3791 | 🔴+0.1651 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 203 | 0.805 |
| win | <5.0 | ✅learned | 370 | 0.741 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 48 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-11-11T20:00:01.910886+09:00_