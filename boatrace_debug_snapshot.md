# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-11T11:20:01.624534+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×33 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×100 (24h)
- 🔴 PSI_DRIFT_DETECTED×33 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×18  [2026-05-11T11:02:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-05-11T11:02:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-05-11T10:57:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift ≥+30%: n=24 hit%=20.8% ROI=0.62 (コスト 6,400/回収 3,960)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-11T06:00:07]
- key: `ROI_STAT|S00: n=151 hit%=25.8% hit_CI[Bonf]=[17.0,37.2]% ROI=0.87 ROI_boot95=[0.59,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-11T06:00:07]
- key: `INSUFFICIENT_SAMPLE|S00: n=151<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-11T06:00:07]
- key: `ORPHAN_SCAN|192 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=18.2% ROI=0.47 (コスト 9,700/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=22 hit%=31.8% ROI=1.66 (コスト 5,600/回収 9,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-11T06:00:07]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=28 hit%=28.6% ROI=1.27 (コスト 7,500/回収 9,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|bt=win: n=164 pred=0.4387 actual=0.2622 error=+0.1765 (+40%) brier=0.2304 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|S00(win): n=151 pred=0.4335 hit=0.2583 cal_err=+0.1752 brier=0.2291 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=15 pred=0.3298 actual=0.1333 gap=+0.1964`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=64 pred=0.4473 actual=0.2656 gap=+0.1817`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-11T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=65 pred=0.5347 actual=0.2923 gap=+0.2424`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-11T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-11T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.45MB / last modified 2026-05-11T11:19:29.217353+09:00

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
rsed
2026-05-11 11:18:56,428 [INFO] scraper: fetch_race 14/7: boats=6 odds=189/191
2026-05-11 11:18:56,439 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 11:18:56,439 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-11 11:18:56,447 [INFO] run_cycle: fetched 14/7 [scan]: 154 combos
2026-05-11 11:18:56,638 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-11 11:19:05,234 [INFO] run_cycle: === run_cycle 11:19:05 ===
2026-05-11 11:19:05,235 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-11 11:19:05,235 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-11 11:19:05,300 [INFO] predictor: Models loaded OK
2026-05-11 11:19:17,885 [INFO] scraper: odds3t: 120/120 parsed
2026-05-11 11:19:19,251 [INFO] scraper: odds3f: 20/20 parsed
2026-05-11 11:19:20,354 [INFO] scraper: odds2t: 30/30 parsed
2026-05-11 11:19:20,355 [INFO] scraper: odds2f: 15/15 parsed
2026-05-11 11:19:21,522 [INFO] scraper: odds_win: 6/6 parsed
2026-05-11 11:19:21,522 [INFO] scraper: fetch_race 03/2: boats=6 odds=191/191
2026-05-11 11:19:21,534 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 11:19:21,534 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-11 11:19:21,541 [INFO] run_cycle: fetched 03/2 [final]: 156 combos
2026-05-11 11:19:25,367 [INFO] scraper: odds3t: 120/120 parsed
2026-05-11 11:19:26,695 [INFO] scraper: odds3f: 19/20 parsed
2026-05-11 11:19:27,811 [INFO] scraper: odds2t: 30/30 parsed
2026-05-11 11:19:27,813 [INFO] scraper: odds2f: 15/15 parsed
2026-05-11 11:19:28,960 [INFO] scraper: odds_win: 3/6 parsed
2026-05-11 11:19:28,960 [INFO] scraper: fetch_race 11/3: boats=6 odds=187/191
2026-05-11 11:19:28,969 [INFO] predictor: CALIBRATION_MODE=on
2026-05-11 11:19:28,969 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-11 11:19:28,976 [INFO] run_cycle: fetched 11/3 [scan]: 153 combos
2026-05-11 11:19:29,084 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 18, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 128
  FINAL_MISSING: 100
  PSI_DRIFT_DETECTED: 33
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 17 | 14,700 | 14,460 | -240 | 0.984 |
| S01_NAKAANA1 | 8 | 3 | 1,600 | 1,560 | -40 | 0.975 |
| S02_TETSUBAN | 7 | 2 | 1,400 | 1,040 | -360 | 0.743 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[11:17:21] FINAL_MISSING: {"deadline": "2026-05-11T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051123061047", "sid": "S00"}
[11:04:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 103, "n_recent": 64, "psi": 0.37}
[11:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:58:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 103, "n_recent": 63, "psi": 0.375}
[10:57:46] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.231, "baseline_mean": 0.564, "baseline_stdev": 0.177, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 3, "z_score": -1.31}
[10:44:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 103, "n_recent": 62, "psi": 0.38}
[10:30:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 102, "n_recent": 63, "psi": 0.376}
[10:01:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:30:10] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 102, "n_recent": 63, "psi": 0.376}
[09:00:50] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 122件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 22件 締切済
- 通知発射: scan=4 nid / final=4 nid / result=1 nid
- predictions: 3 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 092R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.2 drift=+9.1% | 11:04:20 |
| S00 | 112R | win | 1 | 0.4995 | 22.5 | 11.24 | 300 | scan=- drift=- | 10:58:21 |
| S01_NAKAANA1 | 232R | win | 1 | 0.5891 | 3.4 | 2.00 | 200 | scan=- drift=- | 08:55:21 |
| S02_TETSUBAN | 2010R | win | 1 | 0.5719 | 2.4 | 1.37 | 200 | scan=2.7 drift=-11.1% | 19:28:21 |
| S02_TETSUBAN | 0512R | win | 1 | 0.4111 | 2.1 | 0.86 | 200 | scan=2.0 drift=+5.0% | 17:17:32 |
| S02_TETSUBAN | 059R | win | 1 | 0.5990 | 2.1 | 1.26 | 200 | scan=- drift=- | 15:42:21 |
| S02_TETSUBAN | 1610R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 15:36:20 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5123 | 2.6 | 1.33 | 200 | scan=- drift=- | 15:21:32 |
| S00 | 0910R | win | 1 | 0.5123 | 4.9 | 2.51 | 300 | scan=7.8 drift=-37.2% | 15:20:35 |
| S01_NAKAANA1 | 226R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 14:56:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 44 | -10.7% | -75.4% | +124.4% | 23 | 15 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 519.0s |
| **Latency** (scan→final max) | 625.1s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 165 | 0.4396 | 0.2667 | +0.1729 | 🟡+39% | 0.2300 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 151 | 0.4335 | 0.2583 | 0.2291 | 🔴-0.20 | 0.866 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 6 | 0.1899 | 0.1667 | ✅+0.0232 |
| 0.20-0.30 | 9 | 0.2241 | 0.3333 | 🔴-0.1093 |
| 0.30-0.50 | 79 | 0.4250 | 0.2405 | 🔴+0.1845 |
| 0.50+ | 66 | 0.5356 | 0.3030 | 🔴+0.2325 |

## Settlement Ratio データ品質

- 学習済み: 2バンド / fallback: 15バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 2 | 0.4 |
| win | <5.0 | ✅learned | 10 | 1.0 |
| win | <10.0 | ✅learned | 24 | 0.548 |
| win | <20.0 | ⚠️fallback | 8 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-11T11:20:01.624534+09:00_