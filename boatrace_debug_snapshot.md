# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-28T12:00:01.906355+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×37 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×52 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-08-28T11:48:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×29  [2026-08-28T11:30:11]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-28T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-28T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-08-28T11:02:19]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×112  [2026-08-28T11:02:19]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-08-28T11:02:19]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-08-28T10:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S00: n=174 hit%=27.6% hit_CI[Bonf]=[19.0,38.2]% ROI=0.88 ROI_boot95=[0.63,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=25.8% hit_CI[Bonf]=[17.8,35.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=39.7% hit_CI[Bonf]=[25.5,56.0]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-28T06:00:10]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=40 hit%=20.0% ROI=0.62 (コスト 11,600/回収 7,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=32.6% ROI=0.96 (コスト 10,100/回収 9,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.7MB / last modified 2026-08-28T12:00:04.645874+09:00

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
2026-08-28 11:57:27,315 [INFO] scraper: odds2t: 30/30 parsed
2026-08-28 11:57:27,316 [INFO] scraper: odds2f: 13/15 parsed
2026-08-28 11:57:28,417 [INFO] scraper: odds_win: 5/6 parsed
2026-08-28 11:57:28,417 [INFO] scraper: fetch_race 10/8: boats=6 odds=188/191
2026-08-28 11:57:28,420 [INFO] predictor: CALIBRATION_MODE=on
2026-08-28 11:57:28,420 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-28 11:57:28,424 [INFO] run_cycle: fetched 10/8 [scan]: 155 combos
2026-08-28 11:57:28,538 [INFO] run_cycle: run_cycle done: 1 notifications
2026-08-28 11:58:03,462 [INFO] run_cycle: === run_cycle 11:58:03 ===
2026-08-28 11:58:03,462 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 11:58:03,462 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 11:58:03,510 [INFO] predictor: Models loaded OK
2026-08-28 11:58:16,018 [INFO] scraper: odds3t: 120/120 parsed
2026-08-28 11:58:17,109 [INFO] scraper: odds3f: 20/20 parsed
2026-08-28 11:58:18,192 [INFO] scraper: odds2t: 30/30 parsed
2026-08-28 11:58:18,193 [INFO] scraper: odds2f: 15/15 parsed
2026-08-28 11:58:19,264 [INFO] scraper: odds_win: 5/6 parsed
2026-08-28 11:58:19,264 [INFO] scraper: fetch_race 05/2: boats=6 odds=190/191
2026-08-28 11:58:19,268 [INFO] predictor: CALIBRATION_MODE=on
2026-08-28 11:58:19,268 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-28 11:58:19,272 [INFO] run_cycle: fetched 05/2 [final]: 155 combos
2026-08-28 11:58:19,582 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 11:59:04,227 [INFO] run_cycle: === run_cycle 11:59:04 ===
2026-08-28 11:59:04,227 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 11:59:04,227 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 11:59:04,259 [INFO] predictor: Models loaded OK
2026-08-28 11:59:04,364 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 89
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 89
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 23, 'scan': 32}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 52
  CIRCUIT_BREAKER_NO_ACTION: 45
  CIRCUIT_BREAKER_TRIP: 37
  ANOMALY_SCAN_FINAL_RATIO: 28
  ANOMALY_SCRAPER_FAILURE_BURST: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 10 | 13,500 | 9,510 | -3,990 | 0.704 |
| S01_NAKAANA1 | 51 | 12 | 10,200 | 5,920 | -4,280 | 0.58 |
| S02_TETSUBAN | 17 | 7 | 3,400 | 2,800 | -600 | 0.824 |

## 直近アラート (24h・新しい順)
```
[11:59:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1096}
[11:58:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1099}
[11:57:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1091}
[11:56:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1083}
[11:54:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1110}
[11:53:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1117}
[11:52:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1108}
[11:51:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1122}
[11:50:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1127}
[11:50:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.163, "baseline_mean": 0.799, "baseline_stdev": 0.047, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -3.47}
```

## 本日残レース: 104件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 40件 締切済
- 通知発射: scan=11 nid / final=9 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 052R | win | 1 | 0.5113 | 5.2 | 2.66 | 300 | scan=4.0 drift=+30.0% | 11:57:18 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5074 | 3.5 | 1.78 | 200 | scan=4.0 drift=-12.5% | 11:46:19 |
| S00 | 093R | win | 1 | 0.5123 | 8.2 | 4.20 | 300 | scan=4.5 drift=+82.2% | 11:21:19 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5164 | 3.0 | 1.55 | 200 | scan=- drift=- | 11:14:21 |
| S02_TETSUBAN | 132R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:56:37 |
| S00 | 092R | win | 1 | 0.1957 | 5.1 | 1.00 | 300 | scan=4.8 drift=+6.2% | 10:55:20 |
| S00 | 131R | win | 1 | 0.3197 | 7.0 | 2.24 | 300 | scan=26.2 drift=-73.3% | 10:33:30 |
| S02_TETSUBAN | 078R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.2 drift=-9.1% | 18:33:18 |
| S00 | 073R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=6.5 drift=+46.2% | 16:08:30 |
| S01_NAKAANA1 | 228R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 15:46:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +2.1% | -79.6% | +320.7% | 25 | 12 | 51 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 492.6s |
| **Latency** (scan→final max) | 648.5s |
| **Traffic** (notifications 24h) | 89 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 447 | 0.4704 | 0.2886 | +0.1818 | 🟡+39% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4161 | 0.2712 | 0.2182 | 🔴-0.10 | 0.866 |
| S01_NAKAANA1 | win | 191 | 0.4905 | 0.2565 | 0.2487 | 🔴-0.30 | 0.802 |
| S02_TETSUBAN | win | 79 | 0.5434 | 0.4051 | 0.2573 | 🔴-0.07 | 0.667 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 157 | 0.4131 | 0.2293 | 🔴+0.1838 |
| 0.50+ | 256 | 0.5451 | 0.3398 | 🔴+0.2053 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 121 | 0.776 |
| win | <5.0 | ✅learned | 224 | 0.746 |
| win | <10.0 | ✅learned | 107 | 0.456 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-28T12:00:01.906355+09:00_