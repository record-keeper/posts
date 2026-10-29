# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-29T15:50:02.235139+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×62 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-29T15:30:10]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-29T15:30:10]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-29T15:30:10]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-10-29T15:18:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-10-29T15:08:15]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-10-29T15:08:15]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-10-29T15:08:15]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×17  [2026-10-29T15:04:50]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-29T14:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-10-29T13:15:43]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-29T11:30:07]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-10-29T10:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=195<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-29T06:00:19]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-29T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=196<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=69 hit%=33.3% ROI=0.91 (コスト 16,500/回収 15,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-29T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=51 hit%=25.5% ROI=0.83 (コスト 13,500/回収 11,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-29T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2288 actual=0.2000 gap=+0.0288`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.07MB / last modified 2026-10-29T15:46:07.832261+09:00

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
ool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-29 15:47:50,468 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=11&jcd=13&hd=20261029: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-29 15:48:01,535 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=11&jcd=13&hd=20261029: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-29 15:48:24,723 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=11&jcd=13&hd=20261029: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-29 15:48:34,041 [INFO] scraper: odds3t: 120/120 parsed
2026-10-29 15:48:44,149 [INFO] scraper: odds3f: 20/20 parsed
2026-10-29 15:48:54,257 [INFO] scraper: odds2t: 30/30 parsed
2026-10-29 15:48:54,258 [INFO] scraper: odds2f: 15/15 parsed
2026-10-29 15:49:05,265 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=11&jcd=13&hd=20261029: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-29 15:49:15,472 [INFO] scraper: odds_win: 6/6 parsed
2026-10-29 15:49:15,473 [INFO] scraper: fetch_race 13/11: boats=6 odds=191/191
2026-10-29 15:49:15,476 [INFO] predictor: CALIBRATION_MODE=on
2026-10-29 15:49:15,476 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-29 15:49:15,480 [INFO] run_cycle: fetched 13/11 [final]: 156 combos
2026-10-29 15:49:43,936 [INFO] scraper: odds3t: 120/120 parsed
2026-10-29 15:49:54,008 [INFO] scraper: odds3f: 20/20 parsed
2026-10-29 15:50:05,020 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=11&jcd=16&hd=20261029: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

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
    "c": 44
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 44
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 8, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 174
  FINAL_MISSING: 62
  CIRCUIT_BREAKER_TRIP: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 6
  ANOMALY_SCAN_FINAL_RATIO: 4
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 13 | 13,800 | 10,170 | -3,630 | 0.737 |
| S01_NAKAANA1 | 44 | 11 | 8,800 | 5,500 | -3,300 | 0.625 |
| S02_TETSUBAN | 13 | 6 | 2,600 | 4,360 | +1,760 | 1.677 |

## 直近アラート (24h・新しい順)
```
[15:46:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 474}
[15:41:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 473}
[15:39:47] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 5500, "roi_7d": 0.625, "sid": "S01_NAKAANA1"}
[15:39:47] FINAL_MISSING: {"deadline": "2026-10-29T10:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102923041001", "sid": "S00"}
[15:39:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 471}
[15:33:29] FINAL_MISSING: {"deadline": "2026-10-29T14:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102903081402", "sid": "S00"}
[15:33:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 460}
[15:28:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 465}
[15:24:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 469}
[15:23:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 467}
```

## 本日残レース: 35件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 108件 登録 / 73件 締切済
- 通知発射: scan=9 nid / final=7 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 038R | win | 1 | 0.5990 | 3.7 | 2.22 | 200 | scan=- drift=- | 14:00:01 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.1 drift=+54.8% | 13:24:39 |
| S00 | 145R | win | 1 | 0.5123 | 13.5 | 6.92 | 300 | scan=26.0 drift=-48.1% | 10:25:16 |
| S01_NAKAANA1 | 144R | win | 1 | 0.5891 | 3.5 | 2.06 | 200 | scan=3.3 drift=+6.1% | 09:51:37 |
| S00 | 079R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.7 drift=-6.4% | 19:01:31 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 3.4 | 1.74 | 200 | scan=3.5 drift=-2.9% | 17:34:21 |
| S00 | 073R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=4.5 drift=+24.4% | 16:12:21 |
| S00 | 153R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=4.5 drift=+66.7% | 16:04:19 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=- drift=- | 14:59:19 |
| S02_TETSUBAN | 167R | win | 1 | 0.6037 | 2.4 | 1.45 | 200 | scan=- drift=- | 13:45:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +7.3% | -77.4% | +111.7% | 17 | 5 | 36 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 477.5s |
| **Latency** (scan→final max) | 647.5s |
| **Traffic** (notifications 24h) | 44 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 452 | 0.4784 | 0.3451 | +0.1332 | 🟡+28% | 0.2413 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 191 | 0.4438 | 0.3089 | 0.2357 | 🔴-0.10 | 0.832 |
| S01_NAKAANA1 | win | 189 | 0.4869 | 0.3333 | 0.2395 | 🔴-0.08 | 0.91 |
| S02_TETSUBAN | win | 72 | 0.5477 | 0.4722 | 0.2609 | 🔴-0.05 | 1.035 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1854 | 0.0000 | 🔴+0.1854 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 161 | 0.4117 | 0.3106 | 🔴+0.1012 |
| 0.50+ | 268 | 0.5434 | 0.3806 | 🔴+0.1628 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 356 | 0.741 |
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
_auto-generated by claude_snapshot.py at 2026-10-29T15:50:02.235139+09:00_