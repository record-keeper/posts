# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-21T06:50:01.515331+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×85 (24h)
- 🔴 PSI_DRIFT_DETECTED×45 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ORPHAN_SCAN  ×1  [2026-09-21T06:00:18]
- key: `ORPHAN_SCAN|183 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-21T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-21T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-21T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-21T06:00:18]
- key: `ROI_STAT|S00: n=167 hit%=24.0% hit_CI[Bonf]=[15.8,34.6]% ROI=0.76 ROI_boot95=[0.51,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-21T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=20.8% hit_CI[Bonf]=[13.3,31.1]% ROI=0.63 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-21T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=42.5% hit_CI[Bonf]=[27.4,59.1]% ROI=0.76 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-21T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=26.7% ROI=0.86 (コスト 8,600/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-21T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=17.9% ROI=0.54 (コスト 9,000/回収 4,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-21T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=22.9% ROI=0.70 (コスト 19,300/回収 13,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-21T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=23.4% ROI=0.45 (コスト 10,400/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-21T06:00:18]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=12.5% ROI=0.46 (コスト 10,900/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|bt=win: n=408 pred=0.4774 actual=0.2598 error=+0.2176 (+46%) brier=0.2418 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|S00(win): n=167 pred=0.4436 hit=0.2395 cal_err=+0.2041 brier=0.2285 BSS=-0.25 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=168 pred=0.4839 hit=0.2083 cal_err=+0.2756 brier=0.2467 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=73 pred=0.5396 hit=0.4247 cal_err=+0.1149 brier=0.2606 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3233 actual=0.2121 gap=+0.1112`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=117 pred=0.4335 actual=0.2137 gap=+0.2198`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-21T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.50+: n=241 pred=0.5432 actual=0.2988 gap=+0.2444`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-09-21T06:00:12]
- key: `PAYOUT_RATIO_WEIRD|pid=2435 bet=300 odds=9.7 payout=360 ratio=0.12`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.77MB / last modified 2026-09-21T06:30:03.626169+09:00

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
64 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 23:55:04,664 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 23:55:04,719 [INFO] predictor: Models loaded OK
2026-09-20 23:55:04,723 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-20 23:56:03,419 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-20 23:56:03,419 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 23:56:03,419 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 23:56:03,465 [INFO] predictor: Models loaded OK
2026-09-20 23:56:03,469 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-20 23:57:04,412 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-09-20 23:57:04,412 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 23:57:04,412 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 23:57:04,461 [INFO] predictor: Models loaded OK
2026-09-20 23:57:04,465 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-20 23:58:04,184 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-09-20 23:58:04,184 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 23:58:04,184 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 23:58:04,218 [INFO] predictor: Models loaded OK
2026-09-20 23:58:04,221 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-20 23:59:03,470 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-09-20 23:59:03,470 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-20 23:59:03,470 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-20 23:59:03,521 [INFO] predictor: Models loaded OK
2026-09-20 23:59:03,523 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 10, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 148
  FINAL_MISSING: 85
  PSI_DRIFT_DETECTED: 45
  CIRCUIT_BREAKER_TRIP: 18
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 10 | 12,000 | 8,190 | -3,810 | 0.682 |
| S01_NAKAANA1 | 37 | 11 | 7,400 | 7,600 | +200 | 1.027 |
| S02_TETSUBAN | 15 | 9 | 3,000 | 3,520 | +520 | 1.173 |

## 直近アラート (24h・新しい順)
```
[06:00:08] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:08] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 8190, "roi_7d": 0.682, "sid": "S00"}
[06:00:08] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 92, "psi": 0.314}
[06:00:08] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:55:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 92, "psi": 0.314}
[23:55:04] FINAL_MISSING: {"deadline": "2026-09-20T12:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092013051220", "sid": "S00"}
[23:55:04] FINAL_MISSING: {"deadline": "2026-09-20T16:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092001031622", "sid": "S00"}
[23:51:04] FINAL_MISSING: {"deadline": "2026-09-20T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092002041214", "sid": "S00"}
[23:47:04] FINAL_MISSING: {"deadline": "2026-09-20T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092002061314", "sid": "S00"}
[23:23:04] FINAL_MISSING: {"deadline": "2026-09-20T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092002011047", "sid": "S01_NAKAANA1"}
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
| S01_NAKAANA1 | 243R | win | 1 | 0.4989 | 3.4 | 1.70 | 200 | scan=4.8 drift=-29.2% | 18:31:18 |
| S01_NAKAANA1 | 128R | win | 1 | 0.5059 | 3.3 | 1.67 | 200 | scan=4.1 drift=-19.5% | 18:22:19 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=3.0 drift=+3.3% | 16:45:20 |
| S02_TETSUBAN | 169R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=- drift=- | 15:07:20 |
| S01_NAKAANA1 | 037R | win | 1 | 0.5891 | 3.2 | 1.89 | 200 | scan=- drift=- | 13:53:31 |
| S02_TETSUBAN | 135R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 12:17:21 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 12:11:45 |
| S01_NAKAANA1 | 032R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.5 drift=-20.0% | 11:38:20 |
| S01_NAKAANA1 | 173R | win | 1 | 0.3177 | 4.7 | 1.49 | 200 | scan=3.4 drift=+38.2% | 11:34:19 |
| S01_NAKAANA1 | 146R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.1 drift=+12.9% | 10:49:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +2.7% | -81.7% | +119.5% | 14 | 5 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 536.2s |
| **Latency** (scan→final max) | 622.9s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4774 | 0.2598 | +0.2176 | 🟡+46% | 0.2418 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4436 | 0.2395 | 0.2285 | 🔴-0.25 | 0.756 |
| S01_NAKAANA1 | win | 168 | 0.4839 | 0.2083 | 0.2467 | 🔴-0.50 | 0.627 |
| S02_TETSUBAN | win | 73 | 0.5396 | 0.4247 | 0.2606 | 🔴-0.07 | 0.756 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 150 | 0.4092 | 0.2133 | 🔴+0.1959 |
| 0.50+ | 241 | 0.5432 | 0.2988 | 🔴+0.2444 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 147 | 0.772 |
| win | <5.0 | ✅learned | 259 | 0.762 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-21T06:50:01.515331+09:00_