# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-06T12:00:01.768844+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-10-06T11:51:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-06T11:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-10-06T11:25:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×58  [2026-10-06T11:02:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-10-06T11:02:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-10-06T11:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-06T10:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-06T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-06T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S00: n=167 hit%=22.8% hit_CI[Bonf]=[14.8,33.3]% ROI=0.63 ROI_boot95=[0.43,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=30.5% hit_CI[Bonf]=[21.4,41.5]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-06T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=48.2% hit_CI[Bonf]=[33.3,63.5]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-06T06:00:21]
- key: `ORPHAN_SCAN|174 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=40.6% ROI=1.12 (コスト 8,900/回収 9,950)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=25.5% ROI=0.69 (コスト 12,000/回収 8,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=28.1% ROI=0.75 (コスト 20,100/回収 15,050)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=36.4% ROI=0.81 (コスト 10,200/回収 8,240)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-06T06:00:21]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=21.7% ROI=0.66 (コスト 12,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.05MB / last modified 2026-10-06T12:00:05.079311+09:00

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
2026-10-06 11:58:25,814 [INFO] scraper: fetch_race 05/4: boats=6 odds=181/191
2026-10-06 11:58:25,817 [INFO] predictor: CALIBRATION_MODE=on
2026-10-06 11:58:25,817 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-10-06 11:58:25,821 [INFO] run_cycle: fetched 05/4 [scan]: 150 combos
2026-10-06 11:58:25,941 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-06 11:59:04,212 [INFO] run_cycle: === run_cycle 11:59:04 ===
2026-10-06 11:59:04,212 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-06 11:59:04,212 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-06 11:59:04,260 [INFO] predictor: Models loaded OK
2026-10-06 11:59:16,748 [INFO] scraper: odds3t: 120/120 parsed
2026-10-06 11:59:17,987 [INFO] scraper: odds3f: 20/20 parsed
2026-10-06 11:59:19,137 [INFO] scraper: odds2t: 30/30 parsed
2026-10-06 11:59:19,139 [INFO] scraper: odds2f: 15/15 parsed
2026-10-06 11:59:20,226 [INFO] scraper: odds_win: 6/6 parsed
2026-10-06 11:59:20,226 [INFO] scraper: fetch_race 10/4: boats=6 odds=191/191
2026-10-06 11:59:20,230 [INFO] predictor: CALIBRATION_MODE=on
2026-10-06 11:59:20,230 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-06 11:59:20,234 [INFO] run_cycle: fetched 10/4 [final]: 156 combos
2026-10-06 11:59:24,084 [INFO] scraper: odds3t: 120/120 parsed
2026-10-06 11:59:25,193 [INFO] scraper: odds3f: 20/20 parsed
2026-10-06 11:59:26,333 [INFO] scraper: odds2t: 30/30 parsed
2026-10-06 11:59:26,334 [INFO] scraper: odds2f: 14/15 parsed
2026-10-06 11:59:27,423 [INFO] scraper: odds_win: 3/6 parsed
2026-10-06 11:59:27,423 [INFO] scraper: fetch_race 18/8: boats=6 odds=187/191
2026-10-06 11:59:27,427 [INFO] predictor: CALIBRATION_MODE=on
2026-10-06 11:59:27,427 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-10-06 11:59:27,432 [INFO] run_cycle: fetched 18/8 [scan]: 153 combos
2026-10-06 11:59:27,664 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 51
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 51
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 11, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 84
  FINAL_MISSING: 48
  CIRCUIT_BREAKER_NO_ACTION: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 16 | 15,600 | 13,140 | -2,460 | 0.842 |
| S01_NAKAANA1 | 49 | 20 | 9,800 | 14,700 | +4,900 | 1.5 |
| S02_TETSUBAN | 16 | 6 | 3,200 | 1,720 | -1,480 | 0.537 |

## 直近アラート (24h・新しい順)
```
[11:47:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.273, "baseline_mean": 0.845, "baseline_stdev": 0.076, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -3.6}
[11:45:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.178, "baseline_mean": 0.845, "baseline_stdev": 0.076, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 6, "z_score": -2.34}
[11:35:38] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.345, "baseline_mean": 0.845, "baseline_stdev": 0.076, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -4.53}
[11:29:40] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.245, "baseline_mean": 0.845, "baseline_stdev": 0.076, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -3.22}
[11:28:31] FINAL_MISSING: {"deadline": "2026-10-06T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100611021058", "sid": "S00"}
[11:28:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1150}
[11:27:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1153}
[11:26:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1136}
[11:25:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1144}
[11:24:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1149}
```

## 本日残レース: 118件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 38件 締切済
- 通知発射: scan=7 nid / final=6 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 052R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 11:05:19 |
| S00 | 144R | win | 1 | 0.5719 | 9.3 | 5.32 | 300 | scan=- drift=- | 09:50:20 |
| S02_TETSUBAN | 209R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=2.1 drift=+9.5% | 21:38:20 |
| S01_NAKAANA1 | 206R | win | 1 | 0.5476 | 3.5 | 1.92 | 200 | scan=- drift=- | 20:22:20 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=3.5 drift=+31.4% | 18:05:19 |
| S00 | 056R | win | 1 | 0.3177 | 10.0 | 3.18 | 300 | scan=20.5 drift=-51.2% | 13:09:19 |
| S00 | 225R | win | 1 | 0.3177 | 6.3 | 2.00 | 300 | scan=7.5 drift=-16.0% | 13:06:19 |
| S00 | 096R | win | 1 | 0.5334 | 4.2 | 2.24 | 300 | scan=13.5 drift=-68.9% | 12:50:20 |
| S00 | 116R | win | 1 | 0.5334 | 7.8 | 4.16 | 300 | scan=9.0 drift=-13.3% | 12:44:19 |
| S01_NAKAANA1 | 223R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.2 drift=-14.3% | 11:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 79 | +4.2% | -76.2% | +169.2% | 27 | 12 | 60 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.2s |
| **Latency** (scan→final max) | 609.4s |
| **Traffic** (notifications 24h) | 51 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4782 | 0.3058 | +0.1724 | 🟡+36% | 0.2487 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4481 | 0.2229 | 0.2454 | 🔴-0.42 | 0.583 |
| S01_NAKAANA1 | win | 165 | 0.4866 | 0.3030 | 0.2491 | 🔴-0.18 | 1.006 |
| S02_TETSUBAN | win | 81 | 0.5228 | 0.4815 | 0.2549 | 🔴-0.02 | 0.81 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 163 | 0.4191 | 0.2822 | 🔴+0.1369 |
| 0.50+ | 233 | 0.5427 | 0.3262 | 🔴+0.2166 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 168 | 0.768 |
| win | <5.0 | ✅learned | 298 | 0.766 |
| win | <10.0 | ✅learned | 136 | 0.457 |
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
_auto-generated by claude_snapshot.py at 2026-10-06T12:00:01.768844+09:00_