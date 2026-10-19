# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-19T14:30:01.278413+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×70 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×3 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-10-19T14:05:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×41  [2026-10-19T13:49:04]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×37  [2026-10-19T12:27:54]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×18  [2026-10-19T11:09:53]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_DROP  ×57  [2026-10-19T10:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-10-19T09:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-19T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-19T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-19T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=177<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-19T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2287 actual=0.3333 gap=-0.1046`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-19T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-19T06:00:06]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1845 actual=0.0000 gap=+0.1845`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-19T06:00:06]
- key: `ROI_STAT|S00: n=179 hit%=27.9% hit_CI[Bonf]=[19.4,38.4]% ROI=0.76 ROI_boot95=[0.55,0.99]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-19T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=177 hit%=35.6% hit_CI[Bonf]=[26.1,46.4]% ROI=0.99 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-19T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=51.2% hit_CI[Bonf]=[36.1,66.1]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-19T06:00:06]
- key: `ORPHAN_SCAN|153 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-19T06:00:06]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=41.9% ROI=1.08 (コスト 8,900/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-19T06:00:06]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=50 hit%=34.0% ROI=0.77 (コスト 11,700/回収 8,980)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-19T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=85 hit%=42.4% ROI=1.21 (コスト 19,200/回収 23,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-19T06:00:06]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=63 hit%=31.7% ROI=0.81 (コスト 15,100/回収 12,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.21MB / last modified 2026-10-19T14:30:03.420117+09:00

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
-19 14:26:44,051 [INFO] run_cycle: fetched 10/12 [final]: 156 combos
2026-10-19 14:26:44,247 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 14:27:03,481 [INFO] run_cycle: === run_cycle 14:27:03 ===
2026-10-19 14:27:03,481 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 14:27:03,481 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 14:27:03,524 [INFO] predictor: Models loaded OK
2026-10-19 14:27:03,633 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 14:28:03,313 [INFO] run_cycle: === run_cycle 14:28:03 ===
2026-10-19 14:28:03,313 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 14:28:03,313 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 14:28:03,340 [INFO] predictor: Models loaded OK
2026-10-19 14:28:15,822 [INFO] scraper: odds3t: 120/120 parsed
2026-10-19 14:28:16,932 [INFO] scraper: odds3f: 20/20 parsed
2026-10-19 14:28:18,037 [INFO] scraper: odds2t: 30/30 parsed
2026-10-19 14:28:18,039 [INFO] scraper: odds2f: 13/15 parsed
2026-10-19 14:28:19,235 [INFO] scraper: odds_win: 4/6 parsed
2026-10-19 14:28:19,235 [INFO] scraper: fetch_race 09/9: boats=6 odds=187/191
2026-10-19 14:28:19,238 [INFO] predictor: CALIBRATION_MODE=on
2026-10-19 14:28:19,238 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-19 14:28:19,242 [INFO] run_cycle: fetched 09/9 [scan]: 154 combos
2026-10-19 14:28:19,341 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-19 14:29:03,843 [INFO] run_cycle: === run_cycle 14:29:03 ===
2026-10-19 14:29:03,843 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-19 14:29:03,843 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-19 14:29:03,871 [INFO] predictor: Models loaded OK
2026-10-19 14:29:03,951 [INFO] run_cycle: run_cycle done: 0 notifications

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
{'final': 21, 'result': 13, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 93
  FINAL_MISSING: 70
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 15
  PSI_DRIFT_DETECTED: 3
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 48 | 17 | 14,400 | 13,560 | -840 | 0.942 |
| S01_NAKAANA1 | 43 | 16 | 8,600 | 7,720 | -880 | 0.898 |
| S02_TETSUBAN | 17 | 10 | 3,400 | 3,940 | +540 | 1.159 |

## 直近アラート (24h・新しい順)
```
[14:24:38] FINAL_MISSING: {"deadline": "2026-10-19T13:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101916071354", "sid": "S00"}
[14:19:25] FINAL_MISSING: {"deadline": "2026-10-19T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101902011047", "sid": "S00"}
[14:16:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.186, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.7, "today_scan_count": 10, "z_score": -2.61}
[14:09:34] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.286, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.6, "today_scan_count": 10, "z_score": -4.02}
[14:05:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:58:26] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": 166.7, "final": 12.0, "kind": "LARGE_ODDS_DRIFT", "race": "098R", "scan": 4.5, "sid": "S00"}
[13:58:26] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.22, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 9, "z_score": -3.08}
[13:51:27] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.331, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.556, "today_scan_count": 9, "z_score": -4.64}
[13:44:49] FINAL_MISSING: {"deadline": "2026-10-19T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026101902061314", "sid": "S00"}
[13:41:39] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.261, "baseline_mean": 0.886, "baseline_stdev": 0.071, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -3.67}
```

## 本日残レース: 59件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 73件 締切済
- 通知発射: scan=10 nid / final=10 nid / result=8 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 089R | win | 1 | 0.5334 | 3.3 | 1.76 | 200 | scan=3.3 drift=+0.0% | 14:16:19 |
| S00 | 098R | win | 1 | 0.4111 | 12.0 | 4.93 | 300 | scan=4.5 drift=+166.7% | 13:58:18 |
| S01_NAKAANA1 | 166R | win | 1 | 0.4926 | 4.1 | 2.02 | 200 | scan=- drift=- | 13:22:19 |
| S01_NAKAANA1 | 096R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.3 drift=-9.1% | 12:55:19 |
| S00 | 024R | win | 1 | 0.5735 | 20.1 | 11.53 | 300 | scan=19.5 drift=+3.1% | 12:11:19 |
| S02_TETSUBAN | 033R | win | 1 | 0.5990 | 2.6 | 1.56 | 200 | scan=- drift=- | 12:05:31 |
| S00 | 093R | win | 1 | 0.4989 | 4.5 | 2.25 | 300 | scan=- drift=- | 11:27:29 |
| S02_TETSUBAN | 162R | win | 1 | 0.5174 | 2.0 | 1.03 | 200 | scan=2.0 drift=+0.0% | 11:24:18 |
| S00 | 083R | win | 1 | 0.1760 | 30.7 | 5.40 | 300 | scan=- drift=- | 11:09:43 |
| S01_NAKAANA1 | 092R | win | 1 | 0.5109 | 3.5 | 1.79 | 200 | scan=3.7 drift=-5.4% | 10:58:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 68 | +24.5% | -52.2% | +495.8% | 13 | 5 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 393.3s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 437 | 0.4794 | 0.3593 | +0.1201 | 🟡+25% | 0.2447 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 178 | 0.4409 | 0.2809 | 0.2375 | 🔴-0.18 | 0.763 |
| S01_NAKAANA1 | win | 176 | 0.4929 | 0.3636 | 0.2456 | 🔴-0.06 | 1.011 |
| S02_TETSUBAN | win | 83 | 0.5334 | 0.5181 | 0.2581 | 🔴-0.03 | 0.917 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 6 | 0.2287 | 0.3333 | 🔴-0.1046 |
| 0.30-0.50 | 157 | 0.4182 | 0.3312 | 🔴+0.0870 |
| 0.50+ | 258 | 0.5437 | 0.3876 | 🔴+0.1561 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 188 | 0.778 |
| win | <5.0 | ✅learned | 339 | 0.749 |
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
_auto-generated by claude_snapshot.py at 2026-10-19T14:30:01.278413+09:00_