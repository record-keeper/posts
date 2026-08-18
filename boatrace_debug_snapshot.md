# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-18T12:30:02.409221+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×53 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×53 (24h)
- 🟡 FINAL_MISSING×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×54  [2026-08-18T12:02:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×81  [2026-08-18T12:02:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×27  [2026-08-18T12:02:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-18T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-18T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-18T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×1  [2026-08-18T11:59:37]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-08-18T11:50:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×13  [2026-08-18T11:49:38]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=74<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-18T06:00:19]
- key: `ORPHAN_SCAN|205 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=9 pred=0.1189 actual=0.1111 gap=+0.0078`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-18T06:00:19]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=12 pred=0.1827 actual=0.0833 gap=+0.0994`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S00: n=166 hit%=22.9% hit_CI[Bonf]=[14.9,33.5]% ROI=0.64 ROI_boot95=[0.43,0.86]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S01_NAKAANA1: n=172 hit%=22.7% hit_CI[Bonf]=[14.8,33.0]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-18T06:00:19]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=172<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-18T06:00:19]
- key: `ROI_STAT|S02_TETSUBAN: n=74 hit%=47.3% hit_CI[Bonf]=[31.7,63.5]% ROI=0.73 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift ≤-30%: n=36 hit%=22.2% ROI=0.65 (コスト 10,400/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-18T06:00:19]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=35.3% ROI=1.08 (コスト 8,100/回収 8,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.81MB / last modified 2026-08-18T12:30:05.476819+09:00

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
sed
2026-08-18 12:28:19,033 [INFO] scraper: fetch_race 05/3: boats=6 odds=189/191
2026-08-18 12:28:19,037 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 12:28:19,037 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-08-18 12:28:19,041 [INFO] run_cycle: fetched 05/3 [final]: 154 combos
2026-08-18 12:28:19,374 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-18 12:29:03,903 [INFO] run_cycle: === run_cycle 12:29:03 ===
2026-08-18 12:29:03,903 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-18 12:29:03,903 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-18 12:29:03,940 [INFO] predictor: Models loaded OK
2026-08-18 12:29:16,331 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 12:29:17,398 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 12:29:18,492 [INFO] scraper: odds2t: 30/30 parsed
2026-08-18 12:29:18,493 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 12:29:19,566 [INFO] scraper: odds_win: 5/6 parsed
2026-08-18 12:29:19,566 [INFO] scraper: fetch_race 05/3: boats=6 odds=190/191
2026-08-18 12:29:19,573 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 12:29:19,573 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-18 12:29:19,577 [INFO] run_cycle: fetched 05/3 [final]: 155 combos
2026-08-18 12:29:23,260 [INFO] scraper: odds3t: 120/120 parsed
2026-08-18 12:29:24,365 [INFO] scraper: odds3f: 20/20 parsed
2026-08-18 12:29:25,444 [INFO] scraper: odds2t: 30/30 parsed
2026-08-18 12:29:25,445 [INFO] scraper: odds2f: 15/15 parsed
2026-08-18 12:29:26,520 [INFO] scraper: odds_win: 6/6 parsed
2026-08-18 12:29:26,520 [INFO] scraper: fetch_race 16/5: boats=6 odds=191/191
2026-08-18 12:29:26,523 [INFO] predictor: CALIBRATION_MODE=on
2026-08-18 12:29:26,523 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-18 12:29:26,526 [INFO] run_cycle: fetched 16/5 [scan]: 156 combos
2026-08-18 12:29:26,662 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 92
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 92
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 21, 'scan': 33}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 148
  CIRCUIT_BREAKER_TRIP: 53
  CIRCUIT_BREAKER_NO_ACTION: 51
  ANOMALY_SCAN_FINAL_RATIO: 32
  FINAL_MISSING: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_SPIKE: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 44 | 10 | 13,200 | 8,670 | -4,530 | 0.657 |
| S01_NAKAANA1 | 47 | 11 | 9,400 | 7,020 | -2,380 | 0.747 |
| S02_TETSUBAN | 23 | 9 | 4,600 | 2,640 | -1,960 | 0.574 |

## 直近アラート (24h・新しい順)
```
[12:24:25] CIRCUIT_BREAKER_TRIP: {"cost": 4600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 23, "payout": 2640, "roi_7d": 0.574, "sid": "S02_TETSUBAN"}
[12:24:25] FINAL_MISSING: {"deadline": "2026-08-18T10:54:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081814061054", "sid": "S00"}
[12:21:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1155}
[12:20:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1139}
[12:19:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1140}
[12:18:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1127}
[12:15:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1148}
[12:12:51] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1135}
[12:11:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 4, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1138}
[12:10:38] FINAL_MISSING: {"deadline": "2026-08-18T11:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081816031140", "sid": "S00"}
```

## 本日残レース: 94件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 50件 締切済
- 通知発射: scan=10 nid / final=11 nid / result=5 nid
- predictions: 9 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 109R | win | 1 | 0.4019 | 3.8 | 1.53 | 200 | scan=- drift=- | 12:22:19 |
| S01_NAKAANA1 | 052R | win | 1 | 0.4989 | 3.0 | 1.50 | 200 | scan=3.0 drift=+0.0% | 12:02:19 |
| S01_NAKAANA1 | 114R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 11:59:20 |
| S00 | 114R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.5 drift=+0.0% | 11:59:18 |
| S01_NAKAANA1 | 051R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.5 drift=+31.4% | 11:30:21 |
| S00 | 147R | win | 1 | 0.5174 | 7.0 | 3.62 | 300 | scan=8.2 drift=-14.6% | 11:24:18 |
| S01_NAKAANA1 | 162R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 11:07:18 |
| S00 | 131R | win | 1 | 0.4111 | 4.2 | 1.73 | 300 | scan=- drift=- | 10:34:19 |
| S00 | 143R | win | 1 | 0.3177 | 4.7 | 1.49 | 300 | scan=- drift=- | 09:29:20 |
| S02_TETSUBAN | 2011R | win | 1 | 0.5735 | 2.5 | 1.43 | 200 | scan=- drift=- | 20:13:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 70 | +4.9% | -62.9% | +207.5% | 17 | 7 | 34 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 516.5s |
| **Latency** (scan→final max) | 602.3s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 409 | 0.4670 | 0.2738 | +0.1932 | 🟡+41% | 0.2371 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4168 | 0.2349 | 0.2208 | 🔴-0.23 | 0.678 |
| S01_NAKAANA1 | win | 171 | 0.4886 | 0.2222 | 0.2494 | 🔴-0.44 | 0.719 |
| S02_TETSUBAN | win | 72 | 0.5316 | 0.4861 | 0.2454 | ✅+0.02 | 0.751 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 9 | 0.1189 | 0.1111 | ✅+0.0078 |
| 0.15-0.20 | 11 | 0.1843 | 0.0909 | 🔴+0.0934 |
| 0.20-0.30 | 8 | 0.2246 | 0.3750 | 🔴-0.1504 |
| 0.30-0.50 | 153 | 0.4145 | 0.2288 | 🔴+0.1858 |
| 0.50+ | 226 | 0.5422 | 0.3186 | 🔴+0.2236 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 112 | 0.765 |
| win | <5.0 | ✅learned | 193 | 0.735 |
| win | <10.0 | ✅learned | 97 | 0.447 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 7 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-18T12:30:02.409221+09:00_