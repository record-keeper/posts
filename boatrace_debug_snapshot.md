# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-04T06:00:01.566203+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 PSI_DRIFT_DETECTED×45 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-04T06:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×50  [2026-09-03T23:10:08]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-09-03T23:08:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×52  [2026-09-03T23:08:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×52  [2026-09-03T23:08:05]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-09-03T23:08:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-09-03T20:25:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×4  [2026-09-03T14:01:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-03T06:00:42]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S00: n=185 hit%=26.5% hit_CI[Bonf]=[18.3,36.7]% ROI=0.87 ROI_boot95=[0.63,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S01_NAKAANA1: n=191 hit%=24.1% hit_CI[Bonf]=[16.4,34.0]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-03T06:00:42]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=191<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-03T06:00:42]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=40.0% hit_CI[Bonf]=[25.9,56.0]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-03T06:00:42]
- key: `ORPHAN_SCAN|191 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=15.8% ROI=0.48 (コスト 11,000/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-03T06:00:42]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=97 hit%=26.8% ROI=0.89 (コスト 22,200/回収 19,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.24MB / last modified 2026-09-04T05:30:03.639986+09:00

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
65 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 23:55:04,865 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 23:55:04,897 [INFO] predictor: Models loaded OK
2026-09-03 23:55:04,900 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-03 23:56:03,501 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-09-03 23:56:03,501 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 23:56:03,501 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 23:56:03,550 [INFO] predictor: Models loaded OK
2026-09-03 23:56:03,554 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-03 23:57:03,885 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-09-03 23:57:03,885 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 23:57:03,885 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 23:57:03,934 [INFO] predictor: Models loaded OK
2026-09-03 23:57:03,940 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-03 23:58:04,060 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-09-03 23:58:04,060 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 23:58:04,060 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 23:58:04,114 [INFO] predictor: Models loaded OK
2026-09-03 23:58:04,117 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-03 23:59:03,440 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-09-03 23:59:03,440 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-03 23:59:03,440 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-03 23:59:03,493 [INFO] predictor: Models loaded OK
2026-09-03 23:59:03,495 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 7, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 135
  FINAL_MISSING: 78
  PSI_DRIFT_DETECTED: 45
  ANOMALY_SCAN_FINAL_RATIO: 35
  CIRCUIT_BREAKER_TRIP: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 13 | 13,800 | 13,650 | -150 | 0.989 |
| S01_NAKAANA1 | 32 | 3 | 6,400 | 1,560 | -4,840 | 0.244 |
| S02_TETSUBAN | 16 | 7 | 3,200 | 2,660 | -540 | 0.831 |

## 直近アラート (24h・新しい順)
```
[23:57:03] FINAL_MISSING: {"deadline": "2026-09-03T12:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090306031219", "sid": "S00"}
[23:50:05] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 1560, "roi_7d": 0.244, "sid": "S01_NAKAANA1"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-09-03T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090302061314", "sid": "S00"}
[23:45:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 358, "n_recent": 94, "psi": 0.339}
[23:37:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.22, "baseline_mean": 0.87, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.65, "today_scan_count": 20, "z_score": -2.21}
[23:30:10] FINAL_MISSING: {"deadline": "2026-09-03T11:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090317031153", "sid": "S00"}
[23:27:04] FINAL_MISSING: {"deadline": "2026-09-03T17:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090312071755", "sid": "S00"}
[23:23:04] FINAL_MISSING: {"deadline": "2026-09-03T14:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090302091448", "sid": "S00"}
[23:23:04] FINAL_MISSING: {"deadline": "2026-09-03T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090302011047", "sid": "S00"}
[23:18:05] FINAL_MISSING: {"deadline": "2026-09-03T14:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090322061443", "sid": "S00"}
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
| S02_TETSUBAN | 1611R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=- drift=- | 16:42:18 |
| S00 | 028R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.7 drift=-4.3% | 14:13:30 |
| S00 | 225R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 14:05:20 |
| S01_NAKAANA1 | 176R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 13:24:20 |
| S01_NAKAANA1 | 065R | win | 1 | 0.5556 | 3.7 | 2.06 | 200 | scan=3.2 drift=+15.6% | 13:19:19 |
| S00 | 223R | win | 1 | 0.5095 | 6.0 | 3.06 | 300 | scan=5.6 drift=+7.1% | 12:46:18 |
| S00 | 184R | win | 1 | 0.5476 | 5.5 | 3.01 | 300 | scan=5.5 drift=+0.0% | 09:59:20 |
| S00 | 129R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=- drift=- | 18:52:18 |
| S00 | 206R | win | 1 | 0.4111 | 7.8 | 3.21 | 300 | scan=12.7 drift=-38.6% | 17:31:18 |
| S00 | 126R | win | 1 | 0.3177 | 7.4 | 2.35 | 300 | scan=4.1 drift=+80.5% | 17:26:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +11.4% | -73.7% | +158.3% | 12 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 447.4s |
| **Latency** (scan→final max) | 652.4s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 452 | 0.4746 | 0.2832 | +0.1914 | 🟡+40% | 0.2411 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 183 | 0.4241 | 0.2787 | 0.2213 | 🔴-0.10 | 0.95 |
| S01_NAKAANA1 | win | 188 | 0.4911 | 0.2394 | 0.2503 | 🔴-0.37 | 0.74 |
| S02_TETSUBAN | win | 81 | 0.5502 | 0.3951 | 0.2646 | 🔴-0.11 | 0.674 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 157 | 0.4064 | 0.2420 | 🔴+0.1644 |
| 0.50+ | 267 | 0.5465 | 0.3184 | 🔴+0.2281 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 114 | 0.469 |
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
_auto-generated by claude_snapshot.py at 2026-09-04T06:00:01.566203+09:00_