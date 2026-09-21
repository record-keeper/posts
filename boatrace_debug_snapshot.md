# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-22T06:20:01.874309+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×5 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ORPHAN_SCAN  ×1  [2026-09-22T06:00:18]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3233 actual=0.2121 gap=+0.1112`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S00: n=166 hit%=22.9% hit_CI[Bonf]=[14.9,33.5]% ROI=0.74 ROI_boot95=[0.50,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=21.4% hit_CI[Bonf]=[13.8,31.8]% ROI=0.64 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=40.3% hit_CI[Bonf]=[25.5,57.1]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=25.8% ROI=0.83 (コスト 8,900/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=19.5% ROI=0.57 (コスト 9,400/回収 5,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=82 hit%=22.0% ROI=0.70 (コスト 19,000/回収 13,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.47 (コスト 10,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift ≥+30%: n=39 hit%=12.8% ROI=0.47 (コスト 10,700/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|bt=win: n=406 pred=0.4763 actual=0.2537 error=+0.2226 (+47%) brier=0.2424 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|S00(win): n=166 pred=0.4421 hit=0.2289 cal_err=+0.2132 brier=0.2285 BSS=-0.29 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=168 pred=0.4835 hit=0.2143 cal_err=+0.2692 brier=0.2475 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=72 pred=0.5384 hit=0.4028 cal_err=+0.1356 brier=0.2624 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=120 pred=0.4336 actual=0.2167 gap=+0.2170`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.50+: n=236 pred=0.5432 actual=0.2881 gap=+0.2551`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-09-22T06:00:11]
- key: `PAYOUT_RATIO_WEIRD|pid=2504 bet=300 odds=4.5 payout=360 ratio=0.27`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.82MB / last modified 2026-09-22T06:00:26.043579+09:00

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
23 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-21 23:55:04,423 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-21 23:55:04,459 [INFO] predictor: Models loaded OK
2026-09-21 23:55:04,461 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-21 23:56:03,896 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-21 23:56:03,896 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-21 23:56:03,897 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-21 23:56:03,945 [INFO] predictor: Models loaded OK
2026-09-21 23:56:03,951 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-21 23:57:04,077 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-09-21 23:57:04,077 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-21 23:57:04,077 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-21 23:57:04,112 [INFO] predictor: Models loaded OK
2026-09-21 23:57:04,114 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-21 23:58:04,132 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-09-21 23:58:04,133 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-21 23:58:04,133 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-21 23:58:04,162 [INFO] predictor: Models loaded OK
2026-09-21 23:58:04,164 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-21 23:59:04,291 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-09-21 23:59:04,291 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-21 23:59:04,291 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-21 23:59:04,339 [INFO] predictor: Models loaded OK
2026-09-21 23:59:04,343 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 19, 'result': 9, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 69
  PSI_DRIFT_DETECTED: 38
  ANOMALY_SCAN_FINAL_RATIO: 19
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 5
  ANOMALY_BET_VOLUME_DROP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 10 | 11,700 | 8,190 | -3,510 | 0.7 |
| S01_NAKAANA1 | 34 | 10 | 6,800 | 7,140 | +340 | 1.05 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,520 | +120 | 1.035 |

## 直近アラート (24h・新しい順)
```
[06:00:08] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:08] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 90, "psi": 0.432}
[06:00:08] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:47:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 90, "psi": 0.432}
[23:23:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.202, "baseline_mean": 0.798, "baseline_stdev": 0.083, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 15, "z_score": 2.43}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[22:46:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 90, "psi": 0.432}
[22:23:03] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.202, "baseline_mean": 0.798, "baseline_stdev": 0.083, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 15, "z_score": 2.43}
[22:08:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S01_NAKAANA1 | 155R | win | 1 | 0.5719 | 3.1 | 1.77 | 200 | scan=3.4 drift=-8.8% | 17:07:31 |
| S02_TETSUBAN | 169R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=- drift=- | 15:02:19 |
| S00 | 179R | win | 1 | 0.4111 | 11.1 | 4.56 | 300 | scan=- drift=- | 14:44:31 |
| S01_NAKAANA1 | 166R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 13:21:31 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=4.0 drift=-25.0% | 12:22:21 |
| S02_TETSUBAN | 164R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=- drift=- | 12:20:21 |
| S01_NAKAANA1 | 062R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.0 drift=+40.0% | 11:50:33 |
| S00 | 173R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=10.0 drift=-44.0% | 11:34:19 |
| S01_NAKAANA1 | 093R | win | 1 | 0.5174 | 3.8 | 1.97 | 200 | scan=4.5 drift=-15.6% | 11:29:18 |
| S01_NAKAANA1 | 243R | win | 1 | 0.4989 | 3.4 | 1.70 | 200 | scan=4.8 drift=-29.2% | 18:31:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | -0.7% | -81.7% | +119.5% | 16 | 6 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 509.5s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 43 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 406 | 0.4763 | 0.2537 | +0.2226 | 🟡+47% | 0.2424 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4421 | 0.2289 | 0.2285 | 🔴-0.29 | 0.736 |
| S01_NAKAANA1 | win | 168 | 0.4835 | 0.2143 | 0.2475 | 🔴-0.47 | 0.642 |
| S02_TETSUBAN | win | 72 | 0.5384 | 0.4028 | 0.2624 | 🔴-0.09 | 0.724 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 153 | 0.4098 | 0.2157 | 🔴+0.1941 |
| 0.50+ | 236 | 0.5432 | 0.2881 | 🔴+0.2551 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 147 | 0.772 |
| win | <5.0 | ✅learned | 260 | 0.762 |
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
_auto-generated by claude_snapshot.py at 2026-09-22T06:20:01.874309+09:00_