# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-31T16:20:01.846472+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×129 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-31T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-31T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T16:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-10-31T15:52:35]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×13  [2026-10-31T15:31:09]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×28  [2026-10-31T15:25:59]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-10-31T15:25:59]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×14  [2026-10-31T15:25:59]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-10-31T15:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T14:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T13:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×37  [2026-10-31T09:00:18]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S00: n=186<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-31T06:00:41]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-31T06:00:41]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2288 actual=0.2000 gap=+0.0288`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.3MB / last modified 2026-10-31T16:18:55.338069+09:00

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
in 1s
2026-10-31 16:18:19,468 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=16&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-31 16:18:32,541 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=16&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-10-31 16:18:32,541 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds3f?rno=12&jcd=16&hd=20261031
2026-10-31 16:18:41,764 [INFO] scraper: odds2t: 30/30 parsed
2026-10-31 16:18:41,765 [INFO] scraper: odds2f: 15/15 parsed
2026-10-31 16:18:51,830 [INFO] scraper: odds_win: 6/6 parsed
2026-10-31 16:18:51,830 [INFO] scraper: fetch_race 16/12: boats=6 odds=171/191
2026-10-31 16:18:51,833 [INFO] predictor: CALIBRATION_MODE=on
2026-10-31 16:18:51,833 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-31 16:18:51,837 [INFO] run_cycle: fetched 16/12 [scan]: 156 combos
2026-10-31 16:18:51,985 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-31 16:19:04,520 [INFO] run_cycle: === run_cycle 16:19:04 ===
2026-10-31 16:19:04,521 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-31 16:19:04,521 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-31 16:19:04,550 [INFO] predictor: Models loaded OK
2026-10-31 16:19:24,905 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=3&jcd=24&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 16:19:44,319 [INFO] scraper: odds3t: 120/120 parsed
2026-10-31 16:19:53,454 [INFO] scraper: odds3f: 20/20 parsed
2026-10-31 16:20:02,711 [INFO] scraper: odds2t: 30/30 parsed
2026-10-31 16:20:02,713 [INFO] scraper: odds2f: 15/15 parsed

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
{'final': 11, 'result': 8, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 190
  FINAL_MISSING: 129
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 29
  CIRCUIT_BREAKER_TRIP: 27
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 9
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 10 | 11,400 | 7,530 | -3,870 | 0.661 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,620 | -2,380 | 0.66 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[16:18:52] FINAL_MISSING: {"deadline": "2026-10-31T10:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103123051032", "sid": "S00"}
[16:18:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[16:16:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 491}
[16:15:12] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 493}
[16:11:14] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 7530, "roi_7d": 0.644, "sid": "S00"}
[16:11:14] FINAL_MISSING: {"deadline": "2026-10-31T12:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103102051234", "sid": "S00"}
[16:11:14] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.475, "baseline_mean": 0.753, "baseline_stdev": 0.221, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.278, "today_scan_count": 18, "z_score": -2.15}
[16:03:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 495}
[16:03:20] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.458, "baseline_mean": 0.753, "baseline_stdev": 0.221, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.294, "today_scan_count": 17, "z_score": -2.08}
[15:58:32] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4620, "roi_7d": 0.66, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 29件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 115件 締切済
- 通知発射: scan=18 nid / final=9 nid / result=6 nid
- predictions: 8 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 13件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:54:24 |
| S00 | 048R | win | 1 | 0.5174 | 7.7 | 3.98 | 300 | scan=15.8 drift=-51.3% | 14:08:04 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5719 | 3.8 | 2.17 | 200 | scan=3.8 drift=+0.0% | 13:53:40 |
| S00 | 024R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=10.5 drift=-50.5% | 12:04:25 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.1 drift=+25.8% | 11:37:47 |
| S00 | 042R | win | 1 | 0.3177 | 12.1 | 3.84 | 300 | scan=- drift=- | 11:19:12 |
| S00 | 061R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:39:22 |
| S00 | 246R | win | 1 | 0.1957 | 5.5 | 1.08 | 300 | scan=- drift=- | 17:42:12 |
| S00 | 013R | win | 1 | 0.5174 | 5.7 | 2.95 | 300 | scan=- drift=- | 16:16:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +4.2% | -77.4% | +111.7% | 17 | 7 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.1s |
| **Latency** (scan→final max) | 588.4s |
| **Traffic** (notifications 24h) | 39 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 427 | 0.4784 | 0.3443 | +0.1341 | 🟡+28% | 0.2397 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4426 | 0.3090 | 0.2303 | 🔴-0.08 | 0.846 |
| S01_NAKAANA1 | win | 182 | 0.4867 | 0.3297 | 0.2409 | 🔴-0.09 | 0.866 |
| S02_TETSUBAN | win | 67 | 0.5507 | 0.4776 | 0.2613 | 🔴-0.05 | 1.069 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 152 | 0.4124 | 0.3158 | 🔴+0.0966 |
| 0.50+ | 252 | 0.5442 | 0.3810 | 🔴+0.1633 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 358 | 0.741 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-31T16:20:01.846472+09:00_