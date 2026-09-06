# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-06T14:00:02.055686+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×114 (24h)
- 🔴 CALIBRATION_DRIFT×32 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-06T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-09-06T13:46:58]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×57  [2026-09-06T13:02:47]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×57  [2026-09-06T13:02:47]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×57  [2026-09-06T13:02:47]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-09-06T13:02:47]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

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
- DB: 12.52MB / last modified 2026-09-06T14:00:04.868999+09:00

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
per: odds_win: 6/6 parsed
2026-09-06 13:58:32,719 [INFO] scraper: fetch_race 10/12: boats=6 odds=191/191
2026-09-06 13:58:32,722 [INFO] predictor: CALIBRATION_MODE=on
2026-09-06 13:58:32,722 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-06 13:58:32,725 [INFO] run_cycle: fetched 10/12 [scan]: 156 combos
2026-09-06 13:58:32,862 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 13:59:04,689 [INFO] run_cycle: === run_cycle 13:59:04 ===
2026-09-06 13:59:04,690 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 13:59:04,690 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 13:59:04,759 [INFO] predictor: Models loaded OK
2026-09-06 13:59:15,791 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=17&hd=20260906: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-06 13:59:27,191 [INFO] scraper: odds3t: 120/120 parsed
2026-09-06 13:59:28,272 [INFO] scraper: odds3f: 20/20 parsed
2026-09-06 13:59:29,364 [INFO] scraper: odds2t: 30/30 parsed
2026-09-06 13:59:29,366 [INFO] scraper: odds2f: 15/15 parsed
2026-09-06 13:59:30,446 [INFO] scraper: odds_win: 6/6 parsed
2026-09-06 13:59:30,446 [INFO] scraper: fetch_race 17/7: boats=6 odds=191/191
2026-09-06 13:59:30,449 [INFO] predictor: CALIBRATION_MODE=on
2026-09-06 13:59:30,449 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-06 13:59:30,453 [INFO] run_cycle: fetched 17/7 [final]: 156 combos
2026-09-06 13:59:30,793 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-06 14:00:07,252 [INFO] run_cycle: === run_cycle 14:00:07 ===
2026-09-06 14:00:07,252 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-06 14:00:07,252 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-06 14:00:07,341 [INFO] predictor: Models loaded OK

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
{'final': 28, 'result': 16, 'scan': 37}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 117
  FINAL_MISSING: 114
  CALIBRATION_DRIFT: 32
  CIRCUIT_BREAKER_TRIP: 23
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  KS_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 14 | 15,000 | 15,480 | +480 | 1.032 |
| S01_NAKAANA1 | 44 | 5 | 8,800 | 2,340 | -6,460 | 0.266 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 1,580 | -820 | 0.658 |

## 直近アラート (24h・新しい順)
```
[13:59:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1086}
[13:58:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1107}
[13:57:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1091}
[13:55:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1112}
[13:54:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1114}
[13:53:19] FINAL_MISSING: {"deadline": "2026-09-06T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090604041222", "sid": "S00"}
[13:52:05] FINAL_MISSING: {"deadline": "2026-09-06T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090604061322", "sid": "S00"}
[13:52:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1136}
[13:51:50] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1134}
[13:50:45] CALIBRATION_DRIFT: {"avg_actual": 0.2264, "avg_pred": 0.4799, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 106, "overconf_pct": 52.8}
```

## 本日残レース: 76件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 68件 締切済
- 通知発射: scan=18 nid / final=16 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 046R | win | 1 | 0.5072 | 3.8 | 1.93 | 200 | scan=3.9 drift=-2.6% | 13:19:42 |
| S02_TETSUBAN | 096R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=2.7 drift=-7.4% | 13:12:26 |
| S01_NAKAANA1 | 035R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=4.5 drift=-33.3% | 12:59:26 |
| S02_TETSUBAN | 093R | win | 1 | 0.5123 | 2.7 | 1.38 | 200 | scan=2.3 drift=+17.4% | 11:39:26 |
| S00 | 113R | win | 1 | 0.3177 | 7.6 | 2.41 | 300 | scan=- drift=- | 11:33:21 |
| S00 | 022R | win | 1 | 0.5735 | 4.1 | 2.35 | 300 | scan=6.0 drift=-31.7% | 11:13:19 |
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=2.8 drift=-21.4% | 11:09:31 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 10:47:29 |
| S01_NAKAANA1 | 021R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=3.5 drift=+2.9% | 10:44:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5735 | 3.9 | 2.24 | 200 | scan=3.9 drift=+0.0% | 10:25:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +7.0% | -75.5% | +158.3% | 17 | 10 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 449.1s |
| **Latency** (scan→final max) | 652.2s |
| **Traffic** (notifications 24h) | 81 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 471 | 0.4762 | 0.2781 | +0.1980 | 🟡+42% | 0.2417 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4288 | 0.2796 | 0.2233 | 🔴-0.11 | 0.952 |
| S01_NAKAANA1 | win | 198 | 0.4891 | 0.2273 | 0.2494 | 🔴-0.42 | 0.704 |
| S02_TETSUBAN | win | 87 | 0.5480 | 0.3908 | 0.2637 | 🔴-0.11 | 0.672 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1302 | 0.0000 | 🔴+0.1302 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 10 | 0.2255 | 0.2000 | ✅+0.0255 |
| 0.30-0.50 | 161 | 0.4066 | 0.2360 | 🔴+0.1705 |
| 0.50+ | 282 | 0.5458 | 0.3121 | 🔴+0.2337 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 130 | 0.775 |
| win | <5.0 | ✅learned | 236 | 0.738 |
| win | <10.0 | ✅learned | 116 | 0.473 |
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
_auto-generated by claude_snapshot.py at 2026-09-06T14:00:02.055686+09:00_