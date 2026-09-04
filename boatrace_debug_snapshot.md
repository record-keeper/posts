# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-04T12:10:01.468726+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×51 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×77 (24h)
- 🔴 PSI_DRIFT_DETECTED×51 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×6  [2026-09-04T12:03:37]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×6  [2026-09-04T12:03:37]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×6  [2026-09-04T12:03:37]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×6  [2026-09-04T12:03:37]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×9  [2026-09-04T12:00:48]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-04T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-09-04T11:32:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-09-04T06:00:14]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=188<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=19.5% ROI=0.87 (コスト 11,200/回収 9,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=115 pred=0.4375 actual=0.2261 gap=+0.2114`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S00: n=183 hit%=27.9% hit_CI[Bonf]=[19.4,38.2]% ROI=0.95 ROI_boot95=[0.69,1.23]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=188 hit%=23.9% hit_CI[Bonf]=[16.2,33.9]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=39.5% hit_CI[Bonf]=[25.5,55.4]% ROI=0.67 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=17.1% ROI=0.52 (コスト 10,100/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.28MB / last modified 2026-09-04T12:09:18.692426+09:00

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
rsed
2026-09-04 12:08:01,531 [INFO] scraper: fetch_race 22/2: boats=6 odds=174/191
2026-09-04 12:08:01,533 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 12:08:01,533 [INFO] predictor: combos: {'win': 2, '2t': 23, '3t': 120}
2026-09-04 12:08:01,537 [INFO] run_cycle: fetched 22/2 [scan]: 145 combos
2026-09-04 12:08:05,044 [INFO] scraper: odds3t: 120/120 parsed
2026-09-04 12:08:06,193 [INFO] scraper: odds3f: 20/20 parsed
2026-09-04 12:08:07,328 [INFO] scraper: odds2t: 30/30 parsed
2026-09-04 12:08:07,329 [INFO] scraper: odds2f: 15/15 parsed
2026-09-04 12:08:08,414 [INFO] scraper: odds_win: 6/6 parsed
2026-09-04 12:08:08,414 [INFO] scraper: fetch_race 06/3: boats=6 odds=191/191
2026-09-04 12:08:08,417 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 12:08:08,417 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-04 12:08:08,421 [INFO] run_cycle: fetched 06/3 [scan]: 156 combos
2026-09-04 12:08:08,563 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-04 12:09:03,376 [INFO] run_cycle: === run_cycle 12:09:03 ===
2026-09-04 12:09:03,376 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-04 12:09:03,376 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-04 12:09:03,417 [INFO] predictor: Models loaded OK
2026-09-04 12:09:14,864 [INFO] scraper: odds3t: 120/120 parsed
2026-09-04 12:09:15,993 [INFO] scraper: odds3f: 20/20 parsed
2026-09-04 12:09:17,129 [INFO] scraper: odds2t: 30/30 parsed
2026-09-04 12:09:17,130 [INFO] scraper: odds2f: 15/15 parsed
2026-09-04 12:09:18,212 [INFO] scraper: odds_win: 6/6 parsed
2026-09-04 12:09:18,212 [INFO] scraper: fetch_race 17/3: boats=6 odds=191/191
2026-09-04 12:09:18,215 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 12:09:18,216 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-04 12:09:18,220 [INFO] run_cycle: fetched 17/3 [final]: 156 combos
2026-09-04 12:09:18,636 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 53
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 53
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 8, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  FINAL_MISSING: 77
  PSI_DRIFT_DETECTED: 51
  ANOMALY_SCAN_FINAL_RATIO: 30
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 13 | 13,200 | 13,020 | -180 | 0.986 |
| S01_NAKAANA1 | 32 | 3 | 6,400 | 1,560 | -4,840 | 0.244 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 2,000 | -800 | 0.714 |

## 直近アラート (24h・新しい順)
```
[12:03:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:03:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:00:46] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 362, "n_recent": 90, "psi": 0.329}
[12:00:46] CALIBRATION_DRIFT: {"avg_actual": 0.2386, "avg_pred": 0.4775, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 88, "overconf_pct": 50.0}
[11:57:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 361, "n_recent": 91, "psi": 0.33}
[11:46:20] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 361, "n_recent": 91, "psi": 0.329}
[11:41:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 360, "n_recent": 92, "psi": 0.33}
[11:37:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 361, "n_recent": 92, "psi": 0.329}
[11:32:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.351, "baseline_mean": 0.851, "baseline_stdev": 0.128, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -2.75}
[11:21:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 361, "n_recent": 91, "psi": 0.332}
```

## 本日残レース: 121件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 35件 締切済
- 通知発射: scan=7 nid / final=6 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 108R | win | 1 | 0.5044 | 5.1 | 2.57 | 300 | scan=5.6 drift=-8.9% | 11:49:43 |
| S01_NAKAANA1 | 172R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.0 drift=+36.7% | 11:37:30 |
| S01_NAKAANA1 | 106R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.0 drift=+20.0% | 10:47:19 |
| S00 | 102R | win | 1 | 0.5891 | 6.4 | 3.77 | 300 | scan=- drift=- | 08:55:19 |
| S02_TETSUBAN | 1611R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=- drift=- | 16:42:18 |
| S00 | 028R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.7 drift=-4.3% | 14:13:30 |
| S00 | 225R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 14:05:20 |
| S01_NAKAANA1 | 176R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 13:24:20 |
| S01_NAKAANA1 | 065R | win | 1 | 0.5556 | 3.7 | 2.06 | 200 | scan=3.2 drift=+15.6% | 13:19:19 |
| S00 | 223R | win | 1 | 0.5095 | 6.0 | 3.06 | 300 | scan=5.6 drift=+7.1% | 12:46:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +12.4% | -73.7% | +158.3% | 10 | 6 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 457.5s |
| **Latency** (scan→final max) | 652.4s |
| **Traffic** (notifications 24h) | 53 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 450 | 0.4745 | 0.2800 | +0.1945 | 🟡+41% | 0.2414 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4249 | 0.2802 | 0.2217 | 🔴-0.10 | 0.945 |
| S01_NAKAANA1 | win | 188 | 0.4902 | 0.2340 | 0.2502 | 🔴-0.40 | 0.733 |
| S02_TETSUBAN | win | 80 | 0.5502 | 0.3875 | 0.2654 | 🔴-0.12 | 0.667 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 157 | 0.4070 | 0.2420 | 🔴+0.1650 |
| 0.50+ | 265 | 0.5465 | 0.3132 | 🔴+0.2333 |

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
_auto-generated by claude_snapshot.py at 2026-09-04T12:10:01.468726+09:00_