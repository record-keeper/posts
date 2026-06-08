# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-08T12:50:02.334382+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×66 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×66 (24h)
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CALIBRATION_DRIFT×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×7 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×12  [2026-06-08T12:34:23]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T12:30:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T12:30:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-08T12:30:09]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×44  [2026-06-08T12:05:40]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CALIBRATION_DRIFT  ×46  [2026-06-08T12:03:28]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×138  [2026-06-08T12:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×138  [2026-06-08T12:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-06-08T12:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×5  [2026-06-08T12:00:48]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-06-08T11:55:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-08T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-08T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S00: n=154 hit%=24.7% hit_CI[Bonf]=[16.1,35.8]% ROI=0.76 ROI_boot95=[0.52,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=27.0% hit_CI[Bonf]=[17.7,38.8]% ROI=0.67 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-08T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.72 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-08T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-08T06:00:10]
- key: `ORPHAN_SCAN|206 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.67MB / last modified 2026-06-08T12:49:40.525500+09:00

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
-08 12:49:05,791 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-08 12:49:05,833 [INFO] predictor: Models loaded OK
2026-06-08 12:49:16,907 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=21&hd=20260608: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-08 12:49:28,448 [INFO] scraper: odds3t: 120/120 parsed
2026-06-08 12:49:29,560 [INFO] scraper: odds3f: 20/20 parsed
2026-06-08 12:49:30,653 [INFO] scraper: odds2t: 30/30 parsed
2026-06-08 12:49:30,654 [INFO] scraper: odds2f: 15/15 parsed
2026-06-08 12:49:31,741 [INFO] scraper: odds_win: 5/6 parsed
2026-06-08 12:49:31,741 [INFO] scraper: fetch_race 21/10: boats=6 odds=190/191
2026-06-08 12:49:31,753 [INFO] predictor: CALIBRATION_MODE=on
2026-06-08 12:49:31,753 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-08 12:49:31,760 [INFO] run_cycle: fetched 21/10 [final]: 155 combos
2026-06-08 12:49:32,268 [INFO] race_id: notif: nid=2026060821101252 sid=S02_TETSUBAN phase=final rank=B
2026-06-08 12:49:32,642 [INFO] notifier: Discord notify OK (status=204)
2026-06-08 12:49:32,995 [INFO] notifier: Discord notify OK (status=204)
2026-06-08 12:49:32,999 [INFO] run_cycle: FINAL S02_TETSUBAN 芦屋10R B
2026-06-08 12:49:36,541 [INFO] scraper: odds3t: 120/120 parsed
2026-06-08 12:49:37,643 [INFO] scraper: odds3f: 20/20 parsed
2026-06-08 12:49:38,746 [INFO] scraper: odds2t: 30/30 parsed
2026-06-08 12:49:38,747 [INFO] scraper: odds2f: 14/15 parsed
2026-06-08 12:49:39,874 [INFO] scraper: odds_win: 4/6 parsed
2026-06-08 12:49:39,874 [INFO] scraper: fetch_race 06/4: boats=6 odds=188/191
2026-06-08 12:49:39,877 [INFO] predictor: CALIBRATION_MODE=on
2026-06-08 12:49:39,877 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-08 12:49:39,881 [INFO] run_cycle: fetched 06/4 [scan]: 154 combos
2026-06-08 12:49:40,078 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 11, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 246
  CIRCUIT_BREAKER_TRIP: 66
  FINAL_MISSING: 63
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 33
  ANOMALY_SCAN_FINAL_RATIO: 22
  ANOMALY_BET_VOLUME_SPIKE: 18
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 7
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 27 | 4 | 8,100 | 3,390 | -4,710 | 0.419 |
| S01_NAKAANA1 | 25 | 2 | 5,000 | 580 | -4,420 | 0.116 |
| S02_TETSUBAN | 26 | 6 | 5,200 | 1,680 | -3,520 | 0.323 |

## 直近アラート (24h・新しい順)
```
[12:49:40] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1680, "roi_7d": 0.323, "sid": "S02_TETSUBAN"}
[12:49:40] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 78, "psi": 0.32}
[12:45:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1096}
[12:44:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1109}
[12:43:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1105}
[12:42:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1095}
[12:41:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1079}
[12:39:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1084}
[12:38:32] CALIBRATION_DRIFT: {"avg_actual": 0.1558, "avg_pred": 0.4868, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 77, "overconf_pct": 68.0}
[12:38:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1075}
```

## 本日残レース: 90件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 54件 締切済
- 通知発射: scan=13 nid / final=11 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 2110R | win | 1 | 0.5383 | 2.0 | 1.08 | 200 | scan=2.1 drift=-4.8% | 12:49:31 |
| S00 | 094R | win | 1 | 0.5476 | 14.2 | 7.78 | 300 | scan=6.7 drift=+111.9% | 12:05:38 |
| S01_NAKAANA1 | 0710R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=- drift=- | 19:47:21 |
| S02_TETSUBAN | 076R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 18:01:22 |
| S02_TETSUBAN | 073R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.5 drift=-16.0% | 16:38:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=- drift=- | 16:01:21 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 15:22:20 |
| S01_NAKAANA1 | 058R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.5 drift=-5.7% | 15:04:32 |
| S00 | 056R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=- drift=- | 14:01:20 |
| S02_TETSUBAN | 2112R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=2.5 drift=+0.0% | 13:56:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 37 | +6.9% | -62.9% | +274.6% | 13 | 7 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 490.3s |
| **Latency** (scan→final max) | 653.4s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 379 | 0.4688 | 0.2876 | +0.1812 | 🟡+39% | 0.2384 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 155 | 0.4246 | 0.2452 | 0.2208 | 🔴-0.19 | 0.755 |
| S01_NAKAANA1 | win | 141 | 0.4851 | 0.2695 | 0.2436 | 🔴-0.24 | 0.673 |
| S02_TETSUBAN | win | 83 | 0.5237 | 0.3976 | 0.2624 | 🔴-0.10 | 0.717 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 151 | 0.4203 | 0.2384 | 🔴+0.1818 |
| 0.50+ | 205 | 0.5414 | 0.3366 | 🔴+0.2048 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 33 | 0.747 |
| win | <5.0 | ✅learned | 59 | 0.732 |
| win | <10.0 | ✅learned | 40 | 0.525 |
| win | <20.0 | ✅learned | 12 | 0.197 |
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
_auto-generated by claude_snapshot.py at 2026-06-08T12:50:02.334382+09:00_