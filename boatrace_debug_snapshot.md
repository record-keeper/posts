# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-29T06:30:01.973455+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×37 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×57 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=195<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-29T06:00:19]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=196<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=69 hit%=33.3% ROI=0.91 (コスト 16,500/回収 15,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=51 hit%=25.5% ROI=0.83 (コスト 13,500/回収 11,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2288 actual=0.2000 gap=+0.0288`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-29T06:00:19]
- key: `ROI_STAT|S00: n=195 hit%=30.3% hit_CI[Bonf]=[21.7,40.4]% ROI=0.82 ROI_boot95=[0.61,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-29T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=196 hit%=34.2% hit_CI[Bonf]=[25.2,44.4]% ROI=0.93 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-29T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=47.9% hit_CI[Bonf]=[32.2,64.1]% ROI=1.04 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=48.1% ROI=1.31 (コスト 7,800/回収 10,230)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=31.2% ROI=0.83 (コスト 11,400/回収 9,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=40.7% ROI=1.12 (コスト 19,700/回収 22,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=464 pred=0.4778 actual=0.3470 error=+0.1308 (+27%) brier=0.2401 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=195 pred=0.4428 hit=0.3026 cal_err=+0.1403 brier=0.2344 BSS=-0.11 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=196 pred=0.4867 hit=0.3418 cal_err=+0.1448 brier=0.2380 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=73 pred=0.5471 hit=0.4795 cal_err=+0.0676 brier=0.2607 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=37 pred=0.3210 actual=0.2432 gap=+0.0778`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=130 pred=0.4382 actual=0.3308 gap=+0.1074`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.03MB / last modified 2026-10-29T06:00:43.818302+09:00

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
34 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-28 23:55:04,434 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-28 23:55:04,462 [INFO] predictor: Models loaded OK
2026-10-28 23:55:04,464 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-28 23:56:04,623 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-28 23:56:04,623 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-28 23:56:04,623 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-28 23:56:04,666 [INFO] predictor: Models loaded OK
2026-10-28 23:56:04,670 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-28 23:57:04,264 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-28 23:57:04,264 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-28 23:57:04,264 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-28 23:57:04,330 [INFO] predictor: Models loaded OK
2026-10-28 23:57:04,335 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-28 23:58:04,612 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-28 23:58:04,613 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-28 23:58:04,613 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-28 23:58:04,659 [INFO] predictor: Models loaded OK
2026-10-28 23:58:04,663 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-28 23:59:04,279 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-28 23:59:04,279 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-28 23:59:04,279 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-28 23:59:04,345 [INFO] predictor: Models loaded OK
2026-10-28 23:59:04,351 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 13, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 121
  FINAL_MISSING: 57
  CIRCUIT_BREAKER_TRIP: 37
  CIRCUIT_BREAKER_NO_ACTION: 30
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 13 | 14,700 | 10,170 | -4,530 | 0.692 |
| S01_NAKAANA1 | 52 | 12 | 10,400 | 5,780 | -4,620 | 0.556 |
| S02_TETSUBAN | 14 | 6 | 2,800 | 4,360 | +1,560 | 1.557 |

## 直近アラート (24h・新しい順)
```
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] CIRCUIT_BREAKER_TRIP: {"cost": 10400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 5780, "roi_7d": 0.556, "sid": "S01_NAKAANA1"}
[06:00:07] CIRCUIT_BREAKER_TRIP: {"cost": 14700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 10170, "roi_7d": 0.692, "sid": "S00"}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:56:04] CIRCUIT_BREAKER_TRIP: {"cost": 14700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 10170, "roi_7d": 0.692, "sid": "S00"}
[23:38:04] FINAL_MISSING: {"deadline": "2026-10-28T10:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102803011059", "sid": "S02_TETSUBAN"}
[23:32:03] FINAL_MISSING: {"deadline": "2026-10-28T11:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102823081154", "sid": "S00"}
[23:26:04] FINAL_MISSING: {"deadline": "2026-10-28T17:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102815071755", "sid": "S00"}
[23:24:04] FINAL_MISSING: {"deadline": "2026-10-28T10:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102816011046", "sid": "S00"}
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
| S00 | 079R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.7 drift=-6.4% | 19:01:31 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=3.5 drift=-2.9% | 17:34:21 |
| S00 | 073R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=4.5 drift=+24.4% | 16:12:21 |
| S00 | 153R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=4.5 drift=+66.7% | 16:04:19 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=- drift=- | 14:59:19 |
| S02_TETSUBAN | 167R | win | 1 | 0.6037 | 2.4 | 1.45 | 200 | scan=- drift=- | 13:45:31 |
| S00 | 167R | win | 1 | 0.6037 | 19.1 | 11.53 | 300 | scan=19.1 drift=+0.0% | 13:44:31 |
| S01_NAKAANA1 | 224R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=- drift=- | 12:31:30 |
| S01_NAKAANA1 | 135R | win | 1 | 0.3177 | 4.7 | 1.49 | 200 | scan=3.3 drift=+42.4% | 12:25:44 |
| S00 | 223R | win | 1 | 0.5123 | 16.8 | 8.61 | 300 | scan=16.5 drift=+1.8% | 12:00:34 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +8.1% | -77.4% | +111.7% | 17 | 5 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 470.6s |
| **Latency** (scan→final max) | 612.7s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 464 | 0.4778 | 0.3470 | +0.1308 | 🟡+27% | 0.2401 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 195 | 0.4428 | 0.3026 | 0.2344 | 🔴-0.11 | 0.815 |
| S01_NAKAANA1 | win | 196 | 0.4867 | 0.3418 | 0.2380 | 🔴-0.06 | 0.927 |
| S02_TETSUBAN | win | 73 | 0.5471 | 0.4795 | 0.2607 | 🔴-0.04 | 1.037 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 167 | 0.4122 | 0.3114 | 🔴+0.1008 |
| 0.50+ | 273 | 0.5433 | 0.3846 | 🔴+0.1587 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 356 | 0.741 |
| win | <10.0 | ✅learned | 156 | 0.45 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-29T06:30:01.973455+09:00_