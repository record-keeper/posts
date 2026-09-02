# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-02T12:50:01.984851+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×24 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 CALIBRATION_DRIFT×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🟡 FINAL_MISSING×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×17  [2026-09-02T12:33:19]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-02T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-09-02T12:20:40]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-09-02T12:11:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×47  [2026-09-02T12:03:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×47  [2026-09-02T12:03:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-09-02T12:03:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-09-02T10:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=8 pred=0.1250 actual=0.0000 gap=+0.1250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S00: n=176 hit%=26.7% hit_CI[Bonf]=[18.3,37.2]% ROI=0.88 ROI_boot95=[0.62,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=23.3% hit_CI[Bonf]=[15.7,33.1]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=40.7% hit_CI[Bonf]=[26.6,56.6]% ROI=0.70 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-02T06:00:17]
- key: `ORPHAN_SCAN|196 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=15.4% ROI=0.47 (コスト 11,300/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.91 (コスト 10,000/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=96 hit%=27.1% ROI=0.90 (コスト 22,000/回収 19,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.11MB / last modified 2026-09-02T12:49:04.010543+09:00

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
RATION_MODE=on
2026-09-02 12:47:25,063 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-02 12:47:25,068 [INFO] run_cycle: fetched 21/10 [scan]: 156 combos
2026-09-02 12:47:28,665 [INFO] scraper: odds3t: 120/120 parsed
2026-09-02 12:47:29,798 [INFO] scraper: odds3f: 20/20 parsed
2026-09-02 12:47:30,918 [INFO] scraper: odds2t: 30/30 parsed
2026-09-02 12:47:30,919 [INFO] scraper: odds2f: 15/15 parsed
2026-09-02 12:47:32,019 [INFO] scraper: odds_win: 6/6 parsed
2026-09-02 12:47:32,020 [INFO] scraper: fetch_race 05/4: boats=6 odds=191/191
2026-09-02 12:47:32,023 [INFO] predictor: CALIBRATION_MODE=on
2026-09-02 12:47:32,023 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-02 12:47:32,027 [INFO] run_cycle: fetched 05/4 [scan]: 156 combos
2026-09-02 12:47:32,255 [INFO] race_id: notif: nid=2026090205041300 sid=S01_NAKAANA1 phase=scan rank=B
2026-09-02 12:47:32,623 [INFO] notifier: Discord notify OK (status=204)
2026-09-02 12:47:33,196 [INFO] notifier: Discord notify OK (status=204)
2026-09-02 12:47:33,278 [INFO] run_cycle: SCAN S01_NAKAANA1 多摩川4R B
2026-09-02 12:47:33,386 [INFO] run_cycle: run_cycle done: 1 notifications
2026-09-02 12:48:04,263 [INFO] run_cycle: === run_cycle 12:48:04 ===
2026-09-02 12:48:04,264 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 12:48:04,264 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 12:48:04,309 [INFO] predictor: Models loaded OK
2026-09-02 12:48:04,613 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 12:49:03,471 [INFO] run_cycle: === run_cycle 12:49:03 ===
2026-09-02 12:49:03,471 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 12:49:03,471 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 12:49:03,518 [INFO] predictor: Models loaded OK
2026-09-02 12:49:03,779 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 93
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 93
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 22, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 131
  CIRCUIT_BREAKER_NO_ACTION: 28
  CIRCUIT_BREAKER_TRIP: 24
  CALIBRATION_DRIFT: 23
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  ANOMALY_BET_VOLUME_SPIKE: 6
  FINAL_MISSING: 5
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 9,900 | -3,000 | 0.767 |
| S01_NAKAANA1 | 40 | 5 | 8,000 | 2,280 | -5,720 | 0.285 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,420 | -380 | 0.9 |

## 直近アラート (24h・新しい順)
```
[12:47:33] CALIBRATION_DRIFT: {"avg_actual": 0.2255, "avg_pred": 0.4852, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 102, "overconf_pct": 53.5}
[12:33:19] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 2280, "roi_7d": 0.285, "sid": "S01_NAKAANA1"}
[12:33:19] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 346, "n_recent": 102, "psi": 0.329}
[12:33:19] CALIBRATION_DRIFT: {"avg_actual": 0.23, "avg_pred": 0.4839, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 100, "overconf_pct": 52.5}
[12:15:21] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 3100, "roi_7d": 0.378, "sid": "S01_NAKAANA1"}
[12:15:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 344, "n_recent": 104, "psi": 0.333}
[12:11:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.525, "baseline_mean": 0.858, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -5.23}
[12:04:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 344, "n_recent": 102, "psi": 0.331}
[12:03:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:34] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 111件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 45件 締切済
- 通知発射: scan=6 nid / final=5 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 063R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.6 drift=+27.8% | 12:15:20 |
| S00 | 063R | win | 1 | 0.5476 | 4.6 | 2.52 | 300 | scan=- drift=- | 12:15:18 |
| S00 | 062R | win | 1 | 0.5081 | 7.5 | 3.81 | 300 | scan=- drift=- | 11:47:18 |
| S00 | 2010R | win | 1 | 0.5123 | 6.5 | 3.33 | 300 | scan=5.5 drift=+18.2% | 19:39:19 |
| S00 | 243R | win | 1 | 0.4111 | 15.6 | 6.41 | 300 | scan=- drift=- | 18:31:31 |
| S01_NAKAANA1 | 206R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=4.2 drift=-2.4% | 17:33:19 |
| S01_NAKAANA1 | 124R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=- drift=- | 16:27:20 |
| S01_NAKAANA1 | 193R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.1 drift=+4.9% | 16:18:44 |
| S00 | 193R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=4.1 drift=+4.9% | 16:18:43 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.0 drift=+10.0% | 16:01:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +9.0% | -73.7% | +158.3% | 15 | 9 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.5s |
| **Latency** (scan→final max) | 613.1s |
| **Traffic** (notifications 24h) | 93 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 448 | 0.4751 | 0.2768 | +0.1983 | 🟡+42% | 0.2405 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4256 | 0.2670 | 0.2178 | 🔴-0.11 | 0.88 |
| S01_NAKAANA1 | win | 192 | 0.4895 | 0.2344 | 0.2509 | 🔴-0.40 | 0.716 |
| S02_TETSUBAN | win | 80 | 0.5496 | 0.4000 | 0.2655 | 🔴-0.11 | 0.7 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1233 | 0.0000 | 🔴+0.1233 |
| 0.15-0.20 | 10 | 0.1811 | 0.2000 | ✅-0.0189 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 154 | 0.4070 | 0.2468 | 🔴+0.1602 |
| 0.50+ | 266 | 0.5463 | 0.3083 | 🔴+0.2381 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 228 | 0.744 |
| win | <10.0 | ✅learned | 111 | 0.458 |
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
_auto-generated by claude_snapshot.py at 2026-09-02T12:50:01.984851+09:00_