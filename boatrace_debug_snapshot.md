# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-16T12:00:01.952331+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-07-16T11:54:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-07-16T11:42:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-07-16T11:02:15]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×39  [2026-07-16T10:00:43]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-16T06:00:09]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-16T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=42.6% hit_CI[Bonf]=[27.1,59.8]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=68 pred=0.5440 hit=0.4265 cal_err=+0.1175 brier=0.2626 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S00: n=177 hit%=28.8% hit_CI[Bonf]=[20.1,39.4]% ROI=0.74 ROI_boot95=[0.55,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-16T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=156 hit%=30.8% hit_CI[Bonf]=[21.3,42.2]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.76 (コスト 11,300/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=32.2% ROI=0.83 (コスト 19,900/回収 16,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-16T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=31.4% ROI=0.62 (コスト 8,700/回収 5,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-16T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=401 pred=0.4696 actual=0.3192 error=+0.1504 (+32%) brier=0.2376 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.75MB / last modified 2026-07-16T12:00:03.196204+09:00

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
O] scraper: odds3t: 120/120 parsed
2026-07-16 11:59:17,869 [INFO] scraper: odds3f: 20/20 parsed
2026-07-16 11:59:19,011 [INFO] scraper: odds2t: 30/30 parsed
2026-07-16 11:59:19,012 [INFO] scraper: odds2f: 15/15 parsed
2026-07-16 11:59:20,285 [INFO] scraper: odds_win: 6/6 parsed
2026-07-16 11:59:20,285 [INFO] scraper: fetch_race 13/4: boats=6 odds=191/191
2026-07-16 11:59:20,289 [INFO] predictor: CALIBRATION_MODE=on
2026-07-16 11:59:20,289 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-16 11:59:20,293 [INFO] run_cycle: fetched 13/4 [final]: 156 combos
2026-07-16 11:59:23,992 [INFO] scraper: odds3t: 120/120 parsed
2026-07-16 11:59:25,120 [INFO] scraper: odds3f: 20/20 parsed
2026-07-16 11:59:26,248 [INFO] scraper: odds2t: 30/30 parsed
2026-07-16 11:59:26,250 [INFO] scraper: odds2f: 14/15 parsed
2026-07-16 11:59:27,396 [INFO] scraper: odds_win: 4/6 parsed
2026-07-16 11:59:27,396 [INFO] scraper: fetch_race 18/8: boats=6 odds=188/191
2026-07-16 11:59:27,399 [INFO] predictor: CALIBRATION_MODE=on
2026-07-16 11:59:27,399 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-16 11:59:27,403 [INFO] run_cycle: fetched 18/8 [final]: 154 combos
2026-07-16 11:59:30,973 [INFO] scraper: odds3t: 120/120 parsed
2026-07-16 11:59:32,153 [INFO] scraper: odds3f: 20/20 parsed
2026-07-16 11:59:33,371 [INFO] scraper: odds2t: 28/30 parsed
2026-07-16 11:59:33,372 [INFO] scraper: odds2f: 15/15 parsed
2026-07-16 11:59:34,446 [INFO] scraper: odds_win: 4/6 parsed
2026-07-16 11:59:34,446 [INFO] scraper: fetch_race 08/4: boats=6 odds=187/191
2026-07-16 11:59:34,449 [INFO] predictor: CALIBRATION_MODE=on
2026-07-16 11:59:34,449 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-07-16 11:59:34,454 [INFO] run_cycle: fetched 08/4 [scan]: 152 combos
2026-07-16 11:59:37,030 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=3
2026-07-16 11:59:37,030 [WARNING] run_cycle: fetch None: 03/3
2026-07-16 11:59:37,031 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 43
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 43
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 11, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 115
  FINAL_MISSING: 33
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 12
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_SCAN_FINAL_RATIO: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 16 | 14,400 | 14,070 | -330 | 0.977 |
| S01_NAKAANA1 | 38 | 12 | 7,600 | 6,340 | -1,260 | 0.834 |
| S02_TETSUBAN | 15 | 6 | 3,000 | 3,340 | +340 | 1.113 |

## 直近アラート (24h・新しい順)
```
[11:59:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1008}
[11:58:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 980}
[11:57:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 978}
[11:56:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 975}
[11:55:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 985}
[11:54:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 955}
[11:42:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.223, "baseline_mean": 0.777, "baseline_stdev": 0.095, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.35}
[11:02:14] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:39:32] CRITICAL_ODDS_COLLAPSE: {"combo": "1", "drift_pct": -32.2, "final": 6.1, "kind": "CRITICAL_ODDS_COLLAPSE", "race": "111R", "scan": 9.0, "sid": "S00"}
[10:02:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 114件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 30件 締切済
- 通知発射: scan=3 nid / final=5 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 200 | scan=3.7 drift=+21.6% | 11:42:20 |
| S00 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 300 | scan=- drift=- | 11:42:19 |
| S01_NAKAANA1 | 132R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 11:00:23 |
| S01_NAKAANA1 | 186R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=3.7 drift=+27.0% | 10:56:20 |
| S02_TETSUBAN | 216R | win | 1 | 0.5515 | 2.4 | 1.32 | 200 | scan=- drift=- | 10:45:19 |
| S00 | 111R | win | 1 | 0.5735 | 6.1 | 3.50 | 300 | scan=9.0 drift=-32.2% | 10:39:30 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5313 | 3.2 | 1.70 | 200 | scan=4.0 drift=-20.0% | 15:46:21 |
| S00 | 225R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=5.0 drift=-18.0% | 14:16:19 |
| S00 | 189R | win | 1 | 0.5735 | 5.0 | 2.87 | 300 | scan=- drift=- | 12:30:32 |
| S00 | 174R | win | 1 | 0.5079 | 4.5 | 2.29 | 300 | scan=- drift=- | 12:11:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +23.3% | -48.8% | +533.3% | 16 | 5 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 421.2s |
| **Latency** (scan→final max) | 599.7s |
| **Traffic** (notifications 24h) | 43 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4698 | 0.3192 | +0.1506 | 🟡+32% | 0.2384 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4290 | 0.2898 | 0.2268 | 🔴-0.10 | 0.745 |
| S01_NAKAANA1 | win | 157 | 0.4834 | 0.3057 | 0.2408 | 🔴-0.13 | 0.792 |
| S02_TETSUBAN | win | 68 | 0.5437 | 0.4265 | 0.2629 | 🔴-0.07 | 0.851 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2282 | 0.2000 | ✅+0.0282 |
| 0.30-0.50 | 148 | 0.4177 | 0.2838 | 🔴+0.1339 |
| 0.50+ | 223 | 0.5428 | 0.3498 | 🔴+0.1930 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 71 | 0.797 |
| win | <5.0 | ✅learned | 143 | 0.71 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-16T12:00:01.952331+09:00_