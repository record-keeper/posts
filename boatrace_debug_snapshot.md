# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-11T12:30:01.976425+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×69 (24h)
- 🔴 CALIBRATION_DRIFT×32 (24h)
- 🟡 FINAL_MISSING×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×25  [2026-06-11T12:05:54]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CALIBRATION_DRIFT  ×27  [2026-06-11T12:03:42]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×81  [2026-06-11T12:03:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×81  [2026-06-11T12:03:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-06-11T12:03:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-06-11T12:01:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-11T12:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-11T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-11T06:00:11]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S00: n=149 hit%=25.5% hit_CI[Bonf]=[16.7,36.9]% ROI=0.76 ROI_boot95=[0.50,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=149<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=28.3% hit_CI[Bonf]=[18.7,40.3]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-11T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=36.2% hit_CI[Bonf]=[22.7,52.4]% ROI=0.61 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-11T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-11T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=32.4% ROI=0.89 (コスト 10,000/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.81MB / last modified 2026-06-11T12:30:04.440167+09:00

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
2026-06-11 12:28:39,102 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-11 12:29:06,337 [INFO] run_cycle: === run_cycle 12:29:06 ===
2026-06-11 12:29:06,337 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-11 12:29:06,337 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-11 12:29:06,379 [INFO] predictor: Models loaded OK
2026-06-11 12:29:18,958 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 12:29:20,077 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 12:29:21,155 [INFO] scraper: odds2t: 30/30 parsed
2026-06-11 12:29:21,156 [INFO] scraper: odds2f: 15/15 parsed
2026-06-11 12:29:22,230 [INFO] scraper: odds_win: 4/6 parsed
2026-06-11 12:29:22,230 [INFO] scraper: fetch_race 05/3: boats=6 odds=189/191
2026-06-11 12:29:22,243 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 12:29:22,243 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-11 12:29:22,250 [INFO] run_cycle: fetched 05/3 [final]: 154 combos
2026-06-11 12:29:22,324 [INFO] race_id: notif: nid=2026061105031232 sid=S00 phase=final rank=SS
2026-06-11 12:29:22,670 [INFO] notifier: Discord notify OK (status=204)
2026-06-11 12:29:22,992 [INFO] notifier: Discord notify OK (status=204)
2026-06-11 12:29:23,136 [INFO] run_cycle: FINAL S00 多摩川3R SS
2026-06-11 12:29:27,200 [INFO] scraper: odds3t: 120/120 parsed
2026-06-11 12:29:28,314 [INFO] scraper: odds3f: 20/20 parsed
2026-06-11 12:29:29,447 [INFO] scraper: odds2t: 28/30 parsed
2026-06-11 12:29:29,448 [INFO] scraper: odds2f: 14/15 parsed
2026-06-11 12:29:30,526 [INFO] scraper: odds_win: 3/6 parsed
2026-06-11 12:29:30,526 [INFO] scraper: fetch_race 09/5: boats=6 odds=185/191
2026-06-11 12:29:30,536 [INFO] predictor: CALIBRATION_MODE=on
2026-06-11 12:29:30,536 [INFO] predictor: combos: {'win': 3, '2t': 28, '3t': 120}
2026-06-11 12:29:30,544 [INFO] run_cycle: fetched 09/5 [scan]: 151 combos
2026-06-11 12:29:30,692 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 15, 'scan': 26}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_TRIP: 69
  ANOMALY_SCRAPER_FAILURE_BURST: 55
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 32
  FINAL_MISSING: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_SPIKE: 4
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 9 | 12,000 | 7,200 | -4,800 | 0.6 |
| S01_NAKAANA1 | 33 | 8 | 6,600 | 3,780 | -2,820 | 0.573 |
| S02_TETSUBAN | 28 | 5 | 5,600 | 1,560 | -4,040 | 0.279 |

## 直近アラート (24h・新しい順)
```
[12:29:30] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 7200, "roi_7d": 0.6, "sid": "S00"}
[12:29:30] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.9, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 13, "z_score": 3.48}
[12:25:41] CALIBRATION_DRIFT: {"avg_actual": 0.2292, "avg_pred": 0.4884, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 53.1}
[12:23:42] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 7200, "roi_7d": 0.615, "sid": "S00"}
[12:23:42] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.9, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 12, "z_score": 3.05}
[12:18:33] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 1560, "roi_7d": 0.279, "sid": "S02_TETSUBAN"}
[12:18:33] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.9, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 11, "z_score": 2.63}
[12:05:54] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 3780, "roi_7d": 0.573, "sid": "S01_NAKAANA1"}
[12:05:54] CALIBRATION_DRIFT: {"avg_actual": 0.2316, "avg_pred": 0.492, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 95, "overconf_pct": 52.9}
[12:05:54] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.9, "baseline_n_days": 7, "baseline_stdev": 2.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 10, "z_score": 2.2}
```

## 本日残レース: 96件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 48件 締切済
- 通知発射: scan=15 nid / final=16 nid / result=7 nid
- predictions: 13 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 053R | win | 1 | 0.4111 | 9.4 | 3.86 | 300 | scan=15.8 drift=-40.5% | 12:29:22 |
| S00 | 239R | win | 1 | 0.4920 | 6.0 | 2.95 | 300 | scan=- drift=- | 12:23:32 |
| S02_TETSUBAN | 164R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.2 drift=+0.0% | 12:18:31 |
| S01_NAKAANA1 | 094R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=4.2 drift=-23.8% | 12:05:46 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 12:03:32 |
| S00 | 114R | win | 1 | 0.1543 | 5.6 | 0.86 | 300 | scan=5.6 drift=+0.0% | 11:52:32 |
| S00 | 093R | win | 1 | 0.2292 | 4.1 | 0.94 | 300 | scan=- drift=- | 11:33:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 200 | scan=- drift=- | 11:30:25 |
| S00 | 051R | win | 1 | 0.5990 | 4.8 | 2.88 | 300 | scan=7.3 drift=-34.2% | 11:30:25 |
| S01_NAKAANA1 | 031R | win | 1 | 0.5334 | 4.8 | 2.56 | 200 | scan=3.9 drift=+23.1% | 11:11:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +6.6% | -62.9% | +274.6% | 19 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.3s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 369 | 0.4690 | 0.2900 | +0.1790 | 🟡+38% | 0.2364 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 151 | 0.4194 | 0.2649 | 0.2168 | 🔴-0.11 | 0.79 |
| S01_NAKAANA1 | win | 138 | 0.4881 | 0.2826 | 0.2428 | 🔴-0.20 | 0.721 |
| S02_TETSUBAN | win | 80 | 0.5296 | 0.3500 | 0.2625 | 🔴-0.15 | 0.595 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 6 | 0.2236 | 0.3333 | 🔴-0.1097 |
| 0.30-0.50 | 138 | 0.4197 | 0.2246 | 🔴+0.1951 |
| 0.50+ | 206 | 0.5421 | 0.3495 | 🔴+0.1926 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 35 | 0.736 |
| win | <5.0 | ✅learned | 68 | 0.722 |
| win | <10.0 | ✅learned | 42 | 0.51 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-11T12:30:01.976425+09:00_