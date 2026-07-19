# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-20T06:10:01.340334+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×58 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×170 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×58 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-20T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-20T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-20T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=27.3% ROI=0.54 (コスト 8,000/回収 4,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-07-20T06:00:07]
- key: `ROI_STAT|S00: n=192 hit%=27.1% hit_CI[Bonf]=[18.9,37.2]% ROI=0.68 ROI_boot95=[0.51,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-20T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=192<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-20T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=28.9% hit_CI[Bonf]=[20.0,39.9]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-20T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=45.8% hit_CI[Bonf]=[30.2,62.3]% ROI=0.95 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-20T06:00:07]
- key: `ORPHAN_SCAN|168 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-20T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=25.0% ROI=0.61 (コスト 9,300/回収 5,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-20T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=34.0% ROI=0.82 (コスト 12,400/回収 10,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-20T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=33.0% ROI=0.78 (コスト 20,300/回収 15,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-20T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.45 (コスト 10,700/回収 4,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=430 pred=0.4673 actual=0.3093 error=+0.1580 (+34%) brier=0.2370 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=192 pred=0.4291 hit=0.2708 cal_err=+0.1582 brier=0.2291 BSS=-0.16 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=166 pred=0.4799 hit=0.2892 cal_err=+0.1908 brier=0.2377 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=72 pred=0.5402 hit=0.4583 cal_err=+0.0818 brier=0.2564 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1762 actual=0.5000 gap=-0.3238`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3243 actual=0.0857 gap=+0.2386`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-20T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=130 pred=0.4406 actual=0.3077 gap=+0.1329`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.18MB / last modified 2026-07-20T06:00:10.208732+09:00

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
04 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 23:55:04,404 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 23:55:04,432 [INFO] predictor: Models loaded OK
2026-07-19 23:55:04,434 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-19 23:56:04,273 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-07-19 23:56:04,273 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 23:56:04,273 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 23:56:04,300 [INFO] predictor: Models loaded OK
2026-07-19 23:56:04,302 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-19 23:57:04,135 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-07-19 23:57:04,135 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 23:57:04,135 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 23:57:04,178 [INFO] predictor: Models loaded OK
2026-07-19 23:57:04,182 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-19 23:58:04,006 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-07-19 23:58:04,006 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 23:58:04,006 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 23:58:04,050 [INFO] predictor: Models loaded OK
2026-07-19 23:58:04,054 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-19 23:59:03,277 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-07-19 23:59:03,277 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-19 23:59:03,277 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-19 23:59:03,323 [INFO] predictor: Models loaded OK
2026-07-19 23:59:03,325 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 97
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 97
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 20, 'scan': 41}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 229
  FINAL_MISSING: 170
  CIRCUIT_BREAKER_TRIP: 58
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 27
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 6
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 8 | 12,900 | 5,910 | -6,990 | 0.458 |
| S01_NAKAANA1 | 41 | 10 | 8,200 | 5,660 | -2,540 | 0.69 |
| S02_TETSUBAN | 16 | 7 | 3,200 | 2,980 | -220 | 0.931 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5660, "roi_7d": 0.69, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 5910, "roi_7d": 0.458, "sid": "S00"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:58:04] FINAL_MISSING: {"deadline": "2026-07-19T13:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071911061323", "sid": "S00"}
[23:56:04] FINAL_MISSING: {"deadline": "2026-07-19T13:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071916041320", "sid": "S00"}
[23:54:03] FINAL_MISSING: {"deadline": "2026-07-19T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071902021116", "sid": "S00"}
[23:51:03] FINAL_MISSING: {"deadline": "2026-07-19T15:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071909101516", "sid": "S00"}
[23:51:03] FINAL_MISSING: {"deadline": "2026-07-19T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071902041214", "sid": "S00"}
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
| S00 | 197R | win | 1 | 0.5123 | 5.9 | 3.02 | 300 | scan=7.1 drift=-16.9% | 18:30:21 |
| S00 | 1610R | win | 1 | 0.5174 | 7.1 | 3.67 | 300 | scan=7.0 drift=+1.4% | 16:43:18 |
| S00 | 203R | win | 1 | 0.5735 | 16.1 | 9.23 | 300 | scan=20.2 drift=-20.3% | 16:36:18 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=3.7 drift=-18.9% | 16:02:43 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=- drift=- | 15:50:31 |
| S00 | 0210R | win | 1 | 0.5174 | 7.0 | 3.62 | 300 | scan=7.7 drift=-9.1% | 15:18:25 |
| S01_NAKAANA1 | 227R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:10:31 |
| S01_NAKAANA1 | 029R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=- drift=- | 14:45:19 |
| S00 | 165R | win | 1 | 0.5123 | 14.0 | 7.17 | 300 | scan=5.2 drift=+169.2% | 13:50:44 |
| S00 | 1011R | win | 1 | 0.4111 | 32.8 | 13.48 | 300 | scan=4.5 drift=+628.9% | 13:26:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +20.9% | -64.6% | +628.9% | 17 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 473.9s |
| **Latency** (scan→final max) | 610.7s |
| **Traffic** (notifications 24h) | 97 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4673 | 0.3093 | +0.1580 | 🟡+34% | 0.2370 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 192 | 0.4291 | 0.2708 | 0.2291 | 🔴-0.16 | 0.685 |
| S01_NAKAANA1 | win | 166 | 0.4799 | 0.2892 | 0.2377 | 🔴-0.16 | 0.758 |
| S02_TETSUBAN | win | 72 | 0.5402 | 0.4583 | 0.2564 | 🔴-0.03 | 0.947 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1762 | 0.5000 | 🔴-0.3238 |
| 0.20-0.30 | 15 | 0.2268 | 0.2667 | ✅-0.0399 |
| 0.30-0.50 | 165 | 0.4159 | 0.2606 | 🔴+0.1553 |
| 0.50+ | 234 | 0.5412 | 0.3462 | 🔴+0.1951 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 77 | 0.81 |
| win | <5.0 | ✅learned | 148 | 0.711 |
| win | <10.0 | ✅learned | 75 | 0.466 |
| win | <20.0 | ✅learned | 25 | 0.218 |
| win | <50.0 | ⚠️fallback | 5 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-20T06:10:01.340334+09:00_