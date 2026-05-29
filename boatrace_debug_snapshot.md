# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-29T10:40:02.180498+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-29T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×39  [2026-05-29T10:01:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×39  [2026-05-29T10:01:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×39  [2026-05-29T10:01:33]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-05-29T10:01:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×39  [2026-05-29T10:01:33]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-29T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.57 (コスト 9,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2234 actual=0.4167 gap=-0.1933`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.03 (コスト 8,600/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-29T06:00:11]
- key: `ROI_STAT|S00: n=176 hit%=28.4% hit_CI[Bonf]=[19.7,39.0]% ROI=0.96 ROI_boot95=[0.68,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-29T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=92 hit%=30.4% hit_CI[Bonf]=[18.7,45.4]% ROI=0.80 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=92<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-29T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=51 hit%=49.0% hit_CI[Bonf]=[30.4,67.9]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.90 (コスト 14,400/回収 12,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.68MB / last modified 2026-05-29T10:39:29.104023+09:00

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
can]: 155 combos
2026-05-29 10:38:40,653 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 10:39:05,572 [INFO] run_cycle: === run_cycle 10:39:05 ===
2026-05-29 10:39:05,572 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 10:39:05,572 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 10:39:05,631 [INFO] predictor: Models loaded OK
2026-05-29 10:39:18,553 [INFO] scraper: odds3t: 120/120 parsed
2026-05-29 10:39:19,671 [INFO] scraper: odds3f: 20/20 parsed
2026-05-29 10:39:20,787 [INFO] scraper: odds2t: 28/30 parsed
2026-05-29 10:39:20,788 [INFO] scraper: odds2f: 14/15 parsed
2026-05-29 10:39:21,897 [INFO] scraper: odds_win: 5/6 parsed
2026-05-29 10:39:21,897 [INFO] scraper: fetch_race 23/6: boats=6 odds=187/191
2026-05-29 10:39:21,909 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 10:39:21,910 [INFO] predictor: combos: {'win': 5, '2t': 28, '3t': 120}
2026-05-29 10:39:21,917 [INFO] run_cycle: fetched 23/6 [scan]: 153 combos
2026-05-29 10:39:25,364 [INFO] scraper: odds3t: 120/120 parsed
2026-05-29 10:39:26,474 [INFO] scraper: odds3f: 19/20 parsed
2026-05-29 10:39:27,563 [INFO] scraper: odds2t: 19/30 parsed
2026-05-29 10:39:27,564 [INFO] scraper: odds2f: 11/15 parsed
2026-05-29 10:39:28,663 [INFO] scraper: odds_win: 6/6 parsed
2026-05-29 10:39:28,664 [INFO] scraper: fetch_race 17/1: boats=6 odds=175/191
2026-05-29 10:39:28,673 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 10:39:28,673 [INFO] predictor: combos: {'win': 6, '2t': 19, '3t': 120}
2026-05-29 10:39:28,681 [INFO] run_cycle: fetched 17/1 [scan]: 145 combos
2026-05-29 10:39:28,799 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 10:40:09,622 [INFO] run_cycle: === run_cycle 10:40:09 ===
2026-05-29 10:40:09,623 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 10:40:09,623 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000

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
{'final': 32, 'result': 16, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 100
  FINAL_MISSING: 47
  PSI_DRIFT_DETECTED: 38
  CIRCUIT_BREAKER_TRIP: 28
  KS_ODDS_DRIFT: 27
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 7 | 9,300 | 8,010 | -1,290 | 0.861 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,580 | -2,420 | 0.654 |
| S02_TETSUBAN | 13 | 9 | 2,600 | 3,540 | +940 | 1.362 |

## 直近アラート (24h・新しい順)
```
[10:36:20] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.004275, "ks_stat": 0.223}
[10:29:29] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.00361, "ks_stat": 0.227}
[10:29:29] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 239, "n_recent": 80, "psi": 0.563}
[10:14:33] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003397, "ks_stat": 0.228}
[10:14:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 240, "n_recent": 79, "psi": 0.566}
[10:10:25] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4580, "roi_7d": 0.654, "sid": "S01_NAKAANA1"}
[10:10:25] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002896, "ks_stat": 0.23}
[10:10:25] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 241, "n_recent": 79, "psi": 0.565}
[10:01:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 150件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 18件 締切済
- 通知発射: scan=3 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 111R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.8 drift=+0.0% | 10:29:28 |
| S01_NAKAANA1 | 142R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=- drift=- | 09:09:20 |
| S00 | 017R | win | 1 | 0.0568 | 6.0 | 0.34 | 300 | scan=5.8 drift=+3.4% | 18:24:20 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5735 | 3.9 | 2.24 | 200 | scan=- drift=- | 18:05:22 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=4.7 drift=-36.2% | 17:21:32 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=- drift=- | 17:15:21 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 16:57:37 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=4.2 drift=-4.8% | 16:19:44 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=4.0 drift=+22.5% | 15:21:21 |
| S00 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 300 | scan=4.0 drift=+22.5% | 15:21:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | -3.1% | -81.4% | +157.5% | 15 | 10 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.0s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 318 | 0.4541 | 0.3239 | +0.1302 | 🟡+29% | 0.2340 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4213 | 0.2874 | 0.2220 | 🔴-0.08 | 0.975 |
| S01_NAKAANA1 | win | 93 | 0.4842 | 0.3011 | 0.2447 | 🔴-0.16 | 0.791 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.4545 | 🔴-0.2306 |
| 0.30-0.50 | 141 | 0.4157 | 0.2837 | 🔴+0.1320 |
| 0.50+ | 151 | 0.5402 | 0.3775 | 🔴+0.1627 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 44 | 0.801 |
| win | <10.0 | ✅learned | 37 | 0.538 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-05-29T10:40:02.180498+09:00_