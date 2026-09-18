# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-18T11:40:01.846089+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×67 (24h)
- 🔴 PSI_DRIFT_DETECTED×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×16 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×37  [2026-09-18T11:02:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×37  [2026-09-18T11:02:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×37  [2026-09-18T11:02:30]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-09-18T11:02:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-18T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×45  [2026-09-18T10:54:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-09-18T10:19:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×13  [2026-09-18T10:00:41]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-18T06:01:21]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-18T06:01:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-18T06:01:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-18T06:01:21]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-18T06:01:21]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-18T06:01:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.85 (コスト 9,200/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-18T06:01:21]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2221 actual=0.0000 gap=+0.2221`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-18T06:01:21]
- key: `ROI_STAT|S00: n=176 hit%=25.0% hit_CI[Bonf]=[16.9,35.4]% ROI=0.81 ROI_boot95=[0.56,1.09]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-18T06:01:21]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=23.5% hit_CI[Bonf]=[15.5,34.0]% ROI=0.66 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-18T06:01:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-18T06:01:21]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=39.0% hit_CI[Bonf]=[24.8,55.3]% ROI=0.73 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-18T06:01:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=22.2% ROI=0.60 (コスト 10,500/回収 6,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.49MB / last modified 2026-09-18T11:39:36.312217+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-18 11:39:04,804 [INFO] predictor: Models loaded OK
2026-09-18 11:39:17,180 [INFO] scraper: odds3t: 120/120 parsed
2026-09-18 11:39:18,252 [INFO] scraper: odds3f: 20/20 parsed
2026-09-18 11:39:19,355 [INFO] scraper: odds2t: 28/30 parsed
2026-09-18 11:39:19,357 [INFO] scraper: odds2f: 13/15 parsed
2026-09-18 11:39:20,422 [INFO] scraper: odds_win: 4/6 parsed
2026-09-18 11:39:20,422 [INFO] scraper: fetch_race 03/2: boats=6 odds=185/191
2026-09-18 11:39:20,426 [INFO] predictor: CALIBRATION_MODE=on
2026-09-18 11:39:20,426 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-09-18 11:39:20,430 [INFO] run_cycle: fetched 03/2 [final]: 152 combos
2026-09-18 11:39:24,282 [INFO] scraper: odds3t: 120/120 parsed
2026-09-18 11:39:25,350 [INFO] scraper: odds3f: 19/20 parsed
2026-09-18 11:39:26,544 [INFO] scraper: odds2t: 26/30 parsed
2026-09-18 11:39:26,545 [INFO] scraper: odds2f: 11/15 parsed
2026-09-18 11:39:27,623 [INFO] scraper: odds_win: 3/6 parsed
2026-09-18 11:39:27,624 [INFO] scraper: fetch_race 11/4: boats=6 odds=179/191
2026-09-18 11:39:27,626 [INFO] predictor: CALIBRATION_MODE=on
2026-09-18 11:39:27,626 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-09-18 11:39:27,630 [INFO] run_cycle: fetched 11/4 [scan]: 149 combos
2026-09-18 11:39:31,187 [INFO] scraper: odds3t: 120/120 parsed
2026-09-18 11:39:32,273 [INFO] scraper: odds3f: 20/20 parsed
2026-09-18 11:39:33,351 [INFO] scraper: odds2t: 26/30 parsed
2026-09-18 11:39:33,352 [INFO] scraper: odds2f: 10/15 parsed
2026-09-18 11:39:34,490 [INFO] scraper: odds_win: 2/6 parsed
2026-09-18 11:39:34,490 [INFO] scraper: fetch_race 04/3: boats=6 odds=178/191
2026-09-18 11:39:34,493 [INFO] predictor: CALIBRATION_MODE=on
2026-09-18 11:39:34,493 [INFO] predictor: combos: {'win': 2, '2t': 26, '3t': 120}
2026-09-18 11:39:34,496 [INFO] run_cycle: fetched 04/3 [scan]: 148 combos
2026-09-18 11:39:34,642 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 10, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 75
  FINAL_MISSING: 67
  PSI_DRIFT_DETECTED: 45
  CIRCUIT_BREAKER_NO_ACTION: 29
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 16
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 7 | 11,100 | 7,110 | -3,990 | 0.641 |
| S01_NAKAANA1 | 33 | 10 | 6,600 | 6,800 | +200 | 1.03 |
| S02_TETSUBAN | 13 | 7 | 2,600 | 2,880 | +280 | 1.108 |

## 直近アラート (24h・新しい順)
```
[11:37:39] FINAL_MISSING: {"deadline": "2026-09-18T11:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091817021107", "sid": "S00"}
[11:34:43] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.277, "baseline_mean": 0.777, "baseline_stdev": 0.104, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 8, "z_score": -2.66}
[11:32:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.402, "baseline_mean": 0.777, "baseline_stdev": 0.104, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.375, "today_scan_count": 8, "z_score": -3.87}
[11:28:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.348, "baseline_mean": 0.777, "baseline_stdev": 0.104, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.429, "today_scan_count": 7, "z_score": -3.35}
[11:20:38] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 340, "n_recent": 83, "psi": 0.615}
[11:17:39] FINAL_MISSING: {"deadline": "2026-09-18T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091802011047", "sid": "S00"}
[11:17:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1139}
[11:16:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1118}
[11:15:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[11:14:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
```

## 本日残レース: 147件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 33件 締切済
- 通知発射: scan=8 nid / final=5 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 113R | win | 1 | 0.5238 | 2.6 | 1.36 | 200 | scan=- drift=- | 11:20:21 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5719 | 4.6 | 2.63 | 200 | scan=4.6 drift=+0.0% | 11:13:26 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5345 | 3.5 | 1.87 | 200 | scan=3.3 drift=+6.1% | 10:13:20 |
| S00 | 245R | win | 1 | 0.4989 | 5.3 | 2.64 | 300 | scan=- drift=- | 19:28:31 |
| S01_NAKAANA1 | 242R | win | 1 | 0.5334 | 4.0 | 2.13 | 200 | scan=4.6 drift=-13.0% | 18:05:31 |
| S00 | 154R | win | 1 | 0.4989 | 6.7 | 3.34 | 300 | scan=6.7 drift=+0.0% | 16:33:20 |
| S02_TETSUBAN | 057R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=- drift=- | 13:27:21 |
| S02_TETSUBAN | 117R | win | 1 | 0.5612 | 2.0 | 1.12 | 200 | scan=- drift=- | 13:19:20 |
| S00 | 165R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 12:49:21 |
| S00 | 222R | win | 1 | 0.5174 | 7.5 | 3.88 | 300 | scan=7.5 drift=+0.0% | 12:11:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +5.6% | -80.2% | +119.5% | 13 | 2 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.3s |
| **Latency** (scan→final max) | 612.3s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 421 | 0.4780 | 0.2708 | +0.2072 | 🟡+43% | 0.2419 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4389 | 0.2471 | 0.2307 | 🔴-0.24 | 0.809 |
| S01_NAKAANA1 | win | 170 | 0.4874 | 0.2412 | 0.2440 | 🔴-0.33 | 0.689 |
| S02_TETSUBAN | win | 77 | 0.5455 | 0.3896 | 0.2628 | 🔴-0.11 | 0.732 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 6 | 0.2221 | 0.0000 | 🔴+0.2221 |
| 0.30-0.50 | 144 | 0.4105 | 0.2153 | 🔴+0.1952 |
| 0.50+ | 254 | 0.5455 | 0.3110 | 🔴+0.2345 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 142 | 0.777 |
| win | <5.0 | ✅learned | 255 | 0.76 |
| win | <10.0 | ✅learned | 122 | 0.466 |
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
_auto-generated by claude_snapshot.py at 2026-09-18T11:40:01.846089+09:00_