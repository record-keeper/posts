# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-15T16:10:01.628227+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×128 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-15T16:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CALIBRATION_DRIFT  ×5  [2026-11-15T15:51:42]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-15T15:30:16]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×13  [2026-11-15T15:16:49]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×13  [2026-11-15T15:16:49]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×13  [2026-11-15T15:16:49]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-15T15:12:00]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-15T15:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-15T14:00:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-15T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-15T11:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×18  [2026-11-15T10:01:27]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-15T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=49<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-15T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1901 actual=0.0000 gap=+0.1901`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-15T06:00:23]
- key: `ROI_STAT|S00: n=116 hit%=25.0% hit_CI[Bonf]=[15.3,38.0]% ROI=0.65 ROI_boot95=[0.42,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-15T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S00: n=116<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-15T06:00:23]
- key: `ROI_STAT|S01_NAKAANA1: n=128 hit%=28.9% hit_CI[Bonf]=[18.9,41.5]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-15T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=128<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-15T06:00:23]
- key: `ROI_STAT|S02_TETSUBAN: n=49 hit%=44.9% hit_CI[Bonf]=[26.7,64.6]% ROI=1.11 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-15T06:00:23]
- key: `ORPHAN_SCAN|226 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.12MB / last modified 2026-11-15T16:07:17.705502+09:00

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
ce/oddstf?rno=3&jcd=24&hd=20261115: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-15 16:07:14,585 [INFO] scraper: odds_win: 1/6 parsed
2026-11-15 16:07:14,585 [INFO] scraper: fetch_race 24/3: boats=6 odds=186/191
2026-11-15 16:07:14,587 [INFO] predictor: CALIBRATION_MODE=on
2026-11-15 16:07:14,587 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-11-15 16:07:14,591 [INFO] run_cycle: fetched 24/3 [scan]: 151 combos
2026-11-15 16:07:14,738 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-15 16:08:04,549 [INFO] run_cycle: === run_cycle 16:08:04 ===
2026-11-15 16:08:04,549 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-15 16:08:04,549 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-15 16:08:04,622 [INFO] predictor: Models loaded OK
2026-11-15 16:08:34,170 [INFO] scraper: odds3t: 120/120 parsed
2026-11-15 16:08:43,408 [INFO] scraper: odds3f: 20/20 parsed
2026-11-15 16:08:53,585 [INFO] scraper: odds2t: 30/30 parsed
2026-11-15 16:08:53,586 [INFO] scraper: odds2f: 15/15 parsed
2026-11-15 16:09:02,719 [INFO] scraper: odds_win: 6/6 parsed
2026-11-15 16:09:02,719 [INFO] scraper: fetch_race 11/12: boats=6 odds=191/191
2026-11-15 16:09:02,728 [INFO] predictor: CALIBRATION_MODE=on
2026-11-15 16:09:02,728 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-15 16:09:02,736 [INFO] run_cycle: fetched 11/12 [final]: 156 combos
2026-11-15 16:09:31,473 [INFO] scraper: odds3t: 120/120 parsed
2026-11-15 16:09:42,485 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=16&hd=20261115: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-15 16:09:52,761 [INFO] scraper: odds3f: 20/20 parsed
2026-11-15 16:10:02,855 [INFO] scraper: odds2t: 29/30 parsed
2026-11-15 16:10:02,856 [INFO] scraper: odds2f: 15/15 parsed

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
    "c": 37
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 37
  }
]
```

## Phase別通知記録 (24h)
{'final': 12, 'result': 7, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 195
  FINAL_MISSING: 128
  PSI_DRIFT_DETECTED: 38
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_DROP: 1
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 12 | 2 | 3,600 | 2,220 | -1,380 | 0.617 |
| S01_NAKAANA1 | 17 | 2 | 3,400 | 660 | -2,740 | 0.194 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 2,180 | +380 | 1.211 |

## 直近アラート (24h・新しい順)
```
[16:07:14] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 492}
[16:04:54] FINAL_MISSING: {"deadline": "2026-11-15T12:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111516041220", "sid": "S00"}
[16:04:54] FINAL_MISSING: {"deadline": "2026-11-15T11:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111511031128", "sid": "S02_TETSUBAN"}
[16:04:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 11, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[15:59:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 480}
[15:55:12] FINAL_MISSING: {"deadline": "2026-11-15T10:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111523041005", "sid": "S00"}
[15:55:12] FINAL_MISSING: {"deadline": "2026-11-15T13:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111508071318", "sid": "S00"}
[15:55:12] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 482}
[15:51:41] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 240, "n_recent": 38, "psi": 0.802}
[15:51:41] CALIBRATION_DRIFT: {"avg_actual": 0.2368, "avg_pred": 0.4812, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 38, "overconf_pct": 50.8}
```

## 本日残レース: 31件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 113件 締切済
- 通知発射: scan=15 nid / final=7 nid / result=4 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 11件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 201R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=4.1 drift=-26.8% | 15:18:13 |
| S00 | 085R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 12:11:13 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5174 | 4.3 | 2.22 | 200 | scan=- drift=- | 11:11:36 |
| S01_NAKAANA1 | 235R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=4.3 drift=+7.0% | 10:35:40 |
| S00 | 235R | win | 1 | 0.5174 | 4.6 | 2.38 | 300 | scan=- drift=- | 10:35:38 |
| S02_TETSUBAN | 209R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=- drift=- | 18:52:35 |
| S00 | 204R | win | 1 | 0.4989 | 4.3 | 2.15 | 300 | scan=- drift=- | 16:34:01 |
| S01_NAKAANA1 | 139R | win | 1 | 0.5334 | 4.2 | 2.24 | 200 | scan=- drift=- | 14:37:34 |
| S02_TETSUBAN | 097R | win | 1 | 0.5334 | 2.6 | 1.39 | 200 | scan=- drift=- | 13:21:50 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=2.4 drift=+16.7% | 15:06:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 21 | +12.7% | -60.2% | +500.0% | 8 | 4 | 12 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 498.9s |
| **Latency** (scan→final max) | 591.6s |
| **Traffic** (notifications 24h) | 37 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 278 | 0.4785 | 0.2806 | +0.1979 | 🟡+41% | 0.2317 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 106 | 0.4349 | 0.2264 | 0.2108 | 🔴-0.20 | 0.592 |
| S01_NAKAANA1 | win | 125 | 0.4878 | 0.2720 | 0.2369 | 🔴-0.20 | 0.666 |
| S02_TETSUBAN | win | 47 | 0.5522 | 0.4255 | 0.2653 | 🔴-0.09 | 1.079 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 5 | 0.2290 | 0.0000 | 🔴+0.2290 |
| 0.30-0.50 | 104 | 0.4106 | 0.2404 | 🔴+0.1702 |
| 0.50+ | 162 | 0.5441 | 0.3272 | 🔴+0.2170 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 205 | 0.809 |
| win | <5.0 | ✅learned | 371 | 0.74 |
| win | <10.0 | ✅learned | 158 | 0.45 |
| win | <20.0 | ✅learned | 48 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-11-15T16:10:01.628227+09:00_