# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-18T05:20:01.695818+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×48 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×52  [2026-07-17T23:08:03]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-07-17T18:03:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-17T11:16:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-07-17T09:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-17T06:00:09]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=33.3% ROI=0.78 (コスト 11,000/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2282 actual=0.2000 gap=+0.0282`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S00: n=176 hit%=29.0% hit_CI[Bonf]=[20.2,39.6]% ROI=0.74 ROI_boot95=[0.56,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=29.8% hit_CI[Bonf]=[20.6,41.0]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=43.5% hit_CI[Bonf]=[27.9,60.5]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=31.8% ROI=0.82 (コスト 20,100/回収 16,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=30.6% ROI=0.60 (コスト 8,900/回収 5,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=406 pred=0.4691 actual=0.3177 error=+0.1514 (+32%) brier=0.2375 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=176 pred=0.4287 hit=0.2898 cal_err=+0.1389 brier=0.2265 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.87MB / last modified 2026-07-18T05:00:03.063616+09:00

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
66 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 23:55:03,866 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 23:55:03,895 [INFO] predictor: Models loaded OK
2026-07-17 23:55:03,897 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-17 23:56:03,418 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-17 23:56:03,418 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 23:56:03,418 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 23:56:03,446 [INFO] predictor: Models loaded OK
2026-07-17 23:56:03,448 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-17 23:57:03,597 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-07-17 23:57:03,598 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 23:57:03,598 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 23:57:03,658 [INFO] predictor: Models loaded OK
2026-07-17 23:57:03,662 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-17 23:58:04,014 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-07-17 23:58:04,014 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 23:58:04,014 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 23:58:04,042 [INFO] predictor: Models loaded OK
2026-07-17 23:58:04,044 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-17 23:59:03,486 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-07-17 23:59:03,486 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 23:59:03,486 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 23:59:03,514 [INFO] predictor: Models loaded OK
2026-07-17 23:59:03,516 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 77
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 77
  }
]
```

## Phase別通知記録 (24h)
{'final': 32, 'result': 15, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 164
  FINAL_MISSING: 48
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 15 | 13,800 | 13,470 | -330 | 0.976 |
| S01_NAKAANA1 | 40 | 12 | 8,000 | 6,340 | -1,660 | 0.792 |
| S02_TETSUBAN | 15 | 7 | 3,000 | 3,680 | +680 | 1.227 |

## 直近アラート (24h・新しい順)
```
[23:33:03] FINAL_MISSING: {"deadline": "2026-07-17T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071716011157", "sid": "S01_NAKAANA1"}
[23:21:03] FINAL_MISSING: {"deadline": "2026-07-17T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071702051244", "sid": "S00"}
[23:16:04] FINAL_MISSING: {"deadline": "2026-07-17T16:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071701041642", "sid": "S00"}
[23:08:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:05:04] FINAL_MISSING: {"deadline": "2026-07-17T16:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071712041633", "sid": "S00"}
[23:03:04] FINAL_MISSING: {"deadline": "2026-07-17T12:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071716021226", "sid": "S02_TETSUBAN"}
[22:32:19] FINAL_MISSING: {"deadline": "2026-07-17T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071716011157", "sid": "S01_NAKAANA1"}
[22:20:05] FINAL_MISSING: {"deadline": "2026-07-17T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071702051244", "sid": "S00"}
[22:16:03] FINAL_MISSING: {"deadline": "2026-07-17T16:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071701041642", "sid": "S00"}
[22:07:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
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
| S00 | 0110R | win | 1 | 0.4111 | 14.1 | 5.80 | 300 | scan=- drift=- | 19:36:19 |
| S01_NAKAANA1 | 128R | win | 1 | 0.5476 | 4.1 | 2.25 | 200 | scan=- drift=- | 18:22:18 |
| S02_TETSUBAN | 071R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=2.2 drift=-9.1% | 15:17:19 |
| S01_NAKAANA1 | 118R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.0 drift=+10.0% | 14:19:29 |
| S00 | 088R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=6.3 drift=-14.3% | 13:55:29 |
| S01_NAKAANA1 | 117R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.0 drift=+46.7% | 13:48:20 |
| S00 | 117R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=- drift=- | 13:48:18 |
| S02_TETSUBAN | 164R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 13:20:19 |
| S01_NAKAANA1 | 085R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 12:30:25 |
| S00 | 085R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=12.7 drift=-64.6% | 12:30:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +14.3% | -64.6% | +533.3% | 16 | 5 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 467.3s |
| **Latency** (scan→final max) | 610.8s |
| **Traffic** (notifications 24h) | 77 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4685 | 0.3178 | +0.1506 | 🟡+32% | 0.2378 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4272 | 0.2825 | 0.2277 | 🔴-0.12 | 0.731 |
| S01_NAKAANA1 | win | 160 | 0.4803 | 0.3000 | 0.2379 | 🔴-0.13 | 0.777 |
| S02_TETSUBAN | win | 72 | 0.5435 | 0.4444 | 0.2622 | 🔴-0.06 | 0.903 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2276 | 0.2000 | ✅+0.0276 |
| 0.30-0.50 | 157 | 0.4182 | 0.2803 | 🔴+0.1380 |
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
_auto-generated by claude_snapshot.py at 2026-07-18T05:20:01.695818+09:00_