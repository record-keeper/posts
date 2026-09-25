# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-25T11:30:01.945230+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×1 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×25 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×16 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×1 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×2  [2026-09-25T11:28:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×5  [2026-09-25T11:25:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-09-25T11:02:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×54  [2026-09-25T11:02:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-09-25T11:02:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-25T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-25T10:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-25T06:00:23]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S00: n=171<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=27.6% ROI=0.90 (コスト 8,200/回収 7,370)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-25T06:00:23]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=30 pred=0.3237 actual=0.2333 gap=+0.0904`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S00: n=171 hit%=22.2% hit_CI[Bonf]=[14.5,32.6]% ROI=0.71 ROI_boot95=[0.47,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S01_NAKAANA1: n=155 hit%=21.9% hit_CI[Bonf]=[13.9,32.8]% ROI=0.65 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-25T06:00:23]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=155<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-25T06:00:23]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=44.9% hit_CI[Bonf]=[29.9,60.8]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=20.5% ROI=0.58 (コスト 9,100/回収 5,280)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=24.7% ROI=0.76 (コスト 20,800/回収 15,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-25T06:00:23]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=25.0% ROI=0.48 (コスト 9,800/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.02MB / last modified 2026-09-25T11:30:04.700384+09:00

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
out=10), retry in 9s
2026-09-25 11:28:39,891 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=3&jcd=13&hd=20260925
2026-09-25 11:28:39,891 [ERROR] scraper: racelist fetch failed: jcd=13 rno=3
2026-09-25 11:28:39,891 [WARNING] run_cycle: fetch None: 13/3
2026-09-25 11:28:40,134 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-25 11:29:04,831 [INFO] run_cycle: === run_cycle 11:29:04 ===
2026-09-25 11:29:04,831 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-25 11:29:04,831 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-25 11:29:04,865 [INFO] predictor: Models loaded OK
2026-09-25 11:29:17,421 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 11:29:18,617 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 11:29:19,807 [INFO] scraper: odds2t: 27/30 parsed
2026-09-25 11:29:19,809 [INFO] scraper: odds2f: 13/15 parsed
2026-09-25 11:29:20,918 [INFO] scraper: odds_win: 5/6 parsed
2026-09-25 11:29:20,918 [INFO] scraper: fetch_race 13/3: boats=6 odds=185/191
2026-09-25 11:29:20,923 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 11:29:20,924 [INFO] predictor: combos: {'win': 5, '2t': 27, '3t': 120}
2026-09-25 11:29:20,930 [INFO] run_cycle: fetched 13/3 [scan]: 152 combos
2026-09-25 11:29:24,523 [INFO] scraper: odds3t: 120/120 parsed
2026-09-25 11:29:25,614 [INFO] scraper: odds3f: 20/20 parsed
2026-09-25 11:29:26,725 [INFO] scraper: odds2t: 30/30 parsed
2026-09-25 11:29:26,726 [INFO] scraper: odds2f: 15/15 parsed
2026-09-25 11:29:27,898 [INFO] scraper: odds_win: 5/6 parsed
2026-09-25 11:29:27,899 [INFO] scraper: fetch_race 05/2: boats=6 odds=190/191
2026-09-25 11:29:27,902 [INFO] predictor: CALIBRATION_MODE=on
2026-09-25 11:29:27,902 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-25 11:29:27,907 [INFO] run_cycle: fetched 05/2 [scan]: 155 combos
2026-09-25 11:29:28,087 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 67
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 67
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 11, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 77
  CIRCUIT_BREAKER_TRIP: 25
  CIRCUIT_BREAKER_NO_ACTION: 19
  STRATEGY_CI_FAIL: 17
  FINAL_MISSING: 16
  ANOMALY_SCAN_FINAL_RATIO: 10
  ANOMALY_BET_VOLUME_DROP: 2
  CRITICAL_ODDS_COLLAPSE: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 4,530 | -5,970 | 0.431 |
| S01_NAKAANA1 | 31 | 7 | 6,200 | 3,220 | -2,980 | 0.519 |
| S02_TETSUBAN | 20 | 10 | 4,000 | 3,540 | -460 | 0.885 |

## 直近アラート (24h・新しい順)
```
[11:29:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1093}
[11:28:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1075}
[11:25:30] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.23, "baseline_mean": 0.855, "baseline_stdev": 0.11, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -2.1}
[11:21:38] FINAL_MISSING: {"deadline": "2026-09-25T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092510040950", "sid": "S00"}
[11:16:36] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[11:14:20] CIRCUIT_BREAKER_TRIP: {"cost": 6200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 3220, "roi_7d": 0.519, "sid": "S01_NAKAANA1"}
[11:10:41] FINAL_MISSING: {"deadline": "2026-09-25T09:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092521030940", "sid": "S00"}
[11:05:13] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4530, "roi_7d": 0.431, "sid": "S00"}
[11:05:13] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.284, "baseline_mean": 0.855, "baseline_stdev": 0.11, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -2.59}
[11:02:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
```

## 本日残レース: 113件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 31件 締切済
- 通知発射: scan=8 nid / final=5 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 051R | win | 1 | 0.5891 | 6.1 | 3.59 | 300 | scan=4.0 drift=+52.5% | 11:04:56 |
| S01_NAKAANA1 | 131R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=3.7 drift=+2.7% | 10:43:19 |
| S00 | 111R | win | 1 | 0.1485 | 4.0 | 0.59 | 300 | scan=10.5 drift=-61.9% | 10:27:21 |
| S00 | 196R | win | 1 | 0.4989 | 5.7 | 2.84 | 300 | scan=6.0 drift=-5.0% | 17:31:18 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5608 | 3.3 | 1.85 | 200 | scan=- drift=- | 15:44:34 |
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.2 | 1.13 | 200 | scan=- drift=- | 15:24:20 |
| S01_NAKAANA1 | 228R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=4.6 drift=-23.9% | 15:12:19 |
| S02_TETSUBAN | 119R | win | 1 | 0.5735 | 2.8 | 1.61 | 200 | scan=2.7 drift=+3.7% | 14:35:21 |
| S00 | 224R | win | 1 | 0.5891 | 8.2 | 4.83 | 300 | scan=14.2 drift=-42.3% | 13:11:27 |
| S00 | 063R | win | 1 | 0.5476 | 4.1 | 2.25 | 300 | scan=- drift=- | 12:16:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | -4.6% | -81.7% | +57.7% | 17 | 9 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.7s |
| **Latency** (scan→final max) | 665.6s |
| **Traffic** (notifications 24h) | 67 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 400 | 0.4768 | 0.2675 | +0.2093 | 🟡+44% | 0.2446 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4442 | 0.2275 | 0.2336 | 🔴-0.33 | 0.708 |
| S01_NAKAANA1 | win | 155 | 0.4861 | 0.2194 | 0.2494 | 🔴-0.46 | 0.651 |
| S02_TETSUBAN | win | 78 | 0.5280 | 0.4487 | 0.2585 | 🔴-0.05 | 0.81 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0760 | 0.2000 | 🔴-0.1240 |
| 0.15-0.20 | 5 | 0.1823 | 0.0000 | 🔴+0.1823 |
| 0.30-0.50 | 150 | 0.4142 | 0.2333 | 🔴+0.1809 |
| 0.50+ | 232 | 0.5438 | 0.2974 | 🔴+0.2464 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 153 | 0.772 |
| win | <5.0 | ✅learned | 265 | 0.757 |
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
_auto-generated by claude_snapshot.py at 2026-09-25T11:30:01.945230+09:00_