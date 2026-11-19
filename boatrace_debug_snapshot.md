# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-19T11:40:02.025458+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×29 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×114 (24h)
- 🔴 PSI_DRIFT_DETECTED×29 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-19T11:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-11-19T11:10:04]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-11-19T11:04:27]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×9  [2026-11-19T11:04:27]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×9  [2026-11-19T11:04:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_BET_VOLUME_DROP  ×22  [2026-11-19T10:00:17]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-19T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=44<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-19T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2290 actual=0.0000 gap=+0.2290`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-19T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=25 hit%=24.0% ROI=0.86 (コスト 5,500/回収 4,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-19T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3194 actual=0.1154 gap=+0.2040`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-19T06:00:10]
- key: `ROI_STAT|S00: n=96 hit%=22.9% hit_CI[Bonf]=[13.0,37.2]% ROI=0.61 ROI_boot95=[0.36,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-19T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=96<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-19T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=111 hit%=27.0% hit_CI[Bonf]=[16.8,40.5]% ROI=0.69 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-19T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=111<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-19T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=44 hit%=40.9% hit_CI[Bonf]=[22.7,62.0]% ROI=0.98 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-19T06:00:10]
- key: `ORPHAN_SCAN|243 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-19T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=49 hit%=40.8% ROI=0.91 (コスト 11,400/回収 10,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-19T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=25 hit%=20.0% ROI=0.71 (コスト 6,000/回収 4,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-19T06:00:10]
- key: `CALIBRATION_LIVE|bt=win: n=251 pred=0.4743 actual=0.2789 error=+0.1955 (+41%) brier=0.2311 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-19T06:00:10]
- key: `CALIBRATION_LIVE|S00(win): n=96 pred=0.4294 hit=0.2292 cal_err=+0.2003 brier=0.2108 BSS=-0.19 ROI`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.28MB / last modified 2026-11-19T11:38:38.084059+09:00

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
INFO] predictor: combos: {'2t': 30, '3t': 120}
2026-11-19 11:38:36,252 [INFO] run_cycle: fetched 04/3 [scan]: 150 combos
2026-11-19 11:38:36,356 [INFO] run_cycle: run_cycle done: 1 notifications
2026-11-19 11:39:04,952 [INFO] run_cycle: === run_cycle 11:39:04 ===
2026-11-19 11:39:04,952 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-19 11:39:04,952 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-19 11:39:05,037 [INFO] predictor: Models loaded OK
2026-11-19 11:39:16,486 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=09&hd=20261119: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-19 11:39:27,547 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=09&hd=20261119: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-19 11:39:40,636 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=09&hd=20261119: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-19 11:39:40,637 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=4&jcd=09&hd=20261119
2026-11-19 11:39:40,637 [ERROR] scraper: racelist fetch failed: jcd=09 rno=4
2026-11-19 11:39:40,637 [WARNING] run_cycle: fetch None: 09/4
2026-11-19 11:39:51,694 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=14&hd=20261119: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-19 11:40:02,752 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=14&hd=20261119: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s

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
    "c": 23
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 23
  }
]
```

## Phase別通知記録 (24h)
{'final': 5, 'result': 3, 'scan': 15}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 217
  FINAL_MISSING: 114
  PSI_DRIFT_DETECTED: 29
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 12 | 2 | 3,600 | 990 | -2,610 | 0.275 |
| S01_NAKAANA1 | 12 | 4 | 2,400 | 2,260 | -140 | 0.942 |
| S02_TETSUBAN | 9 | 4 | 1,800 | 1,600 | -200 | 0.889 |

## 直近アラート (24h・新しい順)
```
[11:38:36] FINAL_MISSING: {"deadline": "2026-11-19T09:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111914020901", "sid": "S00"}
[11:38:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 492}
[11:31:54] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 215, "n_recent": 33, "psi": 0.606}
[11:31:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 479}
[11:31:54] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.417, "baseline_mean": 0.417, "baseline_stdev": 0.102, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.0, "today_scan_count": 4, "z_score": -4.1}
[11:25:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 472}
[11:23:10] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 216, "n_recent": 33, "psi": 0.602}
[11:23:10] FINAL_MISSING: {"deadline": "2026-11-19T10:51:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111904011051", "sid": "S01_NAKAANA1"}
[11:23:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 470}
[11:20:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 477}
```

## 本日残レース: 89件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 31件 締切済
- 通知発射: scan=4 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 089R | win | 1 | 0.5220 | 3.3 | 1.72 | 200 | scan=3.1 drift=+6.5% | 14:22:25 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 200 | scan=- drift=- | 13:57:35 |
| S00 | 028R | win | 1 | 0.5334 | 4.9 | 2.61 | 300 | scan=5.4 drift=-9.3% | 13:57:34 |
| S02_TETSUBAN | 118R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.9 drift=-10.3% | 13:55:17 |
| S01_NAKAANA1 | 178R | win | 1 | 0.5874 | 3.1 | 1.82 | 200 | scan=- drift=- | 13:17:05 |
| S00 | 131R | win | 1 | 0.5334 | 17.6 | 9.39 | 300 | scan=17.6 drift=+0.0% | 10:42:37 |
| S02_TETSUBAN | 207R | win | 1 | 0.5990 | 2.1 | 1.26 | 200 | scan=- drift=- | 17:54:49 |
| S01_NAKAANA1 | 203R | win | 1 | 0.3177 | 4.5 | 1.43 | 200 | scan=3.2 drift=+40.6% | 16:03:27 |
| S01_NAKAANA1 | 168R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=3.8 drift=-15.8% | 14:17:28 |
| S02_TETSUBAN | 118R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=- drift=- | 13:55:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 16 | +31.3% | -57.5% | +500.0% | 5 | 1 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 331.2s |
| **Latency** (scan→final max) | 500.0s |
| **Traffic** (notifications 24h) | 23 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 248 | 0.4747 | 0.2823 | +0.1924 | 🟡+40% | 0.2314 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 94 | 0.4287 | 0.2340 | 0.2106 | 🔴-0.17 | 0.621 |
| S01_NAKAANA1 | win | 110 | 0.4835 | 0.2727 | 0.2359 | 🔴-0.19 | 0.695 |
| S02_TETSUBAN | win | 44 | 0.5508 | 0.4091 | 0.2649 | 🔴-0.10 | 0.98 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 5 | 0.1918 | 0.0000 | 🔴+0.1918 |
| 0.20-0.30 | 5 | 0.2290 | 0.0000 | 🔴+0.2290 |
| 0.30-0.50 | 96 | 0.4089 | 0.2604 | 🔴+0.1485 |
| 0.50+ | 140 | 0.5449 | 0.3214 | 🔴+0.2234 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 207 | 0.807 |
| win | <5.0 | ✅learned | 374 | 0.741 |
| win | <10.0 | ✅learned | 159 | 0.448 |
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
_auto-generated by claude_snapshot.py at 2026-11-19T11:40:02.025458+09:00_