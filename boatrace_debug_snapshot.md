# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-11T13:10:01.679153+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×98 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×7  [2026-08-11T13:03:06]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×14  [2026-08-11T13:03:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-08-11T13:03:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-11T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

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
- DB: 10.11MB / last modified 2026-08-11T13:09:28.724574+09:00

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
st={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-11 13:09:03,995 [INFO] predictor: Models loaded OK
2026-08-11 13:09:16,344 [INFO] scraper: odds3t: 120/120 parsed
2026-08-11 13:09:17,441 [INFO] scraper: odds3f: 20/20 parsed
2026-08-11 13:09:18,526 [INFO] scraper: odds2t: 30/30 parsed
2026-08-11 13:09:18,527 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 13:09:19,599 [INFO] scraper: odds_win: 6/6 parsed
2026-08-11 13:09:19,599 [INFO] scraper: fetch_race 13/7: boats=6 odds=191/191
2026-08-11 13:09:19,602 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 13:09:19,603 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-11 13:09:19,606 [INFO] run_cycle: fetched 13/7 [scan]: 156 combos
2026-08-11 13:09:23,073 [INFO] scraper: odds3t: 120/120 parsed
2026-08-11 13:09:24,144 [INFO] scraper: odds3f: 20/20 parsed
2026-08-11 13:09:25,259 [INFO] scraper: odds2t: 29/30 parsed
2026-08-11 13:09:25,260 [INFO] scraper: odds2f: 15/15 parsed
2026-08-11 13:09:26,333 [INFO] scraper: odds_win: 3/6 parsed
2026-08-11 13:09:26,334 [INFO] scraper: fetch_race 16/6: boats=6 odds=187/191
2026-08-11 13:09:26,337 [INFO] predictor: CALIBRATION_MODE=on
2026-08-11 13:09:26,337 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-08-11 13:09:26,341 [INFO] run_cycle: fetched 16/6 [scan]: 152 combos
2026-08-11 13:09:26,645 [INFO] race_id: notif: nid=2026081116061319 sid=S00 phase=scan rank=A
2026-08-11 13:09:26,972 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 13:09:27,560 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 13:09:27,623 [INFO] run_cycle: SCAN S00 児島6R A
2026-08-11 13:09:27,684 [INFO] race_id: notif: nid=2026081116061319 sid=S01_NAKAANA1 phase=scan rank=A
2026-08-11 13:09:27,992 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 13:09:28,395 [INFO] notifier: Discord notify OK (status=204)
2026-08-11 13:09:28,457 [INFO] run_cycle: SCAN S01_NAKAANA1 児島6R A
2026-08-11 13:09:28,671 [INFO] run_cycle: run_cycle done: 2 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 15, 'scan': 27}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 98
  ANOMALY_SCRAPER_FAILURE_BURST: 73
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 30
  CIRCUIT_BREAKER_TRIP: 25
  STRATEGY_CI_FAIL: 17
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 8 | 9,900 | 8,070 | -1,830 | 0.815 |
| S01_NAKAANA1 | 48 | 10 | 9,600 | 5,700 | -3,900 | 0.594 |
| S02_TETSUBAN | 14 | 8 | 2,800 | 2,280 | -520 | 0.814 |

## 直近アラート (24h・新しい順)
```
[13:03:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:03:06] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:47:45] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5700, "roi_7d": 0.594, "sid": "S01_NAKAANA1"}
[12:16:34] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 5200, "roi_7d": 0.542, "sid": "S01_NAKAANA1"}
[12:16:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.203, "baseline_mean": 0.797, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 8, "z_score": 2.84}
[12:10:35] CIRCUIT_BREAKER_TRIP: {"cost": 9400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 47, "payout": 5200, "roi_7d": 0.553, "sid": "S01_NAKAANA1"}
[12:10:35] CRITICAL_ODDS_COLLAPSE: {"combo": "1", "drift_pct": -35.4, "final": 3.1, "kind": "CRITICAL_ODDS_COLLAPSE", "race": "238R", "scan": 4.8, "sid": "S01_NAKAANA1"}
[12:02:15] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:15] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 122件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 58件 締切済
- 通知発射: scan=12 nid / final=14 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 164R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=4.3 drift=-30.2% | 12:16:19 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=4.8 drift=-35.4% | 12:10:20 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=- drift=- | 11:36:19 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5891 | 4.3 | 2.53 | 200 | scan=4.3 drift=+0.0% | 11:30:21 |
| S00 | 133R | win | 1 | 0.2290 | 21.0 | 4.81 | 300 | scan=- drift=- | 11:18:43 |
| S01_NAKAANA1 | 236R | win | 1 | 0.5174 | 4.8 | 2.48 | 200 | scan=- drift=- | 11:00:33 |
| S01_NAKAANA1 | 082R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=3.2 drift=+6.2% | 10:54:27 |
| S01_NAKAANA1 | 161R | win | 1 | 0.5334 | 4.0 | 2.13 | 200 | scan=- drift=- | 10:42:20 |
| S02_TETSUBAN | 213R | win | 1 | 0.5174 | 2.8 | 1.45 | 200 | scan=2.2 drift=+27.3% | 09:21:19 |
| S00 | 248R | win | 1 | 0.2290 | 6.5 | 1.49 | 300 | scan=- drift=- | 18:30:35 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +7.4% | -73.3% | +287.7% | 17 | 8 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 484.3s |
| **Latency** (scan→final max) | 631.3s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 1,400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 399 | 0.4651 | 0.2707 | +0.1944 | 🟡+42% | 0.2375 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4173 | 0.2289 | 0.2267 | 🔴-0.28 | 0.665 |
| S01_NAKAANA1 | win | 165 | 0.4850 | 0.2182 | 0.2460 | 🔴-0.44 | 0.678 |
| S02_TETSUBAN | win | 68 | 0.5335 | 0.5000 | 0.2431 | ✅+0.03 | 0.854 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 9 | 0.2243 | 0.3333 | 🔴-0.1091 |
| 0.30-0.50 | 154 | 0.4177 | 0.2143 | 🔴+0.2034 |
| 0.50+ | 213 | 0.5436 | 0.3192 | 🔴+0.2244 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 103 | 0.776 |
| win | <5.0 | ✅learned | 179 | 0.728 |
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
_auto-generated by claude_snapshot.py at 2026-08-11T13:10:01.679153+09:00_