# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-29T08:40:01.742734+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 PSI_DRIFT_DETECTED×35 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-29T08:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×40  [2026-05-29T08:00:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×40  [2026-05-29T08:00:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×40  [2026-05-29T08:00:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×40  [2026-05-29T08:00:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×40  [2026-05-29T08:00:38]
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
- DB: 3.67MB / last modified 2026-05-29T08:39:21.850256+09:00

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
parsed
2026-05-29 08:37:44,177 [INFO] scraper: odds2t: 30/30 parsed
2026-05-29 08:37:44,179 [INFO] scraper: odds2f: 15/15 parsed
2026-05-29 08:37:45,289 [INFO] scraper: odds_win: 6/6 parsed
2026-05-29 08:37:45,289 [INFO] scraper: fetch_race 18/1: boats=6 odds=191/191
2026-05-29 08:37:45,301 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 08:37:45,301 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-29 08:37:45,308 [INFO] run_cycle: fetched 18/1 [final]: 156 combos
2026-05-29 08:37:45,503 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 08:38:06,053 [INFO] run_cycle: === run_cycle 08:38:06 ===
2026-05-29 08:38:06,055 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 08:38:06,055 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 08:38:06,130 [INFO] predictor: Models loaded OK
2026-05-29 08:38:06,225 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 08:39:06,299 [INFO] run_cycle: === run_cycle 08:39:06 ===
2026-05-29 08:39:06,299 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 08:39:06,299 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 08:39:06,344 [INFO] predictor: Models loaded OK
2026-05-29 08:39:18,164 [INFO] scraper: odds3t: 120/120 parsed
2026-05-29 08:39:19,313 [INFO] scraper: odds3f: 20/20 parsed
2026-05-29 08:39:20,618 [INFO] scraper: odds2t: 30/30 parsed
2026-05-29 08:39:20,619 [INFO] scraper: odds2f: 13/15 parsed
2026-05-29 08:39:21,725 [INFO] scraper: odds_win: 6/6 parsed
2026-05-29 08:39:21,725 [INFO] scraper: fetch_race 14/1: boats=6 odds=189/191
2026-05-29 08:39:21,728 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 08:39:21,728 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-29 08:39:21,732 [INFO] run_cycle: fetched 14/1 [scan]: 156 combos
2026-05-29 08:39:21,824 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 100
  FINAL_MISSING: 47
  PSI_DRIFT_DETECTED: 35
  CIRCUIT_BREAKER_TRIP: 27
  KS_ODDS_DRIFT: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 7 | 9,000 | 8,010 | -990 | 0.89 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 4,580 | -2,220 | 0.674 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 3,540 | +740 | 1.264 |

## 直近アラート (24h・新しい順)
```
[08:00:37] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:37] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4580, "roi_7d": 0.674, "sid": "S01_NAKAANA1"}
[08:00:37] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003397, "ks_stat": 0.229}
[08:00:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 241, "n_recent": 78, "psi": 0.567}
[08:00:37] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4580, "roi_7d": 0.674, "sid": "S01_NAKAANA1"}
[06:00:07] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003397, "ks_stat": 0.229}
[06:00:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 241, "n_recent": 78, "psi": 0.567}
[06:00:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 166件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 2件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 017R | win | 1 | 0.0568 | 6.0 | 0.34 | 300 | scan=5.8 drift=+3.4% | 18:24:20 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5735 | 3.9 | 2.24 | 200 | scan=- drift=- | 18:05:22 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=4.7 drift=-36.2% | 17:21:32 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=- drift=- | 17:15:21 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 16:57:37 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=4.2 drift=-4.8% | 16:19:44 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=4.0 drift=+22.5% | 15:21:21 |
| S00 | 011R | win | 1 | 0.4111 | 4.9 | 2.01 | 300 | scan=4.0 drift=+22.5% | 15:21:21 |
| S02_TETSUBAN | 039R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 14:49:32 |
| S01_NAKAANA1 | 029R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=- drift=- | 14:45:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | -3.3% | -81.4% | +157.5% | 16 | 10 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.7s |
| **Latency** (scan→final max) | 611.8s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 319 | 0.4540 | 0.3229 | +0.1311 | 🟡+29% | 0.2339 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4207 | 0.2841 | 0.2212 | 🔴-0.09 | 0.964 |
| S01_NAKAANA1 | win | 92 | 0.4860 | 0.3043 | 0.2463 | 🔴-0.16 | 0.8 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2234 | 0.4167 | 🔴-0.1933 |
| 0.30-0.50 | 140 | 0.4164 | 0.2857 | 🔴+0.1307 |
| 0.50+ | 152 | 0.5400 | 0.3750 | 🔴+0.1650 |

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
_auto-generated by claude_snapshot.py at 2026-05-29T08:40:01.742734+09:00_