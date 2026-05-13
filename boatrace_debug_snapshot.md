# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-14T08:00:02.246453+09:00

### 次に取るべきアクション
> RED最優先: ⚠️ run_cycle.log が481分前（cron停止疑い・今レース時間帯） → ログ/DB確認

### 検出された問題
- 🔴 ⚠️ run_cycle.log が481分前（cron停止疑い・今レース時間帯）
- 🟡 FINAL_MISSING×105 (24h)
- 🔴 PSI_DRIFT_DETECTED×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=13 pred=0.0030 actual=0.0769 gap=-0.0739`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2234 actual=0.3000 gap=-0.0766`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-14T06:00:12]
- key: `ROI_STAT|S00: n=176 hit%=25.6% hit_CI[Bonf]=[17.3,36.0]% ROI=0.87 ROI_boot95=[0.62,1.14]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-14T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-14T06:00:12]
- key: `ROI_STAT|S01_NAKAANA1: n=30 hit%=43.3% hit_CI[Bonf]=[21.6,67.9]% ROI=0.87 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-14T06:00:12]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=30<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-14T06:00:12]
- key: `ORPHAN_SCAN|212 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=20.5% ROI=0.58 (コスト 11,500/回収 6,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=28 hit%=32.1% ROI=1.51 (コスト 6,800/回収 10,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=45 hit%=28.9% ROI=1.04 (コスト 11,400/回収 11,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-14T06:00:12]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=22.6% ROI=0.64 (コスト 8,300/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|bt=win: n=226 pred=0.4505 actual=0.3009 error=+0.1496 (+33%) brier=0.2316 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|S00(win): n=176 pred=0.4372 hit=0.2557 cal_err=+0.1815 brier=0.2280 BSS=-0.20 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=30 pred=0.4869 hit=0.4333 cal_err=+0.0535 brier=0.2321 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=20 pred=0.5127 hit=0.5000 cal_err=+0.0127 brier=0.2624 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=19 pred=0.3272 actual=0.1579 gap=+0.1693`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=87 pred=0.4482 actual=0.2874 gap=+0.1609`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-14T06:00:12]
- key: `CALIBRATION_LIVE|decile 0.50+: n=97 pred=0.5405 actual=0.3608 gap=+0.1797`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-05-14T06:00:09]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 2.62MB / last modified 2026-05-14T08:00:04.903098+09:00

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
50 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 23:55:06,850 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 23:55:06,918 [INFO] predictor: Models loaded OK
2026-05-13 23:55:06,922 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-13 23:56:06,475 [INFO] run_cycle: === run_cycle 23:56:06 ===
2026-05-13 23:56:06,475 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 23:56:06,475 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 23:56:06,520 [INFO] predictor: Models loaded OK
2026-05-13 23:56:06,523 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-13 23:57:05,962 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-05-13 23:57:05,962 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 23:57:05,962 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 23:57:06,017 [INFO] predictor: Models loaded OK
2026-05-13 23:57:06,022 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-13 23:58:06,180 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-05-13 23:58:06,180 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 23:58:06,180 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 23:58:06,221 [INFO] predictor: Models loaded OK
2026-05-13 23:58:06,225 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-13 23:59:06,183 [INFO] run_cycle: === run_cycle 23:59:06 ===
2026-05-13 23:59:06,183 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-13 23:59:06,183 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-13 23:59:06,249 [INFO] predictor: Models loaded OK
2026-05-13 23:59:06,255 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 95
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 95
  }
]
```

## Phase別通知記録 (24h)
{'final': 37, 'result': 21, 'scan': 37}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 163
  FINAL_MISSING: 105
  PSI_DRIFT_DETECTED: 32
  KS_ODDS_DRIFT: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 3
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 49 | 16 | 14,700 | 14,400 | -300 | 0.98 |
| S01_NAKAANA1 | 30 | 13 | 6,000 | 5,200 | -800 | 0.867 |
| S02_TETSUBAN | 20 | 10 | 4,000 | 3,900 | -100 | 0.975 |
| S04_SELL_3T | 12 | 1 | 1,200 | 740 | -460 | 0.617 |

