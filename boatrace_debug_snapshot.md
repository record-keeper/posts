# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-25T14:40:02.297784+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×28 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×4 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×13  [2026-06-25T14:27:07]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 KS_ODDS_DRIFT  ×17  [2026-06-25T14:23:36]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CIRCUIT_BREAKER_TRIP  ×36  [2026-06-25T14:03:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×72  [2026-06-25T14:03:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×36  [2026-06-25T14:03:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-25T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-25T14:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×49  [2026-06-25T13:23:29]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-06-25T12:44:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-06-25T12:30:08]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×1  [2026-06-25T11:00:37]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3217 actual=0.2381 gap=+0.0837`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-25T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=21.9% ROI=0.72 (コスト 9,100/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1802 actual=0.3750 gap=-0.1948`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-25T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.0833 gap=+0.1410`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-25T06:00:11]
- key: `ROI_STAT|S00: n=158 hit%=25.3% hit_CI[Bonf]=[16.7,36.4]% ROI=0.67 ROI_boot95=[0.47,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-25T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=158<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-25T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=31.3% hit_CI[Bonf]=[21.2,43.7]% ROI=0.84 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.94MB / last modified 2026-06-25T14:39:36.478910+09:00

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
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-25 14:39:06,765 [INFO] predictor: Models loaded OK
2026-06-25 14:39:19,192 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 14:39:20,265 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 14:39:21,348 [INFO] scraper: odds2t: 30/30 parsed
2026-06-25 14:39:21,349 [INFO] scraper: odds2f: 15/15 parsed
2026-06-25 14:39:22,451 [INFO] scraper: odds_win: 4/6 parsed
2026-06-25 14:39:22,451 [INFO] scraper: fetch_race 08/9: boats=6 odds=189/191
2026-06-25 14:39:22,456 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 14:39:22,456 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-25 14:39:22,460 [INFO] run_cycle: fetched 08/9 [final]: 154 combos
2026-06-25 14:39:25,987 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 14:39:27,097 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 14:39:28,234 [INFO] scraper: odds2t: 30/30 parsed
2026-06-25 14:39:28,236 [INFO] scraper: odds2f: 15/15 parsed
2026-06-25 14:39:29,331 [INFO] scraper: odds_win: 6/6 parsed
2026-06-25 14:39:29,331 [INFO] scraper: fetch_race 14/9: boats=6 odds=191/191
2026-06-25 14:39:29,340 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 14:39:29,340 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-25 14:39:29,350 [INFO] run_cycle: fetched 14/9 [scan]: 156 combos
2026-06-25 14:39:32,818 [INFO] scraper: odds3t: 120/120 parsed
2026-06-25 14:39:33,944 [INFO] scraper: odds3f: 20/20 parsed
2026-06-25 14:39:35,056 [INFO] scraper: odds2t: 29/30 parsed
2026-06-25 14:39:35,057 [INFO] scraper: odds2f: 13/15 parsed
2026-06-25 14:39:36,139 [INFO] scraper: odds_win: 2/6 parsed
2026-06-25 14:39:36,139 [INFO] scraper: fetch_race 03/9: boats=6 odds=184/191
2026-06-25 14:39:36,148 [INFO] predictor: CALIBRATION_MODE=on
2026-06-25 14:39:36,150 [INFO] predictor: combos: {'win': 2, '2t': 29, '3t': 120}
2026-06-25 14:39:36,159 [INFO] run_cycle: fetched 03/9 [scan]: 151 combos
2026-06-25 14:39:36,329 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 53
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 53
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 10, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 239
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 28
  FINAL_MISSING: 28
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 4
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 2
  KS_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 51 | 9 | 15,300 | 6,690 | -8,610 | 0.437 |
| S01_NAKAANA1 | 34 | 10 | 6,800 | 5,160 | -1,640 | 0.759 |
| S02_TETSUBAN | 11 | 3 | 2,200 | 1,260 | -940 | 0.573 |

## 直近アラート (24h・新しい順)
```
[14:30:56] FINAL_MISSING: {"deadline": "2026-06-25T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062521020858", "sid": "S00"}
[14:25:48] CALIBRATION_DRIFT: {"avg_actual": 0.234, "avg_pred": 0.4685, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 94, "overconf_pct": 50.0}
[14:23:36] CIRCUIT_BREAKER_TRIP: {"cost": 15300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 6690, "roi_7d": 0.437, "sid": "S00"}
[14:23:36] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.008872, "ks_stat": 0.192}
[14:18:46] CIRCUIT_BREAKER_TRIP: {"cost": 15000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 50, "payout": 6690, "roi_7d": 0.446, "sid": "S00"}
[14:10:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1301}
[14:09:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1299}
[14:08:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1291}
[14:07:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1296}
[14:06:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1290}
```

## 本日残レース: 89件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 103件 締切済
- 通知発射: scan=11 nid / final=13 nid / result=6 nid
- predictions: 8 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 225R | win | 1 | 0.4111 | 45.0 | 18.50 | 300 | scan=- drift=- | 14:23:33 |
| S00 | 067R | win | 1 | 0.5735 | 12.0 | 6.88 | 300 | scan=- drift=- | 14:18:32 |
| S00 | 037R | win | 1 | 0.5174 | 5.6 | 2.90 | 300 | scan=9.0 drift=-37.8% | 13:53:27 |
| S00 | 188R | win | 1 | 0.4111 | 10.5 | 4.32 | 300 | scan=- drift=- | 11:59:44 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4920 | 3.3 | 1.62 | 200 | scan=- drift=- | 11:52:22 |
| S00 | 032R | win | 1 | 0.5350 | 9.0 | 4.81 | 300 | scan=9.0 drift=+0.0% | 11:38:21 |
| S00 | 133R | win | 1 | 0.3177 | 13.5 | 4.29 | 300 | scan=- drift=- | 11:24:20 |
| S00 | 132R | win | 1 | 0.6040 | 5.5 | 3.32 | 300 | scan=6.7 drift=-17.9% | 11:01:20 |
| S00 | 227R | win | 1 | 0.5269 | 7.1 | 3.74 | 300 | scan=4.1 drift=+73.2% | 15:35:45 |
| S00 | 048R | win | 1 | 0.5476 | 6.7 | 3.67 | 300 | scan=13.2 drift=-49.2% | 15:29:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +15.5% | -61.4% | +482.2% | 22 | 9 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 489.0s |
| **Latency** (scan→final max) | 610.2s |
| **Traffic** (notifications 24h) | 53 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 369 | 0.4759 | 0.2818 | +0.1941 | 🟡+41% | 0.2414 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 160 | 0.4341 | 0.2437 | 0.2266 | 🔴-0.23 | 0.647 |
| S01_NAKAANA1 | win | 134 | 0.4898 | 0.3060 | 0.2429 | 🔴-0.14 | 0.809 |
| S02_TETSUBAN | win | 75 | 0.5403 | 0.3200 | 0.2703 | 🔴-0.24 | 0.537 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 12 | 0.2243 | 0.0833 | 🔴+0.1410 |
| 0.30-0.50 | 124 | 0.4222 | 0.2258 | 🔴+0.1964 |
| 0.50+ | 218 | 0.5433 | 0.3257 | 🔴+0.2176 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 93 | 0.732 |
| win | <10.0 | ✅learned | 57 | 0.496 |
| win | <20.0 | ✅learned | 15 | 0.207 |
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
_auto-generated by claude_snapshot.py at 2026-06-25T14:40:02.297784+09:00_