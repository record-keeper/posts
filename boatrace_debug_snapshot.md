# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-22T13:50:01.333882+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×18  [2026-07-22T13:32:51]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×96  [2026-07-22T13:02:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×96  [2026-07-22T13:02:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-07-22T13:02:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-22T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-22T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-07-22T12:03:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×41  [2026-07-22T11:45:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-07-22T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=27.3% ROI=0.54 (コスト 8,000/回収 4,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2268 actual=0.2667 gap=-0.0399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3243 actual=0.0857 gap=+0.2386`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=46.4% hit_CI[Bonf]=[30.4,63.1]% ROI=0.94 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S00: n=182 hit%=26.4% hit_CI[Bonf]=[18.1,36.7]% ROI=0.70 ROI_boot95=[0.51,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-22T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-22T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=29.2% hit_CI[Bonf]=[20.1,40.4]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=23.3% ROI=0.54 (コスト 8,800/回収 4,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-22T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.74 (コスト 11,000/回収 8,110)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.4MB / last modified 2026-07-22T13:49:20.741816+09:00

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
arsed
2026-07-22 13:47:24,497 [INFO] scraper: odds2t: 28/30 parsed
2026-07-22 13:47:24,498 [INFO] scraper: odds2f: 15/15 parsed
2026-07-22 13:47:25,579 [INFO] scraper: odds_win: 6/6 parsed
2026-07-22 13:47:25,580 [INFO] scraper: fetch_race 08/8: boats=6 odds=189/191
2026-07-22 13:47:25,583 [INFO] predictor: CALIBRATION_MODE=on
2026-07-22 13:47:25,583 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-07-22 13:47:25,602 [INFO] run_cycle: fetched 08/8 [scan]: 154 combos
2026-07-22 13:47:25,780 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-22 13:48:03,377 [INFO] run_cycle: === run_cycle 13:48:03 ===
2026-07-22 13:48:03,377 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-22 13:48:03,377 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-22 13:48:03,420 [INFO] predictor: Models loaded OK
2026-07-22 13:48:03,656 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-22 13:49:04,114 [INFO] run_cycle: === run_cycle 13:49:04 ===
2026-07-22 13:49:04,114 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-22 13:49:04,114 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-22 13:49:04,157 [INFO] predictor: Models loaded OK
2026-07-22 13:49:16,930 [INFO] scraper: odds3t: 120/120 parsed
2026-07-22 13:49:18,090 [INFO] scraper: odds3f: 20/20 parsed
2026-07-22 13:49:19,183 [INFO] scraper: odds2t: 30/30 parsed
2026-07-22 13:49:19,184 [INFO] scraper: odds2f: 15/15 parsed
2026-07-22 13:49:20,317 [INFO] scraper: odds_win: 6/6 parsed
2026-07-22 13:49:20,317 [INFO] scraper: fetch_race 10/12: boats=6 odds=191/191
2026-07-22 13:49:20,320 [INFO] predictor: CALIBRATION_MODE=on
2026-07-22 13:49:20,320 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-22 13:49:20,324 [INFO] run_cycle: fetched 10/12 [scan]: 156 combos
2026-07-22 13:49:20,437 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 11, 'scan': 22}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 48
  CIRCUIT_BREAKER_TRIP: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCRAPER_FAILURE_BURST: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  CALIBRATION_DRIFT: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 7 | 12,600 | 7,080 | -5,520 | 0.562 |
| S01_NAKAANA1 | 42 | 7 | 8,400 | 4,880 | -3,520 | 0.581 |
| S02_TETSUBAN | 16 | 9 | 3,200 | 3,680 | +480 | 1.15 |

## 直近アラート (24h・新しい順)
```
[13:32:51] CALIBRATION_DRIFT: {"avg_actual": 0.23, "avg_pred": 0.4673, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 100, "overconf_pct": 50.8}
[13:26:44] FINAL_MISSING: {"deadline": "2026-07-22T12:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072223101256", "sid": "S00"}
[13:11:43] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 7080, "roi_7d": 0.562, "sid": "S00"}
[13:02:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:02:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:00:24] CIRCUIT_BREAKER_TRIP: {"cost": 8400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 4880, "roi_7d": 0.581, "sid": "S01_NAKAANA1"}
[13:00:24] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -25.4, "final": 4.7, "kind": "LARGE_ODDS_DRIFT", "race": "054R", "scan": 6.3, "sid": "S00"}
[12:57:27] FINAL_MISSING: {"deadline": "2026-07-22T12:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072214091227", "sid": "S00"}
[12:43:20] CALIBRATION_DRIFT: {"avg_actual": 0.2268, "avg_pred": 0.4674, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 51.5}
```

## 本日残レース: 76件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 68件 締切済
- 通知発射: scan=11 nid / final=13 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 054R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=3.0 drift=+56.7% | 13:00:22 |
| S00 | 054R | win | 1 | 0.4111 | 4.7 | 1.93 | 300 | scan=6.3 drift=-25.4% | 13:00:20 |
| S02_TETSUBAN | 053R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 12:28:19 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=- drift=- | 12:11:29 |
| S00 | 148R | win | 1 | 0.5719 | 4.3 | 2.46 | 300 | scan=- drift=- | 11:55:18 |
| S01_NAKAANA1 | 083R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 11:37:18 |
| S01_NAKAANA1 | 147R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.5 drift=-15.6% | 11:25:18 |
| S01_NAKAANA1 | 159R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=- drift=- | 19:09:29 |
| S01_NAKAANA1 | 196R | win | 1 | 0.4920 | 3.2 | 1.57 | 200 | scan=3.8 drift=-15.8% | 18:06:30 |
| S00 | 126R | win | 1 | 0.4111 | 12.7 | 5.22 | 300 | scan=4.8 drift=+164.6% | 17:46:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +22.0% | -83.7% | +628.9% | 21 | 8 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 449.8s |
| **Latency** (scan→final max) | 618.2s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4676 | 0.3123 | +0.1553 | 🟡+33% | 0.2355 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 181 | 0.4294 | 0.2652 | 0.2272 | 🔴-0.17 | 0.707 |
| S01_NAKAANA1 | win | 162 | 0.4784 | 0.2963 | 0.2373 | 🔴-0.14 | 0.819 |
| S02_TETSUBAN | win | 70 | 0.5413 | 0.4714 | 0.2530 | 🔴-0.02 | 0.951 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1798 | 0.4286 | 🔴-0.2488 |
| 0.20-0.30 | 15 | 0.2268 | 0.2667 | ✅-0.0399 |
| 0.30-0.50 | 164 | 0.4176 | 0.2683 | 🔴+0.1493 |
| 0.50+ | 220 | 0.5418 | 0.3500 | 🔴+0.1918 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 79 | 0.811 |
| win | <5.0 | ✅learned | 150 | 0.722 |
| win | <10.0 | ✅learned | 75 | 0.466 |
| win | <20.0 | ✅learned | 25 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-07-22T13:50:01.333882+09:00_