# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-09T13:00:02.254367+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×49 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×47 (24h)
- 🔴 PSI_DRIFT_DETECTED×39 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-08-09T12:51:04]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-08-09T12:45:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×16  [2026-08-09T12:43:04]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-09T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-09T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×52  [2026-08-09T12:04:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×106  [2026-08-09T12:03:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×106  [2026-08-09T12:03:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×53  [2026-08-09T12:03:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ORPHAN_SCAN  ×1  [2026-08-09T06:00:14]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=159<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=12 pred=0.1229 actual=0.1667 gap=-0.0438`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-09T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2237 actual=0.3636 gap=-0.1399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.70 ROI_boot95=[0.49,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=159 hit%=24.5% hit_CI[Bonf]=[16.1,35.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-09T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=64 hit%=51.6% hit_CI[Bonf]=[34.4,68.3]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-09T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=64<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-09T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.63 (コスト 10,000/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.85MB / last modified 2026-08-09T13:00:04.339347+09:00

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
44,167 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-09 12:59:03,836 [INFO] run_cycle: === run_cycle 12:59:03 ===
2026-08-09 12:59:03,836 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-09 12:59:03,836 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-09 12:59:03,875 [INFO] predictor: Models loaded OK
2026-08-09 12:59:16,287 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 12:59:17,363 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 12:59:18,463 [INFO] scraper: odds2t: 30/30 parsed
2026-08-09 12:59:18,464 [INFO] scraper: odds2f: 15/15 parsed
2026-08-09 12:59:19,556 [INFO] scraper: odds_win: 6/6 parsed
2026-08-09 12:59:19,556 [INFO] scraper: fetch_race 03/5: boats=6 odds=191/191
2026-08-09 12:59:19,560 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 12:59:19,560 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-09 12:59:19,563 [INFO] run_cycle: fetched 03/5 [final]: 156 combos
2026-08-09 12:59:19,606 [INFO] race_id: notif: nid=2026080903051302 sid=S01_NAKAANA1 phase=final rank=B
2026-08-09 12:59:19,968 [INFO] notifier: Discord notify OK (status=204)
2026-08-09 12:59:20,614 [INFO] notifier: Discord notify OK (status=204)
2026-08-09 12:59:20,825 [INFO] run_cycle: FINAL S01_NAKAANA1 江戸川5R B
2026-08-09 12:59:24,247 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 12:59:25,325 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 12:59:26,431 [INFO] scraper: odds2t: 29/30 parsed
2026-08-09 12:59:26,432 [INFO] scraper: odds2f: 15/15 parsed
2026-08-09 12:59:27,524 [INFO] scraper: odds_win: 4/6 parsed
2026-08-09 12:59:27,524 [INFO] scraper: fetch_race 09/6: boats=6 odds=188/191
2026-08-09 12:59:27,527 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 12:59:27,527 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-08-09 12:59:27,530 [INFO] run_cycle: fetched 09/6 [final]: 153 combos
2026-08-09 12:59:27,819 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 84
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 84
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 17, 'scan': 38}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  FINAL_MISSING: 49
  CIRCUIT_BREAKER_TRIP: 47
  PSI_DRIFT_DETECTED: 39
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 8
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 5 | 8,700 | 4,170 | -4,530 | 0.479 |
| S01_NAKAANA1 | 39 | 7 | 7,800 | 3,720 | -4,080 | 0.477 |
| S02_TETSUBAN | 12 | 8 | 2,400 | 2,560 | +160 | 1.067 |

## 直近アラート (24h・新しい順)
```
[12:59:27] CIRCUIT_BREAKER_TRIP: {"cost": 7800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 3720, "roi_7d": 0.477, "sid": "S01_NAKAANA1"}
[12:59:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 324, "n_recent": 80, "psi": 0.284}
[12:59:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1162}
[12:59:27] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.137, "baseline_mean": 0.819, "baseline_stdev": 0.056, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.682, "today_scan_count": 22, "z_score": -2.44}
[12:59:27] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.4, "baseline_n_days": 7, "baseline_stdev": 1.1, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 12, "z_score": 6.68}
[12:58:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1141}
[12:55:34] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 324, "n_recent": 79, "psi": 0.302}
[12:54:19] FINAL_MISSING: {"deadline": "2026-08-09T11:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080916021123", "sid": "S00"}
[12:54:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1127}
[12:53:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1150}
```

## 本日残レース: 107件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 61件 締切済
- 通知発射: scan=22 nid / final=17 nid / result=9 nid
- predictions: 12 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 035R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.9 drift=-7.7% | 12:59:19 |
| S01_NAKAANA1 | 149R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.0 drift=+16.7% | 12:32:25 |
| S02_TETSUBAN | 053R | win | 1 | 0.5476 | 2.8 | 1.53 | 200 | scan=- drift=- | 12:30:20 |
| S02_TETSUBAN | 135R | win | 1 | 0.5735 | 2.6 | 1.49 | 200 | scan=2.2 drift=+18.2% | 12:24:19 |
| S00 | 238R | win | 1 | 0.4989 | 5.2 | 2.59 | 300 | scan=7.7 drift=-32.5% | 12:14:18 |
| S01_NAKAANA1 | 094R | win | 1 | 0.3177 | 3.2 | 1.02 | 200 | scan=- drift=- | 11:53:30 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=3.0 drift=+0.0% | 11:42:43 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5476 | 3.4 | 1.86 | 200 | scan=3.0 drift=+13.3% | 11:40:45 |
| S01_NAKAANA1 | 093R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.3 drift=+12.1% | 11:22:19 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=3.5 drift=-14.3% | 10:44:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | -2.5% | -73.3% | +112.5% | 18 | 9 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 415.0s |
| **Latency** (scan→final max) | 605.5s |
| **Traffic** (notifications 24h) | 84 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4587 | 0.2843 | +0.1745 | 🟡+38% | 0.2343 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4103 | 0.2400 | 0.2214 | 🔴-0.21 | 0.691 |
| S01_NAKAANA1 | win | 162 | 0.4830 | 0.2407 | 0.2450 | 🔴-0.34 | 0.717 |
| S02_TETSUBAN | win | 64 | 0.5300 | 0.5156 | 0.2424 | ✅+0.03 | 0.973 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 155 | 0.4167 | 0.2129 | 🔴+0.2038 |
| 0.50+ | 209 | 0.5413 | 0.3493 | 🔴+0.1920 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 100 | 0.784 |
| win | <5.0 | ✅learned | 174 | 0.723 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
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
_auto-generated by claude_snapshot.py at 2026-08-09T13:00:02.254367+09:00_