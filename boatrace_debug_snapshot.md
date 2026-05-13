# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-13T13:10:01.662347+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×39 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 PSI_DRIFT_DETECTED×39 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×8  [2026-05-13T13:02:59]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-05-13T13:02:59]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×8  [2026-05-13T13:02:59]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-05-13T12:50:31]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-05-13T11:33:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-13T06:00:11]
- key: `ROI_STAT|S00: n=167 hit%=24.6% hit_CI[Bonf]=[16.3,35.2]% ROI=0.83 ROI_boot95=[0.60,1.10]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-13T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-13T06:00:11]
- key: `ORPHAN_SCAN|202 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-13T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=18.9% ROI=0.48 (コスト 10,900/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-13T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=27 hit%=33.3% ROI=1.55 (コスト 6,600/回収 10,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-13T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=39 hit%=30.8% ROI=1.08 (コスト 9,900/回収 10,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-13T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=20.0% ROI=0.57 (コスト 8,100/回収 4,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|bt=win: n=205 pred=0.4484 actual=0.2927 error=+0.1557 (+35%) brier=0.2309 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|S00(win): n=167 pred=0.4365 hit=0.2455 cal_err=+0.1910 brier=0.2285 BSS=-0.23 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=22 pred=0.4980 hit=0.4545 cal_err=+0.0434 brier=0.2304 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=18 pred=0.3278 actual=0.1667 gap=+0.1611`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-13T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=75 pred=0.4472 actual=0.2667 gap=+0.1805`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.59MB / last modified 2026-05-13T13:09:27.813651+09:00

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
== run_cycle 13:08:05 ===
2026-05-13 13:08:05,487 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 13:08:05,487 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 13:08:05,545 [INFO] predictor: Models loaded OK
2026-05-13 13:08:05,726 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-13 13:09:05,670 [INFO] run_cycle: === run_cycle 13:09:05 ===
2026-05-13 13:09:05,670 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 13:09:05,670 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 13:09:05,713 [INFO] predictor: Models loaded OK
2026-05-13 13:09:17,068 [INFO] scraper: odds3t: 120/120 parsed
2026-05-13 13:09:18,170 [INFO] scraper: odds3f: 20/20 parsed
2026-05-13 13:09:19,280 [INFO] scraper: odds2t: 30/30 parsed
2026-05-13 13:09:19,281 [INFO] scraper: odds2f: 15/15 parsed
2026-05-13 13:09:20,371 [INFO] scraper: odds_win: 5/6 parsed
2026-05-13 13:09:20,371 [INFO] scraper: fetch_race 03/6: boats=6 odds=190/191
2026-05-13 13:09:20,382 [INFO] predictor: CALIBRATION_MODE=on
2026-05-13 13:09:20,383 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-13 13:09:20,390 [INFO] run_cycle: fetched 03/6 [final]: 155 combos
2026-05-13 13:09:23,909 [INFO] scraper: odds3t: 120/120 parsed
2026-05-13 13:09:24,981 [INFO] scraper: odds3f: 20/20 parsed
2026-05-13 13:09:26,057 [INFO] scraper: odds2t: 27/30 parsed
2026-05-13 13:09:26,058 [INFO] scraper: odds2f: 14/15 parsed
2026-05-13 13:09:27,159 [INFO] scraper: odds_win: 4/6 parsed
2026-05-13 13:09:27,159 [INFO] scraper: fetch_race 08/7: boats=6 odds=185/191
2026-05-13 13:09:27,170 [INFO] predictor: CALIBRATION_MODE=on
2026-05-13 13:09:27,170 [INFO] predictor: combos: {'win': 4, '2t': 27, '3t': 120}
2026-05-13 13:09:27,178 [INFO] run_cycle: fetched 08/7 [scan]: 151 combos
2026-05-13 13:09:27,318 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 35, 'result': 21, 'scan': 37}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 221
  FINAL_MISSING: 78
  PSI_DRIFT_DETECTED: 39
  KS_ODDS_DRIFT: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 12 | 13,800 | 10,470 | -3,330 | 0.759 |
| S01_NAKAANA1 | 26 | 10 | 5,200 | 3,820 | -1,380 | 0.735 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,700 | +300 | 1.088 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[13:09:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1245}
[13:08:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1250}
[13:07:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1253}
[13:06:32] FINAL_MISSING: {"deadline": "2026-05-13T12:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051314091236", "sid": "S00"}
[13:06:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1246}
[13:05:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1235}
[13:04:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1234}
[13:03:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1236}
[13:02:59] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:01:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1217}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 63件 締切済
- 通知発射: scan=14 nid / final=11 nid / result=6 nid
- predictions: 9 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 086R | win | 1 | 0.5891 | 4.8 | 2.83 | 200 | scan=- drift=- | 12:45:22 |
| S00 | 086R | win | 1 | 0.5891 | 4.8 | 2.83 | 300 | scan=- drift=- | 12:45:21 |
| S01_NAKAANA1 | 035R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=3.7 drift=+24.3% | 12:40:25 |
| S00 | 085R | win | 1 | 0.4989 | 8.2 | 4.09 | 300 | scan=7.5 drift=+9.3% | 12:15:45 |
| S00 | 114R | win | 1 | 0.1371 | 15.0 | 2.06 | 300 | scan=- drift=- | 11:55:31 |
| S00 | 084R | win | 1 | 0.4111 | 8.2 | 3.37 | 300 | scan=8.2 drift=+0.0% | 11:48:44 |
| S01_NAKAANA1 | 033R | win | 1 | 0.3177 | 3.4 | 1.08 | 200 | scan=4.1 drift=-17.1% | 11:45:22 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=3.0 drift=+10.0% | 11:43:32 |
| S02_TETSUBAN | 031R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=2.1 drift=+0.0% | 10:51:20 |
| S01_NAKAANA1 | 209R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=- drift=- | 19:09:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 62 | +4.7% | -75.4% | +522.0% | 25 | 15 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.0s |
| **Latency** (scan→final max) | 650.7s |
| **Traffic** (notifications 24h) | 93 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 211 | 0.4469 | 0.2844 | +0.1625 | 🟡+36% | 0.2293 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4350 | 0.2412 | 0.2271 | 🔴-0.24 | 0.819 |
| S01_NAKAANA1 | win | 24 | 0.4911 | 0.4167 | 0.2264 | ✅+0.07 | 0.796 |
| S02_TETSUBAN | win | 17 | 0.5034 | 0.5294 | 0.2562 | 🔴-0.03 | 1.088 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 97 | 0.4244 | 0.2371 | 🔴+0.1873 |
| 0.50+ | 91 | 0.5381 | 0.3516 | 🔴+0.1864 |

## Settlement Ratio データ品質

- 学習済み: 2バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 9 | 0.4 |
| win | <5.0 | ✅learned | 17 | 0.779 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 9 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-13T13:10:01.662347+09:00_