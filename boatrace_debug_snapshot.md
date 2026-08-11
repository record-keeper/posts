# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-11T16:40:01.868953+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T16:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T16:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×35  [2026-08-11T16:05:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-08-11T16:05:27]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-08-11T16:05:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×24  [2026-08-11T11:54:44]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=67<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-11T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-11T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=11 pred=0.1835 actual=0.1818 gap=+0.0017`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S00: n=171 hit%=22.8% hit_CI[Bonf]=[14.9,33.2]% ROI=0.67 ROI_boot95=[0.46,0.90]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-11T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=23.3% hit_CI[Bonf]=[15.2,34.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-11T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=67 hit%=50.7% hit_CI[Bonf]=[34.0,67.3]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=34.3% ROI=0.82 (コスト 8,600/回収 7,060)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=64 hit%=25.0% ROI=0.68 (コスト 15,100/回収 10,250)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=24.0% ROI=0.49 (コスト 11,600/回収 5,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-11T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=24.3% ROI=0.94 (コスト 10,200/回収 9,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.11MB / last modified 2026-08-11T16:39:15.296746+09:00

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
,599 [INFO] run_cycle: fetched 15/4 [final]: 156 combos
2026-08-11 16:37:22,109 [WARNING] scraper: beforeinfo parse failed: jcd=20 rno=4
2026-08-11 16:37:22,109 [WARNING] run_cycle: fetch None: 20/4
2026-08-11 16:37:22,319 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 16:38:03,776 [INFO] run_cycle: === run_cycle 16:38:03 ===
2026-08-11 16:38:03,776 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 16:38:03,777 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 16:38:03,824 [INFO] predictor: Models loaded OK
2026-08-11 16:38:14,256 [WARNING] scraper: beforeinfo parse failed: jcd=20 rno=4
2026-08-11 16:38:14,256 [WARNING] run_cycle: fetch None: 20/4
2026-08-11 16:38:17,642 [INFO] scraper: odds3t: 120/120 parsed
2026-08-11 16:38:18,728 [INFO] scraper: odds3f: 20/20 parsed
2026-08-11 16:38:19,857 [INFO] scraper: odds2t: 30/30 parsed
2026-08-11 16:38:19,858 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 16:38:20,926 [INFO] scraper: odds_win: 6/6 parsed
2026-08-11 16:38:20,926 [INFO] scraper: fetch_race 16/12: boats=6 odds=191/191
2026-08-11 16:38:20,929 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 16:38:20,930 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-11 16:38:20,933 [INFO] run_cycle: fetched 16/12 [scan]: 156 combos
2026-08-11 16:38:21,116 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-11 16:39:03,405 [INFO] run_cycle: === run_cycle 16:39:03 ===
2026-08-11 16:39:03,405 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-11 16:39:03,405 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 16:39:03,454 [INFO] predictor: Models loaded OK
2026-08-11 16:39:14,792 [WARNING] scraper: beforeinfo parse failed: jcd=20 rno=4
2026-08-11 16:39:14,792 [WARNING] run_cycle: fetch None: 20/4
2026-08-11 16:39:15,003 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 75
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 75
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 15, 'scan': 29}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 78
  ANOMALY_SCRAPER_FAILURE_BURST: 57
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 12
  LARGE_ODDS_DRIFT: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 9 | 10,800 | 8,700 | -2,100 | 0.806 |
| S01_NAKAANA1 | 47 | 9 | 9,400 | 5,480 | -3,920 | 0.583 |
| S02_TETSUBAN | 14 | 8 | 2,800 | 2,280 | -520 | 0.814 |

## 直近アラート (24h・新しい順)
```
[16:16:24] FINAL_MISSING: {"deadline": "2026-08-11T12:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081113061245", "sid": "S00"}
[16:05:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:05:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:05:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:03:55] FINAL_MISSING: {"deadline": "2026-08-11T13:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081105051333", "sid": "S00"}
[15:50:52] CIRCUIT_BREAKER_TRIP: {"cost": 9400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 5480, "roi_7d": 0.583, "sid": "S01_NAKAANA1"}
[15:15:52] FINAL_MISSING: {"deadline": "2026-08-11T12:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081113061245", "sid": "S00"}
[15:04:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:04:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:04:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 52件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 128件 締切済
- 通知発射: scan=25 nid / final=26 nid / result=12 nid
- predictions: 14 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 073R | win | 1 | 0.5174 | 6.1 | 3.16 | 300 | scan=4.0 drift=+52.5% | 16:13:25 |
| S01_NAKAANA1 | 1811R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=4.4 drift=-31.8% | 15:50:34 |
| S00 | 068R | win | 1 | 0.6037 | 4.7 | 2.84 | 300 | scan=5.5 drift=-14.5% | 14:58:19 |
| S01_NAKAANA1 | 166R | win | 1 | 0.5123 | 4.0 | 2.05 | 200 | scan=4.6 drift=-13.0% | 13:16:21 |
| S00 | 166R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=4.6 drift=-13.0% | 13:16:19 |
| S01_NAKAANA1 | 164R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=4.3 drift=-30.2% | 12:16:19 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=4.8 drift=-35.4% | 12:10:20 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 11:36:19 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5891 | 4.3 | 2.53 | 200 | scan=4.3 drift=+0.0% | 11:30:21 |
| S00 | 133R | win | 1 | 0.2290 | 21.0 | 4.81 | 300 | scan=- drift=- | 11:18:43 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 62 | +6.4% | -73.3% | +287.7% | 21 | 9 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 474.7s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 392 | 0.4661 | 0.2704 | +0.1956 | 🟡+42% | 0.2363 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 161 | 0.4190 | 0.2236 | 0.2242 | 🔴-0.29 | 0.631 |
| S01_NAKAANA1 | win | 165 | 0.4856 | 0.2182 | 0.2465 | 🔴-0.45 | 0.678 |
| S02_TETSUBAN | win | 66 | 0.5320 | 0.5152 | 0.2402 | ✅+0.04 | 0.88 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 10 | 0.1843 | 0.1000 | 🔴+0.0843 |
| 0.20-0.30 | 9 | 0.2243 | 0.3333 | 🔴-0.1091 |
| 0.30-0.50 | 150 | 0.4185 | 0.2133 | 🔴+0.2051 |
| 0.50+ | 211 | 0.5433 | 0.3223 | 🔴+0.2210 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 103 | 0.776 |
| win | <5.0 | ✅learned | 180 | 0.726 |
| win | <10.0 | ✅learned | 91 | 0.451 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-11T16:40:01.868953+09:00_