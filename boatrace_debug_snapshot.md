# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-16T11:50:01.806915+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×43 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×67 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×43 (24h)
- 🔴 PSI_DRIFT_DETECTED×40 (24h)
- 🔴 CALIBRATION_DRIFT×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×46  [2026-09-16T11:03:04]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×92  [2026-09-16T11:03:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×92  [2026-09-16T11:03:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×46  [2026-09-16T11:03:04]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-09-16T11:03:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T11:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T11:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_ODDS_SHIFT  ×28  [2026-09-16T10:52:37]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-16T10:44:52]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-16T06:00:12]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2214 actual=0.0000 gap=+0.2214`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S00: n=173 hit%=27.2% hit_CI[Bonf]=[18.6,37.8]% ROI=0.94 ROI_boot95=[0.66,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=174 hit%=24.7% hit_CI[Bonf]=[16.6,35.2]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=33.8% hit_CI[Bonf]=[20.7,49.9]% ROI=0.60 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-16T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=27.3% ROI=0.83 (コスト 9,500/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.36MB / last modified 2026-09-16T11:49:26.341905+09:00

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
sed
2026-09-16 11:48:31,279 [INFO] scraper: fetch_race 14/8: boats=6 odds=191/191
2026-09-16 11:48:31,282 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 11:48:31,283 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-16 11:48:31,286 [INFO] run_cycle: fetched 14/8 [final]: 156 combos
2026-09-16 11:48:31,586 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-16 11:49:03,602 [INFO] run_cycle: === run_cycle 11:49:03 ===
2026-09-16 11:49:03,603 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-16 11:49:03,603 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-16 11:49:03,648 [INFO] predictor: Models loaded OK
2026-09-16 11:49:15,286 [INFO] scraper: odds3t: 120/120 parsed
2026-09-16 11:49:16,397 [INFO] scraper: odds3f: 20/20 parsed
2026-09-16 11:49:17,550 [INFO] scraper: odds2t: 30/30 parsed
2026-09-16 11:49:17,551 [INFO] scraper: odds2f: 15/15 parsed
2026-09-16 11:49:18,704 [INFO] scraper: odds_win: 5/6 parsed
2026-09-16 11:49:18,704 [INFO] scraper: fetch_race 04/3: boats=6 odds=190/191
2026-09-16 11:49:18,708 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 11:49:18,709 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-16 11:49:18,713 [INFO] run_cycle: fetched 04/3 [final]: 155 combos
2026-09-16 11:49:22,411 [INFO] scraper: odds3t: 120/120 parsed
2026-09-16 11:49:23,604 [INFO] scraper: odds3f: 18/20 parsed
2026-09-16 11:49:24,733 [INFO] scraper: odds2t: 26/30 parsed
2026-09-16 11:49:24,734 [INFO] scraper: odds2f: 14/15 parsed
2026-09-16 11:49:25,907 [INFO] scraper: odds_win: 2/6 parsed
2026-09-16 11:49:25,907 [INFO] scraper: fetch_race 13/4: boats=6 odds=180/191
2026-09-16 11:49:25,909 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 11:49:25,910 [INFO] predictor: combos: {'win': 2, '2t': 26, '3t': 120}
2026-09-16 11:49:25,913 [INFO] run_cycle: fetched 13/4 [scan]: 148 combos
2026-09-16 11:49:26,029 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 13, 'scan': 31}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 67
  ANOMALY_SCRAPER_FAILURE_BURST: 51
  CIRCUIT_BREAKER_TRIP: 43
  PSI_DRIFT_DETECTED: 40
  CIRCUIT_BREAKER_NO_ACTION: 34
  CALIBRATION_DRIFT: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_ODDS_SHIFT: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 6 | 10,200 | 4,860 | -5,340 | 0.476 |
| S01_NAKAANA1 | 35 | 8 | 7,000 | 4,440 | -2,560 | 0.634 |
| S02_TETSUBAN | 17 | 5 | 3,400 | 1,360 | -2,040 | 0.4 |

## 直近アラート (24h・新しい順)
```
[11:47:41] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 348, "n_recent": 86, "psi": 0.347}
[11:47:41] CALIBRATION_DRIFT: {"avg_actual": 0.2346, "avg_pred": 0.4836, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 81, "overconf_pct": 51.5}
[11:46:29] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4860, "roi_7d": 0.476, "sid": "S00"}
[11:46:29] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 347, "n_recent": 86, "psi": 0.347}
[11:46:29] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 34.3, "final": 9.0, "kind": "LARGE_ODDS_DRIFT", "race": "114R", "scan": 6.7, "sid": "S00"}
[11:25:39] CALIBRATION_DRIFT: {"avg_actual": 0.2317, "avg_pred": 0.4847, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 82, "overconf_pct": 52.2}
[11:23:05] CALIBRATION_DRIFT: {"avg_actual": 0.2346, "avg_pred": 0.4845, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 81, "overconf_pct": 51.6}
[11:21:45] CIRCUIT_BREAKER_TRIP: {"cost": 7200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 4440, "roi_7d": 0.617, "sid": "S01_NAKAANA1"}
[11:21:45] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 347, "n_recent": 85, "psi": 0.352}
[11:19:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 347, "n_recent": 83, "psi": 0.363}
```

## 本日残レース: 119件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 37件 締切済
- 通知発射: scan=6 nid / final=8 nid / result=3 nid
- predictions: 8 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 114R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 11:47:18 |
| S00 | 114R | win | 1 | 0.5334 | 9.0 | 4.80 | 300 | scan=6.7 drift=+34.3% | 11:46:18 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=4.0 drift=+5.0% | 11:21:08 |
| S00 | 042R | win | 1 | 0.5174 | 4.2 | 2.17 | 300 | scan=4.0 drift=+5.0% | 11:20:28 |
| S00 | 113R | win | 1 | 0.0644 | 10.5 | 0.68 | 300 | scan=- drift=- | 11:18:24 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4978 | 3.2 | 1.59 | 200 | scan=- drift=- | 10:52:27 |
| S00 | 112R | win | 1 | 0.4111 | 23.2 | 9.54 | 300 | scan=- drift=- | 10:51:19 |
| S00 | 111R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=4.5 drift=+0.0% | 10:26:27 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=4.2 drift=+4.8% | 17:05:45 |
| S00 | 075R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.2 drift=+4.8% | 17:05:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +4.9% | -80.2% | +93.9% | 11 | 3 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.3s |
| **Latency** (scan→final max) | 613.6s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 429 | 0.4753 | 0.2727 | +0.2026 | 🟡+43% | 0.2417 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4341 | 0.2686 | 0.2245 | 🔴-0.14 | 0.93 |
| S01_NAKAANA1 | win | 174 | 0.4844 | 0.2471 | 0.2476 | 🔴-0.33 | 0.759 |
| S02_TETSUBAN | win | 80 | 0.5458 | 0.3375 | 0.2665 | 🔴-0.19 | 0.603 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 156 | 0.4046 | 0.2308 | 🔴+0.1738 |
| 0.50+ | 251 | 0.5465 | 0.3108 | 🔴+0.2357 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 250 | 0.753 |
| win | <10.0 | ✅learned | 122 | 0.466 |
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
_auto-generated by claude_snapshot.py at 2026-09-16T11:50:01.806915+09:00_