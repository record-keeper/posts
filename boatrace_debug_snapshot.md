# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-04T11:40:01.865498+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×16 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-10-04T11:34:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-04T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-04T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-10-04T11:03:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-10-04T11:03:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×34  [2026-10-04T10:42:35]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×42  [2026-10-04T10:00:12]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-10-04T09:01:43]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:02:06]
- key: `ROI_STAT|E2E_TEST_A_IGNORE`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-04T06:01:46]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-04T06:01:46]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S00: n=164 hit%=21.3% hit_CI[Bonf]=[13.6,31.8]% ROI=0.61 ROI_boot95=[0.40,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=27.4% hit_CI[Bonf]=[18.7,38.4]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-04T06:01:46]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=47.1% hit_CI[Bonf]=[32.4,62.2]% ROI=0.81 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-04T06:01:46]
- key: `ORPHAN_SCAN|186 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=26.1% ROI=0.67 (コスト 10,600/回収 7,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-04T06:01:46]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=27.0% ROI=0.70 (コスト 20,400/回収 14,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.88MB / last modified 2026-10-04T11:39:29.480166+09:00

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
arsed
2026-10-04 11:38:49,244 [INFO] scraper: fetch_race 11/4: boats=6 odds=184/191
2026-10-04 11:38:49,247 [INFO] predictor: CALIBRATION_MODE=on
2026-10-04 11:38:49,247 [INFO] predictor: combos: {'win': 5, '2t': 26, '3t': 120}
2026-10-04 11:38:49,250 [INFO] run_cycle: fetched 11/4 [scan]: 151 combos
2026-10-04 11:38:49,452 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-04 11:39:05,106 [INFO] run_cycle: === run_cycle 11:39:05 ===
2026-10-04 11:39:05,106 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-04 11:39:05,106 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-04 11:39:05,198 [INFO] predictor: Models loaded OK
2026-10-04 11:39:17,704 [INFO] scraper: odds3t: 120/120 parsed
2026-10-04 11:39:18,805 [INFO] scraper: odds3f: 20/20 parsed
2026-10-04 11:39:19,910 [INFO] scraper: odds2t: 30/30 parsed
2026-10-04 11:39:19,911 [INFO] scraper: odds2f: 15/15 parsed
2026-10-04 11:39:21,252 [INFO] scraper: odds_win: 6/6 parsed
2026-10-04 11:39:21,252 [INFO] scraper: fetch_race 05/3: boats=6 odds=191/191
2026-10-04 11:39:21,256 [INFO] predictor: CALIBRATION_MODE=on
2026-10-04 11:39:21,256 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-04 11:39:21,261 [INFO] run_cycle: fetched 05/3 [final]: 156 combos
2026-10-04 11:39:25,084 [INFO] scraper: odds3t: 120/120 parsed
2026-10-04 11:39:26,301 [INFO] scraper: odds3f: 16/20 parsed
2026-10-04 11:39:27,432 [INFO] scraper: odds2t: 19/30 parsed
2026-10-04 11:39:27,434 [INFO] scraper: odds2f: 8/15 parsed
2026-10-04 11:39:28,589 [INFO] scraper: odds_win: 3/6 parsed
2026-10-04 11:39:28,589 [INFO] scraper: fetch_race 22/3: boats=6 odds=166/191
2026-10-04 11:39:28,591 [INFO] predictor: CALIBRATION_MODE=on
2026-10-04 11:39:28,591 [INFO] predictor: combos: {'win': 3, '2t': 19, '3t': 120}
2026-10-04 11:39:28,595 [INFO] run_cycle: fetched 22/3 [scan]: 142 combos
2026-10-04 11:39:28,763 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 30, 'result': 13, 'scan': 32}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 64
  ANOMALY_SCRAPER_FAILURE_BURST: 52
  CIRCUIT_BREAKER_NO_ACTION: 33
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 16
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 12 | 15,000 | 11,310 | -3,690 | 0.754 |
| S01_NAKAANA1 | 48 | 16 | 9,600 | 11,500 | +1,900 | 1.198 |
| S02_TETSUBAN | 19 | 9 | 3,800 | 2,560 | -1,240 | 0.674 |

## 直近アラート (24h・新しい順)
```
[11:39:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1275}
[11:38:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1266}
[11:38:49] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.197, "baseline_mean": 0.803, "baseline_stdev": 0.068, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 7, "z_score": 2.91}
[11:37:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1264}
[11:36:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1254}
[11:35:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1246}
[11:34:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1236}
[11:32:50] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -20.0, "final": 3.6, "kind": "LARGE_ODDS_DRIFT", "race": "187R", "scan": 4.5, "sid": "S01_NAKAANA1"}
[11:09:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.197, "baseline_mean": 0.803, "baseline_stdev": 0.068, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 5, "z_score": 2.91}
[11:03:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 122件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 34件 締切済
- 通知発射: scan=7 nid / final=9 nid / result=3 nid
- predictions: 6 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.5 drift=-20.0% | 11:32:31 |
| S00 | 061R | win | 1 | 0.1760 | 4.0 | 0.70 | 300 | scan=- drift=- | 11:09:31 |
| S01_NAKAANA1 | 132R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.2 drift=+9.4% | 11:09:21 |
| S01_NAKAANA1 | 186R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 10:59:43 |
| S01_NAKAANA1 | 021R | win | 1 | 0.6037 | 3.3 | 1.99 | 200 | scan=3.3 drift=+0.0% | 10:44:21 |
| S00 | 131R | win | 1 | 0.5097 | 13.1 | 6.68 | 300 | scan=16.8 drift=-22.0% | 10:42:20 |
| S01_NAKAANA1 | 129R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=3.2 drift=+6.2% | 18:51:20 |
| S00 | 071R | win | 1 | 0.5123 | 6.0 | 3.07 | 300 | scan=4.8 drift=+25.0% | 15:18:31 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=- drift=- | 14:49:20 |
| S00 | 227R | win | 1 | 0.4989 | 9.3 | 4.64 | 300 | scan=6.7 drift=+38.8% | 14:12:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 77 | +7.4% | -76.2% | +169.2% | 23 | 10 | 55 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.4s |
| **Latency** (scan→final max) | 631.9s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4797 | 0.2906 | +0.1891 | 🟡+39% | 0.2478 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4488 | 0.2073 | 0.2461 | 🔴-0.50 | 0.598 |
| S01_NAKAANA1 | win | 164 | 0.4886 | 0.2805 | 0.2465 | 🔴-0.22 | 0.912 |
| S02_TETSUBAN | win | 85 | 0.5219 | 0.4706 | 0.2535 | 🔴-0.02 | 0.806 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.20-0.30 | 5 | 0.2203 | 0.2000 | ✅+0.0203 |
| 0.30-0.50 | 158 | 0.4194 | 0.2595 | 🔴+0.1599 |
| 0.50+ | 239 | 0.5421 | 0.3138 | 🔴+0.2283 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 167 | 0.77 |
| win | <5.0 | ✅learned | 289 | 0.765 |
| win | <10.0 | ✅learned | 133 | 0.46 |
| win | <20.0 | ✅learned | 36 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-04T11:40:01.865498+09:00_