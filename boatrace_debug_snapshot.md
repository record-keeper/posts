# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-17T07:10:02.058543+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

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

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=161 pred=0.4814 hit=0.2981 cal_err=+0.1832 brier=0.2389 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=69 pred=0.5438 hit=0.4348 cal_err=+0.1090 brier=0.2620 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3262 actual=0.0938 gap=+0.2325`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=119 pred=0.4404 actual=0.3277 gap=+0.1127`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.76MB / last modified 2026-07-17T07:00:02.448122+09:00

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
39 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 23:55:04,039 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 23:55:04,082 [INFO] predictor: Models loaded OK
2026-07-16 23:55:04,086 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 23:56:03,745 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-07-16 23:56:03,745 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 23:56:03,745 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 23:56:03,773 [INFO] predictor: Models loaded OK
2026-07-16 23:56:03,775 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 23:57:03,697 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-07-16 23:57:03,697 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 23:57:03,697 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 23:57:03,746 [INFO] predictor: Models loaded OK
2026-07-16 23:57:03,751 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 23:58:03,480 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-07-16 23:58:03,481 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 23:58:03,481 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 23:58:03,509 [INFO] predictor: Models loaded OK
2026-07-16 23:58:03,512 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-16 23:59:04,212 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-07-16 23:59:04,212 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-16 23:59:04,212 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-16 23:59:04,244 [INFO] predictor: Models loaded OK
2026-07-16 23:59:04,246 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 50
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 50
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 12, 'scan': 16}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 130
  FINAL_MISSING: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_SCAN_FINAL_RATIO: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 16 | 14,400 | 14,070 | -330 | 0.977 |
| S01_NAKAANA1 | 39 | 12 | 7,800 | 6,340 | -1,460 | 0.813 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 4,000 | +1,200 | 1.429 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:59:04] FINAL_MISSING: {"deadline": "2026-07-16T15:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071601011523", "sid": "S00"}
[23:18:03] FINAL_MISSING: {"deadline": "2026-07-16T12:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071608051242", "sid": "S00"}
[23:10:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[22:59:03] FINAL_MISSING: {"deadline": "2026-07-16T15:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071601011523", "sid": "S00"}
[22:17:04] FINAL_MISSING: {"deadline": "2026-07-16T12:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071608051242", "sid": "S00"}
[22:09:19] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[21:58:04] FINAL_MISSING: {"deadline": "2026-07-16T15:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071601011523", "sid": "S00"}
[21:16:03] FINAL_MISSING: {"deadline": "2026-07-16T12:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071608051242", "sid": "S00"}
[21:08:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
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
| S01_NAKAANA1 | 019R | win | 1 | 0.3177 | 3.0 | 0.95 | 200 | scan=- drift=- | 19:03:17 |
| S00 | 015R | win | 1 | 0.3177 | 6.3 | 2.00 | 300 | scan=- drift=- | 17:06:43 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5174 | 3.6 | 1.86 | 200 | scan=3.5 drift=+2.9% | 16:39:29 |
| S02_TETSUBAN | 072R | win | 1 | 0.5123 | 2.1 | 1.08 | 200 | scan=- drift=- | 15:44:29 |
| S02_TETSUBAN | 071R | win | 1 | 0.5735 | 2.3 | 1.32 | 200 | scan=- drift=- | 15:17:20 |
| S01_NAKAANA1 | 174R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=- drift=- | 12:10:22 |
| S01_NAKAANA1 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 200 | scan=3.7 drift=+21.6% | 11:42:20 |
| S00 | 173R | win | 1 | 0.3564 | 4.5 | 1.60 | 300 | scan=- drift=- | 11:42:19 |
| S01_NAKAANA1 | 132R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=- drift=- | 11:00:23 |
| S01_NAKAANA1 | 186R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=3.7 drift=+27.0% | 10:56:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +21.7% | -48.8% | +533.3% | 15 | 5 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 409.4s |
| **Latency** (scan→final max) | 598.9s |
| **Traffic** (notifications 24h) | 50 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 406 | 0.4691 | 0.3177 | +0.1514 | 🟡+32% | 0.2375 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4287 | 0.2898 | 0.2265 | 🔴-0.10 | 0.745 |
| S01_NAKAANA1 | win | 161 | 0.4814 | 0.2981 | 0.2389 | 🔴-0.14 | 0.773 |
| S02_TETSUBAN | win | 69 | 0.5438 | 0.4348 | 0.2620 | 🔴-0.07 | 0.887 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2282 | 0.2000 | ✅+0.0282 |
| 0.30-0.50 | 151 | 0.4162 | 0.2781 | 🔴+0.1381 |
| 0.50+ | 225 | 0.5427 | 0.3511 | 🔴+0.1916 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 73 | 0.802 |
| win | <5.0 | ✅learned | 143 | 0.71 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
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
_auto-generated by claude_snapshot.py at 2026-07-17T07:10:02.058543+09:00_