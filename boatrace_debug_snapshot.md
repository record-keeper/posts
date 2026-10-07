# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-07T16:00:01.537187+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-10-07T15:45:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-10-07T15:04:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×58  [2026-10-07T15:02:38]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-07T06:01:32]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-07T06:01:32]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-07T06:01:32]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-07T06:01:32]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-07T06:01:32]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-07T06:01:32]
- key: `DRIFT_BUCKET|drift ≥+30%: n=46 hit%=21.7% ROI=0.66 (コスト 12,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-07T06:01:32]
- key: `ROI_STAT|S00: n=167 hit%=22.8% hit_CI[Bonf]=[14.8,33.3]% ROI=0.60 ROI_boot95=[0.41,0.80]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-07T06:01:32]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=31.3% hit_CI[Bonf]=[22.0,42.4]% ROI=1.02 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-07T06:01:32]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=48.8% hit_CI[Bonf]=[33.5,64.2]% ROI=0.83 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-07T06:01:32]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=40.0% ROI=1.11 (コスト 8,400/回収 9,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-07T06:01:32]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=24.0% ROI=0.66 (コスト 11,800/回収 7,760)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-07T06:01:32]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=87 hit%=29.9% ROI=0.78 (コスト 19,700/回収 15,430)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-07T06:01:32]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=38.6% ROI=0.84 (コスト 10,200/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-07T06:01:32]
- key: `CALIBRATION_LIVE|bt=win: n=413 pred=0.4789 actual=0.3123 error=+0.1665 (+35%) brier=0.2498 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-07T06:01:32]
- key: `CALIBRATION_LIVE|S00(win): n=167 pred=0.4491 hit=0.2275 cal_err=+0.2215 brier=0.2466 BSS=-0.40 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-07T06:01:32]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=166 pred=0.4882 hit=0.3133 cal_err=+0.1749 brier=0.2502 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-07T06:01:32]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=80 pred=0.5216 hit=0.4875 cal_err=+0.0341 brier=0.2555 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.14MB / last modified 2026-10-07T15:59:34.072914+09:00

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
515 [INFO] scraper: odds3f: 20/20 parsed
2026-10-07 15:58:35,627 [INFO] scraper: odds2t: 29/30 parsed
2026-10-07 15:58:35,628 [INFO] scraper: odds2f: 15/15 parsed
2026-10-07 15:58:36,724 [INFO] scraper: odds_win: 6/6 parsed
2026-10-07 15:58:36,724 [INFO] scraper: fetch_race 11/12: boats=6 odds=190/191
2026-10-07 15:58:36,726 [INFO] predictor: CALIBRATION_MODE=on
2026-10-07 15:58:36,727 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-10-07 15:58:36,730 [INFO] run_cycle: fetched 11/12 [scan]: 155 combos
2026-10-07 15:58:36,935 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-07 15:59:05,292 [INFO] run_cycle: === run_cycle 15:59:05 ===
2026-10-07 15:59:05,292 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-07 15:59:05,292 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-07 15:59:05,339 [INFO] predictor: Models loaded OK
2026-10-07 15:59:16,467 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=08&hd=20261007: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-07 15:59:27,842 [INFO] scraper: odds3t: 120/120 parsed
2026-10-07 15:59:28,943 [INFO] scraper: odds3f: 20/20 parsed
2026-10-07 15:59:30,023 [INFO] scraper: odds2t: 30/30 parsed
2026-10-07 15:59:30,024 [INFO] scraper: odds2f: 15/15 parsed
2026-10-07 15:59:31,113 [INFO] scraper: odds_win: 5/6 parsed
2026-10-07 15:59:31,114 [INFO] scraper: fetch_race 08/12: boats=6 odds=190/191
2026-10-07 15:59:31,117 [INFO] predictor: CALIBRATION_MODE=on
2026-10-07 15:59:31,117 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-07 15:59:31,122 [INFO] run_cycle: fetched 08/12 [final]: 155 combos
2026-10-07 15:59:33,665 [WARNING] scraper: beforeinfo parse failed: jcd=24 rno=3
2026-10-07 15:59:33,665 [WARNING] run_cycle: fetch None: 24/3
2026-10-07 15:59:33,665 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 35
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 35
  }
]
```

## Phase別通知記録 (24h)
{'final': 13, 'result': 8, 'scan': 14}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 54
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCRAPER_FAILURE_BURST: 13
  ANOMALY_SCAN_FINAL_RATIO: 12
  CIRCUIT_BREAKER_NO_ACTION: 8
  ANOMALY_BET_VOLUME_DROP: 5
  LARGE_ODDS_DRIFT: 2
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 16 | 13,800 | 12,990 | -810 | 0.941 |
| S01_NAKAANA1 | 44 | 19 | 8,800 | 12,400 | +3,600 | 1.409 |
| S02_TETSUBAN | 14 | 6 | 2,800 | 1,900 | -900 | 0.679 |

## 直近アラート (24h・新しい順)
```
[15:52:24] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 11.6, "final": 4.8, "kind": "LARGE_ODDS_DRIFT", "race": "012R", "scan": 4.3, "sid": "S00"}
[15:52:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.282, "baseline_mean": 0.853, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -4.61}
[15:52:24] ANOMALY_BET_VOLUME_DROP: {"baseline_mean": 12.4, "baseline_n_days": 7, "baseline_stdev": 4.0, "hour": 15, "kind": "ANOMALY_BET_VOLUME_DROP", "today_so_far": 4, "z_score": -2.13}
[15:48:36] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.425, "baseline_mean": 0.853, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.429, "today_scan_count": 7, "z_score": -6.95}
[15:27:20] FINAL_MISSING: {"deadline": "2026-10-07T12:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100716051256", "sid": "S00"}
[15:27:20] FINAL_MISSING: {"deadline": "2026-10-07T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100703071356", "sid": "S00"}
[15:22:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.353, "baseline_mean": 0.853, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -5.78}
[15:12:35] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.52, "baseline_mean": 0.853, "baseline_stdev": 0.061, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.333, "today_scan_count": 6, "z_score": -8.51}
[15:05:57] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:04] FINAL_MISSING: {"deadline": "2026-10-07T11:32:00+09:00", "kind": "FINAL_MISSING", "nid": "2026100710031132", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 49件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 95件 締切済
- 通知発射: scan=7 nid / final=6 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 012R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.3 drift=+11.6% | 15:52:23 |
| S00 | 012R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.3 drift=+11.6% | 15:52:20 |
| S01_NAKAANA1 | 051R | win | 1 | 0.3177 | 3.1 | 0.98 | 200 | scan=- drift=- | 10:39:19 |
| S00 | 111R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=- drift=- | 10:27:19 |
| S01_NAKAANA1 | 204R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=- drift=- | 19:27:18 |
| S01_NAKAANA1 | 202R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=3.3 drift=+0.0% | 18:31:30 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5990 | 3.9 | 2.34 | 200 | scan=3.1 drift=+25.8% | 18:05:19 |
| S01_NAKAANA1 | 0212R | win | 1 | 0.5334 | 3.1 | 1.65 | 200 | scan=3.1 drift=+0.0% | 16:27:19 |
| S02_TETSUBAN | 1312R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.7 drift=-7.4% | 16:22:18 |
| S00 | 1111R | win | 1 | 0.5174 | 17.4 | 9.00 | 300 | scan=- drift=- | 15:30:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 69 | +7.4% | -73.0% | +169.2% | 22 | 9 | 53 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 486.7s |
| **Latency** (scan→final max) | 611.7s |
| **Traffic** (notifications 24h) | 35 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 403 | 0.4791 | 0.3151 | +0.1639 | 🟡+34% | 0.2493 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4501 | 0.2317 | 0.2458 | 🔴-0.38 | 0.599 |
| S01_NAKAANA1 | win | 161 | 0.4886 | 0.3168 | 0.2498 | 🔴-0.15 | 1.001 |
| S02_TETSUBAN | win | 78 | 0.5201 | 0.4872 | 0.2556 | 🔴-0.02 | 0.831 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.30-0.50 | 158 | 0.4206 | 0.2911 | 🔴+0.1294 |
| 0.50+ | 229 | 0.5431 | 0.3362 | 🔴+0.2069 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 170 | 0.767 |
| win | <5.0 | ✅learned | 302 | 0.763 |
| win | <10.0 | ✅learned | 136 | 0.457 |
| win | <20.0 | ✅learned | 38 | 0.243 |
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
_auto-generated by claude_snapshot.py at 2026-10-07T16:00:01.537187+09:00_