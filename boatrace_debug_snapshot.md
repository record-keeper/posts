# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-27T09:40:01.545013+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×32 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×32 (24h)
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SNAPSHOT_STALE×10 (24h)
- 🔴 SEND_WITHOUT_DBREC×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×39  [2026-10-27T09:01:13]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×78  [2026-10-27T09:01:13]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-10-27T09:01:13]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-27T09:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-27T09:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-27T06:00:22]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=50 hit%=26.0% ROI=0.83 (コスト 12,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.60 (コスト 11,000/回収 6,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2288 actual=0.2222 gap=+0.0066`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S00: n=189 hit%=30.2% hit_CI[Bonf]=[21.5,40.5]% ROI=0.82 ROI_boot95=[0.62,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=33.7% hit_CI[Bonf]=[24.7,44.0]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=52.1% hit_CI[Bonf]=[35.9,67.8]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=44.4% ROI=1.24 (コスト 7,800/回収 9,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=41.9% ROI=1.13 (コスト 19,500/回収 22,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.85 (コスト 15,800/回収 13,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|bt=win: n=455 pred=0.4794 actual=0.3516 error=+0.1277 (+27%) brier=0.2393 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|S00(win): n=189 pred=0.4434 hit=0.3016 cal_err=+0.1419 brier=0.2348 BSS=-0.11 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.93MB / last modified 2026-10-27T09:39:04.331689+09:00

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
tus=204)
2026-10-27 09:36:33,897 [INFO] run_cycle: RETREAT S00 三国3R
2026-10-27 09:36:34,000 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 09:37:04,077 [INFO] run_cycle: === run_cycle 09:37:04 ===
2026-10-27 09:37:04,078 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 09:37:04,078 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 09:37:04,153 [INFO] predictor: Models loaded OK
2026-10-27 09:37:15,496 [INFO] scraper: odds3t: 120/120 parsed
2026-10-27 09:37:16,582 [INFO] scraper: odds3f: 20/20 parsed
2026-10-27 09:37:17,664 [INFO] scraper: odds2t: 30/30 parsed
2026-10-27 09:37:17,665 [INFO] scraper: odds2f: 14/15 parsed
2026-10-27 09:37:18,784 [INFO] scraper: odds_win: 6/6 parsed
2026-10-27 09:37:18,784 [INFO] scraper: fetch_race 10/3: boats=6 odds=190/191
2026-10-27 09:37:18,790 [INFO] predictor: CALIBRATION_MODE=on
2026-10-27 09:37:18,790 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-27 09:37:18,796 [INFO] run_cycle: fetched 10/3 [final]: 156 combos
2026-10-27 09:37:18,929 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 09:38:04,441 [INFO] run_cycle: === run_cycle 09:38:04 ===
2026-10-27 09:38:04,441 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 09:38:04,441 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 09:38:04,470 [INFO] predictor: Models loaded OK
2026-10-27 09:38:04,472 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 09:39:03,934 [INFO] run_cycle: === run_cycle 09:39:03 ===
2026-10-27 09:39:03,934 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 09:39:03,934 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 09:39:03,970 [INFO] predictor: Models loaded OK
2026-10-27 09:39:03,973 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 74
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 16, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 161
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 33
  CIRCUIT_BREAKER_TRIP: 32
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  SNAPSHOT_STALE: 10
  SEND_WITHOUT_DBREC: 8
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 13 | 13,200 | 10,230 | -2,970 | 0.775 |
| S01_NAKAANA1 | 49 | 10 | 9,800 | 3,760 | -6,040 | 0.384 |
| S02_TETSUBAN | 11 | 6 | 2,200 | 1,980 | -220 | 0.9 |

## 直近アラート (24h・新しい順)
```
[09:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:03] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 3760, "roi_7d": 0.384, "sid": "S01_NAKAANA1"}
[09:01:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[09:01:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[08:00:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:44] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 3760, "roi_7d": 0.384, "sid": "S01_NAKAANA1"}
[08:00:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[08:00:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:08] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:08] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 3760, "roi_7d": 0.384, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 162件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 6件 締切済
- 通知発射: scan=2 nid / final=2 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1511R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 19:56:19 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5334 | 3.6 | 1.92 | 200 | scan=4.6 drift=-21.7% | 16:45:21 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=4.5 drift=-17.8% | 16:03:23 |
| S02_TETSUBAN | 1112R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.3 drift=+0.0% | 15:56:18 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=- drift=- | 15:19:20 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 14:43:19 |
| S00 | 049R | win | 1 | 0.4989 | 7.8 | 3.89 | 300 | scan=6.7 drift=+16.4% | 14:38:19 |
| S02_TETSUBAN | 059R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:28:31 |
| S00 | 046R | win | 1 | 0.4111 | 10.2 | 4.19 | 300 | scan=24.7 drift=-58.7% | 13:10:23 |
| S00 | 225R | win | 1 | 0.4111 | 16.0 | 6.58 | 300 | scan=- drift=- | 12:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +13.6% | -77.4% | +369.8% | 13 | 4 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 444.9s |
| **Latency** (scan→final max) | 661.2s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 454 | 0.4791 | 0.3524 | +0.1267 | 🟡+26% | 0.2391 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 189 | 0.4434 | 0.3016 | 0.2348 | 🔴-0.11 | 0.822 |
| S01_NAKAANA1 | win | 193 | 0.4891 | 0.3368 | 0.2378 | 🔴-0.06 | 0.894 |
| S02_TETSUBAN | win | 72 | 0.5460 | 0.5278 | 0.2539 | 🔴-0.02 | 0.917 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2288 | 0.2222 | ✅+0.0066 |
| 0.30-0.50 | 159 | 0.4123 | 0.3145 | 🔴+0.0978 |
| 0.50+ | 272 | 0.5430 | 0.3897 | 🔴+0.1533 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 195 | 0.778 |
| win | <5.0 | ✅learned | 352 | 0.74 |
| win | <10.0 | ✅learned | 155 | 0.451 |
| win | <20.0 | ✅learned | 45 | 0.254 |
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
_auto-generated by claude_snapshot.py at 2026-10-27T09:40:01.545013+09:00_