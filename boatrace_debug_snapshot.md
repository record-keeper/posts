# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-10T22:20:02.225259+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×47 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×47 (24h)
- 🔴 CALIBRATION_DRIFT×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×11  [2026-09-10T22:09:08]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×33  [2026-09-10T22:09:08]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×33  [2026-09-10T22:09:08]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-09-10T22:09:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-10T22:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-10T22:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-10T22:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-09-10T19:55:19]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×34  [2026-09-10T17:26:24]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-09-10T14:04:23]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-09-10T10:37:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-10T06:00:16]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1773 actual=0.2222 gap=-0.0449`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=46 pred=0.3225 actual=0.3043 gap=+0.0182`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S00: n=182 hit%=26.4% hit_CI[Bonf]=[18.1,36.7]% ROI=0.90 ROI_boot95=[0.64,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=23.7% hit_CI[Bonf]=[16.0,33.6]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=35.7% hit_CI[Bonf]=[22.6,51.5]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.86MB / last modified 2026-09-10T22:19:06.448124+09:00

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
70 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 22:15:05,870 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 22:15:05,931 [INFO] predictor: Models loaded OK
2026-09-10 22:15:05,933 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-10 22:16:05,558 [INFO] run_cycle: === run_cycle 22:16:05 ===
2026-09-10 22:16:05,559 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 22:16:05,559 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 22:16:05,652 [INFO] predictor: Models loaded OK
2026-09-10 22:16:05,656 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-10 22:17:05,226 [INFO] run_cycle: === run_cycle 22:17:05 ===
2026-09-10 22:17:05,226 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 22:17:05,226 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 22:17:05,312 [INFO] predictor: Models loaded OK
2026-09-10 22:17:05,316 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-10 22:18:05,400 [INFO] run_cycle: === run_cycle 22:18:05 ===
2026-09-10 22:18:05,400 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 22:18:05,400 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 22:18:05,452 [INFO] predictor: Models loaded OK
2026-09-10 22:18:05,456 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-10 22:19:04,919 [INFO] run_cycle: === run_cycle 22:19:04 ===
2026-09-10 22:19:04,920 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 22:19:04,920 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 22:19:04,953 [INFO] predictor: Models loaded OK
2026-09-10 22:19:04,955 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 91
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 91
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 19, 'scan': 35}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 72
  ANOMALY_SCRAPER_FAILURE_BURST: 59
  CIRCUIT_BREAKER_TRIP: 47
  CIRCUIT_BREAKER_NO_ACTION: 37
  CALIBRATION_DRIFT: 35
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 5,910 | -4,590 | 0.563 |
| S01_NAKAANA1 | 45 | 9 | 9,000 | 5,620 | -3,380 | 0.624 |
| S02_TETSUBAN | 23 | 8 | 4,600 | 2,400 | -2,200 | 0.522 |

## 直近アラート (24h・新しい順)
```
[22:19:05] FINAL_MISSING: {"deadline": "2026-09-10T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091003021141", "sid": "S00"}
[22:15:06] FINAL_MISSING: {"deadline": "2026-09-10T10:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091013011038", "sid": "S00"}
[22:09:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:09:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[21:59:05] FINAL_MISSING: {"deadline": "2026-09-10T11:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091004021124", "sid": "S00"}
[21:56:07] CALIBRATION_DRIFT: {"avg_actual": 0.233, "avg_pred": 0.4761, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 103, "overconf_pct": 51.1}
[21:53:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[21:43:03] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 5910, "roi_7d": 0.563, "sid": "S00"}
[21:39:04] FINAL_MISSING: {"deadline": "2026-09-10T11:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091005011103", "sid": "S00"}
[21:39:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 132件 締切済
- 通知発射: scan=29 nid / final=32 nid / result=19 nid
- predictions: 19 / うち結果DB記録済: 19
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 2010R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=2.2 drift=-4.5% | 19:22:20 |
| S02_TETSUBAN | 0512R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.1 drift=-4.8% | 16:43:19 |
| S00 | 0511R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=- drift=- | 16:08:21 |
| S00 | 202R | win | 1 | 0.4920 | 7.8 | 3.84 | 300 | scan=4.7 drift=+66.0% | 15:41:45 |
| S01_NAKAANA1 | 1610R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:25:20 |
| S02_TETSUBAN | 1310R | win | 1 | 0.4111 | 2.3 | 0.95 | 200 | scan=- drift=- | 15:07:27 |
| S00 | 178R | win | 1 | 0.5891 | 7.0 | 4.12 | 300 | scan=6.2 drift=+12.9% | 14:07:21 |
| S02_TETSUBAN | 036R | win | 1 | 0.5123 | 2.4 | 1.23 | 200 | scan=2.4 drift=+0.0% | 13:26:20 |
| S00 | 045R | win | 1 | 0.4989 | 10.5 | 5.24 | 300 | scan=7.1 drift=+47.9% | 12:49:20 |
| S02_TETSUBAN | 034R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=- drift=- | 12:32:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +6.8% | -75.5% | +137.8% | 19 | 9 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 424.5s |
| **Latency** (scan→final max) | 650.2s |
| **Traffic** (notifications 24h) | 91 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 1,400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4704 | 0.2681 | +0.2023 | 🟡+43% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4240 | 0.2663 | 0.2185 | 🔴-0.12 | 0.894 |
| S01_NAKAANA1 | win | 185 | 0.4827 | 0.2378 | 0.2485 | 🔴-0.37 | 0.747 |
| S02_TETSUBAN | win | 86 | 0.5434 | 0.3372 | 0.2692 | 🔴-0.20 | 0.579 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 9 | 0.1773 | 0.2222 | ✅-0.0449 |
| 0.20-0.30 | 8 | 0.2235 | 0.1250 | 🔴+0.0985 |
| 0.30-0.50 | 166 | 0.4028 | 0.2289 | 🔴+0.1739 |
| 0.50+ | 262 | 0.5447 | 0.3053 | 🔴+0.2394 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 135 | 0.768 |
| win | <5.0 | ✅learned | 242 | 0.748 |
| win | <10.0 | ✅learned | 120 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-10T22:20:02.225259+09:00_