# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-28T01:40:01.752406+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🟡 FINAL_MISSING×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-28T00:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×44  [2026-10-27T23:16:05]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CIRCUIT_BREAKER_TRIP  ×52  [2026-10-27T23:08:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×104  [2026-10-27T23:08:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-10-27T23:08:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-27T23:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-10-27T14:35:16]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=73<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-27T06:00:22]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-27T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=50 hit%=26.0% ROI=0.83 (コスト 12,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=31.1% ROI=0.60 (コスト 11,000/回収 6,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-27T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2288 actual=0.2222 gap=+0.0066`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S00: n=189 hit%=30.2% hit_CI[Bonf]=[21.5,40.5]% ROI=0.82 ROI_boot95=[0.62,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=33.7% hit_CI[Bonf]=[24.7,44.0]% ROI=0.89 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-27T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=73 hit%=52.1% hit_CI[Bonf]=[35.9,67.8]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=27 hit%=44.4% ROI=1.24 (コスト 7,800/回収 9,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=41.9% ROI=1.13 (コスト 19,500/回収 22,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-27T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=66 hit%=31.8% ROI=0.85 (コスト 15,800/回収 13,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.96MB / last modified 2026-10-28T01:30:05.501086+09:00

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
95 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 23:55:03,695 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 23:55:03,725 [INFO] predictor: Models loaded OK
2026-10-27 23:55:03,727 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 23:56:04,094 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-27 23:56:04,094 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 23:56:04,094 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 23:56:04,138 [INFO] predictor: Models loaded OK
2026-10-27 23:56:04,142 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 23:57:03,636 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-10-27 23:57:03,636 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 23:57:03,636 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 23:57:03,683 [INFO] predictor: Models loaded OK
2026-10-27 23:57:03,687 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 23:58:03,582 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-10-27 23:58:03,582 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 23:58:03,582 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 23:58:03,623 [INFO] predictor: Models loaded OK
2026-10-27 23:58:03,627 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-27 23:59:03,817 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-10-27 23:59:03,817 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-27 23:59:03,817 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-27 23:59:03,861 [INFO] predictor: Models loaded OK
2026-10-27 23:59:03,865 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 93
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 93
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 22, 'scan': 34}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 26
  FINAL_MISSING: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCRAPER_FAILURE_BURST: 10
  ANOMALY_BET_VOLUME_SPIKE: 8
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 50 | 14 | 15,000 | 11,340 | -3,660 | 0.756 |
| S01_NAKAANA1 | 54 | 14 | 10,800 | 6,500 | -4,300 | 0.602 |
| S02_TETSUBAN | 12 | 6 | 2,400 | 4,600 | +2,200 | 1.917 |

## 直近アラート (24h・新しい順)
```
[23:48:04] FINAL_MISSING: {"deadline": "2026-10-27T20:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102701112016", "sid": "S00"}
[23:24:04] FINAL_MISSING: {"deadline": "2026-10-27T13:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102708081348", "sid": "S01_NAKAANA1"}
[23:24:04] FINAL_MISSING: {"deadline": "2026-10-27T16:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102701041651", "sid": "S00"}
[23:16:04] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 54, "payout": 6500, "roi_7d": 0.602, "sid": "S01_NAKAANA1"}
[23:07:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:07:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[23:07:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:00:08] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 14.9, "baseline_n_days": 7, "baseline_stdev": 3.1, "hour": 23, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 22, "z_score": 2.32}
[22:47:05] FINAL_MISSING: {"deadline": "2026-10-27T20:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102701112016", "sid": "S00"}
[22:23:04] FINAL_MISSING: {"deadline": "2026-10-27T13:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102708081348", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 0111R | win | 1 | 0.3177 | 3.6 | 1.14 | 200 | scan=4.6 drift=-21.7% | 20:13:21 |
| S00 | 078R | win | 1 | 0.5735 | 19.9 | 11.41 | 300 | scan=11.2 drift=+77.7% | 18:29:21 |
| S00 | 073R | win | 1 | 0.5174 | 9.7 | 5.02 | 300 | scan=7.5 drift=+29.3% | 16:08:32 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5334 | 3.9 | 2.08 | 200 | scan=4.7 drift=-17.0% | 16:03:20 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=- drift=- | 15:50:44 |
| S00 | 072R | win | 1 | 0.4111 | 9.0 | 3.70 | 300 | scan=6.0 drift=+50.0% | 15:41:20 |
| S02_TETSUBAN | 071R | win | 1 | 0.5476 | 2.5 | 1.37 | 200 | scan=2.2 drift=+13.6% | 15:16:20 |
| S00 | 059R | win | 1 | 0.4996 | 6.4 | 3.20 | 300 | scan=6.8 drift=-5.9% | 14:28:26 |
| S00 | 058R | win | 1 | 0.3599 | 6.7 | 2.41 | 300 | scan=9.7 drift=-30.9% | 14:02:19 |
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=2.3 drift=+0.0% | 13:34:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +8.1% | -77.4% | +111.7% | 17 | 5 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 428.2s |
| **Latency** (scan→final max) | 661.2s |
| **Traffic** (notifications 24h) | 93 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 462 | 0.4778 | 0.3485 | +0.1293 | 🟡+27% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 195 | 0.4433 | 0.2974 | 0.2350 | 🔴-0.12 | 0.807 |
| S01_NAKAANA1 | win | 195 | 0.4872 | 0.3436 | 0.2385 | 🔴-0.06 | 0.932 |
| S02_TETSUBAN | win | 72 | 0.5455 | 0.5000 | 0.2579 | 🔴-0.03 | 1.058 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 9 | 0.1865 | 0.0000 | 🔴+0.1865 |
| 0.20-0.30 | 10 | 0.2288 | 0.2000 | ✅+0.0288 |
| 0.30-0.50 | 165 | 0.4124 | 0.3152 | 🔴+0.0972 |
| 0.50+ | 273 | 0.5428 | 0.3846 | 🔴+0.1582 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 196 | 0.811 |
| win | <5.0 | ✅learned | 356 | 0.741 |
| win | <10.0 | ✅learned | 156 | 0.45 |
| win | <20.0 | ✅learned | 46 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-10-28T01:40:01.752406+09:00_