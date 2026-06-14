# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-14T11:20:01.908455+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-06-14T11:13:44]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-06-14T11:02:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-06-14T11:02:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-06-14T11:02:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-14T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×40  [2026-06-14T10:01:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-14T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-14T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-14T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=5 pred=0.1231 actual=0.2000 gap=-0.0769`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-14T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2244 actual=0.2857 gap=-0.0613`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-14T06:00:19]
- key: `ROI_STAT|S00: n=141 hit%=28.4% hit_CI[Bonf]=[18.9,40.3]% ROI=0.86 ROI_boot95=[0.60,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-14T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-14T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=130 hit%=27.7% hit_CI[Bonf]=[18.0,40.1]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-14T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=130<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-14T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=35.0% hit_CI[Bonf]=[21.7,51.1]% ROI=0.57 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-14T06:00:19]
- key: `ORPHAN_SCAN|137 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-14T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=31.2% ROI=0.89 (コスト 9,300/回収 8,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-14T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=15.6% ROI=0.27 (コスト 7,100/回収 1,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-14T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=63 hit%=30.2% ROI=0.62 (コスト 14,700/回収 9,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-14T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=17.1% ROI=0.84 (コスト 8,000/回収 6,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.05MB / last modified 2026-06-14T11:19:18.182217+09:00

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
17:22,515 [INFO] scraper: odds_win: 6/6 parsed
2026-06-14 11:17:22,516 [INFO] scraper: fetch_race 16/2: boats=6 odds=191/191
2026-06-14 11:17:22,527 [INFO] predictor: CALIBRATION_MODE=on
2026-06-14 11:17:22,527 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-14 11:17:22,535 [INFO] run_cycle: fetched 16/2 [final]: 156 combos
2026-06-14 11:17:26,274 [INFO] scraper: odds3t: 120/120 parsed
2026-06-14 11:17:27,400 [INFO] scraper: odds3f: 20/20 parsed
2026-06-14 11:17:28,554 [INFO] scraper: odds2t: 30/30 parsed
2026-06-14 11:17:28,555 [INFO] scraper: odds2f: 15/15 parsed
2026-06-14 11:17:29,700 [INFO] scraper: odds_win: 3/6 parsed
2026-06-14 11:17:29,702 [INFO] scraper: fetch_race 23/7: boats=6 odds=188/191
2026-06-14 11:17:29,717 [INFO] predictor: CALIBRATION_MODE=on
2026-06-14 11:17:29,717 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-14 11:17:29,729 [INFO] run_cycle: fetched 23/7 [scan]: 153 combos
2026-06-14 11:17:29,873 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 11:18:06,655 [INFO] run_cycle: === run_cycle 11:18:06 ===
2026-06-14 11:18:06,656 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 11:18:06,656 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 11:18:06,704 [INFO] predictor: Models loaded OK
2026-06-14 11:18:07,054 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-14 11:19:07,312 [INFO] run_cycle: === run_cycle 11:19:07 ===
2026-06-14 11:19:07,312 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-14 11:19:07,312 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-14 11:19:07,382 [INFO] predictor: Models loaded OK
2026-06-14 11:19:18,074 [WARNING] scraper: beforeinfo parse failed: jcd=06 rno=1
2026-06-14 11:19:18,074 [WARNING] run_cycle: fetch None: 06/1
2026-06-14 11:19:18,074 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 10, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 108
  FINAL_MISSING: 63
  CIRCUIT_BREAKER_NO_ACTION: 29
  CIRCUIT_BREAKER_TRIP: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 16
  ANOMALY_BET_VOLUME_DROP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 15 | 10,800 | 14,250 | +3,450 | 1.319 |
| S01_NAKAANA1 | 30 | 13 | 6,000 | 7,600 | +1,600 | 1.267 |
| S02_TETSUBAN | 26 | 8 | 5,200 | 2,480 | -2,720 | 0.477 |

## 直近アラート (24h・新しい順)
```
[11:13:44] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.156, "baseline_mean": 0.823, "baseline_stdev": 0.077, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.03}
[11:02:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[10:23:27] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 2480, "roi_7d": 0.477, "sid": "S02_TETSUBAN"}
[10:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[10:00:24] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.2, "baseline_n_days": 5, "baseline_stdev": 1.1, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.01}
[09:22:23] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 2480, "roi_7d": 0.477, "sid": "S02_TETSUBAN"}
[09:01:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:06] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 2720, "roi_7d": 0.504, "sid": "S02_TETSUBAN"}
```

## 本日残レース: 124件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 20件 締切済
- 通知発射: scan=3 nid / final=2 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 106R | win | 1 | 0.4989 | 4.0 | 2.00 | 200 | scan=4.4 drift=-9.1% | 10:41:26 |
| S00 | 106R | win | 1 | 0.4989 | 4.0 | 2.00 | 300 | scan=4.4 drift=-9.1% | 10:41:21 |
| S00 | 069R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=- drift=- | 15:31:21 |
| S02_TETSUBAN | 168R | win | 1 | 0.5053 | 2.5 | 1.26 | 200 | scan=2.1 drift=+19.0% | 14:20:27 |
| S00 | 037R | win | 1 | 0.3177 | 8.3 | 2.64 | 300 | scan=8.0 drift=+3.8% | 13:53:47 |
| S01_NAKAANA1 | 148R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.5 drift=-31.1% | 12:08:26 |
| S01_NAKAANA1 | 033R | win | 1 | 0.4920 | 3.7 | 1.82 | 200 | scan=- drift=- | 12:05:26 |
| S02_TETSUBAN | 134R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=- drift=- | 11:54:45 |
| S00 | 163R | win | 1 | 0.5719 | 6.2 | 3.55 | 300 | scan=8.4 drift=-26.2% | 11:47:32 |
| S00 | 113R | win | 1 | 0.5358 | 9.0 | 4.82 | 300 | scan=- drift=- | 11:21:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +4.7% | -82.9% | +162.5% | 13 | 5 | 25 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 530.8s |
| **Latency** (scan→final max) | 676.7s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 352 | 0.4680 | 0.3011 | +0.1669 | 🟡+36% | 0.2385 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 141 | 0.4175 | 0.2908 | 0.2178 | 🔴-0.06 | 0.891 |
| S01_NAKAANA1 | win | 131 | 0.4844 | 0.2824 | 0.2456 | 🔴-0.21 | 0.8 |
| S02_TETSUBAN | win | 80 | 0.5301 | 0.3500 | 0.2634 | 🔴-0.16 | 0.569 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1231 | 0.2000 | 🔴-0.0769 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 7 | 0.2244 | 0.2857 | 🔴-0.0613 |
| 0.30-0.50 | 128 | 0.4182 | 0.2422 | 🔴+0.1760 |
| 0.50+ | 199 | 0.5409 | 0.3568 | 🔴+0.1841 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 40 | 0.725 |
| win | <5.0 | ✅learned | 75 | 0.746 |
| win | <10.0 | ✅learned | 49 | 0.506 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-14T11:20:01.908455+09:00_