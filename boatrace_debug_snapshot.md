# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-22T12:20:01.820559+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×38 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×127 (24h)
- 🔴 PSI_DRIFT_DETECTED×38 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×4  [2026-11-22T12:06:27]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×4  [2026-11-22T12:06:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-22T11:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 11 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×13  [2026-11-22T11:24:28]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-22T11:00:05]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-22T10:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-22T10:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 10 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-22T09:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=40<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-22T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=20.0% ROI=0.83 (コスト 5,400/回収 4,490)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S00: n=83 hit%=25.3% hit_CI[Bonf]=[14.2,40.9]% ROI=0.68 ROI_boot95=[0.41,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=97 hit%=30.9% hit_CI[Bonf]=[19.3,45.5]% ROI=0.79 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-22T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=97<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-22T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=40 hit%=42.5% hit_CI[Bonf]=[23.2,64.4]% ROI=1.18 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-22T06:00:15]
- key: `ORPHAN_SCAN|251 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-22T06:00:15]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=41 hit%=43.9% ROI=1.09 (コスト 9,400/回収 10,290)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|bt=win: n=220 pred=0.4767 actual=0.3091 error=+0.1676 (+35%) brier=0.2334 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|S00(win): n=83 pred=0.4349 hit=0.2530 cal_err=+0.1819 brier=0.2139 BSS=-0.13 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-22T06:00:15]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=97 pred=0.4824 hit=0.3093 cal_err=+0.1731 brier=0.2367 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.43MB / last modified 2026-11-22T12:18:49.715458+09:00

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
SConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-22 12:17:41,254 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=14&hd=20261122
2026-11-22 12:17:41,254 [WARNING] scraper: beforeinfo fetch failed: jcd=14 rno=9
2026-11-22 12:17:41,254 [WARNING] run_cycle: fetch None: 14/9
2026-11-22 12:18:09,823 [INFO] scraper: odds3t: 120/120 parsed
2026-11-22 12:18:19,944 [INFO] scraper: odds3f: 20/20 parsed
2026-11-22 12:18:29,020 [INFO] scraper: odds2t: 29/30 parsed
2026-11-22 12:18:29,021 [INFO] scraper: odds2f: 13/15 parsed
2026-11-22 12:18:40,033 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=05&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-22 12:18:49,304 [INFO] scraper: odds_win: 6/6 parsed
2026-11-22 12:18:49,304 [INFO] scraper: fetch_race 05/5: boats=6 odds=188/191
2026-11-22 12:18:49,307 [INFO] predictor: CALIBRATION_MODE=on
2026-11-22 12:18:49,307 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-11-22 12:18:49,311 [INFO] run_cycle: fetched 05/5 [scan]: 155 combos
2026-11-22 12:18:49,423 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-22 12:19:03,221 [INFO] run_cycle: === run_cycle 12:19:03 ===
2026-11-22 12:19:03,222 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-22 12:19:03,222 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-22 12:19:03,254 [INFO] predictor: Models loaded OK
2026-11-22 12:19:14,368 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=17&hd=20261122: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-22 12:19:43,774 [INFO] scraper: odds3t: 120/120 parsed
2026-11-22 12:19:53,910 [INFO] scraper: odds3f: 20/20 parsed

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 6, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 222
  FINAL_MISSING: 127
  PSI_DRIFT_DETECTED: 38
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 7 | 3 | 2,100 | 1,860 | -240 | 0.886 |
| S01_NAKAANA1 | 16 | 6 | 3,200 | 2,920 | -280 | 0.912 |
| S02_TETSUBAN | 6 | 3 | 1,200 | 2,200 | +1,000 | 1.833 |

## 直近アラート (24h・新しい順)
```
[12:18:49] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 509}
[12:13:44] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 192, "n_recent": 29, "psi": 0.474}
[12:10:11] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:10:11] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 502}
[12:06:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 191, "n_recent": 30, "psi": 0.48}
[12:06:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 506}
[12:02:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 501}
[11:57:13] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 493}
[11:49:23] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 191, "n_recent": 29, "psi": 0.482}
[11:49:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 497}
```

## 本日残レース: 115件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 53件 締切済
- 通知発射: scan=5 nid / final=3 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 024R | win | 1 | 0.5735 | 4.7 | 2.70 | 200 | scan=- drift=- | 12:04:25 |
| S00 | 174R | win | 1 | 0.5123 | 6.1 | 3.13 | 300 | scan=7.5 drift=-18.7% | 11:32:23 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 09:09:14 |
| S00 | 136R | win | 1 | 0.5891 | 4.8 | 2.83 | 300 | scan=- drift=- | 12:57:00 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5735 | 4.3 | 2.47 | 200 | scan=- drift=- | 12:44:23 |
| S01_NAKAANA1 | 045R | win | 1 | 0.3177 | 4.6 | 1.46 | 200 | scan=- drift=- | 12:38:22 |
| S02_TETSUBAN | 135R | win | 1 | 0.5174 | 2.7 | 1.40 | 200 | scan=2.7 drift=+0.0% | 12:29:13 |
| S01_NAKAANA1 | 023R | win | 1 | 0.4111 | 4.3 | 1.77 | 200 | scan=4.1 drift=+4.9% | 11:37:25 |
| S00 | 042R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=- drift=- | 11:17:13 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5891 | 3.1 | 1.83 | 200 | scan=- drift=- | 10:59:24 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | -1.3% | -26.8% | +55.6% | 7 | 0 | 9 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 319.0s |
| **Latency** (scan→final max) | 695.1s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 220 | 0.4775 | 0.3045 | +0.1729 | 🟡+36% | 0.2334 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 83 | 0.4361 | 0.2410 | 0.2129 | 🔴-0.16 | 0.598 |
| S01_NAKAANA1 | win | 96 | 0.4822 | 0.3125 | 0.2366 | 🔴-0.10 | 0.8 |
| S02_TETSUBAN | win | 41 | 0.5501 | 0.4146 | 0.2676 | 🔴-0.10 | 1.154 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 87 | 0.4108 | 0.2759 | 🔴+0.1349 |
| 0.50+ | 124 | 0.5464 | 0.3468 | 🔴+0.1996 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 208 | 0.818 |
| win | <5.0 | ✅learned | 378 | 0.737 |
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
_auto-generated by claude_snapshot.py at 2026-11-22T12:20:01.820559+09:00_