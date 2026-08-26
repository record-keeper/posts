# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-26T21:10:01.370234+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×18 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×71 (24h)
- 🔴 STRATEGY_CI_FAIL×18 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×13 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-26T21:07:07]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×3  [2026-08-26T21:07:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-26T21:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-08-26T16:07:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×4  [2026-08-26T16:04:50]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×5  [2026-08-26T14:55:33]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×1  [2026-08-26T14:36:04]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

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


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.57MB / last modified 2026-08-26T21:09:04.307320+09:00

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
22 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 21:05:04,422 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 21:05:04,484 [INFO] predictor: Models loaded OK
2026-08-26 21:05:04,487 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-26 21:06:04,661 [INFO] run_cycle: === run_cycle 21:06:04 ===
2026-08-26 21:06:04,661 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 21:06:04,661 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 21:06:04,693 [INFO] predictor: Models loaded OK
2026-08-26 21:06:04,696 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-26 21:07:04,950 [INFO] run_cycle: === run_cycle 21:07:04 ===
2026-08-26 21:07:04,950 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 21:07:04,950 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 21:07:04,997 [INFO] predictor: Models loaded OK
2026-08-26 21:07:05,002 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-26 21:08:04,851 [INFO] run_cycle: === run_cycle 21:08:04 ===
2026-08-26 21:08:04,851 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 21:08:04,851 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 21:08:04,899 [INFO] predictor: Models loaded OK
2026-08-26 21:08:04,903 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-26 21:09:03,777 [INFO] run_cycle: === run_cycle 21:09:03 ===
2026-08-26 21:09:03,777 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-26 21:09:03,777 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-26 21:09:03,855 [INFO] predictor: Models loaded OK
2026-08-26 21:09:03,859 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 90
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 90
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 20, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 179
  FINAL_MISSING: 71
  ANOMALY_SCAN_FINAL_RATIO: 27
  CIRCUIT_BREAKER_NO_ACTION: 18
  STRATEGY_CI_FAIL: 18
  CIRCUIT_BREAKER_TRIP: 13
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_ODDS_SHIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 11 | 12,600 | 9,330 | -3,270 | 0.74 |
| S01_NAKAANA1 | 49 | 15 | 9,800 | 7,560 | -2,240 | 0.771 |
| S02_TETSUBAN | 19 | 7 | 3,800 | 2,820 | -980 | 0.742 |

## 直近アラート (24h・新しい順)
```
[21:07:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:07:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[20:56:03] FINAL_MISSING: {"deadline": "2026-08-26T13:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082617061322", "sid": "S00"}
[20:38:18] FINAL_MISSING: {"deadline": "2026-08-26T20:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082620112008", "sid": "S00"}
[20:36:03] FINAL_MISSING: {"deadline": "2026-08-26T11:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082611021102", "sid": "S00"}
[20:33:20] FINAL_MISSING: {"deadline": "2026-08-26T08:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082614020858", "sid": "S00"}
[20:26:18] FINAL_MISSING: {"deadline": "2026-08-26T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082614040950", "sid": "S00"}
[20:21:19] FINAL_MISSING: {"deadline": "2026-08-26T17:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082615071751", "sid": "S00"}
[20:12:04] FINAL_MISSING: {"deadline": "2026-08-26T11:35:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082610071135", "sid": "S00"}
[20:07:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 168件 締切済
- 通知発射: scan=33 nid / final=34 nid / result=19 nid
- predictions: 20 / うち結果DB記録済: 20
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 2011R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 20:05:42 |
| S02_TETSUBAN | 209R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.4 drift=-8.3% | 19:05:31 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.1 drift=+12.9% | 16:32:29 |
| S00 | 179R | win | 1 | 0.5174 | 7.0 | 3.62 | 300 | scan=- drift=- | 15:03:18 |
| S02_TETSUBAN | 119R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 14:34:20 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.0 drift=+23.3% | 13:45:20 |
| S01_NAKAANA1 | 1010R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=3.0 drift=+20.0% | 13:10:21 |
| S01_NAKAANA1 | 035R | win | 1 | 0.5476 | 4.0 | 2.19 | 200 | scan=3.3 drift=+21.2% | 12:59:19 |
| S00 | 1410R | win | 1 | 0.4111 | 17.2 | 7.07 | 300 | scan=- drift=- | 12:54:26 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5891 | 3.6 | 2.12 | 200 | scan=4.6 drift=-21.7% | 12:50:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +3.4% | -79.6% | +320.7% | 27 | 10 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 526.6s |
| **Latency** (scan→final max) | 618.8s |
| **Traffic** (notifications 24h) | 90 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,000円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 436 | 0.4712 | 0.2936 | +0.1776 | 🟡+38% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4180 | 0.2711 | 0.2221 | 🔴-0.12 | 0.862 |
| S01_NAKAANA1 | win | 189 | 0.4890 | 0.2593 | 0.2489 | 🔴-0.30 | 0.834 |
| S02_TETSUBAN | win | 81 | 0.5386 | 0.4198 | 0.2561 | 🔴-0.05 | 0.688 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 10 | 0.1815 | 0.2000 | ✅-0.0185 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 155 | 0.4114 | 0.2323 | 🔴+0.1791 |
| 0.50+ | 250 | 0.5451 | 0.3440 | 🔴+0.2011 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 120 | 0.775 |
| win | <5.0 | ✅learned | 220 | 0.749 |
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
_auto-generated by claude_snapshot.py at 2026-08-26T21:10:01.370234+09:00_