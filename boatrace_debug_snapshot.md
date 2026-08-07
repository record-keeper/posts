# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-07T15:30:01.375830+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×25  [2026-08-07T15:05:55]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-08-07T15:05:55]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×25  [2026-08-07T15:05:55]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-08-07T15:05:55]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-07T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-07T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_DROP  ×31  [2026-08-07T13:00:23]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-08-07T12:31:45]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×15  [2026-08-07T11:37:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-07T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-07T06:00:08]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-07T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=40 hit%=25.0% ROI=0.88 (コスト 11,100/回収 9,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-07T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2244 actual=0.4000 gap=-0.1756`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-07T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-07T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-07T06:00:08]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=35.3% ROI=0.85 (コスト 8,600/回収 7,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-07T06:00:08]
- key: `ROI_STAT|S00: n=176 hit%=25.0% hit_CI[Bonf]=[16.9,35.4]% ROI=0.71 ROI_boot95=[0.49,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-07T06:00:08]
- key: `ROI_STAT|S01_NAKAANA1: n=154 hit%=24.7% hit_CI[Bonf]=[16.1,35.8]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-07T06:00:08]
- key: `ROI_STAT|S02_TETSUBAN: n=65 hit%=50.8% hit_CI[Bonf]=[33.8,67.5]% ROI=0.96 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-07T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=65<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.61MB / last modified 2026-08-07T15:30:04.473145+09:00

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
2026-08-07 15:28:18,660 [INFO] scraper: fetch_race 04/8: boats=6 odds=190/191
2026-08-07 15:28:18,663 [INFO] predictor: CALIBRATION_MODE=on
2026-08-07 15:28:18,663 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-07 15:28:18,666 [INFO] run_cycle: fetched 04/8 [final]: 155 combos
2026-08-07 15:28:18,837 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-07 15:29:04,217 [INFO] run_cycle: === run_cycle 15:29:04 ===
2026-08-07 15:29:04,217 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-07 15:29:04,217 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-07 15:29:04,263 [INFO] predictor: Models loaded OK
2026-08-07 15:29:15,915 [INFO] scraper: odds3t: 120/120 parsed
2026-08-07 15:29:17,050 [INFO] scraper: odds3f: 20/20 parsed
2026-08-07 15:29:18,153 [INFO] scraper: odds2t: 30/30 parsed
2026-08-07 15:29:18,154 [INFO] scraper: odds2f: 15/15 parsed
2026-08-07 15:29:19,245 [INFO] scraper: odds_win: 5/6 parsed
2026-08-07 15:29:19,245 [INFO] scraper: fetch_race 04/8: boats=6 odds=190/191
2026-08-07 15:29:19,248 [INFO] predictor: CALIBRATION_MODE=on
2026-08-07 15:29:19,248 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-07 15:29:19,252 [INFO] run_cycle: fetched 04/8 [final]: 155 combos
2026-08-07 15:29:22,795 [INFO] scraper: odds3t: 120/120 parsed
2026-08-07 15:29:23,993 [INFO] scraper: odds3f: 20/20 parsed
2026-08-07 15:29:25,139 [INFO] scraper: odds2t: 27/30 parsed
2026-08-07 15:29:25,140 [INFO] scraper: odds2f: 10/15 parsed
2026-08-07 15:29:26,258 [INFO] scraper: odds_win: 3/6 parsed
2026-08-07 15:29:26,258 [INFO] scraper: fetch_race 09/11: boats=6 odds=180/191
2026-08-07 15:29:26,260 [INFO] predictor: CALIBRATION_MODE=on
2026-08-07 15:29:26,261 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-08-07 15:29:26,264 [INFO] run_cycle: fetched 09/11 [scan]: 150 combos
2026-08-07 15:29:26,374 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 8, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 162
  FINAL_MISSING: 54
  PSI_DRIFT_DETECTED: 38
  CIRCUIT_BREAKER_NO_ACTION: 30
  CIRCUIT_BREAKER_TRIP: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 5
  LARGE_ODDS_DRIFT: 3
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 8 | 9,000 | 6,810 | -2,190 | 0.757 |
| S01_NAKAANA1 | 32 | 6 | 6,400 | 2,320 | -4,080 | 0.362 |
| S02_TETSUBAN | 9 | 6 | 1,800 | 2,060 | +260 | 1.144 |

## 直近アラート (24h・新しい順)
```
[15:20:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 71, "psi": 0.617}
[15:14:46] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 326, "n_recent": 71, "psi": 0.615}
[15:14:46] FINAL_MISSING: {"deadline": "2026-08-07T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080702051244", "sid": "S00"}
[15:08:19] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:05:54] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:54] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:50:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 326, "n_recent": 70, "psi": 0.636}
[14:48:37] FINAL_MISSING: {"deadline": "2026-08-07T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080702021116", "sid": "S00"}
[14:45:35] CIRCUIT_BREAKER_TRIP: {"cost": 6400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 32, "payout": 2320, "roi_7d": 0.362, "sid": "S01_NAKAANA1"}
[14:45:35] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 324, "n_recent": 72, "psi": 0.594}
```

## 本日残レース: 68件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 76件 締切済
- 通知発射: scan=14 nid / final=13 nid / result=6 nid
- predictions: 7 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 121R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:14:30 |
| S01_NAKAANA1 | 029R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=4.2 drift=-19.0% | 14:45:18 |
| S02_TETSUBAN | 099R | win | 1 | 0.5990 | 2.4 | 1.44 | 200 | scan=2.1 drift=+14.3% | 14:31:18 |
| S01_NAKAANA1 | 1011R | win | 1 | 0.5123 | 4.8 | 2.46 | 200 | scan=3.9 drift=+23.1% | 13:31:19 |
| S00 | 149R | win | 1 | 0.5334 | 5.2 | 2.77 | 300 | scan=4.2 drift=+23.8% | 12:33:30 |
| S00 | 146R | win | 1 | 0.1084 | 7.2 | 0.78 | 300 | scan=6.0 drift=+20.0% | 10:56:31 |
| S00 | 106R | win | 1 | 0.3177 | 8.5 | 2.70 | 300 | scan=4.0 drift=+112.5% | 10:47:19 |
| S01_NAKAANA1 | 129R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 18:51:29 |
| S01_NAKAANA1 | 245R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=- drift=- | 17:07:20 |
| S01_NAKAANA1 | 1410R | win | 1 | 0.4989 | 3.5 | 1.75 | 200 | scan=3.5 drift=+0.0% | 13:15:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 42 | +0.2% | -73.3% | +112.5% | 14 | 9 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 407.0s |
| **Latency** (scan→final max) | 610.6s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 395 | 0.4599 | 0.2886 | +0.1713 | 🟡+37% | 0.2343 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4125 | 0.2457 | 0.2227 | 🔴-0.20 | 0.703 |
| S01_NAKAANA1 | win | 156 | 0.4853 | 0.2436 | 0.2436 | 🔴-0.32 | 0.706 |
| S02_TETSUBAN | win | 64 | 0.5274 | 0.5156 | 0.2435 | ✅+0.03 | 1.005 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 10 | 0.2244 | 0.4000 | 🔴-0.1756 |
| 0.30-0.50 | 150 | 0.4159 | 0.2133 | 🔴+0.2026 |
| 0.50+ | 210 | 0.5402 | 0.3524 | 🔴+0.1879 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 97 | 0.791 |
| win | <5.0 | ✅learned | 171 | 0.719 |
| win | <10.0 | ✅learned | 88 | 0.449 |
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
_auto-generated by claude_snapshot.py at 2026-08-07T15:30:01.375830+09:00_