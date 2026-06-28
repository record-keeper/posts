# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-28T10:50:01.942405+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×93 (24h)
- 🔴 CALIBRATION_DRIFT×35 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 PSI_DRIFT_DETECTED×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-06-28T10:40:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-28T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×49  [2026-06-28T10:01:44]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×49  [2026-06-28T10:01:44]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×49  [2026-06-28T10:01:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×49  [2026-06-28T10:01:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×49  [2026-06-28T10:01:44]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-06-28T09:31:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1819 actual=0.3333 gap=-0.1514`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-28T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=23 pred=0.3214 actual=0.2174 gap=+0.1040`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S00: n=167 hit%=25.1% hit_CI[Bonf]=[16.8,35.9]% ROI=0.65 ROI_boot95=[0.46,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=29.2% hit_CI[Bonf]=[19.4,41.3]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-28T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=28.8% hit_CI[Bonf]=[16.3,45.6]% ROI=0.45 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-28T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-28T06:00:16]
- key: `ORPHAN_SCAN|155 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-28T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=18.2% ROI=0.61 (コスト 9,500/回収 5,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-28T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=21.6% ROI=0.46 (コスト 8,700/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.28MB / last modified 2026-06-28T10:49:05.749586+09:00

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
== run_cycle 10:48:05 ===
2026-06-28 10:48:05,690 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 10:48:05,690 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 10:48:05,733 [INFO] predictor: Models loaded OK
2026-06-28 10:48:18,103 [INFO] scraper: odds3t: 120/120 parsed
2026-06-28 10:48:19,188 [INFO] scraper: odds3f: 20/20 parsed
2026-06-28 10:48:20,281 [INFO] scraper: odds2t: 30/30 parsed
2026-06-28 10:48:20,282 [INFO] scraper: odds2f: 15/15 parsed
2026-06-28 10:48:21,373 [INFO] scraper: odds_win: 6/6 parsed
2026-06-28 10:48:21,373 [INFO] scraper: fetch_race 14/1: boats=6 odds=191/191
2026-06-28 10:48:21,384 [INFO] predictor: CALIBRATION_MODE=on
2026-06-28 10:48:21,385 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-28 10:48:21,392 [INFO] run_cycle: fetched 14/1 [final]: 156 combos
2026-06-28 10:48:24,998 [INFO] scraper: odds3t: 120/120 parsed
2026-06-28 10:48:26,097 [INFO] scraper: odds3f: 20/20 parsed
2026-06-28 10:48:27,210 [INFO] scraper: odds2t: 27/30 parsed
2026-06-28 10:48:27,212 [INFO] scraper: odds2f: 14/15 parsed
2026-06-28 10:48:28,311 [INFO] scraper: odds_win: 3/6 parsed
2026-06-28 10:48:28,311 [INFO] scraper: fetch_race 17/1: boats=6 odds=184/191
2026-06-28 10:48:28,320 [INFO] predictor: CALIBRATION_MODE=on
2026-06-28 10:48:28,320 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-06-28 10:48:28,328 [INFO] run_cycle: fetched 17/1 [scan]: 150 combos
2026-06-28 10:48:28,568 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-28 10:49:05,206 [INFO] run_cycle: === run_cycle 10:49:05 ===
2026-06-28 10:49:05,206 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-28 10:49:05,206 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-28 10:49:05,273 [INFO] predictor: Models loaded OK
2026-06-28 10:49:05,638 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 10, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 229
  FINAL_MISSING: 93
  KS_ODDS_DRIFT: 49
  CALIBRATION_DRIFT: 35
  ANOMALY_SCAN_FINAL_RATIO: 31
  CIRCUIT_BREAKER_NO_ACTION: 30
  CIRCUIT_BREAKER_TRIP: 27
  PSI_DRIFT_DETECTED: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 10 | 15,300 | 7,170 | -8,130 | 0.469 |
| S01_NAKAANA1 | 31 | 10 | 6,200 | 5,300 | -900 | 0.855 |
| S02_TETSUBAN | 6 | 0 | 1,200 | 0 | -1,200 | 0.0 |

## 直近アラート (24h・新しい順)
```
[10:47:38] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000239, "ks_stat": 0.255}
[10:40:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.481, "baseline_mean": 0.814, "baseline_stdev": 0.097, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -4.97}
[10:30:25] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000217, "ks_stat": 0.256}
[10:22:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.000248, "ks_stat": 0.254}
[10:01:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:44] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 7170, "roi_7d": 0.469, "sid": "S00"}
[10:01:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[09:53:05] CALIBRATION_DRIFT: {"avg_actual": 0.2273, "avg_pred": 0.4717, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 88, "overconf_pct": 51.8}
[09:39:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 610}
[09:38:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 615}
```

## 本日残レース: 172件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 20件 締切済
- 通知発射: scan=3 nid / final=1 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 213R | win | 1 | 0.5534 | 4.5 | 2.49 | 200 | scan=3.3 drift=+36.4% | 09:21:32 |
| S00 | 1710R | win | 1 | 0.5719 | 5.6 | 3.20 | 300 | scan=8.2 drift=-31.7% | 15:24:21 |
| S00 | 038R | win | 1 | 0.4989 | 17.2 | 8.58 | 300 | scan=5.2 drift=+230.8% | 14:21:41 |
| S00 | 178R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 14:21:33 |
| S00 | 028R | win | 1 | 0.4111 | 11.5 | 4.73 | 300 | scan=11.0 drift=+4.5% | 14:13:32 |
| S02_TETSUBAN | 2111R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.6 drift=-15.4% | 13:20:36 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=3.8 drift=-2.6% | 13:11:27 |
| S00 | 176R | win | 1 | 0.3177 | 9.7 | 3.08 | 300 | scan=9.3 drift=+4.3% | 13:08:21 |
| S00 | 022R | win | 1 | 0.5174 | 4.9 | 2.54 | 300 | scan=10.5 drift=-53.3% | 11:13:21 |
| S00 | 031R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=- drift=- | 11:11:51 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +27.8% | -53.3% | +482.2% | 17 | 7 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 497.4s |
| **Latency** (scan→final max) | 654.8s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 375 | 0.4789 | 0.2747 | +0.2042 | 🟡+43% | 0.2416 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4396 | 0.2530 | 0.2266 | 🔴-0.20 | 0.653 |
| S01_NAKAANA1 | win | 136 | 0.4925 | 0.2941 | 0.2438 | 🔴-0.17 | 0.777 |
| S02_TETSUBAN | win | 73 | 0.5429 | 0.2877 | 0.2718 | 🔴-0.33 | 0.452 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 124 | 0.4236 | 0.2177 | 🔴+0.2059 |
| 0.50+ | 225 | 0.5436 | 0.3200 | 🔴+0.2236 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 99 | 0.725 |
| win | <10.0 | ✅learned | 58 | 0.493 |
| win | <20.0 | ✅learned | 17 | 0.211 |
| win | <50.0 | ⚠️fallback | 2 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-28T10:50:01.942405+09:00_