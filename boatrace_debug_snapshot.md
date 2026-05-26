# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-26T10:50:01.389609+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×113 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-05-26T10:37:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×49  [2026-05-26T10:01:24]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×47  [2026-05-26T10:00:09]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-05-26T10:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=183<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-26T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2243 actual=0.3333 gap=-0.1090`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=32.7% ROI=0.88 (コスト 14,500/回収 12,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S00: n=183 hit%=27.3% hit_CI[Bonf]=[19.0,37.7]% ROI=0.91 ROI_boot95=[0.66,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=81 hit%=27.2% hit_CI[Bonf]=[15.5,43.0]% ROI=0.71 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-26T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=45 hit%=46.7% hit_CI[Bonf]=[27.5,66.9]% ROI=0.86 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-26T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=45<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=25.6% ROI=0.94 (コスト 9,000/回収 8,440)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=65 hit%=27.7% ROI=0.85 (コスト 15,700/回収 13,320)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=27 hit%=25.9% ROI=1.03 (コスト 6,600/回収 6,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-26T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.57 (コスト 9,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|bt=win: n=309 pred=0.4553 actual=0.3010 error=+0.1544 (+34%) brier=0.2311 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-26T06:00:11]
- key: `CALIBRATION_LIVE|S00(win): n=183 pred=0.4284 hit=0.2732 cal_err=+0.1552 brier=0.2196 BSS=-0.11 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.53MB / last modified 2026-05-26T10:49:14.798011+09:00

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
== run_cycle 10:48:06 ===
2026-05-26 10:48:06,033 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 10:48:06,033 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 10:48:06,076 [INFO] predictor: Models loaded OK
2026-05-26 10:48:17,517 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 10:48:18,629 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 10:48:19,881 [INFO] scraper: odds2t: 30/30 parsed
2026-05-26 10:48:19,882 [INFO] scraper: odds2f: 15/15 parsed
2026-05-26 10:48:20,994 [INFO] scraper: odds_win: 4/6 parsed
2026-05-26 10:48:20,994 [INFO] scraper: fetch_race 10/6: boats=6 odds=189/191
2026-05-26 10:48:21,006 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 10:48:21,007 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-05-26 10:48:21,016 [INFO] run_cycle: fetched 10/6 [final]: 154 combos
2026-05-26 10:48:24,521 [INFO] scraper: odds3t: 120/120 parsed
2026-05-26 10:48:25,636 [INFO] scraper: odds3f: 20/20 parsed
2026-05-26 10:48:26,728 [INFO] scraper: odds2t: 30/30 parsed
2026-05-26 10:48:26,729 [INFO] scraper: odds2f: 13/15 parsed
2026-05-26 10:48:27,819 [INFO] scraper: odds_win: 5/6 parsed
2026-05-26 10:48:27,819 [INFO] scraper: fetch_race 17/1: boats=6 odds=188/191
2026-05-26 10:48:27,827 [INFO] predictor: CALIBRATION_MODE=on
2026-05-26 10:48:27,827 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-05-26 10:48:27,835 [INFO] run_cycle: fetched 17/1 [scan]: 155 combos
2026-05-26 10:48:28,026 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-26 10:49:05,206 [INFO] run_cycle: === run_cycle 10:49:05 ===
2026-05-26 10:49:05,206 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-26 10:49:05,206 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-26 10:49:05,281 [INFO] predictor: Models loaded OK
2026-05-26 10:49:05,610 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 36
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 36
  }
]
```

## Phase別通知記録 (24h)
{'final': 14, 'result': 8, 'scan': 14}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 147
  FINAL_MISSING: 113
  ANOMALY_SCAN_FINAL_RATIO: 27
  KS_ODDS_DRIFT: 20
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 11 | 10,800 | 13,320 | +2,520 | 1.233 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 5,080 | -1,720 | 0.747 |
| S02_TETSUBAN | 13 | 6 | 2,600 | 1,980 | -620 | 0.762 |

## 直近アラート (24h・新しい順)
```
[10:37:41] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 673}
[10:36:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 652}
[10:35:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 655}
[10:34:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 647}
[10:32:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 633}
[10:30:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 624}
[10:26:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 625}
[10:24:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 636}
[10:23:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 631}
[10:21:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 649}
```

## 本日残レース: 113件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 19件 締切済
- 通知発射: scan=1 nid / final=2 nid / result=0 nid
- predictions: 1 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 106R | win | 1 | 0.5123 | 5.0 | 2.56 | 300 | scan=- drift=- | 10:47:22 |
| S01_NAKAANA1 | 1210R | win | 1 | 0.5735 | 3.5 | 2.01 | 200 | scan=- drift=- | 19:39:21 |
| S00 | 126R | win | 1 | 0.5123 | 5.6 | 2.87 | 300 | scan=- drift=- | 17:56:33 |
| S01_NAKAANA1 | 039R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=3.0 drift=+3.3% | 14:50:24 |
| S02_TETSUBAN | 056R | win | 1 | 0.5226 | 2.0 | 1.05 | 200 | scan=- drift=- | 14:09:21 |
| S00 | 034R | win | 1 | 0.0295 | 5.9 | 0.17 | 300 | scan=14.2 drift=-58.5% | 12:32:22 |
| S01_NAKAANA1 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=4.1 drift=+17.1% | 11:07:21 |
| S00 | 132R | win | 1 | 0.4111 | 4.8 | 1.97 | 300 | scan=4.1 drift=+17.1% | 11:07:21 |
| S01_NAKAANA1 | 236R | win | 1 | 0.5174 | 3.7 | 1.91 | 200 | scan=- drift=- | 10:43:20 |
| S00 | 102R | win | 1 | 0.0918 | 5.6 | 0.51 | 300 | scan=5.4 drift=+3.7% | 09:02:23 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +1.9% | -78.6% | +157.5% | 19 | 10 | 38 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 507.3s |
| **Latency** (scan→final max) | 644.5s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 308 | 0.4551 | 0.2987 | +0.1564 | 🟡+34% | 0.2311 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4279 | 0.2692 | 0.2195 | 🔴-0.12 | 0.899 |
| S01_NAKAANA1 | win | 81 | 0.4857 | 0.2716 | 0.2446 | 🔴-0.24 | 0.71 |
| S02_TETSUBAN | win | 45 | 0.5101 | 0.4667 | 0.2534 | 🔴-0.02 | 0.858 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 12 | 0.2243 | 0.3333 | 🔴-0.1090 |
| 0.30-0.50 | 136 | 0.4185 | 0.2426 | 🔴+0.1758 |
| 0.50+ | 146 | 0.5402 | 0.3699 | 🔴+0.1703 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 21 | 0.761 |
| win | <5.0 | ✅learned | 38 | 0.802 |
| win | <10.0 | ✅learned | 34 | 0.547 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-26T10:50:01.389609+09:00_