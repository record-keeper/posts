# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-28T06:10:01.258425+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×32 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×56 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

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

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=53 hit%=26.4% ROI=0.52 (コスト 12,100/回収 6,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=23.7% ROI=1.15 (コスト 10,300/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=442 pred=0.4711 actual=0.2896 error=+0.1815 (+39%) brier=0.2388 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|S00(win): n=174 pred=0.4174 hit=0.2759 cal_err=+0.1415 brier=0.2196 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=190 pred=0.4904 hit=0.2579 cal_err=+0.2325 brier=0.2486 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=78 pred=0.5438 hit=0.3974 cal_err=+0.1463 brier=0.2576 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3202 actual=0.3235 gap=-0.0034`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.64MB / last modified 2026-08-28T06:00:20.500252+09:00

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
53 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 23:55:04,153 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 23:55:04,201 [INFO] predictor: Models loaded OK
2026-08-27 23:55:04,205 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 23:56:04,256 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-27 23:56:04,256 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 23:56:04,256 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 23:56:04,291 [INFO] predictor: Models loaded OK
2026-08-27 23:56:04,294 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 23:57:04,452 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-08-27 23:57:04,452 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 23:57:04,452 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 23:57:04,502 [INFO] predictor: Models loaded OK
2026-08-27 23:57:04,506 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 23:58:03,744 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-08-27 23:58:03,744 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 23:58:03,744 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 23:58:03,795 [INFO] predictor: Models loaded OK
2026-08-27 23:58:03,799 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 23:59:03,834 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-08-27 23:59:03,834 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 23:59:03,834 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 23:59:03,883 [INFO] predictor: Models loaded OK
2026-08-27 23:59:03,887 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 20, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 56
  ANOMALY_SCRAPER_FAILURE_BURST: 46
  CIRCUIT_BREAKER_NO_ACTION: 42
  CIRCUIT_BREAKER_TRIP: 32
  ANOMALY_SCAN_FINAL_RATIO: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 11 | 13,200 | 10,260 | -2,940 | 0.777 |
| S01_NAKAANA1 | 49 | 12 | 9,800 | 5,920 | -3,880 | 0.604 |
| S02_TETSUBAN | 18 | 6 | 3,600 | 2,420 | -1,180 | 0.672 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 5920, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-08-27T13:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082704041316", "sid": "S00"}
[23:48:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:36:03] FINAL_MISSING: {"deadline": "2026-08-27T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082709021058", "sid": "S00"}
[23:19:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 5920, "roi_7d": 0.604, "sid": "S01_NAKAANA1"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
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
| S02_TETSUBAN | 078R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.2 drift=-9.1% | 18:33:18 |
| S00 | 073R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=6.5 drift=+46.2% | 16:08:30 |
| S01_NAKAANA1 | 228R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 15:46:18 |
| S01_NAKAANA1 | 071R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.0 drift=+53.3% | 15:17:19 |
| S01_NAKAANA1 | 227R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.0 drift=+23.3% | 15:13:20 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 15:01:18 |
| S00 | 179R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=25.5 drift=-54.9% | 14:51:18 |
| S00 | 178R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=18.0 drift=-66.7% | 14:23:30 |
| S00 | 118R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 13:58:20 |
| S00 | 1411R | win | 1 | 0.5719 | 4.0 | 2.29 | 300 | scan=4.5 drift=-11.1% | 13:30:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +2.5% | -79.6% | +320.7% | 23 | 11 | 48 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.3s |
| **Latency** (scan→final max) | 614.1s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |

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
_auto-generated by claude_snapshot.py at 2026-08-28T06:10:01.258425+09:00_