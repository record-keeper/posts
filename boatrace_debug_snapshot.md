# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-10T17:20:01.840387+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×89 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×8 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-07-10T17:06:46]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×14  [2026-07-10T17:06:46]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-10T17:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×44  [2026-07-10T16:58:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-10T16:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-07-10T15:27:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×18  [2026-07-10T11:03:57]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×54  [2026-07-10T09:00:13]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-10T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-10T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2291 actual=0.0769 gap=+0.1522`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-10T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3230 actual=0.1379 gap=+0.1850`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-10T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-10T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1743 actual=0.5000 gap=-0.3257`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-10T06:00:10]
- key: `ROI_STAT|S00: n=161 hit%=29.2% hit_CI[Bonf]=[20.1,40.4]% ROI=0.76 ROI_boot95=[0.57,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-10T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-10T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=147 hit%=32.0% hit_CI[Bonf]=[22.1,43.8]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-10T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=41.9% hit_CI[Bonf]=[27.0,58.4]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-10T06:00:10]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-10T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=37.1% ROI=1.03 (コスト 10,200/回収 10,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-10T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=25.6% ROI=0.63 (コスト 10,100/回収 6,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.27MB / last modified 2026-07-10T17:19:07.416654+09:00

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
2026-07-10 17:17:31,324 [INFO] scraper: odds2t: 30/30 parsed
2026-07-10 17:17:31,325 [INFO] scraper: odds2f: 15/15 parsed
2026-07-10 17:17:32,411 [INFO] scraper: odds_win: 5/6 parsed
2026-07-10 17:17:32,411 [INFO] scraper: fetch_race 16/11: boats=6 odds=190/191
2026-07-10 17:17:32,424 [INFO] predictor: CALIBRATION_MODE=on
2026-07-10 17:17:32,425 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-10 17:17:32,433 [INFO] run_cycle: fetched 16/11 [final]: 155 combos
2026-07-10 17:17:35,967 [INFO] scraper: odds3t: 120/120 parsed
2026-07-10 17:17:37,135 [INFO] scraper: odds3f: 20/20 parsed
2026-07-10 17:17:38,219 [INFO] scraper: odds2t: 30/30 parsed
2026-07-10 17:17:38,220 [INFO] scraper: odds2f: 15/15 parsed
2026-07-10 17:17:39,383 [INFO] scraper: odds_win: 3/6 parsed
2026-07-10 17:17:39,383 [INFO] scraper: fetch_race 15/5: boats=6 odds=188/191
2026-07-10 17:17:39,392 [INFO] predictor: CALIBRATION_MODE=on
2026-07-10 17:17:39,392 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-07-10 17:17:39,402 [INFO] run_cycle: fetched 15/5 [scan]: 153 combos
2026-07-10 17:17:39,511 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-10 17:18:05,606 [INFO] run_cycle: === run_cycle 17:18:05 ===
2026-07-10 17:18:05,606 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-10 17:18:05,606 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-10 17:18:05,649 [INFO] predictor: Models loaded OK
2026-07-10 17:18:05,823 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-10 17:19:05,976 [INFO] run_cycle: === run_cycle 17:19:05 ===
2026-07-10 17:19:05,976 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-10 17:19:05,977 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-10 17:19:06,051 [INFO] predictor: Models loaded OK
2026-07-10 17:19:06,265 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 13, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 93
  FINAL_MISSING: 89
  CIRCUIT_BREAKER_NO_ACTION: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  CIRCUIT_BREAKER_TRIP: 8
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 11 | 10,500 | 6,750 | -3,750 | 0.643 |
| S01_NAKAANA1 | 40 | 10 | 8,000 | 5,500 | -2,500 | 0.688 |
| S02_TETSUBAN | 22 | 13 | 4,400 | 4,800 | +400 | 1.091 |

## 直近アラート (24h・新しい順)
```
[17:06:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:06:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[17:04:28] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 6750, "roi_7d": 0.643, "sid": "S00"}
[16:58:30] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5500, "roi_7d": 0.688, "sid": "S01_NAKAANA1"}
[16:58:30] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 7500, "roi_7d": 0.694, "sid": "S00"}
[16:57:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:50:09] FINAL_MISSING: {"deadline": "2026-07-10T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071010051016", "sid": "S00"}
[16:47:06] FINAL_MISSING: {"deadline": "2026-07-10T09:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071014020912", "sid": "S00"}
[16:44:05] FINAL_MISSING: {"deadline": "2026-07-10T11:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071011021110", "sid": "S00"}
[16:33:33] FINAL_MISSING: {"deadline": "2026-07-10T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071010020858", "sid": "S00"}
```

## 本日残レース: 31件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 125件 締切済
- 通知発射: scan=20 nid / final=20 nid / result=10 nid
- predictions: 12 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 154R | win | 1 | 0.1371 | 27.7 | 3.80 | 300 | scan=- drift=- | 16:58:21 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5174 | 2.4 | 1.24 | 200 | scan=- drift=- | 15:14:23 |
| S00 | 028R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=- drift=- | 14:02:20 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.1 drift=+35.5% | 13:17:34 |
| S00 | 1011R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=8.2 drift=-48.8% | 13:17:33 |
| S00 | 096R | win | 1 | 0.5334 | 33.0 | 17.60 | 300 | scan=19.5 drift=+69.2% | 13:04:21 |
| S00 | 163R | win | 1 | 0.5174 | 5.4 | 2.79 | 300 | scan=6.2 drift=-12.9% | 12:54:20 |
| S01_NAKAANA1 | 2310R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=- drift=- | 12:49:20 |
| S00 | 1010R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=6.7 drift=-35.8% | 12:43:20 |
| S00 | 237R | win | 1 | 0.5123 | 18.0 | 9.22 | 300 | scan=5.2 drift=+246.2% | 11:17:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +5.6% | -73.3% | +246.2% | 17 | 7 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 419.1s |
| **Latency** (scan→final max) | 605.0s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 386 | 0.4779 | 0.3290 | +0.1488 | 🟡+31% | 0.2363 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4451 | 0.2970 | 0.2243 | 🔴-0.07 | 0.764 |
| S01_NAKAANA1 | win | 148 | 0.4823 | 0.3108 | 0.2387 | 🔴-0.11 | 0.868 |
| S02_TETSUBAN | win | 73 | 0.5429 | 0.4384 | 0.2588 | 🔴-0.05 | 0.778 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1743 | 0.5000 | 🔴-0.3257 |
| 0.20-0.30 | 13 | 0.2291 | 0.0769 | 🔴+0.1522 |
| 0.30-0.50 | 139 | 0.4172 | 0.2950 | 🔴+0.1222 |
| 0.50+ | 225 | 0.5430 | 0.3644 | 🔴+0.1786 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 67 | 0.759 |
| win | <5.0 | ✅learned | 126 | 0.716 |
| win | <10.0 | ✅learned | 69 | 0.469 |
| win | <20.0 | ✅learned | 19 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-10T17:20:01.840387+09:00_