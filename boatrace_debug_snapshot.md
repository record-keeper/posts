# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-12T12:00:02.160179+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×56 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×66 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×56 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×29  [2026-06-12T11:31:37]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-12T11:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×116  [2026-06-12T11:02:29]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×174  [2026-06-12T11:02:29]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×58  [2026-06-12T11:02:29]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-12T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S00: n=150 hit%=28.7% hit_CI[Bonf]=[19.4,40.2]% ROI=0.85 ROI_boot95=[0.59,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=150<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=134 hit%=26.9% hit_CI[Bonf]=[17.4,39.0]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=134<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-12T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=34.1% hit_CI[Bonf]=[21.1,50.1]% ROI=0.57 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-12T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-12T06:00:13]
- key: `ORPHAN_SCAN|143 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=34.3% ROI=1.00 (コスト 10,300/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=17.1% ROI=0.35 (コスト 7,700/回収 2,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=70 hit%=28.6% ROI=0.57 (コスト 16,500/回収 9,420)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=35 hit%=20.0% ROI=0.72 (コスト 7,900/回収 5,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-12T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.49 (コスト 8,500/回収 4,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.89MB / last modified 2026-06-12T12:00:05.434497+09:00

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
arsed
2026-06-12 11:58:21,712 [INFO] scraper: fetch_race 14/8: boats=6 odds=191/191
2026-06-12 11:58:21,723 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 11:58:21,723 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-12 11:58:21,731 [INFO] run_cycle: fetched 14/8 [scan]: 156 combos
2026-06-12 11:58:25,233 [INFO] scraper: odds3t: 120/120 parsed
2026-06-12 11:58:26,316 [INFO] scraper: odds3f: 20/20 parsed
2026-06-12 11:58:27,409 [INFO] scraper: odds2t: 30/30 parsed
2026-06-12 11:58:27,410 [INFO] scraper: odds2f: 15/15 parsed
2026-06-12 11:58:28,505 [INFO] scraper: odds_win: 6/6 parsed
2026-06-12 11:58:28,505 [INFO] scraper: fetch_race 03/3: boats=6 odds=191/191
2026-06-12 11:58:28,514 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 11:58:28,514 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-12 11:58:28,522 [INFO] run_cycle: fetched 03/3 [scan]: 156 combos
2026-06-12 11:58:31,948 [INFO] scraper: odds3t: 120/120 parsed
2026-06-12 11:58:33,032 [INFO] scraper: odds3f: 19/20 parsed
2026-06-12 11:58:34,140 [INFO] scraper: odds2t: 27/30 parsed
2026-06-12 11:58:34,141 [INFO] scraper: odds2f: 15/15 parsed
2026-06-12 11:58:35,239 [INFO] scraper: odds_win: 5/6 parsed
2026-06-12 11:58:35,239 [INFO] scraper: fetch_race 09/4: boats=6 odds=186/191
2026-06-12 11:58:35,247 [INFO] predictor: CALIBRATION_MODE=on
2026-06-12 11:58:35,247 [INFO] predictor: combos: {'win': 5, '2t': 27, '3t': 120}
2026-06-12 11:58:35,255 [INFO] run_cycle: fetched 09/4 [scan]: 152 combos
2026-06-12 11:58:35,365 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-12 11:59:05,750 [INFO] run_cycle: === run_cycle 11:59:05 ===
2026-06-12 11:59:05,750 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-12 11:59:05,750 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-12 11:59:05,836 [INFO] predictor: Models loaded OK
2026-06-12 11:59:06,142 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 21, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 66
  ANOMALY_SCRAPER_FAILURE_BURST: 64
  CIRCUIT_BREAKER_TRIP: 56
  CIRCUIT_BREAKER_NO_ACTION: 51
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 12
  CALIBRATION_DRIFT: 6
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 14 | 12,600 | 12,240 | -360 | 0.971 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,100 | -2,900 | 0.586 |
| S02_TETSUBAN | 27 | 6 | 5,400 | 1,840 | -3,560 | 0.341 |

## 直近アラート (24h・新しい順)
```
[11:49:42] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4100, "roi_7d": 0.586, "sid": "S01_NAKAANA1"}
[11:39:30] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4100, "roi_7d": 0.603, "sid": "S01_NAKAANA1"}
[11:34:35] FINAL_MISSING: {"deadline": "2026-06-12T10:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061214041004", "sid": "S00"}
[11:31:37] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4100, "roi_7d": 0.621, "sid": "S01_NAKAANA1"}
[11:14:27] FINAL_MISSING: {"deadline": "2026-06-12T10:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061210061044", "sid": "S00"}
[11:09:30] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 15.4, "final": 6.0, "kind": "LARGE_ODDS_DRIFT", "race": "107R", "scan": 5.2, "sid": "S00"}
[11:09:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.146, "baseline_mean": 0.854, "baseline_stdev": 0.06, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.43}
[11:02:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:28] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 4100, "roi_7d": 0.641, "sid": "S01_NAKAANA1"}
[11:02:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 106件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 38件 締切済
- 通知発射: scan=4 nid / final=10 nid / result=5 nid
- predictions: 8 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 238R | win | 1 | 0.5123 | 3.6 | 1.84 | 200 | scan=- drift=- | 11:49:33 |
| S01_NAKAANA1 | 032R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 11:39:22 |
| S01_NAKAANA1 | 147R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 11:31:21 |
| S00 | 113R | win | 1 | 0.2290 | 4.5 | 1.03 | 300 | scan=- drift=- | 11:21:44 |
| S00 | 107R | win | 1 | 0.5123 | 6.0 | 3.07 | 300 | scan=5.2 drift=+15.4% | 11:09:22 |
| S02_TETSUBAN | 132R | win | 1 | 0.5334 | 2.5 | 1.33 | 200 | scan=- drift=- | 10:59:20 |
| S01_NAKAANA1 | 144R | win | 1 | 0.3177 | 3.3 | 1.05 | 200 | scan=3.1 drift=+6.5% | 10:01:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 09:09:20 |
| S02_TETSUBAN | 2010R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=- drift=- | 19:39:22 |
| S00 | 075R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=36.3 drift=-82.9% | 17:39:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +6.2% | -82.9% | +274.6% | 19 | 9 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 453.9s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4702 | 0.2978 | +0.1724 | 🟡+37% | 0.2375 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 150 | 0.4208 | 0.2933 | 0.2170 | 🔴-0.05 | 0.891 |
| S01_NAKAANA1 | win | 134 | 0.4884 | 0.2761 | 0.2441 | 🔴-0.22 | 0.719 |
| S02_TETSUBAN | win | 82 | 0.5309 | 0.3415 | 0.2641 | 🔴-0.17 | 0.567 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 5 | 0.1231 | 0.2000 | 🔴-0.0769 |
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 7 | 0.2244 | 0.2857 | 🔴-0.0613 |
| 0.30-0.50 | 134 | 0.4206 | 0.2313 | 🔴+0.1893 |
| 0.50+ | 207 | 0.5419 | 0.3575 | 🔴+0.1844 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 37 | 0.733 |
| win | <5.0 | ✅learned | 70 | 0.715 |
| win | <10.0 | ✅learned | 47 | 0.513 |
| win | <20.0 | ✅learned | 14 | 0.21 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-12T12:00:02.160179+09:00_