# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-09T07:40:01.776939+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×40 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×42 (24h)
- 🔴 PSI_DRIFT_DETECTED×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×39 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-09T07:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-09T07:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ORPHAN_SCAN  ×1  [2026-08-09T06:00:14]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=12 pred=0.1229 actual=0.1667 gap=-0.0438`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2237 actual=0.3636 gap=-0.1399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.70 ROI_boot95=[0.49,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=24.5% hit_CI[Bonf]=[16.1,35.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=64 hit%=51.6% hit_CI[Bonf]=[34.4,68.3]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=64<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.63 (コスト 10,000/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=38.9% ROI=0.93 (コスト 9,100/回収 8,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=60 hit%=28.3% ROI=0.76 (コスト 14,300/回収 10,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=20.0% ROI=0.38 (コスト 10,500/回収 4,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=39 hit%=28.2% ROI=1.02 (コスト 10,700/回収 10,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=398 pred=0.4592 actual=0.2889 error=+0.1703 (+37%) brier=0.2348 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=175 pred=0.4117 hit=0.2457 cal_err=+0.1660 brier=0.2222 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=159 pred=0.4833 hit=0.2453 cal_err=+0.2381 brier=0.2453 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.73MB / last modified 2026-08-09T07:30:05.055757+09:00

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
49 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-08 23:55:04,149 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-08 23:55:04,207 [INFO] predictor: Models loaded OK
2026-08-08 23:55:04,214 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-08 23:56:04,315 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-08 23:56:04,315 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-08 23:56:04,315 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-08 23:56:04,345 [INFO] predictor: Models loaded OK
2026-08-08 23:56:04,348 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-08 23:57:04,594 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-08-08 23:57:04,594 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-08 23:57:04,594 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-08 23:57:04,625 [INFO] predictor: Models loaded OK
2026-08-08 23:57:04,627 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-08 23:58:03,599 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-08-08 23:58:03,599 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-08 23:58:03,599 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-08 23:58:03,632 [INFO] predictor: Models loaded OK
2026-08-08 23:58:03,634 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-08 23:59:03,317 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-08-08 23:59:03,317 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-08 23:59:03,317 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-08 23:59:03,376 [INFO] predictor: Models loaded OK
2026-08-08 23:59:03,380 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 12, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 127
  FINAL_MISSING: 42
  PSI_DRIFT_DETECTED: 40
  CIRCUIT_BREAKER_TRIP: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 5 | 8,400 | 4,170 | -4,230 | 0.496 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 3,720 | -3,080 | 0.547 |
| S02_TETSUBAN | 11 | 8 | 2,200 | 2,520 | +320 | 1.145 |

## 直近アラート (24h・新しい順)
```
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3720, "roi_7d": 0.547, "sid": "S01_NAKAANA1"}
[06:00:05] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 4170, "roi_7d": 0.496, "sid": "S00"}
[06:00:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 73, "psi": 0.259}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-08-08T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080802061314", "sid": "S00"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-08-08T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080802041214", "sid": "S00"}
[23:43:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 73, "psi": 0.259}
[23:23:03] FINAL_MISSING: {"deadline": "2026-08-08T14:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080802091448", "sid": "S00"}
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
| S00 | 155R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=5.6 drift=-25.0% | 17:03:30 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4956 | 3.0 | 1.49 | 200 | scan=3.0 drift=+0.0% | 16:37:19 |
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 15:46:18 |
| S02_TETSUBAN | 201R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 15:22:29 |
| S01_NAKAANA1 | 168R | win | 1 | 0.5174 | 3.2 | 1.66 | 200 | scan=3.8 drift=-15.8% | 14:20:19 |
| S01_NAKAANA1 | 044R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=3.1 drift=+12.9% | 13:21:18 |
| S02_TETSUBAN | 166R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 13:19:30 |
| S00 | 025R | win | 1 | 0.5174 | 5.0 | 2.59 | 300 | scan=4.3 drift=+16.3% | 12:41:18 |
| S01_NAKAANA1 | 024R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 12:11:44 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.8 | 1.65 | 200 | scan=- drift=- | 11:47:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 42 | -1.4% | -73.3% | +112.5% | 15 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 412.2s |
| **Latency** (scan→final max) | 594.1s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 398 | 0.4592 | 0.2889 | +0.1703 | 🟡+37% | 0.2348 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4117 | 0.2457 | 0.2222 | 🔴-0.20 | 0.703 |
| S01_NAKAANA1 | win | 159 | 0.4833 | 0.2453 | 0.2453 | 🔴-0.32 | 0.731 |
| S02_TETSUBAN | win | 64 | 0.5291 | 0.5156 | 0.2432 | ✅+0.03 | 1.0 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 152 | 0.4164 | 0.2171 | 🔴+0.1993 |
| 0.50+ | 210 | 0.5402 | 0.3524 | 🔴+0.1878 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 99 | 0.786 |
| win | <5.0 | ✅learned | 174 | 0.723 |
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
_auto-generated by claude_snapshot.py at 2026-08-09T07:40:01.776939+09:00_