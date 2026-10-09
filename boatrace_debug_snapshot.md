# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-10T07:40:02.016944+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×47 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-10T06:00:24]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S00: n=164 hit%=26.8% hit_CI[Bonf]=[18.1,37.8]% ROI=0.70 ROI_boot95=[0.50,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=33.1% hit_CI[Bonf]=[23.5,44.4]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=48.1% hit_CI[Bonf]=[33.1,63.6]% ROI=0.83 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.23 (コスト 8,300/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=29.4% ROI=0.73 (コスト 12,000/回収 8,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=33.0% ROI=0.88 (コスト 19,900/回収 17,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=37.5% ROI=0.81 (コスト 11,300/回収 9,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=23.8% ROI=0.72 (コスト 11,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|bt=win: n=408 pred=0.4820 actual=0.3358 error=+0.1463 (+30%) brier=0.2509 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|S00(win): n=164 pred=0.4538 hit=0.2683 cal_err=+0.1855 brier=0.2527 BSS=-0.29 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=163 pred=0.4907 hit=0.3313 cal_err=+0.1594 brier=0.2456 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=81 pred=0.5218 hit=0.4815 cal_err=+0.0404 brier=0.2578 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=24 pred=0.3207 actual=0.2500 gap=+0.0707`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=132 pred=0.4418 actual=0.3030 gap=+0.1388`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|decile 0.50+: n=237 pred=0.5424 actual=0.3629 gap=+0.1795`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-10-10T06:00:11]
- key: `PAYOUT_RATIO_WEIRD|pid=2713 bet=300 odds=7.8 payout=660 ratio=0.28`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.3MB / last modified 2026-10-10T07:30:03.621107+09:00

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
42 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-09 23:55:04,342 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 23:55:04,388 [INFO] predictor: Models loaded OK
2026-10-09 23:55:04,392 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-09 23:56:04,241 [INFO] run_cycle: === run_cycle 23:56:04 ===
2026-10-09 23:56:04,241 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-09 23:56:04,241 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 23:56:04,289 [INFO] predictor: Models loaded OK
2026-10-09 23:56:04,295 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-09 23:57:04,432 [INFO] run_cycle: === run_cycle 23:57:04 ===
2026-10-09 23:57:04,432 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-09 23:57:04,432 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 23:57:04,476 [INFO] predictor: Models loaded OK
2026-10-09 23:57:04,478 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-09 23:58:04,514 [INFO] run_cycle: === run_cycle 23:58:04 ===
2026-10-09 23:58:04,514 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-09 23:58:04,514 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 23:58:04,562 [INFO] predictor: Models loaded OK
2026-10-09 23:58:04,564 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-09 23:59:03,785 [INFO] run_cycle: === run_cycle 23:59:03 ===
2026-10-09 23:59:03,785 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-09 23:59:03,785 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-09 23:59:03,832 [INFO] predictor: Models loaded OK
2026-10-09 23:59:03,837 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 22, 'result': 10, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 147
  FINAL_MISSING: 47
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 17 | 10,200 | 12,900 | +2,700 | 1.265 |
| S01_NAKAANA1 | 42 | 20 | 8,400 | 12,580 | +4,180 | 1.498 |
| S02_TETSUBAN | 16 | 6 | 3,200 | 1,900 | -1,300 | 0.594 |

## 直近アラート (24h・新しい順)
```
[06:00:07] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:53:04] FINAL_MISSING: {"deadline": "2026-10-09T13:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100923101317", "sid": "S00"}
[23:49:03] FINAL_MISSING: {"deadline": "2026-10-09T15:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100905101515", "sid": "S00"}
[23:49:03] FINAL_MISSING: {"deadline": "2026-10-09T17:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100901051717", "sid": "S00"}
[23:46:04] FINAL_MISSING: {"deadline": "2026-10-09T13:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100905061310", "sid": "S00"}
[23:09:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:02:03] FINAL_MISSING: {"deadline": "2026-10-09T14:28:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100908091428", "sid": "S00"}
[22:52:20] FINAL_MISSING: {"deadline": "2026-10-09T13:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100923101317", "sid": "S00"}
[22:48:04] FINAL_MISSING: {"deadline": "2026-10-09T15:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100905101515", "sid": "S00"}
[22:48:04] FINAL_MISSING: {"deadline": "2026-10-09T17:17:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100901051717", "sid": "S00"}
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
| S02_TETSUBAN | 078R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 18:22:31 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5123 | 3.5 | 1.79 | 200 | scan=- drift=- | 16:45:29 |
| S01_NAKAANA1 | 073R | win | 1 | 0.4989 | 3.9 | 1.95 | 200 | scan=3.9 drift=+0.0% | 16:06:29 |
| S01_NAKAANA1 | 072R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=4.1 drift=-19.5% | 15:40:21 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.7 drift=+13.5% | 15:23:19 |
| S00 | 165R | win | 1 | 0.3177 | 4.9 | 1.56 | 300 | scan=- drift=- | 12:53:19 |
| S00 | 163R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 11:54:29 |
| S00 | 032R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=7.7 drift=-48.1% | 11:38:51 |
| S00 | 162R | win | 1 | 0.5174 | 9.0 | 4.66 | 300 | scan=7.5 drift=+20.0% | 11:26:19 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5719 | 3.2 | 1.83 | 200 | scan=3.6 drift=-11.1% | 11:13:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +1.7% | -68.9% | +159.6% | 22 | 6 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.2s |
| **Latency** (scan→final max) | 646.6s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4820 | 0.3358 | +0.1463 | 🟡+30% | 0.2509 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4538 | 0.2683 | 0.2527 | 🔴-0.29 | 0.698 |
| S01_NAKAANA1 | win | 163 | 0.4907 | 0.3313 | 0.2456 | 🔴-0.11 | 1.028 |
| S02_TETSUBAN | win | 81 | 0.5218 | 0.4815 | 0.2578 | 🔴-0.03 | 0.827 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 156 | 0.4232 | 0.2949 | 🔴+0.1283 |
| 0.50+ | 237 | 0.5424 | 0.3629 | 🔴+0.1795 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 172 | 0.768 |
| win | <5.0 | ✅learned | 312 | 0.762 |
| win | <10.0 | ✅learned | 137 | 0.455 |
| win | <20.0 | ✅learned | 39 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-10T07:40:02.016944+09:00_