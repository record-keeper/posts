# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-11T13:30:00.767812+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×39 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×94 (24h)
- 🔴 PSI_DRIFT_DETECTED×39 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×11  [2026-05-11T13:14:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×28  [2026-05-11T13:02:31]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-05-11T13:02:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×52  [2026-05-11T12:38:05]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-05-11T10:57:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=24 hit%=20.8% ROI=0.62 (コスト 6,400/回収 3,960)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-11T06:00:07]
- key: `ROI_STAT|S00: n=151 hit%=25.8% hit_CI[Bonf]=[17.0,37.2]% ROI=0.87 ROI_boot95=[0.59,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-11T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-11T06:00:07]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=18.2% ROI=0.47 (コスト 9,700/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=22 hit%=31.8% ROI=1.66 (コスト 5,600/回収 9,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=28 hit%=28.6% ROI=1.27 (コスト 7,500/回収 9,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=164 pred=0.4387 actual=0.2622 error=+0.1765 (+40%) brier=0.2304 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=151 pred=0.4335 hit=0.2583 cal_err=+0.1752 brier=0.2291 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=15 pred=0.3298 actual=0.1333 gap=+0.1964`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=64 pred=0.4473 actual=0.2656 gap=+0.1817`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=65 pred=0.5347 actual=0.2923 gap=+0.2424`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.49MB / last modified 2026-05-11T13:30:02.087738+09:00

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
ed
2026-05-11 13:28:34,050 [INFO] scraper: fetch_race 05/5: boats=6 odds=185/191
2026-05-11 13:28:34,064 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 13:28:34,064 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-11 13:28:34,076 [INFO] run_cycle: fetched 05/5 [scan]: 154 combos
2026-05-11 13:28:34,201 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-11 13:29:05,663 [INFO] run_cycle: === run_cycle 13:29:05 ===
2026-05-11 13:29:05,663 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-11 13:29:05,663 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-11 13:29:05,707 [INFO] predictor: Models loaded OK
2026-05-11 13:29:18,104 [INFO] scraper: odds3t: 120/120 parsed
2026-05-11 13:29:19,254 [INFO] scraper: odds3f: 20/20 parsed
2026-05-11 13:29:20,357 [INFO] scraper: odds2t: 30/30 parsed
2026-05-11 13:29:20,358 [INFO] scraper: odds2f: 15/15 parsed
2026-05-11 13:29:21,466 [INFO] scraper: odds_win: 5/6 parsed
2026-05-11 13:29:21,466 [INFO] scraper: fetch_race 23/11: boats=6 odds=190/191
2026-05-11 13:29:21,479 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 13:29:21,479 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-11 13:29:21,486 [INFO] run_cycle: fetched 23/11 [final]: 155 combos
2026-05-11 13:29:25,369 [INFO] scraper: odds3t: 120/120 parsed
2026-05-11 13:29:26,526 [INFO] scraper: odds3f: 20/20 parsed
2026-05-11 13:29:27,638 [INFO] scraper: odds2t: 30/30 parsed
2026-05-11 13:29:27,639 [INFO] scraper: odds2f: 15/15 parsed
2026-05-11 13:29:28,720 [INFO] scraper: odds_win: 6/6 parsed
2026-05-11 13:29:28,720 [INFO] scraper: fetch_race 03/7: boats=6 odds=191/191
2026-05-11 13:29:28,729 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 13:29:28,729 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-11 13:29:28,737 [INFO] run_cycle: fetched 03/7 [scan]: 156 combos
2026-05-11 13:29:28,835 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 90
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 90
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 21, 'scan': 33}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 94
  ANOMALY_SCRAPER_FAILURE_BURST: 82
  PSI_DRIFT_DETECTED: 39
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 12
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 17 | 14,400 | 14,550 | +150 | 1.01 |
| S01_NAKAANA1 | 10 | 3 | 2,000 | 1,560 | -440 | 0.78 |
| S02_TETSUBAN | 10 | 4 | 2,000 | 2,140 | +140 | 1.07 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[13:27:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.001761, "ks_stat": 0.284}
[13:27:29] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 108, "n_recent": 68, "psi": 0.326}
[13:24:34] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.00227, "ks_stat": 0.278}
[13:24:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 107, "n_recent": 69, "psi": 0.336}
[13:24:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1148}
[13:23:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1130}
[13:22:29] FINAL_MISSING: {"deadline": "2026-05-11T12:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051108061252", "sid": "S00"}
[13:22:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1135}
[13:21:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1163}
[13:20:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1161}
```

## 本日残レース: 86件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 58件 締切済
- 通知発射: scan=16 nid / final=16 nid / result=9 nid
- predictions: 12 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 166R | win | 1 | 0.5123 | 6.7 | 3.43 | 300 | scan=4.1 drift=+63.4% | 13:24:32 |
| S02_TETSUBAN | 036R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.7 drift=-11.1% | 13:09:44 |
| S00 | 116R | win | 1 | 0.5735 | 5.7 | 3.27 | 300 | scan=13.5 drift=-57.8% | 13:02:22 |
| S02_TETSUBAN | 035R | win | 1 | 0.3177 | 2.9 | 0.92 | 200 | scan=2.1 drift=+38.1% | 12:40:23 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.8 drift=-13.2% | 12:32:34 |
| S02_TETSUBAN | 034R | win | 1 | 0.4111 | 2.6 | 1.07 | 200 | scan=2.5 drift=+4.0% | 12:12:21 |
| S00 | 148R | win | 1 | 0.5334 | 6.6 | 3.52 | 300 | scan=5.6 drift=+17.9% | 11:59:32 |
| S00 | 238R | win | 1 | 0.4111 | 11.8 | 4.85 | 300 | scan=36.0 drift=-67.2% | 11:43:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5891 | 4.4 | 2.59 | 200 | scan=4.3 drift=+2.3% | 11:37:32 |
| S02_TETSUBAN | 092R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.2 drift=+9.1% | 11:04:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 50 | -10.6% | -75.4% | +124.4% | 27 | 17 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 501.2s |
| **Latency** (scan→final max) | 611.2s |
| **Traffic** (notifications 24h) | 90 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 173 | 0.4407 | 0.2717 | +0.1690 | 🟡+38% | 0.2323 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 154 | 0.4344 | 0.2597 | 0.2287 | 🔴-0.19 | 0.889 |
| S01_NAKAANA1 | win | 10 | 0.4929 | 0.3000 | 0.2500 | 🔴-0.19 | 0.78 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 6 | 0.1899 | 0.1667 | ✅+0.0232 |
| 0.20-0.30 | 9 | 0.2241 | 0.3333 | 🔴-0.1093 |
| 0.30-0.50 | 84 | 0.4241 | 0.2500 | 🔴+0.1741 |
| 0.50+ | 69 | 0.5363 | 0.3043 | 🔴+0.2319 |

## Settlement Ratio データ品質

- 学習済み: 2バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 4 | 0.4 |
| win | <5.0 | ✅learned | 10 | 1.0 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 8 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-05-11T13:30:00.767812+09:00_