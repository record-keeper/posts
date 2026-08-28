# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-28T21:10:01.550505+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×1  [2026-08-28T21:09:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-28T21:09:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×1  [2026-08-28T21:09:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-28T21:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-28T21:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×19  [2026-08-28T16:22:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-08-28T14:50:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×33  [2026-08-28T10:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1807 actual=0.1818 gap=-0.0012`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-28T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S00: n=174 hit%=27.6% hit_CI[Bonf]=[19.0,38.2]% ROI=0.88 ROI_boot95=[0.63,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=25.8% hit_CI[Bonf]=[17.8,35.8]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-28T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-28T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=39.7% hit_CI[Bonf]=[25.5,56.0]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-28T06:00:10]
- key: `ORPHAN_SCAN|198 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=40 hit%=20.0% ROI=0.62 (コスト 11,600/回収 7,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-28T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=32.6% ROI=0.96 (コスト 10,100/回収 9,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.74MB / last modified 2026-08-28T21:09:06.959710+09:00

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
90 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 21:05:04,390 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 21:05:04,438 [INFO] predictor: Models loaded OK
2026-08-28 21:05:04,444 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 21:06:03,889 [INFO] run_cycle: === run_cycle 21:06:03 ===
2026-08-28 21:06:03,889 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 21:06:03,889 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 21:06:03,921 [INFO] predictor: Models loaded OK
2026-08-28 21:06:03,923 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 21:07:04,225 [INFO] run_cycle: === run_cycle 21:07:04 ===
2026-08-28 21:07:04,225 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 21:07:04,225 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 21:07:04,270 [INFO] predictor: Models loaded OK
2026-08-28 21:07:04,274 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 21:08:03,689 [INFO] run_cycle: === run_cycle 21:08:03 ===
2026-08-28 21:08:03,689 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 21:08:03,689 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 21:08:03,720 [INFO] predictor: Models loaded OK
2026-08-28 21:08:03,722 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-28 21:09:03,782 [INFO] run_cycle: === run_cycle 21:09:03 ===
2026-08-28 21:09:03,782 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-28 21:09:03,782 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-28 21:09:03,829 [INFO] predictor: Models loaded OK
2026-08-28 21:09:03,833 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 12, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 109
  FINAL_MISSING: 61
  CIRCUIT_BREAKER_NO_ACTION: 37
  CIRCUIT_BREAKER_TRIP: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 10,380 | -2,520 | 0.805 |
| S01_NAKAANA1 | 44 | 9 | 8,800 | 4,440 | -4,360 | 0.505 |
| S02_TETSUBAN | 18 | 7 | 3,600 | 2,440 | -1,160 | 0.678 |

## 直近アラート (24h・新しい順)
```
[21:09:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:09:03] FINAL_MISSING: {"deadline": "2026-08-28T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082811031132", "sid": "S02_TETSUBAN"}
[21:09:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[21:09:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[20:55:04] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 4440, "roi_7d": 0.505, "sid": "S01_NAKAANA1"}
[20:55:04] FINAL_MISSING: {"deadline": "2026-08-28T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082814091222", "sid": "S00"}
[20:35:05] FINAL_MISSING: {"deadline": "2026-08-28T14:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082805061402", "sid": "S00"}
[20:34:04] FINAL_MISSING: {"deadline": "2026-08-28T13:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082811081359", "sid": "S00"}
[20:27:28] FINAL_MISSING: {"deadline": "2026-08-28T13:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082809081353", "sid": "S00"}
[20:24:05] FINAL_MISSING: {"deadline": "2026-08-28T11:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082814081151", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 144件 締切済
- 通知発射: scan=22 nid / final=20 nid / result=12 nid
- predictions: 12 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 073R | win | 1 | 0.5432 | 2.8 | 1.52 | 200 | scan=2.1 drift=+33.3% | 16:08:18 |
| S00 | 1111R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=4.8 drift=+56.2% | 15:38:19 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.3 drift=-4.3% | 15:00:21 |
| S02_TETSUBAN | 139R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=- drift=- | 14:44:18 |
| S02_TETSUBAN | 114R | win | 1 | 0.5891 | 2.7 | 1.59 | 200 | scan=2.7 drift=+0.0% | 12:00:32 |
| S00 | 052R | win | 1 | 0.5113 | 5.2 | 2.66 | 300 | scan=4.0 drift=+30.0% | 11:57:18 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5074 | 3.5 | 1.78 | 200 | scan=4.0 drift=-12.5% | 11:46:19 |
| S00 | 093R | win | 1 | 0.5123 | 8.2 | 4.20 | 300 | scan=4.5 drift=+82.2% | 11:21:19 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5164 | 3.0 | 1.55 | 200 | scan=- drift=- | 11:14:21 |
| S02_TETSUBAN | 132R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:56:37 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +4.1% | -79.6% | +320.7% | 21 | 10 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 504.7s |
| **Latency** (scan→final max) | 648.5s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4722 | 0.2860 | +0.1862 | 🟡+39% | 0.2393 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4172 | 0.2690 | 0.2194 | 🔴-0.12 | 0.898 |
| S01_NAKAANA1 | win | 187 | 0.4917 | 0.2513 | 0.2499 | 🔴-0.33 | 0.804 |
| S02_TETSUBAN | win | 79 | 0.5452 | 0.4051 | 0.2573 | 🔴-0.07 | 0.657 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1236 | 0.1111 | ✅+0.0125 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 148 | 0.4127 | 0.2297 | 🔴+0.1830 |
| 0.50+ | 256 | 0.5452 | 0.3320 | 🔴+0.2131 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 123 | 0.771 |
| win | <5.0 | ✅learned | 224 | 0.746 |
| win | <10.0 | ✅learned | 108 | 0.459 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-28T21:10:01.550505+09:00_