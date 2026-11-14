# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-14T14:20:01.532269+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×34 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×186 (24h)
- 🔴 PSI_DRIFT_DETECTED×34 (24h)
- 🔴 STRATEGY_CI_FAIL×18 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×1  [2026-11-14T14:15:42]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×1  [2026-11-14T14:15:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-14T14:00:13]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-11-14T13:40:16]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-11-14T13:19:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×3  [2026-11-14T12:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-14T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 13 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-14T11:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 14 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-11-14T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-14T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-14T09:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-14T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=138<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-14T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3219 actual=0.1034 gap=+0.2185`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-14T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=7 pred=0.2290 actual=0.1429 gap=+0.0862`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-14T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1901 actual=0.0000 gap=+0.1901`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-14T06:00:11]
- key: `ROI_STAT|S00: n=122 hit%=26.2% hit_CI[Bonf]=[16.5,39.0]% ROI=0.71 ROI_boot95=[0.45,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-14T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=122<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-14T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=138 hit%=29.7% hit_CI[Bonf]=[19.9,41.8]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-14T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=48 hit%=43.8% hit_CI[Bonf]=[25.6,63.8]% ROI=1.04 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-14T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=48<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.05MB / last modified 2026-11-14T14:15:42.097236+09:00

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
 14:18:04,297 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=9&jcd=09&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-14 14:18:15,401 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=9&jcd=09&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-14 14:18:27,560 [INFO] scraper: odds3t: 120/120 parsed
2026-11-14 14:18:37,635 [INFO] scraper: odds3f: 20/20 parsed
2026-11-14 14:18:48,807 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=9&jcd=09&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-14 14:18:57,968 [INFO] scraper: odds2t: 27/30 parsed
2026-11-14 14:18:57,969 [INFO] scraper: odds2f: 14/15 parsed
2026-11-14 14:19:08,978 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=9&jcd=09&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-14 14:19:18,796 [INFO] scraper: odds_win: 6/6 parsed
2026-11-14 14:19:18,796 [INFO] scraper: fetch_race 09/9: boats=6 odds=187/191
2026-11-14 14:19:18,799 [INFO] predictor: CALIBRATION_MODE=on
2026-11-14 14:19:18,799 [INFO] predictor: combos: {'win': 6, '2t': 27, '3t': 120}
2026-11-14 14:19:18,803 [INFO] run_cycle: fetched 09/9 [scan]: 153 combos
2026-11-14 14:19:49,377 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=12&jcd=23&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-14 14:20:00,430 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=12&jcd=23&hd=20261114: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s

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
    "c": 21
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 21
  }
]
```

## Phase別通知記録 (24h)
{'final': 6, 'result': 2, 'scan': 13}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 240
  FINAL_MISSING: 186
  PSI_DRIFT_DETECTED: 34
  STRATEGY_CI_FAIL: 18
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 13 | 3 | 3,900 | 2,760 | -1,140 | 0.708 |
| S01_NAKAANA1 | 15 | 3 | 3,000 | 1,020 | -1,980 | 0.34 |
| S02_TETSUBAN | 11 | 6 | 2,200 | 2,160 | -40 | 0.982 |

## 直近アラート (24h・新しい順)
```
[14:15:39] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:15:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[14:12:43] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 258, "n_recent": 39, "psi": 1.089}
[14:12:43] FINAL_MISSING: {"deadline": "2026-11-14T11:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111411031137", "sid": "S02_TETSUBAN"}
[14:12:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 471}
[14:08:22] FINAL_MISSING: {"deadline": "2026-11-14T13:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111403071335", "sid": "S02_TETSUBAN"}
[14:08:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 473}
[14:04:37] FINAL_MISSING: {"deadline": "2026-11-14T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111423071132", "sid": "S01_NAKAANA1"}
[14:04:37] FINAL_MISSING: {"deadline": "2026-11-14T11:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111413031130", "sid": "S00"}
[14:04:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 470}
```

## 本日残レース: 73件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 95件 締切済
- 通知発射: scan=11 nid / final=4 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 097R | win | 1 | 0.5334 | 2.6 | 1.39 | 200 | scan=- drift=- | 13:21:50 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=2.4 drift=+16.7% | 15:06:33 |
| S02_TETSUBAN | 166R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=2.6 drift=-7.7% | 13:22:46 |
| S02_TETSUBAN | 164R | win | 1 | 0.5990 | 2.1 | 1.26 | 200 | scan=2.1 drift=+0.0% | 12:20:36 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 11:37:37 |
| S00 | 042R | win | 1 | 0.3177 | 27.0 | 8.58 | 300 | scan=4.5 drift=+500.0% | 11:17:13 |
| S00 | 1311R | win | 1 | 0.5334 | 5.6 | 2.99 | 300 | scan=4.8 drift=+16.7% | 15:39:03 |
| S00 | 137R | win | 1 | 0.3177 | 6.0 | 1.91 | 300 | scan=- drift=- | 13:23:36 |
| S00 | 166R | win | 1 | 0.5334 | 10.5 | 5.60 | 300 | scan=24.7 drift=-57.5% | 13:12:51 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=- drift=- | 12:34:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 24 | +9.3% | -66.8% | +500.0% | 8 | 5 | 12 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.3s |
| **Latency** (scan→final max) | 575.5s |
| **Traffic** (notifications 24h) | 21 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 297 | 0.4740 | 0.3064 | +0.1676 | 🟡+35% | 0.2291 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 119 | 0.4270 | 0.2521 | 0.2055 | 🔴-0.09 | 0.657 |
| S01_NAKAANA1 | win | 129 | 0.4871 | 0.3023 | 0.2386 | 🔴-0.13 | 0.76 |
| S02_TETSUBAN | win | 49 | 0.5534 | 0.4490 | 0.2615 | 🔴-0.06 | 1.073 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1901 | 0.0000 | 🔴+0.1901 |
| 0.20-0.30 | 6 | 0.2290 | 0.0000 | 🔴+0.2290 |
| 0.30-0.50 | 110 | 0.4105 | 0.2727 | 🔴+0.1377 |
| 0.50+ | 170 | 0.5445 | 0.3588 | 🔴+0.1857 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 204 | 0.806 |
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
_auto-generated by claude_snapshot.py at 2026-11-14T14:20:01.532269+09:00_