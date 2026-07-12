# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-13T07:20:01.772482+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-13T07:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S00: n=178 hit%=30.3% hit_CI[Bonf]=[21.5,41.0]% ROI=0.79 ROI_boot95=[0.60,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.1% hit_CI[Bonf]=[20.6,41.6]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-13T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=45.6% hit_CI[Bonf]=[29.6,62.5]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-13T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-13T06:00:06]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=32.4% ROI=0.84 (コスト 9,900/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=31.9% ROI=0.75 (コスト 11,500/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=34.9% ROI=0.99 (コスト 19,900/回収 19,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=33.3% ROI=0.77 (コスト 8,800/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-13T06:00:06]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=20.0% ROI=0.39 (コスト 8,400/回収 3,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|bt=win: n=399 pred=0.4722 actual=0.3283 error=+0.1439 (+30%) brier=0.2371 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|S00(win): n=178 pred=0.4358 hit=0.3034 cal_err=+0.1324 brier=0.2286 BSS=-0.08 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=153 pred=0.4841 hit=0.3007 cal_err=+0.1834 brier=0.2375 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=68 pred=0.5408 hit=0.4559 cal_err=+0.0849 brier=0.2588 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1780 actual=0.6667 gap=-0.4887`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2280 actual=0.2000 gap=+0.0280`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-13T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.58MB / last modified 2026-07-13T07:00:02.621993+09:00

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
28 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 23:55:04,028 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 23:55:04,055 [INFO] predictor: Models loaded OK
2026-07-12 23:55:04,057 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 23:56:03,728 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-12 23:56:03,728 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 23:56:03,728 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 23:56:03,771 [INFO] predictor: Models loaded OK
2026-07-12 23:56:03,775 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 23:57:04,162 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-07-12 23:57:04,162 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 23:57:04,162 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 23:57:04,204 [INFO] predictor: Models loaded OK
2026-07-12 23:57:04,208 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 23:58:03,731 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-07-12 23:58:03,731 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 23:58:03,731 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 23:58:03,758 [INFO] predictor: Models loaded OK
2026-07-12 23:58:03,760 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 23:59:03,706 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-07-12 23:59:03,706 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 23:59:03,707 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 23:59:03,750 [INFO] predictor: Models loaded OK
2026-07-12 23:59:03,754 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 102
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 102
  }
]
```

## Phase別通知記録 (24h)
{'final': 41, 'result': 23, 'scan': 38}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 196
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_NO_ACTION: 33
  CIRCUIT_BREAKER_TRIP: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 19 | 15,000 | 15,150 | +150 | 1.01 |
| S01_NAKAANA1 | 38 | 10 | 7,600 | 5,120 | -2,480 | 0.674 |
| S02_TETSUBAN | 18 | 9 | 3,600 | 4,360 | +760 | 1.211 |

## 直近アラート (24h・新しい順)
```
[06:00:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:03] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 5120, "roi_7d": 0.674, "sid": "S01_NAKAANA1"}
[06:00:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:41:03] FINAL_MISSING: {"deadline": "2026-07-12T12:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071209041205", "sid": "S00"}
[23:36:04] FINAL_MISSING: {"deadline": "2026-07-12T19:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071219041903", "sid": "S00"}
[23:36:04] FINAL_MISSING: {"deadline": "2026-07-12T17:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071215041701", "sid": "S00"}
[23:36:04] FINAL_MISSING: {"deadline": "2026-07-12T15:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071204071500", "sid": "S00"}
[23:32:03] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 5120, "roi_7d": 0.674, "sid": "S01_NAKAANA1"}
[23:29:03] FINAL_MISSING: {"deadline": "2026-07-12T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071210040950", "sid": "S00"}
[23:21:03] FINAL_MISSING: {"deadline": "2026-07-12T10:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071210061044", "sid": "S00"}
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
| S02_TETSUBAN | 205R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=- drift=- | 17:34:29 |
| S00 | 153R | win | 1 | 0.1760 | 7.5 | 1.32 | 300 | scan=7.5 drift=+0.0% | 16:20:30 |
| S00 | 227R | win | 1 | 0.3177 | 9.9 | 3.15 | 300 | scan=13.1 drift=-24.4% | 15:16:18 |
| S00 | 226R | win | 1 | 0.4989 | 9.2 | 4.59 | 300 | scan=12.0 drift=-23.3% | 14:44:18 |
| S00 | 166R | win | 1 | 0.4111 | 19.5 | 8.02 | 300 | scan=- drift=- | 14:37:31 |
| S00 | 038R | win | 1 | 0.6037 | 4.6 | 2.78 | 300 | scan=- drift=- | 14:21:51 |
| S00 | 225R | win | 1 | 0.4111 | 9.0 | 3.70 | 300 | scan=10.8 drift=-16.7% | 14:13:19 |
| S02_TETSUBAN | 056R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 14:01:30 |
| S02_TETSUBAN | 037R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 13:53:48 |
| S01_NAKAANA1 | 087R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.3 drift=+18.2% | 13:29:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +16.9% | -73.3% | +533.3% | 19 | 7 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 451.2s |
| **Latency** (scan→final max) | 615.5s |
| **Traffic** (notifications 24h) | 102 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 399 | 0.4722 | 0.3283 | +0.1439 | 🟡+30% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4358 | 0.3034 | 0.2286 | 🔴-0.08 | 0.789 |
| S01_NAKAANA1 | win | 153 | 0.4841 | 0.3007 | 0.2375 | 🔴-0.13 | 0.798 |
| S02_TETSUBAN | win | 68 | 0.5408 | 0.4559 | 0.2588 | 🔴-0.04 | 0.896 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1780 | 0.6667 | 🔴-0.4887 |
| 0.20-0.30 | 15 | 0.2280 | 0.2000 | ✅+0.0280 |
| 0.30-0.50 | 148 | 0.4189 | 0.2905 | 🔴+0.1284 |
| 0.50+ | 224 | 0.5417 | 0.3616 | 🔴+0.1801 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 70 | 0.794 |
| win | <5.0 | ✅learned | 136 | 0.707 |
| win | <10.0 | ✅learned | 73 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-13T07:20:01.772482+09:00_