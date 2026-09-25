# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-25T14:20:01.791998+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×34 (24h)
- 🟡 FINAL_MISSING×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-09-25T14:04:24]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-09-25T14:04:24]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-09-25T14:04:24]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×7  [2026-09-25T13:53:35]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×36  [2026-09-25T13:38:31]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-25T13:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-09-25T11:25:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-25T06:00:23]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=27.6% ROI=0.90 (コスト 8,200/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3237 actual=0.2333 gap=+0.0904`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S00: n=171 hit%=22.2% hit_CI[Bonf]=[14.5,32.6]% ROI=0.71 ROI_boot95=[0.47,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=21.9% hit_CI[Bonf]=[13.9,32.8]% ROI=0.65 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=44.9% hit_CI[Bonf]=[29.9,60.8]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=20.5% ROI=0.58 (コスト 9,100/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.07MB / last modified 2026-09-25T14:19:21.152814+09:00

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
ed
2026-09-25 14:18:31,004 [INFO] scraper: fetch_race 18/12: boats=6 odds=189/191
2026-09-25 14:18:31,007 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 14:18:31,007 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-25 14:18:31,011 [INFO] run_cycle: fetched 18/12 [final]: 154 combos
2026-09-25 14:18:34,611 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 14:18:35,809 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 14:18:36,968 [INFO] scraper: odds2t: 29/30 parsed
2026-09-25 14:18:36,969 [INFO] scraper: odds2f: 15/15 parsed
2026-09-25 14:18:38,071 [INFO] scraper: odds_win: 6/6 parsed
2026-09-25 14:18:38,071 [INFO] scraper: fetch_race 08/9: boats=6 odds=190/191
2026-09-25 14:18:38,074 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 14:18:38,074 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-09-25 14:18:38,078 [INFO] run_cycle: fetched 08/9 [scan]: 155 combos
2026-09-25 14:18:38,437 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-25 14:19:04,532 [INFO] run_cycle: === run_cycle 14:19:04 ===
2026-09-25 14:19:04,532 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-25 14:19:04,532 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-25 14:19:04,569 [INFO] predictor: Models loaded OK
2026-09-25 14:19:17,452 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 14:19:18,569 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 14:19:19,693 [INFO] scraper: odds2t: 29/30 parsed
2026-09-25 14:19:19,694 [INFO] scraper: odds2f: 14/15 parsed
2026-09-25 14:19:20,824 [INFO] scraper: odds_win: 2/6 parsed
2026-09-25 14:19:20,824 [INFO] scraper: fetch_race 11/9: boats=6 odds=185/191
2026-09-25 14:19:20,827 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 14:19:20,827 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-09-25 14:19:20,831 [INFO] run_cycle: fetched 11/9 [scan]: 151 combos
2026-09-25 14:19:20,951 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 89
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 89
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 16, 'scan': 36}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 153
  CIRCUIT_BREAKER_TRIP: 34
  FINAL_MISSING: 23
  CIRCUIT_BREAKER_NO_ACTION: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_SPIKE: 4
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 5 | 10,800 | 3,690 | -7,110 | 0.342 |
| S01_NAKAANA1 | 33 | 8 | 6,600 | 3,980 | -2,620 | 0.603 |
| S02_TETSUBAN | 22 | 11 | 4,400 | 3,760 | -640 | 0.855 |

## 直近アラート (24h・新しい順)
```
[14:17:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:13:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1084}
[14:12:19] FINAL_MISSING: {"deadline": "2026-09-25T09:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092521030940", "sid": "S00"}
[14:12:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1091}
[14:11:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1099}
[14:10:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1098}
[14:09:18] FINAL_MISSING: {"deadline": "2026-09-25T13:39:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092505061339", "sid": "S00"}
[14:09:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1095}
[14:08:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1086}
[14:07:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1078}
```

## 本日残レース: 64件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 80件 締切済
- 通知発射: scan=21 nid / final=21 nid / result=11 nid
- predictions: 14 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 098R | win | 1 | 0.3177 | 18.0 | 5.72 | 300 | scan=12.7 drift=+41.7% | 13:53:20 |
| S00 | 088R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=- drift=- | 13:51:18 |
| S01_NAKAANA1 | 2111R | win | 1 | 0.5719 | 3.5 | 2.00 | 200 | scan=4.4 drift=-20.5% | 13:48:20 |
| S00 | 225R | win | 1 | 0.5334 | 5.0 | 2.67 | 300 | scan=- drift=- | 13:44:19 |
| S01_NAKAANA1 | 137R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.2 drift=-9.5% | 13:21:22 |
| S02_TETSUBAN | 2110R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=2.5 drift=-16.0% | 13:14:31 |
| S00 | 096R | win | 1 | 0.4989 | 15.0 | 7.48 | 300 | scan=- drift=- | 12:53:20 |
| S02_TETSUBAN | 054R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=- drift=- | 12:30:24 |
| S00 | 053R | win | 1 | 0.1485 | 9.7 | 1.44 | 300 | scan=4.8 drift=+102.1% | 12:03:19 |
| S01_NAKAANA1 | 094R | win | 1 | 0.5663 | 3.9 | 2.21 | 200 | scan=3.7 drift=+5.4% | 11:54:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | -0.7% | -81.7% | +102.1% | 17 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 478.9s |
| **Latency** (scan→final max) | 671.0s |
| **Traffic** (notifications 24h) | 89 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 400 | 0.4769 | 0.2675 | +0.2094 | 🟡+44% | 0.2448 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4450 | 0.2216 | 0.2348 | 🔴-0.36 | 0.684 |
| S01_NAKAANA1 | win | 153 | 0.4847 | 0.2222 | 0.2483 | 🔴-0.44 | 0.658 |
| S02_TETSUBAN | win | 80 | 0.5284 | 0.4500 | 0.2591 | 🔴-0.05 | 0.804 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.30-0.50 | 151 | 0.4148 | 0.2384 | 🔴+0.1764 |
| 0.50+ | 231 | 0.5444 | 0.2944 | 🔴+0.2500 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 154 | 0.771 |
| win | <5.0 | ✅learned | 266 | 0.758 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-25T14:20:01.791998+09:00_