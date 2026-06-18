# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-18T09:50:02.184145+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×58 (24h)
- 🔴 PSI_DRIFT_DETECTED×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×49  [2026-06-18T09:01:33]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×49  [2026-06-18T09:01:33]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×50  [2026-06-18T09:00:11]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-18T06:00:20]
- key: `ORPHAN_SCAN|137 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=21 pred=0.3200 actual=0.3333 gap=-0.0134`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=26.5% ROI=0.80 (コスト 9,900/回収 7,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=18.5% ROI=0.40 (コスト 7,600/回収 3,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S00: n=147 hit%=27.9% hit_CI[Bonf]=[18.6,39.5]% ROI=0.84 ROI_boot95=[0.59,1.13]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S00: n=147<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S01_NAKAANA1: n=135 hit%=28.9% hit_CI[Bonf]=[19.1,41.1]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-18T06:00:20]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=135<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-18T06:00:20]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=36.4% hit_CI[Bonf]=[22.6,52.8]% ROI=0.59 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=32 hit%=12.5% ROI=0.23 (コスト 7,200/回収 1,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=29.4% ROI=0.66 (コスト 16,000/回収 10,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-18T06:00:20]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=39 hit%=23.1% ROI=1.04 (コスト 9,000/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|bt=win: n=359 pred=0.4710 actual=0.3008 error=+0.1702 (+36%) brier=0.2377 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|S00(win): n=147 pred=0.4243 hit=0.2789 cal_err=+0.1454 brier=0.2167 BSS=-0.08 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-18T06:00:20]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=135 pred=0.4852 hit=0.2889 cal_err=+0.1963 brier=0.2451 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.3MB / last modified 2026-06-18T09:49:16.331795+09:00

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
7:32,827 [INFO] scraper: odds_win: 6/6 parsed
2026-06-18 09:47:32,827 [INFO] scraper: fetch_race 21/4: boats=6 odds=191/191
2026-06-18 09:47:32,838 [INFO] predictor: CALIBRATION_MODE=on
2026-06-18 09:47:32,838 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-18 09:47:32,845 [INFO] run_cycle: fetched 21/4 [final]: 156 combos
2026-06-18 09:47:32,962 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-18 09:48:05,390 [INFO] run_cycle: === run_cycle 09:48:05 ===
2026-06-18 09:48:05,391 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-18 09:48:05,391 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-18 09:48:05,454 [INFO] predictor: Models loaded OK
2026-06-18 09:48:17,007 [INFO] scraper: odds3t: 120/120 parsed
2026-06-18 09:48:18,128 [INFO] scraper: odds3f: 20/20 parsed
2026-06-18 09:48:19,247 [INFO] scraper: odds2t: 30/30 parsed
2026-06-18 09:48:19,248 [INFO] scraper: odds2f: 15/15 parsed
2026-06-18 09:48:20,338 [INFO] scraper: odds_win: 6/6 parsed
2026-06-18 09:48:20,338 [INFO] scraper: fetch_race 21/4: boats=6 odds=191/191
2026-06-18 09:48:20,349 [INFO] predictor: CALIBRATION_MODE=on
2026-06-18 09:48:20,350 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-18 09:48:20,357 [INFO] run_cycle: fetched 21/4 [final]: 156 combos
2026-06-18 09:48:20,449 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-18 09:49:04,443 [INFO] run_cycle: === run_cycle 09:49:04 ===
2026-06-18 09:49:04,443 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-18 09:49:04,443 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-18 09:49:04,488 [INFO] predictor: Models loaded OK
2026-06-18 09:49:15,989 [WARNING] scraper: beforeinfo parse failed: jcd=18 rno=4
2026-06-18 09:49:15,989 [WARNING] run_cycle: fetch None: 18/4
2026-06-18 09:49:15,989 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 12, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 165
  FINAL_MISSING: 58
  PSI_DRIFT_DETECTED: 35
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_NO_ACTION: 14
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 13 | 10,500 | 11,790 | +1,290 | 1.123 |
| S01_NAKAANA1 | 29 | 10 | 5,800 | 7,160 | +1,360 | 1.234 |
| S02_TETSUBAN | 16 | 8 | 3,200 | 2,460 | -740 | 0.769 |

## 直近アラート (24h・新しい順)
```
[09:22:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 279, "n_recent": 80, "psi": 0.377}
[09:01:33] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 278, "n_recent": 81, "psi": 0.38}
[09:00:10] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.3, "baseline_n_days": 3, "baseline_stdev": 0.6, "hour": 9, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.31}
[08:00:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 278, "n_recent": 81, "psi": 0.38}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 278, "n_recent": 81, "psi": 0.38}
[23:53:05] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 278, "n_recent": 81, "psi": 0.38}
[23:51:05] FINAL_MISSING: {"deadline": "2026-06-17T15:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061712011516", "sid": "S00"}
```

## 本日残レース: 149件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 7件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 4.3 | 2.22 | 200 | scan=4.5 drift=-4.4% | 17:06:22 |
| S00 | 073R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=10.5 drift=-28.6% | 16:24:21 |
| S00 | 122R | win | 1 | 0.2173 | 9.3 | 2.02 | 300 | scan=7.5 drift=+24.0% | 15:41:21 |
| S00 | 071R | win | 1 | 0.5735 | 5.5 | 3.15 | 300 | scan=4.5 drift=+22.2% | 15:22:33 |
| S01_NAKAANA1 | 0910R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=3.2 drift=-6.2% | 15:15:22 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5891 | 4.0 | 2.36 | 200 | scan=- drift=- | 14:21:21 |
| S00 | 177R | win | 1 | 0.4111 | 6.9 | 2.84 | 300 | scan=5.6 drift=+23.2% | 13:46:20 |
| S01_NAKAANA1 | 223R | win | 1 | 0.5735 | 4.6 | 2.64 | 200 | scan=4.6 drift=+0.0% | 13:26:32 |
| S01_NAKAANA1 | 052R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=- drift=- | 12:03:21 |
| S02_TETSUBAN | 133R | win | 1 | 0.5297 | 2.5 | 1.32 | 200 | scan=- drift=- | 11:25:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | -4.4% | -82.9% | +87.5% | 15 | 9 | 27 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 475.1s |
| **Latency** (scan→final max) | 658.7s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 359 | 0.4710 | 0.3008 | +0.1702 | 🟡+36% | 0.2377 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 147 | 0.4243 | 0.2789 | 0.2167 | 🔴-0.08 | 0.844 |
| S01_NAKAANA1 | win | 135 | 0.4852 | 0.2889 | 0.2451 | 🔴-0.19 | 0.831 |
| S02_TETSUBAN | win | 77 | 0.5353 | 0.3636 | 0.2651 | 🔴-0.15 | 0.592 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 126 | 0.4176 | 0.2460 | 🔴+0.1716 |
| 0.50+ | 208 | 0.5414 | 0.3558 | 🔴+0.1857 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 43 | 0.717 |
| win | <5.0 | ✅learned | 78 | 0.755 |
| win | <10.0 | ✅learned | 53 | 0.493 |
| win | <20.0 | ✅learned | 14 | 0.21 |
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
_auto-generated by claude_snapshot.py at 2026-06-18T09:50:02.184145+09:00_