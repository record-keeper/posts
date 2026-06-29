# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-30T01:50:01.387668+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 PSI_DRIFT_DETECTED×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-30T01:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×12  [2026-06-29T23:48:06]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-06-29T23:06:08]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-06-29T23:06:08]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×54  [2026-06-29T23:06:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-06-29T15:11:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×9  [2026-06-29T13:21:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 KS_ODDS_DRIFT  ×14  [2026-06-29T12:05:42]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-06-29T10:34:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-06-29T06:00:13]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-29T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S00: n=163 hit%=27.6% hit_CI[Bonf]=[18.8,38.6]% ROI=0.72 ROI_boot95=[0.52,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=139 hit%=30.2% hit_CI[Bonf]=[20.4,42.3]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-29T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=30.7% hit_CI[Bonf]=[17.9,47.3]% ROI=0.48 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-29T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=25.7% ROI=0.83 (コスト 10,100/回収 8,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-29T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=22.9% ROI=0.49 (コスト 8,300/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.44MB / last modified 2026-06-30T01:30:04.213894+09:00

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
03 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 23:55:06,503 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 23:55:06,588 [INFO] predictor: Models loaded OK
2026-06-29 23:55:06,602 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-29 23:56:06,470 [INFO] run_cycle: === run_cycle 23:56:06 ===
2026-06-29 23:56:06,470 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 23:56:06,470 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 23:56:06,511 [INFO] predictor: Models loaded OK
2026-06-29 23:56:06,516 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-29 23:57:06,169 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-29 23:57:06,169 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 23:57:06,169 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 23:57:06,212 [INFO] predictor: Models loaded OK
2026-06-29 23:57:06,216 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-29 23:58:05,804 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-06-29 23:58:05,805 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 23:58:05,805 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 23:58:05,847 [INFO] predictor: Models loaded OK
2026-06-29 23:58:05,851 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-29 23:59:05,861 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-29 23:59:05,861 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-29 23:59:05,862 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-29 23:59:05,928 [INFO] predictor: Models loaded OK
2026-06-29 23:59:05,933 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 104
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 104
  }
]
```

## Phase別通知記録 (24h)
{'final': 42, 'result': 20, 'scan': 42}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 63
  ANOMALY_SCRAPER_FAILURE_BURST: 42
  CIRCUIT_BREAKER_TRIP: 23
  PSI_DRIFT_DETECTED: 22
  ANOMALY_BET_VOLUME_SPIKE: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 11 | 13,500 | 8,070 | -5,430 | 0.598 |
| S01_NAKAANA1 | 39 | 18 | 7,800 | 8,980 | +1,180 | 1.151 |
| S02_TETSUBAN | 10 | 3 | 2,000 | 800 | -1,200 | 0.4 |

## 直近アラート (24h・新しい順)
```
[23:47:06] FINAL_MISSING: {"deadline": "2026-06-29T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062911041211", "sid": "S00"}
[23:45:06] FINAL_MISSING: {"deadline": "2026-06-29T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062903031208", "sid": "S00"}
[23:37:06] FINAL_MISSING: {"deadline": "2026-06-29T13:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062910101300", "sid": "S00"}
[23:34:06] FINAL_MISSING: {"deadline": "2026-06-29T15:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062917091500", "sid": "S00"}
[23:34:06] FINAL_MISSING: {"deadline": "2026-06-29T13:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062908081358", "sid": "S00"}
[23:25:06] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 8070, "roi_7d": 0.598, "sid": "S00"}
[23:06:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:06:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:01:06] FINAL_MISSING: {"deadline": "2026-06-29T14:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062917081426", "sid": "S00"}
[23:00:10] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 11.9, "baseline_n_days": 7, "baseline_stdev": 3.1, "hour": 23, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 20, "z_score": 2.65}
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
| S01_NAKAANA1 | 203R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=4.1 drift=-4.9% | 18:31:25 |
| S00 | 127R | win | 1 | 0.5123 | 5.5 | 2.82 | 300 | scan=- drift=- | 18:18:22 |
| S02_TETSUBAN | 0512R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=- drift=- | 17:18:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 15:25:24 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.4 drift=+8.3% | 15:19:29 |
| S00 | 029R | win | 1 | 0.5334 | 5.0 | 2.67 | 300 | scan=16.1 drift=-68.9% | 14:45:33 |
| S02_TETSUBAN | 119R | win | 1 | 0.5990 | 2.7 | 1.62 | 200 | scan=- drift=- | 14:43:23 |
| S01_NAKAANA1 | 099R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 14:40:48 |
| S00 | 117R | win | 1 | 0.5123 | 8.6 | 4.41 | 300 | scan=16.5 drift=-47.9% | 13:40:25 |
| S01_NAKAANA1 | 116R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=4.5 drift=-13.3% | 13:08:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +4.2% | -68.9% | +325.0% | 24 | 12 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 493.0s |
| **Latency** (scan→final max) | 617.1s |
| **Traffic** (notifications 24h) | 104 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 375 | 0.4815 | 0.2933 | +0.1882 | 🟡+39% | 0.2410 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4421 | 0.2687 | 0.2267 | 🔴-0.15 | 0.724 |
| S01_NAKAANA1 | win | 138 | 0.4924 | 0.3116 | 0.2428 | 🔴-0.13 | 0.841 |
| S02_TETSUBAN | win | 77 | 0.5439 | 0.3117 | 0.2672 | 🔴-0.25 | 0.481 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2269 | 0.0909 | 🔴+0.1360 |
| 0.30-0.50 | 126 | 0.4256 | 0.2540 | 🔴+0.1717 |
| 0.50+ | 225 | 0.5441 | 0.3289 | 🔴+0.2152 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 49 | 0.725 |
| win | <5.0 | ✅learned | 109 | 0.72 |
| win | <10.0 | ✅learned | 60 | 0.489 |
| win | <20.0 | ✅learned | 18 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-30T01:50:01.387668+09:00_