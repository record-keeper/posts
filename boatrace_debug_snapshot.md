# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-12T17:00:07.043061+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×15 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-10-12T16:30:40]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-10-12T16:27:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×54  [2026-10-12T16:06:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×43  [2026-10-12T15:17:26]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-12T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-10-12T10:52:20]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-10-12T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-12T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-12T06:00:19]
- key: `ORPHAN_SCAN|168 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-12T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-12T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-12T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=41.4% ROI=1.17 (コスト 8,400/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-12T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=25 pred=0.3205 actual=0.2800 gap=+0.0405`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-12T06:00:19]
- key: `ROI_STAT|S00: n=171 hit%=25.1% hit_CI[Bonf]=[16.9,35.7]% ROI=0.69 ROI_boot95=[0.49,0.93]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-12T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=34.8% hit_CI[Bonf]=[25.0,46.0]% ROI=1.05 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-12T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=51.9% hit_CI[Bonf]=[36.3,67.2]% ROI=0.92 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-12T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=49 hit%=30.6% ROI=0.76 (コスト 11,600/回収 8,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-12T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=35.6% ROI=0.93 (コスト 19,800/回収 18,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-12T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=55 hit%=38.2% ROI=0.93 (コスト 12,900/回収 12,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-12T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=21.4% ROI=0.65 (コスト 11,100/回収 7,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.61MB / last modified 2026-10-12T16:59:29.208031+09:00

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
== run_cycle 16:59:04 ===
2026-10-12 16:59:04,459 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-12 16:59:04,459 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-12 16:59:04,522 [INFO] predictor: Models loaded OK
2026-10-12 16:59:16,938 [INFO] scraper: odds3t: 120/120 parsed
2026-10-12 16:59:18,082 [INFO] scraper: odds3f: 20/20 parsed
2026-10-12 16:59:19,197 [INFO] scraper: odds2t: 30/30 parsed
2026-10-12 16:59:19,198 [INFO] scraper: odds2f: 15/15 parsed
2026-10-12 16:59:20,289 [INFO] scraper: odds_win: 6/6 parsed
2026-10-12 16:59:20,290 [INFO] scraper: fetch_race 12/5: boats=6 odds=191/191
2026-10-12 16:59:20,293 [INFO] predictor: CALIBRATION_MODE=on
2026-10-12 16:59:20,293 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-12 16:59:20,297 [INFO] run_cycle: fetched 12/5 [final]: 156 combos
2026-10-12 16:59:23,866 [INFO] scraper: odds3t: 120/120 parsed
2026-10-12 16:59:25,057 [INFO] scraper: odds3f: 20/20 parsed
2026-10-12 16:59:26,327 [INFO] scraper: odds2t: 30/30 parsed
2026-10-12 16:59:26,329 [INFO] scraper: odds2f: 15/15 parsed
2026-10-12 16:59:27,447 [INFO] scraper: odds_win: 4/6 parsed
2026-10-12 16:59:27,447 [INFO] scraper: fetch_race 15/5: boats=6 odds=189/191
2026-10-12 16:59:27,450 [INFO] predictor: CALIBRATION_MODE=on
2026-10-12 16:59:27,450 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-12 16:59:27,454 [INFO] run_cycle: fetched 15/5 [scan]: 154 combos
2026-10-12 16:59:27,566 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-12 17:00:07,050 [INFO] run_cycle: === run_cycle 17:00:07 ===
2026-10-12 17:00:07,050 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-12 17:00:07,050 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-12 17:00:07,229 [INFO] predictor: Models loaded OK
2026-10-12 17:00:07,490 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 87
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 87
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 19, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 203
  FINAL_MISSING: 44
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 15
  ANOMALY_BET_VOLUME_SPIKE: 12
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 11 | 10,500 | 9,360 | -1,140 | 0.891 |
| S01_NAKAANA1 | 38 | 16 | 7,600 | 7,420 | -180 | 0.976 |
| S02_TETSUBAN | 22 | 10 | 4,400 | 3,700 | -700 | 0.841 |

## 直近アラート (24h・新しい順)
```
[16:59:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 983}
[16:58:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 982}
[16:57:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 991}
[16:56:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1004}
[16:55:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1003}
[16:54:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1008}
[16:53:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1014}
[16:52:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1042}
[16:51:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1050}
[16:50:16] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1056}
```

## 本日残レース: 36件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 132件 締切済
- 通知発射: scan=25 nid / final=30 nid / result=16 nid
- predictions: 16 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 166R | win | 1 | 0.5998 | 2.7 | 1.62 | 200 | scan=- drift=- | 13:37:30 |
| S00 | 066R | win | 1 | 0.3177 | 6.0 | 1.91 | 300 | scan=5.2 drift=+15.4% | 13:17:31 |
| S01_NAKAANA1 | 2310R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 13:04:19 |
| S00 | 225R | win | 1 | 0.1034 | 6.9 | 0.71 | 300 | scan=- drift=- | 12:57:19 |
| S02_TETSUBAN | 096R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=2.6 drift=-23.1% | 12:53:19 |
| S00 | 189R | win | 1 | 0.5891 | 4.2 | 2.47 | 300 | scan=5.0 drift=-16.0% | 12:43:19 |
| S01_NAKAANA1 | 239R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=3.5 drift=-5.7% | 12:35:19 |
| S02_TETSUBAN | 115R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 12:20:20 |
| S01_NAKAANA1 | 064R | win | 1 | 0.3177 | 4.5 | 1.43 | 200 | scan=3.3 drift=+36.4% | 12:14:44 |
| S02_TETSUBAN | 033R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 12:05:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +13.2% | -60.0% | +326.7% | 14 | 5 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.6s |
| **Latency** (scan→final max) | 617.3s |
| **Traffic** (notifications 24h) | 87 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 424 | 0.4827 | 0.3396 | +0.1431 | 🟡+30% | 0.2516 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4527 | 0.2471 | 0.2526 | 🔴-0.36 | 0.683 |
| S01_NAKAANA1 | win | 167 | 0.4922 | 0.3533 | 0.2479 | 🔴-0.08 | 1.065 |
| S02_TETSUBAN | win | 83 | 0.5265 | 0.5060 | 0.2569 | 🔴-0.03 | 0.901 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 154 | 0.4178 | 0.3052 | 🔴+0.1126 |
| 0.50+ | 254 | 0.5437 | 0.3622 | 🔴+0.1815 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 178 | 0.771 |
| win | <5.0 | ✅learned | 318 | 0.757 |
| win | <10.0 | ✅learned | 138 | 0.461 |
| win | <20.0 | ✅learned | 39 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-12T17:00:07.043061+09:00_