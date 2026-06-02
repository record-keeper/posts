# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-02T12:20:01.834466+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×20 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×60 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-06-02T12:09:34]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-06-02T12:02:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-06-02T12:02:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-06-02T12:02:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-02T12:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-06-02T09:00:11]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-02T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-02T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-02T06:00:10]
- key: `ROI_STAT|S00: n=172 hit%=28.5% hit_CI[Bonf]=[19.7,39.2]% ROI=0.87 ROI_boot95=[0.64,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-02T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=116 hit%=31.0% hit_CI[Bonf]=[20.3,44.4]% ROI=0.79 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=116<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-02T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=61 hit%=45.9% hit_CI[Bonf]=[29.1,63.7]% ROI=0.85 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-02T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=61<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-02T06:00:10]
- key: `ORPHAN_SCAN|228 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-02T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=47 hit%=31.9% ROI=0.91 (コスト 13,700/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-02T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=27.5% ROI=0.74 (コスト 8,800/回収 6,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-02T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=30.4% ROI=0.79 (コスト 16,100/回収 12,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-02T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=25.7% ROI=0.96 (コスト 8,200/回収 7,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-02T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=19.4% ROI=0.49 (コスト 9,200/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.04MB / last modified 2026-06-02T12:19:06.689555+09:00

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
rsed
2026-06-02 12:18:20,841 [INFO] scraper: fetch_race 23/9: boats=6 odds=190/191
2026-06-02 12:18:20,853 [INFO] predictor: CALIBRATION_MODE=on
2026-06-02 12:18:20,853 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-02 12:18:20,860 [INFO] run_cycle: fetched 23/9 [final]: 155 combos
2026-06-02 12:18:24,483 [INFO] scraper: odds3t: 120/120 parsed
2026-06-02 12:18:25,570 [INFO] scraper: odds3f: 20/20 parsed
2026-06-02 12:18:26,898 [INFO] scraper: odds2t: 28/30 parsed
2026-06-02 12:18:26,899 [INFO] scraper: odds2f: 15/15 parsed
2026-06-02 12:18:27,968 [INFO] scraper: odds_win: 4/6 parsed
2026-06-02 12:18:27,968 [INFO] scraper: fetch_race 09/5: boats=6 odds=187/191
2026-06-02 12:18:27,977 [INFO] predictor: CALIBRATION_MODE=on
2026-06-02 12:18:27,977 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-06-02 12:18:27,985 [INFO] run_cycle: fetched 09/5 [scan]: 152 combos
2026-06-02 12:18:31,704 [INFO] scraper: odds3t: 120/120 parsed
2026-06-02 12:18:32,805 [INFO] scraper: odds3f: 20/20 parsed
2026-06-02 12:18:33,969 [INFO] scraper: odds2t: 30/30 parsed
2026-06-02 12:18:33,971 [INFO] scraper: odds2f: 15/15 parsed
2026-06-02 12:18:35,108 [INFO] scraper: odds_win: 4/6 parsed
2026-06-02 12:18:35,108 [INFO] scraper: fetch_race 14/9: boats=6 odds=189/191
2026-06-02 12:18:35,118 [INFO] predictor: CALIBRATION_MODE=on
2026-06-02 12:18:35,118 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-02 12:18:35,126 [INFO] run_cycle: fetched 14/9 [scan]: 154 combos
2026-06-02 12:18:35,231 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-02 12:19:06,330 [INFO] run_cycle: === run_cycle 12:19:06 ===
2026-06-02 12:19:06,330 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-02 12:19:06,330 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-02 12:19:06,410 [INFO] predictor: Models loaded OK
2026-06-02 12:19:06,660 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 40
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 40
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 6, 'scan': 18}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 60
  ANOMALY_SCRAPER_FAILURE_BURST: 26
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 7 | 10,200 | 4,350 | -5,850 | 0.426 |
| S01_NAKAANA1 | 36 | 14 | 7,200 | 6,900 | -300 | 0.958 |
| S02_TETSUBAN | 15 | 6 | 3,000 | 2,360 | -640 | 0.787 |

## 直近アラート (24h・新しい順)
```
[12:13:05] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4350, "roi_7d": 0.414, "sid": "S00"}
[12:09:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.195, "baseline_mean": 0.805, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.6}
[12:02:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:48:29] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 5100, "roi_7d": 0.472, "sid": "S00"}
[11:01:41] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:41] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:48:05] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 5100, "roi_7d": 0.472, "sid": "S00"}
[10:01:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:21] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 5100, "roi_7d": 0.459, "sid": "S00"}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 39件 締切済
- 通知発射: scan=3 nid / final=4 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 236R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=- drift=- | 10:49:20 |
| S02_TETSUBAN | 204R | win | 1 | 0.4989 | 2.5 | 1.25 | 200 | scan=2.1 drift=+19.0% | 16:57:21 |
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.5 drift=+4.0% | 14:53:22 |
| S02_TETSUBAN | 136R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 12:57:21 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5735 | 3.4 | 1.95 | 200 | scan=3.4 drift=+0.0% | 12:20:25 |
| S00 | 051R | win | 1 | 0.5735 | 6.6 | 3.78 | 300 | scan=4.0 drift=+65.0% | 11:52:33 |
| S00 | 112R | win | 1 | 0.0923 | 27.7 | 2.56 | 300 | scan=5.2 drift=+432.7% | 11:05:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5174 | 3.9 | 2.02 | 200 | scan=4.1 drift=-4.9% | 09:07:45 |
| S00 | 1510R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.3 drift=+4.7% | 19:30:23 |
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.8 | 1.40 | 200 | scan=- drift=- | 19:24:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +20.9% | -81.4% | +432.7% | 11 | 5 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 429.3s |
| **Latency** (scan→final max) | 602.8s |
| **Traffic** (notifications 24h) | 40 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 347 | 0.4611 | 0.3256 | +0.1355 | 🟡+29% | 0.2357 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4248 | 0.2899 | 0.2206 | 🔴-0.07 | 0.887 |
| S01_NAKAANA1 | win | 117 | 0.4847 | 0.3077 | 0.2457 | 🔴-0.15 | 0.786 |
| S02_TETSUBAN | win | 61 | 0.5165 | 0.4590 | 0.2585 | 🔴-0.04 | 0.854 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.20-0.30 | 7 | 0.2227 | 0.4286 | 🔴-0.2059 |
| 0.30-0.50 | 146 | 0.4154 | 0.2740 | 🔴+0.1414 |
| 0.50+ | 178 | 0.5398 | 0.3876 | 🔴+0.1522 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 28 | 0.77 |
| win | <5.0 | ✅learned | 55 | 0.757 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-02T12:20:01.834466+09:00_