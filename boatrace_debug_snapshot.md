# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-08T15:50:02.082550+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×46 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×46 (24h)
- 🟡 FINAL_MISSING×32 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-08T15:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-08T15:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-08-08T15:28:01]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-08-08T15:20:45]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CIRCUIT_BREAKER_TRIP  ×94  [2026-08-08T15:03:38]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×94  [2026-08-08T15:03:38]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-08-08T15:03:38]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×27  [2026-08-08T12:23:33]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×12  [2026-08-08T11:00:23]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-08T06:00:29]
- key: `ORPHAN_SCAN|171 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-08T06:00:29]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=10 pred=0.1823 actual=0.2000 gap=-0.0177`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=20.0% ROI=0.61 (コスト 10,300/回収 6,270)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S00: n=176 hit%=24.4% hit_CI[Bonf]=[16.4,34.8]% ROI=0.70 ROI_boot95=[0.50,0.94]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=24.8% hit_CI[Bonf]=[16.4,35.7]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-08T06:00:29]
- key: `ROI_STAT|S02_TETSUBAN: n=63 hit%=50.8% hit_CI[Bonf]=[33.6,67.8]% ROI=1.00 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-08T06:00:29]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=63<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=36.1% ROI=0.90 (コスト 9,000/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-08T06:00:29]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=62 hit%=29.0% ROI=0.75 (コスト 14,700/回収 11,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 9.71MB / last modified 2026-08-08T15:49:45.367385+09:00

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
260808: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-08 15:49:27,620 [INFO] scraper: odds3t: 120/120 parsed
2026-08-08 15:49:28,718 [INFO] scraper: odds3f: 20/20 parsed
2026-08-08 15:49:29,815 [INFO] scraper: odds2t: 30/30 parsed
2026-08-08 15:49:29,816 [INFO] scraper: odds2f: 15/15 parsed
2026-08-08 15:49:30,909 [INFO] scraper: odds_win: 6/6 parsed
2026-08-08 15:49:30,909 [INFO] scraper: fetch_race 18/11: boats=6 odds=191/191
2026-08-08 15:49:30,912 [INFO] predictor: CALIBRATION_MODE=on
2026-08-08 15:49:30,912 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-08 15:49:30,916 [INFO] run_cycle: fetched 18/11 [final]: 156 combos
2026-08-08 15:49:34,678 [INFO] scraper: odds3t: 120/120 parsed
2026-08-08 15:49:35,777 [INFO] scraper: odds3f: 20/20 parsed
2026-08-08 15:49:36,884 [INFO] scraper: odds2t: 30/30 parsed
2026-08-08 15:49:36,885 [INFO] scraper: odds2f: 15/15 parsed
2026-08-08 15:49:37,964 [INFO] scraper: odds_win: 5/6 parsed
2026-08-08 15:49:37,964 [INFO] scraper: fetch_race 02/11: boats=6 odds=190/191
2026-08-08 15:49:37,967 [INFO] predictor: CALIBRATION_MODE=on
2026-08-08 15:49:37,967 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-08 15:49:37,971 [INFO] run_cycle: fetched 02/11 [scan]: 155 combos
2026-08-08 15:49:41,793 [INFO] scraper: odds3t: 120/120 parsed
2026-08-08 15:49:42,898 [INFO] scraper: odds3f: 20/20 parsed
2026-08-08 15:49:43,984 [INFO] scraper: odds2t: 30/30 parsed
2026-08-08 15:49:43,986 [INFO] scraper: odds2f: 15/15 parsed
2026-08-08 15:49:45,075 [INFO] scraper: odds_win: 5/6 parsed
2026-08-08 15:49:45,075 [INFO] scraper: fetch_race 17/11: boats=6 odds=190/191
2026-08-08 15:49:45,077 [INFO] predictor: CALIBRATION_MODE=on
2026-08-08 15:49:45,077 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-08 15:49:45,081 [INFO] run_cycle: fetched 17/11 [scan]: 155 combos
2026-08-08 15:49:45,190 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 55
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 55
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 14, 'scan': 19}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 149
  PSI_DRIFT_DETECTED: 46
  CIRCUIT_BREAKER_NO_ACTION: 34
  FINAL_MISSING: 32
  CIRCUIT_BREAKER_TRIP: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_DROP: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 27 | 5 | 8,100 | 4,170 | -3,930 | 0.515 |
| S01_NAKAANA1 | 34 | 7 | 6,800 | 3,720 | -3,080 | 0.547 |
| S02_TETSUBAN | 11 | 7 | 2,200 | 2,260 | +60 | 1.027 |

## 直近アラート (24h・新しい順)
```
[15:46:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 327, "n_recent": 72, "psi": 0.254}
[15:46:26] FINAL_MISSING: {"deadline": "2026-08-08T13:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080802061314", "sid": "S00"}
[15:46:26] FINAL_MISSING: {"deadline": "2026-08-08T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026080802041214", "sid": "S00"}
[15:46:26] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1246}
[15:45:03] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1263}
[15:44:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1258}
[15:43:43] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1231}
[15:42:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1232}
[15:41:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1220}
[15:40:58] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1213}
```

## 本日残レース: 67件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 101件 締切済
- 通知発射: scan=12 nid / final=13 nid / result=8 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 202R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 15:46:18 |
| S02_TETSUBAN | 201R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=- drift=- | 15:22:29 |
| S01_NAKAANA1 | 168R | win | 1 | 0.5174 | 3.2 | 1.66 | 200 | scan=3.8 drift=-15.8% | 14:20:19 |
| S01_NAKAANA1 | 044R | win | 1 | 0.3177 | 3.5 | 1.11 | 200 | scan=3.1 drift=+12.9% | 13:21:18 |
| S02_TETSUBAN | 166R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 13:19:30 |
| S00 | 025R | win | 1 | 0.5174 | 5.0 | 2.59 | 300 | scan=4.3 drift=+16.3% | 12:41:18 |
| S01_NAKAANA1 | 024R | win | 1 | 0.4111 | 4.2 | 1.73 | 200 | scan=- drift=- | 12:11:44 |
| S02_TETSUBAN | 163R | win | 1 | 0.5891 | 2.8 | 1.65 | 200 | scan=- drift=- | 11:47:18 |
| S00 | 162R | win | 1 | 0.4989 | 10.5 | 5.24 | 300 | scan=- drift=- | 11:12:19 |
| S00 | 021R | win | 1 | 0.5174 | 5.5 | 2.85 | 300 | scan=4.5 drift=+22.2% | 10:44:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | -0.9% | -73.3% | +112.5% | 14 | 7 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 344.3s |
| **Latency** (scan→final max) | 592.3s |
| **Traffic** (notifications 24h) | 55 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 397 | 0.4587 | 0.2897 | +0.1690 | 🟡+37% | 0.2347 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4111 | 0.2471 | 0.2220 | 🔴-0.19 | 0.707 |
| S01_NAKAANA1 | win | 159 | 0.4828 | 0.2453 | 0.2448 | 🔴-0.32 | 0.731 |
| S02_TETSUBAN | win | 64 | 0.5282 | 0.5156 | 0.2445 | ✅+0.02 | 0.995 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 12 | 0.1229 | 0.1667 | ✅-0.0438 |
| 0.15-0.20 | 10 | 0.1823 | 0.2000 | ✅-0.0177 |
| 0.20-0.30 | 11 | 0.2237 | 0.3636 | 🔴-0.1399 |
| 0.30-0.50 | 152 | 0.4158 | 0.2171 | 🔴+0.1987 |
| 0.50+ | 209 | 0.5401 | 0.3541 | 🔴+0.1860 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 98 | 0.788 |
| win | <5.0 | ✅learned | 174 | 0.723 |
| win | <10.0 | ✅learned | 88 | 0.449 |
| win | <20.0 | ✅learned | 29 | 0.228 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-08T15:50:02.082550+09:00_