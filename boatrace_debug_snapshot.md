# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-11T21:20:01.954425+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×68 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×68 (24h)
- 🟡 FINAL_MISSING×50 (24h)
- 🔴 CALIBRATION_DRIFT×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×20  [2026-06-11T21:10:11]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×30  [2026-06-11T21:10:11]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×10  [2026-06-11T21:10:11]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T20:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T20:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T20:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×18  [2026-06-11T19:10:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×21  [2026-06-11T17:39:24]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CALIBRATION_DRIFT  ×47  [2026-06-11T12:03:42]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-06-11T12:01:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-11T06:00:11]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S00: n=149 hit%=25.5% hit_CI[Bonf]=[16.7,36.9]% ROI=0.76 ROI_boot95=[0.50,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=28.3% hit_CI[Bonf]=[18.7,40.3]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=36.2% hit_CI[Bonf]=[22.7,52.4]% ROI=0.61 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.84MB / last modified 2026-06-11T21:19:06.166639+09:00

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
95 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 21:15:06,996 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 21:15:07,058 [INFO] predictor: Models loaded OK
2026-06-11 21:15:07,062 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 21:16:05,374 [INFO] run_cycle: === run_cycle 21:16:05 ===
2026-06-11 21:16:05,374 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 21:16:05,374 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 21:16:05,437 [INFO] predictor: Models loaded OK
2026-06-11 21:16:05,445 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 21:17:06,251 [INFO] run_cycle: === run_cycle 21:17:06 ===
2026-06-11 21:17:06,251 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 21:17:06,251 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 21:17:06,320 [INFO] predictor: Models loaded OK
2026-06-11 21:17:06,328 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 21:18:06,503 [INFO] run_cycle: === run_cycle 21:18:06 ===
2026-06-11 21:18:06,504 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 21:18:06,504 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 21:18:06,554 [INFO] predictor: Models loaded OK
2026-06-11 21:18:06,558 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 21:19:05,948 [INFO] run_cycle: === run_cycle 21:19:05 ===
2026-06-11 21:19:05,948 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 21:19:05,948 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 21:19:06,018 [INFO] predictor: Models loaded OK
2026-06-11 21:19:06,025 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 94
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 94
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 20, 'scan': 38}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_TRIP: 68
  ANOMALY_SCRAPER_FAILURE_BURST: 64
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 50
  CALIBRATION_DRIFT: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 12
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 13 | 12,600 | 10,320 | -2,280 | 0.819 |
| S01_NAKAANA1 | 30 | 8 | 6,000 | 3,720 | -2,280 | 0.62 |
| S02_TETSUBAN | 26 | 6 | 5,200 | 1,840 | -3,360 | 0.354 |

## 直近アラート (24h・新しい順)
```
[21:13:06] FINAL_MISSING: {"deadline": "2026-06-11T19:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061120101942", "sid": "S00"}
[21:12:06] FINAL_MISSING: {"deadline": "2026-06-11T16:39:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061120031639", "sid": "S00"}
[21:11:05] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1840, "roi_7d": 0.354, "sid": "S02_TETSUBAN"}
[21:10:10] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:10:10] FINAL_MISSING: {"deadline": "2026-06-11T11:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061114071134", "sid": "S00"}
[21:10:10] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[21:10:10] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[21:10:10] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[20:45:07] FINAL_MISSING: {"deadline": "2026-06-11T19:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061120091915", "sid": "S00"}
[20:43:32] FINAL_MISSING: {"deadline": "2026-06-11T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061103031208", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 144件 締切済
- 通知発射: scan=33 nid / final=32 nid / result=19 nid
- predictions: 20 / うち結果DB記録済: 20
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 2010R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=- drift=- | 19:39:22 |
| S00 | 075R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=36.3 drift=-82.9% | 17:39:22 |
| S00 | 073R | win | 1 | 0.5334 | 9.0 | 4.80 | 300 | scan=4.8 drift=+87.5% | 16:38:21 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=2.5 drift=+0.0% | 15:34:34 |
| S00 | 201R | win | 1 | 0.5334 | 5.4 | 2.88 | 300 | scan=5.5 drift=-1.8% | 15:22:24 |
| S02_TETSUBAN | 036R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 13:27:20 |
| S00 | 035R | win | 1 | 0.5891 | 6.0 | 3.53 | 300 | scan=6.0 drift=+0.0% | 12:59:31 |
| S00 | 053R | win | 1 | 0.4111 | 9.4 | 3.86 | 300 | scan=15.8 drift=-40.5% | 12:29:22 |
| S00 | 239R | win | 1 | 0.4920 | 6.0 | 2.95 | 300 | scan=- drift=- | 12:23:32 |
| S02_TETSUBAN | 164R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 12:18:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +6.1% | -82.9% | +274.6% | 19 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 470.9s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 94 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,300円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4696 | 0.2923 | +0.1773 | 🟡+38% | 0.2372 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 150 | 0.4195 | 0.2867 | 0.2163 | 🔴-0.06 | 0.849 |
| S01_NAKAANA1 | win | 134 | 0.4884 | 0.2687 | 0.2443 | 🔴-0.24 | 0.704 |
| S02_TETSUBAN | win | 82 | 0.5305 | 0.3415 | 0.2636 | 🔴-0.17 | 0.567 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 6 | 0.2236 | 0.3333 | 🔴-0.1097 |
| 0.30-0.50 | 136 | 0.4212 | 0.2279 | 🔴+0.1932 |
| 0.50+ | 205 | 0.5421 | 0.3512 | 🔴+0.1909 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 37 | 0.733 |
| win | <5.0 | ✅learned | 69 | 0.717 |
| win | <10.0 | ✅learned | 46 | 0.501 |
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
_auto-generated by claude_snapshot.py at 2026-06-11T21:20:01.954425+09:00_