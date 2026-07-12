# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-12T10:00:01.580495+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×112 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×35 (24h)
- 🔴 PSI_DRIFT_DETECTED×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-07-12T09:47:28]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×59  [2026-07-12T09:01:04]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×118  [2026-07-12T09:01:04]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×59  [2026-07-12T09:01:04]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-07-12T09:00:06]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-12T09:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-07-12T09:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S00: n=168 hit%=30.4% hit_CI[Bonf]=[21.2,41.3]% ROI=0.79 ROI_boot95=[0.59,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S01_NAKAANA1: n=153 hit%=30.7% hit_CI[Bonf]=[21.2,42.2]% ROI=0.87 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-12T06:00:05]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=46.4% hit_CI[Bonf]=[30.4,63.1]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-12T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-12T06:00:05]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=33.3% ROI=0.87 (コスト 9,600/回収 8,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.74 (コスト 10,400/回収 7,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=34.5% ROI=0.88 (コスト 20,000/回収 17,590)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=32 hit%=37.5% ROI=1.05 (コスト 8,000/回収 8,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-12T06:00:05]
- key: `DRIFT_BUCKET|drift ≥+30%: n=28 hit%=21.4% ROI=0.42 (コスト 7,800/回収 3,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-12T06:00:05]
- key: `CALIBRATION_LIVE|bt=win: n=390 pred=0.4738 actual=0.3333 error=+0.1405 (+30%) brier=0.2371 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.46MB / last modified 2026-07-12T10:00:02.341501+09:00

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
2026-07-12 09:56:03,304 [INFO] predictor: Models loaded OK
2026-07-12 09:56:03,383 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 09:57:04,018 [INFO] run_cycle: === run_cycle 09:57:04 ===
2026-07-12 09:57:04,018 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 09:57:04,018 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 09:57:04,044 [INFO] predictor: Models loaded OK
2026-07-12 09:57:16,605 [INFO] scraper: odds3t: 120/120 parsed
2026-07-12 09:57:17,681 [INFO] scraper: odds3f: 20/20 parsed
2026-07-12 09:57:18,766 [INFO] scraper: odds2t: 29/30 parsed
2026-07-12 09:57:18,767 [INFO] scraper: odds2f: 13/15 parsed
2026-07-12 09:57:19,866 [INFO] scraper: odds_win: 6/6 parsed
2026-07-12 09:57:19,867 [INFO] scraper: fetch_race 14/4: boats=6 odds=188/191
2026-07-12 09:57:19,869 [INFO] predictor: CALIBRATION_MODE=on
2026-07-12 09:57:19,870 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-07-12 09:57:19,873 [INFO] run_cycle: fetched 14/4 [scan]: 155 combos
2026-07-12 09:57:19,956 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 09:58:03,277 [INFO] run_cycle: === run_cycle 09:58:03 ===
2026-07-12 09:58:03,277 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 09:58:03,277 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 09:58:03,318 [INFO] predictor: Models loaded OK
2026-07-12 09:58:03,408 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-12 09:59:03,532 [INFO] run_cycle: === run_cycle 09:59:03 ===
2026-07-12 09:59:03,532 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-12 09:59:03,532 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-12 09:59:03,574 [INFO] predictor: Models loaded OK
2026-07-12 09:59:03,651 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 83
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 83
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 20, 'scan': 30}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 112
  ANOMALY_SCRAPER_FAILURE_BURST: 92
  ANOMALY_SCAN_FINAL_RATIO: 41
  CIRCUIT_BREAKER_TRIP: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  PSI_DRIFT_DETECTED: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 17 | 12,600 | 12,570 | -30 | 0.998 |
| S01_NAKAANA1 | 44 | 10 | 8,800 | 5,580 | -3,220 | 0.634 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 5,400 | +1,200 | 1.286 |

## 直近アラート (24h・新しい順)
```
[09:47:28] CIRCUIT_BREAKER_TRIP: {"cost": 8800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 44, "payout": 5580, "roi_7d": 0.634, "sid": "S01_NAKAANA1"}
[09:47:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.204, "baseline_mean": 0.796, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.01}
[09:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:04] CIRCUIT_BREAKER_TRIP: {"cost": 8600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 5580, "roi_7d": 0.649, "sid": "S01_NAKAANA1"}
[09:01:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[09:01:04] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[09:00:05] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.5, "baseline_n_days": 4, "baseline_stdev": 0.6, "hour": 9, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.6}
[08:00:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:33] CIRCUIT_BREAKER_TRIP: {"cost": 8600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 5580, "roi_7d": 0.649, "sid": "S01_NAKAANA1"}
[08:00:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 181件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 192件 登録 / 11件 締切済
- 通知発射: scan=3 nid / final=4 nid / result=0 nid
- predictions: 2 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 234R | win | 1 | 0.0878 | 8.8 | 0.77 | 300 | scan=- drift=- | 09:55:42 |
| S01_NAKAANA1 | 104R | win | 1 | 0.5891 | 3.0 | 1.77 | 200 | scan=4.2 drift=-28.6% | 09:47:19 |
| S01_NAKAANA1 | 191R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=- drift=- | 17:39:34 |
| S00 | 1610R | win | 1 | 0.4111 | 6.0 | 2.47 | 300 | scan=7.5 drift=-20.0% | 16:40:24 |
| S00 | 153R | win | 1 | 0.2290 | 4.1 | 0.94 | 300 | scan=- drift=- | 16:20:35 |
| S00 | 118R | win | 1 | 0.4111 | 12.7 | 5.22 | 300 | scan=- drift=- | 14:15:45 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=3.7 drift=-18.9% | 14:13:31 |
| S01_NAKAANA1 | 098R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 14:07:21 |
| S00 | 098R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=- drift=- | 14:06:32 |
| S01_NAKAANA1 | 165R | win | 1 | 0.5334 | 4.5 | 2.40 | 200 | scan=4.5 drift=+0.0% | 13:46:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +14.5% | -73.3% | +533.3% | 19 | 7 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 479.4s |
| **Latency** (scan→final max) | 639.3s |
| **Traffic** (notifications 24h) | 83 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 389 | 0.4737 | 0.3316 | +0.1421 | 🟡+30% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4397 | 0.3036 | 0.2255 | 🔴-0.07 | 0.785 |
| S01_NAKAANA1 | win | 152 | 0.4807 | 0.3026 | 0.2413 | 🔴-0.14 | 0.859 |
| S02_TETSUBAN | win | 69 | 0.5411 | 0.4638 | 0.2561 | 🔴-0.03 | 0.891 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1783 | 0.6000 | 🔴-0.4217 |
| 0.20-0.30 | 14 | 0.2288 | 0.1429 | 🔴+0.0860 |
| 0.30-0.50 | 145 | 0.4172 | 0.3034 | 🔴+0.1137 |
| 0.50+ | 220 | 0.5418 | 0.3636 | 🔴+0.1781 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 69 | 0.79 |
| win | <5.0 | ✅learned | 132 | 0.714 |
| win | <10.0 | ✅learned | 71 | 0.467 |
| win | <20.0 | ✅learned | 22 | 0.222 |
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
_auto-generated by claude_snapshot.py at 2026-07-12T10:00:01.580495+09:00_