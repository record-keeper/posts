# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-31T12:20:02.011943+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×125 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×2  [2026-10-31T12:14:08]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×4  [2026-10-31T12:14:08]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×2  [2026-10-31T12:14:08]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T12:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×9  [2026-10-31T11:47:05]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-10-31T11:21:50]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-10-31T10:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
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

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-31T06:00:41]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=31.8% ROI=0.87 (コスト 10,300/回収 8,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S00: n=186 hit%=30.1% hit_CI[Bonf]=[21.4,40.5]% ROI=0.81 ROI_boot95=[0.62,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S01_NAKAANA1: n=185 hit%=33.5% hit_CI[Bonf]=[24.4,44.1]% ROI=0.88 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.27MB / last modified 2026-10-31T12:19:14.698472+09:00

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
n
2026-10-31 12:17:15,008 [INFO] predictor: combos: {'2t': 30, '3t': 120}
2026-10-31 12:17:15,012 [INFO] run_cycle: fetched 16/4 [scan]: 150 combos
2026-10-31 12:17:35,455 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=5&jcd=09&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 12:17:55,586 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=5&jcd=09&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 12:18:05,700 [INFO] scraper: odds3t: 120/120 parsed
2026-10-31 12:18:15,169 [INFO] scraper: odds3f: 20/20 parsed
2026-10-31 12:18:26,181 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=5&jcd=09&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 12:18:36,347 [INFO] scraper: odds2t: 30/30 parsed
2026-10-31 12:18:36,348 [INFO] scraper: odds2f: 15/15 parsed
2026-10-31 12:18:47,360 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=09&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 12:18:58,400 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=09&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-31 12:19:10,572 [INFO] scraper: odds_win: 6/6 parsed
2026-10-31 12:19:10,572 [INFO] scraper: fetch_race 09/5: boats=6 odds=191/191
2026-10-31 12:19:10,575 [INFO] predictor: CALIBRATION_MODE=on
2026-10-31 12:19:10,575 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-31 12:19:10,579 [INFO] run_cycle: fetched 09/5 [scan]: 156 combos
2026-10-31 12:19:10,724 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 33
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 33
  }
]
```

## Phase別通知記録 (24h)
{'final': 11, 'result': 6, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 194
  FINAL_MISSING: 125
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 28
  ANOMALY_SCAN_FINAL_RATIO: 26
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 15
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 11 | 12,300 | 7,470 | -4,830 | 0.607 |
| S01_NAKAANA1 | 36 | 11 | 7,200 | 5,600 | -1,600 | 0.778 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[12:19:10] FINAL_MISSING: {"deadline": "2026-10-31T11:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103104031148", "sid": "S01_NAKAANA1"}
[12:19:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 517}
[12:14:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:14:07] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 7470, "roi_7d": 0.607, "sid": "S00"}
[12:14:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:14:07] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:14:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 525}
[12:11:44] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 7470, "roi_7d": 0.593, "sid": "S00"}
[12:11:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 527}
[12:07:33] CIRCUIT_BREAKER_TRIP: {"cost": 13200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 8400, "roi_7d": 0.636, "sid": "S00"}
```

## 本日残レース: 96件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 48件 締切済
- 通知発射: scan=9 nid / final=5 nid / result=3 nid
- predictions: 4 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 024R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=10.5 drift=-50.5% | 12:04:25 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.1 drift=+25.8% | 11:37:47 |
| S00 | 042R | win | 1 | 0.3177 | 12.1 | 3.84 | 300 | scan=- drift=- | 11:19:12 |
| S00 | 061R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:39:22 |
| S00 | 246R | win | 1 | 0.1957 | 5.5 | 1.08 | 300 | scan=- drift=- | 17:42:12 |
| S00 | 013R | win | 1 | 0.5174 | 5.7 | 2.95 | 300 | scan=- drift=- | 16:16:29 |
| S00 | 067R | win | 1 | 0.5735 | 8.3 | 4.76 | 300 | scan=18.2 drift=-54.4% | 13:39:39 |
| S02_TETSUBAN | 031R | win | 1 | 0.6031 | 2.2 | 1.33 | 200 | scan=- drift=- | 10:57:28 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 17:09:25 |
| S01_NAKAANA1 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 200 | scan=4.5 drift=-6.7% | 16:38:51 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +5.1% | -77.4% | +111.7% | 16 | 6 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 433.0s |
| **Latency** (scan→final max) | 662.1s |
| **Traffic** (notifications 24h) | 33 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 436 | 0.4783 | 0.3394 | +0.1389 | 🟡+29% | 0.2388 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4432 | 0.2989 | 0.2292 | 🔴-0.09 | 0.803 |
| S01_NAKAANA1 | win | 184 | 0.4869 | 0.3315 | 0.2403 | 🔴-0.08 | 0.871 |
| S02_TETSUBAN | win | 68 | 0.5500 | 0.4706 | 0.2612 | 🔴-0.05 | 1.053 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 155 | 0.4117 | 0.3097 | 🔴+0.1020 |
| 0.50+ | 258 | 0.5438 | 0.3760 | 🔴+0.1678 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 358 | 0.741 |
| win | <10.0 | ✅learned | 156 | 0.45 |
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
_auto-generated by claude_snapshot.py at 2026-10-31T12:20:02.011943+09:00_