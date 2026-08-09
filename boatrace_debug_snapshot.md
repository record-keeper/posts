# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-09T16:00:01.891328+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×71 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×49 (24h)
- 🔴 PSI_DRIFT_DETECTED×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×16  [2026-08-09T15:44:04]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-09T15:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-09T15:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×110  [2026-08-09T15:05:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×110  [2026-08-09T15:05:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×55  [2026-08-09T15:05:33]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×55  [2026-08-09T15:05:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×48  [2026-08-09T14:40:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×30  [2026-08-09T12:45:36]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

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
- DB: 9.92MB / last modified 2026-08-09T16:00:04.435642+09:00

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
5000
2026-08-09 15:58:03,586 [INFO] predictor: Models loaded OK
2026-08-09 15:58:14,631 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=12&hd=20260809: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-09 15:58:25,993 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 15:58:27,096 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 15:58:28,247 [INFO] scraper: odds2t: 29/30 parsed
2026-08-09 15:58:28,249 [INFO] scraper: odds2f: 15/15 parsed
2026-08-09 15:58:29,329 [INFO] scraper: odds_win: 6/6 parsed
2026-08-09 15:58:29,329 [INFO] scraper: fetch_race 12/3: boats=6 odds=190/191
2026-08-09 15:58:29,333 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 15:58:29,333 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-08-09 15:58:29,337 [INFO] run_cycle: fetched 12/3 [scan]: 155 combos
2026-08-09 15:58:32,877 [INFO] scraper: odds3t: 120/120 parsed
2026-08-09 15:58:33,989 [INFO] scraper: odds3f: 20/20 parsed
2026-08-09 15:58:35,094 [INFO] scraper: odds2t: 26/30 parsed
2026-08-09 15:58:35,095 [INFO] scraper: odds2f: 12/15 parsed
2026-08-09 15:58:36,199 [INFO] scraper: odds_win: 3/6 parsed
2026-08-09 15:58:36,199 [INFO] scraper: fetch_race 16/11: boats=6 odds=181/191
2026-08-09 15:58:36,202 [INFO] predictor: CALIBRATION_MODE=on
2026-08-09 15:58:36,202 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-08-09 15:58:36,207 [INFO] run_cycle: fetched 16/11 [scan]: 149 combos
2026-08-09 15:58:36,340 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-09 15:59:04,026 [INFO] run_cycle: === run_cycle 15:59:04 ===
2026-08-09 15:59:04,026 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-09 15:59:04,026 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-09 15:59:04,072 [INFO] predictor: Models loaded OK
2026-08-09 15:59:04,341 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 114
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 114
  }
]
```

## Phase別通知記録 (24h)
{'final': 42, 'result': 22, 'scan': 50}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 223
  FINAL_MISSING: 71
  CIRCUIT_BREAKER_TRIP: 49
  PSI_DRIFT_DETECTED: 45
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_BET_VOLUME_SPIKE: 19
  ANOMALY_SCAN_FINAL_RATIO: 19
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 5 | 9,300 | 4,440 | -4,860 | 0.477 |
| S01_NAKAANA1 | 44 | 8 | 8,800 | 4,120 | -4,680 | 0.468 |
| S02_TETSUBAN | 12 | 7 | 2,400 | 2,280 | -120 | 0.95 |

## 直近アラート (24h・新しい順)
```
[15:56:23] CIRCUIT_BREAKER_TRIP: {"cost": 9300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 4440, "roi_7d": 0.477, "sid": "S00"}
[15:56:23] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 322, "n_recent": 87, "psi": 0.29}
[15:56:23] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.1, "baseline_n_days": 7, "baseline_stdev": 1.6, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 22, "z_score": 8.81}
[15:55:22] FINAL_MISSING: {"deadline": "2026-08-09T11:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080916021123", "sid": "S00"}
[15:48:25] FINAL_MISSING: {"deadline": "2026-08-09T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080902021116", "sid": "S00"}
[15:46:36] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 4120, "roi_7d": 0.468, "sid": "S01_NAKAANA1"}
[15:46:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 322, "n_recent": 86, "psi": 0.307}
[15:46:36] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.1, "baseline_n_days": 7, "baseline_stdev": 1.6, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 21, "z_score": 8.17}
[15:44:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 322, "n_recent": 85, "psi": 0.303}
[15:37:31] FINAL_MISSING: {"deadline": "2026-08-09T15:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080905081507", "sid": "S00"}
```

## 本日残レース: 50件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 118件 締切済
- 通知発射: scan=35 nid / final=31 nid / result=18 nid
- predictions: 22 / うち結果DB記録済: 19
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 12件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 202R | win | 1 | 0.4111 | 5.1 | 2.10 | 300 | scan=5.0 drift=+2.0% | 15:56:18 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5109 | 3.4 | 1.74 | 200 | scan=4.1 drift=-17.1% | 15:46:21 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 15:31:18 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.8 drift=-17.9% | 15:19:24 |
| S01_NAKAANA1 | 0210R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=4.9 drift=-2.0% | 15:18:24 |
| S01_NAKAANA1 | 057R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=- drift=- | 14:32:39 |
| S01_NAKAANA1 | 036R | win | 1 | 0.5735 | 4.5 | 2.58 | 200 | scan=4.1 drift=+9.8% | 13:26:20 |
| S00 | 036R | win | 1 | 0.5735 | 4.5 | 2.58 | 300 | scan=4.1 drift=+9.8% | 13:26:18 |
| S00 | 2310R | win | 1 | 0.5719 | 5.0 | 2.86 | 300 | scan=10.7 drift=-53.3% | 13:17:19 |
| S01_NAKAANA1 | 054R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=3.0 drift=+3.3% | 13:00:46 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | -3.0% | -73.3% | +112.5% | 20 | 10 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.8s |
| **Latency** (scan→final max) | 605.5s |
| **Traffic** (notifications 24h) | 114 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 2,400円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 406 | 0.4600 | 0.2833 | +0.1767 | 🟡+38% | 0.2348 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4103 | 0.2414 | 0.2214 | 🔴-0.21 | 0.695 |
| S01_NAKAANA1 | win | 167 | 0.4840 | 0.2395 | 0.2449 | 🔴-0.34 | 0.708 |
| S02_TETSUBAN | win | 65 | 0.5314 | 0.5077 | 0.2445 | ✅+0.02 | 0.958 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 156 | 0.4167 | 0.2115 | 🔴+0.2052 |
| 0.50+ | 213 | 0.5423 | 0.3474 | 🔴+0.1949 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 100 | 0.784 |
| win | <5.0 | ✅learned | 176 | 0.72 |
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
_auto-generated by claude_snapshot.py at 2026-08-09T16:00:01.891328+09:00_