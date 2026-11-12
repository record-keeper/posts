# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-12T16:10:01.818079+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×82 (24h)
- 🔴 PSI_DRIFT_DETECTED×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-11-12T16:04:19]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T16:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T15:30:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 9 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×11  [2026-11-12T15:24:52]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 PSI_DRIFT_DETECTED  ×11  [2026-11-12T15:24:52]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×11  [2026-11-12T15:24:52]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T15:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 8 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T14:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 7 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-12T13:00:06]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-12T12:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-11-12T11:12:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=53<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=141<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-12T06:00:27]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S00: n=128 hit%=28.9% hit_CI[Bonf]=[18.9,41.5]% ROI=0.78 ROI_boot95=[0.55,1.04]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-12T06:00:27]
- key: `INSUFFICIENT_SAMPLE|S00: n=128<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S01_NAKAANA1: n=141 hit%=30.5% hit_CI[Bonf]=[20.7,42.5]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-12T06:00:27]
- key: `ROI_STAT|S02_TETSUBAN: n=53 hit%=47.2% hit_CI[Bonf]=[29.1,66.0]% ROI=1.09 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-11-12T06:00:27]
- key: `ORPHAN_SCAN|201 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-12T06:00:27]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=29 hit%=27.6% ROI=0.87 (コスト 6,500/回収 5,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.89MB / last modified 2026-11-12T16:06:07.332808+09:00

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
FO] scraper: odds2t: 30/30 parsed
2026-11-12 16:07:55,341 [INFO] scraper: odds2f: 15/15 parsed
2026-11-12 16:08:06,353 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=3&jcd=07&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 16:08:16,531 [INFO] scraper: odds_win: 6/6 parsed
2026-11-12 16:08:16,531 [INFO] scraper: fetch_race 07/3: boats=6 odds=191/191
2026-11-12 16:08:16,535 [INFO] predictor: CALIBRATION_MODE=on
2026-11-12 16:08:16,535 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-12 16:08:16,539 [INFO] run_cycle: fetched 07/3 [final]: 156 combos
2026-11-12 16:08:27,687 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=09&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 16:08:59,319 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=12&jcd=09&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 16:09:09,453 [INFO] scraper: odds3t: 120/120 parsed
2026-11-12 16:09:18,550 [INFO] scraper: odds3f: 20/20 parsed
2026-11-12 16:09:27,636 [INFO] scraper: odds2t: 30/30 parsed
2026-11-12 16:09:27,637 [INFO] scraper: odds2f: 15/15 parsed
2026-11-12 16:09:38,649 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=12&jcd=09&hd=20261112: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-12 16:09:47,736 [INFO] scraper: odds_win: 6/6 parsed
2026-11-12 16:09:47,736 [INFO] scraper: fetch_race 09/12: boats=6 odds=191/191
2026-11-12 16:09:47,739 [INFO] predictor: CALIBRATION_MODE=on
2026-11-12 16:09:47,739 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-12 16:09:47,743 [INFO] run_cycle: fetched 09/12 [final]: 156 combos

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
    "c": 49
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 49
  }
]
```

## Phase別通知記録 (24h)
{'final': 17, 'result': 13, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 226
  FINAL_MISSING: 82
  PSI_DRIFT_DETECTED: 32
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 11
  ANOMALY_SCAN_FINAL_RATIO: 2
  CRITICAL_ODDS_COLLAPSE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 13 | 3 | 3,900 | 2,760 | -1,140 | 0.708 |
| S01_NAKAANA1 | 18 | 4 | 3,600 | 2,560 | -1,040 | 0.711 |
| S02_TETSUBAN | 8 | 5 | 1,600 | 1,600 | +0 | 1.0 |

## 直近アラート (24h・新しい順)
```
[16:06:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[16:04:17] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 472}
[16:04:17] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 4.1, "baseline_n_days": 7, "baseline_stdev": 1.6, "hour": 16, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 9, "z_score": 3.09}
[15:54:10] FINAL_MISSING: {"deadline": "2026-11-12T09:09:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111210020909", "sid": "S00"}
[15:54:10] FINAL_MISSING: {"deadline": "2026-11-12T14:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111202091423", "sid": "S00"}
[15:54:10] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 468}
[15:50:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 469}
[15:48:09] FINAL_MISSING: {"deadline": "2026-11-12T15:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111222101518", "sid": "S00"}
[15:48:09] FINAL_MISSING: {"deadline": "2026-11-12T12:06:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111202041206", "sid": "S00"}
[15:48:09] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 468}
```

## 本日残レース: 31件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 125件 締切済
- 通知発射: scan=14 nid / final=11 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 8件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 1311R | win | 1 | 0.5334 | 5.6 | 2.99 | 300 | scan=4.8 drift=+16.7% | 15:39:03 |
| S00 | 137R | win | 1 | 0.3177 | 6.0 | 1.91 | 300 | scan=- drift=- | 13:23:36 |
| S00 | 166R | win | 1 | 0.5334 | 10.5 | 5.60 | 300 | scan=24.7 drift=-57.5% | 13:12:51 |
| S01_NAKAANA1 | 109R | win | 1 | 0.5334 | 3.2 | 1.71 | 200 | scan=- drift=- | 12:34:23 |
| S00 | 163R | win | 1 | 0.3177 | 6.3 | 2.00 | 300 | scan=- drift=- | 11:47:45 |
| S01_NAKAANA1 | 236R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=- drift=- | 11:07:17 |
| S00 | 236R | win | 1 | 0.4111 | 4.9 | 2.01 | 300 | scan=12.3 drift=-60.2% | 11:07:15 |
| S01_NAKAANA1 | 106R | win | 1 | 0.5476 | 3.2 | 1.75 | 200 | scan=3.5 drift=-8.6% | 10:58:12 |
| S01_NAKAANA1 | 102R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 09:08:37 |
| S01_NAKAANA1 | 196R | win | 1 | 0.4111 | 3.8 | 1.56 | 200 | scan=4.5 drift=-15.6% | 17:35:35 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 23 | -10.8% | -66.8% | +17.6% | 8 | 5 | 13 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.5s |
| **Latency** (scan→final max) | 635.1s |
| **Traffic** (notifications 24h) | 49 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 318 | 0.4715 | 0.3113 | +0.1601 | 🟡+34% | 0.2303 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 127 | 0.4235 | 0.2756 | 0.2092 | 🔴-0.05 | 0.751 |
| S01_NAKAANA1 | win | 141 | 0.4859 | 0.2908 | 0.2379 | 🔴-0.15 | 0.721 |
| S02_TETSUBAN | win | 50 | 0.5525 | 0.4600 | 0.2625 | 🔴-0.06 | 1.054 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 7 | 0.2290 | 0.1429 | 🔴+0.0862 |
| 0.30-0.50 | 123 | 0.4125 | 0.2927 | 🔴+0.1198 |
| 0.50+ | 176 | 0.5440 | 0.3523 | 🔴+0.1917 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 203 | 0.805 |
| win | <5.0 | ✅learned | 370 | 0.741 |
| win | <10.0 | ✅learned | 158 | 0.45 |
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
_auto-generated by claude_snapshot.py at 2026-11-12T16:10:01.818079+09:00_