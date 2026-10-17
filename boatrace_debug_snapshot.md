# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-17T16:10:02.706101+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×14 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×8  [2026-10-17T16:06:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-10-17T16:06:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-10-17T16:00:22]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🔴 PSI_DRIFT_DETECTED  ×39  [2026-10-17T15:30:41]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-17T15:00:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-10-17T15:00:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-10-17T14:24:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-10-17T11:17:27]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ORPHAN_SCAN  ×1  [2026-10-17T06:00:26]
- key: `ORPHAN_SCAN|157 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=170<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-17T06:00:26]
- key: `INSUFFICIENT_SAMPLE|S00: n=180<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-17T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-17T06:00:26]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=34 pred=0.3223 actual=0.2353 gap=+0.0870`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S00: n=180 hit%=27.8% hit_CI[Bonf]=[19.3,38.2]% ROI=0.75 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S01_NAKAANA1: n=170 hit%=35.9% hit_CI[Bonf]=[26.2,46.9]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-17T06:00:26]
- key: `ROI_STAT|S02_TETSUBAN: n=86 hit%=53.5% hit_CI[Bonf]=[38.4,68.0]% ROI=0.95 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=42.4% ROI=1.07 (コスト 9,500/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=33.3% ROI=0.77 (コスト 11,300/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-17T06:00:26]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=40.2% ROI=1.19 (コスト 19,800/回収 23,500)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.06MB / last modified 2026-10-17T16:09:30.482503+09:00

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
T S00 大村3R
2026-10-17 16:08:22,529 [WARNING] scraper: beforeinfo parse failed: jcd=09 rno=12
2026-10-17 16:08:22,529 [WARNING] run_cycle: fetch None: 09/12
2026-10-17 16:08:22,695 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-17 16:09:04,394 [INFO] run_cycle: === run_cycle 16:09:04 ===
2026-10-17 16:09:04,394 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-17 16:09:04,394 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-17 16:09:04,427 [INFO] predictor: Models loaded OK
2026-10-17 16:09:16,046 [INFO] scraper: odds3t: 120/120 parsed
2026-10-17 16:09:17,119 [INFO] scraper: odds3f: 20/20 parsed
2026-10-17 16:09:18,228 [INFO] scraper: odds2t: 30/30 parsed
2026-10-17 16:09:18,230 [INFO] scraper: odds2f: 15/15 parsed
2026-10-17 16:09:19,329 [INFO] scraper: odds_win: 6/6 parsed
2026-10-17 16:09:19,329 [INFO] scraper: fetch_race 24/3: boats=6 odds=191/191
2026-10-17 16:09:19,332 [INFO] predictor: CALIBRATION_MODE=on
2026-10-17 16:09:19,332 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-17 16:09:19,336 [INFO] run_cycle: fetched 24/3 [final]: 156 combos
2026-10-17 16:09:21,702 [WARNING] scraper: beforeinfo parse failed: jcd=09 rno=12
2026-10-17 16:09:21,703 [WARNING] run_cycle: fetch None: 09/12
2026-10-17 16:09:25,386 [INFO] scraper: odds3t: 120/120 parsed
2026-10-17 16:09:26,484 [INFO] scraper: odds3f: 20/20 parsed
2026-10-17 16:09:27,658 [INFO] scraper: odds2t: 29/30 parsed
2026-10-17 16:09:27,659 [INFO] scraper: odds2f: 15/15 parsed
2026-10-17 16:09:28,803 [INFO] scraper: odds_win: 4/6 parsed
2026-10-17 16:09:28,803 [INFO] scraper: fetch_race 01/3: boats=6 odds=188/191
2026-10-17 16:09:28,805 [INFO] predictor: CALIBRATION_MODE=on
2026-10-17 16:09:28,806 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-17 16:09:28,809 [INFO] run_cycle: fetched 01/3 [scan]: 153 combos
2026-10-17 16:09:28,942 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 18, 'result': 8, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 230
  FINAL_MISSING: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 14
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 14 | 14,700 | 11,790 | -2,910 | 0.802 |
| S01_NAKAANA1 | 39 | 14 | 7,800 | 6,660 | -1,140 | 0.854 |
| S02_TETSUBAN | 24 | 14 | 4,800 | 5,220 | +420 | 1.087 |

## 直近アラート (24h・新しい順)
```
[16:06:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:06:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[16:06:29] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:01:19] FINAL_MISSING: {"deadline": "2026-10-17T13:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101703061329", "sid": "S00"}
[16:00:20] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 15.1, "baseline_n_days": 7, "baseline_stdev": 3.2, "hour": 16, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 7, "z_score": -2.56}
[15:45:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 323, "n_recent": 112, "psi": 0.271}
[15:42:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 322, "n_recent": 113, "psi": 0.27}
[15:34:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 321, "n_recent": 114, "psi": 0.268}
[15:19:40] FINAL_MISSING: {"deadline": "2026-10-17T13:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101708081348", "sid": "S01_NAKAANA1"}
[15:19:40] FINAL_MISSING: {"deadline": "2026-10-17T13:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101708081348", "sid": "S00"}
```

## 本日残レース: 47件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 121件 締切済
- 通知発射: scan=13 nid / final=16 nid / result=7 nid
- predictions: 7 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 039R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=- drift=- | 14:49:20 |
| S02_TETSUBAN | 099R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.4 drift=-12.5% | 14:31:19 |
| S02_TETSUBAN | 035R | win | 1 | 0.5719 | 2.4 | 1.37 | 200 | scan=- drift=- | 12:59:20 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=- drift=- | 12:38:18 |
| S01_NAKAANA1 | 108R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.2 drift=+15.6% | 12:08:30 |
| S00 | 084R | win | 1 | 0.3131 | 6.0 | 1.88 | 300 | scan=- drift=- | 11:41:19 |
| S00 | 093R | win | 1 | 0.4111 | 5.6 | 2.30 | 300 | scan=7.5 drift=-25.3% | 11:27:19 |
| S02_TETSUBAN | 202R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=- drift=- | 15:47:20 |
| S02_TETSUBAN | 0310R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=- drift=- | 15:19:29 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5031 | 4.0 | 2.01 | 200 | scan=- drift=- | 14:21:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +17.6% | -52.2% | +326.7% | 15 | 6 | 48 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 543.9s |
| **Latency** (scan→final max) | 672.7s |
| **Traffic** (notifications 24h) | 45 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 435 | 0.4779 | 0.3586 | +0.1193 | 🟡+25% | 0.2440 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4403 | 0.2809 | 0.2372 | 🔴-0.17 | 0.755 |
| S01_NAKAANA1 | win | 171 | 0.4907 | 0.3567 | 0.2437 | 🔴-0.06 | 1.028 |
| S02_TETSUBAN | win | 86 | 0.5305 | 0.5233 | 0.2589 | 🔴-0.04 | 0.907 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 6 | 0.1845 | 0.0000 | 🔴+0.1845 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 162 | 0.4160 | 0.3148 | 🔴+0.1012 |
| 0.50+ | 252 | 0.5441 | 0.3968 | 🔴+0.1473 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 187 | 0.773 |
| win | <5.0 | ✅learned | 332 | 0.751 |
| win | <10.0 | ✅learned | 146 | 0.462 |
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
_auto-generated by claude_snapshot.py at 2026-10-17T16:10:02.706101+09:00_