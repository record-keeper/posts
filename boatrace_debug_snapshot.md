# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-01T13:40:01.744159+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×21 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×37 (24h)
- 🔴 PSI_DRIFT_DETECTED×21 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×31  [2026-07-01T13:04:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×31  [2026-07-01T13:04:27]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×31  [2026-07-01T13:04:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-07-01T13:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×5  [2026-07-01T12:59:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-07-01T11:35:29]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×1  [2026-07-01T11:27:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 PSI_DRIFT_DETECTED  ×3  [2026-07-01T11:02:41]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_DROP  ×34  [2026-07-01T11:01:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-01T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-01T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-01T06:00:47]
- key: `ORPHAN_SCAN|154 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-01T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-01T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-01T06:00:47]
- key: `DRIFT_BUCKET|drift ≥+30%: n=30 hit%=26.7% ROI=0.55 (コスト 8,400/回収 4,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-01T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2269 actual=0.0909 gap=+0.1360`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-01T06:00:47]
- key: `ROI_STAT|S00: n=160 hit%=26.9% hit_CI[Bonf]=[18.1,38.0]% ROI=0.72 ROI_boot95=[0.53,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-01T06:00:47]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=31.4% hit_CI[Bonf]=[21.3,43.6]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-01T06:00:47]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=30.6% hit_CI[Bonf]=[17.6,47.5]% ROI=0.47 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-01T06:00:47]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=27.0% ROI=0.83 (コスト 10,800/回収 8,940)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.54MB / last modified 2026-07-01T13:39:35.441771+09:00

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
026-07-01 13:38:23,874 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-01 13:39:07,759 [INFO] run_cycle: === run_cycle 13:39:07 ===
2026-07-01 13:39:07,759 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-01 13:39:07,759 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-01 13:39:07,802 [INFO] predictor: Models loaded OK
2026-07-01 13:39:20,338 [INFO] scraper: odds3t: 120/120 parsed
2026-07-01 13:39:21,474 [INFO] scraper: odds3f: 20/20 parsed
2026-07-01 13:39:22,662 [INFO] scraper: odds2t: 30/30 parsed
2026-07-01 13:39:22,663 [INFO] scraper: odds2f: 15/15 parsed
2026-07-01 13:39:23,759 [INFO] scraper: odds_win: 5/6 parsed
2026-07-01 13:39:23,759 [INFO] scraper: fetch_race 08/7: boats=6 odds=190/191
2026-07-01 13:39:23,772 [INFO] predictor: CALIBRATION_MODE=on
2026-07-01 13:39:23,772 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-01 13:39:23,780 [INFO] run_cycle: fetched 08/7 [final]: 155 combos
2026-07-01 13:39:26,622 [INFO] race_id: notif: nid=2026070108071342 sid=S00 phase=final rank=SSS
2026-07-01 13:39:27,044 [INFO] notifier: Discord notify OK (status=204)
2026-07-01 13:39:27,842 [INFO] notifier: Discord notify OK (status=204)
2026-07-01 13:39:27,966 [INFO] run_cycle: FINAL S00 常滑7R SSS
2026-07-01 13:39:31,473 [INFO] scraper: odds3t: 120/120 parsed
2026-07-01 13:39:32,562 [INFO] scraper: odds3f: 20/20 parsed
2026-07-01 13:39:33,666 [INFO] scraper: odds2t: 30/30 parsed
2026-07-01 13:39:33,667 [INFO] scraper: odds2f: 15/15 parsed
2026-07-01 13:39:34,767 [INFO] scraper: odds_win: 6/6 parsed
2026-07-01 13:39:34,768 [INFO] scraper: fetch_race 02/7: boats=6 odds=191/191
2026-07-01 13:39:34,777 [INFO] predictor: CALIBRATION_MODE=on
2026-07-01 13:39:34,779 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-01 13:39:34,787 [INFO] run_cycle: fetched 02/7 [scan]: 156 combos
2026-07-01 13:39:35,091 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 21, 'result': 9, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 216
  FINAL_MISSING: 37
  PSI_DRIFT_DETECTED: 21
  CIRCUIT_BREAKER_TRIP: 20
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 3
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 10 | 13,500 | 7,590 | -5,910 | 0.562 |
| S01_NAKAANA1 | 39 | 16 | 7,800 | 7,580 | -220 | 0.972 |
| S02_TETSUBAN | 10 | 3 | 2,000 | 800 | -1,200 | 0.4 |

## 直近アラート (24h・新しい順)
```
[13:24:09] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 7590, "roi_7d": 0.562, "sid": "S00"}
[13:05:32] CIRCUIT_BREAKER_TRIP: {"cost": 13200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 7590, "roi_7d": 0.575, "sid": "S00"}
[13:04:24] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:04:24] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:03:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1068}
[13:01:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[13:00:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1050}
[12:59:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1060}
[12:23:59] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 7590, "roi_7d": 0.562, "sid": "S00"}
[12:13:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1131}
```

## 本日残レース: 102件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 66件 締切済
- 通知発射: scan=5 nid / final=9 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 087R | win | 1 | 0.4111 | 18.0 | 7.40 | 300 | scan=6.0 drift=+200.0% | 13:39:23 |
| S00 | 064R | win | 1 | 0.3599 | 4.0 | 1.44 | 300 | scan=- drift=- | 13:07:24 |
| S00 | 115R | win | 1 | 0.2082 | 16.5 | 3.43 | 300 | scan=- drift=- | 12:23:47 |
| S02_TETSUBAN | 164R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=- drift=- | 12:09:32 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 11:56:33 |
| S01_NAKAANA1 | 163R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=4.0 drift=-15.0% | 11:37:36 |
| S00 | 082R | win | 1 | 0.4111 | 9.3 | 3.82 | 300 | scan=6.0 drift=+55.0% | 11:02:34 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 19:00:26 |
| S00 | 197R | win | 1 | 0.4989 | 6.3 | 3.14 | 300 | scan=- drift=- | 18:18:22 |
| S00 | 089R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=6.7 drift=+11.9% | 14:29:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +11.1% | -68.9% | +584.6% | 24 | 13 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 540.3s |
| **Latency** (scan→final max) | 611.6s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 369 | 0.4816 | 0.2873 | +0.1943 | 🟡+40% | 0.2398 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4419 | 0.2625 | 0.2236 | 🔴-0.15 | 0.714 |
| S01_NAKAANA1 | win | 137 | 0.4948 | 0.3139 | 0.2431 | 🔴-0.13 | 0.831 |
| S02_TETSUBAN | win | 72 | 0.5448 | 0.2917 | 0.2694 | 🔴-0.30 | 0.451 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 12 | 0.2253 | 0.0833 | 🔴+0.1420 |
| 0.30-0.50 | 123 | 0.4246 | 0.2439 | 🔴+0.1807 |
| 0.50+ | 222 | 0.5444 | 0.3243 | 🔴+0.2200 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 49 | 0.725 |
| win | <5.0 | ✅learned | 111 | 0.716 |
| win | <10.0 | ✅learned | 60 | 0.489 |
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
_auto-generated by claude_snapshot.py at 2026-07-01T13:40:01.744159+09:00_