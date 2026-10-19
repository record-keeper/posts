# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-20T07:50:01.167787+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×61 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

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

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=178 pred=0.4932 hit=0.3652 cal_err=+0.1280 brier=0.2454 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=84 pred=0.5332 hit=0.5238 cal_err=+0.0094 brier=0.2578 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1833 actual=0.0000 gap=+0.1833`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-20T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=32 pred=0.3211 actual=0.2188 gap=+0.1023`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.22MB / last modified 2026-10-20T07:30:02.571372+09:00

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
90 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 23:55:03,790 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 23:55:03,834 [INFO] predictor: Models loaded OK
2026-10-19 23:55:03,837 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 23:56:03,407 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-10-19 23:56:03,407 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 23:56:03,407 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 23:56:03,453 [INFO] predictor: Models loaded OK
2026-10-19 23:56:03,459 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 23:57:04,229 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-19 23:57:04,229 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 23:57:04,229 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 23:57:04,263 [INFO] predictor: Models loaded OK
2026-10-19 23:57:04,265 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 23:58:03,581 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-10-19 23:58:03,581 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 23:58:03,581 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 23:58:03,621 [INFO] predictor: Models loaded OK
2026-10-19 23:58:03,625 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 23:59:04,098 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-10-19 23:59:04,099 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 23:59:04,099 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 23:59:04,140 [INFO] predictor: Models loaded OK
2026-10-19 23:59:04,144 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 55
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 55
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 14, 'scan': 21}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 61
  ANOMALY_SCRAPER_FAILURE_BURST: 56
  ANOMALY_SCAN_FINAL_RATIO: 28
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 3
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 45 | 17 | 13,500 | 13,560 | +60 | 1.004 |
| S01_NAKAANA1 | 45 | 17 | 9,000 | 7,940 | -1,060 | 0.882 |
| S02_TETSUBAN | 18 | 11 | 3,600 | 4,520 | +920 | 1.256 |

## 直近アラート (24h・新しい順)
```
[06:00:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:49:03] FINAL_MISSING: {"deadline": "2026-10-19T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101902061314", "sid": "S00"}
[23:33:03] FINAL_MISSING: {"deadline": "2026-10-19T17:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101912071759", "sid": "S00"}
[23:28:04] FINAL_MISSING: {"deadline": "2026-10-19T13:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101916071354", "sid": "S00"}
[23:24:04] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.149, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.737, "today_scan_count": 19, "z_score": -2.1}
[23:23:03] FINAL_MISSING: {"deadline": "2026-10-19T14:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101902091446", "sid": "S00"}
[23:23:03] FINAL_MISSING: {"deadline": "2026-10-19T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101902011047", "sid": "S00"}
[23:23:03] FINAL_MISSING: {"deadline": "2026-10-19T16:48:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101901041648", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:06:04] FINAL_MISSING: {"deadline": "2026-10-19T18:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101919031834", "sid": "S00"}
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
| S01_NAKAANA1 | 127R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=- drift=- | 17:56:19 |
| S01_NAKAANA1 | 013R | win | 1 | 0.4989 | 4.9 | 2.44 | 200 | scan=4.5 drift=+8.9% | 16:19:19 |
| S01_NAKAANA1 | 011R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:23:19 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5174 | 2.9 | 1.50 | 200 | scan=2.3 drift=+26.1% | 15:04:29 |
| S01_NAKAANA1 | 089R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 14:16:19 |
| S00 | 098R | win | 1 | 0.4111 | 12.0 | 4.93 | 300 | scan=4.5 drift=+166.7% | 13:58:18 |
| S01_NAKAANA1 | 166R | win | 1 | 0.4926 | 4.1 | 2.02 | 200 | scan=- drift=- | 13:22:19 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 12:55:19 |
| S00 | 024R | win | 1 | 0.5735 | 20.1 | 11.53 | 300 | scan=19.5 drift=+3.1% | 12:11:19 |
| S02_TETSUBAN | 033R | win | 1 | 0.5990 | 2.6 | 1.56 | 200 | scan=- drift=- | 12:05:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 67 | +25.9% | -42.2% | +495.8% | 12 | 4 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 469.9s |
| **Latency** (scan→final max) | 611.0s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 439 | 0.4793 | 0.3599 | +0.1194 | 🟡+25% | 0.2445 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4399 | 0.2768 | 0.2371 | 🔴-0.18 | 0.754 |
| S01_NAKAANA1 | win | 178 | 0.4932 | 0.3652 | 0.2454 | 🔴-0.06 | 1.006 |
| S02_TETSUBAN | win | 84 | 0.5332 | 0.5238 | 0.2578 | 🔴-0.03 | 0.94 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 158 | 0.4182 | 0.3291 | 🔴+0.0891 |
| 0.50+ | 259 | 0.5436 | 0.3900 | 🔴+0.1536 |

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
_auto-generated by claude_snapshot.py at 2026-10-20T07:50:01.167787+09:00_