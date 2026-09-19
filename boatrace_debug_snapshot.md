# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-19T23:20:01.562593+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×92 (24h)
- 🔴 PSI_DRIFT_DETECTED×41 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×11  [2026-09-19T23:09:14]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×11  [2026-09-19T23:09:14]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×11  [2026-09-19T23:09:14]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-09-19T23:09:14]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-19T22:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-09-19T15:50:39]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×38  [2026-09-19T15:27:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×12  [2026-09-19T12:51:32]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S00: n=175 hit%=24.6% hit_CI[Bonf]=[16.5,35.0]% ROI=0.76 ROI_boot95=[0.54,1.02]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=169 hit%=24.3% hit_CI[Bonf]=[16.1,34.8]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-19T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=40.8% hit_CI[Bonf]=[26.2,57.2]% ROI=0.76 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-19T06:00:19]
- key: `ORPHAN_SCAN|177 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=30.3% ROI=0.88 (コスト 9,500/回収 8,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=20.5% ROI=0.55 (コスト 10,200/回収 5,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=81 hit%=22.2% ROI=0.68 (コスト 18,800/回収 12,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-19T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.51 (コスト 9,800/回収 5,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.66MB / last modified 2026-09-19T23:19:05.018776+09:00

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
75 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 23:15:05,075 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 23:15:05,153 [INFO] predictor: Models loaded OK
2026-09-19 23:15:05,157 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 23:16:04,775 [INFO] run_cycle: === run_cycle 23:16:04 ===
2026-09-19 23:16:04,775 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 23:16:04,775 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 23:16:04,846 [INFO] predictor: Models loaded OK
2026-09-19 23:16:04,850 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 23:17:04,599 [INFO] run_cycle: === run_cycle 23:17:04 ===
2026-09-19 23:17:04,599 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 23:17:04,599 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 23:17:04,652 [INFO] predictor: Models loaded OK
2026-09-19 23:17:04,654 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 23:18:03,868 [INFO] run_cycle: === run_cycle 23:18:03 ===
2026-09-19 23:18:03,868 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 23:18:03,868 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 23:18:03,942 [INFO] predictor: Models loaded OK
2026-09-19 23:18:03,944 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-19 23:19:04,699 [INFO] run_cycle: === run_cycle 23:19:04 ===
2026-09-19 23:19:04,699 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-19 23:19:04,699 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-19 23:19:04,773 [INFO] predictor: Models loaded OK
2026-09-19 23:19:04,777 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 15, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 92
  FINAL_MISSING: 92
  PSI_DRIFT_DETECTED: 41
  CIRCUIT_BREAKER_TRIP: 24
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 11 | 13,500 | 9,180 | -4,320 | 0.68 |
| S01_NAKAANA1 | 35 | 11 | 7,000 | 7,700 | +700 | 1.1 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,680 | +280 | 1.082 |

## 直近アラート (24h・新しい順)
```
[23:16:04] FINAL_MISSING: {"deadline": "2026-09-19T16:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091915041642", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:01:04] FINAL_MISSING: {"deadline": "2026-09-19T13:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091913071327", "sid": "S02_TETSUBAN"}
[22:58:04] CIRCUIT_BREAKER_TRIP: {"cost": 13500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 9180, "roi_7d": 0.68, "sid": "S00"}
[22:58:04] FINAL_MISSING: {"deadline": "2026-09-19T11:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091904021122", "sid": "S00"}
[22:55:04] FINAL_MISSING: {"deadline": "2026-09-19T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091902021116", "sid": "S00"}
[22:49:03] FINAL_MISSING: {"deadline": "2026-09-19T16:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091915031616", "sid": "S00"}
[22:47:04] FINAL_MISSING: {"deadline": "2026-09-19T17:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091915051715", "sid": "S00"}
[22:44:03] FINAL_MISSING: {"deadline": "2026-09-19T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091903031208", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 156件 締切済
- 通知発射: scan=28 nid / final=26 nid / result=15 nid
- predictions: 15 / うち結果DB記録済: 15
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 128R | win | 1 | 0.5334 | 5.1 | 2.72 | 300 | scan=5.2 drift=-1.9% | 18:23:18 |
| S01_NAKAANA1 | 0411R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=4.1 drift=-7.3% | 16:03:31 |
| S01_NAKAANA1 | 151R | win | 1 | 0.5735 | 3.3 | 1.89 | 200 | scan=- drift=- | 15:19:36 |
| S00 | 0210R | win | 1 | 0.4989 | 4.1 | 2.05 | 300 | scan=- drift=- | 15:19:20 |
| S01_NAKAANA1 | 028R | win | 1 | 0.3177 | 3.8 | 1.21 | 200 | scan=3.2 drift=+18.7% | 14:13:18 |
| S02_TETSUBAN | 037R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=2.1 drift=-4.8% | 13:53:19 |
| S00 | 036R | win | 1 | 0.5322 | 5.2 | 2.77 | 300 | scan=- drift=- | 13:26:18 |
| S00 | 046R | win | 1 | 0.5476 | 7.2 | 3.94 | 300 | scan=5.8 drift=+24.1% | 13:19:31 |
| S01_NAKAANA1 | 044R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=- drift=- | 12:19:18 |
| S02_TETSUBAN | 054R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 11:54:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +2.7% | -81.7% | +119.5% | 14 | 5 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 423.4s |
| **Latency** (scan→final max) | 613.4s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 416 | 0.4779 | 0.2596 | +0.2183 | 🟡+46% | 0.2409 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 173 | 0.4423 | 0.2428 | 0.2262 | 🔴-0.23 | 0.751 |
| S01_NAKAANA1 | win | 167 | 0.4860 | 0.2096 | 0.2459 | 🔴-0.48 | 0.623 |
| S02_TETSUBAN | win | 76 | 0.5414 | 0.4079 | 0.2634 | 🔴-0.09 | 0.75 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.30-0.50 | 150 | 0.4098 | 0.2133 | 🔴+0.1965 |
| 0.50+ | 247 | 0.5448 | 0.2996 | 🔴+0.2452 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 145 | 0.775 |
| win | <5.0 | ✅learned | 256 | 0.761 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 33 | 0.234 |
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
_auto-generated by claude_snapshot.py at 2026-09-19T23:20:01.562593+09:00_