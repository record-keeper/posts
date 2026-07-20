# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-21T06:40:01.921943+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-21T06:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-21T06:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-07-21T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-21T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-21T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=27.3% ROI=0.54 (コスト 8,000/回収 4,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-21T06:00:07]
- key: `ROI_STAT|S00: n=189 hit%=27.0% hit_CI[Bonf]=[18.8,37.1]% ROI=0.73 ROI_boot95=[0.54,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-21T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-21T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=29.0% hit_CI[Bonf]=[19.9,40.1]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-21T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-21T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=46.4% hit_CI[Bonf]=[30.4,63.1]% ROI=0.94 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-21T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=25.8% ROI=0.63 (コスト 9,100/回収 5,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-21T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.84 (コスト 11,700/回収 9,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-21T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=32.6% ROI=0.77 (コスト 19,900/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-21T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=18.4% ROI=0.45 (コスト 10,600/回収 4,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=420 pred=0.4666 actual=0.3095 error=+0.1571 (+34%) brier=0.2364 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=189 pred=0.4293 hit=0.2698 cal_err=+0.1594 brier=0.2292 BSS=-0.16 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=162 pred=0.4784 hit=0.2901 cal_err=+0.1882 brier=0.2372 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=69 pred=0.5411 hit=0.4638 cal_err=+0.0773 brier=0.2544 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-21T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1793 actual=0.5000 gap=-0.3207`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.29MB / last modified 2026-07-21T06:30:02.841607+09:00

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
99 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-20 23:55:03,999 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-20 23:55:04,043 [INFO] predictor: Models loaded OK
2026-07-20 23:55:04,047 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-20 23:56:03,457 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-20 23:56:03,458 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-20 23:56:03,458 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-20 23:56:03,484 [INFO] predictor: Models loaded OK
2026-07-20 23:56:03,486 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-20 23:57:04,114 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-07-20 23:57:04,114 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-20 23:57:04,114 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-20 23:57:04,158 [INFO] predictor: Models loaded OK
2026-07-20 23:57:04,162 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-20 23:58:03,881 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-07-20 23:58:03,881 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-20 23:58:03,881 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-20 23:58:03,908 [INFO] predictor: Models loaded OK
2026-07-20 23:58:03,910 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-20 23:59:03,293 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-07-20 23:59:03,293 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-20 23:59:03,293 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-20 23:59:03,335 [INFO] predictor: Models loaded OK
2026-07-20 23:59:03,339 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 10, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 153
  FINAL_MISSING: 63
  CIRCUIT_BREAKER_TRIP: 44
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_DROP: 4
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 9 | 13,800 | 8,730 | -5,070 | 0.633 |
| S01_NAKAANA1 | 40 | 8 | 8,000 | 4,800 | -3,200 | 0.6 |
| S02_TETSUBAN | 14 | 8 | 2,800 | 3,300 | +500 | 1.179 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 4800, "roi_7d": 0.6, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 13800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 8730, "roi_7d": 0.633, "sid": "S00"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:59:03] FINAL_MISSING: {"deadline": "2026-07-20T13:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072016041321", "sid": "S00"}
[23:54:04] FINAL_MISSING: {"deadline": "2026-07-20T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072010051018", "sid": "S00"}
[23:49:03] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 4800, "roi_7d": 0.6, "sid": "S01_NAKAANA1"}
[23:43:03] FINAL_MISSING: {"deadline": "2026-07-20T13:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072018101306", "sid": "S01_NAKAANA1"}
[23:23:03] FINAL_MISSING: {"deadline": "2026-07-20T17:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072012061749", "sid": "S00"}
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
| S01_NAKAANA1 | 126R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 17:46:18 |
| S00 | 124R | win | 1 | 0.3177 | 15.6 | 4.96 | 300 | scan=- drift=- | 16:57:19 |
| S02_TETSUBAN | 203R | win | 1 | 0.5595 | 2.0 | 1.12 | 200 | scan=- drift=- | 16:37:18 |
| S01_NAKAANA1 | 227R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:20:20 |
| S00 | 029R | win | 1 | 0.5334 | 14.9 | 7.95 | 300 | scan=46.1 drift=-67.7% | 14:45:19 |
| S00 | 028R | win | 1 | 0.1973 | 45.1 | 8.90 | 300 | scan=- drift=- | 14:13:18 |
| S01_NAKAANA1 | 096R | win | 1 | 0.3177 | 3.7 | 1.18 | 200 | scan=- drift=- | 13:07:18 |
| S00 | 043R | win | 1 | 0.3177 | 4.4 | 1.40 | 300 | scan=27.0 drift=-83.7% | 12:51:19 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4989 | 4.6 | 2.30 | 200 | scan=3.0 drift=+53.3% | 12:49:19 |
| S00 | 093R | win | 1 | 0.4111 | 8.0 | 3.29 | 300 | scan=8.2 drift=-2.4% | 11:33:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +18.1% | -83.7% | +628.9% | 19 | 9 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 505.4s |
| **Latency** (scan→final max) | 644.5s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 420 | 0.4666 | 0.3095 | +0.1571 | 🟡+34% | 0.2364 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 189 | 0.4293 | 0.2698 | 0.2292 | 🔴-0.16 | 0.726 |
| S01_NAKAANA1 | win | 162 | 0.4784 | 0.2901 | 0.2372 | 🔴-0.15 | 0.767 |
| S02_TETSUBAN | win | 69 | 0.5411 | 0.4638 | 0.2544 | 🔴-0.02 | 0.938 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1793 | 0.5000 | 🔴-0.3207 |
| 0.20-0.30 | 15 | 0.2268 | 0.2667 | ✅-0.0399 |
| 0.30-0.50 | 164 | 0.4143 | 0.2561 | 🔴+0.1582 |
| 0.50+ | 226 | 0.5416 | 0.3496 | 🔴+0.1921 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 78 | 0.81 |
| win | <5.0 | ✅learned | 148 | 0.711 |
| win | <10.0 | ✅learned | 75 | 0.466 |
| win | <20.0 | ✅learned | 25 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-07-21T06:40:01.921943+09:00_