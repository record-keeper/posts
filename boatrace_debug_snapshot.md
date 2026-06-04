# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-04T12:00:02.141325+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×20 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-04T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-04T11:50:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-06-04T11:03:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-06-04T11:03:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-06-04T11:03:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-04T09:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2227 actual=0.4286 gap=-0.2059`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S00: n=160 hit%=30.0% hit_CI[Bonf]=[20.7,41.2]% ROI=0.90 ROI_boot95=[0.65,1.20]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=123 hit%=30.1% hit_CI[Bonf]=[19.7,43.0]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=123<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=44.8% hit_CI[Bonf]=[28.8,61.9]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-04T06:00:14]
- key: `ORPHAN_SCAN|216 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=45 hit%=31.1% ROI=0.88 (コスト 13,100/回収 11,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=27.5% ROI=0.75 (コスト 8,700/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-04T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=30.3% ROI=0.72 (コスト 15,200/回収 10,970)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.17MB / last modified 2026-06-04T12:00:04.866436+09:00

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
&hd=20260604: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-04 11:59:29,200 [INFO] scraper: odds3t: 120/120 parsed
2026-06-04 11:59:30,308 [INFO] scraper: odds3f: 20/20 parsed
2026-06-04 11:59:31,423 [INFO] scraper: odds2t: 30/30 parsed
2026-06-04 11:59:31,424 [INFO] scraper: odds2f: 12/15 parsed
2026-06-04 11:59:32,510 [INFO] scraper: odds_win: 4/6 parsed
2026-06-04 11:59:32,510 [INFO] scraper: fetch_race 09/4: boats=6 odds=186/191
2026-06-04 11:59:32,521 [INFO] predictor: CALIBRATION_MODE=on
2026-06-04 11:59:32,521 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-04 11:59:32,529 [INFO] run_cycle: fetched 09/4 [final]: 154 combos
2026-06-04 11:59:36,095 [INFO] scraper: odds3t: 120/120 parsed
2026-06-04 11:59:37,226 [INFO] scraper: odds3f: 20/20 parsed
2026-06-04 11:59:38,316 [INFO] scraper: odds2t: 28/30 parsed
2026-06-04 11:59:38,317 [INFO] scraper: odds2f: 12/15 parsed
2026-06-04 11:59:39,441 [INFO] scraper: odds_win: 2/6 parsed
2026-06-04 11:59:39,441 [INFO] scraper: fetch_race 13/4: boats=6 odds=182/191
2026-06-04 11:59:39,449 [INFO] predictor: CALIBRATION_MODE=on
2026-06-04 11:59:39,449 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-06-04 11:59:39,457 [INFO] run_cycle: fetched 13/4 [scan]: 150 combos
2026-06-04 11:59:43,060 [INFO] scraper: odds3t: 120/120 parsed
2026-06-04 11:59:44,245 [INFO] scraper: odds3f: 20/20 parsed
2026-06-04 11:59:45,420 [INFO] scraper: odds2t: 30/30 parsed
2026-06-04 11:59:45,421 [INFO] scraper: odds2f: 15/15 parsed
2026-06-04 11:59:46,528 [INFO] scraper: odds_win: 5/6 parsed
2026-06-04 11:59:46,528 [INFO] scraper: fetch_race 03/3: boats=6 odds=190/191
2026-06-04 11:59:46,538 [INFO] predictor: CALIBRATION_MODE=on
2026-06-04 11:59:46,540 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-04 11:59:46,546 [INFO] run_cycle: fetched 03/3 [scan]: 155 combos
2026-06-04 11:59:46,726 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 6, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 174
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  FINAL_MISSING: 12
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 6 | 10,500 | 3,390 | -7,110 | 0.323 |
| S01_NAKAANA1 | 40 | 13 | 8,000 | 5,920 | -2,080 | 0.74 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 1,580 | -1,820 | 0.465 |

## 直近アラート (24h・新しい順)
```
[11:38:38] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 3390, "roi_7d": 0.323, "sid": "S00"}
[11:38:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.161, "baseline_mean": 0.839, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 5, "z_score": 2.4}
[11:28:39] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 3390, "roi_7d": 0.332, "sid": "S00"}
[11:28:39] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 73.1, "final": 9.0, "kind": "LARGE_ODDS_DRIFT", "race": "093R", "scan": 5.2, "sid": "S00"}
[11:28:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.161, "baseline_mean": 0.839, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.4}
[11:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:06] CIRCUIT_BREAKER_TRIP: {"cost": 9900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 3390, "roi_7d": 0.342, "sid": "S00"}
[11:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:00:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.161, "baseline_mean": 0.839, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.4}
[10:50:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.173, "baseline_mean": 0.839, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.57}
```

## 本日残レース: 112件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 32件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=0 nid
- predictions: 3 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 084R | win | 1 | 0.5735 | 7.0 | 4.01 | 300 | scan=- drift=- | 11:49:32 |
| S00 | 032R | win | 1 | 0.1957 | 7.1 | 1.39 | 300 | scan=12.7 drift=-44.1% | 11:38:29 |
| S00 | 093R | win | 1 | 0.4111 | 9.0 | 3.70 | 300 | scan=5.2 drift=+73.1% | 11:28:22 |
| S02_TETSUBAN | 209R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 19:06:21 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5990 | 3.0 | 1.80 | 200 | scan=- drift=- | 15:21:20 |
| S02_TETSUBAN | 139R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 14:45:22 |
| S02_TETSUBAN | 2110R | win | 1 | 0.4985 | 2.1 | 1.05 | 200 | scan=- drift=- | 12:48:21 |
| S00 | 133R | win | 1 | 0.1957 | 20.0 | 3.91 | 300 | scan=- drift=- | 11:36:32 |
| S01_NAKAANA1 | 113R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 11:34:20 |
| S02_TETSUBAN | 217R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 11:15:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +18.8% | -81.4% | +432.7% | 13 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 487.5s |
| **Latency** (scan→final max) | 598.0s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 346 | 0.4632 | 0.3266 | +0.1366 | 🟡+30% | 0.2374 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 156 | 0.4206 | 0.2949 | 0.2222 | 🔴-0.07 | 0.894 |
| S01_NAKAANA1 | win | 123 | 0.4872 | 0.3008 | 0.2462 | 🔴-0.17 | 0.759 |
| S02_TETSUBAN | win | 67 | 0.5183 | 0.4478 | 0.2564 | 🔴-0.04 | 0.809 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 7 | 0.2227 | 0.4286 | 🔴-0.2059 |
| 0.30-0.50 | 139 | 0.4192 | 0.2734 | 🔴+0.1458 |
| 0.50+ | 182 | 0.5404 | 0.3846 | 🔴+0.1557 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 30 | 0.748 |
| win | <5.0 | ✅learned | 56 | 0.752 |
| win | <10.0 | ✅learned | 39 | 0.52 |
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
_auto-generated by claude_snapshot.py at 2026-06-04T12:00:02.141325+09:00_