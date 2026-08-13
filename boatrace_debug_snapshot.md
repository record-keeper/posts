# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-14T05:30:01.700583+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×143 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×47 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-14T04:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-14T04:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×104  [2026-08-13T23:08:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×104  [2026-08-13T23:08:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-08-13T23:08:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-08-13T20:43:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-08-13T16:06:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-08-13T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-13T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S00: n=165 hit%=21.8% hit_CI[Bonf]=[14.0,32.3]% ROI=0.62 ROI_boot95=[0.41,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=21.7% hit_CI[Bonf]=[13.9,32.2]% ROI=0.67 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=55.1% hit_CI[Bonf]=[38.2,70.9]% ROI=0.92 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-13T06:00:10]
- key: `ORPHAN_SCAN|178 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.62 (コスト 10,900/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=31.4% ROI=0.79 (コスト 8,600/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=67 hit%=26.9% ROI=0.58 (コスト 15,600/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=46 hit%=26.1% ROI=0.53 (コスト 10,600/回収 5,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.36MB / last modified 2026-08-14T05:30:03.315624+09:00

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
68 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-13 23:55:03,968 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-13 23:55:04,017 [INFO] predictor: Models loaded OK
2026-08-13 23:55:04,020 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-13 23:56:04,447 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-08-13 23:56:04,447 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-13 23:56:04,447 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-13 23:56:04,491 [INFO] predictor: Models loaded OK
2026-08-13 23:56:04,494 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-13 23:57:03,478 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-08-13 23:57:03,479 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-13 23:57:03,479 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-13 23:57:03,526 [INFO] predictor: Models loaded OK
2026-08-13 23:57:03,530 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-13 23:58:03,789 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-08-13 23:58:03,790 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-13 23:58:03,790 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-13 23:58:03,837 [INFO] predictor: Models loaded OK
2026-08-13 23:58:03,841 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-13 23:59:04,050 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-08-13 23:59:04,050 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-13 23:59:04,050 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-13 23:59:04,099 [INFO] predictor: Models loaded OK
2026-08-13 23:59:04,103 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 92
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 92
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 20, 'scan': 37}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 181
  FINAL_MISSING: 143
  CIRCUIT_BREAKER_TRIP: 47
  ANOMALY_SCAN_FINAL_RATIO: 38
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 8 | 13,200 | 6,390 | -6,810 | 0.484 |
| S01_NAKAANA1 | 49 | 8 | 9,800 | 4,940 | -4,860 | 0.504 |
| S02_TETSUBAN | 23 | 12 | 4,600 | 3,620 | -980 | 0.787 |

## 直近アラート (24h・新しい順)
```
[23:56:04] CIRCUIT_BREAKER_TRIP: {"cost": 9800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 49, "payout": 4940, "roi_7d": 0.504, "sid": "S01_NAKAANA1"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-08-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081302021116", "sid": "S00"}
[23:45:04] FINAL_MISSING: {"deadline": "2026-08-13T17:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081307051711", "sid": "S00"}
[23:43:04] FINAL_MISSING: {"deadline": "2026-08-13T14:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081306061408", "sid": "S00"}
[23:42:04] FINAL_MISSING: {"deadline": "2026-08-13T16:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081301031607", "sid": "S00"}
[23:41:03] FINAL_MISSING: {"deadline": "2026-08-13T10:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081323041002", "sid": "S00"}
[23:41:03] FINAL_MISSING: {"deadline": "2026-08-13T16:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081304091605", "sid": "S00"}
[23:37:04] FINAL_MISSING: {"deadline": "2026-08-13T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081306021159", "sid": "S00"}
[23:32:04] FINAL_MISSING: {"deadline": "2026-08-13T14:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081304071458", "sid": "S00"}
[23:30:07] FINAL_MISSING: {"deadline": "2026-08-13T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081304051355", "sid": "S00"}
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
| S00 | 194R | win | 1 | 0.5334 | 5.5 | 2.93 | 300 | scan=4.2 drift=+31.0% | 19:00:22 |
| S00 | 019R | win | 1 | 0.1543 | 19.0 | 2.93 | 300 | scan=- drift=- | 18:49:30 |
| S02_TETSUBAN | 075R | win | 1 | 0.4111 | 2.2 | 0.90 | 200 | scan=- drift=- | 17:08:18 |
| S00 | 125R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 17:03:29 |
| S00 | 015R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=11.6 drift=-62.9% | 16:58:31 |
| S02_TETSUBAN | 074R | win | 1 | 0.5476 | 2.1 | 1.15 | 200 | scan=- drift=- | 16:41:31 |
| S00 | 073R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=- drift=- | 16:16:19 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=3.0 drift=+3.3% | 16:02:18 |
| S00 | 072R | win | 1 | 0.2173 | 5.2 | 1.13 | 300 | scan=- drift=- | 15:47:31 |
| S00 | 012R | win | 1 | 0.0722 | 7.0 | 0.51 | 300 | scan=6.7 drift=+4.5% | 15:39:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 70 | +7.7% | -62.9% | +287.7% | 20 | 8 | 46 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 495.0s |
| **Latency** (scan→final max) | 624.9s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 412 | 0.4671 | 0.2670 | +0.2001 | 🟡+43% | 0.2363 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 172 | 0.4180 | 0.2151 | 0.2237 | 🔴-0.32 | 0.598 |
| S01_NAKAANA1 | win | 169 | 0.4917 | 0.2071 | 0.2475 | 🔴-0.51 | 0.609 |
| S02_TETSUBAN | win | 71 | 0.5276 | 0.5352 | 0.2401 | ✅+0.03 | 0.897 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1201 | 0.2000 | 🔴-0.0799 |
| 0.15-0.20 | 11 | 0.1834 | 0.0909 | 🔴+0.0924 |
| 0.20-0.30 | 9 | 0.2228 | 0.3333 | 🔴-0.1106 |
| 0.30-0.50 | 157 | 0.4198 | 0.2166 | 🔴+0.2032 |
| 0.50+ | 223 | 0.5433 | 0.3139 | 🔴+0.2294 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 108 | 0.771 |
| win | <5.0 | ✅learned | 182 | 0.724 |
| win | <10.0 | ✅learned | 92 | 0.449 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-14T05:30:01.700583+09:00_