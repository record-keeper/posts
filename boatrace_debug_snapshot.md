# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-04T12:40:01.899981+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×71 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×6 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-04T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×38  [2026-08-04T12:02:45]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-08-04T12:02:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×42  [2026-08-04T11:57:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-08-04T11:45:53]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×17  [2026-08-04T10:42:42]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_BET_VOLUME_DROP  ×31  [2026-08-04T10:00:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-04T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-04T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=75<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-04T06:00:07]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-04T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-04T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-04T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-04T06:00:07]
- key: `ROI_STAT|S00: n=176 hit%=27.3% hit_CI[Bonf]=[18.8,37.8]% ROI=0.74 ROI_boot95=[0.54,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-04T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=23.8% hit_CI[Bonf]=[15.6,34.5]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-04T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=75 hit%=50.7% hit_CI[Bonf]=[34.8,66.4]% ROI=0.98 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-04T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=26.5% ROI=0.63 (コスト 10,000/回収 6,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-04T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=37 hit%=37.8% ROI=0.90 (コスト 9,100/回収 8,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-04T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=66 hit%=31.8% ROI=0.76 (コスト 15,400/回収 11,710)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-04T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=23.3% ROI=0.47 (コスト 10,100/回収 4,740)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.4MB / last modified 2026-08-04T12:39:31.191554+09:00

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
5000
2026-08-04 12:38:04,544 [INFO] predictor: Models loaded OK
2026-08-04 12:38:16,923 [INFO] scraper: odds3t: 120/120 parsed
2026-08-04 12:38:17,996 [INFO] scraper: odds3f: 20/20 parsed
2026-08-04 12:38:19,101 [INFO] scraper: odds2t: 30/30 parsed
2026-08-04 12:38:19,103 [INFO] scraper: odds2f: 14/15 parsed
2026-08-04 12:38:20,175 [INFO] scraper: odds_win: 6/6 parsed
2026-08-04 12:38:20,175 [INFO] scraper: fetch_race 06/4: boats=6 odds=190/191
2026-08-04 12:38:20,179 [INFO] predictor: CALIBRATION_MODE=on
2026-08-04 12:38:20,179 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-04 12:38:20,183 [INFO] run_cycle: fetched 06/4 [final]: 156 combos
2026-08-04 12:38:20,505 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-04 12:39:04,568 [INFO] run_cycle: === run_cycle 12:39:04 ===
2026-08-04 12:39:04,568 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-04 12:39:04,568 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-04 12:39:04,642 [INFO] predictor: Models loaded OK
2026-08-04 12:39:15,709 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=06&hd=20260804: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-04 12:39:27,133 [INFO] scraper: odds3t: 120/120 parsed
2026-08-04 12:39:28,238 [INFO] scraper: odds3f: 20/20 parsed
2026-08-04 12:39:29,337 [INFO] scraper: odds2t: 30/30 parsed
2026-08-04 12:39:29,338 [INFO] scraper: odds2f: 15/15 parsed
2026-08-04 12:39:30,427 [INFO] scraper: odds_win: 6/6 parsed
2026-08-04 12:39:30,427 [INFO] scraper: fetch_race 06/4: boats=6 odds=191/191
2026-08-04 12:39:30,431 [INFO] predictor: CALIBRATION_MODE=on
2026-08-04 12:39:30,431 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-04 12:39:30,435 [INFO] run_cycle: fetched 06/4 [final]: 156 combos
2026-08-04 12:39:30,675 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 45
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 45
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 11, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 195
  FINAL_MISSING: 71
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 9
  CIRCUIT_BREAKER_TRIP: 6
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 10 | 10,800 | 7,500 | -3,300 | 0.694 |
| S01_NAKAANA1 | 36 | 8 | 7,200 | 5,440 | -1,760 | 0.756 |
| S02_TETSUBAN | 16 | 8 | 3,200 | 2,680 | -520 | 0.838 |

## 直近アラート (24h・新しい順)
```
[12:15:21] FINAL_MISSING: {"deadline": "2026-08-04T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080410081145", "sid": "S00"}
[12:02:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:02:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:01:03] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.241, "baseline_mean": 0.841, "baseline_stdev": 0.094, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -2.57}
[11:57:31] CIRCUIT_BREAKER_TRIP: {"cost": 10800, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 7500, "roi_7d": 0.694, "sid": "S00"}
[11:45:53] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.341, "baseline_mean": 0.841, "baseline_stdev": 0.094, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -3.64}
[11:01:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[10:42:42] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 1.5, "baseline_n_days": 6, "baseline_stdev": 0.5, "hour": 10, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 3, "z_score": 2.74}
[10:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 92件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 40件 締切済
- 通知発射: scan=6 nid / final=5 nid / result=3 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 218R | win | 1 | 0.5123 | 4.5 | 2.31 | 300 | scan=- drift=- | 11:57:20 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5209 | 4.1 | 2.14 | 200 | scan=4.5 drift=-8.9% | 10:42:33 |
| S00 | 106R | win | 1 | 0.5209 | 4.1 | 2.14 | 300 | scan=4.5 drift=-8.9% | 10:42:31 |
| S00 | 131R | win | 1 | 0.1957 | 7.0 | 1.37 | 300 | scan=14.2 drift=-50.7% | 10:31:30 |
| S02_TETSUBAN | 2010R | win | 1 | 0.5123 | 2.7 | 1.38 | 200 | scan=- drift=- | 19:33:29 |
| S01_NAKAANA1 | 016R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=- drift=- | 17:25:18 |
| S00 | 204R | win | 1 | 0.5735 | 5.0 | 2.87 | 300 | scan=- drift=- | 16:37:19 |
| S00 | 201R | win | 1 | 0.5123 | 11.2 | 5.74 | 300 | scan=11.2 drift=+0.0% | 15:18:19 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5891 | 3.2 | 1.89 | 200 | scan=4.0 drift=-20.0% | 15:15:29 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5891 | 3.2 | 1.89 | 200 | scan=- drift=- | 14:15:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | +11.6% | -65.9% | +375.6% | 17 | 10 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 402.3s |
| **Latency** (scan→final max) | 623.0s |
| **Traffic** (notifications 24h) | 45 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 413 | 0.4619 | 0.2978 | +0.1641 | 🟡+36% | 0.2329 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4181 | 0.2697 | 0.2239 | 🔴-0.14 | 0.728 |
| S01_NAKAANA1 | win | 161 | 0.4793 | 0.2360 | 0.2364 | 🔴-0.31 | 0.717 |
| S02_TETSUBAN | win | 74 | 0.5294 | 0.5000 | 0.2470 | ✅+0.01 | 0.959 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1253 | 0.1818 | 🔴-0.0565 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 160 | 0.4193 | 0.2250 | 🔴+0.1943 |
| 0.50+ | 218 | 0.5408 | 0.3624 | 🔴+0.1784 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 95 | 0.789 |
| win | <5.0 | ✅learned | 166 | 0.724 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 28 | 0.219 |
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
_auto-generated by claude_snapshot.py at 2026-08-04T12:40:01.899981+09:00_