# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-10T07:10:01.685679+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×672 (24h)
- 🔴 PSI_DRIFT_DETECTED×26 (24h)
- 🔴 STRATEGY_CI_FAIL×14 (24h)
- 🔴 STRATEGY_NO_COMBO_FILTER×6 (24h)
- 🔴 STRATEGY_NO_CSCV×6 (24h)
- 🟡 LARGE_ODDS_DRIFT×4 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1899 actual=0.1667 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-10T06:00:08]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=20.0% ROI=0.52 (コスト 8,800/回収 4,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=57 pred=0.4471 actual=0.2632 gap=+0.1840`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-10T06:00:08]
- key: `ROI_STAT|S00: n=144 hit%=25.7% hit_CI[Bonf]=[16.7,37.3]% ROI=0.88 ROI_boot95=[0.61,1.18]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-10T06:00:08]
- key: `INSUFFICIENT_SAMPLE|S00: n=144<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-10T06:00:08]
- key: `DRIFT_BUCKET|drift ≥+30%: n=24 hit%=20.8% ROI=0.62 (コスト 6,400/回収 3,960)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=14 pred=0.3306 actual=0.1429 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-05-10T06:00:08]
- key: `ORPHAN_SCAN|183 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-10T06:00:08]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=25 hit%=28.0% ROI=1.27 (コスト 6,800/回収 8,670)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|bt=win: n=145 pred=0.4308 actual=0.2552 error=+0.1756 (+41%) brier=0.2291 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|S00(win): n=144 pred=0.4297 hit=0.2569 cal_err=+0.1728 brier=0.2283 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-10T06:00:08]
- key: `CALIBRATION_LIVE|decile 0.50+: n=54 pred=0.5321 actual=0.2778 gap=+0.2544`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=881 bet=300 odds=12.7 payout=900 ratio=0.24`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=906 bet=300 odds=14.2 payout=360 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=913 bet=300 odds=4.6 payout=2550 ratio=1.85`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=917 bet=300 odds=6.2 payout=390 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-10T06:00:07]
- key: `PAYOUT_RATIO_WEIRD|pid=931 bet=300 odds=5.9 payout=450 ratio=0.25`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.29MB / last modified 2026-05-10T07:00:02.862808+09:00

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
81 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 23:55:06,381 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 23:55:06,431 [INFO] predictor: Models loaded OK
2026-05-09 23:55:06,436 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 23:56:05,824 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-05-09 23:56:05,824 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 23:56:05,824 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 23:56:05,891 [INFO] predictor: Models loaded OK
2026-05-09 23:56:05,899 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 23:57:05,949 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-05-09 23:57:05,949 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 23:57:05,949 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 23:57:06,010 [INFO] predictor: Models loaded OK
2026-05-09 23:57:06,016 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 23:58:05,240 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-05-09 23:58:05,240 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 23:58:05,240 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 23:58:05,307 [INFO] predictor: Models loaded OK
2026-05-09 23:58:05,313 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-09 23:59:05,969 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-05-09 23:59:05,969 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-09 23:59:05,969 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-09 23:59:06,010 [INFO] predictor: Models loaded OK
2026-05-09 23:59:06,016 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 100
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 100
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 8, 'scan': 77}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 672
  ANOMALY_SCAN_FINAL_RATIO: 76
  ANOMALY_SCRAPER_FAILURE_BURST: 71
  PSI_DRIFT_DETECTED: 26
  ANOMALY_ML_PROB_SHIFT: 19
  ANOMALY_ODDS_SHIFT: 19
  ANOMALY_BET_VOLUME_SPIKE: 18
  STRATEGY_CI_FAIL: 14
  STRATEGY_NO_COMBO_FILTER: 6
  STRATEGY_NO_CSCV: 6
  LARGE_ODDS_DRIFT: 4
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 16 | 14,700 | 14,160 | -540 | 0.963 |
| S02_TETSUBAN | 1 | 0 | 200 | 0 | -200 | 0.0 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:07] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 95, "n_recent": 50, "psi": 0.393}
[23:59:06] FINAL_MISSING: {"deadline": "2026-05-09T17:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050924061725", "sid": "S00"}
[23:59:06] FINAL_MISSING: {"deadline": "2026-05-09T16:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050922091624", "sid": "S04_SELL_3T"}
[23:55:06] FINAL_MISSING: {"deadline": "2026-05-09T11:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050918071119", "sid": "S04_SELL_3T"}
[23:55:06] FINAL_MISSING: {"deadline": "2026-05-09T10:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050918051017", "sid": "S04_SELL_3T"}
[23:55:06] FINAL_MISSING: {"deadline": "2026-05-09T12:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050913051220", "sid": "S04_SELL_3T"}
[23:54:05] FINAL_MISSING: {"deadline": "2026-05-09T16:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050920031619", "sid": "S04_SELL_3T"}
[23:52:06] FINAL_MISSING: {"deadline": "2026-05-09T13:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050921101317", "sid": "S04_SELL_3T"}
[23:47:06] FINAL_MISSING: {"deadline": "2026-05-09T15:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026050905081512", "sid": "S04_SELL_3T"}
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
| S02_TETSUBAN | 208R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=2.0 drift=+5.0% | 18:27:21 |
| S00 | 245R | win | 1 | 0.5123 | 13.6 | 6.97 | 300 | scan=- drift=- | 16:57:22 |
| S00 | 244R | win | 1 | 0.3177 | 6.7 | 2.13 | 300 | scan=4.5 drift=+48.9% | 16:29:21 |
| S00 | 227R | win | 1 | 0.4111 | 8.4 | 3.45 | 300 | scan=26.2 drift=-67.9% | 15:25:21 |
| S00 | 223R | win | 1 | 0.4989 | 6.1 | 3.04 | 300 | scan=18.0 drift=-66.1% | 13:27:21 |
| S00 | 1410R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=6.2 drift=-33.9% | 13:01:32 |
| S04_SELL_3T | 212R | 3t | 1-4-2 | 0.0086 | 7.1 | 0.06 | 100 | scan=7.9 drift=-10.1% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-4-3 | 0.0052 | 16.0 | 0.08 | 100 | scan=14.8 drift=+8.1% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-4-6 | 0.0007 | 20.1 | 0.01 | 100 | scan=34.3 drift=-41.4% | 09:11:21 |
| S04_SELL_3T | 212R | 3t | 1-5-2 | 0.0002 | 63.9 | 0.01 | 100 | scan=47.8 drift=+33.7% | 09:11:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 39 | -10.4% | -67.9% | +124.4% | 20 | 15 | 29 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 520.7s |
| **Latency** (scan→final max) | 612.5s |
| **Traffic** (notifications 24h) | 100 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 145 | 0.4308 | 0.2552 | +0.1756 | 🟡+41% | 0.2291 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 144 | 0.4297 | 0.2569 | 0.2283 | 🔴-0.20 | 0.878 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 6 | 0.1899 | 0.1667 | ✅+0.0232 |
| 0.20-0.30 | 9 | 0.2241 | 0.3333 | 🔴-0.1093 |
| 0.30-0.50 | 71 | 0.4242 | 0.2394 | 🔴+0.1847 |
| 0.50+ | 54 | 0.5321 | 0.2778 | 🔴+0.2544 |

## Settlement Ratio データ品質

- 学習済み: 1バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 6 | 0.35 |
| win | <10.0 | ✅learned | 23 | 0.562 |
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
_auto-generated by claude_snapshot.py at 2026-05-10T07:10:01.685679+09:00_