## 直近アラート (24h・新しい順)
```
[06:00:06] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.452}
[06:00:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 127, "n_recent": 99, "psi": 0.346}
[23:59:06] FINAL_MISSING: {"deadline": "2026-05-13T14:25:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051322051425", "sid": "S00"}
[23:59:06] FINAL_MISSING: {"deadline": "2026-05-13T11:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051303021121", "sid": "S00"}
[23:55:06] FINAL_MISSING: {"deadline": "2026-05-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051323071116", "sid": "S00"}
[23:52:06] FINAL_MISSING: {"deadline": "2026-05-13T12:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051303041215", "sid": "S00"}
[23:41:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.0, "ks_stat": 0.452}
[23:41:06] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 127, "n_recent": 99, "psi": 0.346}
[23:41:06] FINAL_MISSING: {"deadline": "2026-05-13T18:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026051312061808", "sid": "S00"}
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
| S02_TETSUBAN | 0712R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 20:39:20 |
| S02_TETSUBAN | 0710R | win | 1 | 0.5891 | 2.0 | 1.18 | 200 | scan=- drift=- | 19:42:21 |
| S01_NAKAANA1 | 197R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=3.4 drift=+35.3% | 18:18:22 |
| S00 | 197R | win | 1 | 0.4111 | 4.6 | 1.89 | 300 | scan=- drift=- | 18:18:21 |
| S01_NAKAANA1 | 196R | win | 1 | 0.4991 | 3.1 | 1.55 | 200 | scan=- drift=- | 17:53:20 |
| S00 | 125R | win | 1 | 0.5891 | 6.5 | 3.83 | 300 | scan=14.2 drift=-54.2% | 17:40:24 |
| S00 | 073R | win | 1 | 0.4964 | 4.5 | 2.23 | 300 | scan=7.2 drift=-37.5% | 16:36:20 |
| S02_TETSUBAN | 1611R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=- drift=- | 16:08:45 |
| S01_NAKAANA1 | 122R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.3 drift=+6.1% | 16:04:21 |
| S01_NAKAANA1 | 012R | win | 1 | 0.4989 | 3.9 | 1.95 | 200 | scan=- drift=- | 15:54:46 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 3t | 12 | +11.6% | -41.4% | +75.7% | 5 | 1 | 9 |
| win | 65 | +4.7% | -75.4% | +522.0% | 25 | 16 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 461.5s |
| **Latency** (scan→final max) | 644.8s |
| **Traffic** (notifications 24h) | 95 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 226 | 0.4505 | 0.3009 | +0.1496 | 🟡+33% | 0.2316 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4372 | 0.2557 | 0.2280 | 🔴-0.20 | 0.866 |
| S01_NAKAANA1 | win | 30 | 0.4869 | 0.4333 | 0.2321 | ✅+0.05 | 0.867 |
| S02_TETSUBAN | win | 20 | 0.5127 | 0.5000 | 0.2624 | 🔴-0.05 | 0.975 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 13 | 0.0030 | 0.0769 | 🔴-0.0739 |
| 0.15-0.20 | 7 | 0.1907 | 0.1429 | ✅+0.0479 |
| 0.20-0.30 | 10 | 0.2234 | 0.3000 | 🔴-0.0766 |
| 0.30-0.50 | 106 | 0.4265 | 0.2642 | 🔴+0.1624 |
| 0.50+ | 97 | 0.5405 | 0.3608 | 🔴+0.1797 |

## Settlement Ratio データ品質

- 学習済み: 3バンド / fallback: 14バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 10 | 0.785 |
| win | <5.0 | ✅learned | 24 | 0.735 |
| win | <10.0 | ✅learned | 25 | 0.564 |
| win | <20.0 | ⚠️fallback | 9 | 0.22 |
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
_auto-generated by claude_snapshot.py at 2026-05-14T08:00:02.246453+09:00_