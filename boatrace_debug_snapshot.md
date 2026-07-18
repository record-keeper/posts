# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-18T12:10:01.936787+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-07-18T12:02:19]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×4  [2026-07-18T11:57:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-07-18T09:00:22]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=72<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-07-18T06:00:07]
- key: `ORPHAN_SCAN|166 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-18T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=46 hit%=32.6% ROI=0.76 (コスト 11,300/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-18T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3262 actual=0.0938 gap=+0.2325`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-18T06:00:07]
- key: `ROI_STAT|S00: n=177 hit%=28.2% hit_CI[Bonf]=[19.6,38.8]% ROI=0.73 ROI_boot95=[0.54,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-18T06:00:07]
- key: `ROI_STAT|S01_NAKAANA1: n=160 hit%=30.0% hit_CI[Bonf]=[20.7,41.2]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-18T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=160<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-18T06:00:07]
- key: `ROI_STAT|S02_TETSUBAN: n=72 hit%=44.4% hit_CI[Bonf]=[29.0,61.0]% ROI=0.90 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=31.2% ROI=0.80 (コスト 9,300/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-18T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=33.3% ROI=0.85 (コスト 19,900/回収 16,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-18T06:00:07]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=33 hit%=30.3% ROI=0.57 (コスト 8,000/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-18T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=32 hit%=18.8% ROI=0.40 (コスト 8,900/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-18T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=409 pred=0.4685 actual=0.3178 error=+0.1506 (+32%) brier=0.2378 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-18T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=177 pred=0.4272 hit=0.2825 cal_err=+0.1447 brier=0.2277 BSS=-0.12 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-18T06:00:07]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=160 pred=0.4803 hit=0.3000 cal_err=+0.1803 brier=0.2379 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.91MB / last modified 2026-07-18T12:09:40.527838+09:00

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
: combos: {'win': 5, '2t': 30, '3t': 120}
2026-07-18 12:09:19,433 [INFO] run_cycle: fetched 17/4 [final]: 155 combos
2026-07-18 12:09:23,012 [INFO] scraper: odds3t: 120/120 parsed
2026-07-18 12:09:24,162 [INFO] scraper: odds3f: 20/20 parsed
2026-07-18 12:09:25,448 [INFO] scraper: odds2t: 30/30 parsed
2026-07-18 12:09:25,449 [INFO] scraper: odds2f: 15/15 parsed
2026-07-18 12:09:26,534 [INFO] scraper: odds_win: 6/6 parsed
2026-07-18 12:09:26,535 [INFO] scraper: fetch_race 21/9: boats=6 odds=191/191
2026-07-18 12:09:26,537 [INFO] predictor: CALIBRATION_MODE=on
2026-07-18 12:09:26,537 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-18 12:09:26,542 [INFO] run_cycle: fetched 21/9 [scan]: 156 combos
2026-07-18 12:09:30,139 [INFO] scraper: odds3t: 120/120 parsed
2026-07-18 12:09:31,222 [INFO] scraper: odds3f: 20/20 parsed
2026-07-18 12:09:32,347 [INFO] scraper: odds2t: 29/30 parsed
2026-07-18 12:09:32,349 [INFO] scraper: odds2f: 14/15 parsed
2026-07-18 12:09:33,417 [INFO] scraper: odds_win: 3/6 parsed
2026-07-18 12:09:33,418 [INFO] scraper: fetch_race 11/4: boats=6 odds=186/191
2026-07-18 12:09:33,420 [INFO] predictor: CALIBRATION_MODE=on
2026-07-18 12:09:33,420 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-07-18 12:09:33,424 [INFO] run_cycle: fetched 11/4 [scan]: 152 combos
2026-07-18 12:09:36,880 [INFO] scraper: odds3t: 120/120 parsed
2026-07-18 12:09:37,985 [INFO] scraper: odds3f: 20/20 parsed
2026-07-18 12:09:39,074 [INFO] scraper: odds2t: 30/30 parsed
2026-07-18 12:09:39,075 [INFO] scraper: odds2f: 15/15 parsed
2026-07-18 12:09:40,178 [INFO] scraper: odds_win: 4/6 parsed
2026-07-18 12:09:40,178 [INFO] scraper: fetch_race 10/9: boats=6 odds=189/191
2026-07-18 12:09:40,180 [INFO] predictor: CALIBRATION_MODE=on
2026-07-18 12:09:40,181 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-07-18 12:09:40,184 [INFO] run_cycle: fetched 10/9 [scan]: 154 combos
2026-07-18 12:09:40,289 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 34, 'result': 18, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 134
  FINAL_MISSING: 48
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  ANOMALY_BET_VOLUME_DROP: 1
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 13 | 13,800 | 12,090 | -1,710 | 0.876 |
| S01_NAKAANA1 | 38 | 11 | 7,600 | 5,980 | -1,620 | 0.787 |
| S02_TETSUBAN | 15 | 6 | 3,000 | 2,560 | -440 | 0.853 |

## 直近アラート (24h・新しい順)
```
[12:02:18] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:50:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.214, "baseline_mean": 0.786, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 8, "z_score": 2.11}
[11:13:37] CRITICAL_ODDS_COLLAPSE: {"combo": "1", "drift_pct": -44.6, "final": 4.6, "kind": "CRITICAL_ODDS_COLLAPSE", "race": "022R", "scan": 8.3, "sid": "S00"}
[11:13:37] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.214, "baseline_mean": 0.786, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 4, "z_score": 2.11}
[11:01:44] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:56:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.214, "baseline_mean": 0.786, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 1.0, "today_scan_count": 3, "z_score": 2.11}
[10:01:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:00:22] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 1.4, "baseline_n_days": 5, "baseline_stdev": 0.5, "hour": 9, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.56}
[08:00:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 133件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 47件 締切済
- 通知発射: scan=10 nid / final=10 nid / result=4 nid
- predictions: 6 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 161R | win | 1 | 0.5719 | 4.8 | 2.75 | 200 | scan=4.8 drift=+0.0% | 11:48:29 |
| S00 | 113R | win | 1 | 0.5123 | 6.7 | 3.43 | 300 | scan=5.6 drift=+19.6% | 11:40:20 |
| S00 | 083R | win | 1 | 0.4989 | 32.2 | 16.07 | 300 | scan=- drift=- | 11:35:29 |
| S00 | 107R | win | 1 | 0.5123 | 4.8 | 2.46 | 300 | scan=- drift=- | 11:18:18 |
| S00 | 022R | win | 1 | 0.4989 | 4.6 | 2.30 | 300 | scan=8.3 drift=-44.6% | 11:13:36 |
| S02_TETSUBAN | 091R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.6 drift=-7.7% | 10:30:32 |
| S00 | 0110R | win | 1 | 0.4111 | 14.1 | 5.80 | 300 | scan=- drift=- | 19:36:19 |
| S01_NAKAANA1 | 128R | win | 1 | 0.5476 | 4.1 | 2.25 | 200 | scan=- drift=- | 18:22:18 |
| S02_TETSUBAN | 071R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=2.2 drift=-9.1% | 15:17:19 |
| S01_NAKAANA1 | 118R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.0 drift=+10.0% | 14:19:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 49 | +3.4% | -64.6% | +156.7% | 16 | 6 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 480.3s |
| **Latency** (scan→final max) | 616.2s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 411 | 0.4686 | 0.3139 | +0.1547 | 🟡+33% | 0.2374 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4285 | 0.2737 | 0.2275 | 🔴-0.14 | 0.7 |
| S01_NAKAANA1 | win | 159 | 0.4801 | 0.3019 | 0.2377 | 🔴-0.13 | 0.782 |
| S02_TETSUBAN | win | 73 | 0.5417 | 0.4384 | 0.2610 | 🔴-0.06 | 0.89 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2276 | 0.2000 | ✅+0.0276 |
| 0.30-0.50 | 159 | 0.4193 | 0.2704 | 🔴+0.1488 |
| 0.50+ | 222 | 0.5425 | 0.3514 | 🔴+0.1911 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 75 | 0.806 |
| win | <5.0 | ✅learned | 143 | 0.71 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 24 | 0.222 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-18T12:10:01.936787+09:00_