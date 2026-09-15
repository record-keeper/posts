# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-15T16:10:01.642217+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×46 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×89 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 CALIBRATION_DRIFT×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×15 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×14  [2026-09-15T16:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×14  [2026-09-15T16:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-09-15T16:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-15T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-15T16:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 PSI_DRIFT_DETECTED  ×12  [2026-09-15T15:58:39]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-15T13:44:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-09-15T12:53:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×33  [2026-09-15T12:02:23]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-15T06:00:05]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-15T06:00:05]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=24.2% ROI=0.69 (コスト 9,500/回収 6,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=40 pred=0.3232 actual=0.3000 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S00: n=167 hit%=26.9% hit_CI[Bonf]=[18.3,37.8]% ROI=0.93 ROI_boot95=[0.63,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S01_NAKAANA1: n=179 hit%=25.1% hit_CI[Bonf]=[17.0,35.5]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=35.4% hit_CI[Bonf]=[22.1,51.3]% ROI=0.62 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.3MB / last modified 2026-09-15T16:09:28.970529+09:00

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
== run_cycle 16:08:05 ===
2026-09-15 16:08:05,446 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-15 16:08:05,446 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-15 16:08:05,486 [INFO] predictor: Models loaded OK
2026-09-15 16:08:05,982 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-15 16:09:05,175 [INFO] run_cycle: === run_cycle 16:09:05 ===
2026-09-15 16:09:05,175 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-15 16:09:05,175 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-15 16:09:05,268 [INFO] predictor: Models loaded OK
2026-09-15 16:09:17,748 [INFO] scraper: odds3t: 120/120 parsed
2026-09-15 16:09:18,855 [INFO] scraper: odds3f: 20/20 parsed
2026-09-15 16:09:19,980 [INFO] scraper: odds2t: 28/30 parsed
2026-09-15 16:09:19,982 [INFO] scraper: odds2f: 15/15 parsed
2026-09-15 16:09:21,114 [INFO] scraper: odds_win: 4/6 parsed
2026-09-15 16:09:21,114 [INFO] scraper: fetch_race 07/3: boats=6 odds=187/191
2026-09-15 16:09:21,118 [INFO] predictor: CALIBRATION_MODE=on
2026-09-15 16:09:21,118 [INFO] predictor: combos: {'win': 4, '2t': 28, '3t': 120}
2026-09-15 16:09:21,122 [INFO] run_cycle: fetched 07/3 [final]: 152 combos
2026-09-15 16:09:25,130 [INFO] scraper: odds3t: 120/120 parsed
2026-09-15 16:09:26,234 [INFO] scraper: odds3f: 20/20 parsed
2026-09-15 16:09:27,332 [INFO] scraper: odds2t: 30/30 parsed
2026-09-15 16:09:27,333 [INFO] scraper: odds2f: 15/15 parsed
2026-09-15 16:09:28,475 [INFO] scraper: odds_win: 6/6 parsed
2026-09-15 16:09:28,475 [INFO] scraper: fetch_race 20/3: boats=6 odds=191/191
2026-09-15 16:09:28,478 [INFO] predictor: CALIBRATION_MODE=on
2026-09-15 16:09:28,478 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-15 16:09:28,482 [INFO] run_cycle: fetched 20/3 [scan]: 156 combos
2026-09-15 16:09:28,754 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 70
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 70
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 11, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 114
  FINAL_MISSING: 89
  CIRCUIT_BREAKER_TRIP: 46
  CIRCUIT_BREAKER_NO_ACTION: 41
  CALIBRATION_DRIFT: 20
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 15
  ANOMALY_SCAN_FINAL_RATIO: 8
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 29 | 6 | 8,700 | 4,860 | -3,840 | 0.559 |
| S01_NAKAANA1 | 34 | 8 | 6,800 | 4,440 | -2,360 | 0.653 |
| S02_TETSUBAN | 16 | 6 | 3,200 | 1,680 | -1,520 | 0.525 |

## 直近アラート (24h・新しい順)
```
[16:05:23] CIRCUIT_BREAKER_TRIP: {"cost": 6800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4440, "roi_7d": 0.653, "sid": "S01_NAKAANA1"}
[16:05:23] FINAL_MISSING: {"deadline": "2026-09-15T13:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091509071334", "sid": "S00"}
[16:03:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:03:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:03:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:54:27] FINAL_MISSING: {"deadline": "2026-09-15T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091504041222", "sid": "S00"}
[15:51:35] FINAL_MISSING: {"deadline": "2026-09-15T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091510051018", "sid": "S00"}
[15:30:52] CIRCUIT_BREAKER_TRIP: {"cost": 8700, "kind": "CIRCUIT_BREAKER_TRIP", "n": 29, "payout": 4860, "roi_7d": 0.559, "sid": "S00"}
[15:30:52] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 346, "n_recent": 79, "psi": 0.398}
[15:28:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 346, "n_recent": 78, "psi": 0.402}
```

## 本日残レース: 49件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 107件 締切済
- 通知発射: scan=21 nid / final=19 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1111R | win | 1 | 0.5891 | 4.7 | 2.77 | 300 | scan=5.2 drift=-9.6% | 15:30:39 |
| S01_NAKAANA1 | 088R | win | 1 | 0.5998 | 3.0 | 1.80 | 200 | scan=- drift=- | 14:04:19 |
| S00 | 118R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=5.6 drift=+33.9% | 13:54:31 |
| S01_NAKAANA1 | 148R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=3.5 drift=+8.6% | 12:02:18 |
| S00 | 114R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=21.7 drift=-80.2% | 11:54:30 |
| S00 | 093R | win | 1 | 0.5174 | 4.0 | 2.07 | 300 | scan=- drift=- | 11:31:20 |
| S00 | 106R | win | 1 | 0.5174 | 6.8 | 3.52 | 300 | scan=- drift=- | 10:45:19 |
| S00 | 142R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 09:07:20 |
| S01_NAKAANA1 | 198R | win | 1 | 0.5891 | 4.4 | 2.59 | 200 | scan=3.7 drift=+18.9% | 18:43:19 |
| S01_NAKAANA1 | 208R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.3 drift=-9.1% | 18:36:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +5.8% | -80.2% | +93.9% | 11 | 3 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 513.4s |
| **Latency** (scan→final max) | 613.6s |
| **Traffic** (notifications 24h) | 70 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 425 | 0.4756 | 0.2753 | +0.2003 | 🟡+42% | 0.2420 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 171 | 0.4344 | 0.2749 | 0.2255 | 🔴-0.13 | 0.952 |
| S01_NAKAANA1 | win | 174 | 0.4841 | 0.2471 | 0.2473 | 🔴-0.33 | 0.759 |
| S02_TETSUBAN | win | 80 | 0.5452 | 0.3375 | 0.2657 | 🔴-0.19 | 0.603 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 152 | 0.4040 | 0.2368 | 🔴+0.1672 |
| 0.50+ | 251 | 0.5461 | 0.3108 | 🔴+0.2353 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 250 | 0.753 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-15T16:10:01.642217+09:00_