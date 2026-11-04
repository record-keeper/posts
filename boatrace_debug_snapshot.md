# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-04T18:10:01.480076+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×66 (24h)
- 🔴 CALIBRATION_DRIFT×29 (24h)
- 🔴 PSI_DRIFT_DETECTED×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×15  [2026-11-04T17:34:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T17:30:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-04T17:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-04T17:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×27  [2026-11-04T17:18:12]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-11-04T17:18:12]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×27  [2026-11-04T17:18:12]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-11-04T17:18:12]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T17:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T15:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-04T14:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T14:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 13 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-04T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=62<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-04T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-04T06:00:12]
- key: `ORPHAN_SCAN|174 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-04T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-04T06:00:12]
- key: `ROI_STAT|S00: n=161 hit%=30.4% hit_CI[Bonf]=[21.1,41.7]% ROI=0.80 ROI_boot95=[0.58,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.55MB / last modified 2026-11-04T18:08:28.443282+09:00

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
mbos: {'win': 6, '2t': 30, '3t': 120}
2026-11-04 18:07:51,660 [INFO] run_cycle: fetched 19/2 [final]: 156 combos
2026-11-04 18:08:02,811 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=24&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-04 18:08:13,861 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=24&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-04 18:08:26,959 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=24&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-04 18:08:26,959 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=24&hd=20261104
2026-11-04 18:08:26,959 [ERROR] scraper: racelist fetch failed: jcd=24 rno=7
2026-11-04 18:08:26,959 [WARNING] run_cycle: fetch None: 24/7
2026-11-04 18:08:26,959 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-04 18:09:04,318 [INFO] run_cycle: === run_cycle 18:09:04 ===
2026-11-04 18:09:04,318 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-04 18:09:04,318 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-04 18:09:04,409 [INFO] predictor: Models loaded OK
2026-11-04 18:09:33,804 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=7&jcd=24&hd=20261104: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-04 18:09:42,986 [INFO] scraper: odds3t: 120/120 parsed
2026-11-04 18:09:53,085 [INFO] scraper: odds3f: 20/20 parsed
2026-11-04 18:10:02,319 [INFO] scraper: odds2t: 30/30 parsed
2026-11-04 18:10:02,320 [INFO] scraper: odds2f: 15/15 parsed

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
    "c": 36
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 36
  }
]
```

## Phase別通知記録 (24h)
{'final': 13, 'result': 7, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  FINAL_MISSING: 66
  CIRCUIT_BREAKER_NO_ACTION: 33
  CALIBRATION_DRIFT: 29
  PSI_DRIFT_DETECTED: 18
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 3
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 17 | 2 | 5,100 | 2,130 | -2,970 | 0.418 |
| S01_NAKAANA1 | 18 | 7 | 3,600 | 3,600 | +0 | 1.0 |
| S02_TETSUBAN | 7 | 0 | 1,400 | 0 | -1,400 | 0.0 |

## 直近アラート (24h・新しい順)
```
[18:08:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 344, "n_recent": 42, "psi": 0.44}
[18:08:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 449}
[17:58:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 452}
[17:55:21] FINAL_MISSING: {"deadline": "2026-11-04T13:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110422061315", "sid": "S00"}
[17:55:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 459}
[17:50:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 458}
[17:47:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 455}
[17:41:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 437}
[17:40:36] FINAL_MISSING: {"deadline": "2026-11-04T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110421081159", "sid": "S00"}
[17:40:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 442}
```

## 本日残レース: 26件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 118件 締切済
- 通知発射: scan=16 nid / final=13 nid / result=6 nid
- predictions: 6 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 153R | win | 1 | 0.5334 | 5.1 | 2.72 | 300 | scan=- drift=- | 16:17:14 |
| S00 | 2210R | win | 1 | 0.0568 | 11.0 | 0.62 | 300 | scan=- drift=- | 15:11:42 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=3.5 drift=-8.6% | 13:21:49 |
| S02_TETSUBAN | 2110R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 13:03:25 |
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:55:26 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 08:59:15 |
| S01_NAKAANA1 | 191R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.5 drift=-11.4% | 17:40:03 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=4.3 drift=-18.6% | 16:41:26 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.0 drift=+0.0% | 13:48:39 |
| S01_NAKAANA1 | 175R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=- drift=- | 12:12:01 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 19 | -7.5% | -54.4% | +54.8% | 6 | 4 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 466.3s |
| **Latency** (scan→final max) | 671.3s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 386 | 0.4777 | 0.3342 | +0.1435 | 🟡+30% | 0.2352 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 158 | 0.4380 | 0.2911 | 0.2214 | 🔴-0.07 | 0.785 |
| S01_NAKAANA1 | win | 163 | 0.4869 | 0.3313 | 0.2370 | 🔴-0.07 | 0.781 |
| S02_TETSUBAN | win | 65 | 0.5510 | 0.4462 | 0.2643 | 🔴-0.07 | 1.032 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 137 | 0.4126 | 0.2993 | 🔴+0.1134 |
| 0.50+ | 227 | 0.5452 | 0.3789 | 🔴+0.1663 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 364 | 0.741 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-11-04T18:10:01.480076+09:00_