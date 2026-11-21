# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-21T09:50:01.428659+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×29 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×29 (24h)
- 🟡 FINAL_MISSING×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×27  [2026-11-21T09:07:31]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-11-21T09:07:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.0000 gap=+0.1918`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S00: n=86 hit%=22.1% hit_CI[Bonf]=[12.0,37.1]% ROI=0.60 ROI_boot95=[0.35,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S00: n=86<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S01_NAKAANA1: n=105 hit%=26.7% hit_CI[Bonf]=[16.3,40.5]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-21T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=105<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-21T06:00:45]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=40.0% hit_CI[Bonf]=[21.3,62.1]% ROI=0.97 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-21T06:00:45]
- key: `ORPHAN_SCAN|245 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-21T06:00:45]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=20.0% ROI=0.83 (コスト 5,400/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-21T06:00:45]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=44 hit%=38.6% ROI=0.84 (コスト 10,200/回収 8,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-21T06:00:45]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=21 hit%=19.0% ROI=0.73 (コスト 5,000/回収 3,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|bt=win: n=231 pred=0.4724 actual=0.2727 error=+0.1996 (+42%) brier=0.2305 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|S00(win): n=86 pred=0.4273 hit=0.2209 cal_err=+0.2064 brier=0.2093 BSS=-0.22 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=105 pred=0.4797 hit=0.2667 cal_err=+0.2130 brier=0.2338 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=40 pred=0.5500 hit=0.4000 cal_err=+0.1500 brier=0.2674 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=25 pred=0.3194 actual=0.1200 gap=+0.1994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=69 pred=0.4426 actual=0.2899 gap=+0.1527`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-21T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.50+: n=126 pred=0.5447 actual=0.3175 gap=+0.2272`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.36MB / last modified 2026-11-21T09:48:03.900974+09:00

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
A': 200, 'B': 100} default=100
2026-11-21 09:46:04,352 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-21 09:46:04,400 [INFO] predictor: Models loaded OK
2026-11-21 09:46:04,524 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-21 09:47:04,639 [INFO] run_cycle: === run_cycle 09:47:04 ===
2026-11-21 09:47:04,639 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-21 09:47:04,640 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-21 09:47:04,697 [INFO] predictor: Models loaded OK
2026-11-21 09:47:34,155 [INFO] scraper: odds3t: 120/120 parsed
2026-11-21 09:47:44,291 [INFO] scraper: odds3f: 20/20 parsed
2026-11-21 09:47:53,385 [INFO] scraper: odds2t: 30/30 parsed
2026-11-21 09:47:53,386 [INFO] scraper: odds2f: 15/15 parsed
2026-11-21 09:48:02,470 [INFO] scraper: odds_win: 3/6 parsed
2026-11-21 09:48:02,471 [INFO] scraper: fetch_race 14/4: boats=6 odds=188/191
2026-11-21 09:48:02,474 [INFO] predictor: CALIBRATION_MODE=on
2026-11-21 09:48:02,474 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-11-21 09:48:02,479 [INFO] run_cycle: fetched 14/4 [scan]: 153 combos
2026-11-21 09:48:02,617 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-21 09:49:04,204 [INFO] run_cycle: === run_cycle 09:49:04 ===
2026-11-21 09:49:04,204 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-21 09:49:04,204 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-21 09:49:04,252 [INFO] predictor: Models loaded OK
2026-11-21 09:49:15,316 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=21&hd=20261121: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-21 09:49:44,911 [INFO] scraper: odds3t: 120/120 parsed
2026-11-21 09:49:54,046 [INFO] scraper: odds3f: 20/20 parsed

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
    "c": 11
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 11
  }
]
```

## Phase別通知記録 (24h)
{'final': 4, 'result': 2, 'scan': 5}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 266
  PSI_DRIFT_DETECTED: 29
  FINAL_MISSING: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 7 | 1 | 2,100 | 480 | -1,620 | 0.229 |
| S01_NAKAANA1 | 14 | 3 | 2,800 | 1,840 | -960 | 0.657 |
| S02_TETSUBAN | 6 | 4 | 1,200 | 1,600 | +400 | 1.333 |

## 直近アラート (24h・新しい順)
```
[09:07:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:59:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 203, "n_recent": 27, "psi": 0.493}
[08:03:32] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:03:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 204, "n_recent": 27, "psi": 0.491}
[06:00:10] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:10] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 204, "n_recent": 27, "psi": 0.491}
[23:50:05] FINAL_MISSING: {"deadline": "2026-11-20T12:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112004041212", "sid": "S01_NAKAANA1"}
[23:34:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": -0.2, "baseline_mean": 0.4, "baseline_stdev": 0.088, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 5, "z_score": 2.27}
[23:23:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:04] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 204, "n_recent": 27, "psi": 0.491}
```

## 本日残レース: 159件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 9件 締切済
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
| S01_NAKAANA1 | 1410R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=4.8 drift=-25.0% | 12:53:02 |
| S01_NAKAANA1 | 218R | win | 1 | 0.5123 | 3.1 | 1.59 | 200 | scan=- drift=- | 12:08:26 |
| S01_NAKAANA1 | 0410R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.1 drift=+6.5% | 15:03:39 |
| S01_NAKAANA1 | 047R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=3.5 drift=-14.3% | 13:35:14 |
| S01_NAKAANA1 | 089R | win | 1 | 0.5220 | 3.3 | 1.72 | 200 | scan=3.1 drift=+6.5% | 14:22:25 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 200 | scan=- drift=- | 13:57:35 |
| S00 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 300 | scan=5.4 drift=-9.3% | 13:57:34 |
| S02_TETSUBAN | 118R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.9 drift=-10.3% | 13:55:17 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5874 | 3.1 | 1.82 | 200 | scan=- drift=- | 13:17:05 |
| S00 | 131R | win | 1 | 0.5334 | 17.6 | 9.39 | 300 | scan=17.6 drift=+0.0% | 10:42:37 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 13 | -0.0% | -26.8% | +55.6% | 6 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 473.5s |
| **Latency** (scan→final max) | 577.1s |
| **Traffic** (notifications 24h) | 11 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 230 | 0.4726 | 0.2739 | +0.1987 | 🟡+42% | 0.2307 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 86 | 0.4273 | 0.2209 | 0.2093 | 🔴-0.22 | 0.602 |
| S01_NAKAANA1 | win | 104 | 0.4804 | 0.2692 | 0.2344 | 🔴-0.19 | 0.7 |
| S02_TETSUBAN | win | 40 | 0.5500 | 0.4000 | 0.2674 | 🔴-0.11 | 0.973 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1918 | 0.0000 | 🔴+0.1918 |
| 0.30-0.50 | 93 | 0.4098 | 0.2473 | 🔴+0.1625 |
| 0.50+ | 126 | 0.5447 | 0.3175 | 🔴+0.2272 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 207 | 0.807 |
| win | <5.0 | ✅learned | 374 | 0.741 |
| win | <10.0 | ✅learned | 159 | 0.448 |
| win | <20.0 | ✅learned | 48 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-11-21T09:50:01.428659+09:00_