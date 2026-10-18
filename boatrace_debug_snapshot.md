# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-18T13:40:01.501076+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-10-18T13:05:45]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-10-18T13:02:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-10-18T10:59:30]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_BET_VOLUME_DROP  ×42  [2026-10-18T10:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-18T06:00:07]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=42.4% ROI=1.07 (コスト 9,500/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=47 hit%=29.8% ROI=0.93 (コスト 12,000/回収 11,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1845 actual=0.0000 gap=+0.1845`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S00: n=176 hit%=28.4% hit_CI[Bonf]=[19.7,39.0]% ROI=0.76 ROI_boot95=[0.56,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=36.0% hit_CI[Bonf]=[26.3,47.0]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-18T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=86 hit%=52.3% hit_CI[Bonf]=[37.3,67.0]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=49 hit%=34.7% ROI=0.78 (コスト 11,500/回収 8,980)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=85 hit%=41.2% ROI=1.22 (コスト 19,200/回収 23,500)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-18T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=59 hit%=33.9% ROI=0.86 (コスト 14,200/回収 12,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-18T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=434 pred=0.4779 actual=0.3618 error=+0.1161 (+24%) brier=0.2439 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.14MB / last modified 2026-10-18T13:39:21.135013+09:00

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
6 combos
2026-10-18 13:38:22,505 [INFO] scraper: odds3t: 120/120 parsed
2026-10-18 13:38:23,579 [INFO] scraper: odds3f: 19/20 parsed
2026-10-18 13:38:24,685 [INFO] scraper: odds2t: 30/30 parsed
2026-10-18 13:38:24,687 [INFO] scraper: odds2f: 13/15 parsed
2026-10-18 13:38:25,833 [INFO] scraper: odds_win: 4/6 parsed
2026-10-18 13:38:25,833 [INFO] scraper: fetch_race 08/8: boats=6 odds=186/191
2026-10-18 13:38:25,836 [INFO] predictor: CALIBRATION_MODE=on
2026-10-18 13:38:25,836 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-18 13:38:25,840 [INFO] run_cycle: fetched 08/8 [scan]: 154 combos
2026-10-18 13:38:28,332 [WARNING] scraper: beforeinfo parse failed: jcd=10 rno=11
2026-10-18 13:38:28,333 [WARNING] run_cycle: fetch None: 10/11
2026-10-18 13:38:28,333 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-18 13:39:03,535 [INFO] run_cycle: === run_cycle 13:39:03 ===
2026-10-18 13:39:03,535 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-18 13:39:03,535 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-18 13:39:03,565 [INFO] predictor: Models loaded OK
2026-10-18 13:39:14,988 [INFO] scraper: odds3t: 120/120 parsed
2026-10-18 13:39:16,142 [INFO] scraper: odds3f: 20/20 parsed
2026-10-18 13:39:17,317 [INFO] scraper: odds2t: 30/30 parsed
2026-10-18 13:39:17,318 [INFO] scraper: odds2f: 15/15 parsed
2026-10-18 13:39:18,431 [INFO] scraper: odds_win: 6/6 parsed
2026-10-18 13:39:18,431 [INFO] scraper: fetch_race 21/11: boats=6 odds=191/191
2026-10-18 13:39:18,434 [INFO] predictor: CALIBRATION_MODE=on
2026-10-18 13:39:18,435 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-18 13:39:18,439 [INFO] run_cycle: fetched 21/11 [final]: 156 combos
2026-10-18 13:39:20,928 [WARNING] scraper: beforeinfo parse failed: jcd=10 rno=11
2026-10-18 13:39:20,928 [WARNING] run_cycle: fetch None: 10/11
2026-10-18 13:39:20,928 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 15, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 68
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_NO_ACTION: 20
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 10
  PSI_DRIFT_DETECTED: 7
  ANOMALY_BET_VOLUME_SPIKE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 15 | 15,000 | 12,900 | -2,100 | 0.86 |
| S01_NAKAANA1 | 45 | 17 | 9,000 | 8,020 | -980 | 0.891 |
| S02_TETSUBAN | 21 | 11 | 4,200 | 3,880 | -320 | 0.924 |

## 直近アラート (24h・新しい順)
```
[13:35:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.18, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.714, "today_scan_count": 14, "z_score": -2.61}
[13:30:31] FINAL_MISSING: {"deadline": "2026-10-18T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101809041159", "sid": "S00"}
[13:26:25] FINAL_MISSING: {"deadline": "2026-10-18T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101816011055", "sid": "S00"}
[13:15:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.202, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.692, "today_scan_count": 13, "z_score": -2.93}
[13:11:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.145, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.75, "today_scan_count": 12, "z_score": -2.09}
[13:07:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.228, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 12, "z_score": -3.3}
[13:02:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:02:44] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.167, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.727, "today_scan_count": 11, "z_score": -2.42}
[13:01:19] FINAL_MISSING: {"deadline": "2026-10-18T11:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101809031130", "sid": "S00"}
[13:01:19] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.258, "baseline_mean": 0.895, "baseline_stdev": 0.069, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -3.73}
```

## 本日残レース: 79件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 77件 締切済
- 通知発射: scan=14 nid / final=13 nid / result=8 nid
- predictions: 12 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 026R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=4.5 drift=-22.2% | 13:11:18 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.1 drift=+0.0% | 13:02:43 |
| S01_NAKAANA1 | 163R | win | 1 | 0.5719 | 4.8 | 2.75 | 200 | scan=3.7 drift=+29.7% | 11:49:19 |
| S00 | 163R | win | 1 | 0.5719 | 4.8 | 2.75 | 300 | scan=4.1 drift=+17.1% | 11:49:18 |
| S00 | 083R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=- drift=- | 11:17:19 |
| S01_NAKAANA1 | 083R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=3.3 drift=-3.0% | 11:16:19 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=3.5 drift=+17.1% | 11:13:29 |
| S01_NAKAANA1 | 216R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=3.0 drift=+50.0% | 11:00:22 |
| S00 | 216R | win | 1 | 0.5174 | 4.5 | 2.33 | 300 | scan=- drift=- | 11:00:21 |
| S00 | 092R | win | 1 | 0.5334 | 6.0 | 3.20 | 300 | scan=- drift=- | 10:59:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +13.0% | -52.2% | +250.0% | 17 | 6 | 51 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 476.5s |
| **Latency** (scan→final max) | 600.4s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4790 | 0.3570 | +0.1221 | 🟡+26% | 0.2450 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4425 | 0.2825 | 0.2384 | 🔴-0.18 | 0.77 |
| S01_NAKAANA1 | win | 174 | 0.4908 | 0.3563 | 0.2447 | 🔴-0.07 | 0.994 |
| S02_TETSUBAN | win | 86 | 0.5304 | 0.5116 | 0.2593 | 🔴-0.04 | 0.895 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 6 | 0.1845 | 0.0000 | 🔴+0.1845 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 158 | 0.4159 | 0.3228 | 🔴+0.0932 |
| 0.50+ | 258 | 0.5435 | 0.3876 | 🔴+0.1559 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 187 | 0.773 |
| win | <5.0 | ✅learned | 336 | 0.751 |
| win | <10.0 | ✅learned | 146 | 0.462 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-18T13:40:01.501076+09:00_