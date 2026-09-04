# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-04T17:40:02.104370+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×64 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×15 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-09-04T17:07:26]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-09-04T17:07:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×32  [2026-09-04T17:07:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×36  [2026-09-04T17:03:19]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-04T17:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×29  [2026-09-04T15:53:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×33  [2026-09-04T15:05:23]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-09-04T11:32:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-09-04T06:00:14]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-04T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=188<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.90 (コスト 10,100/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-04T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=19.5% ROI=0.87 (コスト 11,200/回収 9,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-04T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=115 pred=0.4375 actual=0.2261 gap=+0.2114`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S00: n=183 hit%=27.9% hit_CI[Bonf]=[19.4,38.2]% ROI=0.95 ROI_boot95=[0.69,1.23]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=188 hit%=23.9% hit_CI[Bonf]=[16.2,33.9]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-04T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=39.5% hit_CI[Bonf]=[25.5,55.4]% ROI=0.67 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.32MB / last modified 2026-09-04T17:39:19.096273+09:00

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
sed
2026-09-04 17:38:18,310 [INFO] scraper: fetch_race 24/1: boats=6 odds=191/191
2026-09-04 17:38:18,314 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 17:38:18,315 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-04 17:38:18,319 [INFO] run_cycle: fetched 24/1 [final]: 156 combos
2026-09-04 17:38:21,992 [INFO] scraper: odds3t: 120/120 parsed
2026-09-04 17:38:23,087 [INFO] scraper: odds3f: 20/20 parsed
2026-09-04 17:38:24,185 [INFO] scraper: odds2t: 30/30 parsed
2026-09-04 17:38:24,186 [INFO] scraper: odds2f: 15/15 parsed
2026-09-04 17:38:25,270 [INFO] scraper: odds_win: 6/6 parsed
2026-09-04 17:38:25,270 [INFO] scraper: fetch_race 20/6: boats=6 odds=191/191
2026-09-04 17:38:25,272 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 17:38:25,273 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-04 17:38:25,276 [INFO] run_cycle: fetched 20/6 [scan]: 156 combos
2026-09-04 17:38:25,412 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-04 17:39:02,715 [INFO] run_cycle: === run_cycle 17:39:02 ===
2026-09-04 17:39:02,715 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-04 17:39:02,715 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-04 17:39:02,762 [INFO] predictor: Models loaded OK
2026-09-04 17:39:15,162 [INFO] scraper: odds3t: 120/120 parsed
2026-09-04 17:39:16,230 [INFO] scraper: odds3f: 20/20 parsed
2026-09-04 17:39:17,306 [INFO] scraper: odds2t: 30/30 parsed
2026-09-04 17:39:17,307 [INFO] scraper: odds2f: 15/15 parsed
2026-09-04 17:39:18,408 [INFO] scraper: odds_win: 6/6 parsed
2026-09-04 17:39:18,408 [INFO] scraper: fetch_race 24/1: boats=6 odds=191/191
2026-09-04 17:39:18,411 [INFO] predictor: CALIBRATION_MODE=on
2026-09-04 17:39:18,411 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-04 17:39:18,415 [INFO] run_cycle: fetched 24/1 [final]: 156 combos
2026-09-04 17:39:18,643 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 25, 'result': 12, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 81
  FINAL_MISSING: 64
  PSI_DRIFT_DETECTED: 38
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 15
  ANOMALY_SCAN_FINAL_RATIO: 12
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 13 | 14,400 | 13,020 | -1,380 | 0.904 |
| S01_NAKAANA1 | 35 | 3 | 7,000 | 1,560 | -5,440 | 0.223 |
| S02_TETSUBAN | 12 | 4 | 2,400 | 1,800 | -600 | 0.75 |

## 直近アラート (24h・新しい順)
```
[17:39:18] FINAL_MISSING: {"deadline": "2026-09-04T17:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090407051709", "sid": "S00"}
[17:38:25] CALIBRATION_DRIFT: {"avg_actual": 0.2128, "avg_pred": 0.4702, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 94, "overconf_pct": 54.7}
[17:07:25] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:07:25] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 1560, "roi_7d": 0.223, "sid": "S01_NAKAANA1"}
[17:07:25] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:53:03] FINAL_MISSING: {"deadline": "2026-09-04T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090406051322", "sid": "S00"}
[16:49:29] FINAL_MISSING: {"deadline": "2026-09-04T15:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090417091519", "sid": "S00"}
[16:45:20] FINAL_MISSING: {"deadline": "2026-09-04T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090417031211", "sid": "S00"}
[16:41:18] FINAL_MISSING: {"deadline": "2026-09-04T15:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090411101510", "sid": "S00"}
[16:37:31] CALIBRATION_DRIFT: {"avg_actual": 0.2128, "avg_pred": 0.4702, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 94, "overconf_pct": 54.7}
```

## 本日残レース: 31件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 125件 締切済
- 通知発射: scan=20 nid / final=19 nid / result=11 nid
- predictions: 13 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 205R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=- drift=- | 17:14:42 |
| S01_NAKAANA1 | 123R | win | 1 | 0.3177 | 4.1 | 1.30 | 200 | scan=- drift=- | 16:06:29 |
| S00 | 072R | win | 1 | 0.5891 | 10.5 | 6.19 | 300 | scan=5.2 drift=+101.9% | 15:47:19 |
| S00 | 122R | win | 1 | 0.2290 | 8.2 | 1.88 | 300 | scan=5.2 drift=+57.7% | 15:38:29 |
| S01_NAKAANA1 | 176R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=- drift=- | 13:41:18 |
| S00 | 176R | win | 1 | 0.5174 | 6.3 | 3.26 | 300 | scan=6.0 drift=+5.0% | 13:40:21 |
| S00 | 026R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=6.6 drift=-1.5% | 13:11:31 |
| S01_NAKAANA1 | 025R | win | 1 | 0.5588 | 3.8 | 2.12 | 200 | scan=3.3 drift=+15.2% | 12:41:30 |
| S00 | 024R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=12.0 drift=-44.2% | 12:11:25 |
| S00 | 108R | win | 1 | 0.5044 | 5.1 | 2.57 | 300 | scan=5.6 drift=-8.9% | 11:49:43 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +12.6% | -73.7% | +158.3% | 11 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 456.3s |
| **Latency** (scan→final max) | 611.1s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4737 | 0.2725 | +0.2012 | 🟡+42% | 0.2402 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4255 | 0.2703 | 0.2199 | 🔴-0.11 | 0.902 |
| S01_NAKAANA1 | win | 190 | 0.4884 | 0.2263 | 0.2494 | 🔴-0.42 | 0.709 |
| S02_TETSUBAN | win | 80 | 0.5502 | 0.3875 | 0.2654 | 🔴-0.12 | 0.667 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 10 | 0.2255 | 0.2000 | ✅+0.0255 |
| 0.30-0.50 | 159 | 0.4071 | 0.2327 | 🔴+0.1744 |
| 0.50+ | 267 | 0.5460 | 0.3071 | 🔴+0.2389 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 232 | 0.741 |
| win | <10.0 | ✅learned | 115 | 0.468 |
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
_auto-generated by claude_snapshot.py at 2026-09-04T17:40:02.104370+09:00_