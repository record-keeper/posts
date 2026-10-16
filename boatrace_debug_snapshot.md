# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-16T11:40:01.606462+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×3 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-10-16T11:23:59]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-10-16T11:13:25]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×37  [2026-10-16T11:02:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-10-16T11:02:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-16T11:00:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-10-16T10:45:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ORPHAN_SCAN  ×1  [2026-10-16T06:00:19]
- key: `ORPHAN_SCAN|156 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=87<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-16T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S00: n=180 hit%=26.7% hit_CI[Bonf]=[18.3,37.1]% ROI=0.73 ROI_boot95=[0.53,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=35.3% hit_CI[Bonf]=[25.6,46.3]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-16T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=87 hit%=51.7% hit_CI[Bonf]=[36.8,66.3]% ROI=0.93 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=39.4% ROI=1.00 (コスト 9,500/回収 9,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=32.0% ROI=0.74 (コスト 11,800/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=38.5% ROI=1.09 (コスト 21,000/回収 22,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=58 hit%=36.2% ROI=0.86 (コスト 13,800/回収 11,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-16T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=23.9% ROI=0.79 (コスト 11,800/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=437 pred=0.4784 actual=0.3501 error=+0.1283 (+27%) brier=0.2482 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-16T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=180 pred=0.4435 hit=0.2667 cal_err=+0.1768 brier=0.2458 BSS=-0.26 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.89MB / last modified 2026-10-16T11:39:25.740418+09:00

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
sed
2026-10-16 11:38:31,704 [INFO] scraper: fetch_race 03/2: boats=6 odds=190/191
2026-10-16 11:38:31,707 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 11:38:31,707 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-16 11:38:31,711 [INFO] run_cycle: fetched 03/2 [final]: 155 combos
2026-10-16 11:38:32,275 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-16 11:39:03,587 [INFO] run_cycle: === run_cycle 11:39:03 ===
2026-10-16 11:39:03,587 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-16 11:39:03,587 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-16 11:39:03,618 [INFO] predictor: Models loaded OK
2026-10-16 11:39:15,179 [INFO] scraper: odds3t: 120/120 parsed
2026-10-16 11:39:16,310 [INFO] scraper: odds3f: 20/20 parsed
2026-10-16 11:39:17,389 [INFO] scraper: odds2t: 30/30 parsed
2026-10-16 11:39:17,391 [INFO] scraper: odds2f: 15/15 parsed
2026-10-16 11:39:18,483 [INFO] scraper: odds_win: 5/6 parsed
2026-10-16 11:39:18,483 [INFO] scraper: fetch_race 03/2: boats=6 odds=190/191
2026-10-16 11:39:18,487 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 11:39:18,487 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-16 11:39:18,491 [INFO] run_cycle: fetched 03/2 [final]: 155 combos
2026-10-16 11:39:22,009 [INFO] scraper: odds3t: 120/120 parsed
2026-10-16 11:39:23,095 [INFO] scraper: odds3f: 20/20 parsed
2026-10-16 11:39:24,208 [INFO] scraper: odds2t: 30/30 parsed
2026-10-16 11:39:24,209 [INFO] scraper: odds2f: 15/15 parsed
2026-10-16 11:39:25,289 [INFO] scraper: odds_win: 6/6 parsed
2026-10-16 11:39:25,289 [INFO] scraper: fetch_race 02/3: boats=6 odds=191/191
2026-10-16 11:39:25,293 [INFO] predictor: CALIBRATION_MODE=on
2026-10-16 11:39:25,293 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-16 11:39:25,299 [INFO] run_cycle: fetched 02/3 [scan]: 156 combos
2026-10-16 11:39:25,607 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 19, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 116
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 16
  ANOMALY_BET_VOLUME_SPIKE: 3
  CIRCUIT_BREAKER_TRIP: 3
  ANOMALY_SCAN_FINAL_RATIO: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 10 | 14,100 | 10,200 | -3,900 | 0.723 |
| S01_NAKAANA1 | 43 | 16 | 8,600 | 6,400 | -2,200 | 0.744 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 4,300 | +100 | 1.024 |

## 直近アラート (24h・新しい順)
```
[11:39:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1153}
[11:38:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1158}
[11:37:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1157}
[11:36:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1139}
[11:35:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1124}
[11:34:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1141}
[11:33:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1123}
[11:32:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1119}
[11:31:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1121}
[11:29:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1111}
```

## 本日残レース: 120件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 36件 締切済
- 通知発射: scan=4 nid / final=6 nid / result=2 nid
- predictions: 7 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 107R | win | 1 | 0.4038 | 9.3 | 3.76 | 300 | scan=4.0 drift=+132.5% | 11:36:19 |
| S00 | 133R | win | 1 | 0.1957 | 17.2 | 3.37 | 300 | scan=- drift=- | 11:31:31 |
| S01_NAKAANA1 | 093R | win | 1 | 0.5735 | 4.8 | 2.75 | 200 | scan=- drift=- | 11:27:20 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=3.7 drift=+10.8% | 11:13:21 |
| S00 | 022R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=- drift=- | 11:13:19 |
| S01_NAKAANA1 | 216R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=- drift=- | 11:01:19 |
| S00 | 082R | win | 1 | 0.1371 | 5.0 | 0.69 | 300 | scan=4.3 drift=+16.3% | 10:42:21 |
| S00 | 248R | win | 1 | 0.1156 | 5.4 | 0.62 | 300 | scan=4.8 drift=+12.5% | 18:36:20 |
| S01_NAKAANA1 | 244R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=- drift=- | 16:46:19 |
| S00 | 153R | win | 1 | 0.5735 | 5.2 | 2.98 | 300 | scan=5.2 drift=+0.0% | 16:10:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 68 | +19.4% | -52.2% | +326.7% | 14 | 6 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 359.2s |
| **Latency** (scan→final max) | 593.5s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 433 | 0.4790 | 0.3533 | +0.1256 | 🟡+26% | 0.2465 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4444 | 0.2655 | 0.2420 | 🔴-0.24 | 0.718 |
| S01_NAKAANA1 | win | 169 | 0.4899 | 0.3609 | 0.2446 | 🔴-0.06 | 1.043 |
| S02_TETSUBAN | win | 87 | 0.5283 | 0.5172 | 0.2594 | 🔴-0.04 | 0.925 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 159 | 0.4174 | 0.3208 | 🔴+0.0967 |
| 0.50+ | 254 | 0.5431 | 0.3819 | 🔴+0.1612 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 183 | 0.772 |
| win | <5.0 | ✅learned | 328 | 0.751 |
| win | <10.0 | ✅learned | 142 | 0.463 |
| win | <20.0 | ✅learned | 42 | 0.244 |
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
_auto-generated by claude_snapshot.py at 2026-10-16T11:40:01.606462+09:00_