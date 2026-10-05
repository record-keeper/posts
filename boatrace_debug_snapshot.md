# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-06T07:20:01.908897+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×46 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-06T06:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S00: n=167 hit%=22.8% hit_CI[Bonf]=[14.8,33.3]% ROI=0.63 ROI_boot95=[0.43,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=30.5% hit_CI[Bonf]=[21.4,41.5]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=48.2% hit_CI[Bonf]=[33.3,63.5]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-06T06:00:21]
- key: `ORPHAN_SCAN|174 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=40.6% ROI=1.12 (コスト 8,900/回収 9,950)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=25.5% ROI=0.69 (コスト 12,000/回収 8,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=28.1% ROI=0.75 (コスト 20,100/回収 15,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=36.4% ROI=0.81 (コスト 10,200/回収 8,240)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=21.7% ROI=0.66 (コスト 12,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|bt=win: n=417 pred=0.4782 actual=0.3094 error=+0.1689 (+35%) brier=0.2494 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|S00(win): n=167 pred=0.4473 hit=0.2275 cal_err=+0.2197 brier=0.2467 BSS=-0.40 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=167 pred=0.4872 hit=0.3054 cal_err=+0.1818 brier=0.2494 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=83 pred=0.5226 hit=0.4819 cal_err=+0.0406 brier=0.2548 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3222 actual=0.3333 gap=-0.0111`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=135 pred=0.4405 actual=0.2741 gap=+0.1664`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.0MB / last modified 2026-10-06T07:00:09.951203+09:00

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
21 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-05 23:55:04,821 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-05 23:55:04,852 [INFO] predictor: Models loaded OK
2026-10-05 23:55:04,854 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-05 23:56:04,113 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-05 23:56:04,113 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-05 23:56:04,113 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-05 23:56:04,148 [INFO] predictor: Models loaded OK
2026-10-05 23:56:04,150 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-05 23:57:04,168 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-05 23:57:04,169 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-05 23:57:04,169 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-05 23:57:04,220 [INFO] predictor: Models loaded OK
2026-10-05 23:57:04,224 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-05 23:58:04,137 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-05 23:58:04,137 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-05 23:58:04,138 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-05 23:58:04,171 [INFO] predictor: Models loaded OK
2026-10-05 23:58:04,174 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-05 23:59:03,854 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-10-05 23:59:03,854 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-05 23:59:03,854 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-05 23:59:03,886 [INFO] predictor: Models loaded OK
2026-10-05 23:59:03,888 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 11, 'scan': 23}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 46
  CIRCUIT_BREAKER_NO_ACTION: 33
  ANOMALY_SCRAPER_FAILURE_BURST: 24
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 5
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 15 | 15,900 | 12,630 | -3,270 | 0.794 |
| S01_NAKAANA1 | 52 | 21 | 10,400 | 15,180 | +4,780 | 1.46 |
| S02_TETSUBAN | 16 | 6 | 3,200 | 1,720 | -1,480 | 0.537 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:58:04] FINAL_MISSING: {"deadline": "2026-10-05T14:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100502081423", "sid": "S00"}
[23:58:04] FINAL_MISSING: {"deadline": "2026-10-05T12:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100502041219", "sid": "S00"}
[23:49:04] FINAL_MISSING: {"deadline": "2026-10-05T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100505041211", "sid": "S00"}
[23:16:04] FINAL_MISSING: {"deadline": "2026-10-05T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100505031141", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[22:58:03] FINAL_MISSING: {"deadline": "2026-10-05T14:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100502081423", "sid": "S00"}
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
| S02_TETSUBAN | 209R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=2.1 drift=+9.5% | 21:38:20 |
| S01_NAKAANA1 | 206R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=- drift=- | 20:22:20 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=3.5 drift=+31.4% | 18:05:19 |
| S00 | 056R | win | 1 | 0.3177 | 10.0 | 3.18 | 300 | scan=20.5 drift=-51.2% | 13:09:19 |
| S00 | 225R | win | 1 | 0.3177 | 6.3 | 2.00 | 300 | scan=7.5 drift=-16.0% | 13:06:19 |
| S00 | 096R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=13.5 drift=-68.9% | 12:50:20 |
| S00 | 116R | win | 1 | 0.5334 | 7.8 | 4.16 | 300 | scan=9.0 drift=-13.3% | 12:44:19 |
| S01_NAKAANA1 | 223R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.2 drift=-14.3% | 11:56:21 |
| S01_NAKAANA1 | 053R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 11:38:19 |
| S01_NAKAANA1 | 186R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=3.3 drift=+36.4% | 10:59:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 83 | +4.1% | -76.2% | +169.2% | 29 | 12 | 63 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 494.7s |
| **Latency** (scan→final max) | 606.9s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 417 | 0.4782 | 0.3094 | +0.1689 | 🟡+35% | 0.2494 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4473 | 0.2275 | 0.2467 | 🔴-0.40 | 0.63 |
| S01_NAKAANA1 | win | 167 | 0.4872 | 0.3054 | 0.2494 | 🔴-0.18 | 1.012 |
| S02_TETSUBAN | win | 83 | 0.5226 | 0.4819 | 0.2548 | 🔴-0.02 | 0.818 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 165 | 0.4190 | 0.2848 | 🔴+0.1342 |
| 0.50+ | 236 | 0.5426 | 0.3305 | 🔴+0.2121 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 168 | 0.768 |
| win | <5.0 | ✅learned | 298 | 0.766 |
| win | <10.0 | ✅learned | 135 | 0.459 |
| win | <20.0 | ✅learned | 36 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-06T07:20:01.908897+09:00_