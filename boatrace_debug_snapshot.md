# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-07T17:00:02.599944+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×74 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×74 (24h)
- 🟡 FINAL_MISSING×43 (24h)
- 🔴 CALIBRATION_DRIFT×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T17:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T17:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-07T17:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×3  [2026-06-07T16:57:56]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-06-07T16:20:10]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×55  [2026-06-07T16:05:39]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×165  [2026-06-07T16:05:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×165  [2026-06-07T16:05:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×55  [2026-06-07T16:05:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-07T15:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×21  [2026-06-07T14:54:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 PSI_DRIFT_DETECTED  ×26  [2026-06-07T13:00:24]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2201 actual=0.4000 gap=-0.1799`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-07T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=25.0% ROI=0.96 (コスト 8,200/回収 7,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-07T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=22.5% ROI=0.57 (コスト 8,400/回収 4,750)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-07T06:00:10]
- key: `ROI_STAT|S00: n=156 hit%=26.3% hit_CI[Bonf]=[17.5,37.5]% ROI=0.78 ROI_boot95=[0.54,1.06]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-07T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.6MB / last modified 2026-06-07T17:00:05.238838+09:00

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
p/owpc/pc/race/racelist?rno=4&jcd=15&hd=20260607: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-06-07 16:58:39,976 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=15&hd=20260607
2026-06-07 16:58:39,976 [ERROR] scraper: racelist fetch failed: jcd=15 rno=4
2026-06-07 16:58:39,976 [WARNING] run_cycle: fetch None: 15/4
2026-06-07 16:58:40,165 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-07 16:59:06,197 [INFO] run_cycle: === run_cycle 16:59:06 ===
2026-06-07 16:59:06,201 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-07 16:59:06,201 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-07 16:59:06,312 [INFO] predictor: Models loaded OK
2026-06-07 16:59:17,370 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=01&hd=20260607: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-07 16:59:28,427 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=01&hd=20260607: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-07 16:59:42,839 [INFO] scraper: odds3t: 120/120 parsed
2026-06-07 16:59:43,947 [INFO] scraper: odds3f: 20/20 parsed
2026-06-07 16:59:45,053 [INFO] scraper: odds2t: 30/30 parsed
2026-06-07 16:59:45,055 [INFO] scraper: odds2f: 15/15 parsed
2026-06-07 16:59:46,161 [INFO] scraper: odds_win: 6/6 parsed
2026-06-07 16:59:46,161 [INFO] scraper: fetch_race 01/4: boats=6 odds=191/191
2026-06-07 16:59:46,173 [INFO] predictor: CALIBRATION_MODE=on
2026-06-07 16:59:46,173 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-07 16:59:46,183 [INFO] run_cycle: fetched 01/4 [scan]: 156 combos
2026-06-07 16:59:46,398 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 82
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 82
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 22, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 237
  CIRCUIT_BREAKER_TRIP: 74
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 43
  CALIBRATION_DRIFT: 38
  ANOMALY_SCAN_FINAL_RATIO: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 13
  PSI_DRIFT_DETECTED: 6
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 5 | 9,000 | 3,720 | -5,280 | 0.413 |
| S01_NAKAANA1 | 27 | 2 | 5,400 | 580 | -4,820 | 0.107 |
| S02_TETSUBAN | 25 | 6 | 5,000 | 1,680 | -3,320 | 0.336 |

## 直近アラート (24h・新しい順)
```
[16:59:46] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 898}
[16:58:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 897}
[16:41:07] FINAL_MISSING: {"deadline": "2026-06-07T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060703031208", "sid": "S00"}
[16:38:29] CIRCUIT_BREAKER_TRIP: {"cost": 5000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 25, "payout": 1680, "roi_7d": 0.336, "sid": "S02_TETSUBAN"}
[16:38:29] FINAL_MISSING: {"deadline": "2026-06-07T15:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060705081507", "sid": "S00"}
[16:38:29] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 8.4, "baseline_n_days": 7, "baseline_stdev": 2.6, "hour": 16, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 17, "z_score": 3.33}
[16:33:46] FINAL_MISSING: {"deadline": "2026-06-07T11:00:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060718061100", "sid": "S00"}
[16:31:06] FINAL_MISSING: {"deadline": "2026-06-07T09:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060710040957", "sid": "S00"}
[16:31:06] FINAL_MISSING: {"deadline": "2026-06-07T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060706021159", "sid": "S00"}
[16:24:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 968}
```

## 本日残レース: 40件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 116件 締切済
- 通知発射: scan=15 nid / final=21 nid / result=15 nid
- predictions: 17 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 073R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.5 drift=-16.0% | 16:38:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4989 | 3.6 | 1.80 | 200 | scan=- drift=- | 16:01:21 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 15:22:20 |
| S01_NAKAANA1 | 058R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.5 drift=-5.7% | 15:04:32 |
| S00 | 056R | win | 1 | 0.5123 | 7.1 | 3.64 | 300 | scan=- drift=- | 14:01:20 |
| S02_TETSUBAN | 2112R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=2.5 drift=+0.0% | 13:56:20 |
| S00 | 055R | win | 1 | 0.2290 | 45.0 | 10.31 | 300 | scan=- drift=- | 13:29:43 |
| S02_TETSUBAN | 2111R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 13:21:31 |
| S00 | 188R | win | 1 | 0.1231 | 4.4 | 0.54 | 300 | scan=- drift=- | 11:59:21 |
| S02_TETSUBAN | 032R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 11:39:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | +15.6% | -62.9% | +432.7% | 14 | 7 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.3s |
| **Latency** (scan→final max) | 653.4s |
| **Traffic** (notifications 24h) | 82 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 375 | 0.4683 | 0.2907 | +0.1776 | 🟡+38% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 154 | 0.4238 | 0.2468 | 0.2203 | 🔴-0.19 | 0.76 |
| S01_NAKAANA1 | win | 140 | 0.4857 | 0.2714 | 0.2441 | 🔴-0.23 | 0.678 |
| S02_TETSUBAN | win | 81 | 0.5230 | 0.4074 | 0.2613 | 🔴-0.08 | 0.735 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 150 | 0.4203 | 0.2400 | 🔴+0.1803 |
| 0.50+ | 202 | 0.5413 | 0.3416 | 🔴+0.1997 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 33 | 0.747 |
| win | <5.0 | ✅learned | 59 | 0.732 |
| win | <10.0 | ✅learned | 40 | 0.525 |
| win | <20.0 | ✅learned | 12 | 0.197 |
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
_auto-generated by claude_snapshot.py at 2026-06-07T17:00:02.599944+09:00_