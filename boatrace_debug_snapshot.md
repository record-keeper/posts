# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-01T12:30:01.364474+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🟡 FINAL_MISSING×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×29  [2026-08-01T12:01:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×58  [2026-08-01T12:01:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×29  [2026-08-01T12:01:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×37  [2026-08-01T11:33:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-01T11:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-01T11:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-01T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-01T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-01T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-01T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=35.9% ROI=0.87 (コスト 9,600/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-01T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=8 pred=0.1275 actual=0.1250 gap=+0.0025`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-01T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-01T06:00:08]
- key: `ROI_STAT|S00: n=174 hit%=27.0% hit_CI[Bonf]=[18.5,37.6]% ROI=0.74 ROI_boot95=[0.52,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-01T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=26.1% hit_CI[Bonf]=[17.5,37.1]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-01T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=51.9% hit_CI[Bonf]=[36.4,66.9]% ROI=1.02 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-01T06:00:08]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-01T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=26.7% ROI=0.62 (コスト 8,800/回収 5,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-01T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=71 hit%=31.0% ROI=0.73 (コスト 16,500/回収 11,970)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-01T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=25.6% ROI=0.50 (コスト 10,100/回収 5,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-01T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=21.6% ROI=0.78 (コスト 10,300/回収 8,000)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.17MB / last modified 2026-08-01T12:30:04.327233+09:00

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
2026-08-01 12:27:28,398 [INFO] scraper: odds2t: 30/30 parsed
2026-08-01 12:27:28,399 [INFO] scraper: odds2f: 13/15 parsed
2026-08-01 12:27:29,497 [INFO] scraper: odds_win: 5/6 parsed
2026-08-01 12:27:29,497 [INFO] scraper: fetch_race 08/5: boats=6 odds=188/191
2026-08-01 12:27:29,500 [INFO] predictor: CALIBRATION_MODE=on
2026-08-01 12:27:29,500 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-01 12:27:29,503 [INFO] run_cycle: fetched 08/5 [scan]: 155 combos
2026-08-01 12:27:29,596 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-01 12:28:04,071 [INFO] run_cycle: === run_cycle 12:28:04 ===
2026-08-01 12:28:04,071 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-01 12:28:04,071 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-01 12:28:04,099 [INFO] predictor: Models loaded OK
2026-08-01 12:28:16,513 [INFO] scraper: odds3t: 120/120 parsed
2026-08-01 12:28:17,583 [INFO] scraper: odds3f: 20/20 parsed
2026-08-01 12:28:18,754 [INFO] scraper: odds2t: 30/30 parsed
2026-08-01 12:28:18,756 [INFO] scraper: odds2f: 15/15 parsed
2026-08-01 12:28:19,847 [INFO] scraper: odds_win: 5/6 parsed
2026-08-01 12:28:19,847 [INFO] scraper: fetch_race 06/3: boats=6 odds=190/191
2026-08-01 12:28:19,851 [INFO] predictor: CALIBRATION_MODE=on
2026-08-01 12:28:19,851 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-01 12:28:19,856 [INFO] run_cycle: fetched 06/3 [final]: 155 combos
2026-08-01 12:28:20,160 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-01 12:29:03,531 [INFO] run_cycle: === run_cycle 12:29:03 ===
2026-08-01 12:29:03,531 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-01 12:29:03,531 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-01 12:29:03,559 [INFO] predictor: Models loaded OK
2026-08-01 12:29:03,662 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 78
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 27
  CIRCUIT_BREAKER_TRIP: 25
  FINAL_MISSING: 23
  STRATEGY_CI_FAIL: 17
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 7 | 11,100 | 4,830 | -6,270 | 0.435 |
| S01_NAKAANA1 | 35 | 11 | 7,000 | 6,900 | -100 | 0.986 |
| S02_TETSUBAN | 19 | 7 | 3,800 | 2,300 | -1,500 | 0.605 |

## 直近アラート (24h・新しい順)
```
[12:27:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.189, "baseline_mean": 0.811, "baseline_stdev": 0.089, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 7, "z_score": 2.13}
[12:22:19] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4830, "roi_7d": 0.435, "sid": "S00"}
[12:01:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:01:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:51:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.189, "baseline_mean": 0.811, "baseline_stdev": 0.089, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 6, "z_score": 2.13}
[11:41:47] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 4830, "roi_7d": 0.447, "sid": "S00"}
[11:22:52] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.189, "baseline_mean": 0.811, "baseline_stdev": 0.089, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 5, "z_score": 2.13}
[11:21:30] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4830, "roi_7d": 0.435, "sid": "S00"}
[11:17:28] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4320, "roi_7d": 0.389, "sid": "S00"}
```

## 本日残レース: 108件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 48件 締切済
- 通知発射: scan=7 nid / final=9 nid / result=6 nid
- predictions: 6 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 238R | win | 1 | 0.5123 | 8.3 | 4.25 | 300 | scan=4.0 drift=+107.5% | 11:51:20 |
| S02_TETSUBAN | 134R | win | 1 | 0.5719 | 2.1 | 1.20 | 200 | scan=- drift=- | 11:45:18 |
| S02_TETSUBAN | 133R | win | 1 | 0.4989 | 2.9 | 1.45 | 200 | scan=2.7 drift=+7.4% | 11:22:43 |
| S00 | 237R | win | 1 | 0.1123 | 4.2 | 0.47 | 300 | scan=- drift=- | 11:17:19 |
| S00 | 236R | win | 1 | 0.4111 | 5.1 | 2.10 | 300 | scan=5.6 drift=-8.9% | 10:48:19 |
| S00 | 131R | win | 1 | 0.5735 | 4.8 | 2.75 | 300 | scan=7.5 drift=-36.0% | 10:32:20 |
| S01_NAKAANA1 | 0111R | win | 1 | 0.5174 | 4.4 | 2.28 | 200 | scan=3.4 drift=+29.4% | 19:56:30 |
| S01_NAKAANA1 | 0110R | win | 1 | 0.5891 | 3.3 | 1.94 | 200 | scan=- drift=- | 19:30:23 |
| S01_NAKAANA1 | 226R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=- drift=- | 14:49:22 |
| S00 | 226R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=7.5 drift=-46.7% | 14:49:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +14.2% | -86.1% | +375.6% | 15 | 9 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 446.9s |
| **Latency** (scan→final max) | 602.8s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 420 | 0.4615 | 0.3143 | +0.1472 | 🟡+32% | 0.2341 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4209 | 0.2697 | 0.2278 | 🔴-0.16 | 0.728 |
| S01_NAKAANA1 | win | 160 | 0.4715 | 0.2625 | 0.2340 | 🔴-0.21 | 0.788 |
| S02_TETSUBAN | win | 82 | 0.5301 | 0.5122 | 0.2480 | ✅+0.01 | 1.004 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1258 | 0.1111 | ✅+0.0147 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 12 | 0.2289 | 0.3333 | 🔴-0.1044 |
| 0.30-0.50 | 171 | 0.4182 | 0.2632 | 🔴+0.1550 |
| 0.50+ | 216 | 0.5401 | 0.3657 | 🔴+0.1744 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 91 | 0.796 |
| win | <5.0 | ✅learned | 164 | 0.725 |
| win | <10.0 | ✅learned | 86 | 0.455 |
| win | <20.0 | ✅learned | 26 | 0.216 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-01T12:30:01.364474+09:00_