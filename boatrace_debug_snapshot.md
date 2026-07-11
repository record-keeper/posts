# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-11T11:00:03.124508+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×34 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×74 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×34 (24h)
- 🔴 PSI_DRIFT_DETECTED×17 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-11T11:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-11T11:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-07-11T10:55:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×22  [2026-07-11T10:38:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×118  [2026-07-11T10:01:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×118  [2026-07-11T10:01:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×59  [2026-07-11T10:01:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×59  [2026-07-11T10:01:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×9  [2026-07-11T09:00:12]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2291 actual=0.0769 gap=+0.1522`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3230 actual=0.1379 gap=+0.1850`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1743 actual=0.5000 gap=-0.3257`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-11T06:00:14]
- key: `ROI_STAT|S00: n=167 hit%=29.3% hit_CI[Bonf]=[20.3,40.3]% ROI=0.76 ROI_boot95=[0.56,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-11T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=149 hit%=30.9% hit_CI[Bonf]=[21.2,42.6]% ROI=0.86 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-11T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=45.2% hit_CI[Bonf]=[29.8,61.6]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-11T06:00:14]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=36.1% ROI=1.00 (コスト 10,500/回収 10,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.32MB / last modified 2026-07-11T11:00:05.916742+09:00

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
&hd=20260711: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-11 10:59:29,028 [INFO] scraper: odds3t: 120/120 parsed
2026-07-11 10:59:30,148 [INFO] scraper: odds3f: 20/20 parsed
2026-07-11 10:59:31,269 [INFO] scraper: odds2t: 30/30 parsed
2026-07-11 10:59:31,270 [INFO] scraper: odds2f: 15/15 parsed
2026-07-11 10:59:32,357 [INFO] scraper: odds_win: 6/6 parsed
2026-07-11 10:59:32,358 [INFO] scraper: fetch_race 14/6: boats=6 odds=191/191
2026-07-11 10:59:32,369 [INFO] predictor: CALIBRATION_MODE=on
2026-07-11 10:59:32,369 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-11 10:59:32,378 [INFO] run_cycle: fetched 14/6 [final]: 156 combos
2026-07-11 10:59:35,963 [INFO] scraper: odds3t: 120/120 parsed
2026-07-11 10:59:37,047 [INFO] scraper: odds3f: 20/20 parsed
2026-07-11 10:59:38,161 [INFO] scraper: odds2t: 30/30 parsed
2026-07-11 10:59:38,163 [INFO] scraper: odds2f: 13/15 parsed
2026-07-11 10:59:39,277 [INFO] scraper: odds_win: 4/6 parsed
2026-07-11 10:59:39,277 [INFO] scraper: fetch_race 08/2: boats=6 odds=187/191
2026-07-11 10:59:39,286 [INFO] predictor: CALIBRATION_MODE=on
2026-07-11 10:59:39,286 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-11 10:59:39,294 [INFO] run_cycle: fetched 08/2 [scan]: 154 combos
2026-07-11 10:59:42,729 [INFO] scraper: odds3t: 120/120 parsed
2026-07-11 10:59:43,841 [INFO] scraper: odds3f: 20/20 parsed
2026-07-11 10:59:44,926 [INFO] scraper: odds2t: 28/30 parsed
2026-07-11 10:59:44,927 [INFO] scraper: odds2f: 12/15 parsed
2026-07-11 10:59:46,041 [INFO] scraper: odds_win: 2/6 parsed
2026-07-11 10:59:46,041 [INFO] scraper: fetch_race 09/2: boats=6 odds=182/191
2026-07-11 10:59:46,048 [INFO] predictor: CALIBRATION_MODE=on
2026-07-11 10:59:46,048 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-07-11 10:59:46,056 [INFO] run_cycle: fetched 09/2 [scan]: 150 combos
2026-07-11 10:59:46,260 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 15, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 98
  FINAL_MISSING: 74
  CIRCUIT_BREAKER_TRIP: 34
  CIRCUIT_BREAKER_NO_ACTION: 32
  PSI_DRIFT_DETECTED: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 10 | 10,500 | 6,480 | -4,020 | 0.617 |
| S01_NAKAANA1 | 41 | 10 | 8,200 | 5,500 | -2,700 | 0.671 |
| S02_TETSUBAN | 22 | 13 | 4,400 | 5,020 | +620 | 1.141 |

## 直近アラート (24h・新しい順)
```
[10:59:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 873}
[10:58:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 859}
[10:57:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 854}
[10:56:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 845}
[10:55:57] FINAL_MISSING: {"deadline": "2026-07-11T09:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071110030924", "sid": "S00"}
[10:55:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 827}
[10:41:22] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6480, "roi_7d": 0.617, "sid": "S00"}
[10:41:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 290, "n_recent": 98, "psi": 0.578}
[10:41:22] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.214, "baseline_mean": 0.814, "baseline_stdev": 0.073, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.94}
[10:34:56] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.414, "baseline_mean": 0.814, "baseline_stdev": 0.073, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.4, "today_scan_count": 5, "z_score": -5.69}
```

## 本日残レース: 158件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 22件 締切済
- 通知発射: scan=5 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 106R | win | 1 | 0.0918 | 5.2 | 0.48 | 300 | scan=5.2 drift=+0.0% | 10:41:20 |
| S00 | 142R | win | 1 | 0.5436 | 5.2 | 2.83 | 300 | scan=5.5 drift=-5.5% | 09:09:20 |
| S02_TETSUBAN | 208R | win | 1 | 0.5269 | 2.5 | 1.32 | 200 | scan=2.4 drift=+4.2% | 18:51:21 |
| S01_NAKAANA1 | 206R | win | 1 | 0.4989 | 4.4 | 2.20 | 200 | scan=3.7 drift=+18.9% | 18:00:28 |
| S00 | 206R | win | 1 | 0.4989 | 4.4 | 2.20 | 300 | scan=- drift=- | 18:00:25 |
| S00 | 154R | win | 1 | 0.1371 | 27.7 | 3.80 | 300 | scan=- drift=- | 16:58:21 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5174 | 2.4 | 1.24 | 200 | scan=- drift=- | 15:14:23 |
| S00 | 028R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=- drift=- | 14:02:20 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.1 drift=+35.5% | 13:17:34 |
| S00 | 1011R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=8.2 drift=-48.8% | 13:17:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +5.5% | -73.3% | +246.2% | 17 | 7 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 399.3s |
| **Latency** (scan→final max) | 605.0s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 387 | 0.4768 | 0.3307 | +0.1461 | 🟡+31% | 0.2357 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4435 | 0.2952 | 0.2238 | 🔴-0.08 | 0.757 |
| S01_NAKAANA1 | win | 149 | 0.4824 | 0.3087 | 0.2388 | 🔴-0.12 | 0.862 |
| S02_TETSUBAN | win | 72 | 0.5421 | 0.4583 | 0.2567 | 🔴-0.03 | 0.818 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1743 | 0.5000 | 🔴-0.3257 |
| 0.20-0.30 | 13 | 0.2291 | 0.0769 | 🔴+0.1522 |
| 0.30-0.50 | 140 | 0.4184 | 0.2929 | 🔴+0.1255 |
| 0.50+ | 224 | 0.5426 | 0.3705 | 🔴+0.1720 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 68 | 0.76 |
| win | <5.0 | ✅learned | 126 | 0.716 |
| win | <10.0 | ✅learned | 70 | 0.467 |
| win | <20.0 | ✅learned | 19 | 0.212 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-11T11:00:03.124508+09:00_