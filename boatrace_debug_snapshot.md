# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-02T14:40:01.978503+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×118 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×1  [2026-11-02T14:39:26]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-11-02T14:34:23]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T14:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CIRCUIT_BREAKER_TRIP  ×11  [2026-11-02T14:11:26]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×11  [2026-11-02T14:11:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-11-02T14:11:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-11-02T14:04:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-11-02T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 12 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T13:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T12:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-02T10:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ORPHAN_SCAN  ×1  [2026-11-02T06:00:13]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=174<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-02T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-02T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1865 actual=0.0000 gap=+0.1865`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-02T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=41 hit%=34.1% ROI=0.94 (コスト 9,500/回収 8,930)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-02T06:00:13]
- key: `ROI_STAT|S00: n=174 hit%=30.5% hit_CI[Bonf]=[21.5,41.2]% ROI=0.83 ROI_boot95=[0.61,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.44MB / last modified 2026-11-02T14:39:26.965293+09:00

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
ww.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-02 14:36:59,785 [INFO] scraper: odds_win: 6/6 parsed
2026-11-02 14:36:59,785 [INFO] scraper: fetch_race 04/9: boats=6 odds=191/191
2026-11-02 14:36:59,788 [INFO] predictor: CALIBRATION_MODE=on
2026-11-02 14:36:59,788 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-02 14:36:59,792 [INFO] run_cycle: fetched 04/9 [scan]: 156 combos
2026-11-02 14:36:59,932 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-02 14:38:04,974 [INFO] run_cycle: === run_cycle 14:38:04 ===
2026-11-02 14:38:04,974 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-02 14:38:04,974 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-02 14:38:05,051 [INFO] predictor: Models loaded OK
2026-11-02 14:38:25,301 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=04&hd=20261102: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-02 14:38:46,446 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=9&jcd=04&hd=20261102: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-02 14:38:55,870 [INFO] scraper: odds3t: 120/120 parsed
2026-11-02 14:39:05,945 [INFO] scraper: odds3f: 20/20 parsed
2026-11-02 14:39:16,048 [INFO] scraper: odds2t: 30/30 parsed
2026-11-02 14:39:16,049 [INFO] scraper: odds2f: 15/15 parsed
2026-11-02 14:39:25,131 [INFO] scraper: odds_win: 6/6 parsed
2026-11-02 14:39:25,131 [INFO] scraper: fetch_race 04/9: boats=6 odds=191/191
2026-11-02 14:39:25,134 [INFO] predictor: CALIBRATION_MODE=on
2026-11-02 14:39:25,134 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-02 14:39:25,138 [INFO] run_cycle: fetched 04/9 [final]: 156 combos
2026-11-02 14:39:25,272 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 30
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 4, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 310
  FINAL_MISSING: 118
  ANOMALY_SCAN_FINAL_RATIO: 28
  CIRCUIT_BREAKER_NO_ACTION: 26
  CIRCUIT_BREAKER_TRIP: 22
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 5 | 8,700 | 4,050 | -4,650 | 0.466 |
| S01_NAKAANA1 | 28 | 8 | 5,600 | 4,480 | -1,120 | 0.8 |
| S02_TETSUBAN | 12 | 3 | 2,400 | 3,500 | +1,100 | 1.458 |

## 直近アラート (24h・新しい順)
```
[14:39:25] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 4050, "roi_7d": 0.466, "sid": "S00"}
[14:39:25] CALIBRATION_DRIFT: {"avg_actual": 0.2319, "avg_pred": 0.4745, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 69, "overconf_pct": 51.1}
[14:39:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 526}
[14:36:59] FINAL_MISSING: {"deadline": "2026-11-02T14:05:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110206081405", "sid": "S00"}
[14:36:59] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 527}
[14:34:21] FINAL_MISSING: {"deadline": "2026-11-02T10:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110209021057", "sid": "S02_TETSUBAN"}
[14:34:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 525}
[14:31:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 529}
[14:30:38] FINAL_MISSING: {"deadline": "2026-11-02T12:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110206061259", "sid": "S00"}
[14:30:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 523}
```

## 本日残レース: 42件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 78件 締切済
- 通知発射: scan=14 nid / final=6 nid / result=3 nid
- predictions: 3 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 097R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.2 drift=+0.0% | 13:21:36 |
| S02_TETSUBAN | 036R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 13:08:13 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 11:47:38 |
| S02_TETSUBAN | 0711R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.3 drift=+13.0% | 20:05:24 |
| S00 | 1810R | win | 1 | 0.4111 | 15.0 | 6.17 | 300 | scan=12.0 drift=+25.0% | 13:06:12 |
| S00 | 224R | win | 1 | 0.4111 | 16.5 | 6.78 | 300 | scan=- drift=- | 12:13:13 |
| S00 | 022R | win | 1 | 0.2290 | 5.7 | 1.31 | 300 | scan=- drift=- | 11:11:18 |
| S00 | 243R | win | 1 | 0.3177 | 4.5 | 1.43 | 300 | scan=- drift=- | 16:23:14 |
| S00 | 153R | win | 1 | 0.3177 | 16.0 | 5.08 | 300 | scan=- drift=- | 16:05:49 |
| S01_NAKAANA1 | 242R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:54:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | +5.4% | -54.4% | +85.6% | 12 | 5 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 346.7s |
| **Latency** (scan→final max) | 531.5s |
| **Traffic** (notifications 24h) | 30 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 407 | 0.4779 | 0.3415 | +0.1364 | 🟡+28% | 0.2369 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4400 | 0.3000 | 0.2236 | 🔴-0.06 | 0.789 |
| S01_NAKAANA1 | win | 174 | 0.4879 | 0.3333 | 0.2403 | 🔴-0.08 | 0.829 |
| S02_TETSUBAN | win | 63 | 0.5529 | 0.4762 | 0.2637 | 🔴-0.06 | 1.081 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 144 | 0.4094 | 0.3056 | 🔴+0.1038 |
| 0.50+ | 241 | 0.5451 | 0.3859 | 🔴+0.1592 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 197 | 0.811 |
| win | <5.0 | ✅learned | 360 | 0.741 |
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
_auto-generated by claude_snapshot.py at 2026-11-02T14:40:01.978503+09:00_