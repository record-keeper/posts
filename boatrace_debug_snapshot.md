# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-15T19:10:02.159135+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-15T19:08:03]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×2  [2026-07-15T19:08:03]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-15T19:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-07-15T17:38:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×18  [2026-07-15T11:36:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=68<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-15T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=16 pred=0.2282 actual=0.1875 gap=+0.0407`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S00: n=173 hit%=28.9% hit_CI[Bonf]=[20.1,39.6]% ROI=0.74 ROI_boot95=[0.55,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-15T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.1% hit_CI[Bonf]=[20.6,41.6]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-15T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=68 hit%=42.6% hit_CI[Bonf]=[27.1,59.8]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-15T06:00:08]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=33.3% ROI=0.78 (コスト 11,000/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=31.0% ROI=0.82 (コスト 19,900/回収 16,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=30.6% ROI=0.60 (コスト 8,900/回収 5,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-15T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.71MB / last modified 2026-07-15T19:09:19.259183+09:00

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
ult=5000
2026-07-15 19:06:03,344 [INFO] predictor: Models loaded OK
2026-07-15 19:06:03,441 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-15 19:07:04,301 [INFO] run_cycle: === run_cycle 19:07:04 ===
2026-07-15 19:07:04,301 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-15 19:07:04,301 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-15 19:07:04,345 [INFO] predictor: Models loaded OK
2026-07-15 19:07:04,443 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-15 19:08:03,436 [INFO] run_cycle: === run_cycle 19:08:03 ===
2026-07-15 19:08:03,436 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-15 19:08:03,436 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-15 19:08:03,479 [INFO] predictor: Models loaded OK
2026-07-15 19:08:03,483 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-15 19:09:03,387 [INFO] run_cycle: === run_cycle 19:09:03 ===
2026-07-15 19:09:03,387 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-15 19:09:03,387 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-15 19:09:03,442 [INFO] predictor: Models loaded OK
2026-07-15 19:09:15,794 [INFO] scraper: odds3t: 120/120 parsed
2026-07-15 19:09:16,901 [INFO] scraper: odds3f: 20/20 parsed
2026-07-15 19:09:18,004 [INFO] scraper: odds2t: 30/30 parsed
2026-07-15 19:09:18,005 [INFO] scraper: odds2f: 15/15 parsed
2026-07-15 19:09:19,108 [INFO] scraper: odds_win: 5/6 parsed
2026-07-15 19:09:19,108 [INFO] scraper: fetch_race 07/9: boats=6 odds=190/191
2026-07-15 19:09:19,111 [INFO] predictor: CALIBRATION_MODE=on
2026-07-15 19:09:19,111 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-15 19:09:19,115 [INFO] run_cycle: fetched 07/9 [final]: 155 combos
2026-07-15 19:09:19,211 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 48
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 48
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 13, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 161
  FINAL_MISSING: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 16 | 15,000 | 14,070 | -930 | 0.938 |
| S01_NAKAANA1 | 39 | 13 | 7,800 | 7,000 | -800 | 0.897 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 2,860 | +60 | 1.021 |

## 直近アラート (24h・新しい順)
```
[19:08:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[19:08:03] FINAL_MISSING: {"deadline": "2026-07-15T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071513031132", "sid": "S00"}
[19:08:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[18:36:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 709}
[18:35:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 705}
[18:33:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 699}
[18:32:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 705}
[18:29:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 707}
[18:27:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 726}
[18:26:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 708}
```

## 本日残レース: 18件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 150件 締切済
- 通知発射: scan=13 nid / final=18 nid / result=12 nid
- predictions: 12 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 012R | win | 1 | 0.5313 | 3.2 | 1.70 | 200 | scan=4.0 drift=-20.0% | 15:46:21 |
| S00 | 225R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=5.0 drift=-18.0% | 14:16:19 |
| S00 | 189R | win | 1 | 0.5735 | 5.0 | 2.87 | 300 | scan=- drift=- | 12:30:32 |
| S00 | 174R | win | 1 | 0.5079 | 4.5 | 2.29 | 300 | scan=- drift=- | 12:11:19 |
| S00 | 084R | win | 1 | 0.2290 | 4.1 | 0.94 | 300 | scan=4.5 drift=-8.9% | 12:03:31 |
| S00 | 134R | win | 1 | 0.1303 | 9.3 | 1.21 | 300 | scan=- drift=- | 11:58:18 |
| S01_NAKAANA1 | 238R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 11:51:19 |
| S00 | 082R | win | 1 | 0.4111 | 22.1 | 9.09 | 300 | scan=- drift=- | 11:05:19 |
| S01_NAKAANA1 | 186R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=- drift=- | 10:56:29 |
| S01_NAKAANA1 | 081R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=3.0 drift=+0.0% | 10:37:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +21.3% | -73.3% | +533.3% | 17 | 5 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 376.1s |
| **Latency** (scan→final max) | 599.7s |
| **Traffic** (notifications 24h) | 48 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4696 | 0.3192 | +0.1504 | 🟡+32% | 0.2376 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4286 | 0.2881 | 0.2261 | 🔴-0.10 | 0.741 |
| S01_NAKAANA1 | win | 156 | 0.4838 | 0.3077 | 0.2398 | 🔴-0.13 | 0.793 |
| S02_TETSUBAN | win | 68 | 0.5440 | 0.4265 | 0.2626 | 🔴-0.07 | 0.85 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2282 | 0.2000 | ✅+0.0282 |
| 0.30-0.50 | 148 | 0.4177 | 0.2770 | 🔴+0.1407 |
| 0.50+ | 223 | 0.5425 | 0.3543 | 🔴+0.1883 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 70 | 0.794 |
| win | <5.0 | ✅learned | 142 | 0.712 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-15T19:10:02.159135+09:00_