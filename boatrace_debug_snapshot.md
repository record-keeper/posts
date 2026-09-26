# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-27T06:10:01.200876+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×38 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-27T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-27T06:00:13]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-27T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-27T06:00:13]
- key: `ROI_STAT|S00: n=161 hit%=22.4% hit_CI[Bonf]=[14.4,33.1]% ROI=0.67 ROI_boot95=[0.44,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-27T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=152 hit%=21.7% hit_CI[Bonf]=[13.7,32.7]% ROI=0.66 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-27T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=152<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-27T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=46.2% hit_CI[Bonf]=[31.3,61.9]% ROI=0.85 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-27T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=32.1% ROI=0.94 (コスト 7,900/回収 7,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-27T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=25.0% ROI=0.70 (コスト 8,900/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-27T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=24.1% ROI=0.72 (コスト 20,200/回収 14,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-27T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=38 hit%=26.3% ROI=0.53 (コスト 8,400/回収 4,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-27T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=9.5% ROI=0.26 (コスト 11,600/回収 3,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=393 pred=0.4780 actual=0.2697 error=+0.2083 (+44%) brier=0.2464 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=161 pred=0.4443 hit=0.2236 cal_err=+0.2207 brier=0.2360 BSS=-0.36 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=152 pred=0.4882 hit=0.2171 cal_err=+0.2711 brier=0.2516 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=80 pred=0.5263 hit=0.4625 cal_err=+0.0638 brier=0.2576 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3235 actual=0.2188 gap=+0.1048`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=117 pred=0.4376 actual=0.2479 gap=+0.1897`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-27T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.50+: n=228 pred=0.5448 actual=0.2939 gap=+0.2509`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-09-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=2542 bet=200 odds=2.6 payout=640 ratio=1.23`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.2MB / last modified 2026-09-27T06:00:22.340785+09:00

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
39 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-26 23:55:04,639 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-26 23:55:04,694 [INFO] predictor: Models loaded OK
2026-09-26 23:55:04,700 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-26 23:56:03,963 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-26 23:56:03,963 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-26 23:56:03,963 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-26 23:56:04,010 [INFO] predictor: Models loaded OK
2026-09-26 23:56:04,016 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-26 23:57:04,161 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-09-26 23:57:04,161 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-26 23:57:04,161 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-26 23:57:04,206 [INFO] predictor: Models loaded OK
2026-09-26 23:57:04,210 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-26 23:58:03,643 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-09-26 23:58:03,643 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-26 23:58:03,643 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-26 23:58:03,689 [INFO] predictor: Models loaded OK
2026-09-26 23:58:03,693 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-26 23:59:03,407 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-09-26 23:59:03,407 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-26 23:59:03,408 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-26 23:59:03,459 [INFO] predictor: Models loaded OK
2026-09-26 23:59:03,463 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 10, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 223
  FINAL_MISSING: 38
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 5 | 9,600 | 3,660 | -5,940 | 0.381 |
| S01_NAKAANA1 | 34 | 10 | 6,800 | 5,080 | -1,720 | 0.747 |
| S02_TETSUBAN | 22 | 12 | 4,400 | 4,580 | +180 | 1.041 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3660, "roi_7d": 0.381, "sid": "S00"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:43:03] FINAL_MISSING: {"deadline": "2026-09-26T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092603031208", "sid": "S00"}
[23:28:04] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 3660, "roi_7d": 0.381, "sid": "S00"}
[23:24:03] FINAL_MISSING: {"deadline": "2026-09-26T16:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092622111650", "sid": "S00"}
[23:19:04] FINAL_MISSING: {"deadline": "2026-09-26T16:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092619041644", "sid": "S00"}
[23:07:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:07:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
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
| S01_NAKAANA1 | 153R | win | 1 | 0.5476 | 4.8 | 2.63 | 200 | scan=3.1 drift=+54.8% | 16:05:30 |
| S02_TETSUBAN | 118R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 14:01:29 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=3.5 drift=+2.9% | 12:53:20 |
| S00 | 054R | win | 1 | 0.3229 | 19.2 | 6.20 | 300 | scan=4.2 drift=+357.1% | 12:30:23 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=4.8 drift=-27.1% | 12:11:20 |
| S01_NAKAANA1 | 218R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.7 drift=+0.0% | 12:04:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 11:46:30 |
| S00 | 083R | win | 1 | 0.5334 | 4.1 | 2.19 | 300 | scan=10.5 drift=-61.0% | 11:30:22 |
| S01_NAKAANA1 | 092R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=- drift=- | 10:59:30 |
| S02_TETSUBAN | 213R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.6 drift=-15.4% | 09:33:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +4.8% | -72.2% | +357.1% | 21 | 7 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 459.3s |
| **Latency** (scan→final max) | 640.9s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 393 | 0.4780 | 0.2697 | +0.2083 | 🟡+44% | 0.2464 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 161 | 0.4443 | 0.2236 | 0.2360 | 🔴-0.36 | 0.671 |
| S01_NAKAANA1 | win | 152 | 0.4882 | 0.2171 | 0.2516 | 🔴-0.48 | 0.657 |
| S02_TETSUBAN | win | 80 | 0.5263 | 0.4625 | 0.2576 | 🔴-0.04 | 0.848 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 149 | 0.4131 | 0.2416 | 🔴+0.1715 |
| 0.50+ | 228 | 0.5448 | 0.2939 | 🔴+0.2509 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 157 | 0.78 |
| win | <5.0 | ✅learned | 270 | 0.755 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-27T06:10:01.200876+09:00_