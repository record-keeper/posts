# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-24T07:20:01.710475+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×36 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×201 (24h)
- 🔴 PSI_DRIFT_DETECTED×36 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=71<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-24T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=90<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S00: n=71 hit%=22.5% hit_CI[Bonf]=[11.6,39.3]% ROI=0.57 ROI_boot95=[0.31,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=90 hit%=33.3% hit_CI[Bonf]=[20.9,48.5]% ROI=0.85 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-24T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=40.0% hit_CI[Bonf]=[21.3,62.1]% ROI=1.15 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-24T06:00:19]
- key: `ORPHAN_SCAN|266 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=23 hit%=17.4% ROI=0.77 (コスト 5,000/回収 3,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-24T06:00:19]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=38 hit%=44.7% ROI=1.14 (コスト 8,700/回収 9,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|bt=win: n=201 pred=0.4776 actual=0.3085 error=+0.1692 (+35%) brier=0.2354 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S00(win): n=71 pred=0.4276 hit=0.2254 cal_err=+0.2022 brier=0.2098 BSS=-0.20 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=90 pred=0.4851 hit=0.3333 cal_err=+0.1518 brier=0.2408 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=40 pred=0.5496 hit=0.4000 cal_err=+0.1496 brier=0.2685 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=20 pred=0.3198 actual=0.2000 gap=+0.1198`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=58 pred=0.4470 actual=0.3276 gap=+0.1194`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-24T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.50+: n=114 pred=0.5457 actual=0.3421 gap=+0.2036`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-24T06:00:10]
- key: `PAYOUT_RATIO_WEIRD|pid=3342 bet=300 odds=6.7 payout=420 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-24T06:00:10]
- key: `PAYOUT_RATIO_WEIRD|pid=3346 bet=300 odds=4.4 payout=360 ratio=0.27`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-24T06:00:10]
- key: `PAYOUT_RATIO_WEIRD|pid=3358 bet=300 odds=16.0 payout=1200 ratio=0.25`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-24T06:00:10]
- key: `PAYOUT_RATIO_WEIRD|pid=3359 bet=300 odds=10.2 payout=840 ratio=0.27`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.57MB / last modified 2026-11-24T07:00:07.082983+09:00

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
20 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-23 23:55:04,320 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-23 23:55:04,370 [INFO] predictor: Models loaded OK
2026-11-23 23:55:04,376 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-23 23:56:03,374 [INFO] run_cycle: === run_cycle 23:56:03 ===
2026-11-23 23:56:03,374 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-23 23:56:03,374 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-23 23:56:03,405 [INFO] predictor: Models loaded OK
2026-11-23 23:56:03,408 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-23 23:57:03,743 [INFO] run_cycle: === run_cycle 23:57:03 ===
2026-11-23 23:57:03,743 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-23 23:57:03,743 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-23 23:57:03,776 [INFO] predictor: Models loaded OK
2026-11-23 23:57:03,778 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-23 23:58:03,534 [INFO] run_cycle: === run_cycle 23:58:03 ===
2026-11-23 23:58:03,534 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-23 23:58:03,534 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-23 23:58:03,567 [INFO] predictor: Models loaded OK
2026-11-23 23:58:03,569 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-23 23:59:03,191 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-11-23 23:59:03,191 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-23 23:59:03,191 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-23 23:59:03,223 [INFO] predictor: Models loaded OK
2026-11-23 23:59:03,225 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 52
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 52
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 9, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 243
  FINAL_MISSING: 201
  PSI_DRIFT_DETECTED: 36
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 5
  ANOMALY_SCAN_FINAL_RATIO: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 8 | 2 | 2,400 | 1,380 | -1,020 | 0.575 |
| S01_NAKAANA1 | 19 | 8 | 3,800 | 3,360 | -440 | 0.884 |
| S02_TETSUBAN | 4 | 1 | 800 | 1,680 | +880 | 2.1 |

## 直近アラート (24h・新しい順)
```
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 170, "n_recent": 31, "psi": 0.61}
[23:55:04] FINAL_MISSING: {"deadline": "2026-11-23T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112321101311", "sid": "S01_NAKAANA1"}
[23:55:04] FINAL_MISSING: {"deadline": "2026-11-23T13:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112321101311", "sid": "S00"}
[23:41:04] FINAL_MISSING: {"deadline": "2026-11-23T12:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112322051250", "sid": "S00"}
[23:41:04] FINAL_MISSING: {"deadline": "2026-11-23T10:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112314061051", "sid": "S01_NAKAANA1"}
[23:41:04] FINAL_MISSING: {"deadline": "2026-11-23T10:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112311021053", "sid": "S02_TETSUBAN"}
[23:41:04] FINAL_MISSING: {"deadline": "2026-11-23T11:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112309041156", "sid": "S02_TETSUBAN"}
[23:23:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:23:04] FINAL_MISSING: {"deadline": "2026-11-23T12:37:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112321091237", "sid": "S01_NAKAANA1"}
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
| S01_NAKAANA1 | 074R | win | 1 | 0.5719 | 3.5 | 2.00 | 200 | scan=3.1 drift=+12.9% | 16:34:46 |
| S01_NAKAANA1 | 122R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=- drift=- | 15:49:13 |
| S01_NAKAANA1 | 135R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=- drift=- | 12:38:14 |
| S01_NAKAANA1 | 023R | win | 1 | 0.5104 | 3.5 | 1.79 | 200 | scan=3.0 drift=+16.7% | 11:38:24 |
| S00 | 107R | win | 1 | 0.5123 | 24.0 | 12.30 | 300 | scan=- drift=- | 11:34:39 |
| S02_TETSUBAN | 052R | win | 1 | 0.5080 | 2.1 | 1.07 | 200 | scan=- drift=- | 11:00:54 |
| S01_NAKAANA1 | 145R | win | 1 | 0.5476 | 4.9 | 2.68 | 200 | scan=3.9 drift=+25.6% | 10:18:24 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.3 drift=+33.3% | 08:59:31 |
| S00 | 142R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=- drift=- | 08:59:29 |
| S00 | 122R | win | 1 | 0.1034 | 4.7 | 0.49 | 300 | scan=- drift=- | 15:48:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 15 | +1.9% | -25.0% | +33.3% | 4 | 0 | 8 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 412.6s |
| **Latency** (scan→final max) | 611.9s |
| **Traffic** (notifications 24h) | 52 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 201 | 0.4776 | 0.3085 | +0.1692 | 🟡+35% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 71 | 0.4276 | 0.2254 | 0.2098 | 🔴-0.20 | 0.57 |
| S01_NAKAANA1 | win | 90 | 0.4851 | 0.3333 | 0.2408 | 🔴-0.08 | 0.854 |
| S02_TETSUBAN | win | 40 | 0.5496 | 0.4000 | 0.2685 | 🔴-0.12 | 1.15 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 78 | 0.4144 | 0.2949 | 🔴+0.1195 |
| 0.50+ | 114 | 0.5457 | 0.3421 | 🔴+0.2036 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 208 | 0.818 |
| win | <5.0 | ✅learned | 381 | 0.737 |
| win | <10.0 | ✅learned | 160 | 0.449 |
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
_auto-generated by claude_snapshot.py at 2026-11-24T07:20:01.710475+09:00_