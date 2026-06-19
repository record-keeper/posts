# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-19T09:10:01.534657+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×40 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×78 (24h)
- 🔴 PSI_DRIFT_DETECTED×40 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×3 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×8  [2026-06-19T09:02:07]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-06-19T09:02:07]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×10  [2026-06-19T09:00:26]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1835 actual=0.2000 gap=-0.0165`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-19T06:00:19]
- key: `ORPHAN_SCAN|139 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S00: n=146 hit%=28.8% hit_CI[Bonf]=[19.3,40.5]% ROI=0.82 ROI_boot95=[0.58,1.09]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=146<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=132 hit%=29.5% hit_CI[Bonf]=[19.6,41.9]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-19T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=132<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-19T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=35.9% hit_CI[Bonf]=[22.3,52.2]% ROI=0.58 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=28.6% ROI=0.87 (コスト 10,200/回収 8,910)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=12.9% ROI=0.24 (コスト 6,900/回収 1,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=69 hit%=30.4% ROI=0.72 (コスト 16,300/回収 11,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=38 hit%=23.7% ROI=1.05 (コスト 8,900/回収 9,350)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-19T06:00:19]
- key: `DRIFT_BUCKET|drift ≥+30%: n=27 hit%=22.2% ROI=0.46 (コスト 7,500/回収 3,450)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=356 pred=0.4721 actual=0.3062 error=+0.1660 (+35%) brier=0.2400 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=146 pred=0.4270 hit=0.2877 cal_err=+0.1393 brier=0.2199 BSS=-0.07 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-19T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=132 pred=0.4850 hit=0.2955 cal_err=+0.1895 brier=0.2475 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.36MB / last modified 2026-06-19T09:09:05.524806+09:00

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
arsed
2026-06-19 09:07:21,748 [INFO] scraper: odds2t: 30/30 parsed
2026-06-19 09:07:21,749 [INFO] scraper: odds2f: 15/15 parsed
2026-06-19 09:07:22,842 [INFO] scraper: odds_win: 6/6 parsed
2026-06-19 09:07:22,842 [INFO] scraper: fetch_race 18/2: boats=6 odds=191/191
2026-06-19 09:07:22,854 [INFO] predictor: CALIBRATION_MODE=on
2026-06-19 09:07:22,854 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-19 09:07:22,862 [INFO] run_cycle: fetched 18/2 [final]: 156 combos
2026-06-19 09:07:22,986 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-19 09:08:05,886 [INFO] run_cycle: === run_cycle 09:08:05 ===
2026-06-19 09:08:05,886 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-19 09:08:05,886 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-19 09:08:05,953 [INFO] predictor: Models loaded OK
2026-06-19 09:08:18,511 [INFO] scraper: odds3t: 120/120 parsed
2026-06-19 09:08:19,632 [INFO] scraper: odds3f: 20/20 parsed
2026-06-19 09:08:20,716 [INFO] scraper: odds2t: 30/30 parsed
2026-06-19 09:08:20,718 [INFO] scraper: odds2f: 15/15 parsed
2026-06-19 09:08:21,804 [INFO] scraper: odds_win: 6/6 parsed
2026-06-19 09:08:21,804 [INFO] scraper: fetch_race 18/2: boats=6 odds=191/191
2026-06-19 09:08:21,817 [INFO] predictor: CALIBRATION_MODE=on
2026-06-19 09:08:21,817 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-19 09:08:21,825 [INFO] run_cycle: fetched 18/2 [final]: 156 combos
2026-06-19 09:08:21,939 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-19 09:09:05,310 [INFO] run_cycle: === run_cycle 09:09:05 ===
2026-06-19 09:09:05,312 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-19 09:09:05,312 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-19 09:09:05,385 [INFO] predictor: Models loaded OK
2026-06-19 09:09:05,393 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 46
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 46
  }
]
```

## Phase別通知記録 (24h)
{'final': 16, 'result': 7, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 103
  FINAL_MISSING: 78
  PSI_DRIFT_DETECTED: 40
  ANOMALY_SCAN_FINAL_RATIO: 31
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 3
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 10 | 8,400 | 9,780 | +1,380 | 1.164 |
| S01_NAKAANA1 | 26 | 8 | 5,200 | 6,220 | +1,020 | 1.196 |
| S02_TETSUBAN | 13 | 7 | 2,600 | 2,100 | -500 | 0.808 |

## 直近アラート (24h・新しい順)
```
[09:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:02:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 288, "n_recent": 68, "psi": 0.604}
[09:00:25] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.3, "baseline_n_days": 3, "baseline_stdev": 0.6, "hour": 9, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.31}
[08:01:14] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:01:14] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 288, "n_recent": 68, "psi": 0.604}
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 288, "n_recent": 68, "psi": 0.604}
[23:56:06] FINAL_MISSING: {"deadline": "2026-06-18T16:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061801031620", "sid": "S00"}
[23:48:06] FINAL_MISSING: {"deadline": "2026-06-18T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061817041212", "sid": "S00"}
[23:48:06] FINAL_MISSING: {"deadline": "2026-06-18T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026061809061311", "sid": "S00"}
```

## 本日残レース: 140件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 4件 締切済
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
| S02_TETSUBAN | 201R | win | 1 | 0.5123 | 2.6 | 1.33 | 200 | scan=2.1 drift=+23.8% | 17:38:56 |
| S01_NAKAANA1 | 015R | win | 1 | 0.3599 | 4.3 | 1.55 | 200 | scan=3.0 drift=+43.3% | 17:15:22 |
| S00 | 099R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=14.0 drift=-61.4% | 14:45:30 |
| S02_TETSUBAN | 055R | win | 1 | 0.5123 | 2.8 | 1.43 | 200 | scan=2.7 drift=+3.7% | 13:30:24 |
| S00 | 053R | win | 1 | 0.4111 | 5.0 | 2.06 | 300 | scan=4.1 drift=+22.0% | 12:32:21 |
| S01_NAKAANA1 | 172R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 11:11:21 |
| S00 | 021R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.3 drift=+2.3% | 10:44:20 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 4.3 | 2.22 | 200 | scan=4.5 drift=-4.4% | 17:06:22 |
| S00 | 073R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=10.5 drift=-28.6% | 16:24:21 |
| S00 | 122R | win | 1 | 0.2173 | 9.3 | 2.02 | 300 | scan=7.5 drift=+24.0% | 15:41:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 39 | -3.3% | -61.4% | +43.3% | 12 | 7 | 24 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 450.6s |
| **Latency** (scan→final max) | 623.2s |
| **Traffic** (notifications 24h) | 46 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 356 | 0.4721 | 0.3062 | +0.1660 | 🟡+35% | 0.2400 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 146 | 0.4270 | 0.2877 | 0.2199 | 🔴-0.07 | 0.822 |
| S01_NAKAANA1 | win | 132 | 0.4850 | 0.2955 | 0.2475 | 🔴-0.19 | 0.78 |
| S02_TETSUBAN | win | 78 | 0.5349 | 0.3590 | 0.2651 | 🔴-0.15 | 0.585 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1835 | 0.2000 | ✅-0.0165 |
| 0.20-0.30 | 9 | 0.2241 | 0.1111 | 🔴+0.1130 |
| 0.30-0.50 | 125 | 0.4180 | 0.2720 | 🔴+0.1460 |
| 0.50+ | 207 | 0.5415 | 0.3478 | 🔴+0.1937 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 44 | 0.711 |
| win | <5.0 | ✅learned | 80 | 0.754 |
| win | <10.0 | ✅learned | 54 | 0.496 |
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
_auto-generated by claude_snapshot.py at 2026-06-19T09:10:01.534657+09:00_