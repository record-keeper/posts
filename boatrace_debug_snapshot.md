# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-20T13:50:01.805880+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×57 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-10-20T13:02:18]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×35  [2026-10-20T11:52:25]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-10-20T11:19:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-10-20T10:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-20T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-20T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-20T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=34.0% ROI=0.77 (コスト 11,700/回収 8,980)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-20T06:00:09]
- key: `ROI_STAT|S00: n=177 hit%=27.7% hit_CI[Bonf]=[19.1,38.2]% ROI=0.75 ROI_boot95=[0.54,0.97]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-20T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=178 hit%=36.5% hit_CI[Bonf]=[26.9,47.3]% ROI=1.01 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-20T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-20T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=52.4% hit_CI[Bonf]=[37.2,67.2]% ROI=0.94 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-20T06:00:09]
- key: `ORPHAN_SCAN|151 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-20T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=43.3% ROI=1.12 (コスト 8,600/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-20T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=40.9% ROI=1.16 (コスト 19,800/回収 23,010)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-20T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=60 hit%=35.0% ROI=0.90 (コスト 14,300/回収 12,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-20T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=51 hit%=25.5% ROI=0.81 (コスト 13,200/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=439 pred=0.4793 actual=0.3599 error=+0.1194 (+25%) brier=0.2445 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=177 pred=0.4399 hit=0.2768 cal_err=+0.1630 brier=0.2371 BSS=-0.18 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.25MB / last modified 2026-10-20T13:49:40.277163+09:00

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
r: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-20 13:49:18,715 [INFO] run_cycle: fetched 16/7 [scan]: 156 combos
2026-10-20 13:49:22,504 [INFO] scraper: odds3t: 120/120 parsed
2026-10-20 13:49:23,692 [INFO] scraper: odds3f: 20/20 parsed
2026-10-20 13:49:24,774 [INFO] scraper: odds2t: 30/30 parsed
2026-10-20 13:49:24,775 [INFO] scraper: odds2f: 15/15 parsed
2026-10-20 13:49:25,883 [INFO] scraper: odds_win: 2/6 parsed
2026-10-20 13:49:25,883 [INFO] scraper: fetch_race 03/7: boats=6 odds=187/191
2026-10-20 13:49:25,885 [INFO] predictor: CALIBRATION_MODE=on
2026-10-20 13:49:25,885 [INFO] predictor: combos: {'win': 2, '2t': 30, '3t': 120}
2026-10-20 13:49:25,889 [INFO] run_cycle: fetched 03/7 [scan]: 152 combos
2026-10-20 13:49:29,409 [INFO] scraper: odds3t: 120/120 parsed
2026-10-20 13:49:30,487 [INFO] scraper: odds3f: 20/20 parsed
2026-10-20 13:49:31,568 [INFO] scraper: odds2t: 23/30 parsed
2026-10-20 13:49:31,569 [INFO] scraper: odds2f: 13/15 parsed
2026-10-20 13:49:32,641 [INFO] scraper: odds_win: 4/6 parsed
2026-10-20 13:49:32,642 [INFO] scraper: fetch_race 17/9: boats=6 odds=180/191
2026-10-20 13:49:33,017 [INFO] predictor: CALIBRATION_MODE=on
2026-10-20 13:49:33,017 [INFO] predictor: combos: {'win': 4, '2t': 23, '3t': 120}
2026-10-20 13:49:33,021 [INFO] run_cycle: fetched 17/9 [scan]: 147 combos
2026-10-20 13:49:36,503 [INFO] scraper: odds3t: 120/120 parsed
2026-10-20 13:49:37,635 [INFO] scraper: odds3f: 20/20 parsed
2026-10-20 13:49:38,738 [INFO] scraper: odds2t: 30/30 parsed
2026-10-20 13:49:38,740 [INFO] scraper: odds2f: 15/15 parsed
2026-10-20 13:49:39,876 [INFO] scraper: odds_win: 4/6 parsed
2026-10-20 13:49:39,876 [INFO] scraper: fetch_race 08/8: boats=6 odds=189/191
2026-10-20 13:49:39,879 [INFO] predictor: CALIBRATION_MODE=on
2026-10-20 13:49:39,879 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-20 13:49:39,883 [INFO] run_cycle: fetched 08/8 [scan]: 154 combos
2026-10-20 13:49:40,101 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 54
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 54
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 12, 'scan': 22}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 78
  FINAL_MISSING: 57
  ANOMALY_SCAN_FINAL_RATIO: 24
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 14 | 13,200 | 11,580 | -1,620 | 0.877 |
| S01_NAKAANA1 | 42 | 15 | 8,400 | 7,320 | -1,080 | 0.871 |
| S02_TETSUBAN | 18 | 10 | 3,600 | 4,180 | +580 | 1.161 |

## 直近アラート (24h・新しい順)
```
[13:02:18] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:25:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1074}
[12:24:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1065}
[12:23:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1067}
[12:21:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1060}
[12:19:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1066}
[12:16:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1083}
[12:15:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1081}
[12:13:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1079}
[12:11:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1093}
```

## 本日残レース: 74件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 70件 締切済
- 通知発射: scan=9 nid / final=9 nid / result=5 nid
- predictions: 5 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 096R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 12:55:19 |
| S00 | 175R | win | 1 | 0.5174 | 29.6 | 15.31 | 300 | scan=6.3 drift=+369.8% | 12:11:19 |
| S00 | 107R | win | 1 | 0.5174 | 21.6 | 11.18 | 300 | scan=15.0 drift=+44.0% | 11:30:20 |
| S00 | 133R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=6.0 drift=+11.7% | 11:22:18 |
| S01_NAKAANA1 | 172R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 10:45:18 |
| S01_NAKAANA1 | 127R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=- drift=- | 17:56:19 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4989 | 4.9 | 2.44 | 200 | scan=4.5 drift=+8.9% | 16:19:19 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:23:19 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5174 | 2.9 | 1.50 | 200 | scan=2.3 drift=+26.1% | 15:04:29 |
| S01_NAKAANA1 | 089R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 14:16:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 66 | +28.1% | -42.2% | +495.8% | 12 | 4 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 426.8s |
| **Latency** (scan→final max) | 611.0s |
| **Traffic** (notifications 24h) | 54 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 439 | 0.4797 | 0.3508 | +0.1289 | 🟡+27% | 0.2446 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4406 | 0.2722 | 0.2371 | 🔴-0.20 | 0.741 |
| S01_NAKAANA1 | win | 175 | 0.4939 | 0.3543 | 0.2453 | 🔴-0.07 | 0.973 |
| S02_TETSUBAN | win | 84 | 0.5337 | 0.5119 | 0.2592 | 🔴-0.04 | 0.927 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 158 | 0.4188 | 0.3228 | 🔴+0.0960 |
| 0.50+ | 259 | 0.5438 | 0.3784 | 🔴+0.1654 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 189 | 0.779 |
| win | <5.0 | ✅learned | 340 | 0.748 |
| win | <10.0 | ✅learned | 147 | 0.459 |
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
_auto-generated by claude_snapshot.py at 2026-10-20T13:50:01.805880+09:00_