# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-01T14:30:01.690746+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×34 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×27  [2026-09-01T14:03:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-09-01T14:03:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-09-01T14:03:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-01T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-01T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×50  [2026-09-01T13:40:23]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-09-01T11:53:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×59  [2026-09-01T10:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-01T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-01T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-01T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1819 actual=0.1667 gap=+0.0152`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-01T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-01T06:00:15]
- key: `ROI_STAT|S00: n=168 hit%=26.2% hit_CI[Bonf]=[17.7,36.9]% ROI=0.85 ROI_boot95=[0.59,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-01T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=185 hit%=24.3% hit_CI[Bonf]=[16.5,34.4]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-01T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-01T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=42.2% hit_CI[Bonf]=[27.9,57.8]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-01T06:00:15]
- key: `ORPHAN_SCAN|199 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-01T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=13.9% ROI=0.36 (コスト 10,400/回収 3,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-01T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=29.5% ROI=0.92 (コスト 10,200/回収 9,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-01T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=90 hit%=30.0% ROI=0.98 (コスト 20,600/回収 20,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.02MB / last modified 2026-09-01T14:30:04.338534+09:00

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
&hd=20260901: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-01 14:29:28,244 [INFO] scraper: odds3t: 120/120 parsed
2026-09-01 14:29:29,381 [INFO] scraper: odds3f: 20/20 parsed
2026-09-01 14:29:30,512 [INFO] scraper: odds2t: 30/30 parsed
2026-09-01 14:29:30,513 [INFO] scraper: odds2f: 15/15 parsed
2026-09-01 14:29:31,592 [INFO] scraper: odds_win: 6/6 parsed
2026-09-01 14:29:31,592 [INFO] scraper: fetch_race 05/7: boats=6 odds=191/191
2026-09-01 14:29:31,595 [INFO] predictor: CALIBRATION_MODE=on
2026-09-01 14:29:31,596 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-01 14:29:31,599 [INFO] run_cycle: fetched 05/7 [final]: 156 combos
2026-09-01 14:29:35,065 [INFO] scraper: odds3t: 120/120 parsed
2026-09-01 14:29:36,183 [INFO] scraper: odds3f: 20/20 parsed
2026-09-01 14:29:37,296 [INFO] scraper: odds2t: 30/30 parsed
2026-09-01 14:29:37,297 [INFO] scraper: odds2f: 15/15 parsed
2026-09-01 14:29:38,402 [INFO] scraper: odds_win: 5/6 parsed
2026-09-01 14:29:38,402 [INFO] scraper: fetch_race 13/9: boats=6 odds=190/191
2026-09-01 14:29:38,405 [INFO] predictor: CALIBRATION_MODE=on
2026-09-01 14:29:38,405 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-01 14:29:38,409 [INFO] run_cycle: fetched 13/9 [scan]: 155 combos
2026-09-01 14:29:41,915 [INFO] scraper: odds3t: 120/120 parsed
2026-09-01 14:29:43,038 [INFO] scraper: odds3f: 20/20 parsed
2026-09-01 14:29:44,176 [INFO] scraper: odds2t: 30/30 parsed
2026-09-01 14:29:44,177 [INFO] scraper: odds2f: 14/15 parsed
2026-09-01 14:29:45,283 [INFO] scraper: odds_win: 4/6 parsed
2026-09-01 14:29:45,283 [INFO] scraper: fetch_race 08/9: boats=6 odds=188/191
2026-09-01 14:29:45,286 [INFO] predictor: CALIBRATION_MODE=on
2026-09-01 14:29:45,286 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-01 14:29:45,290 [INFO] run_cycle: fetched 08/9 [scan]: 154 combos
2026-09-01 14:29:45,440 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 14, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 75
  CIRCUIT_BREAKER_NO_ACTION: 43
  FINAL_MISSING: 34
  CIRCUIT_BREAKER_TRIP: 26
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 7
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 9 | 13,200 | 9,360 | -3,840 | 0.709 |
| S01_NAKAANA1 | 37 | 6 | 7,400 | 3,100 | -4,300 | 0.419 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,420 | -380 | 0.9 |

## 直近アラート (24h・新しい順)
```
[14:23:30] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 3100, "roi_7d": 0.419, "sid": "S01_NAKAANA1"}
[14:21:19] CALIBRATION_DRIFT: {"avg_actual": 0.2371, "avg_pred": 0.4763, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 50.2}
[14:16:38] CALIBRATION_DRIFT: {"avg_actual": 0.2347, "avg_pred": 0.4766, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 98, "overconf_pct": 50.8}
[14:08:19] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 3100, "roi_7d": 0.408, "sid": "S01_NAKAANA1"}
[14:03:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:43:23] CALIBRATION_DRIFT: {"avg_actual": 0.2396, "avg_pred": 0.4799, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 50.1}
[13:43:23] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 10.5, "final": 4.2, "kind": "LARGE_ODDS_DRIFT", "race": "066R", "scan": 3.8, "sid": "S01_NAKAANA1"}
[13:40:23] CALIBRATION_DRIFT: {"avg_actual": 0.2371, "avg_pred": 0.4803, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 50.6}
```

## 本日残レース: 84件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 60件 締切済
- 通知発射: scan=11 nid / final=16 nid / result=7 nid
- predictions: 12 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 067R | win | 1 | 0.5891 | 5.6 | 3.30 | 300 | scan=- drift=- | 14:13:20 |
| S00 | 088R | win | 1 | 0.4111 | 6.1 | 2.51 | 300 | scan=23.2 drift=-73.7% | 14:05:19 |
| S00 | 056R | win | 1 | 0.5174 | 6.7 | 3.47 | 300 | scan=11.7 drift=-42.7% | 13:59:31 |
| S01_NAKAANA1 | 066R | win | 1 | 0.3177 | 4.2 | 1.33 | 200 | scan=3.8 drift=+10.5% | 13:43:22 |
| S00 | 066R | win | 1 | 0.3177 | 4.2 | 1.33 | 300 | scan=4.0 drift=+5.0% | 13:43:20 |
| S01_NAKAANA1 | 165R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=4.1 drift=-2.4% | 13:07:21 |
| S00 | 165R | win | 1 | 0.5891 | 4.0 | 2.36 | 300 | scan=4.1 drift=-2.4% | 13:07:19 |
| S01_NAKAANA1 | 135R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 12:22:18 |
| S01_NAKAANA1 | 063R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 12:15:19 |
| S00 | 188R | win | 1 | 0.4989 | 8.6 | 4.29 | 300 | scan=4.0 drift=+115.0% | 12:03:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +5.9% | -73.7% | +158.3% | 18 | 8 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 494.7s |
| **Latency** (scan→final max) | 602.5s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 438 | 0.4726 | 0.2763 | +0.1963 | 🟡+42% | 0.2388 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4160 | 0.2560 | 0.2122 | 🔴-0.11 | 0.84 |
| S01_NAKAANA1 | win | 189 | 0.4902 | 0.2381 | 0.2516 | 🔴-0.39 | 0.728 |
| S02_TETSUBAN | win | 81 | 0.5488 | 0.4074 | 0.2640 | 🔴-0.09 | 0.705 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 8 | 0.1250 | 0.0000 | 🔴+0.1250 |
| 0.15-0.20 | 12 | 0.1819 | 0.1667 | ✅+0.0152 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 148 | 0.4068 | 0.2432 | 🔴+0.1635 |
| 0.50+ | 259 | 0.5460 | 0.3127 | 🔴+0.2333 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 227 | 0.745 |
| win | <10.0 | ✅learned | 109 | 0.458 |
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
_auto-generated by claude_snapshot.py at 2026-09-01T14:30:01.690746+09:00_