# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-18T14:10:01.636548+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-08-18T14:03:41]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×21  [2026-08-18T14:03:41]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-08-18T14:03:41]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×16  [2026-08-18T13:54:43]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-08-18T13:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-18T13:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-08-18T11:59:37]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-08-18T11:49:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-18T06:00:19]
- key: `ORPHAN_SCAN|205 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S00: n=166 hit%=22.9% hit_CI[Bonf]=[14.9,33.5]% ROI=0.64 ROI_boot95=[0.43,0.86]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=22.7% hit_CI[Bonf]=[14.8,33.0]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=47.3% hit_CI[Bonf]=[31.7,63.5]% ROI=0.73 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.65 (コスト 10,400/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.83MB / last modified 2026-08-18T14:09:04.736322+09:00

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
arsed
2026-08-18 14:07:49,870 [INFO] scraper: odds2t: 30/30 parsed
2026-08-18 14:07:49,871 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 14:07:50,941 [INFO] scraper: odds_win: 4/6 parsed
2026-08-18 14:07:50,942 [INFO] scraper: fetch_race 10/12: boats=6 odds=189/191
2026-08-18 14:07:50,945 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 14:07:50,945 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-18 14:07:50,951 [INFO] run_cycle: fetched 10/12 [scan]: 154 combos
2026-08-18 14:07:54,468 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 14:07:55,594 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 14:07:56,703 [INFO] scraper: odds2t: 28/30 parsed
2026-08-18 14:07:56,704 [INFO] scraper: odds2f: 13/15 parsed
2026-08-18 14:07:57,785 [INFO] scraper: odds_win: 2/6 parsed
2026-08-18 14:07:57,785 [INFO] scraper: fetch_race 17/8: boats=6 odds=183/191
2026-08-18 14:07:57,788 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 14:07:57,788 [INFO] predictor: combos: {'win': 2, '2t': 28, '3t': 120}
2026-08-18 14:07:57,793 [INFO] run_cycle: fetched 17/8 [scan]: 150 combos
2026-08-18 14:07:58,010 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-18 14:08:02,797 [INFO] run_cycle: === run_cycle 14:08:02 ===
2026-08-18 14:08:02,797 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-18 14:08:02,798 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-18 14:08:02,841 [INFO] predictor: Models loaded OK
2026-08-18 14:08:03,162 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-18 14:09:03,873 [INFO] run_cycle: === run_cycle 14:09:03 ===
2026-08-18 14:09:03,873 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-18 14:09:03,873 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-18 14:09:03,924 [INFO] predictor: Models loaded OK
2026-08-18 14:09:04,140 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 21, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 211
  CIRCUIT_BREAKER_NO_ACTION: 51
  CIRCUIT_BREAKER_TRIP: 45
  FINAL_MISSING: 32
  ANOMALY_SCAN_FINAL_RATIO: 29
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 11 | 13,500 | 11,970 | -1,530 | 0.887 |
| S01_NAKAANA1 | 46 | 13 | 9,200 | 10,160 | +960 | 1.104 |
| S02_TETSUBAN | 24 | 9 | 4,800 | 2,640 | -2,160 | 0.55 |

## 直近アラート (24h・新しい順)
```
[14:08:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1078}
[14:07:58] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1073}
[14:06:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1078}
[14:05:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[14:04:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1055}
[14:03:39] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[14:03:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:03:39] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:03:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1047}
```

## 本日残レース: 67件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 77件 締切済
- 通知発射: scan=17 nid / final=18 nid / result=10 nid
- predictions: 12 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 098R | win | 1 | 0.4111 | 7.6 | 3.12 | 300 | scan=5.8 drift=+31.0% | 13:51:19 |
| S00 | 117R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=5.2 drift=+28.8% | 13:34:18 |
| S02_TETSUBAN | 097R | win | 1 | 0.5123 | 2.8 | 1.43 | 200 | scan=2.6 drift=+7.7% | 13:17:31 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4019 | 3.8 | 1.53 | 200 | scan=- drift=- | 12:22:19 |
| S01_NAKAANA1 | 052R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.0 drift=+0.0% | 12:02:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 11:59:20 |
| S00 | 114R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.5 drift=+0.0% | 11:59:18 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.5 drift=+31.4% | 11:30:21 |
| S00 | 147R | win | 1 | 0.5174 | 7.0 | 3.62 | 300 | scan=8.2 drift=-14.6% | 11:24:18 |
| S01_NAKAANA1 | 162R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 11:07:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +6.2% | -62.9% | +207.5% | 15 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.1s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 411 | 0.4664 | 0.2774 | +0.1890 | 🟡+40% | 0.2373 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4155 | 0.2364 | 0.2199 | 🔴-0.22 | 0.738 |
| S01_NAKAANA1 | win | 173 | 0.4876 | 0.2312 | 0.2505 | 🔴-0.41 | 0.802 |
| S02_TETSUBAN | win | 73 | 0.5313 | 0.4795 | 0.2456 | ✅+0.02 | 0.741 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 11 | 0.1843 | 0.0909 | 🔴+0.0934 |
| 0.20-0.30 | 8 | 0.2246 | 0.3750 | 🔴-0.1504 |
| 0.30-0.50 | 157 | 0.4149 | 0.2357 | 🔴+0.1793 |
| 0.50+ | 224 | 0.5424 | 0.3214 | 🔴+0.2209 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 112 | 0.765 |
| win | <5.0 | ✅learned | 196 | 0.755 |
| win | <10.0 | ✅learned | 97 | 0.447 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-18T14:10:01.636548+09:00_