# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-17T09:30:01.988566+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 PSI_DRIFT_DETECTED×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×15 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-17T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×29  [2026-06-17T09:01:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×29  [2026-06-17T09:01:21]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×29  [2026-06-17T09:01:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×30  [2026-06-17T09:00:11]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-17T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-17T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=15.6% ROI=0.27 (コスト 7,100/回収 1,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-17T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-17T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=143<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-17T06:00:11]
- key: `ORPHAN_SCAN|134 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-17T06:00:11]
- key: `ROI_STAT|S00: n=143 hit%=27.3% hit_CI[Bonf]=[18.0,39.1]% ROI=0.84 ROI_boot95=[0.57,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-17T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=131 hit%=29.8% hit_CI[Bonf]=[19.7,42.2]% ROI=0.86 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-17T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=131<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-17T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=37.2% hit_CI[Bonf]=[23.4,53.5]% ROI=0.60 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-17T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-17T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=26.5% ROI=0.80 (コスト 9,900/回収 7,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-17T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=65 hit%=30.8% ROI=0.68 (コスト 15,400/回収 10,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-17T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=22.2% ROI=1.06 (コスト 8,100/回収 8,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-17T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=18.5% ROI=0.40 (コスト 7,600/回収 3,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-17T06:00:11]
- key: `CALIBRATION_LIVE|bt=win: n=352 pred=0.4710 actual=0.3040 error=+0.1670 (+35%) brier=0.2383 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.22MB / last modified 2026-06-17T09:30:04.773023+09:00

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
ault=5000
2026-06-17 09:26:05,294 [INFO] predictor: Models loaded OK
2026-06-17 09:26:05,496 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-17 09:27:06,663 [INFO] run_cycle: === run_cycle 09:27:06 ===
2026-06-17 09:27:06,663 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-17 09:27:06,663 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-17 09:27:06,717 [INFO] predictor: Models loaded OK
2026-06-17 09:27:18,218 [INFO] scraper: odds3t: 120/120 parsed
2026-06-17 09:27:19,385 [INFO] scraper: odds3f: 20/20 parsed
2026-06-17 09:27:20,490 [INFO] scraper: odds2t: 30/30 parsed
2026-06-17 09:27:20,491 [INFO] scraper: odds2f: 15/15 parsed
2026-06-17 09:27:21,567 [INFO] scraper: odds_win: 6/6 parsed
2026-06-17 09:27:21,568 [INFO] scraper: fetch_race 18/3: boats=6 odds=191/191
2026-06-17 09:27:21,580 [INFO] predictor: CALIBRATION_MODE=on
2026-06-17 09:27:21,580 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-17 09:27:21,587 [INFO] run_cycle: fetched 18/3 [scan]: 156 combos
2026-06-17 09:27:21,720 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-17 09:28:05,955 [INFO] run_cycle: === run_cycle 09:28:05 ===
2026-06-17 09:28:05,955 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-17 09:28:05,955 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-17 09:28:06,032 [INFO] predictor: Models loaded OK
2026-06-17 09:28:06,185 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-17 09:29:05,772 [INFO] run_cycle: === run_cycle 09:29:05 ===
2026-06-17 09:29:05,773 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-17 09:29:05,773 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-17 09:29:05,815 [INFO] predictor: Models loaded OK
2026-06-17 09:29:05,911 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 37
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 37
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 7, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 132
  FINAL_MISSING: 48
  PSI_DRIFT_DETECTED: 33
  ANOMALY_SCAN_FINAL_RATIO: 17
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 15
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 12 | 9,900 | 11,340 | +1,440 | 1.145 |
| S01_NAKAANA1 | 25 | 11 | 5,000 | 7,380 | +2,380 | 1.476 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 2,460 | -1,340 | 0.647 |

## 直近アラート (24h・新しい順)
```
[09:04:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 274, "n_recent": 77, "psi": 0.364}
[09:01:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 275, "n_recent": 77, "psi": 0.365}
[09:01:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[09:00:10] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.3, "baseline_n_days": 3, "baseline_stdev": 0.6, "hour": 9, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.31}
[08:00:41] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:41] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 275, "n_recent": 77, "psi": 0.365}
[08:00:41] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 275, "n_recent": 77, "psi": 0.365}
```

## 本日残レース: 151件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 5件 締切済
- 通知発射: scan=1 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 1612R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 16:47:23 |
| S00 | 098R | win | 1 | 0.4111 | 11.6 | 4.77 | 300 | scan=15.7 drift=-26.1% | 14:11:21 |
| S00 | 097R | win | 1 | 0.3177 | 4.1 | 1.30 | 300 | scan=- drift=- | 13:39:45 |
| S00 | 062R | win | 1 | 0.4111 | 5.8 | 2.38 | 300 | scan=- drift=- | 11:57:22 |
| S02_TETSUBAN | 032R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=2.3 drift=+21.7% | 11:38:33 |
| S00 | 186R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=27.7 drift=-58.5% | 10:55:34 |
| S01_NAKAANA1 | 103R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 09:28:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 200 | scan=3.7 drift=+29.7% | 15:54:23 |
| S00 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=4.5 drift=+6.7% | 15:54:21 |
| S01_NAKAANA1 | 224R | win | 1 | 0.5476 | 3.1 | 1.70 | 200 | scan=3.9 drift=-20.5% | 13:54:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | -6.3% | -82.9% | +87.5% | 18 | 10 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 513.0s |
| **Latency** (scan→final max) | 664.8s |
| **Traffic** (notifications 24h) | 37 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 351 | 0.4712 | 0.3048 | +0.1663 | 🟡+35% | 0.2385 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 142 | 0.4229 | 0.2746 | 0.2185 | 🔴-0.10 | 0.846 |
| S01_NAKAANA1 | win | 131 | 0.4850 | 0.2977 | 0.2450 | 🔴-0.17 | 0.856 |
| S02_TETSUBAN | win | 78 | 0.5358 | 0.3718 | 0.2641 | 🔴-0.13 | 0.601 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 8 | 0.2250 | 0.1250 | 🔴+0.1000 |
| 0.30-0.50 | 123 | 0.4178 | 0.2520 | 🔴+0.1658 |
| 0.50+ | 204 | 0.5410 | 0.3578 | 🔴+0.1832 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 43 | 0.717 |
| win | <5.0 | ✅learned | 78 | 0.755 |
| win | <10.0 | ✅learned | 51 | 0.498 |
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
_auto-generated by claude_snapshot.py at 2026-06-17T09:30:01.988566+09:00_