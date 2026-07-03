# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-03T13:00:01.771253+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×40 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×10 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×9  [2026-07-03T12:51:23]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-03T12:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×57  [2026-07-03T12:02:48]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-07-03T12:02:48]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-07-03T11:35:30]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-03T06:00:09]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2253 actual=0.0833 gap=+0.1420`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 9,500/回収 5,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=26 hit%=30.8% ROI=1.03 (コスト 6,300/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=23.3% ROI=0.51 (コスト 8,400/回収 4,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=22 pred=0.3216 actual=0.1818 gap=+0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S00: n=165 hit%=26.1% hit_CI[Bonf]=[17.5,36.9]% ROI=0.71 ROI_boot95=[0.51,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-03T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-03T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=28.4% hit_CI[Bonf]=[16.1,45.1]% ROI=0.44 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=27.8% ROI=0.85 (コスト 10,500/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-03T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=85 hit%=29.4% ROI=0.74 (コスト 19,900/回収 14,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-03T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=376 pred=0.4808 actual=0.2846 error=+0.1962 (+41%) brier=0.2376 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.64MB / last modified 2026-07-03T13:00:03.936887+09:00

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
 154 combos
2026-07-03 12:58:24,196 [WARNING] scraper: beforeinfo parse failed: jcd=23 rno=10
2026-07-03 12:58:24,196 [WARNING] run_cycle: fetch None: 23/10
2026-07-03 12:58:27,706 [INFO] scraper: odds3t: 120/120 parsed
2026-07-03 12:58:28,796 [INFO] scraper: odds3f: 20/20 parsed
2026-07-03 12:58:29,908 [INFO] scraper: odds2t: 30/30 parsed
2026-07-03 12:58:29,909 [INFO] scraper: odds2f: 12/15 parsed
2026-07-03 12:58:30,990 [INFO] scraper: odds_win: 3/6 parsed
2026-07-03 12:58:30,990 [INFO] scraper: fetch_race 09/6: boats=6 odds=185/191
2026-07-03 12:58:31,000 [INFO] predictor: CALIBRATION_MODE=on
2026-07-03 12:58:31,000 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-07-03 12:58:31,008 [INFO] run_cycle: fetched 09/6 [scan]: 153 combos
2026-07-03 12:58:31,128 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-03 12:59:06,491 [INFO] run_cycle: === run_cycle 12:59:06 ===
2026-07-03 12:59:06,491 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-03 12:59:06,491 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-03 12:59:06,566 [INFO] predictor: Models loaded OK
2026-07-03 12:59:17,054 [WARNING] scraper: beforeinfo parse failed: jcd=23 rno=10
2026-07-03 12:59:17,054 [WARNING] run_cycle: fetch None: 23/10
2026-07-03 12:59:20,837 [INFO] scraper: odds3t: 120/120 parsed
2026-07-03 12:59:21,934 [INFO] scraper: odds3f: 18/20 parsed
2026-07-03 12:59:23,124 [INFO] scraper: odds2t: 27/30 parsed
2026-07-03 12:59:23,125 [INFO] scraper: odds2f: 13/15 parsed
2026-07-03 12:59:24,238 [INFO] scraper: odds_win: 2/6 parsed
2026-07-03 12:59:24,239 [INFO] scraper: fetch_race 22/3: boats=6 odds=180/191
2026-07-03 12:59:24,251 [INFO] predictor: CALIBRATION_MODE=on
2026-07-03 12:59:24,251 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-07-03 12:59:24,259 [INFO] run_cycle: fetched 22/3 [scan]: 149 combos
2026-07-03 12:59:24,375 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 57
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 57
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 8, 'scan': 24}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 40
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 10
  ANOMALY_BET_VOLUME_DROP: 7
  ANOMALY_SCRAPER_FAILURE_BURST: 7
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 10 | 11,100 | 7,710 | -3,390 | 0.695 |
| S01_NAKAANA1 | 37 | 12 | 7,400 | 5,820 | -1,580 | 0.786 |
| S02_TETSUBAN | 17 | 4 | 3,400 | 1,300 | -2,100 | 0.382 |

## 直近アラート (24h・新しい順)
```
[12:54:24] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 7710, "roi_7d": 0.695, "sid": "S00"}
[12:51:23] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -18.6, "final": 3.5, "kind": "LARGE_ODDS_DRIFT", "race": "043R", "scan": 4.3, "sid": "S01_NAKAANA1"}
[12:01:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:54:06] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 7710, "roi_7d": 0.695, "sid": "S00"}
[11:50:35] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 7710, "roi_7d": 0.676, "sid": "S00"}
[11:35:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1030}
[11:01:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 114件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 54件 締切済
- 通知発射: scan=11 nid / final=12 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 116R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 12:57:33 |
| S01_NAKAANA1 | 043R | win | 1 | 0.2864 | 3.5 | 1.00 | 200 | scan=4.3 drift=-18.6% | 12:51:21 |
| S02_TETSUBAN | 094R | win | 1 | 0.5545 | 2.5 | 1.39 | 200 | scan=2.4 drift=+4.2% | 12:06:20 |
| S02_TETSUBAN | 162R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=2.5 drift=-12.0% | 11:09:20 |
| S01_NAKAANA1 | 234R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.4 drift=+8.8% | 09:59:45 |
| S00 | 194R | win | 1 | 0.4111 | 6.5 | 2.67 | 300 | scan=- drift=- | 17:04:46 |
| S02_TETSUBAN | 0510R | win | 1 | 0.5174 | 2.6 | 1.35 | 200 | scan=2.3 drift=+13.0% | 16:13:20 |
| S00 | 0610R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 16:05:22 |
| S02_TETSUBAN | 059R | win | 1 | 0.5719 | 2.6 | 1.49 | 200 | scan=2.5 drift=+4.0% | 15:38:21 |
| S00 | 088R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.3 drift=+4.7% | 14:10:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +8.9% | -68.9% | +584.6% | 22 | 11 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 478.3s |
| **Latency** (scan→final max) | 624.3s |
| **Traffic** (notifications 24h) | 57 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 373 | 0.4813 | 0.2869 | +0.1945 | 🟡+40% | 0.2384 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4434 | 0.2622 | 0.2206 | 🔴-0.14 | 0.711 |
| S01_NAKAANA1 | win | 136 | 0.4945 | 0.3162 | 0.2430 | 🔴-0.12 | 0.838 |
| S02_TETSUBAN | win | 73 | 0.5422 | 0.2877 | 0.2696 | 🔴-0.32 | 0.466 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1780 | 0.2857 | 🔴-0.1077 |
| 0.20-0.30 | 12 | 0.2253 | 0.0833 | 🔴+0.1420 |
| 0.30-0.50 | 130 | 0.4228 | 0.2462 | 🔴+0.1767 |
| 0.50+ | 221 | 0.5445 | 0.3258 | 🔴+0.2187 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 50 | 0.733 |
| win | <5.0 | ✅learned | 111 | 0.716 |
| win | <10.0 | ✅learned | 62 | 0.486 |
| win | <20.0 | ✅learned | 18 | 0.212 |
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
_auto-generated by claude_snapshot.py at 2026-07-03T13:00:01.771253+09:00_