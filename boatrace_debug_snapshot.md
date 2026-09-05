# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-05T11:50:01.806947+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 CALIBRATION_DRIFT×30 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×14 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-05T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×45  [2026-09-05T11:03:28]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×45  [2026-09-05T11:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×45  [2026-09-05T11:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-09-05T11:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-09-05T10:47:54]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-09-05T10:11:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×46  [2026-09-05T10:00:50]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-05T06:00:11]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1266 actual=0.0000 gap=+0.1266`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S00: n=185 hit%=27.0% hit_CI[Bonf]=[18.7,37.3]% ROI=0.90 ROI_boot95=[0.64,1.22]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=22.6% hit_CI[Bonf]=[15.1,32.4]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=38.3% hit_CI[Bonf]=[24.5,54.3]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-05T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=14.3% ROI=0.38 (コスト 10,100/回収 3,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-05T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=29.3% ROI=0.95 (コスト 9,600/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-05T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=99 hit%=27.3% ROI=0.98 (コスト 22,900/回収 22,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.35MB / last modified 2026-09-05T11:49:27.610271+09:00

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
n
2026-09-05 11:48:29,664 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-05 11:48:29,668 [INFO] run_cycle: fetched 10/8 [final]: 156 combos
2026-09-05 11:48:32,132 [WARNING] scraper: beforeinfo parse failed: jcd=13 rno=4
2026-09-05 11:48:32,132 [WARNING] run_cycle: fetch None: 13/4
2026-09-05 11:48:32,132 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-05 11:49:04,536 [INFO] run_cycle: === run_cycle 11:49:04 ===
2026-09-05 11:49:04,536 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-05 11:49:04,536 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-05 11:49:04,569 [INFO] predictor: Models loaded OK
2026-09-05 11:49:17,068 [INFO] scraper: odds3t: 120/120 parsed
2026-09-05 11:49:18,137 [INFO] scraper: odds3f: 20/20 parsed
2026-09-05 11:49:19,237 [INFO] scraper: odds2t: 30/30 parsed
2026-09-05 11:49:19,238 [INFO] scraper: odds2f: 13/15 parsed
2026-09-05 11:49:20,303 [INFO] scraper: odds_win: 3/6 parsed
2026-09-05 11:49:20,303 [INFO] scraper: fetch_race 13/4: boats=6 odds=186/191
2026-09-05 11:49:20,306 [INFO] predictor: CALIBRATION_MODE=on
2026-09-05 11:49:20,306 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-05 11:49:20,310 [INFO] run_cycle: fetched 13/4 [scan]: 153 combos
2026-09-05 11:49:23,784 [INFO] scraper: odds3t: 120/120 parsed
2026-09-05 11:49:24,887 [INFO] scraper: odds3f: 20/20 parsed
2026-09-05 11:49:26,012 [INFO] scraper: odds2t: 30/30 parsed
2026-09-05 11:49:26,013 [INFO] scraper: odds2f: 11/15 parsed
2026-09-05 11:49:27,121 [INFO] scraper: odds_win: 4/6 parsed
2026-09-05 11:49:27,121 [INFO] scraper: fetch_race 11/4: boats=6 odds=185/191
2026-09-05 11:49:27,124 [INFO] predictor: CALIBRATION_MODE=on
2026-09-05 11:49:27,125 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-05 11:49:27,129 [INFO] run_cycle: fetched 11/4 [scan]: 154 combos
2026-09-05 11:49:27,283 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 13, 'scan': 26}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 54
  CALIBRATION_DRIFT: 30
  ANOMALY_SCRAPER_FAILURE_BURST: 28
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 14
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 12 | 14,400 | 12,420 | -1,980 | 0.863 |
| S01_NAKAANA1 | 38 | 3 | 7,600 | 1,560 | -6,040 | 0.205 |
| S02_TETSUBAN | 12 | 4 | 2,400 | 1,800 | -600 | 0.75 |

## 直近アラート (24h・新しい順)
```
[11:43:47] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 1560, "roi_7d": 0.205, "sid": "S01_NAKAANA1"}
[11:38:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.273, "baseline_mean": 0.844, "baseline_stdev": 0.131, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.09}
[11:29:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.344, "baseline_mean": 0.844, "baseline_stdev": 0.131, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -2.64}
[11:27:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.244, "baseline_mean": 0.844, "baseline_stdev": 0.131, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -1.87}
[11:25:31] CALIBRATION_DRIFT: {"avg_actual": 0.2021, "avg_pred": 0.4723, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 94, "overconf_pct": 57.2}
[11:21:42] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 1560, "roi_7d": 0.211, "sid": "S01_NAKAANA1"}
[11:18:00] FINAL_MISSING: {"deadline": "2026-09-05T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090502011047", "sid": "S01_NAKAANA1"}
[11:11:59] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.344, "baseline_mean": 0.844, "baseline_stdev": 0.131, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -2.64}
[11:03:27] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:03:27] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 134件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 34件 締切済
- 通知発射: scan=7 nid / final=5 nid / result=2 nid
- predictions: 6 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 023R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=- drift=- | 11:43:30 |
| S00 | 023R | win | 1 | 0.5123 | 8.1 | 4.15 | 300 | scan=33.0 drift=-75.5% | 11:42:20 |
| S02_TETSUBAN | 133R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=2.2 drift=+0.0% | 11:34:32 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5476 | 4.7 | 2.57 | 200 | scan=4.0 drift=+17.5% | 11:21:27 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=3.1 drift=+12.9% | 10:52:26 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5890 | 3.6 | 2.12 | 200 | scan=3.0 drift=+20.0% | 10:47:29 |
| S02_TETSUBAN | 205R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=- drift=- | 17:14:42 |
| S01_NAKAANA1 | 123R | win | 1 | 0.3177 | 4.1 | 1.30 | 200 | scan=- drift=- | 16:06:29 |
| S00 | 072R | win | 1 | 0.5891 | 10.5 | 6.19 | 300 | scan=5.2 drift=+101.9% | 15:47:19 |
| S00 | 122R | win | 1 | 0.2290 | 8.2 | 1.88 | 300 | scan=5.2 drift=+57.7% | 15:38:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +10.7% | -75.5% | +158.3% | 11 | 8 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 410.7s |
| **Latency** (scan→final max) | 603.8s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4741 | 0.2703 | +0.2038 | 🟡+43% | 0.2407 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4256 | 0.2717 | 0.2202 | 🔴-0.11 | 0.907 |
| S01_NAKAANA1 | win | 190 | 0.4888 | 0.2211 | 0.2499 | 🔴-0.45 | 0.7 |
| S02_TETSUBAN | win | 81 | 0.5498 | 0.3827 | 0.2654 | 🔴-0.12 | 0.659 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 10 | 0.2255 | 0.2000 | ✅+0.0255 |
| 0.30-0.50 | 158 | 0.4071 | 0.2342 | 🔴+0.1729 |
| 0.50+ | 268 | 0.5462 | 0.3022 | 🔴+0.2440 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 115 | 0.468 |
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
_auto-generated by claude_snapshot.py at 2026-09-05T11:50:01.806947+09:00_