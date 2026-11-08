# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-08T13:00:02.218845+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×35 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×65 (24h)
- 🔴 PSI_DRIFT_DETECTED×35 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×7  [2026-11-08T12:33:13]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-08T12:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×13  [2026-11-08T12:07:37]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×13  [2026-11-08T12:07:37]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-08T12:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-08T11:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-08T11:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×19  [2026-11-08T10:01:38]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-08T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-08T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-08T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-08T06:00:15]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.50 (コスト 9,600/回収 4,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-08T06:00:15]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=29 pred=0.3219 actual=0.1379 gap=+0.1840`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-08T06:00:15]
- key: `ROI_STAT|S00: n=148 hit%=25.7% hit_CI[Bonf]=[16.8,37.1]% ROI=0.71 ROI_boot95=[0.49,0.95]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-08T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S00: n=148<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-08T06:00:15]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=32.9% hit_CI[Bonf]=[23.1,44.4]% ROI=0.78 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-08T06:00:15]
- key: `ROI_STAT|S02_TETSUBAN: n=59 hit%=47.5% hit_CI[Bonf]=[30.2,65.3]% ROI=1.07 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-08T06:00:15]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=59<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-08T06:00:15]
- key: `ORPHAN_SCAN|184 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-08T06:00:15]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=31 hit%=35.5% ROI=0.98 (コスト 7,000/回収 6,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.66MB / last modified 2026-11-08T12:55:24.875089+09:00

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
:58:16,686 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=7&jcd=08&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-08 12:58:25,823 [INFO] scraper: odds3t: 120/120 parsed
2026-11-08 12:58:36,835 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=7&jcd=08&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-08 12:58:46,069 [INFO] scraper: odds3f: 20/20 parsed
2026-11-08 12:58:57,081 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=7&jcd=08&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-08 12:59:08,124 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=7&jcd=08&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-08 12:59:19,288 [INFO] scraper: odds2t: 29/30 parsed
2026-11-08 12:59:19,289 [INFO] scraper: odds2f: 15/15 parsed
2026-11-08 12:59:30,301 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=7&jcd=08&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-08 12:59:40,431 [INFO] scraper: odds_win: 5/6 parsed
2026-11-08 12:59:40,431 [INFO] scraper: fetch_race 08/7: boats=6 odds=189/191
2026-11-08 12:59:40,433 [INFO] predictor: CALIBRATION_MODE=on
2026-11-08 12:59:40,433 [INFO] predictor: combos: {'win': 5, '2t': 29, '3t': 120}
2026-11-08 12:59:40,437 [INFO] run_cycle: fetched 08/7 [scan]: 154 combos
2026-11-08 13:00:01,713 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=6&jcd=14&hd=20261108: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s

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
{'final': 13, 'result': 6, 'scan': 17}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 261
  FINAL_MISSING: 65
  PSI_DRIFT_DETECTED: 35
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 7 | 1 | 2,100 | 540 | -1,560 | 0.257 |
| S01_NAKAANA1 | 17 | 9 | 3,400 | 5,020 | +1,620 | 1.476 |
| S02_TETSUBAN | 10 | 2 | 2,000 | 420 | -1,580 | 0.21 |

## 直近アラート (24h・新しい順)
```
[12:55:24] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 325, "n_recent": 34, "psi": 1.132}
[12:55:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[12:50:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 485}
[12:43:45] FINAL_MISSING: {"deadline": "2026-11-08T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026110802021112", "sid": "S01_NAKAANA1"}
[12:43:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 494}
[12:40:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 492}
[12:37:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 498}
[12:33:12] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 499}
[12:28:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 504}
[12:21:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 502}
```

## 本日残レース: 79件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 53件 締切済
- 通知発射: scan=6 nid / final=4 nid / result=2 nid
- predictions: 2 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 083R | win | 1 | 0.3177 | 7.2 | 2.29 | 300 | scan=21.7 drift=-66.8% | 11:08:23 |
| S00 | 112R | win | 1 | 0.3177 | 8.5 | 2.70 | 300 | scan=- drift=- | 10:53:11 |
| S02_TETSUBAN | 0511R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.2 drift=+0.0% | 15:22:38 |
| S01_NAKAANA1 | 039R | win | 1 | 0.5891 | 4.3 | 2.53 | 200 | scan=- drift=- | 14:28:13 |
| S01_NAKAANA1 | 029R | win | 1 | 0.5735 | 4.5 | 2.58 | 200 | scan=4.5 drift=+0.0% | 14:25:12 |
| S00 | 029R | win | 1 | 0.5735 | 4.5 | 2.58 | 300 | scan=4.5 drift=+0.0% | 14:25:03 |
| S00 | 113R | win | 1 | 0.5174 | 7.6 | 3.93 | 300 | scan=6.8 drift=+11.8% | 11:22:13 |
| S02_TETSUBAN | 111R | win | 1 | 0.5719 | 2.6 | 1.49 | 200 | scan=2.3 drift=+13.0% | 10:26:11 |
| S01_NAKAANA1 | 014R | win | 1 | 0.5735 | 3.8 | 2.18 | 200 | scan=3.4 drift=+11.8% | 16:33:25 |
| S01_NAKAANA1 | 153R | win | 1 | 0.5174 | 4.5 | 2.33 | 200 | scan=- drift=- | 16:11:12 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 18 | -4.5% | -66.8% | +25.0% | 5 | 1 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 367.2s |
| **Latency** (scan→final max) | 621.6s |
| **Traffic** (notifications 24h) | 36 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 359 | 0.4761 | 0.3203 | +0.1558 | 🟡+33% | 0.2313 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 146 | 0.4325 | 0.2534 | 0.2136 | 🔴-0.13 | 0.701 |
| S01_NAKAANA1 | win | 154 | 0.4875 | 0.3247 | 0.2377 | 🔴-0.08 | 0.771 |
| S02_TETSUBAN | win | 59 | 0.5542 | 0.4746 | 0.2582 | 🔴-0.04 | 1.073 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 132 | 0.4127 | 0.2879 | 🔴+0.1248 |
| 0.50+ | 206 | 0.5460 | 0.3689 | 🔴+0.1770 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 199 | 0.807 |
| win | <5.0 | ✅learned | 369 | 0.742 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-11-08T13:00:02.218845+09:00_