# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-11T12:00:01.859402+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×65 (24h)
- 🔴 CALIBRATION_DRIFT×29 (24h)
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×58  [2026-06-11T11:02:40]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×174  [2026-06-11T11:02:40]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×174  [2026-06-11T11:02:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-06-11T11:02:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-06-11T10:54:30]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-11T06:00:11]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S00: n=149 hit%=25.5% hit_CI[Bonf]=[16.7,36.9]% ROI=0.76 ROI_boot95=[0.50,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=28.3% hit_CI[Bonf]=[18.7,40.3]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=36.2% hit_CI[Bonf]=[22.7,52.4]% ROI=0.61 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-11T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=32.4% ROI=0.89 (コスト 10,000/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-11T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=20.0% ROI=0.42 (コスト 7,700/回収 3,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.8MB / last modified 2026-06-11T12:00:05.728355+09:00

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
2026-06-11 11:58:29,752 [INFO] scraper: fetch_race 09/4: boats=6 odds=188/191
2026-06-11 11:58:29,761 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 11:58:29,761 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-06-11 11:58:29,769 [INFO] run_cycle: fetched 09/4 [scan]: 153 combos
2026-06-11 11:58:29,881 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 11:59:05,869 [INFO] run_cycle: === run_cycle 11:59:05 ===
2026-06-11 11:59:05,871 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 11:59:05,871 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 11:59:05,948 [INFO] predictor: Models loaded OK
2026-06-11 11:59:17,380 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 11:59:18,673 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 11:59:19,848 [INFO] scraper: odds2t: 28/30 parsed
2026-06-11 11:59:19,849 [INFO] scraper: odds2f: 15/15 parsed
2026-06-11 11:59:20,958 [INFO] scraper: odds_win: 6/6 parsed
2026-06-11 11:59:20,958 [INFO] scraper: fetch_race 05/2: boats=6 odds=189/191
2026-06-11 11:59:20,971 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 11:59:20,971 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-06-11 11:59:20,977 [INFO] run_cycle: fetched 05/2 [scan]: 154 combos
2026-06-11 11:59:24,502 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 11:59:25,636 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 11:59:26,819 [INFO] scraper: odds2t: 30/30 parsed
2026-06-11 11:59:26,820 [INFO] scraper: odds2f: 15/15 parsed
2026-06-11 11:59:27,932 [INFO] scraper: odds_win: 6/6 parsed
2026-06-11 11:59:27,932 [INFO] scraper: fetch_race 14/8: boats=6 odds=191/191
2026-06-11 11:59:27,941 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 11:59:27,943 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-11 11:59:27,951 [INFO] run_cycle: fetched 14/8 [scan]: 156 combos
2026-06-11 11:59:28,258 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 11, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 81
  CIRCUIT_BREAKER_TRIP: 65
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 29
  FINAL_MISSING: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 8 | 11,400 | 6,090 | -5,310 | 0.534 |
| S01_NAKAANA1 | 31 | 7 | 6,200 | 3,040 | -3,160 | 0.49 |
| S02_TETSUBAN | 27 | 5 | 5,400 | 1,560 | -3,840 | 0.289 |

## 直近アラート (24h・新しい順)
```
[11:56:36] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 6090, "roi_7d": 0.534, "sid": "S00"}
[11:49:39] CALIBRATION_DRIFT: {"avg_actual": 0.2174, "avg_pred": 0.4925, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 55.9}
[11:42:28] CALIBRATION_DRIFT: {"avg_actual": 0.2151, "avg_pred": 0.4934, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 93, "overconf_pct": 56.4}
[11:39:32] CALIBRATION_DRIFT: {"avg_actual": 0.2174, "avg_pred": 0.4929, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 55.9}
[11:33:22] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 6090, "roi_7d": 0.521, "sid": "S00"}
[11:30:27] CIRCUIT_BREAKER_TRIP: {"cost": 6200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 3040, "roi_7d": 0.49, "sid": "S01_NAKAANA1"}
[11:29:41] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 1560, "roi_7d": 0.289, "sid": "S02_TETSUBAN"}
[11:29:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.19, "baseline_mean": 0.857, "baseline_stdev": 0.062, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 9, "z_score": -3.07}
[11:28:25] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 6090, "roi_7d": 0.549, "sid": "S00"}
[11:28:25] CALIBRATION_DRIFT: {"avg_actual": 0.2151, "avg_pred": 0.4897, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 93, "overconf_pct": 56.1}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 39件 締切済
- 通知発射: scan=12 nid / final=10 nid / result=4 nid
- predictions: 8 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 114R | win | 1 | 0.1543 | 5.6 | 0.86 | 300 | scan=5.6 drift=+0.0% | 11:52:32 |
| S00 | 093R | win | 1 | 0.2292 | 4.1 | 0.94 | 300 | scan=- drift=- | 11:33:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 200 | scan=- drift=- | 11:30:25 |
| S00 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 300 | scan=7.3 drift=-34.2% | 11:30:25 |
| S01_NAKAANA1 | 031R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=3.9 drift=+23.1% | 11:11:20 |
| S02_TETSUBAN | 111R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=2.6 drift=-3.8% | 10:28:38 |
| S00 | 234R | win | 1 | 0.4111 | 7.9 | 3.25 | 300 | scan=5.9 drift=+33.9% | 09:54:22 |
| S00 | 103R | win | 1 | 0.5891 | 12.7 | 7.48 | 300 | scan=12.7 drift=+0.0% | 09:21:33 |
| S02_TETSUBAN | 0710R | win | 1 | 0.5509 | 2.5 | 1.38 | 200 | scan=2.8 drift=-10.7% | 19:47:21 |
| S01_NAKAANA1 | 0610R | win | 1 | 0.5719 | 3.4 | 1.94 | 200 | scan=- drift=- | 16:04:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +8.1% | -62.9% | +274.6% | 17 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 484.2s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4699 | 0.2896 | +0.1803 | 🟡+38% | 0.2379 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 148 | 0.4213 | 0.2635 | 0.2195 | 🔴-0.13 | 0.781 |
| S01_NAKAANA1 | win | 137 | 0.4873 | 0.2774 | 0.2434 | 🔴-0.21 | 0.699 |
| S02_TETSUBAN | win | 81 | 0.5294 | 0.3580 | 0.2621 | 🔴-0.14 | 0.602 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.20-0.30 | 5 | 0.2225 | 0.4000 | 🔴-0.1775 |
| 0.30-0.50 | 138 | 0.4197 | 0.2246 | 🔴+0.1951 |
| 0.50+ | 205 | 0.5414 | 0.3463 | 🔴+0.1951 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 35 | 0.736 |
| win | <5.0 | ✅learned | 66 | 0.72 |
| win | <10.0 | ✅learned | 42 | 0.51 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-11T12:00:01.859402+09:00_