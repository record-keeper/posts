# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-24T10:20:01.300909+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×48 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×110 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×48 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×38  [2026-07-24T10:01:19]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×38  [2026-07-24T10:01:19]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×19  [2026-07-24T10:01:19]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-24T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-24T09:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-24T06:00:16]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-24T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-24T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3249 actual=0.0938 gap=+0.2311`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S00: n=178 hit%=27.5% hit_CI[Bonf]=[19.0,38.0]% ROI=0.73 ROI_boot95=[0.53,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=28.4% hit_CI[Bonf]=[19.4,39.5]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-24T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=48.6% hit_CI[Bonf]=[32.9,64.7]% ROI=0.97 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=27.3% ROI=0.57 (コスト 9,700/回収 5,520)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=31.8% ROI=0.88 (コスト 10,700/回収 9,390)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=79 hit%=35.4% ROI=0.85 (コスト 18,000/回収 15,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=32 hit%=25.0% ROI=0.50 (コスト 7,700/回収 3,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-24T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=38 hit%=21.1% ROI=0.50 (コスト 10,500/回収 5,220)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-24T06:00:16]
- key: `CALIBRATION_LIVE|bt=win: n=414 pred=0.4693 actual=0.3164 error=+0.1528 (+33%) brier=0.2368 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-24T06:00:16]
- key: `CALIBRATION_LIVE|S00(win): n=178 pred=0.4290 hit=0.2753 cal_err=+0.1537 brier=0.2289 BSS=-0.15 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 8.54MB / last modified 2026-07-24T10:19:03.724150+09:00

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
 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-24 10:17:03,353 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-24 10:17:03,397 [INFO] predictor: Models loaded OK
2026-07-24 10:17:14,512 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=14&hd=20260724: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-24 10:17:25,987 [INFO] scraper: odds3t: 120/120 parsed
2026-07-24 10:17:27,086 [INFO] scraper: odds3f: 20/20 parsed
2026-07-24 10:17:28,165 [INFO] scraper: odds2t: 25/30 parsed
2026-07-24 10:17:28,166 [INFO] scraper: odds2f: 9/15 parsed
2026-07-24 10:17:29,267 [INFO] scraper: odds_win: 6/6 parsed
2026-07-24 10:17:29,268 [INFO] scraper: fetch_race 14/5: boats=6 odds=180/191
2026-07-24 10:17:29,271 [INFO] predictor: CALIBRATION_MODE=on
2026-07-24 10:17:29,271 [INFO] predictor: combos: {'win': 6, '2t': 25, '3t': 120}
2026-07-24 10:17:29,274 [INFO] run_cycle: fetched 14/5 [scan]: 151 combos
2026-07-24 10:17:29,375 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-24 10:18:03,226 [INFO] run_cycle: === run_cycle 10:18:03 ===
2026-07-24 10:18:03,226 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-24 10:18:03,226 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-24 10:18:03,262 [INFO] predictor: Models loaded OK
2026-07-24 10:18:03,447 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-24 10:19:03,436 [INFO] run_cycle: === run_cycle 10:19:03 ===
2026-07-24 10:19:03,436 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-24 10:19:03,436 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-24 10:19:03,479 [INFO] predictor: Models loaded OK
2026-07-24 10:19:03,582 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 29, 'result': 15, 'scan': 31}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 327
  FINAL_MISSING: 110
  CIRCUIT_BREAKER_TRIP: 48
  ANOMALY_SCAN_FINAL_RATIO: 46
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  CALIBRATION_DRIFT: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 10 | 14,100 | 8,640 | -5,460 | 0.613 |
| S01_NAKAANA1 | 40 | 7 | 8,000 | 5,220 | -2,780 | 0.652 |
| S02_TETSUBAN | 17 | 9 | 3,400 | 3,320 | -80 | 0.976 |

## 直近アラート (24h・新しい順)
```
[10:09:29] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5220, "roi_7d": 0.652, "sid": "S01_NAKAANA1"}
[10:01:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:01:19] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 8640, "roi_7d": 0.613, "sid": "S00"}
[10:01:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:01:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[09:09:20] CIRCUIT_BREAKER_TRIP: {"cost": 8000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 5220, "roi_7d": 0.652, "sid": "S01_NAKAANA1"}
[09:09:20] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 27.0, "final": 4.7, "kind": "LARGE_ODDS_DRIFT", "race": "142R", "scan": 3.7, "sid": "S01_NAKAANA1"}
[09:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:03] CIRCUIT_BREAKER_TRIP: {"cost": 7800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 39, "payout": 5220, "roi_7d": 0.669, "sid": "S01_NAKAANA1"}
[09:01:03] CIRCUIT_BREAKER_TRIP: {"cost": 14100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 8640, "roi_7d": 0.613, "sid": "S00"}
```

## 本日残レース: 167件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 13件 締切済
- 通知発射: scan=2 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 142R | win | 1 | 0.4989 | 4.7 | 2.34 | 200 | scan=3.7 drift=+27.0% | 09:09:19 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=- drift=- | 19:54:18 |
| S00 | 246R | win | 1 | 0.5174 | 5.6 | 2.90 | 300 | scan=5.6 drift=+0.0% | 19:53:29 |
| S00 | 155R | win | 1 | 0.1731 | 4.2 | 0.73 | 300 | scan=- drift=- | 17:27:29 |
| S00 | 015R | win | 1 | 0.1034 | 5.4 | 0.56 | 300 | scan=8.2 drift=-34.1% | 17:21:20 |
| S00 | 152R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 15:57:20 |
| S00 | 0911R | win | 1 | 0.4111 | 9.6 | 3.95 | 300 | scan=- drift=- | 15:43:18 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 14:01:29 |
| S02_TETSUBAN | 097R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=- drift=- | 13:36:29 |
| S02_TETSUBAN | 054R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.2 drift=+4.5% | 13:00:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 54 | +20.8% | -83.7% | +628.9% | 21 | 10 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 481.1s |
| **Latency** (scan→final max) | 618.7s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 415 | 0.4693 | 0.3157 | +0.1537 | 🟡+33% | 0.2369 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4290 | 0.2753 | 0.2289 | 🔴-0.15 | 0.729 |
| S01_NAKAANA1 | win | 163 | 0.4797 | 0.2822 | 0.2388 | 🔴-0.18 | 0.778 |
| S02_TETSUBAN | win | 74 | 0.5436 | 0.4865 | 0.2519 | 🔴-0.01 | 0.966 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1267 | 0.1667 | ✅-0.0400 |
| 0.15-0.20 | 7 | 0.1794 | 0.4286 | 🔴-0.2492 |
| 0.20-0.30 | 12 | 0.2272 | 0.3333 | 🔴-0.1061 |
| 0.30-0.50 | 162 | 0.4177 | 0.2778 | 🔴+0.1399 |
| 0.50+ | 225 | 0.5427 | 0.3467 | 🔴+0.1961 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 82 | 0.81 |
| win | <5.0 | ✅learned | 151 | 0.724 |
| win | <10.0 | ✅learned | 78 | 0.458 |
| win | <20.0 | ✅learned | 25 | 0.218 |
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
_auto-generated by claude_snapshot.py at 2026-07-24T10:20:01.300909+09:00_