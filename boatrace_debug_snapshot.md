# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-29T09:20:01.459155+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×20 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×19  [2026-07-29T09:01:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×38  [2026-07-29T09:01:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×19  [2026-07-29T09:01:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-29T08:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-29T08:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-29T06:00:10]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-29T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-29T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=7 pred=0.1262 actual=0.1429 gap=-0.0167`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-29T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1785 actual=0.3750 gap=-0.1965`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S00: n=178 hit%=25.8% hit_CI[Bonf]=[17.6,36.2]% ROI=0.69 ROI_boot95=[0.49,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=27.2% hit_CI[Bonf]=[18.4,38.2]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-29T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=50.0% hit_CI[Bonf]=[34.8,65.2]% ROI=0.98 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=24.1% ROI=0.41 (コスト 8,500/回収 3,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=34.1% ROI=0.91 (コスト 10,700/回収 9,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=74 hit%=32.4% ROI=0.76 (コスト 17,100/回収 13,030)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=40 hit%=22.5% ROI=0.46 (コスト 9,400/回収 4,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-29T06:00:10]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.59 (コスト 9,800/回収 5,800)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-29T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=422 pred=0.4639 actual=0.3104 error=+0.1534 (+33%) brier=0.2329 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.91MB / last modified 2026-07-29T09:19:19.905740+09:00

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
trace.jp/owpc/pc/race/racelist?rno=3&jcd=10&hd=20260729: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-29 09:18:40,153 [INFO] scraper: odds3t: 120/120 parsed
2026-07-29 09:18:41,238 [INFO] scraper: odds3f: 20/20 parsed
2026-07-29 09:18:42,317 [INFO] scraper: odds2t: 30/30 parsed
2026-07-29 09:18:42,319 [INFO] scraper: odds2f: 15/15 parsed
2026-07-29 09:18:43,404 [INFO] scraper: odds_win: 6/6 parsed
2026-07-29 09:18:43,404 [INFO] scraper: fetch_race 10/3: boats=6 odds=191/191
2026-07-29 09:18:43,407 [INFO] predictor: CALIBRATION_MODE=on
2026-07-29 09:18:43,407 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-29 09:18:43,411 [INFO] run_cycle: fetched 10/3 [scan]: 156 combos
2026-07-29 09:18:45,700 [WARNING] scraper: beforeinfo parse failed: jcd=23 rno=3
2026-07-29 09:18:45,700 [WARNING] run_cycle: fetch None: 23/3
2026-07-29 09:18:45,700 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-29 09:19:03,468 [INFO] run_cycle: === run_cycle 09:19:03 ===
2026-07-29 09:19:03,468 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-29 09:19:03,468 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-29 09:19:03,495 [INFO] predictor: Models loaded OK
2026-07-29 09:19:15,948 [INFO] scraper: odds3t: 120/120 parsed
2026-07-29 09:19:17,053 [INFO] scraper: odds3f: 19/20 parsed
2026-07-29 09:19:18,159 [INFO] scraper: odds2t: 24/30 parsed
2026-07-29 09:19:18,160 [INFO] scraper: odds2f: 12/15 parsed
2026-07-29 09:19:19,240 [INFO] scraper: odds_win: 3/6 parsed
2026-07-29 09:19:19,240 [INFO] scraper: fetch_race 23/3: boats=6 odds=178/191
2026-07-29 09:19:19,243 [INFO] predictor: CALIBRATION_MODE=on
2026-07-29 09:19:19,243 [INFO] predictor: combos: {'win': 3, '2t': 24, '3t': 120}
2026-07-29 09:19:19,247 [INFO] run_cycle: fetched 23/3 [scan]: 147 combos
2026-07-29 09:19:19,347 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 22, 'result': 14, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 86
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 32
  CIRCUIT_BREAKER_TRIP: 20
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 3
  ANOMALY_SCAN_FINAL_RATIO: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 8 | 12,000 | 5,550 | -6,450 | 0.463 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 6,440 | -360 | 0.947 |
| S02_TETSUBAN | 19 | 11 | 3,800 | 3,680 | -120 | 0.968 |

## 直近アラート (24h・新しい順)
```
[09:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:03] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5550, "roi_7d": 0.463, "sid": "S00"}
[09:01:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[09:01:03] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[08:00:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:45] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5550, "roi_7d": 0.463, "sid": "S00"}
[08:00:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[08:00:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:04] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5550, "roi_7d": 0.463, "sid": "S00"}
```

## 本日残レース: 150件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 6件 締切済
- 通知発射: scan=1 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 156R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.9 drift=-10.3% | 17:46:19 |
| S01_NAKAANA1 | 0410R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.8 drift=+15.8% | 16:39:18 |
| S00 | 192R | win | 1 | 0.5174 | 12.0 | 6.21 | 300 | scan=10.5 drift=+14.3% | 16:04:18 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=- drift=- | 15:49:19 |
| S02_TETSUBAN | 0310R | win | 1 | 0.3177 | 2.5 | 0.79 | 200 | scan=2.9 drift=-13.8% | 15:19:18 |
| S01_NAKAANA1 | 045R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=- drift=- | 13:51:18 |
| S02_TETSUBAN | 117R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 13:46:19 |
| S00 | 165R | win | 1 | 0.5174 | 11.2 | 5.79 | 300 | scan=12.0 drift=-6.7% | 13:36:42 |
| S01_NAKAANA1 | 164R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 13:05:30 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.5 drift=+0.0% | 12:50:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +3.9% | -86.1% | +198.5% | 14 | 8 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 430.1s |
| **Latency** (scan→final max) | 624.8s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 422 | 0.4639 | 0.3104 | +0.1534 | 🟡+33% | 0.2329 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4218 | 0.2584 | 0.2219 | 🔴-0.16 | 0.692 |
| S01_NAKAANA1 | win | 162 | 0.4753 | 0.2716 | 0.2364 | 🔴-0.19 | 0.77 |
| S02_TETSUBAN | win | 82 | 0.5326 | 0.5000 | 0.2502 | 🔴-0.00 | 0.977 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1262 | 0.1429 | ✅-0.0167 |
| 0.15-0.20 | 8 | 0.1785 | 0.3750 | 🔴-0.1965 |
| 0.20-0.30 | 12 | 0.2272 | 0.2500 | ✅-0.0228 |
| 0.30-0.50 | 168 | 0.4157 | 0.2619 | 🔴+0.1538 |
| 0.50+ | 223 | 0.5405 | 0.3587 | 🔴+0.1817 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 89 | 0.799 |
| win | <5.0 | ✅learned | 158 | 0.724 |
| win | <10.0 | ✅learned | 82 | 0.455 |
| win | <20.0 | ✅learned | 26 | 0.216 |
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
_auto-generated by claude_snapshot.py at 2026-07-29T09:20:01.459155+09:00_