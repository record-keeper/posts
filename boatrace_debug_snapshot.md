# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-27T11:50:01.642177+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×42 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CALIBRATION_DRIFT×42 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×37 (24h)
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-27T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 KS_ODDS_DRIFT  ×36  [2026-06-27T11:14:40]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×32  [2026-06-27T11:07:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×32  [2026-06-27T11:03:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CALIBRATION_DRIFT  ×48  [2026-06-27T11:01:22]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×48  [2026-06-27T11:01:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×96  [2026-06-27T11:01:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-06-27T11:01:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-06-27T11:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-27T06:00:09]
- key: `ORPHAN_SCAN|149 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-27T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 8,500/回収 4,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-27T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2250 actual=0.0000 gap=+0.2250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S00: n=164 hit%=24.4% hit_CI[Bonf]=[16.1,35.2]% ROI=0.63 ROI_boot95=[0.45,0.83]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=145 hit%=30.3% hit_CI[Bonf]=[20.6,42.2]% ROI=0.80 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-27T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=145<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-27T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=29.7% hit_CI[Bonf]=[17.1,46.5]% ROI=0.46 ROI_boot95=[0.2`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-27T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=18.2% ROI=0.61 (コスト 9,400/回収 5,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 6.17MB / last modified 2026-06-27T11:49:20.961530+09:00

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
 11:47:41,290 [INFO] notifier: Discord notify OK (status=204)
2026-06-27 11:47:41,641 [INFO] notifier: Discord notify OK (status=204)
2026-06-27 11:47:41,646 [INFO] run_cycle: SCAN S01_NAKAANA1 唐津8R A
2026-06-27 11:47:41,743 [INFO] run_cycle: run_cycle done: 1 notifications
2026-06-27 11:48:06,158 [INFO] run_cycle: === run_cycle 11:48:06 ===
2026-06-27 11:48:06,158 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 11:48:06,160 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 11:48:06,208 [INFO] predictor: Models loaded OK
2026-06-27 11:48:17,639 [WARNING] scraper: beforeinfo parse failed: jcd=04 rno=1
2026-06-27 11:48:17,639 [WARNING] run_cycle: fetch None: 04/1
2026-06-27 11:48:21,104 [INFO] scraper: odds3t: 120/120 parsed
2026-06-27 11:48:22,204 [INFO] scraper: odds3f: 19/20 parsed
2026-06-27 11:48:23,394 [INFO] scraper: odds2t: 24/30 parsed
2026-06-27 11:48:23,396 [INFO] scraper: odds2f: 12/15 parsed
2026-06-27 11:48:24,572 [INFO] scraper: odds_win: 4/6 parsed
2026-06-27 11:48:24,572 [INFO] scraper: fetch_race 18/8: boats=6 odds=179/191
2026-06-27 11:48:24,584 [INFO] predictor: CALIBRATION_MODE=on
2026-06-27 11:48:24,584 [INFO] predictor: combos: {'win': 4, '2t': 24, '3t': 120}
2026-06-27 11:48:24,589 [INFO] run_cycle: fetched 18/8 [scan]: 148 combos
2026-06-27 11:48:24,694 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-27 11:49:06,383 [INFO] run_cycle: === run_cycle 11:49:06 ===
2026-06-27 11:49:06,383 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-27 11:49:06,383 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-27 11:49:06,431 [INFO] predictor: Models loaded OK
2026-06-27 11:49:17,860 [WARNING] scraper: beforeinfo parse failed: jcd=04 rno=1
2026-06-27 11:49:17,860 [WARNING] run_cycle: fetch None: 04/1
2026-06-27 11:49:18,066 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 17, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 154
  CALIBRATION_DRIFT: 42
  CIRCUIT_BREAKER_TRIP: 37
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  KS_ODDS_DRIFT: 5
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 53 | 10 | 15,900 | 6,810 | -9,090 | 0.428 |
| S01_NAKAANA1 | 34 | 10 | 6,800 | 5,360 | -1,440 | 0.788 |
| S02_TETSUBAN | 9 | 2 | 1,800 | 1,020 | -780 | 0.567 |

## 直近アラート (24h・新しい順)
```
[11:49:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1162}
[11:48:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1160}
[11:47:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1159}
[11:47:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.187, "baseline_mean": 0.853, "baseline_stdev": 0.067, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 6, "z_score": -2.8}
[11:46:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1163}
[11:45:52] CALIBRATION_DRIFT: {"avg_actual": 0.2292, "avg_pred": 0.4723, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 51.5}
[11:45:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1154}
[11:42:31] CIRCUIT_BREAKER_TRIP: {"cost": 15900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 6810, "roi_7d": 0.428, "sid": "S00"}
[11:42:31] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.006506, "ks_stat": 0.198}
[11:42:31] CALIBRATION_DRIFT: {"avg_actual": 0.2316, "avg_pred": 0.4718, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 95, "overconf_pct": 50.9}
```

## 本日残レース: 141件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 39件 締切済
- 通知発射: scan=6 nid / final=5 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 022R | win | 1 | 0.5174 | 4.9 | 2.54 | 300 | scan=10.5 drift=-53.3% | 11:13:21 |
| S00 | 031R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=- drift=- | 11:11:51 |
| S02_TETSUBAN | 079R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 19:22:23 |
| S01_NAKAANA1 | 126R | win | 1 | 0.5476 | 3.4 | 1.86 | 200 | scan=- drift=- | 17:53:22 |
| S00 | 015R | win | 1 | 0.3177 | 4.6 | 1.46 | 300 | scan=6.7 drift=-31.3% | 17:34:23 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=3.3 drift=+48.5% | 17:09:33 |
| S00 | 124R | win | 1 | 0.3177 | 5.4 | 1.72 | 300 | scan=- drift=- | 17:04:34 |
| S00 | 0410R | win | 1 | 0.5735 | 5.1 | 2.92 | 300 | scan=5.1 drift=+0.0% | 16:34:48 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5236 | 4.5 | 2.36 | 200 | scan=- drift=- | 15:59:21 |
| S01_NAKAANA1 | 0911R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:46:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +20.5% | -53.3% | +482.2% | 20 | 9 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 468.8s |
| **Latency** (scan→final max) | 654.8s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 383 | 0.4782 | 0.2794 | +0.1988 | 🟡+42% | 0.2401 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4374 | 0.2485 | 0.2245 | 🔴-0.20 | 0.638 |
| S01_NAKAANA1 | win | 145 | 0.4917 | 0.3034 | 0.2426 | 🔴-0.15 | 0.805 |
| S02_TETSUBAN | win | 73 | 0.5434 | 0.3014 | 0.2704 | 🔴-0.28 | 0.47 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1819 | 0.3333 | 🔴-0.1514 |
| 0.20-0.30 | 11 | 0.2250 | 0.0000 | 🔴+0.2250 |
| 0.30-0.50 | 125 | 0.4228 | 0.2160 | 🔴+0.2068 |
| 0.50+ | 231 | 0.5432 | 0.3290 | 🔴+0.2142 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 98 | 0.729 |
| win | <10.0 | ✅learned | 58 | 0.493 |
| win | <20.0 | ✅learned | 16 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-27T11:50:01.642177+09:00_