# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-26T12:30:01.510040+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×18 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×69 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-08-26T12:23:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×28  [2026-08-26T12:02:33]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×28  [2026-08-26T12:02:33]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×28  [2026-08-26T12:02:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×55  [2026-08-26T11:15:44]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-26T11:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_ODDS_SHIFT  ×14  [2026-08-26T10:47:29]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_BET_VOLUME_DROP  ×18  [2026-08-26T10:00:22]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-08-26T06:00:09]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.3333 gap=-0.1082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=187 hit%=27.3% hit_CI[Bonf]=[19.0,37.5]% ROI=0.85 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-26T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=187<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-26T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1799 actual=0.2222 gap=-0.0423`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S00: n=161 hit%=26.7% hit_CI[Bonf]=[18.0,37.7]% ROI=0.83 ROI_boot95=[0.57,1.12]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-26T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=41.0% hit_CI[Bonf]=[26.6,57.2]% ROI=0.65 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=18.4% ROI=0.58 (コスト 11,000/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-26T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=37.5% ROI=1.00 (コスト 9,100/回収 9,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.53MB / last modified 2026-08-26T12:30:05.216043+09:00

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
sed
2026-08-26 12:28:19,482 [INFO] scraper: fetch_race 08/5: boats=6 odds=189/191
2026-08-26 12:28:19,485 [INFO] predictor: CALIBRATION_MODE=on
2026-08-26 12:28:19,486 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-26 12:28:19,489 [INFO] run_cycle: fetched 08/5 [final]: 154 combos
2026-08-26 12:28:23,110 [INFO] scraper: odds3t: 120/120 parsed
2026-08-26 12:28:24,337 [INFO] scraper: odds3f: 20/20 parsed
2026-08-26 12:28:25,446 [INFO] scraper: odds2t: 30/30 parsed
2026-08-26 12:28:25,448 [INFO] scraper: odds2f: 15/15 parsed
2026-08-26 12:28:26,657 [INFO] scraper: odds_win: 5/6 parsed
2026-08-26 12:28:26,657 [INFO] scraper: fetch_race 03/4: boats=6 odds=190/191
2026-08-26 12:28:26,660 [INFO] predictor: CALIBRATION_MODE=on
2026-08-26 12:28:26,660 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-26 12:28:26,664 [INFO] run_cycle: fetched 03/4 [scan]: 155 combos
2026-08-26 12:28:26,868 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-26 12:29:03,683 [INFO] run_cycle: === run_cycle 12:29:03 ===
2026-08-26 12:29:03,683 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 12:29:03,683 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 12:29:03,712 [INFO] predictor: Models loaded OK
2026-08-26 12:29:16,250 [INFO] scraper: odds3t: 120/120 parsed
2026-08-26 12:29:17,359 [INFO] scraper: odds3f: 20/20 parsed
2026-08-26 12:29:18,470 [INFO] scraper: odds2t: 30/30 parsed
2026-08-26 12:29:18,471 [INFO] scraper: odds2f: 15/15 parsed
2026-08-26 12:29:19,574 [INFO] scraper: odds_win: 4/6 parsed
2026-08-26 12:29:19,574 [INFO] scraper: fetch_race 08/5: boats=6 odds=189/191
2026-08-26 12:29:19,577 [INFO] predictor: CALIBRATION_MODE=on
2026-08-26 12:29:19,577 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-26 12:29:19,581 [INFO] run_cycle: fetched 08/5 [final]: 154 combos
2026-08-26 12:29:19,871 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 60
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 60
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 13, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 147
  FINAL_MISSING: 69
  CIRCUIT_BREAKER_TRIP: 18
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 16
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_ODDS_SHIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 12 | 12,600 | 11,280 | -1,320 | 0.895 |
| S01_NAKAANA1 | 46 | 15 | 9,200 | 7,360 | -1,840 | 0.8 |
| S02_TETSUBAN | 20 | 6 | 4,000 | 2,380 | -1,620 | 0.595 |

## 直近アラート (24h・新しい順)
```
[12:29:19] FINAL_MISSING: {"deadline": "2026-08-26T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082614020858", "sid": "S00"}
[12:25:47] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.228, "baseline_mean": 0.812, "baseline_stdev": 0.055, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.583, "today_scan_count": 12, "z_score": -4.16}
[12:21:28] FINAL_MISSING: {"deadline": "2026-08-26T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082614040950", "sid": "S00"}
[12:15:33] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.175, "baseline_mean": 0.812, "baseline_stdev": 0.055, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 11, "z_score": -3.19}
[12:09:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1270}
[12:08:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1258}
[12:06:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1271}
[12:05:45] FINAL_MISSING: {"deadline": "2026-08-26T11:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082610071135", "sid": "S00"}
[12:05:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.266, "baseline_mean": 0.812, "baseline_stdev": 0.055, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.545, "today_scan_count": 11, "z_score": -4.85}
[12:04:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1249}
```

## 本日残レース: 113件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 55件 締切済
- 通知発射: scan=12 nid / final=11 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 108R | win | 1 | 0.1957 | 10.2 | 2.00 | 300 | scan=11.3 drift=-9.7% | 12:04:29 |
| S00 | 094R | win | 1 | 0.5123 | 4.2 | 2.15 | 300 | scan=- drift=- | 11:51:19 |
| S00 | 133R | win | 1 | 0.2290 | 4.8 | 1.10 | 300 | scan=6.3 drift=-23.8% | 11:19:29 |
| S00 | 031R | win | 1 | 0.4111 | 4.2 | 1.73 | 300 | scan=- drift=- | 11:11:37 |
| S00 | 106R | win | 1 | 0.4111 | 8.5 | 3.49 | 300 | scan=8.7 drift=-2.3% | 11:01:43 |
| S00 | 146R | win | 1 | 0.4111 | 35.0 | 14.39 | 300 | scan=- drift=- | 10:47:20 |
| S00 | 131R | win | 1 | 0.4111 | 5.8 | 2.38 | 300 | scan=6.7 drift=-13.4% | 10:32:25 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5746 | 4.3 | 2.47 | 200 | scan=- drift=- | 10:18:19 |
| S02_TETSUBAN | 208R | win | 1 | 0.5640 | 2.0 | 1.13 | 200 | scan=2.8 drift=-28.6% | 18:34:30 |
| S00 | 228R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=- drift=- | 15:43:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +5.4% | -79.6% | +320.7% | 25 | 10 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 533.5s |
| **Latency** (scan→final max) | 618.8s |
| **Traffic** (notifications 24h) | 60 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 430 | 0.4708 | 0.2907 | +0.1801 | 🟡+38% | 0.2403 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4194 | 0.2651 | 0.2231 | 🔴-0.15 | 0.837 |
| S01_NAKAANA1 | win | 186 | 0.4887 | 0.2634 | 0.2487 | 🔴-0.28 | 0.836 |
| S02_TETSUBAN | win | 78 | 0.5374 | 0.4103 | 0.2565 | 🔴-0.06 | 0.653 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 9 | 0.1799 | 0.2222 | ✅-0.0423 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 154 | 0.4108 | 0.2338 | 🔴+0.1771 |
| 0.50+ | 246 | 0.5446 | 0.3374 | 🔴+0.2072 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 118 | 0.77 |
| win | <5.0 | ✅learned | 218 | 0.748 |
| win | <10.0 | ✅learned | 105 | 0.454 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-26T12:30:01.510040+09:00_