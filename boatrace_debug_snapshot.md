# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-10T16:10:01.781344+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×40 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×121 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×40 (24h)
- 🔴 PSI_DRIFT_DETECTED×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×8  [2026-08-10T16:06:19]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×8  [2026-08-10T16:06:19]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-08-10T16:06:19]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×49  [2026-08-10T15:21:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-10T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-10T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×40  [2026-08-10T12:34:18]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×38  [2026-08-10T11:02:54]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_DROP  ×50  [2026-08-10T10:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-08-10T06:00:14]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-10T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2237 actual=0.3636 gap=-0.1399`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S00: n=175 hit%=25.1% hit_CI[Bonf]=[17.0,35.6]% ROI=0.73 ROI_boot95=[0.51,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=24.0% hit_CI[Bonf]=[15.8,34.6]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-10T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=66 hit%=50.0% hit_CI[Bonf]=[33.3,66.7]% ROI=0.93 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-10T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=66<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=34.2% ROI=0.83 (コスト 9,400/回収 7,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-10T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=67 hit%=28.4% ROI=0.80 (コスト 15,900/回収 12,650)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.03MB / last modified 2026-08-10T16:09:06.565740+09:00

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
d
2026-08-10 16:08:25,451 [INFO] scraper: fetch_race 05/10: boats=6 odds=191/191
2026-08-10 16:08:25,453 [INFO] predictor: CALIBRATION_MODE=on
2026-08-10 16:08:25,453 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-10 16:08:25,458 [INFO] run_cycle: fetched 05/10 [scan]: 156 combos
2026-08-10 16:08:28,876 [INFO] scraper: odds3t: 120/120 parsed
2026-08-10 16:08:30,009 [INFO] scraper: odds3f: 20/20 parsed
2026-08-10 16:08:31,100 [INFO] scraper: odds2t: 30/30 parsed
2026-08-10 16:08:31,101 [INFO] scraper: odds2f: 15/15 parsed
2026-08-10 16:08:32,239 [INFO] scraper: odds_win: 6/6 parsed
2026-08-10 16:08:32,239 [INFO] scraper: fetch_race 09/12: boats=6 odds=191/191
2026-08-10 16:08:32,242 [INFO] predictor: CALIBRATION_MODE=on
2026-08-10 16:08:32,242 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-10 16:08:32,247 [INFO] run_cycle: fetched 09/12 [scan]: 156 combos
2026-08-10 16:08:35,706 [INFO] scraper: odds3t: 120/120 parsed
2026-08-10 16:08:36,802 [INFO] scraper: odds3f: 20/20 parsed
2026-08-10 16:08:37,961 [INFO] scraper: odds2t: 29/30 parsed
2026-08-10 16:08:37,963 [INFO] scraper: odds2f: 13/15 parsed
2026-08-10 16:08:39,127 [INFO] scraper: odds_win: 6/6 parsed
2026-08-10 16:08:39,127 [INFO] scraper: fetch_race 20/3: boats=6 odds=188/191
2026-08-10 16:08:39,130 [INFO] predictor: CALIBRATION_MODE=on
2026-08-10 16:08:39,130 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-08-10 16:08:39,133 [INFO] run_cycle: fetched 20/3 [scan]: 155 combos
2026-08-10 16:08:39,235 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-10 16:09:03,691 [INFO] run_cycle: === run_cycle 16:09:03 ===
2026-08-10 16:09:03,691 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-10 16:09:03,691 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-10 16:09:03,726 [INFO] predictor: Models loaded OK
2026-08-10 16:09:04,080 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 28, 'result': 16, 'scan': 31}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 121
  ANOMALY_SCRAPER_FAILURE_BURST: 88
  CIRCUIT_BREAKER_TRIP: 40
  CIRCUIT_BREAKER_NO_ACTION: 34
  ANOMALY_SCAN_FINAL_RATIO: 26
  PSI_DRIFT_DETECTED: 25
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 10
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 7,140 | -3,360 | 0.68 |
| S01_NAKAANA1 | 43 | 9 | 8,600 | 5,200 | -3,400 | 0.605 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 2,760 | -40 | 0.986 |

## 直近アラート (24h・新しい順)
```
[16:08:39] FINAL_MISSING: {"deadline": "2026-08-10T13:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081008071336", "sid": "S00"}
[16:06:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:06:19] FINAL_MISSING: {"deadline": "2026-08-10T11:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081005011133", "sid": "S00"}
[16:06:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:06:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:04:37] FINAL_MISSING: {"deadline": "2026-08-10T13:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081005051333", "sid": "S00"}
[15:58:20] FINAL_MISSING: {"deadline": "2026-08-10T14:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081016081428", "sid": "S00"}
[15:53:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.155, "baseline_mean": 0.809, "baseline_stdev": 0.049, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.654, "today_scan_count": 26, "z_score": -3.15}
[15:46:33] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.129, "baseline_mean": 0.809, "baseline_stdev": 0.049, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.68, "today_scan_count": 25, "z_score": -2.62}
[15:40:35] FINAL_MISSING: {"deadline": "2026-08-10T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081003031208", "sid": "S00"}
```

## 本日残レース: 36件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 120件 締切済
- 通知発射: scan=26 nid / final=20 nid / result=9 nid
- predictions: 12 / うち結果DB記録済: 11
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 152R | win | 1 | 0.4989 | 11.2 | 5.59 | 300 | scan=10.1 drift=+10.9% | 15:38:26 |
| S02_TETSUBAN | 058R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=- drift=- | 15:04:26 |
| S02_TETSUBAN | 098R | win | 1 | 0.5891 | 2.9 | 1.71 | 200 | scan=2.5 drift=+16.0% | 13:58:18 |
| S00 | 239R | win | 1 | 0.4111 | 22.1 | 9.09 | 300 | scan=5.7 drift=+287.7% | 12:44:20 |
| S01_NAKAANA1 | 053R | win | 1 | 0.4988 | 3.6 | 1.80 | 200 | scan=- drift=- | 12:31:20 |
| S01_NAKAANA1 | 134R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.5 drift=-4.4% | 11:51:19 |
| S00 | 237R | win | 1 | 0.4111 | 4.1 | 1.69 | 300 | scan=- drift=- | 11:43:18 |
| S01_NAKAANA1 | 237R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.3 drift=+18.2% | 11:42:19 |
| S00 | 236R | win | 1 | 0.4920 | 5.6 | 2.76 | 300 | scan=5.2 drift=+7.7% | 11:09:30 |
| S00 | 082R | win | 1 | 0.5334 | 8.6 | 4.59 | 300 | scan=4.5 drift=+91.1% | 11:02:44 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +6.2% | -73.3% | +287.7% | 17 | 8 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 532.2s |
| **Latency** (scan→final max) | 653.2s |
| **Traffic** (notifications 24h) | 75 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 401 | 0.4629 | 0.2743 | +0.1886 | 🟡+41% | 0.2367 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4148 | 0.2235 | 0.2275 | 🔴-0.31 | 0.658 |
| S01_NAKAANA1 | win | 164 | 0.4839 | 0.2317 | 0.2437 | 🔴-0.37 | 0.699 |
| S02_TETSUBAN | win | 67 | 0.5337 | 0.5075 | 0.2427 | ✅+0.03 | 0.867 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 11 | 0.1835 | 0.1818 | ✅+0.0017 |
| 0.20-0.30 | 10 | 0.2236 | 0.4000 | 🔴-0.1764 |
| 0.30-0.50 | 156 | 0.4176 | 0.2051 | 🔴+0.2125 |
| 0.50+ | 211 | 0.5437 | 0.3318 | 🔴+0.2120 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 103 | 0.776 |
| win | <5.0 | ✅learned | 178 | 0.727 |
| win | <10.0 | ✅learned | 90 | 0.453 |
| win | <20.0 | ✅learned | 29 | 0.228 |
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
_auto-generated by claude_snapshot.py at 2026-08-10T16:10:01.781344+09:00_