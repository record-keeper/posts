# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-03T13:50:01.276692+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×24 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×70 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×24 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×2  [2026-10-03T13:48:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-10-03T13:42:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×16  [2026-10-03T13:31:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×41  [2026-10-03T13:04:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×40  [2026-10-03T13:04:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-10-03T13:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×10  [2026-10-03T10:50:42]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_BET_VOLUME_DROP  ×20  [2026-10-03T10:00:11]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-03T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-03T06:00:21]
- key: `ORPHAN_SCAN|188 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.67 (コスト 10,200/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-03T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0730 actual=0.4000 gap=-0.3270`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=31 hit%=35.5% ROI=1.00 (コスト 8,700/回収 8,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=43 hit%=27.9% ROI=0.50 (コスト 9,700/回収 4,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S00: n=163 hit%=20.9% hit_CI[Bonf]=[13.2,31.3]% ROI=0.62 ROI_boot95=[0.40,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=162 hit%=25.9% hit_CI[Bonf]=[17.3,36.9]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-03T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=47.6% hit_CI[Bonf]=[32.6,63.0]% ROI=0.82 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-03T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=91 hit%=27.5% ROI=0.83 (コスト 21,100/回収 17,460)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.84MB / last modified 2026-10-03T13:49:38.633435+09:00

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
3 13:48:38,263 [INFO] run_cycle: fetched 13/8 [scan]: 156 combos
2026-10-03 13:48:38,389 [INFO] run_cycle: run_cycle done: 1 notifications
2026-10-03 13:49:04,075 [INFO] run_cycle: === run_cycle 13:49:04 ===
2026-10-03 13:49:04,075 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-03 13:49:04,075 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-03 13:49:04,122 [INFO] predictor: Models loaded OK
2026-10-03 13:49:15,174 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=7&jcd=16&hd=20261003: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-10-03 13:49:27,583 [INFO] scraper: odds3t: 120/120 parsed
2026-10-03 13:49:28,660 [INFO] scraper: odds3f: 20/20 parsed
2026-10-03 13:49:29,877 [INFO] scraper: odds2t: 30/30 parsed
2026-10-03 13:49:29,878 [INFO] scraper: odds2f: 15/15 parsed
2026-10-03 13:49:30,958 [INFO] scraper: odds_win: 6/6 parsed
2026-10-03 13:49:30,959 [INFO] scraper: fetch_race 16/7: boats=6 odds=191/191
2026-10-03 13:49:30,962 [INFO] predictor: CALIBRATION_MODE=on
2026-10-03 13:49:30,962 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-03 13:49:30,966 [INFO] run_cycle: fetched 16/7 [final]: 156 combos
2026-10-03 13:49:34,577 [INFO] scraper: odds3t: 120/120 parsed
2026-10-03 13:49:35,738 [INFO] scraper: odds3f: 20/20 parsed
2026-10-03 13:49:36,848 [INFO] scraper: odds2t: 30/30 parsed
2026-10-03 13:49:36,849 [INFO] scraper: odds2f: 15/15 parsed
2026-10-03 13:49:37,956 [INFO] scraper: odds_win: 5/6 parsed
2026-10-03 13:49:37,956 [INFO] scraper: fetch_race 02/7: boats=6 odds=190/191
2026-10-03 13:49:37,959 [INFO] predictor: CALIBRATION_MODE=on
2026-10-03 13:49:37,959 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-03 13:49:37,963 [INFO] run_cycle: fetched 02/7 [scan]: 155 combos
2026-10-03 13:49:38,235 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 15, 'scan': 38}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 70
  CIRCUIT_BREAKER_TRIP: 24
  ANOMALY_SCRAPER_FAILURE_BURST: 23
  CIRCUIT_BREAKER_NO_ACTION: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 13
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 47 | 11 | 14,100 | 10,380 | -3,720 | 0.736 |
| S01_NAKAANA1 | 44 | 14 | 8,800 | 9,860 | +1,060 | 1.12 |
| S02_TETSUBAN | 20 | 10 | 4,000 | 2,720 | -1,280 | 0.68 |

## 直近アラート (24h・新しい順)
```
[13:49:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[13:49:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1092}
[13:48:38] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2720, "roi_7d": 0.68, "sid": "S02_TETSUBAN"}
[13:48:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1097}
[13:46:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1073}
[13:45:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1076}
[13:43:23] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1081}
[13:42:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1069}
[13:42:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.127, "baseline_mean": 0.794, "baseline_stdev": 0.058, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.667, "today_scan_count": 18, "z_score": -2.19}
[13:41:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1067}
```

## 本日残レース: 82件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 74件 締切済
- 通知発射: scan=18 nid / final=16 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 167R | win | 1 | 0.4989 | 2.2 | 1.10 | 200 | scan=2.9 drift=-24.1% | 13:48:19 |
| S02_TETSUBAN | 094R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 11:54:26 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.1 drift=+19.4% | 11:33:30 |
| S00 | 093R | win | 1 | 0.2296 | 7.1 | 1.63 | 300 | scan=4.8 drift=+47.9% | 11:25:38 |
| S00 | 042R | win | 1 | 0.5174 | 4.0 | 2.07 | 300 | scan=- drift=- | 11:22:30 |
| S01_NAKAANA1 | 236R | win | 1 | 0.4111 | 4.9 | 2.01 | 200 | scan=3.9 drift=+25.6% | 10:50:21 |
| S00 | 131R | win | 1 | 0.3177 | 10.5 | 3.34 | 300 | scan=6.7 drift=+56.7% | 10:38:31 |
| S01_NAKAANA1 | 235R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=3.6 drift=-13.9% | 10:20:46 |
| S02_TETSUBAN | 078R | win | 1 | 0.5990 | 2.2 | 1.32 | 200 | scan=2.2 drift=+0.0% | 18:37:19 |
| S01_NAKAANA1 | 197R | win | 1 | 0.5174 | 3.4 | 1.76 | 200 | scan=3.1 drift=+9.7% | 18:12:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 74 | +8.3% | -76.2% | +169.2% | 21 | 10 | 53 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 505.9s |
| **Latency** (scan→final max) | 631.9s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 410 | 0.4786 | 0.2854 | +0.1932 | 🟡+40% | 0.2465 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4481 | 0.2073 | 0.2446 | 🔴-0.49 | 0.592 |
| S01_NAKAANA1 | win | 163 | 0.4874 | 0.2699 | 0.2455 | 🔴-0.25 | 0.867 |
| S02_TETSUBAN | win | 83 | 0.5213 | 0.4699 | 0.2523 | 🔴-0.01 | 0.808 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0730 | 0.4000 | 🔴-0.3270 |
| 0.20-0.30 | 5 | 0.2203 | 0.2000 | ✅+0.0203 |
| 0.30-0.50 | 158 | 0.4177 | 0.2468 | 🔴+0.1709 |
| 0.50+ | 236 | 0.5420 | 0.3136 | 🔴+0.2285 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 166 | 0.771 |
| win | <5.0 | ✅learned | 287 | 0.762 |
| win | <10.0 | ✅learned | 132 | 0.46 |
| win | <20.0 | ✅learned | 36 | 0.249 |
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
_auto-generated by claude_snapshot.py at 2026-10-03T13:50:01.276692+09:00_