# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-28T19:10:01.723013+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×113 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×14 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-28T19:00:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🔴 PSI_DRIFT_DETECTED  ×8  [2026-11-28T18:58:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-28T18:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×25  [2026-11-28T18:29:47]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×31  [2026-11-28T18:17:45]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-11-28T18:08:06]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-28T17:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×3  [2026-11-28T16:01:31]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-28T15:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-28T15:00:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-28T12:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-28T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=37<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-28T06:00:06]
- key: `ROI_STAT|S00: n=52 hit%=17.3% hit_CI[Bonf]=[7.1,36.6]% ROI=0.48 ROI_boot95=[0.20,0.82]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-28T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S00: n=52<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-28T06:00:06]
- key: `ROI_STAT|S01_NAKAANA1: n=79 hit%=35.4% hit_CI[Bonf]=[22.0,51.7]% ROI=0.95 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-28T06:00:06]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=79<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-28T06:00:06]
- key: `ROI_STAT|S02_TETSUBAN: n=37 hit%=43.2% hit_CI[Bonf]=[23.2,65.8]% ROI=0.94 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-28T06:00:06]
- key: `ORPHAN_SCAN|288 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-28T06:00:06]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=32 hit%=50.0% ROI=1.39 (コスト 7,000/回収 9,730)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-28T06:00:06]
- key: `CALIBRATION_LIVE|bt=win: n=168 pred=0.4736 actual=0.3155 error=+0.1581 (+33%) brier=0.2335 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.86MB / last modified 2026-11-28T19:09:22.910592+09:00

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
7:14,436 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=15&hd=20261128: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-28 19:07:35,616 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=15&hd=20261128: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-28 19:07:46,645 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=15&hd=20261128: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-28 19:07:59,687 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=15&hd=20261128: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-28 19:07:59,687 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/beforeinfo?rno=9&jcd=15&hd=20261128
2026-11-28 19:07:59,687 [WARNING] scraper: beforeinfo fetch failed: jcd=15 rno=9
2026-11-28 19:07:59,688 [WARNING] run_cycle: fetch None: 15/9
2026-11-28 19:08:18,932 [WARNING] scraper: beforeinfo parse failed: jcd=24 rno=9
2026-11-28 19:08:18,932 [WARNING] run_cycle: fetch None: 24/9
2026-11-28 19:08:18,932 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-28 19:09:03,648 [INFO] run_cycle: === run_cycle 19:09:03 ===
2026-11-28 19:09:03,648 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-28 19:09:03,648 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-28 19:09:03,678 [INFO] predictor: Models loaded OK
2026-11-28 19:09:21,903 [WARNING] scraper: beforeinfo parse failed: jcd=24 rno=9
2026-11-28 19:09:21,903 [WARNING] run_cycle: fetch None: 24/9
2026-11-28 19:09:22,036 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 26
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 26
  }
]
```

## Phase別通知記録 (24h)
{'final': 6, 'result': 6, 'scan': 14}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 260
  FINAL_MISSING: 113
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 14
  PSI_DRIFT_DETECTED: 14
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 13 | 1 | 3,900 | 810 | -3,090 | 0.208 |
| S01_NAKAANA1 | 27 | 10 | 5,400 | 5,560 | +160 | 1.03 |
| S02_TETSUBAN | 11 | 5 | 2,200 | 1,880 | -320 | 0.855 |

## 直近アラート (24h・新しい順)
```
[19:09:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 461}
[19:08:18] FINAL_MISSING: {"deadline": "2026-11-28T11:27:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112806031127", "sid": "S00"}
[19:08:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 10, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 459}
[19:06:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 455}
[19:04:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 460}
[19:02:57] FINAL_MISSING: {"deadline": "2026-11-28T12:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112806051221", "sid": "S00"}
[19:02:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 9, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 462}
[19:00:36] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 463}
[18:59:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 462}
[18:58:38] FINAL_MISSING: {"deadline": "2026-11-28T11:12:00+09:00", "kind": "FINAL_MISSING", "nid": "2026112802021112", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 16件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 152件 締切済
- 通知発射: scan=14 nid / final=6 nid / result=6 nid
- predictions: 6 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 10件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 078R | win | 1 | 0.5735 | 2.0 | 1.15 | 200 | scan=2.1 drift=-4.8% | 18:26:35 |
| S01_NAKAANA1 | 013R | win | 1 | 0.5735 | 4.1 | 2.35 | 200 | scan=3.1 drift=+32.3% | 16:17:39 |
| S01_NAKAANA1 | 073R | win | 1 | 0.4111 | 4.6 | 1.89 | 200 | scan=- drift=- | 16:12:48 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5123 | 4.2 | 2.15 | 200 | scan=3.7 drift=+13.5% | 12:05:13 |
| S01_NAKAANA1 | 148R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.5 drift=+2.9% | 11:54:36 |
| S01_NAKAANA1 | 235R | win | 1 | 0.5123 | 3.7 | 1.90 | 200 | scan=- drift=- | 10:32:00 |
| S01_NAKAANA1 | 246R | win | 1 | 0.5612 | 3.0 | 1.68 | 200 | scan=3.2 drift=-6.2% | 17:45:27 |
| S01_NAKAANA1 | 014R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=- drift=- | 16:43:40 |
| S01_NAKAANA1 | 072R | win | 1 | 0.5735 | 3.6 | 2.06 | 200 | scan=4.3 drift=-16.3% | 15:45:24 |
| S02_TETSUBAN | 039R | win | 1 | 0.5719 | 2.2 | 1.26 | 200 | scan=- drift=- | 14:28:27 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 25 | +10.6% | -58.9% | +114.7% | 6 | 2 | 19 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 339.9s |
| **Latency** (scan→final max) | 452.7s |
| **Traffic** (notifications 24h) | 26 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 166 | 0.4731 | 0.3133 | +0.1599 | 🟡+34% | 0.2310 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 50 | 0.4056 | 0.1600 | 0.1881 | 🔴-0.40 | 0.444 |
| S01_NAKAANA1 | win | 78 | 0.4818 | 0.3590 | 0.2379 | 🔴-0.03 | 0.95 |
| S02_TETSUBAN | win | 38 | 0.5443 | 0.4211 | 0.2732 | 🔴-0.12 | 0.918 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 64 | 0.4068 | 0.2812 | 🔴+0.1256 |
| 0.50+ | 95 | 0.5438 | 0.3579 | 🔴+0.1859 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 213 | 0.817 |
| win | <5.0 | ✅learned | 389 | 0.738 |
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
_auto-generated by claude_snapshot.py at 2026-11-28T19:10:01.723013+09:00_