# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-06T12:50:02.035555+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×33 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×47  [2026-07-06T12:03:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×47  [2026-07-06T12:03:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-07-06T12:03:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-06T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×52  [2026-07-06T11:58:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-07-06T11:56:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×4  [2026-07-06T11:01:33]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-06T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=14 pred=0.2291 actual=0.0714 gap=+0.1577`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-06T06:00:15]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-06T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1746 actual=0.4286 gap=-0.2540`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S00: n=167 hit%=28.7% hit_CI[Bonf]=[19.8,39.7]% ROI=0.78 ROI_boot95=[0.57,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=149 hit%=32.2% hit_CI[Bonf]=[22.4,44.0]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-06T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-06T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=38.5% hit_CI[Bonf]=[24.4,54.7]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=31.4% ROI=0.94 (コスト 10,200/回収 9,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=42 hit%=26.2% ROI=0.63 (コスト 9,900/回収 6,240)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=93 hit%=31.2% ROI=0.76 (コスト 21,600/回収 16,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-06T06:00:15]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=29 hit%=37.9% ROI=1.08 (コスト 7,100/回収 7,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.92MB / last modified 2026-07-06T12:49:07.167413+09:00

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
2026-07-06 12:47:21,650 [INFO] scraper: odds2t: 30/30 parsed
2026-07-06 12:47:21,651 [INFO] scraper: odds2f: 15/15 parsed
2026-07-06 12:47:22,759 [INFO] scraper: odds_win: 6/6 parsed
2026-07-06 12:47:22,759 [INFO] scraper: fetch_race 21/10: boats=6 odds=191/191
2026-07-06 12:47:22,772 [INFO] predictor: CALIBRATION_MODE=on
2026-07-06 12:47:22,772 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-06 12:47:22,780 [INFO] run_cycle: fetched 21/10 [final]: 156 combos
2026-07-06 12:47:26,278 [INFO] scraper: odds3t: 120/120 parsed
2026-07-06 12:47:27,396 [INFO] scraper: odds3f: 20/20 parsed
2026-07-06 12:47:28,532 [INFO] scraper: odds2t: 30/30 parsed
2026-07-06 12:47:28,533 [INFO] scraper: odds2f: 15/15 parsed
2026-07-06 12:47:29,607 [INFO] scraper: odds_win: 6/6 parsed
2026-07-06 12:47:29,608 [INFO] scraper: fetch_race 04/3: boats=6 odds=191/191
2026-07-06 12:47:29,617 [INFO] predictor: CALIBRATION_MODE=on
2026-07-06 12:47:29,617 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-06 12:47:29,625 [INFO] run_cycle: fetched 04/3 [scan]: 156 combos
2026-07-06 12:47:29,736 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-06 12:48:05,964 [INFO] run_cycle: === run_cycle 12:48:05 ===
2026-07-06 12:48:05,964 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-06 12:48:05,964 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-06 12:48:06,040 [INFO] predictor: Models loaded OK
2026-07-06 12:48:06,250 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-06 12:49:06,065 [INFO] run_cycle: === run_cycle 12:49:06 ===
2026-07-06 12:49:06,065 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-06 12:49:06,065 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-06 12:49:06,126 [INFO] predictor: Models loaded OK
2026-07-06 12:49:06,271 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 19, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 177
  FINAL_MISSING: 33
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_BET_VOLUME_DROP: 3
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 9 | 10,500 | 6,450 | -4,050 | 0.614 |
| S01_NAKAANA1 | 36 | 10 | 7,200 | 5,180 | -2,020 | 0.719 |
| S02_TETSUBAN | 27 | 13 | 5,400 | 4,680 | -720 | 0.867 |

## 直近アラート (24h・新しい順)
```
[12:49:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 990}
[12:48:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 994}
[12:47:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 989}
[12:46:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 980}
[12:45:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 986}
[12:44:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 979}
[12:43:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 976}
[12:42:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 989}
[12:41:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 984}
[12:40:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 960}
```

## 本日残レース: 95件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 37件 締切済
- 通知発射: scan=6 nid / final=8 nid / result=2 nid
- predictions: 5 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 2110R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.4 drift=-12.5% | 12:46:22 |
| S01_NAKAANA1 | 222R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=4.5 drift=-13.3% | 12:41:44 |
| S00 | 042R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=6.7 drift=-38.8% | 12:21:33 |
| S01_NAKAANA1 | 133R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=- drift=- | 11:23:21 |
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.6 | 1.33 | 200 | scan=- drift=- | 11:05:23 |
| S00 | 245R | win | 1 | 0.5334 | 10.8 | 5.76 | 300 | scan=- drift=- | 19:27:33 |
| S02_TETSUBAN | 078R | win | 1 | 0.5830 | 2.7 | 1.57 | 200 | scan=2.1 drift=+28.6% | 18:51:46 |
| S01_NAKAANA1 | 015R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=- drift=- | 17:27:32 |
| S02_TETSUBAN | 1611R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=2.8 drift=-28.6% | 16:08:22 |
| S01_NAKAANA1 | 011R | win | 1 | 0.3599 | 3.3 | 1.19 | 200 | scan=4.7 drift=-29.8% | 15:22:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +9.5% | -68.9% | +584.6% | 18 | 6 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.6s |
| **Latency** (scan→final max) | 623.5s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 391 | 0.4788 | 0.3223 | +0.1566 | 🟡+33% | 0.2384 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4421 | 0.2909 | 0.2229 | 🔴-0.08 | 0.785 |
| S01_NAKAANA1 | win | 148 | 0.4878 | 0.3243 | 0.2431 | 🔴-0.11 | 0.883 |
| S02_TETSUBAN | win | 78 | 0.5395 | 0.3846 | 0.2621 | 🔴-0.11 | 0.656 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1746 | 0.4286 | 🔴-0.2540 |
| 0.20-0.30 | 14 | 0.2291 | 0.0714 | 🔴+0.1577 |
| 0.30-0.50 | 136 | 0.4192 | 0.2941 | 🔴+0.1251 |
| 0.50+ | 231 | 0.5433 | 0.3550 | 🔴+0.1883 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 61 | 0.748 |
| win | <5.0 | ✅learned | 120 | 0.717 |
| win | <10.0 | ✅learned | 65 | 0.479 |
| win | <20.0 | ✅learned | 19 | 0.212 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-06T12:50:02.035555+09:00_