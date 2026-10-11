# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-11T10:40:02.084356+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×38 (24h)
- 🔴 PSI_DRIFT_DETECTED×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×39  [2026-10-11T10:01:09]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×40  [2026-10-11T10:00:16]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-11T06:00:17]
- key: `ORPHAN_SCAN|169 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-11T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S00: n=166 hit%=25.9% hit_CI[Bonf]=[17.4,36.7]% ROI=0.72 ROI_boot95=[0.50,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=34.4% hit_CI[Bonf]=[24.6,45.6]% ROI=1.05 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-11T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=51.3% hit_CI[Bonf]=[35.5,66.9]% ROI=0.91 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=41.4% ROI=1.17 (コスト 8,400/回収 9,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=30.0% ROI=0.74 (コスト 11,800/回収 8,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=34.5% ROI=0.91 (コスト 19,800/回収 18,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=50 hit%=40.0% ROI=1.00 (コスト 11,800/回収 11,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-11T06:00:17]
- key: `DRIFT_BUCKET|drift ≥+30%: n=41 hit%=22.0% ROI=0.67 (コスト 10,800/回収 7,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|bt=win: n=405 pred=0.4826 actual=0.3407 error=+0.1419 (+29%) brier=0.2522 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S00(win): n=166 pred=0.4543 hit=0.2590 cal_err=+0.1952 brier=0.2550 BSS=-0.33 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=163 pred=0.4924 hit=0.3436 cal_err=+0.1488 brier=0.2475 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=76 pred=0.5237 hit=0.5132 cal_err=+0.0106 brier=0.2563 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=25 pred=0.3205 actual=0.2800 gap=+0.0405`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-11T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.40-0.50: n=125 pred=0.4401 actual=0.3120 gap=+0.1281`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.43MB / last modified 2026-10-11T10:39:04.697273+09:00

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
arsed
2026-10-11 10:38:18,765 [INFO] scraper: fetch_race 08/2: boats=6 odds=188/191
2026-10-11 10:38:18,768 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 10:38:18,768 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-11 10:38:18,772 [INFO] run_cycle: fetched 08/2 [scan]: 153 combos
2026-10-11 10:38:22,218 [INFO] scraper: odds3t: 120/120 parsed
2026-10-11 10:38:23,338 [INFO] scraper: odds3f: 20/20 parsed
2026-10-11 10:38:24,456 [INFO] scraper: odds2t: 30/30 parsed
2026-10-11 10:38:24,457 [INFO] scraper: odds2f: 15/15 parsed
2026-10-11 10:38:25,553 [INFO] scraper: odds_win: 6/6 parsed
2026-10-11 10:38:25,553 [INFO] scraper: fetch_race 02/1: boats=6 odds=191/191
2026-10-11 10:38:25,555 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 10:38:25,556 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-11 10:38:25,559 [INFO] run_cycle: fetched 02/1 [scan]: 156 combos
2026-10-11 10:38:28,988 [INFO] scraper: odds3t: 120/120 parsed
2026-10-11 10:38:30,113 [INFO] scraper: odds3f: 20/20 parsed
2026-10-11 10:38:31,229 [INFO] scraper: odds2t: 29/30 parsed
2026-10-11 10:38:31,230 [INFO] scraper: odds2f: 12/15 parsed
2026-10-11 10:38:32,299 [INFO] scraper: odds_win: 4/6 parsed
2026-10-11 10:38:32,300 [INFO] scraper: fetch_race 16/1: boats=6 odds=185/191
2026-10-11 10:38:32,302 [INFO] predictor: CALIBRATION_MODE=on
2026-10-11 10:38:32,302 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-10-11 10:38:32,306 [INFO] run_cycle: fetched 16/1 [scan]: 153 combos
2026-10-11 10:38:32,467 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-11 10:39:04,125 [INFO] run_cycle: === run_cycle 10:39:04 ===
2026-10-11 10:39:04,126 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-11 10:39:04,126 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-11 10:39:04,174 [INFO] predictor: Models loaded OK
2026-10-11 10:39:04,512 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 16, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 130
  FINAL_MISSING: 38
  PSI_DRIFT_DETECTED: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_ODDS_SHIFT: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 15 | 11,100 | 11,490 | +390 | 1.035 |
| S01_NAKAANA1 | 44 | 20 | 8,800 | 10,740 | +1,940 | 1.22 |
| S02_TETSUBAN | 14 | 7 | 2,800 | 2,540 | -260 | 0.907 |

## 直近アラート (24h・新しい順)
```
[10:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:00:12] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 2.2, "baseline_n_days": 5, "baseline_stdev": 0.8, "hour": 10, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 0, "z_score": -2.63}
[09:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:50] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:54:03] FINAL_MISSING: {"deadline": "2026-10-10T15:19:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101001011519", "sid": "S01_NAKAANA1"}
[23:49:03] FINAL_MISSING: {"deadline": "2026-10-10T20:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101001112016", "sid": "S00"}
[23:42:04] FINAL_MISSING: {"deadline": "2026-10-10T17:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101015051708", "sid": "S00"}
[23:26:03] FINAL_MISSING: {"deadline": "2026-10-10T18:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101012091854", "sid": "S00"}
[23:26:03] FINAL_MISSING: {"deadline": "2026-10-10T16:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101001041653", "sid": "S00"}
```

## 本日残レース: 144件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 12件 締切済
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
| S02_TETSUBAN | 076R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 17:41:18 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.7 drift=+0.0% | 16:50:44 |
| S00 | 124R | win | 1 | 0.2290 | 14.9 | 3.41 | 300 | scan=- drift=- | 16:31:30 |
| S00 | 013R | win | 1 | 0.5334 | 4.5 | 2.40 | 300 | scan=4.0 drift=+12.5% | 16:20:22 |
| S02_TETSUBAN | 072R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=2.0 drift=+20.0% | 15:45:20 |
| S01_NAKAANA1 | 152R | win | 1 | 0.5174 | 3.3 | 1.71 | 200 | scan=- drift=- | 15:42:18 |
| S00 | 1610R | win | 1 | 0.5735 | 6.6 | 3.78 | 300 | scan=6.3 drift=+4.8% | 15:33:30 |
| S00 | 036R | win | 1 | 0.3177 | 5.7 | 1.81 | 300 | scan=4.6 drift=+23.9% | 13:26:29 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=4.3 drift=+2.3% | 13:23:19 |
| S00 | 224R | win | 1 | 0.6040 | 4.6 | 2.78 | 300 | scan=9.0 drift=-48.9% | 12:27:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +3.1% | -68.9% | +222.0% | 21 | 7 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.5s |
| **Latency** (scan→final max) | 610.9s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 405 | 0.4826 | 0.3407 | +0.1419 | 🟡+29% | 0.2522 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4543 | 0.2590 | 0.2550 | 🔴-0.33 | 0.716 |
| S01_NAKAANA1 | win | 163 | 0.4924 | 0.3436 | 0.2475 | 🔴-0.10 | 1.051 |
| S02_TETSUBAN | win | 76 | 0.5237 | 0.5132 | 0.2563 | 🔴-0.03 | 0.911 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 150 | 0.4202 | 0.3067 | 🔴+0.1135 |
| 0.50+ | 240 | 0.5429 | 0.3625 | 🔴+0.1804 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 174 | 0.771 |
| win | <5.0 | ✅learned | 315 | 0.759 |
| win | <10.0 | ✅learned | 138 | 0.461 |
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
_auto-generated by claude_snapshot.py at 2026-10-11T10:40:02.084356+09:00_