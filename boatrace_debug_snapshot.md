# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-22T12:30:02.282353+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×43 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×7 (24h)
- 🟡 FINAL_MISSING×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-22T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×21  [2026-09-22T12:09:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-09-22T12:02:27]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×28  [2026-09-22T12:02:27]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-09-22T12:02:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-22T11:48:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×53  [2026-09-22T10:41:08]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×55  [2026-09-22T10:00:41]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-22T06:00:18]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-22T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-22T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3233 actual=0.2121 gap=+0.1112`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S00: n=166 hit%=22.9% hit_CI[Bonf]=[14.9,33.5]% ROI=0.74 ROI_boot95=[0.50,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=168 hit%=21.4% hit_CI[Bonf]=[13.8,31.8]% ROI=0.64 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-22T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=40.3% hit_CI[Bonf]=[25.5,57.1]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=25.8% ROI=0.83 (コスト 8,900/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=19.5% ROI=0.57 (コスト 9,400/回収 5,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=82 hit%=22.0% ROI=0.70 (コスト 19,000/回収 13,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-22T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.47 (コスト 10,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.82MB / last modified 2026-09-22T12:30:05.393107+09:00

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
2026-09-22 12:28:37,782 [INFO] scraper: fetch_race 03/4: boats=6 odds=190/191
2026-09-22 12:28:37,784 [INFO] predictor: CALIBRATION_MODE=on
2026-09-22 12:28:37,784 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-09-22 12:28:37,789 [INFO] run_cycle: fetched 03/4 [scan]: 155 combos
2026-09-22 12:28:41,335 [INFO] scraper: odds3t: 120/120 parsed
2026-09-22 12:28:42,465 [INFO] scraper: odds3f: 20/20 parsed
2026-09-22 12:28:43,585 [INFO] scraper: odds2t: 30/30 parsed
2026-09-22 12:28:43,586 [INFO] scraper: odds2f: 15/15 parsed
2026-09-22 12:28:44,732 [INFO] scraper: odds_win: 1/6 parsed
2026-09-22 12:28:44,733 [INFO] scraper: fetch_race 18/9: boats=6 odds=186/191
2026-09-22 12:28:44,736 [INFO] predictor: CALIBRATION_MODE=on
2026-09-22 12:28:44,736 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-09-22 12:28:44,741 [INFO] run_cycle: fetched 18/9 [scan]: 151 combos
2026-09-22 12:28:44,989 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-22 12:29:04,099 [INFO] run_cycle: === run_cycle 12:29:04 ===
2026-09-22 12:29:04,100 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-22 12:29:04,100 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-22 12:29:04,147 [INFO] predictor: Models loaded OK
2026-09-22 12:29:16,801 [INFO] scraper: odds3t: 120/120 parsed
2026-09-22 12:29:17,913 [INFO] scraper: odds3f: 20/20 parsed
2026-09-22 12:29:19,015 [INFO] scraper: odds2t: 30/30 parsed
2026-09-22 12:29:19,016 [INFO] scraper: odds2f: 15/15 parsed
2026-09-22 12:29:20,114 [INFO] scraper: odds_win: 6/6 parsed
2026-09-22 12:29:20,114 [INFO] scraper: fetch_race 11/5: boats=6 odds=191/191
2026-09-22 12:29:20,117 [INFO] predictor: CALIBRATION_MODE=on
2026-09-22 12:29:20,118 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-22 12:29:20,121 [INFO] run_cycle: fetched 11/5 [final]: 156 combos
2026-09-22 12:29:20,598 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 37
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 37
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 10, 'scan': 12}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 115
  PSI_DRIFT_DETECTED: 43
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 15
  CIRCUIT_BREAKER_TRIP: 7
  ANOMALY_BET_VOLUME_DROP: 1
  FINAL_MISSING: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 7 | 10,800 | 5,340 | -5,460 | 0.494 |
| S01_NAKAANA1 | 36 | 9 | 7,200 | 6,260 | -940 | 0.869 |
| S02_TETSUBAN | 18 | 10 | 3,600 | 3,980 | +380 | 1.106 |

## 直近アラート (24h・新しい順)
```
[12:28:45] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 315, "n_recent": 90, "psi": 0.406}
[12:23:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 316, "n_recent": 90, "psi": 0.44}
[12:12:40] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 317, "n_recent": 90, "psi": 0.44}
[12:05:31] FINAL_MISSING: {"deadline": "2026-09-22T11:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092208031135", "sid": "S00"}
[12:04:50] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:04:50] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:02:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 318, "n_recent": 90, "psi": 0.439}
[11:58:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 317, "n_recent": 91, "psi": 0.439}
[11:57:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 317, "n_recent": 90, "psi": 0.45}
[11:55:39] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 5340, "roi_7d": 0.494, "sid": "S00"}
```

## 本日残レース: 118件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 50件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 114R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=3.5 drift=+8.6% | 11:58:20 |
| S02_TETSUBAN | 113R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=- drift=- | 11:27:18 |
| S01_NAKAANA1 | 107R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=3.5 drift=-8.6% | 11:16:19 |
| S01_NAKAANA1 | 112R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=4.7 drift=-36.2% | 11:00:22 |
| S00 | 186R | win | 1 | 0.0199 | 5.2 | 0.10 | 300 | scan=5.2 drift=+0.0% | 10:56:43 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5719 | 3.1 | 1.77 | 200 | scan=3.4 drift=-8.8% | 17:07:31 |
| S02_TETSUBAN | 169R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=- drift=- | 15:02:19 |
| S00 | 179R | win | 1 | 0.4111 | 11.1 | 4.56 | 300 | scan=- drift=- | 14:44:31 |
| S01_NAKAANA1 | 166R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 13:21:31 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=4.0 drift=-25.0% | 12:22:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +0.0% | -81.7% | +119.5% | 16 | 6 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 457.5s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 37 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 404 | 0.4764 | 0.2574 | +0.2190 | 🟡+46% | 0.2427 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4418 | 0.2331 | 0.2293 | 🔴-0.28 | 0.75 |
| S01_NAKAANA1 | win | 168 | 0.4833 | 0.2143 | 0.2473 | 🔴-0.47 | 0.642 |
| S02_TETSUBAN | win | 73 | 0.5379 | 0.4110 | 0.2622 | 🔴-0.08 | 0.745 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 153 | 0.4116 | 0.2222 | 🔴+0.1893 |
| 0.50+ | 234 | 0.5433 | 0.2906 | 🔴+0.2527 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 148 | 0.773 |
| win | <5.0 | ✅learned | 260 | 0.762 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-22T12:30:02.282353+09:00_