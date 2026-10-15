# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-16T05:50:02.039330+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×1 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-16T05:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×24  [2026-10-15T23:36:14]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×50  [2026-10-15T23:10:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×24  [2026-10-15T18:36:29]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-10-15T16:24:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×31  [2026-10-15T13:31:52]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×24  [2026-10-15T11:03:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-15T06:00:14]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=87<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=40.6% ROI=1.12 (コスト 9,300/回収 10,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.50+: n=256 pred=0.5435 actual=0.3711 gap=+0.1724`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S00: n=181 hit%=26.5% hit_CI[Bonf]=[18.2,36.9]% ROI=0.72 ROI_boot95=[0.52,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=35.2% hit_CI[Bonf]=[25.3,46.5]% ROI=1.04 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=87 hit%=50.6% hit_CI[Bonf]=[35.7,65.3]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=32.0% ROI=0.73 (コスト 11,900/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=35.6% ROI=0.97 (コスト 20,100/回収 19,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=55 hit%=36.4% ROI=0.90 (コスト 13,000/回収 11,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=23.9% ROI=0.79 (コスト 11,900/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.87MB / last modified 2026-10-16T05:30:09.106939+09:00

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
39 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 23:55:05,539 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 23:55:05,626 [INFO] predictor: Models loaded OK
2026-10-15 23:55:05,630 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 23:56:04,652 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-15 23:56:04,652 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 23:56:04,652 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 23:56:04,706 [INFO] predictor: Models loaded OK
2026-10-15 23:56:04,708 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 23:57:04,525 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-15 23:57:04,526 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 23:57:04,526 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 23:57:04,601 [INFO] predictor: Models loaded OK
2026-10-15 23:57:04,607 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 23:58:04,520 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-15 23:58:04,521 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 23:58:04,521 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 23:58:04,579 [INFO] predictor: Models loaded OK
2026-10-15 23:58:04,581 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 23:59:04,883 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-15 23:59:04,883 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 23:59:04,883 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 23:59:04,929 [INFO] predictor: Models loaded OK
2026-10-15 23:59:04,931 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 69
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 69
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 19, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 118
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 11
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_SPIKE: 3
  CIRCUIT_BREAKER_TRIP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 11 | 13,500 | 11,220 | -2,280 | 0.831 |
| S01_NAKAANA1 | 41 | 16 | 8,200 | 6,200 | -2,000 | 0.756 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 4,300 | +100 | 1.024 |

## 直近アラート (24h・新しい順)
```
[23:56:04] FINAL_MISSING: {"deadline": "2026-10-15T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101502021116", "sid": "S00"}
[23:47:06] FINAL_MISSING: {"deadline": "2026-10-15T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101524051715", "sid": "S00"}
[23:36:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:55:05] FINAL_MISSING: {"deadline": "2026-10-15T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101502021116", "sid": "S00"}
[22:47:05] FINAL_MISSING: {"deadline": "2026-10-15T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101524051715", "sid": "S00"}
[22:36:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[22:08:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:55:04] FINAL_MISSING: {"deadline": "2026-10-15T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101502021116", "sid": "S00"}
[21:47:04] FINAL_MISSING: {"deadline": "2026-10-15T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101524051715", "sid": "S00"}
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
| S00 | 248R | win | 1 | 0.1156 | 5.4 | 0.62 | 300 | scan=4.8 drift=+12.5% | 18:36:20 |
| S01_NAKAANA1 | 244R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=- drift=- | 16:46:19 |
| S00 | 153R | win | 1 | 0.5735 | 5.2 | 2.98 | 300 | scan=5.2 drift=+0.0% | 16:10:31 |
| S00 | 2211R | win | 1 | 0.2290 | 8.1 | 1.85 | 300 | scan=- drift=- | 16:04:18 |
| S00 | 242R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=4.5 drift=+15.6% | 15:44:20 |
| S01_NAKAANA1 | 029R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.5 drift=-31.1% | 14:43:22 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.2 drift=+18.2% | 14:36:30 |
| S00 | 028R | win | 1 | 0.3599 | 7.8 | 2.81 | 300 | scan=13.5 drift=-42.2% | 14:12:19 |
| S01_NAKAANA1 | 1411R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=3.0 drift=+10.0% | 13:31:19 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.7 drift=-5.4% | 12:55:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 68 | +16.4% | -52.2% | +326.7% | 16 | 7 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 384.5s |
| **Latency** (scan→final max) | 593.5s |
| **Traffic** (notifications 24h) | 69 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4784 | 0.3501 | +0.1283 | 🟡+27% | 0.2482 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4435 | 0.2667 | 0.2458 | 🔴-0.26 | 0.734 |
| S01_NAKAANA1 | win | 170 | 0.4898 | 0.3529 | 0.2450 | 🔴-0.07 | 1.014 |
| S02_TETSUBAN | win | 87 | 0.5283 | 0.5172 | 0.2594 | 🔴-0.04 | 0.925 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1249 | 0.4000 | 🔴-0.2751 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 162 | 0.4173 | 0.3148 | 🔴+0.1025 |
| 0.50+ | 255 | 0.5430 | 0.3765 | 🔴+0.1665 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 183 | 0.772 |
| win | <5.0 | ✅learned | 327 | 0.75 |
| win | <10.0 | ✅learned | 142 | 0.463 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-16T05:50:02.039330+09:00_