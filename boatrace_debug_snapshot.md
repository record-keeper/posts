# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-03T06:50:01.294370+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×122 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×15 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-03T06:00:13]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=63<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-03T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=22 hit%=50.0% ROI=1.35 (コスト 6,400/回収 8,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S00: n=169 hit%=29.6% hit_CI[Bonf]=[20.6,40.5]% ROI=0.78 ROI_boot95=[0.58,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=173 hit%=32.9% hit_CI[Bonf]=[23.6,43.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-03T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=63 hit%=47.6% hit_CI[Bonf]=[30.8,65.0]% ROI=1.08 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=33.3% ROI=0.95 (コスト 9,100/回収 8,650)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=76 hit%=40.8% ROI=1.08 (コスト 17,400/回収 18,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=58 hit%=29.3% ROI=0.80 (コスト 14,000/回収 11,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-03T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=20.0% ROI=0.55 (コスト 10,500/回収 5,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=405 pred=0.4781 actual=0.3383 error=+0.1398 (+29%) brier=0.2367 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=169 pred=0.4396 hit=0.2959 cal_err=+0.1437 brier=0.2235 BSS=-0.07 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=173 pred=0.4883 hit=0.3295 cal_err=+0.1588 brier=0.2397 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=63 pred=0.5532 hit=0.4762 cal_err=+0.0770 brier=0.2641 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3214 actual=0.1818 gap=+0.1396`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-03T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=110 pred=0.4358 actual=0.3364 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.46MB / last modified 2026-11-03T06:30:04.164295+09:00

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
93 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 23:55:05,193 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 23:55:05,223 [INFO] predictor: Models loaded OK
2026-11-02 23:55:05,225 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-02 23:56:04,088 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-11-02 23:56:04,088 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 23:56:04,088 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 23:56:04,121 [INFO] predictor: Models loaded OK
2026-11-02 23:56:04,123 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-02 23:57:04,929 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-11-02 23:57:04,929 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 23:57:04,929 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 23:57:04,990 [INFO] predictor: Models loaded OK
2026-11-02 23:57:04,992 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-02 23:58:05,684 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-11-02 23:58:05,684 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 23:58:05,684 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 23:58:05,713 [INFO] predictor: Models loaded OK
2026-11-02 23:58:05,715 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-02 23:59:04,314 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-11-02 23:59:04,314 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 23:59:04,314 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 23:59:04,343 [INFO] predictor: Models loaded OK
2026-11-02 23:59:04,345 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 26
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 26
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 4, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 302
  FINAL_MISSING: 122
  ANOMALY_SCAN_FINAL_RATIO: 25
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 15
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 5 | 8,700 | 4,050 | -4,650 | 0.466 |
| S01_NAKAANA1 | 24 | 7 | 4,800 | 4,220 | -580 | 0.879 |
| S02_TETSUBAN | 11 | 2 | 2,200 | 3,220 | +1,020 | 1.464 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 4050, "roi_7d": 0.466, "sid": "S00"}
[06:00:05] CALIBRATION_DRIFT: {"avg_actual": 0.2188, "avg_pred": 0.4726, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 64, "overconf_pct": 53.7}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:58:05] CALIBRATION_DRIFT: {"avg_actual": 0.2188, "avg_pred": 0.4726, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 64, "overconf_pct": 53.7}
[23:58:05] FINAL_MISSING: {"deadline": "2026-11-02T14:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110217101418", "sid": "S00"}
[23:58:05] FINAL_MISSING: {"deadline": "2026-11-02T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110202021112", "sid": "S00"}
[23:58:05] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.283, "baseline_mean": 0.616, "baseline_stdev": 0.312, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 15, "z_score": -0.91}
[23:45:05] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 4050, "roi_7d": 0.466, "sid": "S00"}
[23:45:05] FINAL_MISSING: {"deadline": "2026-11-02T11:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110217031104", "sid": "S00"}
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
| S02_TETSUBAN | 0310R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 14:58:13 |
| S01_NAKAANA1 | 097R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.2 drift=+0.0% | 13:21:36 |
| S02_TETSUBAN | 036R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 13:08:13 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 11:47:38 |
| S02_TETSUBAN | 0711R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 20:05:24 |
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |
| S00 | 022R | win | 1 | 0.2290 | 5.7 | 1.31 | 300 | scan=- drift=- | 11:11:18 |
| S00 | 243R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 16:23:14 |
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 37 | +6.9% | -54.4% | +85.6% | 10 | 5 | 25 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 378.0s |
| **Latency** (scan→final max) | 531.5s |
| **Traffic** (notifications 24h) | 26 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 405 | 0.4781 | 0.3383 | +0.1398 | 🟡+29% | 0.2367 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4396 | 0.2959 | 0.2235 | 🔴-0.07 | 0.776 |
| S01_NAKAANA1 | win | 173 | 0.4883 | 0.3295 | 0.2397 | 🔴-0.08 | 0.809 |
| S02_TETSUBAN | win | 63 | 0.5532 | 0.4762 | 0.2641 | 🔴-0.06 | 1.081 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 143 | 0.4094 | 0.3007 | 🔴+0.1087 |
| 0.50+ | 240 | 0.5453 | 0.3833 | 🔴+0.1620 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 360 | 0.741 |
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
_auto-generated by claude_snapshot.py at 2026-11-03T06:50:01.294370+09:00_