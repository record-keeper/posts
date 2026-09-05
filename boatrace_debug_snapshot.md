# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-05T15:00:01.775136+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×34 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×63 (24h)
- 🔴 CALIBRATION_DRIFT×34 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 PSI_DRIFT_DETECTED×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-05T14:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 KS_ODDS_DRIFT  ×30  [2026-09-05T14:29:31]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CALIBRATION_DRIFT  ×53  [2026-09-05T14:06:28]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×53  [2026-09-05T14:06:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×53  [2026-09-05T14:06:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×53  [2026-09-05T14:06:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-05T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×53  [2026-09-05T13:22:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×10  [2026-09-05T12:49:31]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×21  [2026-09-05T11:52:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×46  [2026-09-05T10:00:50]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-05T06:00:11]
- key: `ORPHAN_SCAN|195 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1791 actual=0.2000 gap=-0.0209`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-05T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-05T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1266 actual=0.0000 gap=+0.1266`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S00: n=185 hit%=27.0% hit_CI[Bonf]=[18.7,37.3]% ROI=0.90 ROI_boot95=[0.64,1.22]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=22.6% hit_CI[Bonf]=[15.1,32.4]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-05T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=38.3% hit_CI[Bonf]=[24.5,54.3]% ROI=0.66 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.4MB / last modified 2026-09-05T15:00:03.771987+09:00

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
_cycle done: 0 notifications
2026-09-05 14:59:03,429 [INFO] run_cycle: === run_cycle 14:59:03 ===
2026-09-05 14:59:03,429 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-05 14:59:03,429 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-05 14:59:03,460 [INFO] predictor: Models loaded OK
2026-09-05 14:59:15,893 [INFO] scraper: odds3t: 120/120 parsed
2026-09-05 14:59:16,975 [INFO] scraper: odds3f: 20/20 parsed
2026-09-05 14:59:18,077 [INFO] scraper: odds2t: 30/30 parsed
2026-09-05 14:59:18,078 [INFO] scraper: odds2f: 14/15 parsed
2026-09-05 14:59:19,149 [INFO] scraper: odds_win: 5/6 parsed
2026-09-05 14:59:19,149 [INFO] scraper: fetch_race 22/7: boats=6 odds=189/191
2026-09-05 14:59:19,153 [INFO] predictor: CALIBRATION_MODE=on
2026-09-05 14:59:19,153 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-05 14:59:19,157 [INFO] run_cycle: fetched 22/7 [final]: 155 combos
2026-09-05 14:59:22,703 [INFO] scraper: odds3t: 120/120 parsed
2026-09-05 14:59:23,813 [INFO] scraper: odds3f: 20/20 parsed
2026-09-05 14:59:24,925 [INFO] scraper: odds2t: 30/30 parsed
2026-09-05 14:59:24,926 [INFO] scraper: odds2f: 15/15 parsed
2026-09-05 14:59:26,038 [INFO] scraper: odds_win: 6/6 parsed
2026-09-05 14:59:26,038 [INFO] scraper: fetch_race 11/10: boats=6 odds=191/191
2026-09-05 14:59:26,040 [INFO] predictor: CALIBRATION_MODE=on
2026-09-05 14:59:26,041 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-05 14:59:26,045 [INFO] run_cycle: fetched 11/10 [scan]: 156 combos
2026-09-05 14:59:26,170 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-05 15:00:05,528 [INFO] run_cycle: === run_cycle 15:00:05 ===
2026-09-05 15:00:05,528 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-05 15:00:05,528 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-05 15:00:05,573 [INFO] predictor: Models loaded OK

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
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 14, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 108
  FINAL_MISSING: 63
  CALIBRATION_DRIFT: 34
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
  KS_ODDS_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
  PSI_DRIFT_DETECTED: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 12 | 14,700 | 12,420 | -2,280 | 0.845 |
| S01_NAKAANA1 | 37 | 3 | 7,400 | 1,460 | -5,940 | 0.197 |
| S02_TETSUBAN | 9 | 4 | 1,800 | 1,800 | +0 | 1.0 |

## 直近アラート (24h・新しい順)
```
[14:54:49] FINAL_MISSING: {"deadline": "2026-09-05T11:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090504021124", "sid": "S00"}
[14:46:19] FINAL_MISSING: {"deadline": "2026-09-05T14:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090502081416", "sid": "S00"}
[14:39:44] FINAL_MISSING: {"deadline": "2026-09-05T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090503031208", "sid": "S00"}
[14:29:30] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 1460, "roi_7d": 0.197, "sid": "S01_NAKAANA1"}
[14:29:30] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.009773, "ks_stat": 0.185}
[14:29:30] CALIBRATION_DRIFT: {"avg_actual": 0.2, "avg_pred": 0.4727, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 95, "overconf_pct": 57.7}
[14:20:38] FINAL_MISSING: {"deadline": "2026-09-05T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090502011047", "sid": "S01_NAKAANA1"}
[14:15:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1186}
[14:14:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1176}
[14:13:20] FINAL_MISSING: {"deadline": "2026-09-05T11:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026090509031142", "sid": "S00"}
```

## 本日残レース: 76件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 92件 締切済
- 通知発射: scan=17 nid / final=14 nid / result=9 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 036R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=4.1 drift=-26.8% | 13:26:28 |
| S00 | 045R | win | 1 | 0.5891 | 4.3 | 2.53 | 300 | scan=4.1 drift=+4.9% | 12:49:18 |
| S01_NAKAANA1 | 025R | win | 1 | 0.5334 | 3.9 | 2.08 | 200 | scan=- drift=- | 12:41:19 |
| S01_NAKAANA1 | 222R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=3.7 drift=+13.5% | 12:15:20 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=- drift=- | 11:43:30 |
| S00 | 023R | win | 1 | 0.5123 | 8.1 | 4.15 | 300 | scan=33.0 drift=-75.5% | 11:42:20 |
| S02_TETSUBAN | 133R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=2.2 drift=+0.0% | 11:34:32 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5476 | 4.7 | 2.57 | 200 | scan=4.0 drift=+17.5% | 11:21:27 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=3.1 drift=+12.9% | 10:52:26 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5890 | 3.6 | 2.12 | 200 | scan=3.0 drift=+20.0% | 10:47:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 55 | +9.8% | -75.5% | +158.3% | 12 | 8 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 402.5s |
| **Latency** (scan→final max) | 603.8s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 461 | 0.4747 | 0.2690 | +0.2057 | 🟡+43% | 0.2409 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 186 | 0.4270 | 0.2688 | 0.2211 | 🔴-0.12 | 0.897 |
| S01_NAKAANA1 | win | 193 | 0.4890 | 0.2228 | 0.2495 | 🔴-0.44 | 0.699 |
| S02_TETSUBAN | win | 82 | 0.5493 | 0.3780 | 0.2654 | 🔴-0.13 | 0.651 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1266 | 0.0000 | 🔴+0.1266 |
| 0.15-0.20 | 10 | 0.1791 | 0.2000 | ✅-0.0209 |
| 0.20-0.30 | 10 | 0.2255 | 0.2000 | ✅+0.0255 |
| 0.30-0.50 | 158 | 0.4065 | 0.2342 | 🔴+0.1723 |
| 0.50+ | 274 | 0.5459 | 0.2993 | 🔴+0.2467 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 127 | 0.776 |
| win | <5.0 | ✅learned | 233 | 0.739 |
| win | <10.0 | ✅learned | 115 | 0.468 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-05T15:00:01.775136+09:00_