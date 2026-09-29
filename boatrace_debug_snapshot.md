# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-29T12:20:01.647674+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×44 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×90 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×44 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-09-29T12:04:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-09-29T12:04:32]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-09-29T12:04:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×18  [2026-09-29T11:51:47]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-09-29T11:48:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-29T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-29T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

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

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=38 hit%=23.7% ROI=0.47 (コスト 8,500/回収 3,960)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-29T06:00:18]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=7.1% ROI=0.14 (コスト 11,300/回収 1,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.46MB / last modified 2026-09-29T12:19:21.943720+09:00

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
s3t: 120/120 parsed
2026-09-29 12:18:38,575 [INFO] scraper: odds3f: 20/20 parsed
2026-09-29 12:18:39,665 [INFO] scraper: odds2t: 29/30 parsed
2026-09-29 12:18:39,666 [INFO] scraper: odds2f: 14/15 parsed
2026-09-29 12:18:40,800 [INFO] scraper: odds_win: 3/6 parsed
2026-09-29 12:18:40,800 [INFO] scraper: fetch_race 05/4: boats=6 odds=186/191
2026-09-29 12:18:40,803 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 12:18:40,803 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-09-29 12:18:40,806 [INFO] run_cycle: fetched 05/4 [scan]: 152 combos
2026-09-29 12:18:40,945 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-29 12:19:04,895 [INFO] run_cycle: === run_cycle 12:19:04 ===
2026-09-29 12:19:04,895 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-29 12:19:04,895 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-29 12:19:04,926 [INFO] predictor: Models loaded OK
2026-09-29 12:19:17,373 [INFO] scraper: odds3t: 120/120 parsed
2026-09-29 12:19:18,468 [INFO] scraper: odds3f: 20/20 parsed
2026-09-29 12:19:19,679 [INFO] scraper: odds2t: 30/30 parsed
2026-09-29 12:19:19,680 [INFO] scraper: odds2f: 15/15 parsed
2026-09-29 12:19:20,823 [INFO] scraper: odds_win: 6/6 parsed
2026-09-29 12:19:20,823 [INFO] scraper: fetch_race 13/5: boats=6 odds=191/191
2026-09-29 12:19:20,827 [INFO] predictor: CALIBRATION_MODE=on
2026-09-29 12:19:20,827 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-29 12:19:20,833 [INFO] run_cycle: fetched 13/5 [final]: 156 combos
2026-09-29 12:19:21,403 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-29 12:20:05,930 [INFO] run_cycle: === run_cycle 12:20:05 ===
2026-09-29 12:20:05,930 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-29 12:20:05,930 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-29 12:20:05,997 [INFO] predictor: Models loaded OK

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
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 12, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 177
  FINAL_MISSING: 90
  CIRCUIT_BREAKER_TRIP: 44
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 3
  ANOMALY_BET_VOLUME_SPIKE: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 6 | 12,600 | 4,470 | -8,130 | 0.355 |
| S01_NAKAANA1 | 33 | 9 | 6,600 | 4,200 | -2,400 | 0.636 |
| S02_TETSUBAN | 24 | 14 | 4,800 | 4,920 | +120 | 1.025 |

## 直近アラート (24h・新しい順)
```
[12:11:44] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 4470, "roi_7d": 0.355, "sid": "S00"}
[12:11:44] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 6.4, "baseline_n_days": 7, "baseline_stdev": 1.3, "hour": 12, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 9, "z_score": 2.02}
[12:05:30] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 4470, "roi_7d": 0.363, "sid": "S00"}
[12:04:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:04:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:04:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:01:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.249, "baseline_mean": 0.832, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.583, "today_scan_count": 12, "z_score": -2.95}
[11:51:47] CIRCUIT_BREAKER_TRIP: {"cost": 6600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4200, "roi_7d": 0.636, "sid": "S01_NAKAANA1"}
[11:51:47] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.1, "baseline_n_days": 7, "baseline_stdev": 0.9, "hour": 11, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 6, "z_score": 2.06}
[11:48:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.232, "baseline_mean": 0.832, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 10, "z_score": -2.75}
```

## 本日残レース: 107件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 37件 締切済
- 通知発射: scan=13 nid / final=10 nid / result=5 nid
- predictions: 9 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 024R | win | 1 | 0.5719 | 4.0 | 2.29 | 200 | scan=3.7 drift=+8.1% | 12:11:28 |
| S00 | 024R | win | 1 | 0.5719 | 4.0 | 2.29 | 300 | scan=5.2 drift=-23.1% | 12:11:27 |
| S00 | 033R | win | 1 | 0.1957 | 5.2 | 1.02 | 300 | scan=4.8 drift=+8.3% | 12:05:27 |
| S01_NAKAANA1 | 043R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.1 drift=+54.8% | 11:51:31 |
| S01_NAKAANA1 | 032R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 11:39:30 |
| S00 | 147R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=15.7 drift=-28.7% | 11:26:31 |
| S01_NAKAANA1 | 042R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=3.5 drift=+0.0% | 11:23:21 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5990 | 3.7 | 2.22 | 200 | scan=- drift=- | 11:05:18 |
| S00 | 021R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=4.9 drift=-16.3% | 10:44:19 |
| S01_NAKAANA1 | 193R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=- drift=- | 16:09:32 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +9.1% | -72.2% | +357.1% | 20 | 6 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 445.2s |
| **Latency** (scan→final max) | 617.8s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 400 | 0.4799 | 0.2700 | +0.2099 | 🟡+44% | 0.2451 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4502 | 0.2121 | 0.2374 | 🔴-0.42 | 0.633 |
| S01_NAKAANA1 | win | 158 | 0.4892 | 0.2215 | 0.2489 | 🔴-0.44 | 0.659 |
| S02_TETSUBAN | win | 77 | 0.5243 | 0.4935 | 0.2536 | 🔴-0.01 | 0.866 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 150 | 0.4120 | 0.2200 | 🔴+0.1920 |
| 0.50+ | 236 | 0.5439 | 0.3051 | 🔴+0.2388 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 162 | 0.773 |
| win | <5.0 | ✅learned | 274 | 0.752 |
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
_auto-generated by claude_snapshot.py at 2026-09-29T12:20:01.647674+09:00_