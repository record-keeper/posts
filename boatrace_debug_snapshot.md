# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-02T00:00:01.737744+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-01T23:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×51  [2026-06-01T23:09:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×51  [2026-06-01T23:09:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×51  [2026-06-01T23:09:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-06-01T13:34:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-06-01T11:50:00]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×7  [2026-06-01T09:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-01T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.45 (コスト 9,200/回収 4,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S00: n=181 hit%=27.6% hit_CI[Bonf]=[19.2,38.0]% ROI=0.90 ROI_boot95=[0.66,1.17]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=114 hit%=31.6% hit_CI[Bonf]=[20.6,45.0]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=114<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=58 hit%=46.6% hit_CI[Bonf]=[29.3,64.7]% ROI=0.88 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=58<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-01T06:00:22]
- key: `ORPHAN_SCAN|230 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-01T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=30.6% ROI=0.87 (コスト 14,300/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.01MB / last modified 2026-06-01T23:59:05.732815+09:00

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
85 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-01 23:55:06,185 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-01 23:55:06,253 [INFO] predictor: Models loaded OK
2026-06-01 23:55:06,259 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-01 23:56:06,511 [INFO] run_cycle: === run_cycle 23:56:06 ===
2026-06-01 23:56:06,511 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-01 23:56:06,511 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-01 23:56:06,556 [INFO] predictor: Models loaded OK
2026-06-01 23:56:06,560 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-01 23:57:06,232 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-01 23:57:06,232 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-01 23:57:06,232 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-01 23:57:06,296 [INFO] predictor: Models loaded OK
2026-06-01 23:57:06,299 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-01 23:58:06,331 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-01 23:58:06,332 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-01 23:58:06,332 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-01 23:58:06,413 [INFO] predictor: Models loaded OK
2026-06-01 23:58:06,417 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-01 23:59:05,520 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-06-01 23:59:05,520 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-01 23:59:05,521 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-01 23:59:05,588 [INFO] predictor: Models loaded OK
2026-06-01 23:59:05,594 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 50
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 50
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 7, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 63
  ANOMALY_SCRAPER_FAILURE_BURST: 26
  CIRCUIT_BREAKER_TRIP: 21
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 8 | 11,100 | 5,100 | -6,000 | 0.459 |
| S01_NAKAANA1 | 35 | 14 | 7,000 | 6,900 | -100 | 0.986 |
| S02_TETSUBAN | 16 | 7 | 3,200 | 2,700 | -500 | 0.844 |

## 直近アラート (24h・新しい順)
```
[23:56:06] FINAL_MISSING: {"deadline": "2026-06-01T14:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060105061420", "sid": "S00"}
[23:56:06] FINAL_MISSING: {"deadline": "2026-06-01T13:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060105041321", "sid": "S00"}
[23:50:09] FINAL_MISSING: {"deadline": "2026-06-01T13:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060108071315", "sid": "S00"}
[23:47:06] FINAL_MISSING: {"deadline": "2026-06-01T09:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060114020910", "sid": "S00"}
[23:33:05] FINAL_MISSING: {"deadline": "2026-06-01T18:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060119061800", "sid": "S00"}
[23:15:05] FINAL_MISSING: {"deadline": "2026-06-01T13:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060108081342", "sid": "S00"}
[23:09:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:01:06] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 5100, "roi_7d": 0.459, "sid": "S00"}
[22:56:05] FINAL_MISSING: {"deadline": "2026-06-01T13:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060105041321", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 204R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.1 drift=+19.0% | 16:57:21 |
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.5 drift=+4.0% | 14:53:22 |
| S02_TETSUBAN | 136R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 12:57:21 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5735 | 3.4 | 1.95 | 200 | scan=3.4 drift=+0.0% | 12:20:25 |
| S00 | 051R | win | 1 | 0.5735 | 6.6 | 3.78 | 300 | scan=4.0 drift=+65.0% | 11:52:33 |
| S00 | 112R | win | 1 | 0.0923 | 27.7 | 2.56 | 300 | scan=5.2 drift=+432.7% | 11:05:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5174 | 3.9 | 2.02 | 200 | scan=4.1 drift=-4.9% | 09:07:45 |
| S00 | 1510R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.3 drift=+4.7% | 19:30:23 |
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.8 | 1.40 | 200 | scan=- drift=- | 19:24:22 |
| S00 | 076R | win | 1 | 0.5334 | 4.8 | 2.56 | 300 | scan=- drift=- | 18:07:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +17.9% | -81.4% | +432.7% | 13 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 509.8s |
| **Latency** (scan→final max) | 620.5s |
| **Traffic** (notifications 24h) | 50 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 349 | 0.4609 | 0.3238 | +0.1371 | 🟡+30% | 0.2353 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4252 | 0.2849 | 0.2203 | 🔴-0.08 | 0.872 |
| S01_NAKAANA1 | win | 116 | 0.4845 | 0.3103 | 0.2455 | 🔴-0.15 | 0.793 |
| S02_TETSUBAN | win | 61 | 0.5165 | 0.4590 | 0.2585 | 🔴-0.04 | 0.854 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.20-0.30 | 7 | 0.2227 | 0.4286 | 🔴-0.2059 |
| 0.30-0.50 | 148 | 0.4153 | 0.2703 | 🔴+0.1451 |
| 0.50+ | 178 | 0.5399 | 0.3876 | 🔴+0.1522 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 28 | 0.77 |
| win | <5.0 | ✅learned | 55 | 0.757 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 11 | 0.193 |
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
_auto-generated by claude_snapshot.py at 2026-06-02T00:00:01.737744+09:00_