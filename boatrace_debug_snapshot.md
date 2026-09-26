# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-26T12:10:01.632381+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×41 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×74 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×41 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×14  [2026-09-26T12:03:12]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×14  [2026-09-26T12:03:12]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×7  [2026-09-26T12:03:12]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-26T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-26T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-09-26T11:51:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×15  [2026-09-26T11:13:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=80<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S00: n=169<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-26T06:00:21]
- key: `ORPHAN_SCAN|162 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-26T06:00:21]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=154<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-26T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0760 actual=0.2000 gap=-0.1240`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-26T06:00:21]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=31 pred=0.3235 actual=0.2258 gap=+0.0977`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S00: n=169 hit%=22.5% hit_CI[Bonf]=[14.6,32.9]% ROI=0.69 ROI_boot95=[0.46,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S01_NAKAANA1: n=154 hit%=22.7% hit_CI[Bonf]=[14.5,33.7]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-26T06:00:21]
- key: `ROI_STAT|S02_TETSUBAN: n=80 hit%=45.0% hit_CI[Bonf]=[30.2,60.8]% ROI=0.83 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=30.0% ROI=0.92 (コスト 8,500/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=39 hit%=25.6% ROI=0.71 (コスト 8,800/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=89 hit%=23.6% ROI=0.71 (コスト 20,600/回収 14,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-26T06:00:21]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=40 hit%=27.5% ROI=0.52 (コスト 9,000/回収 4,680)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.16MB / last modified 2026-09-26T12:09:45.029944+09:00

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
&hd=20260926: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-26 12:09:27,374 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:09:28,455 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:09:29,601 [INFO] scraper: odds2t: 30/30 parsed
2026-09-26 12:09:29,602 [INFO] scraper: odds2f: 15/15 parsed
2026-09-26 12:09:30,722 [INFO] scraper: odds_win: 5/6 parsed
2026-09-26 12:09:30,722 [INFO] scraper: fetch_race 22/2: boats=6 odds=190/191
2026-09-26 12:09:30,726 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:09:30,726 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-26 12:09:30,730 [INFO] run_cycle: fetched 22/2 [final]: 155 combos
2026-09-26 12:09:34,442 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:09:35,545 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:09:36,654 [INFO] scraper: odds2t: 30/30 parsed
2026-09-26 12:09:36,655 [INFO] scraper: odds2f: 14/15 parsed
2026-09-26 12:09:37,747 [INFO] scraper: odds_win: 4/6 parsed
2026-09-26 12:09:37,747 [INFO] scraper: fetch_race 11/5: boats=6 odds=188/191
2026-09-26 12:09:37,750 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:09:37,750 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-26 12:09:37,754 [INFO] run_cycle: fetched 11/5 [scan]: 154 combos
2026-09-26 12:09:41,344 [INFO] scraper: odds3t: 120/120 parsed
2026-09-26 12:09:42,462 [INFO] scraper: odds3f: 20/20 parsed
2026-09-26 12:09:43,593 [INFO] scraper: odds2t: 22/30 parsed
2026-09-26 12:09:43,595 [INFO] scraper: odds2f: 15/15 parsed
2026-09-26 12:09:44,670 [INFO] scraper: odds_win: 2/6 parsed
2026-09-26 12:09:44,671 [INFO] scraper: fetch_race 13/5: boats=6 odds=179/191
2026-09-26 12:09:44,673 [INFO] predictor: CALIBRATION_MODE=on
2026-09-26 12:09:44,673 [INFO] predictor: combos: {'win': 2, '2t': 22, '3t': 120}
2026-09-26 12:09:44,676 [INFO] run_cycle: fetched 13/5 [scan]: 144 combos
2026-09-26 12:09:44,814 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 87
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 87
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 18, 'scan': 34}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 133
  FINAL_MISSING: 74
  CIRCUIT_BREAKER_TRIP: 41
  CIRCUIT_BREAKER_NO_ACTION: 35
  ANOMALY_BET_VOLUME_SPIKE: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  LARGE_ODDS_DRIFT: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 35 | 7 | 10,500 | 4,890 | -5,610 | 0.466 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,740 | -2,260 | 0.677 |
| S02_TETSUBAN | 22 | 12 | 4,400 | 4,700 | +300 | 1.068 |

## 直近アラート (24h・新しい順)
```
[12:04:32] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4740, "roi_7d": 0.677, "sid": "S01_NAKAANA1"}
[12:03:10] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4890, "roi_7d": 0.466, "sid": "S00"}
[12:03:10] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.248, "baseline_mean": 0.864, "baseline_stdev": 0.1, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.615, "today_scan_count": 13, "z_score": -2.49}
[12:01:55] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:01:55] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:01:55] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[11:59:19] FINAL_MISSING: {"deadline": "2026-09-26T11:29:00+09:00", "kind": "FINAL_MISSING", "nid": "2026092609031129", "sid": "S00"}
[11:54:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1267}
[11:53:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1280}
[11:52:45] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1278}
```

## 本日残レース: 114件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 42件 締切済
- 通知発射: scan=13 nid / final=11 nid / result=3 nid
- predictions: 5 / うち結果DB記録済: 3
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 218R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.7 drift=+0.0% | 12:04:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=3.0 drift=+23.3% | 11:46:30 |
| S00 | 083R | win | 1 | 0.5334 | 4.1 | 2.19 | 300 | scan=10.5 drift=-61.0% | 11:30:22 |
| S01_NAKAANA1 | 092R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=- drift=- | 10:59:30 |
| S02_TETSUBAN | 213R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=2.6 drift=-15.4% | 09:33:21 |
| S01_NAKAANA1 | 196R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=- drift=- | 17:32:33 |
| S02_TETSUBAN | 204R | win | 1 | 0.4989 | 2.1 | 1.05 | 200 | scan=- drift=- | 16:22:20 |
| S00 | 192R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=- drift=- | 15:40:21 |
| S02_TETSUBAN | 201R | win | 1 | 0.4989 | 2.4 | 1.20 | 200 | scan=2.8 drift=-14.3% | 14:55:20 |
| S02_TETSUBAN | 139R | win | 1 | 0.5174 | 2.1 | 1.09 | 200 | scan=2.4 drift=-12.5% | 14:32:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 56 | -1.7% | -72.2% | +102.1% | 20 | 7 | 35 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 481.3s |
| **Latency** (scan→final max) | 671.0s |
| **Traffic** (notifications 24h) | 87 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 402 | 0.4778 | 0.2711 | +0.2067 | 🟡+43% | 0.2458 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 169 | 0.4460 | 0.2308 | 0.2353 | 🔴-0.33 | 0.699 |
| S01_NAKAANA1 | win | 152 | 0.4873 | 0.2237 | 0.2500 | 🔴-0.44 | 0.666 |
| S02_TETSUBAN | win | 81 | 0.5265 | 0.4444 | 0.2600 | 🔴-0.05 | 0.825 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 153 | 0.4147 | 0.2418 | 🔴+0.1729 |
| 0.50+ | 232 | 0.5447 | 0.2974 | 🔴+0.2473 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 156 | 0.782 |
| win | <5.0 | ✅learned | 269 | 0.757 |
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
_auto-generated by claude_snapshot.py at 2026-09-26T12:10:01.632381+09:00_