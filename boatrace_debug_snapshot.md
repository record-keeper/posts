# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-09T06:30:02.362359+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×63 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×63 (24h)
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 CALIBRATION_DRIFT×26 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=27.0% ROI=1.00 (コスト 8,400/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S00: n=152 hit%=24.3% hit_CI[Bonf]=[15.8,35.6]% ROI=0.75 ROI_boot95=[0.50,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=152<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=40.5% hit_CI[Bonf]=[26.6,56.1]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-09T06:00:17]
- key: `ORPHAN_SCAN|149 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=28.9% ROI=0.79 (コスト 11,200/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=21.6% ROI=0.49 (コスト 8,200/回収 4,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=27.1% ROI=0.53 (コスト 16,100/回収 8,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift ≥+30%: n=32 hit%=15.6% ROI=0.32 (コスト 8,700/回収 2,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|bt=win: n=380 pred=0.4691 actual=0.2921 error=+0.1770 (+38%) brier=0.2380 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|S00(win): n=152 pred=0.4226 hit=0.2434 cal_err=+0.1791 brier=0.2201 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=144 pred=0.4861 hit=0.2778 cal_err=+0.2084 brier=0.2431 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=84 pred=0.5239 hit=0.4048 cal_err=+0.1192 brier=0.2619 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=23 pred=0.3198 actual=0.2174 gap=+0.1024`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.7MB / last modified 2026-06-09T06:30:04.637325+09:00

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
27 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 23:55:06,827 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 23:55:06,870 [INFO] predictor: Models loaded OK
2026-06-08 23:55:06,876 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-08 23:56:06,178 [INFO] run_cycle: === run_cycle 23:56:06 ===
2026-06-08 23:56:06,178 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 23:56:06,178 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 23:56:06,223 [INFO] predictor: Models loaded OK
2026-06-08 23:56:06,227 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-08 23:57:06,295 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-08 23:57:06,295 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 23:57:06,295 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 23:57:06,358 [INFO] predictor: Models loaded OK
2026-06-08 23:57:06,364 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-08 23:58:06,476 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-08 23:58:06,476 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 23:58:06,476 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 23:58:06,520 [INFO] predictor: Models loaded OK
2026-06-08 23:58:06,524 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-08 23:59:06,166 [INFO] run_cycle: === run_cycle 23:59:06 ===
2026-06-08 23:59:06,166 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 23:59:06,167 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 23:59:06,239 [INFO] predictor: Models loaded OK
2026-06-08 23:59:06,249 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 8, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 220
  CIRCUIT_BREAKER_TRIP: 63
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 48
  CALIBRATION_DRIFT: 26
  PSI_DRIFT_DETECTED: 26
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 4 | 8,700 | 3,390 | -5,310 | 0.39 |
| S01_NAKAANA1 | 28 | 4 | 5,600 | 1,740 | -3,860 | 0.311 |
| S02_TETSUBAN | 24 | 6 | 4,800 | 1,720 | -3,080 | 0.358 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 4800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 24, "payout": 1720, "roi_7d": 0.358, "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 1740, "roi_7d": 0.311, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 3390, "roi_7d": 0.39, "sid": "S00"}
[06:00:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 299, "n_recent": 81, "psi": 0.336}
[06:00:04] CALIBRATION_DRIFT: {"avg_actual": 0.1728, "avg_pred": 0.4842, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 81, "overconf_pct": 64.3}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:46:06] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 1740, "roi_7d": 0.311, "sid": "S01_NAKAANA1"}
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
| S01_NAKAANA1 | 241R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.2 drift=-6.2% | 17:38:20 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 17:08:27 |
| S01_NAKAANA1 | 151R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=- drift=- | 15:22:21 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.5 drift=+4.0% | 15:10:24 |
| S00 | 065R | win | 1 | 0.1760 | 11.2 | 1.97 | 300 | scan=6.7 drift=+67.2% | 13:20:24 |
| S00 | 096R | win | 1 | 0.4989 | 5.0 | 2.49 | 300 | scan=- drift=- | 13:07:22 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5383 | 2.0 | 1.08 | 200 | scan=2.1 drift=-4.8% | 12:49:31 |
| S00 | 094R | win | 1 | 0.5476 | 14.2 | 7.78 | 300 | scan=6.7 drift=+111.9% | 12:05:38 |
| S01_NAKAANA1 | 0710R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=- drift=- | 19:47:21 |
| S02_TETSUBAN | 076R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 18:01:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 38 | +7.8% | -62.9% | +274.6% | 13 | 7 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 470.8s |
| **Latency** (scan→final max) | 601.0s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 380 | 0.4691 | 0.2921 | +0.1770 | 🟡+38% | 0.2380 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 152 | 0.4226 | 0.2434 | 0.2201 | 🔴-0.20 | 0.75 |
| S01_NAKAANA1 | win | 144 | 0.4861 | 0.2778 | 0.2431 | 🔴-0.21 | 0.699 |
| S02_TETSUBAN | win | 84 | 0.5239 | 0.4048 | 0.2619 | 🔴-0.09 | 0.723 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1918 | 0.2000 | ✅-0.0082 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 150 | 0.4215 | 0.2333 | 🔴+0.1882 |
| 0.50+ | 206 | 0.5418 | 0.3495 | 🔴+0.1923 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 34 | 0.743 |
| win | <5.0 | ✅learned | 61 | 0.738 |
| win | <10.0 | ✅learned | 40 | 0.525 |
| win | <20.0 | ✅learned | 12 | 0.197 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-09T06:30:02.362359+09:00_