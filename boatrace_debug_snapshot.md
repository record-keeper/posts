# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-02T15:00:02.377601+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×27 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CALIBRATION_DRIFT×27 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 PSI_DRIFT_DETECTED×21 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×5 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-02T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×10  [2026-09-02T14:50:45]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×39  [2026-09-02T14:21:19]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×56  [2026-09-02T14:04:18]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×56  [2026-09-02T14:04:18]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×56  [2026-09-02T14:04:18]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CALIBRATION_DRIFT  ×34  [2026-09-02T13:33:38]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-09-02T12:11:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-09-02T10:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2251 actual=0.2222 gap=+0.0029`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-02T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=8 pred=0.1250 actual=0.0000 gap=+0.1250`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S00: n=176 hit%=26.7% hit_CI[Bonf]=[18.3,37.2]% ROI=0.88 ROI_boot95=[0.62,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=193 hit%=23.3% hit_CI[Bonf]=[15.7,33.1]% ROI=0.71 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-02T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=193<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-02T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=40.7% hit_CI[Bonf]=[26.6,56.6]% ROI=0.70 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-09-02T06:00:17]
- key: `ORPHAN_SCAN|196 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=39 hit%=15.4% ROI=0.47 (コスト 11,300/回収 5,300)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-02T06:00:17]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.91 (コスト 10,000/回収 9,100)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.13MB / last modified 2026-09-02T15:00:04.915472+09:00

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
= run_cycle 14:58:03 ===
2026-09-02 14:58:03,352 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 14:58:03,352 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 14:58:03,399 [INFO] predictor: Models loaded OK
2026-09-02 14:58:16,001 [INFO] scraper: odds3t: 120/120 parsed
2026-09-02 14:58:17,086 [INFO] scraper: odds3f: 20/20 parsed
2026-09-02 14:58:18,334 [INFO] scraper: odds2t: 30/30 parsed
2026-09-02 14:58:18,335 [INFO] scraper: odds2f: 15/15 parsed
2026-09-02 14:58:19,445 [INFO] scraper: odds_win: 3/6 parsed
2026-09-02 14:58:19,445 [INFO] scraper: fetch_race 13/10: boats=6 odds=188/191
2026-09-02 14:58:19,448 [INFO] predictor: CALIBRATION_MODE=on
2026-09-02 14:58:19,448 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-02 14:58:19,452 [INFO] run_cycle: fetched 13/10 [scan]: 153 combos
2026-09-02 14:58:19,573 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-02 14:59:03,418 [INFO] run_cycle: === run_cycle 14:59:03 ===
2026-09-02 14:59:03,419 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-02 14:59:03,419 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-02 14:59:03,466 [INFO] predictor: Models loaded OK
2026-09-02 14:59:14,909 [INFO] scraper: odds3t: 120/120 parsed
2026-09-02 14:59:16,024 [INFO] scraper: odds3f: 20/20 parsed
2026-09-02 14:59:17,134 [INFO] scraper: odds2t: 30/30 parsed
2026-09-02 14:59:17,135 [INFO] scraper: odds2f: 15/15 parsed
2026-09-02 14:59:18,237 [INFO] scraper: odds_win: 6/6 parsed
2026-09-02 14:59:18,237 [INFO] scraper: fetch_race 05/8: boats=6 odds=191/191
2026-09-02 14:59:18,241 [INFO] predictor: CALIBRATION_MODE=on
2026-09-02 14:59:18,242 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-02 14:59:18,246 [INFO] run_cycle: fetched 05/8 [scan]: 156 combos
2026-09-02 14:59:18,524 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 85
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 85
  }
]
```

## Phase別通知記録 (24h)
{'final': 36, 'result': 20, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 122
  CALIBRATION_DRIFT: 27
  CIRCUIT_BREAKER_NO_ACTION: 26
  CIRCUIT_BREAKER_TRIP: 24
  PSI_DRIFT_DETECTED: 21
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 6
  FINAL_MISSING: 5
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 10,710 | -3,390 | 0.76 |
| S01_NAKAANA1 | 39 | 6 | 7,800 | 2,820 | -4,980 | 0.362 |
| S02_TETSUBAN | 19 | 8 | 3,800 | 3,420 | -380 | 0.9 |

## 直近アラート (24h・新しい順)
```
[14:59:18] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1024}
[14:58:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1026}
[14:57:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1057}
[14:56:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1051}
[14:55:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1042}
[14:54:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1044}
[14:53:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 350, "n_recent": 105, "psi": 0.327}
[14:53:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1053}
[14:52:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1049}
[14:51:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1045}
```

## 本日残レース: 75件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 81件 締切済
- 通知発射: scan=11 nid / final=14 nid / result=7 nid
- predictions: 12 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 168R | win | 1 | 0.5891 | 2.4 | 1.41 | 200 | scan=- drift=- | 14:53:19 |
| S00 | 227R | win | 1 | 0.5735 | 4.9 | 2.81 | 300 | scan=4.8 drift=+2.1% | 14:40:43 |
| S01_NAKAANA1 | 057R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 14:29:19 |
| S00 | 066R | win | 1 | 0.5174 | 9.5 | 4.92 | 300 | scan=13.0 drift=-26.9% | 13:42:18 |
| S01_NAKAANA1 | 225R | win | 1 | 0.5012 | 4.1 | 2.05 | 200 | scan=3.9 drift=+5.1% | 13:36:20 |
| S00 | 225R | win | 1 | 0.5012 | 4.1 | 2.05 | 300 | scan=- drift=- | 13:36:19 |
| S00 | 165R | win | 1 | 0.1760 | 10.9 | 1.92 | 300 | scan=- drift=- | 13:22:18 |
| S01_NAKAANA1 | 054R | win | 1 | 0.5719 | 3.3 | 1.89 | 200 | scan=3.0 drift=+10.0% | 12:57:19 |
| S00 | 164R | win | 1 | 0.5891 | 8.5 | 5.01 | 300 | scan=6.2 drift=+37.1% | 12:51:18 |
| S01_NAKAANA1 | 063R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.6 drift=+27.8% | 12:15:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +8.8% | -73.7% | +158.3% | 15 | 9 | 41 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 484.0s |
| **Latency** (scan→final max) | 613.1s |
| **Traffic** (notifications 24h) | 85 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,100円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 452 | 0.4747 | 0.2788 | +0.1960 | 🟡+41% | 0.2402 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 180 | 0.4260 | 0.2667 | 0.2179 | 🔴-0.11 | 0.876 |
| S01_NAKAANA1 | win | 192 | 0.4892 | 0.2396 | 0.2505 | 🔴-0.38 | 0.73 |
| S02_TETSUBAN | win | 80 | 0.5496 | 0.4000 | 0.2655 | 🔴-0.11 | 0.7 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 7 | 0.1233 | 0.0000 | 🔴+0.1233 |
| 0.15-0.20 | 11 | 0.1807 | 0.1818 | ✅-0.0012 |
| 0.20-0.30 | 9 | 0.2251 | 0.2222 | ✅+0.0029 |
| 0.30-0.50 | 154 | 0.4070 | 0.2468 | 🔴+0.1602 |
| 0.50+ | 269 | 0.5460 | 0.3123 | 🔴+0.2337 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 126 | 0.778 |
| win | <5.0 | ✅learned | 230 | 0.743 |
| win | <10.0 | ✅learned | 111 | 0.458 |
| win | <20.0 | ✅learned | 31 | 0.231 |
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
_auto-generated by claude_snapshot.py at 2026-09-02T15:00:02.377601+09:00_