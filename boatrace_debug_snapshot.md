# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-22T07:40:01.886773+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×42 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×50 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×42 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-22T06:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-22T06:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-07-22T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=27.3% ROI=0.54 (コスト 8,000/回収 4,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3243 actual=0.0857 gap=+0.2386`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=46.4% hit_CI[Bonf]=[30.4,63.1]% ROI=0.94 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S00: n=182 hit%=26.4% hit_CI[Bonf]=[18.1,36.7]% ROI=0.70 ROI_boot95=[0.51,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=29.2% hit_CI[Bonf]=[20.1,40.4]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=23.3% ROI=0.54 (コスト 8,800/回収 4,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.74 (コスト 11,000/回収 8,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=80 hit%=35.0% ROI=0.84 (コスト 18,300/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=19.5% ROI=0.45 (コスト 11,500/回収 5,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=412 pred=0.4661 actual=0.3083 error=+0.1579 (+34%) brier=0.2346 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=182 pred=0.4280 hit=0.2637 cal_err=+0.1643 brier=0.2258 BSS=-0.16 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=161 pred=0.4772 hit=0.2919 cal_err=+0.1852 brier=0.2362 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=69 pred=0.5408 hit=0.4638 cal_err=+0.0771 brier=0.2541 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.36MB / last modified 2026-07-22T07:30:02.634039+09:00

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
42 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-21 23:55:03,742 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-21 23:55:03,784 [INFO] predictor: Models loaded OK
2026-07-21 23:55:03,788 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-21 23:56:03,596 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-21 23:56:03,596 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-21 23:56:03,596 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-21 23:56:03,623 [INFO] predictor: Models loaded OK
2026-07-21 23:56:03,625 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-21 23:57:03,364 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-07-21 23:57:03,364 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-21 23:57:03,364 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-21 23:57:03,407 [INFO] predictor: Models loaded OK
2026-07-21 23:57:03,411 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-21 23:58:04,087 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-07-21 23:58:04,087 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-21 23:58:04,087 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-21 23:58:04,115 [INFO] predictor: Models loaded OK
2026-07-21 23:58:04,117 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-21 23:59:03,788 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-07-21 23:59:03,788 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-21 23:59:03,788 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-21 23:59:03,815 [INFO] predictor: Models loaded OK
2026-07-21 23:59:03,817 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 20, 'result': 11, 'scan': 20}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 50
  CIRCUIT_BREAKER_TRIP: 42
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCRAPER_FAILURE_BURST: 33
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 9 | 13,500 | 8,730 | -4,770 | 0.647 |
| S01_NAKAANA1 | 43 | 8 | 8,600 | 3,620 | -4,980 | 0.421 |
| S02_TETSUBAN | 15 | 8 | 3,000 | 3,300 | +300 | 1.1 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 8600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 3620, "roi_7d": 0.421, "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 8730, "roi_7d": 0.647, "sid": "S00"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:41:04] FINAL_MISSING: {"deadline": "2026-07-21T18:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072119061808", "sid": "S00"}
[23:24:04] FINAL_MISSING: {"deadline": "2026-07-21T11:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072116011149", "sid": "S00"}
[23:22:04] FINAL_MISSING: {"deadline": "2026-07-21T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072110081145", "sid": "S00"}
[23:11:03] CIRCUIT_BREAKER_TRIP: {"cost": 8600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 3620, "roi_7d": 0.421, "sid": "S01_NAKAANA1"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S01_NAKAANA1 | 159R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=- drift=- | 19:09:29 |
| S01_NAKAANA1 | 196R | win | 1 | 0.4920 | 3.2 | 1.57 | 200 | scan=3.8 drift=-15.8% | 18:06:30 |
| S00 | 126R | win | 1 | 0.4111 | 12.7 | 5.22 | 300 | scan=4.8 drift=+164.6% | 17:46:19 |
| S00 | 121R | win | 1 | 0.5891 | 7.1 | 4.18 | 300 | scan=4.1 drift=+73.2% | 15:24:19 |
| S01_NAKAANA1 | 223R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 13:11:19 |
| S02_TETSUBAN | 096R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 13:06:21 |
| S00 | 043R | win | 1 | 0.4111 | 35.2 | 14.47 | 300 | scan=25.5 drift=+38.0% | 12:51:18 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.4920 | 4.5 | 2.21 | 200 | scan=3.0 drift=+50.0% | 12:48:30 |
| S01_NAKAANA1 | 094R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.5 drift=+17.1% | 12:05:31 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5063 | 3.3 | 1.67 | 200 | scan=- drift=- | 11:52:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +21.9% | -83.7% | +628.9% | 19 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 489.7s |
| **Latency** (scan→final max) | 604.8s |
| **Traffic** (notifications 24h) | 51 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4661 | 0.3083 | +0.1579 | 🟡+34% | 0.2346 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4280 | 0.2637 | 0.2258 | 🔴-0.16 | 0.703 |
| S01_NAKAANA1 | win | 161 | 0.4772 | 0.2919 | 0.2362 | 🔴-0.14 | 0.765 |
| S02_TETSUBAN | win | 69 | 0.5408 | 0.4638 | 0.2541 | 🔴-0.02 | 0.938 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1798 | 0.4286 | 🔴-0.2488 |
| 0.20-0.30 | 15 | 0.2268 | 0.2667 | ✅-0.0399 |
| 0.30-0.50 | 164 | 0.4148 | 0.2622 | 🔴+0.1526 |
| 0.50+ | 219 | 0.5414 | 0.3470 | 🔴+0.1944 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 78 | 0.81 |
| win | <5.0 | ✅learned | 149 | 0.71 |
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
_auto-generated by claude_snapshot.py at 2026-07-22T07:40:01.886773+09:00_