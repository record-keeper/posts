# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-20T20:40:02.360720+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×38 (24h)
- 🔴 PSI_DRIFT_DETECTED×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×10  [2026-11-20T20:20:16]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×10  [2026-11-20T20:20:16]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-11-20T20:01:47]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-11-20T20:00:03]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-20T19:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-20T18:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-20T18:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-20T17:30:09]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-20T16:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-20T13:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×28  [2026-11-20T10:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=110<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-20T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2290 actual=0.0000 gap=+0.2290`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-20T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.0000 gap=+0.1918`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-20T06:00:12]
- key: `ROI_STAT|S00: n=92 hit%=22.8% hit_CI[Bonf]=[12.8,37.4]% ROI=0.62 ROI_boot95=[0.36,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=92<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-20T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=110 hit%=27.3% hit_CI[Bonf]=[16.9,40.8]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-20T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=41 hit%=41.5% hit_CI[Bonf]=[22.6,63.2]% ROI=1.02 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-20T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=41<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-20T06:00:12]
- key: `ORPHAN_SCAN|248 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.32MB / last modified 2026-11-20T20:39:14.298224+09:00

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
er: fetch_race 24/12: boats=6 odds=71/191
2026-11-20 20:36:52,965 [INFO] predictor: CALIBRATION_MODE=on
2026-11-20 20:36:52,965 [INFO] predictor: combos: {'win': 6, '2t': 30}
2026-11-20 20:36:52,967 [INFO] run_cycle: fetched 24/12 [final]: 36 combos
2026-11-20 20:36:53,262 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-20 20:37:04,702 [INFO] run_cycle: === run_cycle 20:37:04 ===
2026-11-20 20:37:04,702 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-20 20:37:04,702 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-20 20:37:04,769 [INFO] predictor: Models loaded OK
2026-11-20 20:37:35,241 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=12&jcd=15&hd=20261120: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-20 20:37:44,407 [INFO] scraper: odds3t: 120/120 parsed
2026-11-20 20:37:53,513 [INFO] scraper: odds3f: 20/20 parsed
2026-11-20 20:38:03,620 [INFO] scraper: odds2t: 30/30 parsed
2026-11-20 20:38:03,621 [INFO] scraper: odds2f: 15/15 parsed
2026-11-20 20:38:12,823 [INFO] scraper: odds_win: 6/6 parsed
2026-11-20 20:38:12,823 [INFO] scraper: fetch_race 15/12: boats=6 odds=191/191
2026-11-20 20:38:12,826 [INFO] predictor: CALIBRATION_MODE=on
2026-11-20 20:38:12,826 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-20 20:38:12,830 [INFO] run_cycle: fetched 15/12 [scan]: 156 combos
2026-11-20 20:38:12,957 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-20 20:39:04,689 [INFO] run_cycle: === run_cycle 20:39:04 ===
2026-11-20 20:39:04,689 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-20 20:39:04,689 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-20 20:39:04,752 [INFO] predictor: Models loaded OK
2026-11-20 20:39:04,888 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 11
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 11
  }
]
```

## Phase別通知記録 (24h)
{'final': 4, 'result': 2, 'scan': 5}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 271
  FINAL_MISSING: 38
  PSI_DRIFT_DETECTED: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 7 | 1 | 2,100 | 480 | -1,620 | 0.229 |
| S01_NAKAANA1 | 14 | 3 | 2,800 | 1,840 | -960 | 0.657 |
| S02_TETSUBAN | 6 | 4 | 1,200 | 1,600 | +400 | 1.333 |

## 直近アラート (24h・新しい順)
```
[20:39:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 413}
[20:36:53] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 409}
[20:32:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 406}
[20:32:22] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.2, "baseline_mean": 0.4, "baseline_stdev": 0.088, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": 2.27}
[20:27:02] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 408}
[20:24:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 405}
[20:23:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 404}
[20:21:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 402}
[20:20:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[20:20:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 403}
```

## 本日残レース: 1件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 119件 締切済
- 通知発射: scan=5 nid / final=4 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1410R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.8 drift=-25.0% | 12:53:02 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 12:08:26 |
| S01_NAKAANA1 | 0410R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.1 drift=+6.5% | 15:03:39 |
| S01_NAKAANA1 | 047R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=3.5 drift=-14.3% | 13:35:14 |
| S01_NAKAANA1 | 089R | win | 1 | 0.5220 | 3.3 | 1.72 | 200 | scan=3.1 drift=+6.5% | 14:22:25 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 200 | scan=- drift=- | 13:57:35 |
| S00 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 300 | scan=5.4 drift=-9.3% | 13:57:34 |
| S02_TETSUBAN | 118R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.9 drift=-10.3% | 13:55:17 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5874 | 3.1 | 1.82 | 200 | scan=- drift=- | 13:17:05 |
| S00 | 131R | win | 1 | 0.5334 | 17.6 | 9.39 | 300 | scan=17.6 drift=+0.0% | 10:42:37 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 13 | -0.0% | -26.8% | +55.6% | 6 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.7s |
| **Latency** (scan→final max) | 577.1s |
| **Traffic** (notifications 24h) | 11 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 231 | 0.4724 | 0.2727 | +0.1996 | 🟡+42% | 0.2305 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 86 | 0.4273 | 0.2209 | 0.2093 | 🔴-0.22 | 0.602 |
| S01_NAKAANA1 | win | 105 | 0.4797 | 0.2667 | 0.2338 | 🔴-0.20 | 0.693 |
| S02_TETSUBAN | win | 40 | 0.5500 | 0.4000 | 0.2674 | 🔴-0.11 | 0.973 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1918 | 0.0000 | 🔴+0.1918 |
| 0.30-0.50 | 94 | 0.4098 | 0.2447 | 🔴+0.1651 |
| 0.50+ | 126 | 0.5447 | 0.3175 | 🔴+0.2272 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 207 | 0.807 |
| win | <5.0 | ✅learned | 374 | 0.741 |
| win | <10.0 | ✅learned | 159 | 0.448 |
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
_auto-generated by claude_snapshot.py at 2026-11-20T20:40:02.360720+09:00_