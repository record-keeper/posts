# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-28T14:00:02.084654+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×92 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🔴 CALIBRATION_DRIFT×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×16  [2026-06-28T13:43:20]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-28T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×47  [2026-06-28T13:11:34]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-06-28T13:02:40]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-06-28T13:02:40]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-06-28T13:02:40]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×25  [2026-06-28T13:02:40]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CALIBRATION_DRIFT  ×51  [2026-06-28T11:01:46]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-06-28T11:00:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×26  [2026-06-28T10:40:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=23 pred=0.3214 actual=0.2174 gap=+0.1040`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S00: n=167 hit%=25.1% hit_CI[Bonf]=[16.8,35.9]% ROI=0.65 ROI_boot95=[0.46,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=29.2% hit_CI[Bonf]=[19.4,41.3]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=28.8% hit_CI[Bonf]=[16.3,45.6]% ROI=0.45 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-28T06:00:16]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.32MB / last modified 2026-06-28T14:00:07.969506+09:00

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
:19,006 [INFO] scraper: odds3t: 120/120 parsed
2026-06-28 13:58:20,094 [INFO] scraper: odds3f: 20/20 parsed
2026-06-28 13:58:21,192 [INFO] scraper: odds2t: 30/30 parsed
2026-06-28 13:58:21,193 [INFO] scraper: odds2f: 15/15 parsed
2026-06-28 13:58:22,263 [INFO] scraper: odds_win: 5/6 parsed
2026-06-28 13:58:22,263 [INFO] scraper: fetch_race 05/6: boats=6 odds=190/191
2026-06-28 13:58:22,275 [INFO] predictor: CALIBRATION_MODE=on
2026-06-28 13:58:22,275 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-06-28 13:58:22,283 [INFO] run_cycle: fetched 05/6 [scan]: 155 combos
2026-06-28 13:58:22,817 [INFO] race_id: notif: nid=2026062805061404 sid=S01_NAKAANA1 phase=scan rank=B
2026-06-28 13:58:23,140 [INFO] notifier: Discord notify OK (status=204)
2026-06-28 13:58:23,572 [INFO] notifier: Discord notify OK (status=204)
2026-06-28 13:58:23,686 [INFO] run_cycle: SCAN S01_NAKAANA1 多摩川6R B
2026-06-28 13:58:24,068 [INFO] run_cycle: run_cycle done: 1 notifications
2026-06-28 13:59:07,476 [INFO] run_cycle: === run_cycle 13:59:07 ===
2026-06-28 13:59:07,476 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 13:59:07,476 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 13:59:07,525 [INFO] predictor: Models loaded OK
2026-06-28 13:59:18,973 [INFO] scraper: odds3t: 120/120 parsed
2026-06-28 13:59:20,068 [INFO] scraper: odds3f: 20/20 parsed
2026-06-28 13:59:21,142 [INFO] scraper: odds2t: 30/30 parsed
2026-06-28 13:59:21,143 [INFO] scraper: odds2f: 15/15 parsed
2026-06-28 13:59:22,269 [INFO] scraper: odds_win: 6/6 parsed
2026-06-28 13:59:22,270 [INFO] scraper: fetch_race 10/12: boats=6 odds=191/191
2026-06-28 13:59:22,286 [INFO] predictor: CALIBRATION_MODE=on
2026-06-28 13:59:22,287 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-28 13:59:22,298 [INFO] run_cycle: fetched 10/12 [final]: 156 combos
2026-06-28 13:59:22,757 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 80
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 80
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 14, 'scan': 36}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 153
  FINAL_MISSING: 92
  KS_ODDS_DRIFT: 54
  CIRCUIT_BREAKER_NO_ACTION: 27
  CIRCUIT_BREAKER_TRIP: 27
  PSI_DRIFT_DETECTED: 26
  ANOMALY_SCAN_FINAL_RATIO: 24
  CALIBRATION_DRIFT: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 10 | 14,100 | 7,650 | -6,450 | 0.543 |
| S01_NAKAANA1 | 32 | 12 | 6,400 | 6,120 | -280 | 0.956 |
| S02_TETSUBAN | 5 | 1 | 1,000 | 360 | -640 | 0.36 |

## 直近アラート (24h・新しい順)
```
[13:59:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1262}
[13:58:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1264}
[13:57:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1250}
[13:56:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1276}
[13:55:01] FINAL_MISSING: {"deadline": "2026-06-28T13:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062804041325", "sid": "S00"}
[13:55:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1263}
[13:53:30] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1257}
[13:52:37] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 7650, "roi_7d": 0.543, "sid": "S00"}
[13:52:37] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008642, "ks_stat": 0.201}
[13:52:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 292, "n_recent": 84, "psi": 0.265}
```

## 本日残レース: 105件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 87件 締切済
- 通知発射: scan=20 nid / final=20 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1011R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=3.3 drift=-3.0% | 13:23:28 |
| S00 | 054R | win | 1 | 0.5701 | 15.9 | 9.06 | 300 | scan=25.0 drift=-36.4% | 13:00:43 |
| S02_TETSUBAN | 034R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 12:33:20 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.3 drift=-9.1% | 12:21:30 |
| S01_NAKAANA1 | 174R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=3.1 drift=+0.0% | 12:18:21 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.6 drift=-6.5% | 11:55:33 |
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 11:47:20 |
| S01_NAKAANA1 | 093R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=- drift=- | 11:33:31 |
| S00 | 172R | win | 1 | 0.4989 | 5.3 | 2.64 | 300 | scan=16.5 drift=-67.9% | 11:22:21 |
| S01_NAKAANA1 | 213R | win | 1 | 0.5534 | 4.5 | 2.49 | 200 | scan=3.3 drift=+36.4% | 09:21:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +26.7% | -67.9% | +482.2% | 16 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 461.5s |
| **Latency** (scan→final max) | 652.5s |
| **Traffic** (notifications 24h) | 80 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 376 | 0.4789 | 0.2899 | +0.1890 | 🟡+40% | 0.2409 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 163 | 0.4390 | 0.2699 | 0.2255 | 🔴-0.14 | 0.703 |
| S01_NAKAANA1 | win | 139 | 0.4912 | 0.3094 | 0.2434 | 🔴-0.14 | 0.814 |
| S02_TETSUBAN | win | 74 | 0.5436 | 0.2973 | 0.2703 | 🔴-0.29 | 0.47 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 127 | 0.4255 | 0.2362 | 🔴+0.1892 |
| 0.50+ | 223 | 0.5439 | 0.3363 | 🔴+0.2075 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 47 | 0.736 |
| win | <5.0 | ✅learned | 102 | 0.725 |
| win | <10.0 | ✅learned | 59 | 0.493 |
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
_auto-generated by claude_snapshot.py at 2026-06-28T14:00:02.084654+09:00_