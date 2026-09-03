# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-03T11:20:01.323988+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×47 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×47 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×13 (24h)
- 🔴 CALIBRATION_DRIFT×10 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-09-03T11:03:20]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-09-03T11:02:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-09-03T11:02:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×18  [2026-09-03T11:02:20]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-09-03T11:02:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-03T11:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×43  [2026-09-03T09:49:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S00: n=185 hit%=26.5% hit_CI[Bonf]=[18.3,36.7]% ROI=0.87 ROI_boot95=[0.63,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S01_NAKAANA1: n=191 hit%=24.1% hit_CI[Bonf]=[16.4,34.0]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=191<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=40.0% hit_CI[Bonf]=[25.9,56.0]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-03T06:00:42]
- key: `ORPHAN_SCAN|191 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=15.8% ROI=0.48 (コスト 11,000/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=97 hit%=26.8% ROI=0.89 (コスト 22,200/回収 19,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=51 hit%=23.5% ROI=0.46 (コスト 11,500/回収 5,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.2MB / last modified 2026-09-03T11:19:33.441067+09:00

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
2026-09-03 11:19:03,471 [INFO] predictor: Models loaded OK
2026-09-03 11:19:15,901 [INFO] scraper: odds3t: 120/120 parsed
2026-09-03 11:19:17,008 [INFO] scraper: odds3f: 20/20 parsed
2026-09-03 11:19:18,084 [INFO] scraper: odds2t: 30/30 parsed
2026-09-03 11:19:18,086 [INFO] scraper: odds2f: 15/15 parsed
2026-09-03 11:19:19,189 [INFO] scraper: odds_win: 5/6 parsed
2026-09-03 11:19:19,189 [INFO] scraper: fetch_race 16/1: boats=6 odds=190/191
2026-09-03 11:19:19,194 [INFO] predictor: CALIBRATION_MODE=on
2026-09-03 11:19:19,194 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-03 11:19:19,200 [INFO] run_cycle: fetched 16/1 [final]: 155 combos
2026-09-03 11:19:22,749 [INFO] scraper: odds3t: 120/120 parsed
2026-09-03 11:19:23,856 [INFO] scraper: odds3f: 20/20 parsed
2026-09-03 11:19:24,941 [INFO] scraper: odds2t: 24/30 parsed
2026-09-03 11:19:24,942 [INFO] scraper: odds2f: 12/15 parsed
2026-09-03 11:19:26,035 [INFO] scraper: odds_win: 2/6 parsed
2026-09-03 11:19:26,036 [INFO] scraper: fetch_race 08/3: boats=6 odds=178/191
2026-09-03 11:19:26,038 [INFO] predictor: CALIBRATION_MODE=on
2026-09-03 11:19:26,038 [INFO] predictor: combos: {'win': 2, '2t': 24, '3t': 120}
2026-09-03 11:19:26,042 [INFO] run_cycle: fetched 08/3 [scan]: 146 combos
2026-09-03 11:19:29,486 [INFO] scraper: odds3t: 120/120 parsed
2026-09-03 11:19:30,595 [INFO] scraper: odds3f: 20/20 parsed
2026-09-03 11:19:31,710 [INFO] scraper: odds2t: 30/30 parsed
2026-09-03 11:19:31,711 [INFO] scraper: odds2f: 13/15 parsed
2026-09-03 11:19:32,813 [INFO] scraper: odds_win: 6/6 parsed
2026-09-03 11:19:32,813 [INFO] scraper: fetch_race 18/7: boats=6 odds=189/191
2026-09-03 11:19:32,815 [INFO] predictor: CALIBRATION_MODE=on
2026-09-03 11:19:32,815 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-03 11:19:32,819 [INFO] run_cycle: fetched 18/7 [scan]: 156 combos
2026-09-03 11:19:32,931 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 19, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 108
  PSI_DRIFT_DETECTED: 47
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  FINAL_MISSING: 13
  CALIBRATION_DRIFT: 10
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 15 | 15,600 | 13,170 | -2,430 | 0.844 |
| S01_NAKAANA1 | 37 | 6 | 7,400 | 2,820 | -4,580 | 0.381 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,660 | -740 | 0.782 |

## 直近アラート (24h・新しい順)
```
[11:17:51] FINAL_MISSING: {"deadline": "2026-09-03T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090302011047", "sid": "S00"}
[11:13:31] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.203, "baseline_mean": 0.87, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.04}
[11:03:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.537, "baseline_mean": 0.87, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -5.39}
[11:02:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:49:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 701}
[10:48:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 693}
[10:47:16] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 2820, "roi_7d": 0.381, "sid": "S01_NAKAANA1"}
[10:47:16] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 348, "n_recent": 106, "psi": 0.327}
[10:47:16] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 685}
```

## 本日残レース: 146件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 22件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 184R | win | 1 | 0.5476 | 5.5 | 3.01 | 300 | scan=5.5 drift=+0.0% | 09:59:20 |
| S00 | 129R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=- drift=- | 18:52:18 |
| S00 | 206R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=12.7 drift=-38.6% | 17:31:18 |
| S00 | 126R | win | 1 | 0.3177 | 7.4 | 2.35 | 300 | scan=4.1 drift=+80.5% | 17:26:18 |
| S00 | 204R | win | 1 | 0.3177 | 4.1 | 1.30 | 300 | scan=- drift=- | 16:34:29 |
| S00 | 123R | win | 1 | 0.3177 | 14.3 | 4.54 | 300 | scan=- drift=- | 16:03:25 |
| S00 | 179R | win | 1 | 0.0448 | 4.2 | 0.19 | 300 | scan=- drift=- | 15:01:19 |
| S02_TETSUBAN | 168R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 14:53:19 |
| S00 | 227R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=4.8 drift=+2.1% | 14:40:43 |
| S01_NAKAANA1 | 057R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 14:29:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +9.1% | -73.7% | +158.3% | 16 | 10 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.0s |
| **Latency** (scan→final max) | 600.8s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 454 | 0.4729 | 0.2819 | +0.1909 | 🟡+40% | 0.2407 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4229 | 0.2717 | 0.2208 | 🔴-0.12 | 0.88 |
| S01_NAKAANA1 | win | 190 | 0.4885 | 0.2421 | 0.2499 | 🔴-0.36 | 0.738 |
| S02_TETSUBAN | win | 80 | 0.5506 | 0.4000 | 0.2646 | 🔴-0.10 | 0.682 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1233 | 0.0000 | 🔴+0.1233 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 159 | 0.4053 | 0.2453 | 🔴+0.1600 |
| 0.50+ | 266 | 0.5464 | 0.3158 | 🔴+0.2306 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 113 | 0.456 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-03T11:20:01.323988+09:00_