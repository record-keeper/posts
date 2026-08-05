# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-05T10:40:01.433062+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×69 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×8 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-05T10:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-05T10:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-08-05T10:16:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×76  [2026-08-05T10:02:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×76  [2026-08-05T10:02:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-08-05T10:02:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-05T06:00:07]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-05T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.69 ROI_boot95=[0.48,0.93]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=157 hit%=23.6% hit_CI[Bonf]=[15.3,34.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-05T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-05T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=49.3% hit_CI[Bonf]=[32.9,65.8]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.53 (コスト 10,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=38.2% ROI=0.92 (コスト 8,500/回収 7,820)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=31.8% ROI=0.76 (コスト 15,500/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-05T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=42 hit%=21.4% ROI=0.42 (コスト 9,800/回収 4,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-05T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=404 pred=0.4593 actual=0.2896 error=+0.1697 (+37%) brier=0.2327 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.48MB / last modified 2026-08-05T10:39:04.428667+09:00

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
ault=5000
2026-08-05 10:36:04,096 [INFO] predictor: Models loaded OK
2026-08-05 10:36:04,219 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 10:37:04,148 [INFO] run_cycle: === run_cycle 10:37:04 ===
2026-08-05 10:37:04,148 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 10:37:04,148 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 10:37:04,180 [INFO] predictor: Models loaded OK
2026-08-05 10:37:04,282 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 10:38:03,548 [INFO] run_cycle: === run_cycle 10:38:03 ===
2026-08-05 10:38:03,548 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 10:38:03,548 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 10:38:03,597 [INFO] predictor: Models loaded OK
2026-08-05 10:38:15,976 [INFO] scraper: odds3t: 120/120 parsed
2026-08-05 10:38:17,066 [INFO] scraper: odds3f: 20/20 parsed
2026-08-05 10:38:18,182 [INFO] scraper: odds2t: 30/30 parsed
2026-08-05 10:38:18,183 [INFO] scraper: odds2f: 14/15 parsed
2026-08-05 10:38:19,318 [INFO] scraper: odds_win: 5/6 parsed
2026-08-05 10:38:19,318 [INFO] scraper: fetch_race 10/6: boats=6 odds=189/191
2026-08-05 10:38:19,321 [INFO] predictor: CALIBRATION_MODE=on
2026-08-05 10:38:19,322 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-05 10:38:19,325 [INFO] run_cycle: fetched 10/6 [scan]: 155 combos
2026-08-05 10:38:19,424 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-05 10:39:03,337 [INFO] run_cycle: === run_cycle 10:39:03 ===
2026-08-05 10:39:03,338 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-05 10:39:03,338 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-05 10:39:03,398 [INFO] predictor: Models loaded OK
2026-08-05 10:39:03,511 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 12, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 98
  FINAL_MISSING: 69
  CIRCUIT_BREAKER_TRIP: 35
  CIRCUIT_BREAKER_NO_ACTION: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  PSI_DRIFT_DETECTED: 8
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 10 | 11,100 | 7,500 | -3,600 | 0.676 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 4,360 | -2,440 | 0.641 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,140 | -660 | 0.764 |

## 直近アラート (24h・新しい順)
```
[10:39:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 631}
[10:38:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 632}
[10:34:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 641}
[10:32:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 651}
[10:31:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 646}
[10:30:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 653}
[10:29:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 654}
[10:28:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 657}
[10:27:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 663}
[10:26:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 661}
```

## 本日残レース: 116件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 16件 締切済
- 通知発射: scan=1 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 211R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 08:37:18 |
| S01_NAKAANA1 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=3.2 drift=+28.1% | 18:40:45 |
| S00 | 198R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 18:40:44 |
| S00 | 196R | win | 1 | 0.5123 | 6.3 | 3.23 | 300 | scan=23.6 drift=-73.3% | 17:43:30 |
| S01_NAKAANA1 | 047R | win | 1 | 0.3177 | 3.6 | 1.14 | 200 | scan=3.1 drift=+16.1% | 14:55:19 |
| S01_NAKAANA1 | 056R | win | 1 | 0.3177 | 3.4 | 1.08 | 200 | scan=- drift=- | 14:00:24 |
| S01_NAKAANA1 | 045R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 13:52:20 |
| S00 | 175R | win | 1 | 0.1034 | 10.6 | 1.10 | 300 | scan=18.0 drift=-41.1% | 13:09:20 |
| S00 | 218R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=- drift=- | 11:57:20 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5209 | 4.1 | 2.14 | 200 | scan=4.5 drift=-8.9% | 10:42:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 53 | +10.8% | -73.3% | +375.6% | 17 | 12 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 532.5s |
| **Latency** (scan→final max) | 646.4s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 405 | 0.4595 | 0.2914 | +0.1681 | 🟡+37% | 0.2327 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4151 | 0.2584 | 0.2222 | 🔴-0.16 | 0.692 |
| S01_NAKAANA1 | win | 157 | 0.4787 | 0.2357 | 0.2387 | 🔴-0.33 | 0.701 |
| S02_TETSUBAN | win | 70 | 0.5293 | 0.5000 | 0.2458 | ✅+0.02 | 0.963 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1235 | 0.1667 | ✅-0.0432 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 157 | 0.4180 | 0.2166 | 🔴+0.2015 |
| 0.50+ | 212 | 0.5404 | 0.3585 | 🔴+0.1819 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 96 | 0.787 |
| win | <5.0 | ✅learned | 167 | 0.721 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 28 | 0.219 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-05T10:40:01.433062+09:00_