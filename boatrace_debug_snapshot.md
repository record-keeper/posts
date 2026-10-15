# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-15T11:10:01.508445+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-10-15T11:03:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-10-15T11:03:42]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×8  [2026-10-15T11:02:15]
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
- DB: 15.84MB / last modified 2026-10-15T11:09:10.910664+09:00

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
1120 sid=S01_NAKAANA1 phase=scan rank=A
2026-10-15 11:07:35,783 [INFO] notifier: Discord notify OK (status=204)
2026-10-15 11:07:36,152 [INFO] notifier: Discord notify OK (status=204)
2026-10-15 11:07:36,174 [INFO] run_cycle: SCAN S01_NAKAANA1 鳴門7R A
2026-10-15 11:07:36,329 [INFO] run_cycle: run_cycle done: 2 notifications
2026-10-15 11:08:05,910 [INFO] run_cycle: === run_cycle 11:08:05 ===
2026-10-15 11:08:05,911 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 11:08:05,911 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 11:08:05,946 [INFO] predictor: Models loaded OK
2026-10-15 11:08:17,016 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=11&hd=20261015: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-15 11:08:28,415 [INFO] scraper: odds3t: 120/120 parsed
2026-10-15 11:08:29,516 [INFO] scraper: odds3f: 20/20 parsed
2026-10-15 11:08:30,631 [INFO] scraper: odds2t: 30/30 parsed
2026-10-15 11:08:30,632 [INFO] scraper: odds2f: 15/15 parsed
2026-10-15 11:08:31,708 [INFO] scraper: odds_win: 2/6 parsed
2026-10-15 11:08:31,709 [INFO] scraper: fetch_race 11/3: boats=6 odds=187/191
2026-10-15 11:08:31,720 [INFO] predictor: CALIBRATION_MODE=on
2026-10-15 11:08:31,720 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-10-15 11:08:31,729 [INFO] run_cycle: fetched 11/3 [scan]: 152 combos
2026-10-15 11:08:32,297 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-15 11:09:06,257 [INFO] run_cycle: === run_cycle 11:09:06 ===
2026-10-15 11:09:06,257 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-15 11:09:06,258 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-15 11:09:06,304 [INFO] predictor: Models loaded OK
2026-10-15 11:09:06,684 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 70
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 70
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 14, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 62
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 13 | 13,200 | 11,730 | -1,470 | 0.889 |
| S01_NAKAANA1 | 38 | 15 | 7,600 | 6,520 | -1,080 | 0.858 |
| S02_TETSUBAN | 21 | 11 | 4,200 | 4,100 | -100 | 0.976 |

## 直近アラート (24h・新しい順)
```
[11:08:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1039}
[11:07:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1038}
[11:07:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.374, "baseline_mean": 0.874, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 4, "z_score": -4.42}
[11:06:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1028}
[11:05:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1020}
[11:03:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1001}
[11:03:42] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.208, "baseline_mean": 0.874, "baseline_stdev": 0.085, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 3, "z_score": -2.45}
[11:02:13] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:18:40] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 39.4, "final": 4.6, "kind": "LARGE_ODDS_DRIFT", "race": "145R", "scan": 3.3, "sid": "S01_NAKAANA1"}
[10:02:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 129件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 27件 締切済
- 通知発射: scan=4 nid / final=3 nid / result=1 nid
- predictions: 2 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 216R | win | 1 | 0.5476 | 3.6 | 1.97 | 200 | scan=- drift=- | 10:57:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.3599 | 4.6 | 1.66 | 200 | scan=3.3 drift=+39.4% | 10:18:20 |
| S00 | 205R | win | 1 | 0.5076 | 5.0 | 2.54 | 300 | scan=6.6 drift=-24.2% | 17:16:20 |
| S01_NAKAANA1 | 154R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=3.7 drift=-13.5% | 16:39:29 |
| S00 | 202R | win | 1 | 0.5123 | 6.2 | 3.18 | 300 | scan=4.8 drift=+29.2% | 15:51:19 |
| S02_TETSUBAN | 201R | win | 1 | 0.5674 | 2.7 | 1.53 | 200 | scan=2.4 drift=+12.5% | 15:22:19 |
| S02_TETSUBAN | 1111R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 15:12:21 |
| S02_TETSUBAN | 1110R | win | 1 | 0.5096 | 2.0 | 1.02 | 200 | scan=- drift=- | 14:45:21 |
| S00 | 119R | win | 1 | 0.3177 | 8.6 | 2.73 | 300 | scan=9.7 drift=-11.3% | 14:15:44 |
| S02_TETSUBAN | 118R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=2.4 drift=-4.2% | 13:42:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 65 | +15.2% | -60.0% | +326.7% | 19 | 7 | 49 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.5s |
| **Latency** (scan→final max) | 617.4s |
| **Traffic** (notifications 24h) | 70 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 429 | 0.4815 | 0.3427 | +0.1389 | 🟡+29% | 0.2493 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 179 | 0.4497 | 0.2570 | 0.2492 | 🔴-0.31 | 0.701 |
| S01_NAKAANA1 | win | 163 | 0.4910 | 0.3497 | 0.2432 | 🔴-0.07 | 1.031 |
| S02_TETSUBAN | win | 87 | 0.5293 | 0.5057 | 0.2608 | 🔴-0.04 | 0.914 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 157 | 0.4173 | 0.3057 | 🔴+0.1115 |
| 0.50+ | 255 | 0.5436 | 0.3686 | 🔴+0.1750 |

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
_auto-generated by claude_snapshot.py at 2026-10-15T11:10:01.508445+09:00_