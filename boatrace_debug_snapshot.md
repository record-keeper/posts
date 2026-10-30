# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-31T06:20:01.226175+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×125 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2288 actual=0.2000 gap=+0.0288`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=31.8% ROI=0.87 (コスト 10,300/回収 8,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S00: n=186 hit%=30.1% hit_CI[Bonf]=[21.4,40.5]% ROI=0.81 ROI_boot95=[0.62,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S01_NAKAANA1: n=185 hit%=33.5% hit_CI[Bonf]=[24.4,44.1]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=47.8% hit_CI[Bonf]=[31.7,64.5]% ROI=1.06 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-31T06:00:41]
- key: `ORPHAN_SCAN|158 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift ≤-30%: n=26 hit%=42.3% ROI=1.09 (コスト 7,600/回収 8,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=80 hit%=43.8% ROI=1.18 (コスト 18,300/回収 21,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=64 hit%=32.8% ROI=0.94 (コスト 15,500/回収 14,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift ≥+30%: n=50 hit%=26.0% ROI=0.85 (コスト 13,200/回収 11,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|bt=win: n=440 pred=0.4792 actual=0.3432 error=+0.1360 (+28%) brier=0.2400 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|S00(win): n=186 pred=0.4443 hit=0.3011 cal_err=+0.1432 brier=0.2318 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=185 pred=0.4881 hit=0.3351 cal_err=+0.1530 brier=0.2403 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=69 pred=0.5492 hit=0.4783 cal_err=+0.0709 brier=0.2611 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3212 actual=0.2286 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=121 pred=0.4393 actual=0.3471 gap=+0.0922`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.22MB / last modified 2026-10-31T06:00:55.665766+09:00

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
55 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 23:55:05,855 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 23:55:05,883 [INFO] predictor: Models loaded OK
2026-10-30 23:55:05,885 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-30 23:56:04,281 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-30 23:56:04,281 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 23:56:04,281 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 23:56:04,352 [INFO] predictor: Models loaded OK
2026-10-30 23:56:04,355 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-30 23:57:05,465 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-10-30 23:57:05,466 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 23:57:05,466 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 23:57:05,496 [INFO] predictor: Models loaded OK
2026-10-30 23:57:05,498 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-30 23:58:04,354 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-30 23:58:04,354 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 23:58:04,354 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 23:58:04,387 [INFO] predictor: Models loaded OK
2026-10-30 23:58:04,389 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-30 23:59:05,367 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-10-30 23:59:05,367 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-30 23:59:05,367 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-30 23:59:05,414 [INFO] predictor: Models loaded OK
2026-10-30 23:59:05,478 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 26
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 26
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 4, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 211
  FINAL_MISSING: 125
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 26
  ANOMALY_SCAN_FINAL_RATIO: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 16
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 13 | 13,500 | 9,030 | -4,470 | 0.669 |
| S01_NAKAANA1 | 37 | 11 | 7,400 | 5,600 | -1,800 | 0.757 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[06:00:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:19] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 9030, "roi_7d": 0.669, "sid": "S00"}
[06:00:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:59:05] FINAL_MISSING: {"deadline": "2026-10-30T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023081206", "sid": "S01_NAKAANA1"}
[23:59:05] FINAL_MISSING: {"deadline": "2026-10-30T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023081206", "sid": "S00"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-10-30T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103023061101", "sid": "S01_NAKAANA1"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-10-30T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103014061055", "sid": "S01_NAKAANA1"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-10-30T12:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103006041203", "sid": "S00"}
[23:37:04] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 9030, "roi_7d": 0.669, "sid": "S00"}
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
| S00 | 246R | win | 1 | 0.1957 | 5.5 | 1.08 | 300 | scan=- drift=- | 17:42:12 |
| S00 | 013R | win | 1 | 0.5174 | 5.7 | 2.95 | 300 | scan=- drift=- | 16:16:29 |
| S00 | 067R | win | 1 | 0.5735 | 8.3 | 4.76 | 300 | scan=18.2 drift=-54.4% | 13:39:39 |
| S02_TETSUBAN | 031R | win | 1 | 0.6031 | 2.2 | 1.33 | 200 | scan=- drift=- | 10:57:28 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 17:09:25 |
| S01_NAKAANA1 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 200 | scan=4.5 drift=-6.7% | 16:38:51 |
| S00 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 300 | scan=4.5 drift=-6.7% | 16:38:48 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 16:15:38 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5990 | 3.7 | 2.22 | 200 | scan=- drift=- | 14:00:01 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.1 drift=+54.8% | 13:24:39 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +5.6% | -77.4% | +111.7% | 17 | 6 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.2s |
| **Latency** (scan→final max) | 662.1s |
| **Traffic** (notifications 24h) | 26 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 440 | 0.4792 | 0.3432 | +0.1360 | 🟡+28% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4443 | 0.3011 | 0.2318 | 🔴-0.10 | 0.81 |
| S01_NAKAANA1 | win | 185 | 0.4881 | 0.3351 | 0.2403 | 🔴-0.08 | 0.881 |
| S02_TETSUBAN | win | 69 | 0.5492 | 0.4783 | 0.2611 | 🔴-0.05 | 1.062 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 156 | 0.4128 | 0.3205 | 🔴+0.0923 |
| 0.50+ | 261 | 0.5440 | 0.3755 | 🔴+0.1686 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 358 | 0.741 |
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
_auto-generated by claude_snapshot.py at 2026-10-31T06:20:01.226175+09:00_