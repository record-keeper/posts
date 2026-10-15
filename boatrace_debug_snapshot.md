# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-15T11:50:01.695532+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×40  [2026-10-15T11:03:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×21  [2026-10-15T11:03:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×48  [2026-10-15T11:02:15]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-15T06:00:14]
- key: `ORPHAN_SCAN|161 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-15T06:00:14]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=87<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=40.6% ROI=1.12 (コスト 9,300/回収 10,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|decile 0.50+: n=256 pred=0.5435 actual=0.3711 gap=+0.1724`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S00: n=181 hit%=26.5% hit_CI[Bonf]=[18.2,36.9]% ROI=0.72 ROI_boot95=[0.52,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=35.2% hit_CI[Bonf]=[25.3,46.5]% ROI=1.04 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-15T06:00:14]
- key: `ROI_STAT|S02_TETSUBAN: n=87 hit%=50.6% hit_CI[Bonf]=[35.7,65.3]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=32.0% ROI=0.73 (コスト 11,900/回収 8,720)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=35.6% ROI=0.97 (コスト 20,100/回収 19,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=55 hit%=36.4% ROI=0.90 (コスト 13,000/回収 11,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-15T06:00:14]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=23.9% ROI=0.79 (コスト 11,900/回収 9,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|bt=win: n=430 pred=0.4817 actual=0.3465 error=+0.1352 (+28%) brier=0.2497 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|S00(win): n=181 pred=0.4498 hit=0.2652 cal_err=+0.1846 brier=0.2496 BSS=-0.28 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=162 pred=0.4918 hit=0.3519 cal_err=+0.1400 brier=0.2439 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-15T06:00:14]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=87 pred=0.5293 hit=0.5057 cal_err=+0.0235 brier=0.2608 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.85MB / last modified 2026-10-15T11:49:22.947940+09:00

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
2026-10-15 11:47:51,167 [INFO] scraper: odds2t: 30/30 parsed
2026-10-15 11:47:51,169 [INFO] scraper: odds2f: 13/15 parsed
2026-10-15 11:47:52,298 [INFO] scraper: odds_win: 4/6 parsed
2026-10-15 11:47:52,298 [INFO] scraper: fetch_race 21/8: boats=6 odds=187/191
2026-10-15 11:47:52,301 [INFO] predictor: CALIBRATION_MODE=on
2026-10-15 11:47:52,301 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-15 11:47:52,305 [INFO] run_cycle: fetched 21/8 [scan]: 154 combos
2026-10-15 11:47:52,496 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 11:48:05,124 [INFO] run_cycle: === run_cycle 11:48:05 ===
2026-10-15 11:48:05,124 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 11:48:05,124 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 11:48:05,222 [INFO] predictor: Models loaded OK
2026-10-15 11:48:05,719 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 11:49:05,796 [INFO] run_cycle: === run_cycle 11:49:05 ===
2026-10-15 11:49:05,797 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 11:49:05,797 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 11:49:05,835 [INFO] predictor: Models loaded OK
2026-10-15 11:49:17,726 [INFO] scraper: odds3t: 120/120 parsed
2026-10-15 11:49:18,798 [INFO] scraper: odds3f: 20/20 parsed
2026-10-15 11:49:19,880 [INFO] scraper: odds2t: 30/30 parsed
2026-10-15 11:49:19,881 [INFO] scraper: odds2f: 14/15 parsed
2026-10-15 11:49:21,027 [INFO] scraper: odds_win: 3/6 parsed
2026-10-15 11:49:21,027 [INFO] scraper: fetch_race 13/4: boats=6 odds=187/191
2026-10-15 11:49:21,030 [INFO] predictor: CALIBRATION_MODE=on
2026-10-15 11:49:21,030 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-10-15 11:49:21,034 [INFO] run_cycle: fetched 13/4 [scan]: 153 combos
2026-10-15 11:49:21,190 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 74
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 74
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 15, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 93
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 13 | 13,800 | 11,730 | -2,070 | 0.85 |
| S01_NAKAANA1 | 38 | 15 | 7,600 | 6,520 | -1,080 | 0.858 |
| S02_TETSUBAN | 21 | 11 | 4,200 | 4,100 | -100 | 0.976 |

## 直近アラート (24h・新しい順)
```
[11:46:31] FINAL_MISSING: {"deadline": "2026-10-15T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101502021116", "sid": "S00"}
[11:42:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1197}
[11:41:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1176}
[11:40:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1160}
[11:39:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1174}
[11:38:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1182}
[11:37:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1200}
[11:36:34] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1205}
[11:35:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1187}
[11:35:54] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.274, "baseline_mean": 0.874, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": -3.24}
```

## 本日残レース: 117件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 39件 締切済
- 通知発射: scan=5 nid / final=5 nid / result=2 nid
- predictions: 5 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 023R | win | 1 | 0.2290 | 6.1 | 1.40 | 300 | scan=5.7 drift=+7.0% | 11:42:21 |
| S01_NAKAANA1 | 147R | win | 1 | 0.4989 | 4.5 | 2.25 | 200 | scan=4.1 drift=+9.8% | 11:17:25 |
| S00 | 147R | win | 1 | 0.4989 | 4.5 | 2.25 | 300 | scan=4.1 drift=+9.8% | 11:17:21 |
| S01_NAKAANA1 | 216R | win | 1 | 0.5476 | 3.6 | 1.97 | 200 | scan=- drift=- | 10:57:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.3599 | 4.6 | 1.66 | 200 | scan=3.3 drift=+39.4% | 10:18:20 |
| S00 | 205R | win | 1 | 0.5076 | 5.0 | 2.54 | 300 | scan=6.6 drift=-24.2% | 17:16:20 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=3.7 drift=-13.5% | 16:39:29 |
| S00 | 202R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=4.8 drift=+29.2% | 15:51:19 |
| S02_TETSUBAN | 201R | win | 1 | 0.5674 | 2.7 | 1.53 | 200 | scan=2.4 drift=+12.5% | 15:22:19 |
| S02_TETSUBAN | 1111R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 15:12:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +15.5% | -60.0% | +326.7% | 18 | 7 | 48 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 500.0s |
| **Latency** (scan→final max) | 617.4s |
| **Traffic** (notifications 24h) | 74 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 429 | 0.4816 | 0.3427 | +0.1389 | 🟡+29% | 0.2493 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4493 | 0.2584 | 0.2491 | 🔴-0.30 | 0.705 |
| S01_NAKAANA1 | win | 164 | 0.4913 | 0.3476 | 0.2435 | 🔴-0.07 | 1.025 |
| S02_TETSUBAN | win | 87 | 0.5293 | 0.5057 | 0.2608 | 🔴-0.04 | 0.914 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 157 | 0.4173 | 0.3057 | 🔴+0.1115 |
| 0.50+ | 255 | 0.5437 | 0.3686 | 🔴+0.1751 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 182 | 0.775 |
| win | <5.0 | ✅learned | 322 | 0.752 |
| win | <10.0 | ✅learned | 140 | 0.46 |
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
_auto-generated by claude_snapshot.py at 2026-10-15T11:50:01.695532+09:00_