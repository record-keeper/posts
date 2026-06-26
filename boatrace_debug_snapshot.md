# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-26T12:10:01.824635+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×79 (24h)
- 🔴 CALIBRATION_DRIFT×28 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×8  [2026-06-26T12:02:23]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×10  [2026-06-26T12:02:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×16  [2026-06-26T12:02:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-06-26T12:02:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×12  [2026-06-26T11:54:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-06-26T11:30:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 KS_ODDS_DRIFT  ×49  [2026-06-26T11:01:44]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-26T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-26T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1802 actual=0.3750 gap=-0.1948`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=34 hit%=26.5% ROI=0.84 (コスト 8,200/回収 6,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S00: n=160 hit%=24.4% hit_CI[Bonf]=[16.0,35.3]% ROI=0.64 ROI_boot95=[0.45,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=30.7% hit_CI[Bonf]=[20.7,42.9]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=31.6% hit_CI[Bonf]=[18.7,48.1]% ROI=0.53 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-26T06:00:13]
- key: `ORPHAN_SCAN|152 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=19.4% ROI=0.65 (コスト 8,800/回収 5,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.05MB / last modified 2026-06-26T12:09:47.326607+09:00

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
&hd=20260626: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-26 12:09:29,858 [INFO] scraper: odds3t: 120/120 parsed
2026-06-26 12:09:30,975 [INFO] scraper: odds3f: 19/20 parsed
2026-06-26 12:09:32,078 [INFO] scraper: odds2t: 29/30 parsed
2026-06-26 12:09:32,079 [INFO] scraper: odds2f: 15/15 parsed
2026-06-26 12:09:33,219 [INFO] scraper: odds_win: 6/6 parsed
2026-06-26 12:09:33,219 [INFO] scraper: fetch_race 17/4: boats=6 odds=189/191
2026-06-26 12:09:33,231 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 12:09:33,231 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-06-26 12:09:33,240 [INFO] run_cycle: fetched 17/4 [final]: 155 combos
2026-06-26 12:09:36,912 [INFO] scraper: odds3t: 120/120 parsed
2026-06-26 12:09:38,026 [INFO] scraper: odds3f: 20/20 parsed
2026-06-26 12:09:39,171 [INFO] scraper: odds2t: 28/30 parsed
2026-06-26 12:09:39,172 [INFO] scraper: odds2f: 14/15 parsed
2026-06-26 12:09:40,260 [INFO] scraper: odds_win: 6/6 parsed
2026-06-26 12:09:40,260 [INFO] scraper: fetch_race 21/9: boats=6 odds=188/191
2026-06-26 12:09:40,269 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 12:09:40,271 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-06-26 12:09:40,280 [INFO] run_cycle: fetched 21/9 [scan]: 154 combos
2026-06-26 12:09:43,791 [INFO] scraper: odds3t: 120/120 parsed
2026-06-26 12:09:44,892 [INFO] scraper: odds3f: 20/20 parsed
2026-06-26 12:09:45,981 [INFO] scraper: odds2t: 29/30 parsed
2026-06-26 12:09:45,982 [INFO] scraper: odds2f: 14/15 parsed
2026-06-26 12:09:47,096 [INFO] scraper: odds_win: 2/6 parsed
2026-06-26 12:09:47,096 [INFO] scraper: fetch_race 13/5: boats=6 odds=185/191
2026-06-26 12:09:47,106 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 12:09:47,106 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-06-26 12:09:47,114 [INFO] run_cycle: fetched 13/5 [scan]: 151 combos
2026-06-26 12:09:47,240 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 26, 'result': 12, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 268
  FINAL_MISSING: 79
  CIRCUIT_BREAKER_NO_ACTION: 34
  CALIBRATION_DRIFT: 28
  CIRCUIT_BREAKER_TRIP: 28
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 16
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 8 | 15,300 | 5,490 | -9,810 | 0.359 |
| S01_NAKAANA1 | 38 | 11 | 7,600 | 5,440 | -2,160 | 0.716 |
| S02_TETSUBAN | 10 | 2 | 2,000 | 1,020 | -980 | 0.51 |

## 直近アラート (24h・新しい順)
```
[12:07:33] CALIBRATION_DRIFT: {"avg_actual": 0.2188, "avg_pred": 0.4708, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 53.5}
[12:06:40] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 5490, "roi_7d": 0.359, "sid": "S00"}
[12:06:40] CALIBRATION_DRIFT: {"avg_actual": 0.2211, "avg_pred": 0.4705, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 95, "overconf_pct": 53.0}
[12:05:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1211}
[12:04:35] CALIBRATION_DRIFT: {"avg_actual": 0.2292, "avg_pred": 0.471, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 51.3}
[12:04:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1203}
[12:02:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:02:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:02:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1201}
```

## 本日残レース: 135件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 45件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=1 nid
- predictions: 4 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 041R | win | 1 | 0.5719 | 18.1 | 10.35 | 300 | scan=7.3 drift=+147.9% | 11:53:21 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4998 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:51:22 |
| S00 | 134R | win | 1 | 0.4998 | 15.0 | 7.50 | 300 | scan=10.5 drift=+42.9% | 11:50:23 |
| S01_NAKAANA1 | 173R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:36:24 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=4.4 drift=-15.9% | 18:05:23 |
| S01_NAKAANA1 | 075R | win | 1 | 0.5020 | 3.7 | 1.86 | 200 | scan=- drift=- | 17:40:33 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=- drift=- | 16:02:21 |
| S01_NAKAANA1 | 0311R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 15:50:23 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=- drift=- | 15:11:37 |
| S00 | 225R | win | 1 | 0.4111 | 45.0 | 18.50 | 300 | scan=- drift=- | 14:23:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +19.6% | -49.2% | +482.2% | 21 | 7 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 356.5s |
| **Latency** (scan→final max) | 610.2s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 373 | 0.4777 | 0.2788 | +0.1989 | 🟡+42% | 0.2413 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4363 | 0.2437 | 0.2260 | 🔴-0.23 | 0.643 |
| S01_NAKAANA1 | win | 138 | 0.4912 | 0.3043 | 0.2427 | 🔴-0.15 | 0.797 |
| S02_TETSUBAN | win | 75 | 0.5413 | 0.3067 | 0.2714 | 🔴-0.28 | 0.508 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 123 | 0.4223 | 0.2195 | 🔴+0.2028 |
| 0.50+ | 224 | 0.5430 | 0.3259 | 🔴+0.2171 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 95 | 0.727 |
| win | <10.0 | ✅learned | 57 | 0.496 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-26T12:10:01.824635+09:00_