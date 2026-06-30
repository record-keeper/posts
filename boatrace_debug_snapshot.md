# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-30T20:50:01.871709+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×12 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×28  [2026-06-30T20:22:23]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×43  [2026-06-30T20:07:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×43  [2026-06-30T20:07:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×43  [2026-06-30T20:07:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-30T20:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-30T20:00:08]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-06-30T19:41:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-30T13:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-06-30T12:08:55]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-30T06:00:44]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-30T06:00:44]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-30T06:00:44]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S00: n=160 hit%=26.9% hit_CI[Bonf]=[18.1,38.0]% ROI=0.72 ROI_boot95=[0.52,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=31.2% hit_CI[Bonf]=[21.1,43.3]% ROI=0.84 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-30T06:00:44]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=31.2% hit_CI[Bonf]=[18.4,47.6]% ROI=0.48 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=24.3% ROI=0.78 (コスト 10,700/回収 8,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=24.4% ROI=0.58 (コスト 9,700/回収 5,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-30T06:00:44]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=28.9% ROI=0.73 (コスト 19,400/回収 14,180)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.49MB / last modified 2026-06-30T20:49:12.857922+09:00

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
ault=5000
2026-06-30 20:46:06,920 [INFO] predictor: Models loaded OK
2026-06-30 20:46:06,925 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-30 20:47:06,658 [INFO] run_cycle: === run_cycle 20:47:06 ===
2026-06-30 20:47:06,658 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-30 20:47:06,658 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-30 20:47:06,707 [INFO] predictor: Models loaded OK
2026-06-30 20:47:18,279 [INFO] scraper: odds3t: 120/120 parsed
2026-06-30 20:47:19,355 [INFO] scraper: odds3f: 20/20 parsed
2026-06-30 20:47:20,440 [INFO] scraper: odds2t: 30/30 parsed
2026-06-30 20:47:20,441 [INFO] scraper: odds2f: 14/15 parsed
2026-06-30 20:47:21,556 [INFO] scraper: odds_win: 3/6 parsed
2026-06-30 20:47:21,556 [INFO] scraper: fetch_race 20/8: boats=6 odds=187/191
2026-06-30 20:47:21,568 [INFO] predictor: CALIBRATION_MODE=on
2026-06-30 20:47:21,568 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-30 20:47:21,575 [INFO] run_cycle: fetched 20/8 [scan]: 153 combos
2026-06-30 20:47:21,714 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-30 20:48:06,583 [INFO] run_cycle: === run_cycle 20:48:06 ===
2026-06-30 20:48:06,583 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-30 20:48:06,585 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-30 20:48:06,666 [INFO] predictor: Models loaded OK
2026-06-30 20:48:06,907 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-30 20:49:06,717 [INFO] run_cycle: === run_cycle 20:49:06 ===
2026-06-30 20:49:06,718 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-30 20:49:06,718 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-30 20:49:06,774 [INFO] predictor: Models loaded OK
2026-06-30 20:49:06,878 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 10, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 258
  FINAL_MISSING: 47
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 12
  ANOMALY_SCAN_FINAL_RATIO: 7
  ANOMALY_BET_VOLUME_SPIKE: 3
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 7,590 | -5,310 | 0.588 |
| S01_NAKAANA1 | 38 | 16 | 7,600 | 7,580 | -20 | 0.997 |
| S02_TETSUBAN | 9 | 3 | 1,800 | 800 | -1,000 | 0.444 |

## 直近アラート (24h・新しい順)
```
[20:49:06] FINAL_MISSING: {"deadline": "2026-06-30T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026063002061314", "sid": "S00"}
[20:41:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 681}
[20:40:09] FINAL_MISSING: {"deadline": "2026-06-30T10:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026063023041002", "sid": "S00"}
[20:39:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 705}
[20:38:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 700}
[20:37:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 714}
[20:36:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 709}
[20:35:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 701}
[20:34:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 697}
[20:33:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 708}
```

## 本日残レース: 5件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 163件 締切済
- 通知発射: scan=22 nid / final=21 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 204R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 19:00:26 |
| S00 | 197R | win | 1 | 0.4989 | 6.3 | 3.14 | 300 | scan=- drift=- | 18:18:22 |
| S00 | 089R | win | 1 | 0.5476 | 7.5 | 4.11 | 300 | scan=6.7 drift=+11.9% | 14:29:33 |
| S00 | 177R | win | 1 | 0.3177 | 4.7 | 1.49 | 300 | scan=- drift=- | 13:53:21 |
| S00 | 054R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=4.5 drift=-4.4% | 13:00:38 |
| S00 | 064R | win | 1 | 0.4111 | 35.6 | 14.64 | 300 | scan=5.2 drift=+584.6% | 12:58:23 |
| S00 | 1010R | win | 1 | 0.5990 | 4.7 | 2.82 | 300 | scan=12.0 drift=-60.8% | 12:45:24 |
| S00 | 084R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=- drift=- | 12:06:21 |
| S01_NAKAANA1 | 021R | win | 1 | 0.5891 | 4.1 | 2.42 | 200 | scan=4.2 drift=-2.4% | 10:44:21 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5476 | 4.2 | 2.30 | 200 | scan=4.0 drift=+5.0% | 10:41:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +7.6% | -68.9% | +584.6% | 23 | 13 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 525.2s |
| **Latency** (scan→final max) | 649.9s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 369 | 0.4819 | 0.2927 | +0.1892 | 🟡+39% | 0.2395 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4422 | 0.2687 | 0.2234 | 🔴-0.14 | 0.721 |
| S01_NAKAANA1 | win | 137 | 0.4953 | 0.3139 | 0.2436 | 🔴-0.13 | 0.831 |
| S02_TETSUBAN | win | 72 | 0.5448 | 0.3056 | 0.2673 | 🔴-0.26 | 0.465 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2269 | 0.0909 | 🔴+0.1360 |
| 0.30-0.50 | 122 | 0.4247 | 0.2459 | 🔴+0.1788 |
| 0.50+ | 223 | 0.5448 | 0.3318 | 🔴+0.2130 |

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
_auto-generated by claude_snapshot.py at 2026-06-30T20:50:01.871709+09:00_