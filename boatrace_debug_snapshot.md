# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-27T06:10:02.010493+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×122 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S00: n=55 hit%=16.4% hit_CI[Bonf]=[6.7,34.9]% ROI=0.44 ROI_boot95=[0.17,0.78]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=55<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=80 hit%=33.8% hit_CI[Bonf]=[20.7,49.9]% ROI=0.90 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-27T06:00:12]
- key: `ROI_STAT|S02_TETSUBAN: n=38 hit%=42.1% hit_CI[Bonf]=[22.5,64.5]% ROI=0.93 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-27T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=38<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-27T06:00:12]
- key: `ORPHAN_SCAN|282 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-27T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=34 hit%=50.0% ROI=1.33 (コスト 7,700/回収 10,210)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=173 pred=0.4718 actual=0.3006 error=+0.1712 (+36%) brier=0.2335 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|S00(win): n=55 pred=0.4106 hit=0.1636 cal_err=+0.2470 brier=0.1933 BSS=-0.41 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=80 pred=0.4797 hit=0.3375 cal_err=+0.1422 brier=0.2410 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=38 pred=0.5435 hit=0.4211 cal_err=+0.1225 brier=0.2756 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=19 pred=0.3177 actual=0.1053 gap=+0.2125`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=50 pred=0.4423 actual=0.3600 gap=+0.0823`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-27T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.50+: n=97 pred=0.5424 actual=0.3299 gap=+0.2125`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3393 bet=300 odds=16.8 payout=480 ratio=0.10`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3451 bet=200 odds=3.8 payout=1280 ratio=1.68`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3482 bet=300 odds=6.3 payout=510 ratio=0.27`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3495 bet=200 odds=2.0 payout=520 ratio=1.30`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-11-27T06:00:08]
- key: `PAYOUT_RATIO_WEIRD|pid=3502 bet=300 odds=7.0 payout=480 ratio=0.23`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.75MB / last modified 2026-11-27T06:00:24.569475+09:00

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
23 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-26 23:55:04,123 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-26 23:55:04,163 [INFO] predictor: Models loaded OK
2026-11-26 23:55:04,165 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-26 23:56:04,826 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-11-26 23:56:04,826 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-26 23:56:04,826 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-26 23:56:04,890 [INFO] predictor: Models loaded OK
2026-11-26 23:56:04,894 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-26 23:57:04,653 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-11-26 23:57:04,654 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-26 23:57:04,654 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-26 23:57:04,706 [INFO] predictor: Models loaded OK
2026-11-26 23:57:04,709 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-26 23:58:04,249 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-11-26 23:58:04,249 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-26 23:58:04,249 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-26 23:58:04,301 [INFO] predictor: Models loaded OK
2026-11-26 23:58:04,303 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-26 23:59:04,487 [INFO] run_cycle: === run_cycle 23:59:04 ===
2026-11-26 23:59:04,488 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-26 23:59:04,488 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-26 23:59:04,519 [INFO] predictor: Models loaded OK
2026-11-26 23:59:04,522 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 51
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 51
  }
]
```

## Phase別通知記録 (24h)
{'final': 18, 'result': 7, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 235
  FINAL_MISSING: 122
  PSI_DRIFT_DETECTED: 38
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 13 | 2 | 3,900 | 1,380 | -2,520 | 0.354 |
| S01_NAKAANA1 | 24 | 11 | 4,800 | 5,600 | +800 | 1.167 |
| S02_TETSUBAN | 9 | 5 | 1,800 | 3,260 | +1,460 | 1.811 |

## 直近アラート (24h・新しい順)
```
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 127, "n_recent": 46, "psi": 0.362}
[23:50:05] FINAL_MISSING: {"deadline": "2026-11-26T12:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112618081204", "sid": "S01_NAKAANA1"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-11-26T12:04:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112618081204", "sid": "S00"}
[23:50:05] FINAL_MISSING: {"deadline": "2026-11-26T11:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112605021101", "sid": "S02_TETSUBAN"}
[23:33:03] FINAL_MISSING: {"deadline": "2026-11-26T16:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112615041655", "sid": "S00"}
[23:28:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:28:04] FINAL_MISSING: {"deadline": "2026-11-26T13:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112618111342", "sid": "S01_NAKAANA1"}
[23:28:04] FINAL_MISSING: {"deadline": "2026-11-26T12:46:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112610091246", "sid": "S01_NAKAANA1"}
[23:28:04] FINAL_MISSING: {"deadline": "2026-11-26T11:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112610071140", "sid": "S00"}
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
| S01_NAKAANA1 | 206R | win | 1 | 0.5047 | 3.0 | 1.51 | 200 | scan=- drift=- | 17:28:06 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.0 drift=+20.0% | 16:53:40 |
| S02_TETSUBAN | 0312R | win | 1 | 0.4111 | 2.4 | 0.99 | 200 | scan=2.4 drift=+0.0% | 15:59:32 |
| S01_NAKAANA1 | 192R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 15:45:15 |
| S00 | 1710R | win | 1 | 0.5073 | 9.3 | 4.72 | 300 | scan=4.5 drift=+106.7% | 14:24:12 |
| S01_NAKAANA1 | 175R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=4.8 drift=-37.5% | 12:07:27 |
| S00 | 114R | win | 1 | 0.5031 | 12.3 | 6.19 | 300 | scan=- drift=- | 11:41:14 |
| S01_NAKAANA1 | 197R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=- drift=- | 17:56:13 |
| S00 | 194R | win | 1 | 0.0347 | 8.0 | 0.28 | 300 | scan=- drift=- | 16:38:03 |
| S02_TETSUBAN | 204R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.0 drift=+10.0% | 16:33:53 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 20 | +12.5% | -58.9% | +114.7% | 5 | 2 | 16 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 338.9s |
| **Latency** (scan→final max) | 551.0s |
| **Traffic** (notifications 24h) | 51 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 173 | 0.4718 | 0.3006 | +0.1712 | 🟡+36% | 0.2335 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 55 | 0.4106 | 0.1636 | 0.1933 | 🔴-0.41 | 0.438 |
| S01_NAKAANA1 | win | 80 | 0.4797 | 0.3375 | 0.2410 | 🔴-0.08 | 0.899 |
| S02_TETSUBAN | win | 38 | 0.5435 | 0.4211 | 0.2756 | 🔴-0.13 | 0.926 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 69 | 0.4080 | 0.2899 | 🔴+0.1182 |
| 0.50+ | 97 | 0.5424 | 0.3299 | 🔴+0.2125 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 212 | 0.818 |
| win | <5.0 | ✅learned | 386 | 0.739 |
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
_auto-generated by claude_snapshot.py at 2026-11-27T06:10:02.010493+09:00_