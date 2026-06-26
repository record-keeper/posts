# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-26T12:00:02.133953+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×27 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×79 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×27 (24h)
- 🔴 CALIBRATION_DRIFT×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×6  [2026-06-26T11:54:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-06-26T11:30:50]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×58  [2026-06-26T11:01:44]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×67  [2026-06-26T11:01:44]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×116  [2026-06-26T11:01:44]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-06-26T11:01:44]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×49  [2026-06-26T11:01:44]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-26T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-26T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-26T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1802 actual=0.3750 gap=-0.1948`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=34 hit%=26.5% ROI=0.84 (コスト 8,200/回収 6,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S00: n=160 hit%=24.4% hit_CI[Bonf]=[16.0,35.3]% ROI=0.64 ROI_boot95=[0.45,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=137 hit%=30.7% hit_CI[Bonf]=[20.7,42.9]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-26T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=137<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-26T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=31.6% hit_CI[Bonf]=[18.7,48.1]% ROI=0.53 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-26T06:00:13]
- key: `ORPHAN_SCAN|152 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-26T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=19.4% ROI=0.65 (コスト 8,800/回収 5,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.05MB / last modified 2026-06-26T12:00:06.259173+09:00

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
rsed
2026-06-26 11:58:22,467 [INFO] scraper: fetch_race 16/3: boats=6 odds=191/191
2026-06-26 11:58:22,479 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 11:58:22,479 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-26 11:58:22,487 [INFO] run_cycle: fetched 16/3 [final]: 156 combos
2026-06-26 11:58:26,210 [INFO] scraper: odds3t: 120/120 parsed
2026-06-26 11:58:27,335 [INFO] scraper: odds3f: 17/20 parsed
2026-06-26 11:58:28,424 [INFO] scraper: odds2t: 29/30 parsed
2026-06-26 11:58:28,425 [INFO] scraper: odds2f: 15/15 parsed
2026-06-26 11:58:29,541 [INFO] scraper: odds_win: 3/6 parsed
2026-06-26 11:58:29,542 [INFO] scraper: fetch_race 17/4: boats=6 odds=184/191
2026-06-26 11:58:29,552 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 11:58:29,552 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-06-26 11:58:29,558 [INFO] run_cycle: fetched 17/4 [scan]: 152 combos
2026-06-26 11:58:29,693 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-26 11:59:05,941 [INFO] run_cycle: === run_cycle 11:59:05 ===
2026-06-26 11:59:05,941 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-26 11:59:05,941 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-26 11:59:05,988 [INFO] predictor: Models loaded OK
2026-06-26 11:59:18,498 [INFO] scraper: odds3t: 120/120 parsed
2026-06-26 11:59:19,573 [INFO] scraper: odds3f: 20/20 parsed
2026-06-26 11:59:20,716 [INFO] scraper: odds2t: 29/30 parsed
2026-06-26 11:59:20,717 [INFO] scraper: odds2f: 12/15 parsed
2026-06-26 11:59:21,850 [INFO] scraper: odds_win: 5/6 parsed
2026-06-26 11:59:21,850 [INFO] scraper: fetch_race 03/3: boats=6 odds=186/191
2026-06-26 11:59:21,863 [INFO] predictor: CALIBRATION_MODE=on
2026-06-26 11:59:21,863 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-06-26 11:59:21,870 [INFO] run_cycle: fetched 03/3 [scan]: 154 combos
2026-06-26 11:59:22,073 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 11, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 263
  FINAL_MISSING: 79
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 27
  CALIBRATION_DRIFT: 25
  STRATEGY_CI_FAIL: 17
  KS_ODDS_DRIFT: 16
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 52 | 9 | 15,600 | 6,240 | -9,360 | 0.4 |
| S01_NAKAANA1 | 39 | 11 | 7,800 | 5,440 | -2,360 | 0.697 |
| S02_TETSUBAN | 10 | 2 | 2,000 | 1,020 | -980 | 0.51 |

## 直近アラート (24h・新しい順)
```
[11:59:22] CALIBRATION_DRIFT: {"avg_actual": 0.2268, "avg_pred": 0.4712, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 51.9}
[11:59:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1199}
[11:58:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1200}
[11:57:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1192}
[11:56:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1179}
[11:55:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1187}
[11:54:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1184}
[11:53:46] CIRCUIT_BREAKER_TRIP: {"cost": 15600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 6240, "roi_7d": 0.4, "sid": "S00"}
[11:53:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.158, "baseline_mean": 0.825, "baseline_stdev": 0.074, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 6, "z_score": -2.14}
[11:51:30] CIRCUIT_BREAKER_TRIP: {"cost": 7800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 5440, "roi_7d": 0.697, "sid": "S01_NAKAANA1"}
```

## 本日残レース: 138件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 42件 締切済
- 通知発射: scan=6 nid / final=6 nid / result=0 nid
- predictions: 4 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 041R | win | 1 | 0.5719 | 18.1 | 10.35 | 300 | scan=7.3 drift=+147.9% | 11:53:21 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4998 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:51:22 |
| S00 | 134R | win | 1 | 0.4998 | 15.0 | 7.50 | 300 | scan=10.5 drift=+42.9% | 11:50:23 |
| S01_NAKAANA1 | 173R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 11:36:24 |
| S01_NAKAANA1 | 076R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=4.4 drift=-15.9% | 18:05:23 |
| S01_NAKAANA1 | 075R | win | 1 | 0.5020 | 3.7 | 1.86 | 200 | scan=- drift=- | 17:40:33 |
| S01_NAKAANA1 | 049R | win | 1 | 0.5334 | 3.8 | 2.03 | 200 | scan=- drift=- | 16:02:21 |
| S01_NAKAANA1 | 0311R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 15:50:23 |
| S02_TETSUBAN | 1310R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=- drift=- | 15:11:37 |
| S00 | 225R | win | 1 | 0.4111 | 45.0 | 18.50 | 300 | scan=- drift=- | 14:23:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +18.5% | -49.2% | +482.2% | 22 | 8 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 356.5s |
| **Latency** (scan→final max) | 610.2s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 372 | 0.4777 | 0.2796 | +0.1981 | 🟡+42% | 0.2413 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4363 | 0.2437 | 0.2260 | 🔴-0.23 | 0.643 |
| S01_NAKAANA1 | win | 137 | 0.4911 | 0.3066 | 0.2426 | 🔴-0.14 | 0.803 |
| S02_TETSUBAN | win | 75 | 0.5413 | 0.3067 | 0.2714 | 🔴-0.28 | 0.508 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 122 | 0.4217 | 0.2213 | 🔴+0.2004 |
| 0.50+ | 224 | 0.5430 | 0.3259 | 🔴+0.2171 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 95 | 0.727 |
| win | <10.0 | ✅learned | 57 | 0.496 |
| win | <20.0 | ✅learned | 15 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-26T12:00:02.133953+09:00_