# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-01T13:10:01.989447+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×25 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×146 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-01T13:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×6  [2026-11-01T12:44:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-01T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-01T12:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-01T12:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-11-01T12:29:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×13  [2026-11-01T12:11:11]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×26  [2026-11-01T12:11:11]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×13  [2026-11-01T12:11:11]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-01T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-01T11:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 12 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-01T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 14 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×43  [2026-11-01T09:00:05]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-01T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-01T06:00:10]
- key: `ORPHAN_SCAN|164 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-01T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-01T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-01T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-01T06:00:10]
- key: `ROI_STAT|S00: n=178 hit%=30.9% hit_CI[Bonf]=[21.9,41.6]% ROI=0.85 ROI_boot95=[0.63,1.10]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-01T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=182 hit%=33.5% hit_CI[Bonf]=[24.3,44.1]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.38MB / last modified 2026-11-01T13:09:44.323848+09:00

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
 run_cycle 13:08:04 ===
2026-11-01 13:08:04,274 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-01 13:08:04,274 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-01 13:08:04,302 [INFO] predictor: Models loaded OK
2026-11-01 13:08:15,363 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=22&hd=20261101: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-01 13:08:26,433 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=22&hd=20261101: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-01 13:08:48,661 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=6&jcd=22&hd=20261101: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-01 13:09:06,986 [INFO] scraper: odds3t: 120/120 parsed
2026-11-01 13:09:16,099 [INFO] scraper: odds3f: 20/20 parsed
2026-11-01 13:09:26,230 [INFO] scraper: odds2t: 30/30 parsed
2026-11-01 13:09:26,231 [INFO] scraper: odds2f: 15/15 parsed
2026-11-01 13:09:36,305 [INFO] scraper: odds_win: 2/6 parsed
2026-11-01 13:09:36,305 [INFO] scraper: fetch_race 22/6: boats=6 odds=187/191
2026-11-01 13:09:36,542 [INFO] predictor: CALIBRATION_MODE=on
2026-11-01 13:09:36,542 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-11-01 13:09:36,546 [INFO] run_cycle: fetched 22/6 [scan]: 152 combos
2026-11-01 13:09:39,482 [INFO] race_id: notif: nid=2026110122061319 sid=S01_NAKAANA1 phase=scan rank=B
2026-11-01 13:09:39,987 [INFO] notifier: Discord notify OK (status=204)
2026-11-01 13:09:42,012 [INFO] notifier: Discord notify OK (status=204)
2026-11-01 13:09:42,054 [INFO] run_cycle: SCAN S01_NAKAANA1 福岡6R B
2026-11-01 13:09:42,199 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 32
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 32
  }
]
```

## Phase別通知記録 (24h)
{'final': 9, 'result': 7, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 239
  FINAL_MISSING: 146
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  ANOMALY_SCAN_FINAL_RATIO: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 39 | 9 | 11,700 | 7,110 | -4,590 | 0.608 |
| S01_NAKAANA1 | 31 | 8 | 6,200 | 4,560 | -1,640 | 0.735 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[13:09:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 490}
[13:09:42] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.43, "baseline_mean": 0.68, "baseline_stdev": 0.283, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 8, "z_score": -1.52}
[13:07:26] CIRCUIT_BREAKER_TRIP: {"cost": 11700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 7110, "roi_7d": 0.608, "sid": "S00"}
[13:07:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 484}
[13:07:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.395, "baseline_mean": 0.68, "baseline_stdev": 0.283, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.286, "today_scan_count": 7, "z_score": -1.4}
[13:04:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 482}
[13:04:05] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.538, "baseline_mean": 0.68, "baseline_stdev": 0.283, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.143, "today_scan_count": 7, "z_score": -1.9}
[12:56:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 480}
[12:56:29] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.48, "baseline_mean": 0.68, "baseline_stdev": 0.283, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.2, "today_scan_count": 5, "z_score": -1.7}
[12:49:12] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 7110, "roi_7d": 0.624, "sid": "S00"}
```

## 本日残レース: 89件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 67件 締切済
- 通知発射: scan=8 nid / final=4 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |
| S00 | 022R | win | 1 | 0.2290 | 5.7 | 1.31 | 300 | scan=- drift=- | 11:11:18 |
| S00 | 243R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 16:23:14 |
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:54:24 |
| S00 | 048R | win | 1 | 0.5174 | 7.7 | 3.98 | 300 | scan=15.8 drift=-51.3% | 14:08:04 |
| S01_NAKAANA1 | 098R | win | 1 | 0.5719 | 3.8 | 2.17 | 200 | scan=3.8 drift=+0.0% | 13:53:40 |
| S00 | 024R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=10.5 drift=-50.5% | 12:04:25 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.1 drift=+25.8% | 11:37:47 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | +5.3% | -77.4% | +111.7% | 15 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 443.9s |
| **Latency** (scan→final max) | 554.6s |
| **Traffic** (notifications 24h) | 32 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 420 | 0.4772 | 0.3476 | +0.1296 | 🟡+27% | 0.2396 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4402 | 0.3051 | 0.2291 | 🔴-0.08 | 0.829 |
| S01_NAKAANA1 | win | 176 | 0.4865 | 0.3409 | 0.2419 | 🔴-0.08 | 0.888 |
| S02_TETSUBAN | win | 67 | 0.5507 | 0.4776 | 0.2613 | 🔴-0.05 | 1.069 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2291 | 0.2000 | ✅+0.0291 |
| 0.30-0.50 | 150 | 0.4100 | 0.3267 | 🔴+0.0834 |
| 0.50+ | 247 | 0.5445 | 0.3806 | 🔴+0.1640 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 359 | 0.742 |
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
_auto-generated by claude_snapshot.py at 2026-11-01T13:10:01.989447+09:00_