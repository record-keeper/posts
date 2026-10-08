# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-08T10:20:01.229294+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×37 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×16 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×19  [2026-10-08T10:01:17]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×19  [2026-10-08T10:01:17]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-10-08T10:00:13]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-08T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-08T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-08T06:00:47]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-08T06:00:47]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-08T06:00:47]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-08T06:00:47]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=21.7% ROI=0.66 (コスト 12,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-08T06:00:47]
- key: `ROI_STAT|S00: n=165 hit%=23.0% hit_CI[Bonf]=[15.0,33.6]% ROI=0.60 ROI_boot95=[0.41,0.81]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-08T06:00:47]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=30.9% hit_CI[Bonf]=[21.5,42.1]% ROI=0.97 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-08T06:00:47]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=47.0% hit_CI[Bonf]=[32.2,62.3]% ROI=0.81 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-08T06:00:47]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=39.3% ROI=0.97 (コスト 7,900/回収 7,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-08T06:00:47]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=48 hit%=22.9% ROI=0.60 (コスト 11,400/回収 6,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-08T06:00:47]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=30.7% ROI=0.80 (コスト 19,900/回収 15,950)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-08T06:00:47]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=45 hit%=37.8% ROI=0.82 (コスト 10,500/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-08T06:00:47]
- key: `CALIBRATION_LIVE|bt=win: n=410 pred=0.4800 actual=0.3098 error=+0.1702 (+35%) brier=0.2489 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-08T06:00:47]
- key: `CALIBRATION_LIVE|S00(win): n=165 pred=0.4499 hit=0.2303 cal_err=+0.2196 brier=0.2454 BSS=-0.38 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-08T06:00:47]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=162 pred=0.4893 hit=0.3086 cal_err=+0.1806 brier=0.2480 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-08T06:00:47]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=83 pred=0.5216 hit=0.4699 cal_err=+0.0517 brier=0.2578 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.18MB / last modified 2026-10-08T10:19:04.663134+09:00

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
 parsed
2026-10-08 10:17:25,348 [INFO] scraper: odds2t: 30/30 parsed
2026-10-08 10:17:25,350 [INFO] scraper: odds2f: 15/15 parsed
2026-10-08 10:17:26,458 [INFO] scraper: odds_win: 6/6 parsed
2026-10-08 10:17:26,458 [INFO] scraper: fetch_race 14/5: boats=6 odds=191/191
2026-10-08 10:17:26,460 [INFO] predictor: CALIBRATION_MODE=on
2026-10-08 10:17:26,461 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-08 10:17:26,465 [INFO] run_cycle: fetched 14/5 [scan]: 156 combos
2026-10-08 10:17:26,604 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-08 10:18:03,772 [INFO] run_cycle: === run_cycle 10:18:03 ===
2026-10-08 10:18:03,772 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-08 10:18:03,773 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-08 10:18:03,818 [INFO] predictor: Models loaded OK
2026-10-08 10:18:16,460 [INFO] scraper: odds3t: 120/120 parsed
2026-10-08 10:18:17,568 [INFO] scraper: odds3f: 17/20 parsed
2026-10-08 10:18:18,673 [INFO] scraper: odds2t: 27/30 parsed
2026-10-08 10:18:18,674 [INFO] scraper: odds2f: 13/15 parsed
2026-10-08 10:18:19,800 [INFO] scraper: odds_win: 3/6 parsed
2026-10-08 10:18:19,800 [INFO] scraper: fetch_race 11/1: boats=6 odds=180/191
2026-10-08 10:18:19,804 [INFO] predictor: CALIBRATION_MODE=on
2026-10-08 10:18:19,804 [INFO] predictor: combos: {'win': 3, '2t': 27, '3t': 120}
2026-10-08 10:18:19,807 [INFO] run_cycle: fetched 11/1 [scan]: 150 combos
2026-10-08 10:18:19,930 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-08 10:19:03,707 [INFO] run_cycle: === run_cycle 10:19:03 ===
2026-10-08 10:19:03,707 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-08 10:19:03,707 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-08 10:19:03,738 [INFO] predictor: Models loaded OK
2026-10-08 10:19:03,940 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 39
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 39
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 10, 'scan': 14}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 41
  FINAL_MISSING: 37
  ANOMALY_SCAN_FINAL_RATIO: 24
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 16
  ANOMALY_BET_VOLUME_DROP: 6
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 15 | 13,500 | 11,430 | -2,070 | 0.847 |
| S01_NAKAANA1 | 44 | 18 | 8,800 | 11,880 | +3,080 | 1.35 |
| S02_TETSUBAN | 19 | 7 | 3,800 | 2,420 | -1,380 | 0.637 |

## 直近アラート (24h・新しい順)
```
[10:02:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:02:19] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 108, "psi": 0.267}
[10:00:05] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.1, "baseline_n_days": 7, "baseline_stdev": 0.7, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -3.11}
[09:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 108, "psi": 0.267}
[08:00:47] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:47] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 108, "psi": 0.267}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 108, "psi": 0.267}
[23:59:03] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 302, "n_recent": 108, "psi": 0.267}
```

## 本日残レース: 135件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 9件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 206R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=2.3 drift=-8.7% | 20:22:19 |
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=2.1 drift=+0.0% | 18:31:18 |
| S02_TETSUBAN | 078R | win | 1 | 0.5735 | 2.1 | 1.20 | 200 | scan=2.0 drift=+5.0% | 18:22:19 |
| S02_TETSUBAN | 075R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 16:59:19 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=- drift=- | 16:45:19 |
| S02_TETSUBAN | 074R | win | 1 | 0.5334 | 2.8 | 1.49 | 200 | scan=- drift=- | 16:32:18 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.3 drift=+11.6% | 15:52:23 |
| S00 | 012R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.3 drift=+11.6% | 15:52:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 10:39:19 |
| S00 | 111R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=- drift=- | 10:27:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 71 | +7.1% | -73.0% | +169.2% | 22 | 9 | 53 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 458.5s |
| **Latency** (scan→final max) | 604.5s |
| **Traffic** (notifications 24h) | 39 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 410 | 0.4800 | 0.3098 | +0.1702 | 🟡+36% | 0.2489 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4499 | 0.2303 | 0.2454 | 🔴-0.38 | 0.596 |
| S01_NAKAANA1 | win | 162 | 0.4893 | 0.3086 | 0.2480 | 🔴-0.16 | 0.966 |
| S02_TETSUBAN | win | 83 | 0.5216 | 0.4699 | 0.2578 | 🔴-0.04 | 0.812 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 160 | 0.4216 | 0.2812 | 🔴+0.1403 |
| 0.50+ | 234 | 0.5431 | 0.3333 | 🔴+0.2098 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 171 | 0.77 |
| win | <5.0 | ✅learned | 302 | 0.763 |
| win | <10.0 | ✅learned | 136 | 0.457 |
| win | <20.0 | ✅learned | 38 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-08T10:20:01.229294+09:00_