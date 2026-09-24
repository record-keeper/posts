# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-24T16:10:01.895629+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×22 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×30 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×22 (24h)
- 🔴 PSI_DRIFT_DETECTED×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×3  [2026-09-24T16:07:34]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-24T16:07:34]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×3  [2026-09-24T16:07:34]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-09-24T15:30:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×14  [2026-09-24T14:32:38]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-09-24T14:00:07]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×16  [2026-09-24T12:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-09-24T10:53:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 PSI_DRIFT_DETECTED  ×55  [2026-09-24T10:02:14]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-24T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-24T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-24T06:00:31]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-24T06:00:31]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=157<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-24T06:00:31]
- key: `DRIFT_BUCKET|drift ≥+30%: n=39 hit%=12.8% ROI=0.47 (コスト 10,700/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-24T06:00:31]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-24T06:00:31]
- key: `ROI_STAT|S00: n=169 hit%=22.5% hit_CI[Bonf]=[14.6,32.9]% ROI=0.72 ROI_boot95=[0.48,1.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-24T06:00:31]
- key: `ROI_STAT|S01_NAKAANA1: n=157 hit%=21.0% hit_CI[Bonf]=[13.2,31.7]% ROI=0.63 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-24T06:00:31]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=42.9% hit_CI[Bonf]=[28.1,59.0]% ROI=0.77 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-24T06:00:31]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=27.6% ROI=0.90 (コスト 8,200/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-24T06:00:31]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=17.9% ROI=0.55 (コスト 9,100/回収 4,980)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.98MB / last modified 2026-09-24T16:09:19.282683+09:00

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
n_cycle 16:08:03 ===
2026-09-24 16:08:03,558 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-24 16:08:03,558 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-24 16:08:03,603 [INFO] predictor: Models loaded OK
2026-09-24 16:08:15,331 [INFO] scraper: odds3t: 120/120 parsed
2026-09-24 16:08:16,420 [INFO] scraper: odds3f: 20/20 parsed
2026-09-24 16:08:17,547 [INFO] scraper: odds2t: 30/30 parsed
2026-09-24 16:08:17,548 [INFO] scraper: odds2f: 15/15 parsed
2026-09-24 16:08:18,637 [INFO] scraper: odds_win: 5/6 parsed
2026-09-24 16:08:18,637 [INFO] scraper: fetch_race 11/12: boats=6 odds=190/191
2026-09-24 16:08:18,641 [INFO] predictor: CALIBRATION_MODE=on
2026-09-24 16:08:18,641 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-24 16:08:18,645 [INFO] run_cycle: fetched 11/12 [final]: 155 combos
2026-09-24 16:08:19,059 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-24 16:09:03,455 [INFO] run_cycle: === run_cycle 16:09:03 ===
2026-09-24 16:09:03,455 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-24 16:09:03,455 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-24 16:09:03,504 [INFO] predictor: Models loaded OK
2026-09-24 16:09:15,135 [INFO] scraper: odds3t: 120/120 parsed
2026-09-24 16:09:16,240 [INFO] scraper: odds3f: 20/20 parsed
2026-09-24 16:09:17,484 [INFO] scraper: odds2t: 30/30 parsed
2026-09-24 16:09:17,485 [INFO] scraper: odds2f: 15/15 parsed
2026-09-24 16:09:18,589 [INFO] scraper: odds_win: 5/6 parsed
2026-09-24 16:09:18,589 [INFO] scraper: fetch_race 11/12: boats=6 odds=190/191
2026-09-24 16:09:18,592 [INFO] predictor: CALIBRATION_MODE=on
2026-09-24 16:09:18,592 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-24 16:09:18,596 [INFO] run_cycle: fetched 11/12 [final]: 155 combos
2026-09-24 16:09:18,980 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 13, 'scan': 20}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 101
  FINAL_MISSING: 30
  CIRCUIT_BREAKER_TRIP: 22
  PSI_DRIFT_DETECTED: 22
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  ANOMALY_SCAN_FINAL_RATIO: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 6 | 10,200 | 4,050 | -6,150 | 0.397 |
| S01_NAKAANA1 | 33 | 9 | 6,600 | 5,160 | -1,440 | 0.782 |
| S02_TETSUBAN | 21 | 11 | 4,200 | 3,740 | -460 | 0.89 |

## 直近アラート (24h・新しい順)
```
[16:05:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:05:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:31:28] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 4050, "roi_7d": 0.397, "sid": "S00"}
[15:12:23] LARGE_ODDS_DRIFT: {"combo": "1", "drift_pct": -23.9, "final": 3.5, "kind": "LARGE_ODDS_DRIFT", "race": "228R", "scan": 4.6, "sid": "S01_NAKAANA1"}
[15:12:23] FINAL_MISSING: {"deadline": "2026-09-24T09:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092421030940", "sid": "S00"}
[15:05:15] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:05:15] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:45:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1059}
[14:44:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1038}
[14:43:32] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1030}
```

## 本日残レース: 37件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 119件 締切済
- 通知発射: scan=17 nid / final=19 nid / result=9 nid
- predictions: 10 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 012R | win | 1 | 0.5608 | 3.3 | 1.85 | 200 | scan=- drift=- | 15:44:34 |
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=- drift=- | 15:24:20 |
| S01_NAKAANA1 | 228R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.6 drift=-23.9% | 15:12:19 |
| S02_TETSUBAN | 119R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=2.7 drift=+3.7% | 14:35:21 |
| S00 | 224R | win | 1 | 0.5891 | 8.2 | 4.83 | 300 | scan=14.2 drift=-42.3% | 13:11:27 |
| S00 | 063R | win | 1 | 0.5476 | 4.1 | 2.25 | 300 | scan=- drift=- | 12:16:18 |
| S00 | 084R | win | 1 | 0.4111 | 11.2 | 4.60 | 300 | scan=- drift=- | 12:04:20 |
| S00 | 092R | win | 1 | 0.1720 | 13.5 | 2.32 | 300 | scan=9.0 drift=+50.0% | 10:57:19 |
| S00 | 112R | win | 1 | 0.5334 | 4.5 | 2.40 | 300 | scan=5.0 drift=-10.0% | 10:55:31 |
| S02_TETSUBAN | 213R | win | 1 | 0.5990 | 2.8 | 1.68 | 200 | scan=- drift=- | 09:37:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | -4.6% | -81.7% | +57.7% | 17 | 8 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.1s |
| **Latency** (scan→final max) | 665.6s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 403 | 0.4764 | 0.2655 | +0.2109 | 🟡+44% | 0.2428 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 170 | 0.4435 | 0.2235 | 0.2291 | 🔴-0.32 | 0.716 |
| S01_NAKAANA1 | win | 154 | 0.4860 | 0.2208 | 0.2494 | 🔴-0.45 | 0.655 |
| S02_TETSUBAN | win | 79 | 0.5284 | 0.4430 | 0.2593 | 🔴-0.05 | 0.8 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.15-0.20 | 5 | 0.1823 | 0.0000 | 🔴+0.1823 |
| 0.30-0.50 | 153 | 0.4136 | 0.2353 | 🔴+0.1783 |
| 0.50+ | 232 | 0.5441 | 0.2974 | 🔴+0.2467 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 153 | 0.772 |
| win | <5.0 | ✅learned | 264 | 0.758 |
| win | <10.0 | ✅learned | 126 | 0.46 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-24T16:10:01.895629+09:00_