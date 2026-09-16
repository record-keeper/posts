# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-16T12:40:01.586541+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×67 (24h)
- 🔴 PSI_DRIFT_DETECTED×45 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×44 (24h)
- 🔴 CALIBRATION_DRIFT×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-09-16T12:31:11]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-09-16T12:20:53]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🔴 CALIBRATION_DRIFT  ×28  [2026-09-16T12:04:44]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×64  [2026-09-16T12:04:44]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×64  [2026-09-16T12:04:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×32  [2026-09-16T12:04:44]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×32  [2026-09-16T12:04:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-16T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_ODDS_SHIFT  ×28  [2026-09-16T10:52:37]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-16T10:44:52]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-16T06:00:12]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=173<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2214 actual=0.0000 gap=+0.2214`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S00: n=173 hit%=27.2% hit_CI[Bonf]=[18.6,37.8]% ROI=0.94 ROI_boot95=[0.66,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-16T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=174 hit%=24.7% hit_CI[Bonf]=[16.6,35.2]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.37MB / last modified 2026-09-16T12:39:06.356639+09:00

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
ed
2026-09-16 12:38:49,754 [INFO] scraper: odds2f: 13/15 parsed
2026-09-16 12:38:50,867 [INFO] scraper: odds_win: 5/6 parsed
2026-09-16 12:38:50,867 [INFO] scraper: fetch_race 22/3: boats=6 odds=186/191
2026-09-16 12:38:50,870 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 12:38:50,870 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-16 12:38:50,874 [INFO] run_cycle: fetched 22/3 [scan]: 155 combos
2026-09-16 12:38:54,444 [INFO] scraper: odds3t: 120/120 parsed
2026-09-16 12:38:55,556 [INFO] scraper: odds3f: 20/20 parsed
2026-09-16 12:38:56,666 [INFO] scraper: odds2t: 27/30 parsed
2026-09-16 12:38:56,667 [INFO] scraper: odds2f: 15/15 parsed
2026-09-16 12:38:57,747 [INFO] scraper: odds_win: 3/6 parsed
2026-09-16 12:38:57,747 [INFO] scraper: fetch_race 11/6: boats=6 odds=185/191
2026-09-16 12:38:57,750 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 12:38:57,750 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-09-16 12:38:57,753 [INFO] run_cycle: fetched 11/6 [scan]: 150 combos
2026-09-16 12:39:01,378 [INFO] scraper: odds3t: 120/120 parsed
2026-09-16 12:39:02,591 [INFO] scraper: odds3f: 20/20 parsed
2026-09-16 12:39:03,709 [INFO] scraper: odds2t: 27/30 parsed
2026-09-16 12:39:03,710 [INFO] scraper: odds2f: 12/15 parsed
2026-09-16 12:39:04,812 [INFO] scraper: odds_win: 5/6 parsed
2026-09-16 12:39:04,813 [INFO] scraper: fetch_race 04/5: boats=6 odds=184/191
2026-09-16 12:39:04,815 [INFO] predictor: CALIBRATION_MODE=on
2026-09-16 12:39:04,815 [INFO] predictor: combos: {'win': 5, '2t': 27, '3t': 120}
2026-09-16 12:39:04,819 [INFO] run_cycle: fetched 04/5 [scan]: 152 combos
2026-09-16 12:39:04,896 [INFO] race_id: notif: nid=2026091604051251 sid=S00 phase=scan rank=SS
2026-09-16 12:39:05,531 [INFO] notifier: Discord notify OK (status=204)
2026-09-16 12:39:05,955 [INFO] notifier: Discord notify OK (status=204)
2026-09-16 12:39:05,980 [INFO] run_cycle: SCAN S00 平和島5R SS
2026-09-16 12:39:06,154 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 76
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 76
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 15, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 67
  PSI_DRIFT_DETECTED: 45
  CIRCUIT_BREAKER_TRIP: 44
  ANOMALY_SCRAPER_FAILURE_BURST: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  CALIBRATION_DRIFT: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_ODDS_SHIFT: 2
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 7 | 10,200 | 6,420 | -3,780 | 0.629 |
| S01_NAKAANA1 | 35 | 8 | 7,000 | 4,440 | -2,560 | 0.634 |
| S02_TETSUBAN | 16 | 5 | 3,200 | 1,360 | -1,840 | 0.425 |

## 直近アラート (24h・新しい順)
```
[12:39:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1145}
[12:37:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1126}
[12:36:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1146}
[12:34:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1141}
[12:32:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1142}
[12:31:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1169}
[12:26:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 348, "n_recent": 85, "psi": 0.667}
[12:20:52] CALIBRATION_DRIFT: {"avg_actual": 0.2381, "avg_pred": 0.4845, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 84, "overconf_pct": 50.9}
[12:20:52] SEND_WITHOUT_DBREC: {"kind": "SEND_WITHOUT_DBREC", "nid": "2026091611041149", "phase": "result", "sid": "S02_TETSUBAN"}
[12:18:42] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 6420, "roi_7d": 0.629, "sid": "S00"}
```

## 本日残レース: 102件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 54件 締切済
- 通知発射: scan=9 nid / final=10 nid / result=6 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 222R | win | 1 | 0.5123 | 9.0 | 4.61 | 300 | scan=4.1 drift=+119.5% | 12:11:20 |
| S02_TETSUBAN | 114R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 11:47:18 |
| S00 | 114R | win | 1 | 0.5334 | 9.0 | 4.80 | 300 | scan=6.7 drift=+34.3% | 11:46:18 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5174 | 4.2 | 2.17 | 200 | scan=4.0 drift=+5.0% | 11:21:08 |
| S00 | 042R | win | 1 | 0.5174 | 4.2 | 2.17 | 300 | scan=4.0 drift=+5.0% | 11:20:28 |
| S00 | 113R | win | 1 | 0.0644 | 10.5 | 0.68 | 300 | scan=- drift=- | 11:18:24 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4978 | 3.2 | 1.59 | 200 | scan=- drift=- | 10:52:27 |
| S00 | 112R | win | 1 | 0.4111 | 23.2 | 9.54 | 300 | scan=- drift=- | 10:51:19 |
| S00 | 111R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=4.5 drift=+0.0% | 10:26:27 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=4.2 drift=+4.8% | 17:05:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +7.1% | -80.2% | +119.5% | 11 | 3 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.3s |
| **Latency** (scan→final max) | 613.6s |
| **Traffic** (notifications 24h) | 76 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 432 | 0.4754 | 0.2708 | +0.2045 | 🟡+43% | 0.2431 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4338 | 0.2670 | 0.2278 | 🔴-0.16 | 0.943 |
| S01_NAKAANA1 | win | 175 | 0.4846 | 0.2457 | 0.2477 | 🔴-0.34 | 0.754 |
| S02_TETSUBAN | win | 81 | 0.5457 | 0.3333 | 0.2667 | 🔴-0.20 | 0.595 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 154 | 0.4051 | 0.2273 | 🔴+0.1778 |
| 0.50+ | 255 | 0.5462 | 0.3059 | 🔴+0.2403 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 250 | 0.753 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 32 | 0.24 |
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
_auto-generated by claude_snapshot.py at 2026-09-16T12:40:01.586541+09:00_