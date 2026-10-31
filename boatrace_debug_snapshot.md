# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-31T11:30:02.391160+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×126 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T11:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-10-31T11:21:50]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×5  [2026-10-31T11:12:55]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×10  [2026-10-31T11:12:55]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×5  [2026-10-31T11:12:55]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-31T11:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-10-31T10:46:08]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

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

### ℹ️ ROI_STAT  ×1  [2026-10-31T06:00:41]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=47.8% hit_CI[Bonf]=[31.7,64.5]% ROI=1.06 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.27MB / last modified 2026-10-31T11:30:04.825441+09:00

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
11:27:49,291 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-31 11:27:49,295 [INFO] run_cycle: fetched 18/7 [scan]: 155 combos
2026-10-31 11:28:09,592 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=3&jcd=02&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 11:28:20,701 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=3&jcd=02&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-31 11:28:43,885 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=3&jcd=02&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 11:28:54,957 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=3&jcd=02&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-10-31 11:29:07,107 [INFO] scraper: odds3t: 120/120 parsed
2026-10-31 11:29:17,191 [INFO] scraper: odds3f: 20/20 parsed
2026-10-31 11:29:26,333 [INFO] scraper: odds2t: 30/30 parsed
2026-10-31 11:29:26,334 [INFO] scraper: odds2f: 15/15 parsed
2026-10-31 11:29:37,439 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=3&jcd=02&hd=20261031: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-31 11:29:46,722 [INFO] scraper: odds_win: 6/6 parsed
2026-10-31 11:29:46,722 [INFO] scraper: fetch_race 02/3: boats=6 odds=191/191
2026-10-31 11:29:46,725 [INFO] predictor: CALIBRATION_MODE=on
2026-10-31 11:29:46,725 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-31 11:29:46,728 [INFO] run_cycle: fetched 02/3 [scan]: 156 combos
2026-10-31 11:29:46,846 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 30
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 29
  }
]
```

## Phase別通知記録 (24h)
{'final': 9, 'result': 5, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 195
  FINAL_MISSING: 126
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 27
  ANOMALY_SCAN_FINAL_RATIO: 24
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 15
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 12 | 13,200 | 8,400 | -4,800 | 0.636 |
| S01_NAKAANA1 | 35 | 11 | 7,000 | 5,600 | -1,400 | 0.8 |
| S02_TETSUBAN | 12 | 5 | 2,400 | 4,100 | +1,700 | 1.708 |

## 直近アラート (24h・新しい順)
```
[11:29:46] FINAL_MISSING: {"deadline": "2026-10-31T10:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103109021057", "sid": "S02_TETSUBAN"}
[11:29:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 513}
[11:25:53] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 513}
[11:25:53] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.553, "baseline_mean": 0.753, "baseline_stdev": 0.221, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.2, "today_scan_count": 5, "z_score": -2.51}
[11:21:49] FINAL_MISSING: {"deadline": "2026-10-31T10:49:00+09:00", "kind": "FINAL_MISSING", "nid": "2026103116011049", "sid": "S00"}
[11:21:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 505}
[11:17:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 507}
[11:17:18] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.753, "baseline_mean": 0.753, "baseline_stdev": 0.221, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.0, "today_scan_count": 5, "z_score": -3.41}
[11:12:54] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:12:54] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 8400, "roi_7d": 0.651, "sid": "S00"}
```

## 本日残レース: 112件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 32件 締切済
- 通知発射: scan=5 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 042R | win | 1 | 0.3177 | 12.1 | 3.84 | 300 | scan=- drift=- | 11:19:12 |
| S00 | 061R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:39:22 |
| S00 | 246R | win | 1 | 0.1957 | 5.5 | 1.08 | 300 | scan=- drift=- | 17:42:12 |
| S00 | 013R | win | 1 | 0.5174 | 5.7 | 2.95 | 300 | scan=- drift=- | 16:16:29 |
| S00 | 067R | win | 1 | 0.5735 | 8.3 | 4.76 | 300 | scan=18.2 drift=-54.4% | 13:39:39 |
| S02_TETSUBAN | 031R | win | 1 | 0.6031 | 2.2 | 1.33 | 200 | scan=- drift=- | 10:57:28 |
| S01_NAKAANA1 | 075R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=- drift=- | 17:09:25 |
| S01_NAKAANA1 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 200 | scan=4.5 drift=-6.7% | 16:38:51 |
| S00 | 074R | win | 1 | 0.4450 | 4.2 | 1.87 | 300 | scan=4.5 drift=-6.7% | 16:38:48 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=- drift=- | 16:15:38 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +5.9% | -77.4% | +111.7% | 15 | 5 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 472.9s |
| **Latency** (scan→final max) | 662.1s |
| **Traffic** (notifications 24h) | 29 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4794 | 0.3410 | +0.1385 | 🟡+29% | 0.2394 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4446 | 0.2989 | 0.2304 | 🔴-0.10 | 0.803 |
| S01_NAKAANA1 | win | 185 | 0.4881 | 0.3351 | 0.2403 | 🔴-0.08 | 0.881 |
| S02_TETSUBAN | win | 68 | 0.5500 | 0.4706 | 0.2612 | 🔴-0.05 | 1.053 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 153 | 0.4123 | 0.3137 | 🔴+0.0986 |
| 0.50+ | 261 | 0.5440 | 0.3755 | 🔴+0.1685 |

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
_auto-generated by claude_snapshot.py at 2026-10-31T11:30:02.391160+09:00_