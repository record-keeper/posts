# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-11T17:30:01.771407+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×73 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T17:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-08-11T17:17:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×23  [2026-08-11T17:06:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×46  [2026-08-11T17:06:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×23  [2026-08-11T17:06:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×24  [2026-08-11T11:54:44]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-11T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1835 actual=0.1818 gap=+0.0017`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.67 ROI_boot95=[0.46,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=23.3% hit_CI[Bonf]=[15.2,34.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.82 (コスト 8,600/回収 7,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=25.0% ROI=0.68 (コスト 15,100/回収 10,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=24.0% ROI=0.49 (コスト 11,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.13MB / last modified 2026-08-11T17:30:04.924330+09:00

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

2026-08-11 17:29:18,184 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 17:29:19,253 [INFO] scraper: odds_win: 6/6 parsed
2026-08-11 17:29:19,253 [INFO] scraper: fetch_race 15/6: boats=6 odds=191/191
2026-08-11 17:29:19,256 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 17:29:19,257 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-11 17:29:19,260 [INFO] run_cycle: fetched 15/6 [final]: 156 combos
2026-08-11 17:29:22,792 [INFO] scraper: odds3t: 120/120 parsed
2026-08-11 17:29:23,892 [INFO] scraper: odds3f: 20/20 parsed
2026-08-11 17:29:24,977 [INFO] scraper: odds2t: 29/30 parsed
2026-08-11 17:29:24,978 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 17:29:26,085 [INFO] scraper: odds_win: 5/6 parsed
2026-08-11 17:29:26,086 [INFO] scraper: fetch_race 07/6: boats=6 odds=189/191
2026-08-11 17:29:26,088 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 17:29:26,088 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-08-11 17:29:26,092 [INFO] run_cycle: fetched 07/6 [scan]: 154 combos
2026-08-11 17:29:29,666 [INFO] scraper: odds3t: 120/120 parsed
2026-08-11 17:29:30,784 [INFO] scraper: odds3f: 20/20 parsed
2026-08-11 17:29:31,903 [INFO] scraper: odds2t: 30/30 parsed
2026-08-11 17:29:31,904 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 17:29:32,998 [INFO] scraper: odds_win: 5/6 parsed
2026-08-11 17:29:32,998 [INFO] scraper: fetch_race 04/12: boats=6 odds=190/191
2026-08-11 17:29:33,000 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 17:29:33,000 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-11 17:29:33,005 [INFO] run_cycle: fetched 04/12 [scan]: 155 combos
2026-08-11 17:29:33,622 [INFO] race_id: notif: nid=2026081104121742 sid=S00 phase=scan rank=S
2026-08-11 17:29:34,002 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 17:29:34,759 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 17:29:34,873 [INFO] run_cycle: SCAN S00 平和島12R S
2026-08-11 17:29:34,977 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 88
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 88
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 17, 'scan': 35}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 73
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 24
  ANOMALY_SCRAPER_FAILURE_BURST: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 11
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 9 | 10,800 | 8,700 | -2,100 | 0.806 |
| S01_NAKAANA1 | 48 | 9 | 9,600 | 5,480 | -4,120 | 0.571 |
| S02_TETSUBAN | 15 | 8 | 3,000 | 2,280 | -720 | 0.76 |

## 直近アラート (24h・新しい順)
```
[17:23:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1097}
[17:22:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
[17:21:14] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1066}
[17:20:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1084}
[17:19:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1081}
[17:18:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1073}
[17:17:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1071}
[17:16:33] FINAL_MISSING: {"deadline": "2026-08-11T12:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081113061245", "sid": "S00"}
[17:13:05] FINAL_MISSING: {"deadline": "2026-08-11T16:43:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081107041643", "sid": "S00"}
[17:05:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 40件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 140件 締切済
- 通知発射: scan=31 nid / final=31 nid / result=14 nid
- predictions: 16 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 0512R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.4 drift=+4.2% | 17:22:36 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.2 drift=+15.6% | 16:40:45 |
| S00 | 073R | win | 1 | 0.5174 | 6.1 | 3.16 | 300 | scan=4.0 drift=+52.5% | 16:13:25 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=4.4 drift=-31.8% | 15:50:34 |
| S00 | 068R | win | 1 | 0.6037 | 4.7 | 2.84 | 300 | scan=5.5 drift=-14.5% | 14:58:19 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=4.6 drift=-13.0% | 13:16:21 |
| S00 | 166R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=4.6 drift=-13.0% | 13:16:19 |
| S01_NAKAANA1 | 164R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=4.3 drift=-30.2% | 12:16:19 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=4.8 drift=-35.4% | 12:10:20 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 11:36:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +6.5% | -73.3% | +287.7% | 21 | 9 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 454.4s |
| **Latency** (scan→final max) | 616.7s |
| **Traffic** (notifications 24h) | 88 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 2,000円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 394 | 0.4665 | 0.2690 | +0.1975 | 🟡+42% | 0.2366 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 162 | 0.4196 | 0.2222 | 0.2244 | 🔴-0.30 | 0.627 |
| S01_NAKAANA1 | win | 166 | 0.4862 | 0.2169 | 0.2471 | 🔴-0.45 | 0.674 |
| S02_TETSUBAN | win | 66 | 0.5320 | 0.5152 | 0.2402 | ✅+0.04 | 0.88 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 10 | 0.1843 | 0.1000 | 🔴+0.0843 |
| 0.20-0.30 | 9 | 0.2243 | 0.3333 | 🔴-0.1091 |
| 0.30-0.50 | 150 | 0.4185 | 0.2133 | 🔴+0.2051 |
| 0.50+ | 213 | 0.5434 | 0.3192 | 🔴+0.2241 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 103 | 0.776 |
| win | <5.0 | ✅learned | 180 | 0.726 |
| win | <10.0 | ✅learned | 91 | 0.451 |
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
_auto-generated by claude_snapshot.py at 2026-08-11T17:30:01.771407+09:00_