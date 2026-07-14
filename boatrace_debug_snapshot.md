# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-14T12:30:01.356797+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×74 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×4 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×15  [2026-07-14T12:15:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×29  [2026-07-14T12:01:26]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×29  [2026-07-14T12:01:26]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-07-14T12:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-14T11:55:23]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-07-14T10:00:40]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-14T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3244 actual=0.1034 gap=+0.2210`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S00: n=176 hit%=29.5% hit_CI[Bonf]=[20.7,40.2]% ROI=0.76 ROI_boot95=[0.57,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=156 hit%=30.8% hit_CI[Bonf]=[21.3,42.2]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-14T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=156<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-14T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=43.5% hit_CI[Bonf]=[27.9,60.5]% ROI=0.86 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-14T06:00:06]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=33.3% ROI=0.86 (コスト 9,700/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.77 (コスト 11,200/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=33.0% ROI=0.90 (コスト 20,200/回収 18,230)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=32.4% ROI=0.75 (コスト 9,100/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-14T06:00:06]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=22.6% ROI=0.45 (コスト 8,600/回収 3,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-14T06:00:06]
- key: `CALIBRATION_LIVE|bt=win: n=401 pred=0.4712 actual=0.3242 error=+0.1470 (+31%) brier=0.2366 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.69MB / last modified 2026-07-14T12:30:02.682248+09:00

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
e.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-14 12:28:25,609 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=5&jcd=13&hd=20260714: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-07-14 12:28:39,145 [INFO] scraper: odds3t: 120/120 parsed
2026-07-14 12:28:40,246 [INFO] scraper: odds3f: 20/20 parsed
2026-07-14 12:28:41,392 [INFO] scraper: odds2t: 30/30 parsed
2026-07-14 12:28:41,393 [INFO] scraper: odds2f: 15/15 parsed
2026-07-14 12:28:42,514 [INFO] scraper: odds_win: 6/6 parsed
2026-07-14 12:28:42,514 [INFO] scraper: fetch_race 13/5: boats=6 odds=191/191
2026-07-14 12:28:42,517 [INFO] predictor: CALIBRATION_MODE=on
2026-07-14 12:28:42,518 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-14 12:28:42,521 [INFO] run_cycle: fetched 13/5 [final]: 156 combos
2026-07-14 12:28:42,906 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-14 12:29:03,346 [INFO] run_cycle: === run_cycle 12:29:03 ===
2026-07-14 12:29:03,346 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-14 12:29:03,346 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-14 12:29:03,389 [INFO] predictor: Models loaded OK
2026-07-14 12:29:16,002 [INFO] scraper: odds3t: 120/120 parsed
2026-07-14 12:29:17,088 [INFO] scraper: odds3f: 20/20 parsed
2026-07-14 12:29:18,171 [INFO] scraper: odds2t: 29/30 parsed
2026-07-14 12:29:18,172 [INFO] scraper: odds2f: 11/15 parsed
2026-07-14 12:29:19,268 [INFO] scraper: odds_win: 3/6 parsed
2026-07-14 12:29:19,269 [INFO] scraper: fetch_race 09/5: boats=6 odds=183/191
2026-07-14 12:29:19,272 [INFO] predictor: CALIBRATION_MODE=on
2026-07-14 12:29:19,272 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-07-14 12:29:19,275 [INFO] run_cycle: fetched 09/5 [scan]: 152 combos
2026-07-14 12:29:19,367 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 47
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 47
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 11, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 165
  FINAL_MISSING: 74
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  CIRCUIT_BREAKER_TRIP: 4
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 17 | 13,800 | 14,010 | +210 | 1.015 |
| S01_NAKAANA1 | 36 | 10 | 7,200 | 4,760 | -2,440 | 0.661 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,860 | +60 | 1.016 |

## 直近アラート (24h・新しい順)
```
[12:23:34] CIRCUIT_BREAKER_TRIP: {"cost": 7200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 4760, "roi_7d": 0.661, "sid": "S01_NAKAANA1"}
[12:19:44] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.182, "baseline_mean": 0.782, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.43}
[12:15:39] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4760, "roi_7d": 0.68, "sid": "S01_NAKAANA1"}
[12:03:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.532, "baseline_mean": 0.782, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.25, "today_scan_count": 4, "z_score": -7.12}
[12:01:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:55:23] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.448, "baseline_mean": 0.782, "baseline_stdev": 0.075, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -6.01}
[11:01:18] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:18] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[10:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 119件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 37件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 063R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=4.5 drift=-33.3% | 12:23:19 |
| S02_TETSUBAN | 218R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.1 drift=+0.0% | 11:45:18 |
| S02_TETSUBAN | 078R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=2.5 drift=+8.0% | 18:39:19 |
| S01_NAKAANA1 | 073R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=4.2 drift=+11.9% | 16:12:20 |
| S00 | 073R | win | 1 | 0.4111 | 4.7 | 1.93 | 300 | scan=4.2 drift=+11.9% | 16:12:20 |
| S02_TETSUBAN | 072R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 15:44:29 |
| S01_NAKAANA1 | 0310R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.0 drift=+3.3% | 15:19:18 |
| S00 | 226R | win | 1 | 0.1760 | 4.9 | 0.86 | 300 | scan=- drift=- | 14:45:42 |
| S01_NAKAANA1 | 043R | win | 1 | 0.2307 | 4.5 | 1.04 | 200 | scan=4.6 drift=-2.2% | 12:51:19 |
| S01_NAKAANA1 | 2310R | win | 1 | 0.5174 | 4.8 | 2.48 | 200 | scan=3.3 drift=+45.5% | 12:49:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +20.2% | -73.3% | +533.3% | 16 | 6 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 390.4s |
| **Latency** (scan→final max) | 605.1s |
| **Traffic** (notifications 24h) | 47 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4710 | 0.3199 | +0.1511 | 🟡+32% | 0.2366 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4329 | 0.2931 | 0.2254 | 🔴-0.09 | 0.751 |
| S01_NAKAANA1 | win | 154 | 0.4814 | 0.3052 | 0.2376 | 🔴-0.12 | 0.796 |
| S02_TETSUBAN | win | 69 | 0.5439 | 0.4203 | 0.2629 | 🔴-0.08 | 0.838 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 16 | 0.2282 | 0.1875 | ✅+0.0407 |
| 0.30-0.50 | 143 | 0.4162 | 0.2797 | 🔴+0.1364 |
| 0.50+ | 225 | 0.5422 | 0.3556 | 🔴+0.1867 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 70 | 0.794 |
| win | <5.0 | ✅learned | 138 | 0.704 |
| win | <10.0 | ✅learned | 73 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-14T12:30:01.356797+09:00_