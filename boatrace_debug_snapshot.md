# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-08T11:20:01.701854+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×68 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×68 (24h)
- 🟡 FINAL_MISSING×67 (24h)
- 🔴 CALIBRATION_DRIFT×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×15  [2026-06-08T11:05:29]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CALIBRATION_DRIFT  ×17  [2026-06-08T11:03:06]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×51  [2026-06-08T11:03:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×51  [2026-06-08T11:03:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-06-08T11:03:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×44  [2026-06-08T10:36:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-06-08T10:32:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-08T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-08T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S00: n=154 hit%=24.7% hit_CI[Bonf]=[16.1,35.8]% ROI=0.76 ROI_boot95=[0.52,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=27.0% hit_CI[Bonf]=[17.7,38.8]% ROI=0.67 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.72 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-08T06:00:10]
- key: `ORPHAN_SCAN|206 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-08T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=42 hit%=28.6% ROI=0.80 (コスト 12,200/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.65MB / last modified 2026-06-08T11:19:29.350625+09:00

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
arsed
2026-06-08 11:18:23,125 [INFO] scraper: fetch_race 18/7: boats=6 odds=186/191
2026-06-08 11:18:23,138 [INFO] predictor: CALIBRATION_MODE=on
2026-06-08 11:18:23,138 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-06-08 11:18:23,146 [INFO] run_cycle: fetched 18/7 [scan]: 151 combos
2026-06-08 11:18:23,281 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-08 11:19:06,173 [INFO] run_cycle: === run_cycle 11:19:06 ===
2026-06-08 11:19:06,173 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-08 11:19:06,173 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 11:19:06,247 [INFO] predictor: Models loaded OK
2026-06-08 11:19:17,942 [INFO] scraper: odds3t: 120/120 parsed
2026-06-08 11:19:19,104 [INFO] scraper: odds3f: 18/20 parsed
2026-06-08 11:19:20,309 [INFO] scraper: odds2t: 27/30 parsed
2026-06-08 11:19:20,310 [INFO] scraper: odds2f: 13/15 parsed
2026-06-08 11:19:21,503 [INFO] scraper: odds_win: 4/6 parsed
2026-06-08 11:19:21,504 [INFO] scraper: fetch_race 08/3: boats=6 odds=182/191
2026-06-08 11:19:21,516 [INFO] predictor: CALIBRATION_MODE=on
2026-06-08 11:19:21,516 [INFO] predictor: combos: {'win': 4, '2t': 27, '3t': 120}
2026-06-08 11:19:21,523 [INFO] run_cycle: fetched 08/3 [scan]: 151 combos
2026-06-08 11:19:25,375 [INFO] scraper: odds3t: 120/120 parsed
2026-06-08 11:19:26,653 [INFO] scraper: odds3f: 20/20 parsed
2026-06-08 11:19:27,773 [INFO] scraper: odds2t: 30/30 parsed
2026-06-08 11:19:27,774 [INFO] scraper: odds2f: 15/15 parsed
2026-06-08 11:19:28,958 [INFO] scraper: odds_win: 6/6 parsed
2026-06-08 11:19:28,958 [INFO] scraper: fetch_race 10/7: boats=6 odds=191/191
2026-06-08 11:19:28,967 [INFO] predictor: CALIBRATION_MODE=on
2026-06-08 11:19:28,967 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-08 11:19:28,975 [INFO] run_cycle: fetched 10/7 [scan]: 156 combos
2026-06-08 11:19:29,226 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 21, 'result': 18, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 183
  CIRCUIT_BREAKER_TRIP: 68
  FINAL_MISSING: 67
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 38
  ANOMALY_BET_VOLUME_SPIKE: 22
  ANOMALY_SCAN_FINAL_RATIO: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 27 | 5 | 8,100 | 3,720 | -4,380 | 0.459 |
| S01_NAKAANA1 | 26 | 2 | 5,200 | 580 | -4,620 | 0.112 |
| S02_TETSUBAN | 25 | 6 | 5,000 | 1,680 | -3,320 | 0.336 |

## 直近アラート (24h・新しい順)
```
[11:19:29] FINAL_MISSING: {"deadline": "2026-06-08T10:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060821061049", "sid": "S00"}
[11:16:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.443, "baseline_mean": 0.843, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -6.62}
[11:10:36] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 580, "roi_7d": 0.112, "sid": "S01_NAKAANA1"}
[11:05:29] CIRCUIT_BREAKER_TRIP: {"cost": 8100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 3720, "roi_7d": 0.459, "sid": "S00"}
[11:05:29] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 300, "n_recent": 78, "psi": 0.324}
[11:05:29] CALIBRATION_DRIFT: {"avg_actual": 0.1667, "avg_pred": 0.4882, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 78, "overconf_pct": 65.9}
[11:02:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:21] CIRCUIT_BREAKER_TRIP: {"cost": 5000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 25, "payout": 1680, "roi_7d": 0.336, "sid": "S02_TETSUBAN"}
[11:02:21] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 3720, "roi_7d": 0.443, "sid": "S00"}
[11:02:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 117件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 27件 締切済
- 通知発射: scan=5 nid / final=2 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 0710R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=- drift=- | 19:47:21 |
| S02_TETSUBAN | 076R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 18:01:22 |
| S02_TETSUBAN | 073R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.5 drift=-16.0% | 16:38:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=- drift=- | 16:01:21 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 15:22:20 |
| S01_NAKAANA1 | 058R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.5 drift=-5.7% | 15:04:32 |
| S00 | 056R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=- drift=- | 14:01:20 |
| S02_TETSUBAN | 2112R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=2.5 drift=+0.0% | 13:56:20 |
| S00 | 055R | win | 1 | 0.2290 | 45.0 | 10.31 | 300 | scan=- drift=- | 13:29:43 |
| S02_TETSUBAN | 2111R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 13:21:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 37 | +5.8% | -62.9% | +274.6% | 13 | 7 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.3s |
| **Latency** (scan→final max) | 653.4s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 378 | 0.4686 | 0.2884 | +0.1803 | 🟡+38% | 0.2382 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 154 | 0.4238 | 0.2468 | 0.2203 | 🔴-0.19 | 0.76 |
| S01_NAKAANA1 | win | 141 | 0.4851 | 0.2695 | 0.2436 | 🔴-0.24 | 0.673 |
| S02_TETSUBAN | win | 83 | 0.5237 | 0.3976 | 0.2624 | 🔴-0.10 | 0.717 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 151 | 0.4203 | 0.2384 | 🔴+0.1818 |
| 0.50+ | 204 | 0.5414 | 0.3382 | 🔴+0.2031 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 33 | 0.747 |
| win | <5.0 | ✅learned | 59 | 0.732 |
| win | <10.0 | ✅learned | 40 | 0.525 |
| win | <20.0 | ✅learned | 12 | 0.197 |
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
_auto-generated by claude_snapshot.py at 2026-06-08T11:20:01.701854+09:00_