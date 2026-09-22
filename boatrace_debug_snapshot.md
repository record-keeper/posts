# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-23T06:30:02.534024+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×49 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×49 (24h)
- 🟡 FINAL_MISSING×42 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=41.9% hit_CI[Bonf]=[27.0,58.4]% ROI=0.75 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-23T06:00:15]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.47 (コスト 10,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S00: n=163 hit%=22.7% hit_CI[Bonf]=[14.7,33.4]% ROI=0.72 ROI_boot95=[0.48,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=160 hit%=21.9% hit_CI[Bonf]=[14.0,32.6]% ROI=0.65 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=26.7% ROI=0.87 (コスト 8,500/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=20.0% ROI=0.58 (コスト 9,200/回収 5,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=22.9% ROI=0.70 (コスト 19,300/回収 13,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=13.2% ROI=0.48 (コスト 10,400/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|bt=win: n=397 pred=0.4757 actual=0.2594 error=+0.2163 (+45%) brier=0.2428 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|S00(win): n=163 pred=0.4398 hit=0.2270 cal_err=+0.2128 brier=0.2288 BSS=-0.30 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=160 pred=0.4850 hit=0.2188 cal_err=+0.2662 brier=0.2481 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=74 pred=0.5348 hit=0.4189 cal_err=+0.1159 brier=0.2621 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3235 actual=0.2258 gap=+0.0977`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=118 pred=0.4351 actual=0.2288 gap=+0.2063`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-23T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.50+: n=230 pred=0.5439 actual=0.2913 gap=+0.2525`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.86MB / last modified 2026-09-23T06:00:21.227231+09:00

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
31 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 23:55:04,931 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 23:55:04,997 [INFO] predictor: Models loaded OK
2026-09-22 23:55:05,002 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-22 23:56:04,864 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-09-22 23:56:04,864 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 23:56:04,864 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 23:56:04,910 [INFO] predictor: Models loaded OK
2026-09-22 23:56:04,916 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-22 23:57:04,698 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-09-22 23:57:04,698 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 23:57:04,698 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 23:57:04,728 [INFO] predictor: Models loaded OK
2026-09-22 23:57:04,730 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-22 23:58:04,807 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-09-22 23:58:04,807 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 23:58:04,807 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 23:58:04,874 [INFO] predictor: Models loaded OK
2026-09-22 23:58:04,881 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-22 23:59:04,549 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-09-22 23:59:04,549 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 23:59:04,549 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 23:59:04,593 [INFO] predictor: Models loaded OK
2026-09-22 23:59:04,597 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 51
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 51
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 12, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 79
  PSI_DRIFT_DETECTED: 49
  FINAL_MISSING: 42
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 5,340 | -5,160 | 0.509 |
| S01_NAKAANA1 | 36 | 10 | 7,200 | 6,580 | -620 | 0.914 |
| S02_TETSUBAN | 19 | 11 | 3,800 | 4,240 | +440 | 1.116 |

## 直近アラート (24h・新しい順)
```
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 5340, "roi_7d": 0.509, "sid": "S00"}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 307, "n_recent": 90, "psi": 0.441}
[06:00:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:51:04] FINAL_MISSING: {"deadline": "2026-09-22T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092202061314", "sid": "S00"}
[23:48:04] FINAL_MISSING: {"deadline": "2026-09-22T16:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092201031615", "sid": "S00"}
[23:37:04] FINAL_MISSING: {"deadline": "2026-09-22T13:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092211061301", "sid": "S00"}
[23:23:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 307, "n_recent": 90, "psi": 0.441}
[23:11:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:11:04] FINAL_MISSING: {"deadline": "2026-09-22T11:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092208031135", "sid": "S00"}
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
| S02_TETSUBAN | 207R | win | 1 | 0.4111 | 2.3 | 0.95 | 200 | scan=- drift=- | 17:50:32 |
| S02_TETSUBAN | 204R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.8 drift=-10.7% | 16:22:27 |
| S01_NAKAANA1 | 069R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=3.5 drift=+0.0% | 15:27:20 |
| S00 | 038R | win | 1 | 0.0568 | 9.0 | 0.51 | 300 | scan=7.7 drift=+16.9% | 14:21:30 |
| S00 | 168R | win | 1 | 0.5990 | 5.2 | 3.11 | 300 | scan=- drift=- | 14:19:20 |
| S00 | 067R | win | 1 | 0.4480 | 8.2 | 3.67 | 300 | scan=5.2 drift=+57.7% | 14:16:20 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.3177 | 3.6 | 1.14 | 200 | scan=3.1 drift=+16.1% | 12:51:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=3.5 drift=+8.6% | 11:58:20 |
| S02_TETSUBAN | 113R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=- drift=- | 11:27:18 |
| S01_NAKAANA1 | 107R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=3.5 drift=-8.6% | 11:16:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +1.3% | -81.7% | +119.5% | 16 | 6 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 405.5s |
| **Latency** (scan→final max) | 618.1s |
| **Traffic** (notifications 24h) | 51 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4757 | 0.2594 | +0.2163 | 🟡+46% | 0.2428 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4398 | 0.2270 | 0.2288 | 🔴-0.30 | 0.724 |
| S01_NAKAANA1 | win | 160 | 0.4850 | 0.2188 | 0.2481 | 🔴-0.45 | 0.645 |
| S02_TETSUBAN | win | 74 | 0.5348 | 0.4189 | 0.2621 | 🔴-0.08 | 0.753 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.30-0.50 | 149 | 0.4119 | 0.2282 | 🔴+0.1837 |
| 0.50+ | 230 | 0.5439 | 0.2913 | 🔴+0.2525 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 149 | 0.772 |
| win | <5.0 | ✅learned | 261 | 0.761 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-23T06:30:02.534024+09:00_