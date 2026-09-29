# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-29T15:40:02.329130+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×46 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×90 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×46 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×17  [2026-09-29T15:23:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×35  [2026-09-29T15:05:45]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×70  [2026-09-29T15:05:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×35  [2026-09-29T15:05:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-29T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-29T15:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×29  [2026-09-29T13:56:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×7  [2026-09-29T13:53:20]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-09-29T11:48:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×22  [2026-09-29T11:01:28]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-29T06:00:18]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-29T06:00:18]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=32.1% ROI=0.94 (コスト 7,900/回収 7,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S00: n=163 hit%=21.5% hit_CI[Bonf]=[13.7,32.0]% ROI=0.64 ROI_boot95=[0.41,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=21.9% hit_CI[Bonf]=[13.9,32.8]% ROI=0.66 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-29T06:00:18]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=49.4% hit_CI[Bonf]=[33.8,65.0]% ROI=0.87 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=40 hit%=25.0% ROI=0.69 (コスト 9,100/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=25.0% ROI=0.72 (コスト 20,500/回収 14,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.48MB / last modified 2026-09-29T15:39:28.124460+09:00

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

2026-09-29 15:38:54,339 [INFO] scraper: fetch_race 07/2: boats=6 odds=186/191
2026-09-29 15:38:54,343 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 15:38:54,343 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-09-29 15:38:54,348 [INFO] run_cycle: fetched 07/2 [scan]: 152 combos
2026-09-29 15:38:54,499 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-29 15:39:04,412 [INFO] run_cycle: === run_cycle 15:39:04 ===
2026-09-29 15:39:04,412 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-29 15:39:04,412 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-29 15:39:04,519 [INFO] predictor: Models loaded OK
2026-09-29 15:39:17,051 [INFO] scraper: odds3t: 120/120 parsed
2026-09-29 15:39:18,163 [INFO] scraper: odds3f: 20/20 parsed
2026-09-29 15:39:19,287 [INFO] scraper: odds2t: 30/30 parsed
2026-09-29 15:39:19,288 [INFO] scraper: odds2f: 15/15 parsed
2026-09-29 15:39:20,398 [INFO] scraper: odds_win: 5/6 parsed
2026-09-29 15:39:20,398 [INFO] scraper: fetch_race 16/10: boats=6 odds=190/191
2026-09-29 15:39:20,401 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 15:39:20,401 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-29 15:39:20,405 [INFO] run_cycle: fetched 16/10 [final]: 155 combos
2026-09-29 15:39:23,971 [INFO] scraper: odds3t: 120/120 parsed
2026-09-29 15:39:25,183 [INFO] scraper: odds3f: 20/20 parsed
2026-09-29 15:39:26,311 [INFO] scraper: odds2t: 30/30 parsed
2026-09-29 15:39:26,312 [INFO] scraper: odds2f: 15/15 parsed
2026-09-29 15:39:27,427 [INFO] scraper: odds_win: 3/6 parsed
2026-09-29 15:39:27,428 [INFO] scraper: fetch_race 13/11: boats=6 odds=188/191
2026-09-29 15:39:27,430 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 15:39:27,430 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-29 15:39:27,435 [INFO] run_cycle: fetched 13/11 [scan]: 153 combos
2026-09-29 15:39:27,802 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 77
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 77
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 19, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 98
  FINAL_MISSING: 90
  CIRCUIT_BREAKER_TRIP: 46
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  PSI_DRIFT_DETECTED: 6
  ANOMALY_BET_VOLUME_DROP: 3
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 6 | 12,000 | 4,470 | -7,530 | 0.372 |
| S01_NAKAANA1 | 36 | 11 | 7,200 | 5,360 | -1,840 | 0.744 |
| S02_TETSUBAN | 25 | 15 | 5,000 | 5,160 | +160 | 1.032 |

## 直近アラート (24h・新しい順)
```
[15:36:26] FINAL_MISSING: {"deadline": "2026-09-29T11:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092921061103", "sid": "S00"}
[15:27:23] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 303, "n_recent": 101, "psi": 0.407}
[15:23:05] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 4470, "roi_7d": 0.372, "sid": "S00"}
[15:23:05] FINAL_MISSING: {"deadline": "2026-09-29T10:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092914061051", "sid": "S00"}
[15:19:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 102, "psi": 0.408}
[15:07:39] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 303, "n_recent": 102, "psi": 0.406}
[15:05:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:05:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:58:05] FINAL_MISSING: {"deadline": "2026-09-29T12:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092914091227", "sid": "S00"}
```

## 本日残レース: 57件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 87件 締切済
- 通知発射: scan=22 nid / final=20 nid / result=14 nid
- predictions: 16 / うち結果DB記録済: 16
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 7件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 168R | win | 1 | 0.4989 | 2.7 | 1.35 | 200 | scan=2.3 drift=+17.4% | 14:35:31 |
| S01_NAKAANA1 | 056R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.9 drift=-15.4% | 13:30:23 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5891 | 4.2 | 2.47 | 200 | scan=3.4 drift=+23.5% | 13:11:20 |
| S01_NAKAANA1 | 055R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 12:59:46 |
| S00 | 055R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 12:59:44 |
| S01_NAKAANA1 | 219R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=4.9 drift=-36.7% | 12:38:21 |
| S01_NAKAANA1 | 044R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=- drift=- | 12:21:19 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5719 | 4.0 | 2.29 | 200 | scan=3.7 drift=+8.1% | 12:11:28 |
| S00 | 024R | win | 1 | 0.5719 | 4.0 | 2.29 | 300 | scan=5.2 drift=-23.1% | 12:11:27 |
| S00 | 033R | win | 1 | 0.1957 | 5.2 | 1.02 | 300 | scan=4.8 drift=+8.3% | 12:05:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +7.5% | -72.2% | +357.1% | 22 | 7 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 437.1s |
| **Latency** (scan→final max) | 617.8s |
| **Traffic** (notifications 24h) | 77 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 2,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 404 | 0.4806 | 0.2748 | +0.2058 | 🟡+43% | 0.2456 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4502 | 0.2134 | 0.2377 | 🔴-0.42 | 0.637 |
| S01_NAKAANA1 | win | 163 | 0.4906 | 0.2331 | 0.2496 | 🔴-0.40 | 0.685 |
| S02_TETSUBAN | win | 77 | 0.5242 | 0.4935 | 0.2538 | 🔴-0.02 | 0.843 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 150 | 0.4145 | 0.2333 | 🔴+0.1811 |
| 0.50+ | 239 | 0.5439 | 0.3054 | 🔴+0.2385 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 163 | 0.771 |
| win | <5.0 | ✅learned | 277 | 0.752 |
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
_auto-generated by claude_snapshot.py at 2026-09-29T15:40:02.329130+09:00_