# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-28T10:50:01.996297+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×56 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-08-28T10:45:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×48  [2026-08-28T10:02:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×96  [2026-08-28T10:02:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-08-28T10:02:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-08-28T10:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-28T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-28T10:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S00: n=174 hit%=27.6% hit_CI[Bonf]=[19.0,38.2]% ROI=0.88 ROI_boot95=[0.63,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=25.8% hit_CI[Bonf]=[17.8,35.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=39.7% hit_CI[Bonf]=[25.5,56.0]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-28T06:00:10]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=40 hit%=20.0% ROI=0.62 (コスト 11,600/回収 7,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=32.6% ROI=0.96 (コスト 10,100/回収 9,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=29.0% ROI=0.96 (コスト 21,200/回収 20,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.66MB / last modified 2026-08-28T10:49:05.571352+09:00

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
2026-08-28 10:48:19,697 [INFO] scraper: fetch_race 09/2: boats=6 odds=184/191
2026-08-28 10:48:19,700 [INFO] predictor: CALIBRATION_MODE=on
2026-08-28 10:48:19,700 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-28 10:48:19,751 [INFO] run_cycle: fetched 09/2 [scan]: 153 combos
2026-08-28 10:48:23,230 [INFO] scraper: odds3t: 120/120 parsed
2026-08-28 10:48:24,318 [INFO] scraper: odds3f: 20/20 parsed
2026-08-28 10:48:25,409 [INFO] scraper: odds2t: 27/30 parsed
2026-08-28 10:48:25,411 [INFO] scraper: odds2f: 13/15 parsed
2026-08-28 10:48:26,489 [INFO] scraper: odds_win: 3/6 parsed
2026-08-28 10:48:26,489 [INFO] scraper: fetch_race 13/2: boats=6 odds=183/191
2026-08-28 10:48:26,491 [INFO] predictor: CALIBRATION_MODE=on
2026-08-28 10:48:26,491 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-08-28 10:48:26,495 [INFO] run_cycle: fetched 13/2 [scan]: 150 combos
2026-08-28 10:48:30,046 [INFO] scraper: odds3t: 120/120 parsed
2026-08-28 10:48:31,134 [INFO] scraper: odds3f: 20/20 parsed
2026-08-28 10:48:32,219 [INFO] scraper: odds2t: 29/30 parsed
2026-08-28 10:48:32,220 [INFO] scraper: odds2f: 11/15 parsed
2026-08-28 10:48:33,606 [INFO] scraper: odds_win: 3/6 parsed
2026-08-28 10:48:33,606 [INFO] scraper: fetch_race 11/2: boats=6 odds=183/191
2026-08-28 10:48:33,609 [INFO] predictor: CALIBRATION_MODE=on
2026-08-28 10:48:33,609 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-08-28 10:48:33,613 [INFO] run_cycle: fetched 11/2 [scan]: 152 combos
2026-08-28 10:48:33,763 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 10:49:04,810 [INFO] run_cycle: === run_cycle 10:49:04 ===
2026-08-28 10:49:04,810 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 10:49:04,811 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 10:49:04,841 [INFO] predictor: Models loaded OK
2026-08-28 10:49:05,297 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 20, 'scan': 23}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 56
  CIRCUIT_BREAKER_NO_ACTION: 45
  CIRCUIT_BREAKER_TRIP: 35
  ANOMALY_SCRAPER_FAILURE_BURST: 23
  ANOMALY_SCAN_FINAL_RATIO: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 10 | 13,200 | 9,510 | -3,690 | 0.72 |
| S01_NAKAANA1 | 49 | 12 | 9,800 | 5,920 | -3,880 | 0.604 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 2,420 | -980 | 0.712 |

## 直近アラート (24h・新しい順)
```
[10:46:42] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.133, "baseline_mean": 0.799, "baseline_stdev": 0.047, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.83}
[10:45:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.466, "baseline_mean": 0.799, "baseline_stdev": 0.047, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -9.94}
[10:02:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 5920, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[10:02:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:02:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:00:40] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.9, "baseline_n_days": 7, "baseline_stdev": 0.7, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.69}
[09:01:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:44] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 5920, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[09:01:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 124件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 20件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 131R | win | 1 | 0.3197 | 7.0 | 2.24 | 300 | scan=26.2 drift=-73.3% | 10:33:30 |
| S02_TETSUBAN | 078R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.2 drift=-9.1% | 18:33:18 |
| S00 | 073R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=6.5 drift=+46.2% | 16:08:30 |
| S01_NAKAANA1 | 228R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 15:46:18 |
| S01_NAKAANA1 | 071R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.0 drift=+53.3% | 15:17:19 |
| S01_NAKAANA1 | 227R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.0 drift=+23.3% | 15:13:20 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 15:01:18 |
| S00 | 179R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=25.5 drift=-54.9% | 14:51:18 |
| S00 | 178R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=18.0 drift=-66.7% | 14:23:30 |
| S00 | 118R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 13:58:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +1.3% | -79.6% | +320.7% | 24 | 12 | 49 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.1s |
| **Latency** (scan→final max) | 606.7s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 442 | 0.4711 | 0.2896 | +0.1815 | 🟡+38% | 0.2388 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4174 | 0.2759 | 0.2196 | 🔴-0.10 | 0.881 |
| S01_NAKAANA1 | win | 190 | 0.4904 | 0.2579 | 0.2486 | 🔴-0.30 | 0.806 |
| S02_TETSUBAN | win | 78 | 0.5438 | 0.3974 | 0.2576 | 🔴-0.08 | 0.651 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 11 | 0.1807 | 0.1818 | ✅-0.0012 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 156 | 0.4137 | 0.2308 | 🔴+0.1829 |
| 0.50+ | 253 | 0.5455 | 0.3399 | 🔴+0.2056 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 120 | 0.775 |
| win | <5.0 | ✅learned | 224 | 0.746 |
| win | <10.0 | ✅learned | 107 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-28T10:50:01.996297+09:00_