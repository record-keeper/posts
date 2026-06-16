# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-17T04:00:03.354039+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 PSI_DRIFT_DETECTED×29 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-17T03:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×19  [2026-06-16T23:41:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×52  [2026-06-16T23:08:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-06-16T23:08:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×8  [2026-06-16T20:05:19]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×38  [2026-06-16T18:10:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-16T16:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-06-16T15:05:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-06-16T11:27:50]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=29.1% hit_CI[Bonf]=[19.3,41.4]% ROI=0.86 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=79 hit%=35.4% hit_CI[Bonf]=[22.0,51.7]% ROI=0.58 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=16.1% ROI=0.28 (コスト 6,800/回収 1,900)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-16T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=29 hit%=20.7% ROI=0.48 (コスト 8,000/回収 3,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-16T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=79 pred=0.5344 hit=0.3544 cal_err=+0.1800 brier=0.2647 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-16T06:00:12]
- key: `ROI_STAT|S00: n=143 hit%=28.0% hit_CI[Bonf]=[18.6,39.8]% ROI=0.86 ROI_boot95=[0.60,1.16]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-16T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=143<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.2MB / last modified 2026-06-17T04:00:03.882550+09:00

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
00 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 23:55:06,700 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 23:55:06,742 [INFO] predictor: Models loaded OK
2026-06-16 23:55:06,748 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-16 23:56:05,977 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-06-16 23:56:05,978 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 23:56:05,978 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 23:56:06,067 [INFO] predictor: Models loaded OK
2026-06-16 23:56:06,180 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-16 23:57:06,567 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-06-16 23:57:06,568 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 23:57:06,568 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 23:57:06,639 [INFO] predictor: Models loaded OK
2026-06-16 23:57:06,644 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-16 23:58:06,411 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-06-16 23:58:06,411 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 23:58:06,411 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 23:58:06,462 [INFO] predictor: Models loaded OK
2026-06-16 23:58:06,464 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-16 23:59:06,562 [INFO] run_cycle: === run_cycle 23:59:06 ===
2026-06-16 23:59:06,562 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-16 23:59:06,562 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-16 23:59:06,606 [INFO] predictor: Models loaded OK
2026-06-16 23:59:06,612 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 39
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 39
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 7, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 132
  FINAL_MISSING: 48
  PSI_DRIFT_DETECTED: 29
  CIRCUIT_BREAKER_TRIP: 18
  ANOMALY_SCAN_FINAL_RATIO: 17
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 12 | 9,900 | 11,340 | +1,440 | 1.145 |
| S01_NAKAANA1 | 25 | 11 | 5,000 | 7,380 | +2,380 | 1.476 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 2,460 | -1,340 | 0.647 |

## 直近アラート (24h・新しい順)
```
[23:49:06] FINAL_MISSING: {"deadline": "2026-06-16T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061609061311", "sid": "S00"}
[23:44:06] FINAL_MISSING: {"deadline": "2026-06-16T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061609041209", "sid": "S00"}
[23:41:06] FINAL_MISSING: {"deadline": "2026-06-16T11:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061608021103", "sid": "S00"}
[23:27:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 275, "n_recent": 77, "psi": 0.365}
[23:08:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:08:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[23:00:10] FINAL_MISSING: {"deadline": "2026-06-16T11:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061610071122", "sid": "S01_NAKAANA1"}
[22:48:06] FINAL_MISSING: {"deadline": "2026-06-16T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061609061311", "sid": "S00"}
[22:44:05] FINAL_MISSING: {"deadline": "2026-06-16T12:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061609041209", "sid": "S00"}
[22:40:10] FINAL_MISSING: {"deadline": "2026-06-16T11:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061608021103", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 1612R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 16:47:23 |
| S00 | 098R | win | 1 | 0.4111 | 11.6 | 4.77 | 300 | scan=15.7 drift=-26.1% | 14:11:21 |
| S00 | 097R | win | 1 | 0.3177 | 4.1 | 1.30 | 300 | scan=- drift=- | 13:39:45 |
| S00 | 062R | win | 1 | 0.4111 | 5.8 | 2.38 | 300 | scan=- drift=- | 11:57:22 |
| S02_TETSUBAN | 032R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=2.3 drift=+21.7% | 11:38:33 |
| S00 | 186R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=27.7 drift=-58.5% | 10:55:34 |
| S01_NAKAANA1 | 103R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 09:28:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 200 | scan=3.7 drift=+29.7% | 15:54:23 |
| S00 | 012R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=4.5 drift=+6.7% | 15:54:21 |
| S01_NAKAANA1 | 224R | win | 1 | 0.5476 | 3.1 | 1.70 | 200 | scan=3.9 drift=-20.5% | 13:54:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | -6.3% | -82.9% | +87.5% | 18 | 10 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 500.2s |
| **Latency** (scan→final max) | 664.8s |
| **Traffic** (notifications 24h) | 39 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 352 | 0.4710 | 0.3040 | +0.1670 | 🟡+36% | 0.2383 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 143 | 0.4228 | 0.2727 | 0.2182 | 🔴-0.10 | 0.841 |
| S01_NAKAANA1 | win | 131 | 0.4850 | 0.2977 | 0.2450 | 🔴-0.17 | 0.856 |
| S02_TETSUBAN | win | 78 | 0.5358 | 0.3718 | 0.2641 | 🔴-0.13 | 0.601 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 8 | 0.2250 | 0.1250 | 🔴+0.1000 |
| 0.30-0.50 | 124 | 0.4177 | 0.2500 | 🔴+0.1677 |
| 0.50+ | 204 | 0.5410 | 0.3578 | 🔴+0.1832 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 43 | 0.717 |
| win | <5.0 | ✅learned | 78 | 0.755 |
| win | <10.0 | ✅learned | 51 | 0.498 |
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
_auto-generated by claude_snapshot.py at 2026-06-17T04:00:03.354039+09:00_