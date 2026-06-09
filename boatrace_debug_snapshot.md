# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-09T15:30:02.401234+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×63 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×63 (24h)
- 🟡 FINAL_MISSING×45 (24h)
- 🔴 CALIBRATION_DRIFT×26 (24h)
- 🔴 PSI_DRIFT_DETECTED×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CALIBRATION_DRIFT  ×27  [2026-06-09T15:03:20]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×81  [2026-06-09T15:03:20]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×81  [2026-06-09T15:03:20]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-06-09T15:03:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-09T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-09T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-09T14:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-06-09T13:26:54]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 PSI_DRIFT_DETECTED  ×32  [2026-06-09T11:01:07]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=27.0% ROI=1.00 (コスト 8,400/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-09T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S00: n=152 hit%=24.3% hit_CI[Bonf]=[15.8,35.6]% ROI=0.75 ROI_boot95=[0.50,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=152<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=144 hit%=27.8% hit_CI[Bonf]=[18.4,39.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-09T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=40.5% hit_CI[Bonf]=[26.6,56.1]% ROI=0.72 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-09T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-09T06:00:17]
- key: `ORPHAN_SCAN|149 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-09T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=28.9% ROI=0.79 (コスト 11,200/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.76MB / last modified 2026-06-09T15:30:04.254708+09:00

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
ed
2026-06-09 15:28:21,001 [INFO] scraper: fetch_race 17/10: boats=6 odds=191/191
2026-06-09 15:28:21,013 [INFO] predictor: CALIBRATION_MODE=on
2026-06-09 15:28:21,013 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-09 15:28:21,021 [INFO] run_cycle: fetched 17/10 [final]: 156 combos
2026-06-09 15:28:21,318 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-09 15:29:06,158 [INFO] run_cycle: === run_cycle 15:29:06 ===
2026-06-09 15:29:06,158 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-09 15:29:06,158 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-09 15:29:06,203 [INFO] predictor: Models loaded OK
2026-06-09 15:29:17,709 [INFO] scraper: odds3t: 120/120 parsed
2026-06-09 15:29:18,945 [INFO] scraper: odds3f: 20/20 parsed
2026-06-09 15:29:20,115 [INFO] scraper: odds2t: 30/30 parsed
2026-06-09 15:29:20,116 [INFO] scraper: odds2f: 15/15 parsed
2026-06-09 15:29:21,300 [INFO] scraper: odds_win: 4/6 parsed
2026-06-09 15:29:21,300 [INFO] scraper: fetch_race 06/9: boats=6 odds=189/191
2026-06-09 15:29:21,313 [INFO] predictor: CALIBRATION_MODE=on
2026-06-09 15:29:21,313 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-09 15:29:21,321 [INFO] run_cycle: fetched 06/9 [scan]: 154 combos
2026-06-09 15:29:25,066 [INFO] scraper: odds3t: 120/120 parsed
2026-06-09 15:29:26,207 [INFO] scraper: odds3f: 20/20 parsed
2026-06-09 15:29:27,292 [INFO] scraper: odds2t: 30/30 parsed
2026-06-09 15:29:27,293 [INFO] scraper: odds2f: 15/15 parsed
2026-06-09 15:29:28,420 [INFO] scraper: odds_win: 3/6 parsed
2026-06-09 15:29:28,420 [INFO] scraper: fetch_race 05/9: boats=6 odds=188/191
2026-06-09 15:29:28,431 [INFO] predictor: CALIBRATION_MODE=on
2026-06-09 15:29:28,431 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-06-09 15:29:28,438 [INFO] run_cycle: fetched 05/9 [scan]: 153 combos
2026-06-09 15:29:28,549 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 68
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 68
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 12, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 70
  CIRCUIT_BREAKER_TRIP: 63
  CIRCUIT_BREAKER_NO_ACTION: 51
  FINAL_MISSING: 45
  CALIBRATION_DRIFT: 26
  PSI_DRIFT_DETECTED: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 5 | 10,200 | 4,620 | -5,580 | 0.453 |
| S01_NAKAANA1 | 30 | 5 | 6,000 | 2,160 | -3,840 | 0.36 |
| S02_TETSUBAN | 24 | 6 | 4,800 | 1,720 | -3,080 | 0.358 |

## 直近アラート (24h・新しい順)
```
[15:29:28] CIRCUIT_BREAKER_TRIP: {"cost": 6000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 2160, "roi_7d": 0.36, "sid": "S01_NAKAANA1"}
[15:22:52] CALIBRATION_DRIFT: {"avg_actual": 0.186, "avg_pred": 0.4804, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 86, "overconf_pct": 61.3}
[15:10:34] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4620, "roi_7d": 0.453, "sid": "S00"}
[15:05:40] CIRCUIT_BREAKER_TRIP: {"cost": 6200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 2160, "roi_7d": 0.348, "sid": "S01_NAKAANA1"}
[15:03:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:20] FINAL_MISSING: {"deadline": "2026-06-09T10:30:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060918051030", "sid": "S00"}
[15:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[15:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:03:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:02:22] FINAL_MISSING: {"deadline": "2026-06-09T13:31:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060905051331", "sid": "S00"}
```

## 本日残レース: 61件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 83件 締切済
- 通知発射: scan=16 nid / final=19 nid / result=7 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 0910R | win | 1 | 0.5891 | 8.2 | 4.83 | 300 | scan=- drift=- | 15:10:25 |
| S01_NAKAANA1 | 058R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:05:33 |
| S00 | 098R | win | 1 | 0.4111 | 10.5 | 4.32 | 300 | scan=4.0 drift=+162.5% | 14:09:31 |
| S01_NAKAANA1 | 055R | win | 1 | 0.5719 | 3.6 | 2.06 | 200 | scan=4.8 drift=-25.0% | 13:28:31 |
| S02_TETSUBAN | 115R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=- drift=- | 12:21:22 |
| S00 | 093R | win | 1 | 0.0918 | 6.3 | 0.58 | 300 | scan=4.1 drift=+53.7% | 11:33:21 |
| S01_NAKAANA1 | 113R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=4.5 drift=+0.0% | 11:20:37 |
| S00 | 113R | win | 1 | 0.5174 | 4.5 | 2.33 | 300 | scan=4.5 drift=+0.0% | 11:20:35 |
| S00 | 092R | win | 1 | 0.5123 | 5.4 | 2.77 | 300 | scan=- drift=- | 11:05:32 |
| S01_NAKAANA1 | 111R | win | 1 | 0.5891 | 3.6 | 2.12 | 200 | scan=4.3 drift=-16.3% | 10:28:28 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | +10.7% | -62.9% | +274.6% | 15 | 7 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 503.7s |
| **Latency** (scan→final max) | 615.1s |
| **Traffic** (notifications 24h) | 68 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 373 | 0.4683 | 0.2922 | +0.1760 | 🟡+38% | 0.2378 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 149 | 0.4173 | 0.2416 | 0.2190 | 🔴-0.20 | 0.764 |
| S01_NAKAANA1 | win | 140 | 0.4890 | 0.2786 | 0.2433 | 🔴-0.21 | 0.687 |
| S02_TETSUBAN | win | 84 | 0.5240 | 0.4048 | 0.2619 | 🔴-0.09 | 0.723 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1918 | 0.2000 | ✅-0.0082 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 144 | 0.4208 | 0.2361 | 🔴+0.1847 |
| 0.50+ | 204 | 0.5420 | 0.3480 | 🔴+0.1940 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 34 | 0.743 |
| win | <5.0 | ✅learned | 62 | 0.735 |
| win | <10.0 | ✅learned | 40 | 0.525 |
| win | <20.0 | ✅learned | 13 | 0.212 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-09T15:30:02.401234+09:00_