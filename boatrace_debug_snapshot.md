# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-06T06:40:01.527538+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×16 (24h)
- 🔴 PSI_DRIFT_DETECTED×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-06T06:00:21]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=12 pred=0.1235 actual=0.1667 gap=-0.0432`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.72 ROI_boot95=[0.51,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=154 hit%=24.7% hit_CI[Bonf]=[16.1,35.8]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-06T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.97 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=22.9% ROI=0.65 (コスト 10,300/回収 6,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=35.3% ROI=0.85 (コスト 8,600/回収 7,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=62 hit%=32.3% ROI=0.80 (コスト 14,700/回収 11,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-06T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=41 hit%=22.0% ROI=0.43 (コスト 9,500/回収 4,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|bt=win: n=399 pred=0.4598 actual=0.2957 error=+0.1640 (+36%) brier=0.2341 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|S00(win): n=178 pred=0.4154 hit=0.2584 cal_err=+0.1569 brier=0.2245 BSS=-0.17 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=154 pred=0.4815 hit=0.2468 cal_err=+0.2348 brier=0.2405 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=67 pred=0.5278 hit=0.5075 cal_err=+0.0203 brier=0.2452 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3227 actual=0.2414 gap=+0.0813`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.54MB / last modified 2026-08-06T06:30:03.047775+09:00

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
54 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 23:55:03,754 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 23:55:03,804 [INFO] predictor: Models loaded OK
2026-08-05 23:55:03,808 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 23:56:03,545 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-08-05 23:56:03,546 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 23:56:03,546 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 23:56:03,593 [INFO] predictor: Models loaded OK
2026-08-05 23:56:03,597 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 23:57:03,636 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-08-05 23:57:03,636 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 23:57:03,636 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 23:57:03,687 [INFO] predictor: Models loaded OK
2026-08-05 23:57:03,693 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 23:58:04,313 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-08-05 23:58:04,313 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 23:58:04,313 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 23:58:04,346 [INFO] predictor: Models loaded OK
2026-08-05 23:58:04,347 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 23:59:03,955 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-08-05 23:59:03,955 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 23:59:03,955 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 23:59:04,014 [INFO] predictor: Models loaded OK
2026-08-05 23:59:04,020 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 50
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 50
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 9, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 134
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 25
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 16
  PSI_DRIFT_DETECTED: 4
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 9 | 10,200 | 9,030 | -1,170 | 0.885 |
| S01_NAKAANA1 | 32 | 7 | 6,400 | 4,680 | -1,720 | 0.731 |
| S02_TETSUBAN | 10 | 5 | 2,000 | 1,500 | -500 | 0.75 |

## 直近アラート (24h・新しい順)
```
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:33:04] FINAL_MISSING: {"deadline": "2026-08-05T14:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080504071458", "sid": "S00"}
[23:18:04] FINAL_MISSING: {"deadline": "2026-08-05T17:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080519061746", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:08:03] FINAL_MISSING: {"deadline": "2026-08-05T13:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080505051331", "sid": "S00"}
[22:33:03] FINAL_MISSING: {"deadline": "2026-08-05T14:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080504071458", "sid": "S00"}
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
| S00 | 098R | win | 1 | 0.3177 | 10.5 | 3.34 | 300 | scan=18.0 drift=-41.7% | 13:58:19 |
| S00 | 045R | win | 1 | 0.3177 | 9.5 | 3.02 | 300 | scan=10.5 drift=-9.5% | 13:52:19 |
| S01_NAKAANA1 | 055R | win | 1 | 0.5891 | 4.6 | 2.71 | 200 | scan=- drift=- | 13:28:18 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.9 drift=-10.3% | 12:35:45 |
| S00 | 053R | win | 1 | 0.5476 | 4.2 | 2.30 | 300 | scan=- drift=- | 12:29:19 |
| S00 | 094R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=6.0 drift=-13.3% | 11:56:18 |
| S01_NAKAANA1 | 172R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=- drift=- | 11:41:18 |
| S00 | 216R | win | 1 | 0.5476 | 4.7 | 2.57 | 300 | scan=4.7 drift=+0.0% | 10:51:42 |
| S02_TETSUBAN | 211R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 08:37:18 |
| S01_NAKAANA1 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.2 drift=+28.1% | 18:40:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -1.9% | -73.3% | +107.5% | 17 | 11 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.5s |
| **Latency** (scan→final max) | 623.6s |
| **Traffic** (notifications 24h) | 50 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 399 | 0.4598 | 0.2957 | +0.1640 | 🟡+36% | 0.2341 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4154 | 0.2584 | 0.2245 | 🔴-0.17 | 0.721 |
| S01_NAKAANA1 | win | 154 | 0.4815 | 0.2468 | 0.2405 | 🔴-0.29 | 0.728 |
| S02_TETSUBAN | win | 67 | 0.5278 | 0.5075 | 0.2452 | ✅+0.02 | 0.969 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1235 | 0.1667 | ✅-0.0432 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 155 | 0.4170 | 0.2258 | 🔴+0.1912 |
| 0.50+ | 209 | 0.5407 | 0.3589 | 🔴+0.1818 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 96 | 0.787 |
| win | <5.0 | ✅learned | 170 | 0.72 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
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
_auto-generated by claude_snapshot.py at 2026-08-06T06:40:01.527538+09:00_