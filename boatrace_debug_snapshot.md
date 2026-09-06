# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-06T21:00:01.361394+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×97 (24h)
- 🔴 CALIBRATION_DRIFT×24 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-06T21:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-09-06T20:25:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-09-06T20:08:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×52  [2026-09-06T20:08:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-09-06T20:08:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×11  [2026-09-06T19:01:44]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-09-06T12:08:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×20  [2026-09-06T11:39:28]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_BET_VOLUME_DROP  ×25  [2026-09-06T10:00:25]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-06T06:00:18]
- key: `ORPHAN_SCAN|202 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-06T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-06T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-06T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-06T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=29.5% ROI=0.92 (コスト 10,200/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-06T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1266 actual=0.0000 gap=+0.1266`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-06T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=14.3% ROI=0.38 (コスト 10,100/回収 3,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-06T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.2000 gap=+0.0255`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-06T06:00:18]
- key: `ROI_STAT|S00: n=187 hit%=26.7% hit_CI[Bonf]=[18.5,36.9]% ROI=0.89 ROI_boot95=[0.63,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-06T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=194 hit%=22.7% hit_CI[Bonf]=[15.2,32.4]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-06T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=194<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.55MB / last modified 2026-09-06T20:59:04.789076+09:00

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
59 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 20:55:03,659 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 20:55:03,705 [INFO] predictor: Models loaded OK
2026-09-06 20:55:03,709 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 20:56:03,923 [INFO] run_cycle: === run_cycle 20:56:03 ===
2026-09-06 20:56:03,923 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 20:56:03,923 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 20:56:03,973 [INFO] predictor: Models loaded OK
2026-09-06 20:56:03,977 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 20:57:04,312 [INFO] run_cycle: === run_cycle 20:57:04 ===
2026-09-06 20:57:04,312 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 20:57:04,312 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 20:57:04,361 [INFO] predictor: Models loaded OK
2026-09-06 20:57:04,365 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 20:58:04,135 [INFO] run_cycle: === run_cycle 20:58:04 ===
2026-09-06 20:58:04,135 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 20:58:04,135 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 20:58:04,168 [INFO] predictor: Models loaded OK
2026-09-06 20:58:04,170 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 20:59:04,186 [INFO] run_cycle: === run_cycle 20:59:04 ===
2026-09-06 20:59:04,187 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 20:59:04,187 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 20:59:04,231 [INFO] predictor: Models loaded OK
2026-09-06 20:59:04,235 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 81
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 81
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 17, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 143
  FINAL_MISSING: 97
  CALIBRATION_DRIFT: 24
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 15 | 14,400 | 15,780 | +1,380 | 1.096 |
| S01_NAKAANA1 | 45 | 6 | 9,000 | 2,780 | -6,220 | 0.309 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,440 | -1,360 | 0.514 |

## 直近アラート (24h・新しい順)
```
[20:59:04] FINAL_MISSING: {"deadline": "2026-09-06T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090604041222", "sid": "S00"}
[20:56:04] FINAL_MISSING: {"deadline": "2026-09-06T11:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090610071119", "sid": "S00"}
[20:56:04] FINAL_MISSING: {"deadline": "2026-09-06T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090604061322", "sid": "S00"}
[20:50:05] FINAL_MISSING: {"deadline": "2026-09-06T14:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090602081416", "sid": "S00"}
[20:48:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 576}
[20:46:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 577}
[20:45:04] FINAL_MISSING: {"deadline": "2026-09-06T13:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090614101309", "sid": "S00"}
[20:45:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 594}
[20:44:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 604}
[20:43:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 600}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 144件 締切済
- 通知発射: scan=31 nid / final=31 nid / result=17 nid
- predictions: 17 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 079R | win | 1 | 0.5719 | 2.0 | 1.14 | 200 | scan=2.1 drift=-4.8% | 19:11:19 |
| S01_NAKAANA1 | 019R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=- drift=- | 18:51:18 |
| S01_NAKAANA1 | 078R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.0 drift=+0.0% | 18:40:20 |
| S02_TETSUBAN | 074R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=- drift=- | 16:49:30 |
| S00 | 014R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=6.0 drift=+86.7% | 16:30:21 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5174 | 2.9 | 1.50 | 200 | scan=- drift=- | 15:08:19 |
| S00 | 119R | win | 1 | 0.5719 | 5.5 | 3.15 | 300 | scan=- drift=- | 14:38:31 |
| S01_NAKAANA1 | 046R | win | 1 | 0.5072 | 3.8 | 1.93 | 200 | scan=3.9 drift=-2.6% | 13:19:42 |
| S02_TETSUBAN | 096R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=2.7 drift=-7.4% | 13:12:26 |
| S01_NAKAANA1 | 035R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=4.5 drift=-33.3% | 12:59:26 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +6.3% | -75.5% | +137.8% | 16 | 9 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 432.0s |
| **Latency** (scan→final max) | 652.2s |
| **Traffic** (notifications 24h) | 81 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 469 | 0.4767 | 0.2793 | +0.1974 | 🟡+41% | 0.2416 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 187 | 0.4306 | 0.2834 | 0.2238 | 🔴-0.10 | 0.952 |
| S01_NAKAANA1 | win | 193 | 0.4889 | 0.2280 | 0.2480 | 🔴-0.41 | 0.683 |
| S02_TETSUBAN | win | 89 | 0.5470 | 0.3820 | 0.2653 | 🔴-0.12 | 0.638 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1302 | 0.0000 | 🔴+0.1302 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 9 | 0.2264 | 0.2222 | ✅+0.0042 |
| 0.30-0.50 | 159 | 0.4059 | 0.2327 | 🔴+0.1732 |
| 0.50+ | 283 | 0.5453 | 0.3145 | 🔴+0.2308 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 131 | 0.772 |
| win | <5.0 | ✅learned | 237 | 0.738 |
| win | <10.0 | ✅learned | 117 | 0.47 |
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
_auto-generated by claude_snapshot.py at 2026-09-06T21:00:01.361394+09:00_