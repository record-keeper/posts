# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-05T16:40:04.088374+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×66 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×66 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×15 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-06-05T16:12:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×108  [2026-06-05T16:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×108  [2026-06-05T16:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-06-05T16:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-05T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×59  [2026-06-05T15:40:32]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-05T09:00:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-05T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-05T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1957 actual=0.1667 gap=+0.0291`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-05T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-05T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-05T06:00:08]
- key: `ROI_STAT|S00: n=151 hit%=27.8% hit_CI[Bonf]=[18.7,39.3]% ROI=0.85 ROI_boot95=[0.59,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-05T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=126 hit%=30.2% hit_CI[Bonf]=[19.9,42.9]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-05T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=126<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-05T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=43.1% hit_CI[Bonf]=[27.8,59.7]% ROI=0.78 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-05T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-05T06:00:08]
- key: `ORPHAN_SCAN|209 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-05T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=42 hit%=31.0% ROI=0.87 (コスト 12,200/回収 10,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.35MB / last modified 2026-06-05T16:39:27.654299+09:00

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
_cycle done: 0 notifications
2026-06-05 16:39:05,353 [INFO] run_cycle: === run_cycle 16:39:05 ===
2026-06-05 16:39:05,353 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-05 16:39:05,353 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-05 16:39:05,407 [INFO] predictor: Models loaded OK
2026-06-05 16:39:17,062 [INFO] scraper: odds3t: 120/120 parsed
2026-06-05 16:39:18,167 [INFO] scraper: odds3f: 20/20 parsed
2026-06-05 16:39:19,281 [INFO] scraper: odds2t: 30/30 parsed
2026-06-05 16:39:19,282 [INFO] scraper: odds2f: 15/15 parsed
2026-06-05 16:39:20,445 [INFO] scraper: odds_win: 6/6 parsed
2026-06-05 16:39:20,446 [INFO] scraper: fetch_race 01/3: boats=6 odds=191/191
2026-06-05 16:39:20,457 [INFO] predictor: CALIBRATION_MODE=on
2026-06-05 16:39:20,457 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-05 16:39:20,465 [INFO] run_cycle: fetched 01/3 [final]: 156 combos
2026-06-05 16:39:24,077 [INFO] scraper: odds3t: 120/120 parsed
2026-06-05 16:39:25,202 [INFO] scraper: odds3f: 20/20 parsed
2026-06-05 16:39:26,292 [INFO] scraper: odds2t: 30/30 parsed
2026-06-05 16:39:26,293 [INFO] scraper: odds2f: 15/15 parsed
2026-06-05 16:39:27,365 [INFO] scraper: odds_win: 6/6 parsed
2026-06-05 16:39:27,365 [INFO] scraper: fetch_race 17/12: boats=6 odds=191/191
2026-06-05 16:39:27,374 [INFO] predictor: CALIBRATION_MODE=on
2026-06-05 16:39:27,374 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-05 16:39:27,382 [INFO] run_cycle: fetched 17/12 [scan]: 156 combos
2026-06-05 16:39:27,472 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-05 16:40:08,130 [INFO] run_cycle: === run_cycle 16:40:08 ===
2026-06-05 16:40:08,130 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-05 16:40:08,131 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-05 16:40:08,255 [INFO] predictor: Models loaded OK

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 11, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 269
  CIRCUIT_BREAKER_TRIP: 66
  CIRCUIT_BREAKER_NO_ACTION: 52
  STRATEGY_CI_FAIL: 17
  FINAL_MISSING: 15
  ANOMALY_SCAN_FINAL_RATIO: 12
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 7 | 9,600 | 3,750 | -5,850 | 0.391 |
| S01_NAKAANA1 | 30 | 9 | 6,000 | 3,780 | -2,220 | 0.63 |
| S02_TETSUBAN | 23 | 6 | 4,600 | 1,640 | -2,960 | 0.357 |

## 直近アラート (24h・新しい順)
```
[16:39:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 929}
[16:38:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 926}
[16:36:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 922}
[16:35:37] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 1640, "roi_7d": 0.357, "sid": "S02_TETSUBAN"}
[16:35:37] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -10.3, "final": 2.6, "kind": "LARGE_ODDS_DRIFT", "race": "073R", "scan": 2.9, "sid": "S02_TETSUBAN"}
[16:35:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 921}
[16:34:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 901}
[16:33:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 914}
[16:32:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 909}
[16:31:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 891}
```

## 本日残レース: 38件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 94件 締切済
- 通知発射: scan=16 nid / final=18 nid / result=8 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 073R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.9 drift=-10.3% | 16:35:21 |
| S02_TETSUBAN | 039R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:49:21 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.3177 | 4.8 | 1.53 | 200 | scan=- drift=- | 13:25:21 |
| S01_NAKAANA1 | 087R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=4.7 drift=+0.0% | 13:19:20 |
| S00 | 1810R | win | 1 | 0.4111 | 9.7 | 3.99 | 300 | scan=6.0 drift=+61.7% | 13:02:20 |
| S00 | 109R | win | 1 | 0.4111 | 4.7 | 1.93 | 300 | scan=7.9 drift=-40.5% | 12:19:21 |
| S00 | 219R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=4.5 drift=+2.2% | 12:16:21 |
| S00 | 083R | win | 1 | 0.5174 | 14.2 | 7.35 | 300 | scan=- drift=- | 11:22:32 |
| S00 | 216R | win | 1 | 0.4989 | 15.7 | 7.83 | 300 | scan=- drift=- | 10:44:46 |
| S01_NAKAANA1 | 2012R | win | 1 | 0.4989 | 4.2 | 2.10 | 200 | scan=3.2 drift=+31.2% | 20:28:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +21.0% | -61.1% | +432.7% | 11 | 5 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 504.5s |
| **Latency** (scan→final max) | 658.2s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 354 | 0.4639 | 0.3164 | +0.1475 | 🟡+32% | 0.2379 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 153 | 0.4195 | 0.2810 | 0.2232 | 🔴-0.10 | 0.843 |
| S01_NAKAANA1 | win | 128 | 0.4842 | 0.2969 | 0.2433 | 🔴-0.17 | 0.741 |
| S02_TETSUBAN | win | 73 | 0.5212 | 0.4247 | 0.2592 | 🔴-0.06 | 0.764 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 6 | 0.2216 | 0.5000 | 🔴-0.2784 |
| 0.30-0.50 | 142 | 0.4177 | 0.2676 | 🔴+0.1501 |
| 0.50+ | 187 | 0.5415 | 0.3690 | 🔴+0.1725 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 31 | 0.746 |
| win | <5.0 | ✅learned | 58 | 0.737 |
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
_auto-generated by claude_snapshot.py at 2026-06-05T16:40:04.088374+09:00_