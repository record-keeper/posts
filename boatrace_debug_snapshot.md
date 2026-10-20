# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-20T18:20:01.499904+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-10-20T18:04:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×52  [2026-10-20T15:47:43]
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
- DB: 16.25MB / last modified 2026-10-20T18:19:19.711394+09:00

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
FO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-20 18:17:04,375 [INFO] predictor: Models loaded OK
2026-10-20 18:17:04,496 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-20 18:18:04,566 [INFO] run_cycle: === run_cycle 18:18:04 ===
2026-10-20 18:18:04,566 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-20 18:18:04,566 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-20 18:18:04,641 [INFO] predictor: Models loaded OK
2026-10-20 18:18:04,763 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-20 18:19:04,480 [INFO] run_cycle: === run_cycle 18:19:04 ===
2026-10-20 18:19:04,480 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-20 18:19:04,480 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-20 18:19:04,547 [INFO] predictor: Models loaded OK
2026-10-20 18:19:16,024 [INFO] scraper: odds3t: 120/120 parsed
2026-10-20 18:19:17,143 [INFO] scraper: odds3f: 20/20 parsed
2026-10-20 18:19:18,275 [INFO] scraper: odds2t: 30/30 parsed
2026-10-20 18:19:18,276 [INFO] scraper: odds2f: 15/15 parsed
2026-10-20 18:19:19,386 [INFO] scraper: odds_win: 6/6 parsed
2026-10-20 18:19:19,386 [INFO] scraper: fetch_race 12/8: boats=6 odds=191/191
2026-10-20 18:19:19,390 [INFO] predictor: CALIBRATION_MODE=on
2026-10-20 18:19:19,390 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-20 18:19:19,393 [INFO] run_cycle: fetched 12/8 [scan]: 156 combos
2026-10-20 18:19:19,489 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-20 18:20:05,940 [INFO] run_cycle: === run_cycle 18:20:05 ===
2026-10-20 18:20:05,940 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-20 18:20:05,940 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-20 18:20:05,985 [INFO] predictor: Models loaded OK

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
    "c": 48
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 48
  }
]
```

## Phase別通知記録 (24h)
{'final': 19, 'result': 11, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 122
  FINAL_MISSING: 47
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 14 | 12,600 | 11,340 | -1,260 | 0.9 |
| S01_NAKAANA1 | 44 | 15 | 8,800 | 7,320 | -1,480 | 0.832 |
| S02_TETSUBAN | 18 | 10 | 3,600 | 3,760 | +160 | 1.044 |

## 直近アラート (24h・新しい順)
```
[18:04:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:01:19] FINAL_MISSING: {"deadline": "2026-10-20T13:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102009071328", "sid": "S01_NAKAANA1"}
[18:00:06] FINAL_MISSING: {"deadline": "2026-10-20T16:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102012041629", "sid": "S00"}
[17:59:03] FINAL_MISSING: {"deadline": "2026-10-20T17:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102012061729", "sid": "S00"}
[17:04:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:01:04] FINAL_MISSING: {"deadline": "2026-10-20T13:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102009071328", "sid": "S01_NAKAANA1"}
[16:59:30] FINAL_MISSING: {"deadline": "2026-10-20T16:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102012041629", "sid": "S00"}
[16:47:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 908}
[16:46:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 913}
[16:45:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 918}
```

## 本日残レース: 20件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 124件 締切済
- 通知発射: scan=17 nid / final=18 nid / result=10 nid
- predictions: 10 / うち結果DB記録済: 10
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 1612R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=2.7 drift=-25.9% | 16:43:30 |
| S02_TETSUBAN | 1311R | win | 1 | 0.5174 | 2.2 | 1.14 | 200 | scan=- drift=- | 15:43:19 |
| S00 | 0910R | win | 1 | 0.5123 | 5.2 | 2.66 | 300 | scan=- drift=- | 15:05:20 |
| S01_NAKAANA1 | 038R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=- drift=- | 14:21:49 |
| S01_NAKAANA1 | 138R | win | 1 | 0.5891 | 4.6 | 2.71 | 200 | scan=3.7 drift=+24.3% | 14:03:18 |
| S02_TETSUBAN | 096R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 12:55:19 |
| S00 | 175R | win | 1 | 0.5174 | 29.6 | 15.31 | 300 | scan=6.3 drift=+369.8% | 12:11:19 |
| S00 | 107R | win | 1 | 0.5174 | 21.6 | 11.18 | 300 | scan=15.0 drift=+44.0% | 11:30:20 |
| S00 | 133R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=6.0 drift=+11.7% | 11:22:18 |
| S01_NAKAANA1 | 172R | win | 1 | 0.4111 | 3.4 | 1.40 | 200 | scan=- drift=- | 10:45:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +28.5% | -42.2% | +495.8% | 12 | 3 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 342.6s |
| **Latency** (scan→final max) | 601.3s |
| **Traffic** (notifications 24h) | 48 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 441 | 0.4799 | 0.3515 | +0.1284 | 🟡+27% | 0.2445 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 181 | 0.4410 | 0.2762 | 0.2371 | 🔴-0.19 | 0.743 |
| S01_NAKAANA1 | win | 175 | 0.4939 | 0.3543 | 0.2453 | 🔴-0.07 | 0.973 |
| S02_TETSUBAN | win | 85 | 0.5340 | 0.5059 | 0.2588 | 🔴-0.04 | 0.915 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 158 | 0.4188 | 0.3228 | 🔴+0.0960 |
| 0.50+ | 261 | 0.5437 | 0.3793 | 🔴+0.1644 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 190 | 0.778 |
| win | <5.0 | ✅learned | 340 | 0.748 |
| win | <10.0 | ✅learned | 148 | 0.458 |
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
_auto-generated by claude_snapshot.py at 2026-10-20T18:20:01.499904+09:00_