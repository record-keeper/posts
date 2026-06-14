# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-15T07:10:01.881370+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2244 actual=0.2857 gap=-0.0613`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-15T06:00:14]
- key: `ROI_STAT|S00: n=144 hit%=28.5% hit_CI[Bonf]=[19.0,40.3]% ROI=0.88 ROI_boot95=[0.60,1.20]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-15T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=29.1% hit_CI[Bonf]=[19.3,41.4]% ROI=0.86 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-15T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=35.4% hit_CI[Bonf]=[22.0,51.7]% ROI=0.58 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-15T06:00:14]
- key: `ORPHAN_SCAN|140 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=29.4% ROI=0.88 (コスト 9,900/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-15T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=16.1% ROI=0.28 (コスト 6,800/回収 1,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-15T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=31.8% ROI=0.71 (コスト 15,500/回収 10,970)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-15T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=19.4% ROI=0.99 (コスト 8,200/回収 8,140)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=29 hit%=20.7% ROI=0.48 (コスト 8,000/回収 3,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=357 pred=0.4718 actual=0.3025 error=+0.1692 (+36%) brier=0.2403 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=144 pred=0.4234 hit=0.2847 cal_err=+0.1387 brier=0.2214 BSS=-0.09 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=134 pred=0.4868 hit=0.2910 cal_err=+0.1957 brier=0.2462 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=79 pred=0.5344 hit=0.3544 cal_err=+0.1800 brier=0.2647 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=103 pred=0.4394 actual=0.2233 gap=+0.2161`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.11MB / last modified 2026-06-15T07:00:05.681089+09:00

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
91 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 23:55:06,891 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 23:55:06,959 [INFO] predictor: Models loaded OK
2026-06-14 23:55:06,963 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 23:56:05,641 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-14 23:56:05,643 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 23:56:05,643 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 23:56:05,715 [INFO] predictor: Models loaded OK
2026-06-14 23:56:05,722 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 23:57:05,810 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-06-14 23:57:05,811 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 23:57:05,811 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 23:57:05,880 [INFO] predictor: Models loaded OK
2026-06-14 23:57:05,886 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 23:58:06,316 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-14 23:58:06,316 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 23:58:06,316 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 23:58:06,360 [INFO] predictor: Models loaded OK
2026-06-14 23:58:06,364 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 23:59:05,402 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-14 23:59:05,403 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 23:59:05,403 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 23:59:05,461 [INFO] predictor: Models loaded OK
2026-06-14 23:59:05,468 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 148
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 15 | 11,400 | 13,620 | +2,220 | 1.195 |
| S01_NAKAANA1 | 30 | 15 | 6,000 | 9,620 | +3,620 | 1.603 |
| S02_TETSUBAN | 23 | 8 | 4,600 | 2,300 | -2,300 | 0.5 |

## 直近アラート (24h・新しい順)
```
[06:00:09] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:09] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 2300, "roi_7d": 0.5, "sid": "S02_TETSUBAN"}
[06:00:09] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:59:05] FINAL_MISSING: {"deadline": "2026-06-14T14:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061422051425", "sid": "S00"}
[23:59:05] FINAL_MISSING: {"deadline": "2026-06-14T15:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061401011525", "sid": "S00"}
[23:52:06] FINAL_MISSING: {"deadline": "2026-06-14T13:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061416061316", "sid": "S00"}
[23:35:07] FINAL_MISSING: {"deadline": "2026-06-14T19:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061419041903", "sid": "S00"}
[23:33:06] FINAL_MISSING: {"deadline": "2026-06-14T14:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061406081459", "sid": "S00"}
[23:21:06] FINAL_MISSING: {"deadline": "2026-06-14T13:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061406061345", "sid": "S00"}
[23:09:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S00 | 127R | win | 1 | 0.5476 | 5.4 | 2.96 | 300 | scan=9.2 drift=-41.3% | 18:18:20 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=4.5 drift=-11.1% | 17:10:25 |
| S00 | 012R | win | 1 | 0.5174 | 16.1 | 8.33 | 300 | scan=- drift=- | 15:52:22 |
| S02_TETSUBAN | 201R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 15:15:22 |
| S00 | 168R | win | 1 | 0.5123 | 5.7 | 2.92 | 300 | scan=8.2 drift=-30.5% | 14:30:37 |
| S01_NAKAANA1 | 223R | win | 1 | 0.5476 | 4.5 | 2.46 | 200 | scan=4.5 drift=+0.0% | 13:26:41 |
| S00 | 223R | win | 1 | 0.5476 | 4.5 | 2.46 | 300 | scan=4.5 drift=+0.0% | 13:26:39 |
| S01_NAKAANA1 | 222R | win | 1 | 0.5990 | 4.1 | 2.46 | 200 | scan=- drift=- | 12:59:32 |
| S00 | 222R | win | 1 | 0.5990 | 9.3 | 5.57 | 300 | scan=19.0 drift=-51.1% | 12:58:22 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.5032 | 3.9 | 1.96 | 200 | scan=3.3 drift=+18.2% | 12:45:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +2.2% | -82.9% | +162.5% | 17 | 9 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 510.9s |
| **Latency** (scan→final max) | 676.7s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 357 | 0.4718 | 0.3025 | +0.1692 | 🟡+36% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4234 | 0.2847 | 0.2214 | 🔴-0.09 | 0.883 |
| S01_NAKAANA1 | win | 134 | 0.4868 | 0.2910 | 0.2462 | 🔴-0.19 | 0.857 |
| S02_TETSUBAN | win | 79 | 0.5344 | 0.3544 | 0.2647 | 🔴-0.16 | 0.582 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 7 | 0.2244 | 0.2857 | 🔴-0.0613 |
| 0.30-0.50 | 124 | 0.4192 | 0.2419 | 🔴+0.1772 |
| 0.50+ | 209 | 0.5408 | 0.3541 | 🔴+0.1867 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 41 | 0.721 |
| win | <5.0 | ✅learned | 77 | 0.76 |
| win | <10.0 | ✅learned | 50 | 0.503 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-15T07:10:01.881370+09:00_