# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-27T16:00:02.164803+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×19 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×69 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×8  [2026-08-27T15:56:27]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-27T15:30:07]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×159  [2026-08-27T15:05:23]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×53  [2026-08-27T15:05:23]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-27T15:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-27T15:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×25  [2026-08-27T14:13:52]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-08-27T11:03:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×29  [2026-08-27T10:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-27T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=18.9% ROI=0.60 (コスト 10,700/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3201 actual=0.3429 gap=-0.0228`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S00: n=166 hit%=27.1% hit_CI[Bonf]=[18.4,38.0]% ROI=0.86 ROI_boot95=[0.59,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=189 hit%=25.9% hit_CI[Bonf]=[17.9,36.0]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=42.0% hit_CI[Bonf]=[27.6,57.8]% ROI=0.69 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-27T06:00:10]
- key: `ORPHAN_SCAN|197 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.63MB / last modified 2026-08-27T15:59:37.439321+09:00

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
15:58:19,248 [INFO] run_cycle: fetched 07/3 [scan]: 153 combos
2026-08-27 15:58:19,349 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 15:59:04,123 [INFO] run_cycle: === run_cycle 15:59:04 ===
2026-08-27 15:59:04,123 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 15:59:04,123 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 15:59:04,166 [INFO] predictor: Models loaded OK
2026-08-27 15:59:15,204 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=11&hd=20260827: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-27 15:59:26,760 [INFO] scraper: odds3t: 120/120 parsed
2026-08-27 15:59:27,885 [INFO] scraper: odds3f: 20/20 parsed
2026-08-27 15:59:29,012 [INFO] scraper: odds2t: 30/30 parsed
2026-08-27 15:59:29,013 [INFO] scraper: odds2f: 13/15 parsed
2026-08-27 15:59:30,099 [INFO] scraper: odds_win: 6/6 parsed
2026-08-27 15:59:30,099 [INFO] scraper: fetch_race 11/12: boats=6 odds=189/191
2026-08-27 15:59:30,103 [INFO] predictor: CALIBRATION_MODE=on
2026-08-27 15:59:30,103 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-27 15:59:30,107 [INFO] run_cycle: fetched 11/12 [scan]: 156 combos
2026-08-27 15:59:33,731 [INFO] scraper: odds3t: 120/120 parsed
2026-08-27 15:59:34,805 [INFO] scraper: odds3f: 20/20 parsed
2026-08-27 15:59:35,898 [INFO] scraper: odds2t: 29/30 parsed
2026-08-27 15:59:35,899 [INFO] scraper: odds2f: 14/15 parsed
2026-08-27 15:59:36,987 [INFO] scraper: odds_win: 4/6 parsed
2026-08-27 15:59:36,988 [INFO] scraper: fetch_race 15/3: boats=6 odds=187/191
2026-08-27 15:59:36,991 [INFO] predictor: CALIBRATION_MODE=on
2026-08-27 15:59:36,991 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-08-27 15:59:36,996 [INFO] run_cycle: fetched 15/3 [scan]: 153 combos
2026-08-27 15:59:37,218 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 79
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 79
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 20, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 96
  FINAL_MISSING: 69
  CIRCUIT_BREAKER_NO_ACTION: 26
  ANOMALY_SCAN_FINAL_RATIO: 22
  CIRCUIT_BREAKER_TRIP: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 10 | 12,900 | 8,310 | -4,590 | 0.644 |
| S01_NAKAANA1 | 53 | 14 | 10,600 | 6,780 | -3,820 | 0.64 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 2,420 | -980 | 0.712 |

## 直近アラート (24h・新しい順)
```
[15:56:26] FINAL_MISSING: {"deadline": "2026-08-27T11:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082709031124", "sid": "S00"}
[15:56:26] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:55:43] FINAL_MISSING: {"deadline": "2026-08-27T10:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082714051021", "sid": "S00"}
[15:48:19] FINAL_MISSING: {"deadline": "2026-08-27T13:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082704041316", "sid": "S00"}
[15:47:19] CIRCUIT_BREAKER_TRIP: {"cost": 10600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 6780, "roi_7d": 0.64, "sid": "S01_NAKAANA1"}
[15:42:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[15:31:09] FINAL_MISSING: {"deadline": "2026-08-27T10:58:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082709021058", "sid": "S00"}
[15:28:20] CIRCUIT_BREAKER_TRIP: {"cost": 10400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 52, "payout": 6580, "roi_7d": 0.633, "sid": "S01_NAKAANA1"}
[15:24:06] CIRCUIT_BREAKER_TRIP: {"cost": 10600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 53, "payout": 6580, "roi_7d": 0.621, "sid": "S01_NAKAANA1"}
[15:19:19] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 8310, "roi_7d": 0.644, "sid": "S00"}
```

## 本日残レース: 42件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 114件 締切済
- 通知発射: scan=19 nid / final=21 nid / result=17 nid
- predictions: 18 / うち結果DB記録済: 17
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 228R | win | 1 | 0.5334 | 3.5 | 1.87 | 200 | scan=- drift=- | 15:46:18 |
| S01_NAKAANA1 | 071R | win | 1 | 0.5476 | 4.6 | 2.52 | 200 | scan=3.0 drift=+53.3% | 15:17:19 |
| S01_NAKAANA1 | 227R | win | 1 | 0.5891 | 3.7 | 2.18 | 200 | scan=3.0 drift=+23.3% | 15:13:20 |
| S02_TETSUBAN | 0910R | win | 1 | 0.5990 | 2.0 | 1.20 | 200 | scan=- drift=- | 15:01:18 |
| S00 | 179R | win | 1 | 0.5174 | 11.5 | 5.95 | 300 | scan=25.5 drift=-54.9% | 14:51:18 |
| S00 | 178R | win | 1 | 0.4989 | 6.0 | 2.99 | 300 | scan=18.0 drift=-66.7% | 14:23:30 |
| S00 | 118R | win | 1 | 0.4111 | 5.3 | 2.18 | 300 | scan=- drift=- | 13:58:20 |
| S00 | 1411R | win | 1 | 0.5719 | 4.0 | 2.29 | 300 | scan=4.5 drift=-11.1% | 13:30:25 |
| S00 | 117R | win | 1 | 0.1720 | 11.2 | 1.93 | 300 | scan=- drift=- | 13:23:20 |
| S00 | 097R | win | 1 | 0.4111 | 6.6 | 2.71 | 300 | scan=10.8 drift=-38.9% | 13:20:55 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 61 | +2.0% | -79.6% | +320.7% | 23 | 11 | 47 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.3s |
| **Latency** (scan→final max) | 615.9s |
| **Traffic** (notifications 24h) | 79 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,700円 used |
| **Saturation** (S01_NAKAANA1) | 1,600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 442 | 0.4705 | 0.2873 | +0.1832 | 🟡+39% | 0.2389 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4174 | 0.2701 | 0.2198 | 🔴-0.12 | 0.844 |
| S01_NAKAANA1 | win | 191 | 0.4893 | 0.2565 | 0.2489 | 🔴-0.30 | 0.799 |
| S02_TETSUBAN | win | 77 | 0.5441 | 0.4026 | 0.2575 | 🔴-0.07 | 0.66 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 11 | 0.1807 | 0.1818 | ✅-0.0012 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 158 | 0.4137 | 0.2342 | 🔴+0.1795 |
| 0.50+ | 251 | 0.5457 | 0.3347 | 🔴+0.2110 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 120 | 0.775 |
| win | <5.0 | ✅learned | 223 | 0.746 |
| win | <10.0 | ✅learned | 106 | 0.454 |
| win | <20.0 | ✅learned | 30 | 0.227 |
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
_auto-generated by claude_snapshot.py at 2026-08-27T16:00:02.164803+09:00_