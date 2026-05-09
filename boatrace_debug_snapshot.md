# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-09T13:10:02.298403+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×116 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🟡 LARGE_ODDS_DRIFT×4 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-05-09T13:03:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 PSI_DRIFT_DETECTED  ×7  [2026-05-09T13:03:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×10  [2026-05-09T13:00:43]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 ANOMALY_ML_PROB_SHIFT  ×12  [2026-05-09T12:58:27]
- key: `ANOMALY_ML_PROB_SHIFT|`
- **FIX**: predictions.ml_prob 分布が2σシフト。model drift / CAL_MODE 変更 / 計算バグ

### 🟡 ANOMALY_ODDS_SHIFT  ×12  [2026-05-09T12:58:27]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×27  [2026-05-09T09:25:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_DISPATCH_WARNING_REPEATED  ×2  [2026-05-09T05:30:03]
- key: `CODE_AUDIT_DISPATCH_WARNING_REPEATED|直近1時間で WARNING 3件`
- **FIX**: dispatch_pending が WARNING 連発。webhook 解決失敗。config_loader lazy dotenv 動作確認

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×2  [2026-05-09T05:12:26]
- key: `ROI_STAT|S00: n=139 hit%=25.9% hit_CI[Bonf]=[16.8,37.8]% ROI=0.89 ROI_boot95=[0.61,1.21]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×2  [2026-05-09T05:12:26]
- key: `INSUFFICIENT_SAMPLE|S00: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×2  [2026-05-09T05:12:26]
- key: `ORPHAN_SCAN|120 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×2  [2026-05-09T05:12:26]
- key: `DRIFT_BUCKET|drift ≤-30%: n=26 hit%=19.2% ROI=0.47 (コスト 7,800/回収 3,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×2  [2026-05-09T05:12:26]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=21 hit%=33.3% ROI=1.38 (コスト 6,300/回収 8,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|bt=win: n=139 pred=0.4290 actual=0.2590 error=+0.1700 (+40%) brier=0.2290 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|S00(win): n=139 pred=0.4290 hit=0.2590 cal_err=+0.1700 brier=0.2290 BSS=-0.19 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=13 pred=0.3316 actual=0.1538 gap=+0.1778`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=55 pred=0.4469 actual=0.2545 gap=+0.1923`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×2  [2026-05-09T05:12:26]
- key: `CALIBRATION_LIVE|decile 0.50+: n=51 pred=0.5318 actual=0.2941 gap=+0.2377`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-05-09T05:12:11]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `d3e97601d6febcc877a6fc9779762cac`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.05MB / last modified 2026-05-09T13:09:06.157318+09:00

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
arsed
2026-05-09 13:07:37,773 [INFO] scraper: odds2t: 30/30 parsed
2026-05-09 13:07:37,774 [INFO] scraper: odds2f: 15/15 parsed
2026-05-09 13:07:38,997 [INFO] scraper: odds_win: 4/6 parsed
2026-05-09 13:07:38,997 [INFO] scraper: fetch_race 11/6: boats=6 odds=189/191
2026-05-09 13:07:39,005 [INFO] predictor: CALIBRATION_MODE=on
2026-05-09 13:07:39,005 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-09 13:07:39,013 [INFO] run_cycle: fetched 11/6 [scan]: 154 combos
2026-05-09 13:07:42,725 [INFO] scraper: odds3t: 120/120 parsed
2026-05-09 13:07:43,861 [INFO] scraper: odds3f: 20/20 parsed
2026-05-09 13:07:44,958 [INFO] scraper: odds2t: 30/30 parsed
2026-05-09 13:07:44,959 [INFO] scraper: odds2f: 15/15 parsed
2026-05-09 13:07:46,379 [INFO] scraper: odds_win: 5/6 parsed
2026-05-09 13:07:46,379 [INFO] scraper: fetch_race 21/10: boats=6 odds=190/191
2026-05-09 13:07:46,388 [INFO] predictor: CALIBRATION_MODE=on
2026-05-09 13:07:46,390 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-09 13:07:46,396 [INFO] run_cycle: fetched 21/10 [scan]: 155 combos
2026-05-09 13:07:46,509 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 13:08:06,015 [INFO] run_cycle: === run_cycle 13:08:06 ===
2026-05-09 13:08:06,015 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 13:08:06,016 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 13:08:06,096 [INFO] predictor: Models loaded OK
2026-05-09 13:08:06,296 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 13:09:05,777 [INFO] run_cycle: === run_cycle 13:09:05 ===
2026-05-09 13:09:05,777 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 13:09:05,777 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 13:09:05,834 [INFO] predictor: Models loaded OK
2026-05-09 13:09:06,040 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01 | A | win | 1.5 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 7, 'scan': 45}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 116
  ANOMALY_SCRAPER_FAILURE_BURST: 35
  ANOMALY_SCAN_FINAL_RATIO: 34
  PSI_DRIFT_DETECTED: 26
  ANOMALY_ML_PROB_SHIFT: 6
  ANOMALY_ODDS_SHIFT: 6
  ANOMALY_BET_VOLUME_SPIKE: 5
  LARGE_ODDS_DRIFT: 4
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 16 | 15,000 | 15,840 | +840 | 1.056 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[13:07:46] FINAL_MISSING: {"deadline": "2026-05-09T10:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050921051036", "sid": "S04_SELL_3T"}
[13:06:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 90, "n_recent": 50, "psi": 0.489}
[13:06:32] FINAL_MISSING: {"deadline": "2026-05-09T11:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050921071135", "sid": "S04_SELL_3T"}
[13:06:32] FINAL_MISSING: {"deadline": "2026-05-09T10:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050913011034", "sid": "S04_SELL_3T"}
[13:05:22] FINAL_MISSING: {"deadline": "2026-05-09T08:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050918010832", "sid": "S04_SELL_3T"}
[13:04:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.455, "baseline_mean": 0.573, "baseline_stdev": 0.084, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.118, "today_scan_count": 34, "z_score": -5.43}
[13:03:05] FINAL_MISSING: {"deadline": "2026-05-09T12:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050922011233", "sid": "S04_SELL_3T"}
[13:03:05] FINAL_MISSING: {"deadline": "2026-05-09T09:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050914030932", "sid": "S04_SELL_3T"}
[13:01:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 89, "n_recent": 51, "psi": 0.483}
[13:01:36] ANOMALY_ODDS_SHIFT: {"baseline_mean": 9.57, "baseline_n": 62, "baseline_stdev": 8.34, "kind": "ANOMALY_ODDS_SHIFT", "today_mean": 48.85, "today_n": 13, "z_score": 4.71}
```

## 本日残レース: 80件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 52件 締切済
- 通知発射: scan=34 nid / final=4 nid / result=2 nid
- predictions: 13 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 34件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1410R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=6.2 drift=-33.9% | 13:01:32 |
| S04_SELL_3T | 212R | 3t | 1-4-2 | 0.0086 | 7.1 | 0.06 | 100 | scan=7.9 drift=-10.1% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-4-3 | 0.0052 | 16.0 | 0.08 | 100 | scan=14.8 drift=+8.1% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-4-6 | 0.0007 | 20.1 | 0.01 | 100 | scan=34.3 drift=-41.4% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-5-2 | 0.0002 | 63.9 | 0.01 | 100 | scan=47.8 drift=+33.7% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-5-3 | 0.0001 | 91.1 | 0.01 | 100 | scan=60.0 drift=+51.8% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-5-6 | 0.0000 | 106.0 | 0.00 | 100 | scan=122.1 drift=-13.2% | 09:11:21 |
| S04_SELL_3T | 182R | 3t | 1-4-6 | 0.0010 | 10.6 | 0.01 | 100 | scan=11.1 drift=-4.5% | 08:55:20 |
| S04_SELL_3T | 182R | 3t | 1-4-3 | 0.0010 | 28.4 | 0.03 | 100 | scan=26.3 drift=+8.0% | 08:55:20 |
| S04_SELL_3T | 182R | 3t | 1-5-6 | 0.0020 | 35.0 | 0.07 | 100 | scan=47.5 drift=-26.3% | 08:55:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 39 | -9.3% | -81.4% | +124.4% | 20 | 14 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 488.0s |
| **Latency** (scan→final max) | 599.7s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S04_SELL_3T) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 139 | 0.4290 | 0.2590 | +0.1700 | 🟡+40% | 0.2290 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 139 | 0.4290 | 0.2590 | 0.2290 | 🔴-0.19 | 0.887 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 6 | 0.1899 | 0.1667 | ✅+0.0232 |
| 0.20-0.30 | 9 | 0.2241 | 0.3333 | 🔴-0.1093 |
| 0.30-0.50 | 68 | 0.4248 | 0.2353 | 🔴+0.1895 |
| 0.50+ | 51 | 0.5318 | 0.2941 | 🔴+0.2377 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 6 | 0.35 |
| win | <10.0 | ✅learned | 22 | 0.564 |
| win | <20.0 | ⚠️fallback | 8 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-09T13:10:02.298403+09:00_