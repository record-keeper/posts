# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-23T11:40:02.220534+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×39 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×39 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×1  [2026-06-23T11:39:06]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-06-23T11:28:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×70  [2026-06-23T11:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-06-23T11:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-06-23T11:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×4  [2026-06-23T11:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-23T10:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-23T10:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×21  [2026-06-23T09:37:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0816 actual=0.0000 gap=+0.0816`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-23T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.67 (コスト 9,700/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1808 actual=0.4286 gap=-0.2478`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S00: n=153 hit%=24.8% hit_CI[Bonf]=[16.2,36.0]% ROI=0.67 ROI_boot95=[0.47,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=139 hit%=27.3% hit_CI[Bonf]=[17.9,39.3]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=34.2% hit_CI[Bonf]=[20.8,50.8]% ROI=0.58 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-23T06:00:17]
- key: `ORPHAN_SCAN|157 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.74MB / last modified 2026-06-23T11:39:06.475174+09:00

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
=== run_cycle 11:38:05 ===
2026-06-23 11:38:05,504 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-23 11:38:05,505 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-23 11:38:05,549 [INFO] predictor: Models loaded OK
2026-06-23 11:38:18,145 [INFO] scraper: odds3t: 120/120 parsed
2026-06-23 11:38:19,238 [INFO] scraper: odds3f: 20/20 parsed
2026-06-23 11:38:20,347 [INFO] scraper: odds2t: 30/30 parsed
2026-06-23 11:38:20,348 [INFO] scraper: odds2f: 15/15 parsed
2026-06-23 11:38:21,453 [INFO] scraper: odds_win: 6/6 parsed
2026-06-23 11:38:21,453 [INFO] scraper: fetch_race 02/3: boats=6 odds=191/191
2026-06-23 11:38:21,465 [INFO] predictor: CALIBRATION_MODE=on
2026-06-23 11:38:21,465 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-23 11:38:21,472 [INFO] run_cycle: fetched 02/3 [scan]: 156 combos
2026-06-23 11:38:24,981 [INFO] scraper: odds3t: 120/120 parsed
2026-06-23 11:38:26,084 [INFO] scraper: odds3f: 20/20 parsed
2026-06-23 11:38:27,272 [INFO] scraper: odds2t: 30/30 parsed
2026-06-23 11:38:27,273 [INFO] scraper: odds2f: 15/15 parsed
2026-06-23 11:38:28,413 [INFO] scraper: odds_win: 3/6 parsed
2026-06-23 11:38:28,414 [INFO] scraper: fetch_race 10/8: boats=6 odds=188/191
2026-06-23 11:38:28,423 [INFO] predictor: CALIBRATION_MODE=on
2026-06-23 11:38:28,425 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-23 11:38:28,431 [INFO] run_cycle: fetched 10/8 [scan]: 153 combos
2026-06-23 11:38:28,550 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-23 11:39:06,017 [INFO] run_cycle: === run_cycle 11:39:06 ===
2026-06-23 11:39:06,017 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-23 11:39:06,017 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-23 11:39:06,081 [INFO] predictor: Models loaded OK
2026-06-23 11:39:06,404 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 53
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 53
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 9, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 156
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_TRIP: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 10 | 12,300 | 8,010 | -4,290 | 0.651 |
| S01_NAKAANA1 | 35 | 6 | 7,000 | 2,840 | -4,160 | 0.406 |
| S02_TETSUBAN | 13 | 4 | 2,600 | 1,460 | -1,140 | 0.562 |

## 直近アラート (24h・新しい順)
```
[11:39:06] CALIBRATION_DRIFT: {"avg_actual": 0.2299, "avg_pred": 0.473, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 87, "overconf_pct": 51.4}
[11:34:32] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 2840, "roi_7d": 0.406, "sid": "S01_NAKAANA1"}
[11:34:32] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 8010, "roi_7d": 0.651, "sid": "S00"}
[11:29:38] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 2840, "roi_7d": 0.418, "sid": "S01_NAKAANA1"}
[11:28:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.224, "baseline_mean": 0.776, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.73}
[11:05:41] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 8010, "roi_7d": 0.667, "sid": "S00"}
[11:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:00:34] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.9, "baseline_n_days": 7, "baseline_stdev": 1.3, "hour": 11, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.12}
```

## 本日残レース: 117件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 27件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 11:34:23 |
| S00 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 11:34:21 |
| S00 | 082R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=- drift=- | 11:05:32 |
| S00 | 156R | win | 1 | 0.4111 | 7.2 | 2.96 | 300 | scan=9.7 drift=-25.8% | 17:35:23 |
| S00 | 193R | win | 1 | 0.5891 | 12.3 | 7.25 | 300 | scan=4.1 drift=+200.0% | 16:20:35 |
| S00 | 167R | win | 1 | 0.5174 | 12.5 | 6.47 | 300 | scan=6.0 drift=+108.3% | 14:11:25 |
| S01_NAKAANA1 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 200 | scan=- drift=- | 13:30:32 |
| S00 | 055R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 13:30:29 |
| S00 | 1011R | win | 1 | 0.5174 | 7.6 | 3.93 | 300 | scan=6.3 drift=+20.6% | 13:21:22 |
| S00 | 222R | win | 1 | 0.3177 | 26.2 | 8.32 | 300 | scan=4.5 drift=+482.2% | 12:58:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +11.1% | -61.4% | +482.2% | 18 | 7 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 516.8s |
| **Latency** (scan→final max) | 605.7s |
| **Traffic** (notifications 24h) | 53 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 364 | 0.4732 | 0.2802 | +0.1930 | 🟡+41% | 0.2407 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 152 | 0.4253 | 0.2500 | 0.2233 | 🔴-0.19 | 0.674 |
| S01_NAKAANA1 | win | 136 | 0.4897 | 0.2794 | 0.2446 | 🔴-0.21 | 0.743 |
| S02_TETSUBAN | win | 76 | 0.5397 | 0.3421 | 0.2689 | 🔴-0.19 | 0.582 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 7 | 0.1808 | 0.4286 | 🔴-0.2478 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 123 | 0.4224 | 0.2276 | 🔴+0.1947 |
| 0.50+ | 214 | 0.5427 | 0.3224 | 🔴+0.2203 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 88 | 0.737 |
| win | <10.0 | ✅learned | 56 | 0.499 |
| win | <20.0 | ✅learned | 15 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-23T11:40:02.220534+09:00_