# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-11T07:10:01.735670+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×30 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×102 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×30 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×13 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T07:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T07:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-11T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1835 actual=0.1818 gap=+0.0017`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.67 ROI_boot95=[0.46,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=23.3% hit_CI[Bonf]=[15.2,34.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.82 (コスト 8,600/回収 7,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=25.0% ROI=0.68 (コスト 15,100/回収 10,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=24.0% ROI=0.49 (コスト 11,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=24.3% ROI=0.94 (コスト 10,200/回収 9,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=401 pred=0.4632 actual=0.2768 error=+0.1864 (+40%) brier=0.2369 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=171 pred=0.4160 hit=0.2281 cal_err=+0.1879 brier=0.2283 BSS=-0.30 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=163 pred=0.4838 hit=0.2331 cal_err=+0.2507 brier=0.2437 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=67 pred=0.5337 hit=0.5075 cal_err=+0.0263 brier=0.2427 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.05MB / last modified 2026-08-11T07:00:03.482148+09:00

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
92 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 23:55:04,092 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 23:55:04,124 [INFO] predictor: Models loaded OK
2026-08-10 23:55:04,127 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 23:56:04,158 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-10 23:56:04,158 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 23:56:04,158 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 23:56:04,206 [INFO] predictor: Models loaded OK
2026-08-10 23:56:04,210 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 23:57:04,222 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-08-10 23:57:04,222 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 23:57:04,223 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 23:57:04,270 [INFO] predictor: Models loaded OK
2026-08-10 23:57:04,274 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 23:58:04,394 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-08-10 23:58:04,394 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 23:58:04,394 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 23:58:04,426 [INFO] predictor: Models loaded OK
2026-08-10 23:58:04,428 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 23:59:04,280 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-08-10 23:59:04,280 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 23:59:04,280 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 23:59:04,323 [INFO] predictor: Models loaded OK
2026-08-10 23:59:04,325 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 14, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 117
  FINAL_MISSING: 102
  ANOMALY_SCAN_FINAL_RATIO: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 30
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 13
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 8 | 10,800 | 8,070 | -2,730 | 0.747 |
| S01_NAKAANA1 | 42 | 9 | 8,400 | 5,200 | -3,200 | 0.619 |
| S02_TETSUBAN | 13 | 8 | 2,600 | 2,280 | -320 | 0.877 |

## 直近アラート (24h・新しい順)
```
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 5200, "roi_7d": 0.619, "sid": "S01_NAKAANA1"}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:43:04] FINAL_MISSING: {"deadline": "2026-08-10T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081003031208", "sid": "S00"}
[23:40:05] FINAL_MISSING: {"deadline": "2026-08-10T16:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081015031606", "sid": "S00"}
[23:37:04] FINAL_MISSING: {"deadline": "2026-08-10T12:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081008041200", "sid": "S00"}
[23:33:04] FINAL_MISSING: {"deadline": "2026-08-10T13:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081013081354", "sid": "S00"}
[23:33:04] FINAL_MISSING: {"deadline": "2026-08-10T12:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081013061253", "sid": "S00"}
[23:33:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.143, "baseline_mean": 0.809, "baseline_stdev": 0.049, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 27, "z_score": -2.89}
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
| S00 | 248R | win | 1 | 0.2290 | 6.5 | 1.49 | 300 | scan=- drift=- | 18:30:35 |
| S00 | 207R | win | 1 | 0.5277 | 22.8 | 12.03 | 300 | scan=- drift=- | 18:10:32 |
| S00 | 152R | win | 1 | 0.4989 | 11.2 | 5.59 | 300 | scan=10.1 drift=+10.9% | 15:38:26 |
| S02_TETSUBAN | 058R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=- drift=- | 15:04:26 |
| S02_TETSUBAN | 098R | win | 1 | 0.5891 | 2.9 | 1.71 | 200 | scan=2.5 drift=+16.0% | 13:58:18 |
| S00 | 239R | win | 1 | 0.4111 | 22.1 | 9.09 | 300 | scan=5.7 drift=+287.7% | 12:44:20 |
| S01_NAKAANA1 | 053R | win | 1 | 0.4988 | 3.6 | 1.80 | 200 | scan=- drift=- | 12:31:20 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.5 drift=-4.4% | 11:51:19 |
| S00 | 237R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 11:43:18 |
| S01_NAKAANA1 | 237R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.3 drift=+18.2% | 11:42:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +6.2% | -73.3% | +287.7% | 17 | 8 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 520.3s |
| **Latency** (scan→final max) | 631.3s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4632 | 0.2768 | +0.1864 | 🟡+40% | 0.2369 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4160 | 0.2281 | 0.2283 | 🔴-0.30 | 0.67 |
| S01_NAKAANA1 | win | 163 | 0.4838 | 0.2331 | 0.2437 | 🔴-0.36 | 0.703 |
| S02_TETSUBAN | win | 67 | 0.5337 | 0.5075 | 0.2427 | ✅+0.03 | 0.867 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 10 | 0.2236 | 0.4000 | 🔴-0.1764 |
| 0.30-0.50 | 155 | 0.4176 | 0.2129 | 🔴+0.2047 |
| 0.50+ | 212 | 0.5436 | 0.3302 | 🔴+0.2134 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 103 | 0.776 |
| win | <5.0 | ✅learned | 178 | 0.727 |
| win | <10.0 | ✅learned | 91 | 0.451 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-11T07:10:01.735670+09:00_