# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-23T15:20:02.207184+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×53 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×53 (24h)
- 🟡 FINAL_MISSING×44 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-09-23T15:03:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×17  [2026-09-23T15:03:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×17  [2026-09-23T15:03:28]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×17  [2026-09-23T15:03:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×3  [2026-09-23T14:21:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-23T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-23T13:30:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-23T12:22:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×37  [2026-09-23T11:01:36]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=41.9% hit_CI[Bonf]=[27.0,58.4]% ROI=0.75 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-23T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-23T06:00:15]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=24.4% ROI=0.47 (コスト 10,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S00: n=163 hit%=22.7% hit_CI[Bonf]=[14.7,33.4]% ROI=0.72 ROI_boot95=[0.48,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-23T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=160 hit%=21.9% hit_CI[Bonf]=[14.0,32.6]% ROI=0.65 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=26.7% ROI=0.87 (コスト 8,500/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=20.0% ROI=0.58 (コスト 9,200/回収 5,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-23T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=83 hit%=22.9% ROI=0.70 (コスト 19,300/回収 13,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.9MB / last modified 2026-09-23T15:19:33.370929+09:00

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
ust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-23 15:19:03,577 [INFO] predictor: Models loaded OK
2026-09-23 15:19:14,983 [INFO] scraper: odds3t: 120/120 parsed
2026-09-23 15:19:16,072 [INFO] scraper: odds3f: 20/20 parsed
2026-09-23 15:19:17,200 [INFO] scraper: odds2t: 30/30 parsed
2026-09-23 15:19:17,201 [INFO] scraper: odds2f: 15/15 parsed
2026-09-23 15:19:18,295 [INFO] scraper: odds_win: 6/6 parsed
2026-09-23 15:19:18,295 [INFO] scraper: fetch_race 02/10: boats=6 odds=191/191
2026-09-23 15:19:18,299 [INFO] predictor: CALIBRATION_MODE=on
2026-09-23 15:19:18,299 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-23 15:19:18,304 [INFO] run_cycle: fetched 02/10 [final]: 156 combos
2026-09-23 15:19:21,866 [INFO] scraper: odds3t: 120/120 parsed
2026-09-23 15:19:22,987 [INFO] scraper: odds3f: 20/20 parsed
2026-09-23 15:19:24,149 [INFO] scraper: odds2t: 30/30 parsed
2026-09-23 15:19:24,150 [INFO] scraper: odds2f: 15/15 parsed
2026-09-23 15:19:25,238 [INFO] scraper: odds_win: 3/6 parsed
2026-09-23 15:19:25,238 [INFO] scraper: fetch_race 03/10: boats=6 odds=188/191
2026-09-23 15:19:25,240 [INFO] predictor: CALIBRATION_MODE=on
2026-09-23 15:19:25,241 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-23 15:19:25,244 [INFO] run_cycle: fetched 03/10 [final]: 153 combos
2026-09-23 15:19:29,033 [INFO] scraper: odds3t: 120/120 parsed
2026-09-23 15:19:30,144 [INFO] scraper: odds3f: 20/20 parsed
2026-09-23 15:19:31,253 [INFO] scraper: odds2t: 30/30 parsed
2026-09-23 15:19:31,255 [INFO] scraper: odds2f: 15/15 parsed
2026-09-23 15:19:32,366 [INFO] scraper: odds_win: 6/6 parsed
2026-09-23 15:19:32,366 [INFO] scraper: fetch_race 06/9: boats=6 odds=191/191
2026-09-23 15:19:32,369 [INFO] predictor: CALIBRATION_MODE=on
2026-09-23 15:19:32,369 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-23 15:19:32,373 [INFO] run_cycle: fetched 06/9 [scan]: 156 combos
2026-09-23 15:19:32,510 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 15, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 62
  PSI_DRIFT_DETECTED: 53
  FINAL_MISSING: 44
  CIRCUIT_BREAKER_TRIP: 28
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 5
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 6 | 10,800 | 4,740 | -6,060 | 0.439 |
| S01_NAKAANA1 | 32 | 9 | 6,400 | 5,980 | -420 | 0.934 |
| S02_TETSUBAN | 20 | 11 | 4,000 | 4,240 | +240 | 1.06 |

## 直近アラート (24h・新しい順)
```
[15:18:30] FINAL_MISSING: {"deadline": "2026-09-23T14:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092302091448", "sid": "S00"}
[15:14:39] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 4740, "roi_7d": 0.439, "sid": "S00"}
[15:14:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 315, "n_recent": 88, "psi": 0.412}
[15:05:16] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 314, "n_recent": 89, "psi": 0.419}
[15:03:28] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:28] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:02:31] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 5040, "roi_7d": 0.454, "sid": "S00"}
[15:02:31] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 315, "n_recent": 89, "psi": 0.418}
[14:55:53] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 314, "n_recent": 90, "psi": 0.415}
[14:35:21] FINAL_MISSING: {"deadline": "2026-09-23T12:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092308041203", "sid": "S00"}
```

## 本日残レース: 56件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 100件 締切済
- 通知発射: scan=17 nid / final=18 nid / result=11 nid
- predictions: 13 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 201R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=2.0 drift=+0.0% | 14:55:19 |
| S00 | 089R | win | 1 | 0.4111 | 29.2 | 12.00 | 300 | scan=- drift=- | 14:28:20 |
| S02_TETSUBAN | 118R | win | 1 | 0.5123 | 2.5 | 1.28 | 200 | scan=2.4 drift=+4.2% | 13:52:18 |
| S00 | 225R | win | 1 | 0.5476 | 6.2 | 3.40 | 300 | scan=- drift=- | 13:41:19 |
| S00 | 097R | win | 1 | 0.4989 | 17.2 | 8.58 | 300 | scan=- drift=- | 13:24:20 |
| S00 | 117R | win | 1 | 0.5174 | 5.2 | 2.69 | 300 | scan=18.7 drift=-72.2% | 13:20:20 |
| S02_TETSUBAN | 116R | win | 1 | 0.4111 | 2.8 | 1.15 | 200 | scan=- drift=- | 12:51:20 |
| S00 | 116R | win | 1 | 0.4111 | 8.0 | 3.29 | 300 | scan=5.2 drift=+53.8% | 12:50:31 |
| S00 | 223R | win | 1 | 0.4989 | 12.0 | 5.99 | 300 | scan=12.0 drift=+0.0% | 12:44:19 |
| S00 | 034R | win | 1 | 0.4111 | 5.7 | 2.34 | 300 | scan=14.6 drift=-61.0% | 12:32:43 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | -3.2% | -81.7% | +87.5% | 17 | 8 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.8s |
| **Latency** (scan→final max) | 628.7s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 3,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 402 | 0.4761 | 0.2537 | +0.2224 | 🟡+47% | 0.2431 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4428 | 0.2235 | 0.2300 | 🔴-0.33 | 0.719 |
| S01_NAKAANA1 | win | 156 | 0.4849 | 0.2115 | 0.2488 | 🔴-0.49 | 0.637 |
| S02_TETSUBAN | win | 76 | 0.5328 | 0.4079 | 0.2609 | 🔴-0.08 | 0.733 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.30-0.50 | 152 | 0.4136 | 0.2303 | 🔴+0.1834 |
| 0.50+ | 232 | 0.5436 | 0.2802 | 🔴+0.2635 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 149 | 0.772 |
| win | <5.0 | ✅learned | 261 | 0.761 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-23T15:20:02.207184+09:00_