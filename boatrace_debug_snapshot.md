# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-27T13:00:01.665690+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×49 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×87 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×49 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-27T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-27T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-07-27T12:55:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×116  [2026-07-27T12:01:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×116  [2026-07-27T12:01:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-07-27T12:01:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×50  [2026-07-27T11:13:54]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-07-27T06:00:18]
- key: `ORPHAN_SCAN|182 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-27T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-27T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-27T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-27T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=13 pred=0.2273 actual=0.3077 gap=-0.0804`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-27T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=25.7% ROI=0.52 (コスト 8,200/回収 4,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-27T06:00:18]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1262 actual=0.1429 gap=-0.0167`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-27T06:00:18]
- key: `ROI_STAT|S00: n=181 hit%=28.2% hit_CI[Bonf]=[19.7,38.6]% ROI=0.75 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-27T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=26.1% hit_CI[Bonf]=[17.5,37.1]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-27T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=50.0% hit_CI[Bonf]=[34.6,65.4]% ROI=0.98 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-27T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=30.3% ROI=0.63 (コスト 9,700/回収 6,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-27T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.86 (コスト 10,500/回収 9,070)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-27T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=81 hit%=33.3% ROI=0.80 (コスト 18,600/回収 14,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.81MB / last modified 2026-07-27T13:00:03.702319+09:00

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
:26,133 [INFO] scraper: odds2f: 15/15 parsed
2026-07-27 12:59:27,233 [INFO] scraper: odds_win: 6/6 parsed
2026-07-27 12:59:27,233 [INFO] scraper: fetch_race 03/5: boats=6 odds=190/191
2026-07-27 12:59:27,235 [INFO] predictor: CALIBRATION_MODE=on
2026-07-27 12:59:27,235 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-07-27 12:59:27,239 [INFO] run_cycle: fetched 03/5 [final]: 155 combos
2026-07-27 12:59:27,244 [INFO] race_id: notif: nid=2026072703051302 sid=S01_NAKAANA1 phase=final rank=
2026-07-27 12:59:27,709 [INFO] notifier: Discord notify OK (status=204)
2026-07-27 12:59:28,007 [INFO] notifier: Discord notify OK (status=204)
2026-07-27 12:59:28,165 [INFO] run_cycle: RETREAT S01_NAKAANA1 江戸川5R
2026-07-27 12:59:31,593 [INFO] scraper: odds3t: 120/120 parsed
2026-07-27 12:59:32,701 [INFO] scraper: odds3f: 20/20 parsed
2026-07-27 12:59:33,804 [INFO] scraper: odds2t: 30/30 parsed
2026-07-27 12:59:33,806 [INFO] scraper: odds2f: 15/15 parsed
2026-07-27 12:59:34,872 [INFO] scraper: odds_win: 6/6 parsed
2026-07-27 12:59:34,872 [INFO] scraper: fetch_race 14/10: boats=6 odds=191/191
2026-07-27 12:59:34,874 [INFO] predictor: CALIBRATION_MODE=on
2026-07-27 12:59:34,875 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-27 12:59:34,879 [INFO] run_cycle: fetched 14/10 [scan]: 156 combos
2026-07-27 12:59:38,351 [INFO] scraper: odds3t: 120/120 parsed
2026-07-27 12:59:39,455 [INFO] scraper: odds3f: 18/20 parsed
2026-07-27 12:59:40,573 [INFO] scraper: odds2t: 24/30 parsed
2026-07-27 12:59:40,574 [INFO] scraper: odds2f: 9/15 parsed
2026-07-27 12:59:41,636 [INFO] scraper: odds_win: 4/6 parsed
2026-07-27 12:59:41,637 [INFO] scraper: fetch_race 09/6: boats=6 odds=175/191
2026-07-27 12:59:41,639 [INFO] predictor: CALIBRATION_MODE=on
2026-07-27 12:59:41,639 [INFO] predictor: combos: {'win': 4, '2t': 24, '3t': 120}
2026-07-27 12:59:41,643 [INFO] run_cycle: fetched 09/6 [scan]: 148 combos
2026-07-27 12:59:41,760 [INFO] run_cycle: run_cycle done: 1 notifications

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
{'final': 24, 'result': 12, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 167
  FINAL_MISSING: 87
  CIRCUIT_BREAKER_TRIP: 49
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 9 | 12,300 | 8,370 | -3,930 | 0.68 |
| S01_NAKAANA1 | 34 | 6 | 6,800 | 4,320 | -2,480 | 0.635 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,020 | -380 | 0.888 |

## 直近アラート (24h・新しい順)
```
[12:51:45] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 8370, "roi_7d": 0.698, "sid": "S00"}
[12:51:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.245, "baseline_mean": 0.745, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -2.98}
[12:49:21] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4320, "roi_7d": 0.655, "sid": "S01_NAKAANA1"}
[12:44:03] FINAL_MISSING: {"deadline": "2026-07-27T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026072702041214", "sid": "S00"}
[12:35:33] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 8370, "roi_7d": 0.68, "sid": "S00"}
[12:12:18] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4320, "roi_7d": 0.635, "sid": "S01_NAKAANA1"}
[12:10:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1105}
[12:09:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1113}
[12:08:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1117}
[12:07:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1114}
```

## 本日残レース: 102件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 54件 締切済
- 通知発射: scan=6 nid / final=7 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 175R | win | 1 | 0.5334 | 6.3 | 3.36 | 300 | scan=- drift=- | 12:59:18 |
| S01_NAKAANA1 | 175R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.0 drift=+10.0% | 12:58:18 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=4.1 drift=-7.3% | 11:40:22 |
| S01_NAKAANA1 | 022R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:14:30 |
| S00 | 104R | win | 1 | 0.5891 | 4.2 | 2.47 | 300 | scan=- drift=- | 09:54:18 |
| S02_TETSUBAN | 208R | win | 1 | 0.4920 | 2.2 | 1.08 | 200 | scan=- drift=- | 18:55:31 |
| S00 | 203R | win | 1 | 0.5010 | 5.4 | 2.71 | 300 | scan=6.0 drift=-10.0% | 16:34:26 |
| S02_TETSUBAN | 1312R | win | 1 | 0.4111 | 2.9 | 1.19 | 200 | scan=- drift=- | 16:20:20 |
| S00 | 012R | win | 1 | 0.3177 | 10.6 | 3.37 | 300 | scan=5.6 drift=+89.3% | 15:55:42 |
| S00 | 0210R | win | 1 | 0.5123 | 7.6 | 3.89 | 300 | scan=7.8 drift=-2.6% | 15:18:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | +9.3% | -86.1% | +198.5% | 13 | 8 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.3s |
| **Latency** (scan→final max) | 628.7s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 423 | 0.4640 | 0.3168 | +0.1472 | 🟡+32% | 0.2333 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4205 | 0.2778 | 0.2239 | 🔴-0.12 | 0.749 |
| S01_NAKAANA1 | win | 163 | 0.4757 | 0.2699 | 0.2364 | 🔴-0.20 | 0.74 |
| S02_TETSUBAN | win | 80 | 0.5381 | 0.5000 | 0.2484 | ✅+0.01 | 0.978 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 13 | 0.2273 | 0.3077 | 🔴-0.0804 |
| 0.30-0.50 | 169 | 0.4168 | 0.2722 | 🔴+0.1446 |
| 0.50+ | 222 | 0.5415 | 0.3604 | 🔴+0.1812 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 86 | 0.804 |
| win | <5.0 | ✅learned | 154 | 0.722 |
| win | <10.0 | ✅learned | 82 | 0.455 |
| win | <20.0 | ✅learned | 26 | 0.216 |
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
_auto-generated by claude_snapshot.py at 2026-07-27T13:00:01.665690+09:00_